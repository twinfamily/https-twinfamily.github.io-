title: React Clean Code Tip!
author: Daehan Kang
date: 2023-09-04 13:01:25
categories: [React]
tags: [React]
subTitle:
---
1. 단일 조건인 조건부 렌더링에는 && 를 쓰자

만약 어떤 값이 true 일 때 렌더링하고 false일 때는 렌더하지 않는 식으로, 조건에 따라 렌더링을 하거나 하지 않는 경우가 있습니다. 이때는 삼항연산자를 사용하지 말고 대신 &&연산자를 활용하는 것이 좋습니다.

[Bad]
```
import React, { useState } from 'react'

export const ConditionalRenderingWhenTrueBad = () => {
  const [showConditionalText, setShowConditionalText] = useState(false)

  const handleClick = () =>
    setShowConditionalText(showConditionalText => !showConditionalText)

  return (
    <div>
      <button onClick={handleClick}>Toggle the text</button>
	  {/* (역주) 삼항연산자를 사용하면 null 같이 불필요한 코드가 늘어납니다. */} 
      {showConditionalText ? <p>The condition must be true!</p> : null}
    </div>
  )
}
```

[Good]
```
import React, { useState } from 'react'

export const ConditionalRenderingWhenTrueGood = () => {
  const [showConditionalText, setShowConditionalText] = useState(false)

  const handleClick = () =>
    setShowConditionalText(showConditionalText => !showConditionalText)

  return (
    <div>
      <button onClick={handleClick}>Toggle the text</button>
	  {/* (역주) 삼항연산자를 활용하면 조건별 렌더링을 더 가시적으로 표현할 수 있습니다. */}
      {showConditionalText && <p>The condition must be true!</p>}
    </div>
  )
}
```

<br>
<br>
2. 다중 조건인 조건부 렌더링에서는 삼항연산자를 쓰자

만약 어떤 값이 true 일 때 A를 렌더링하고 false일 때는 B를 렌더하지 식으로 조건에 따라 서로 다른 결과를 렌더링해야 하는 경우가 있습니다. 이때는 삼항연산자를 쓰는 것이 좋습니다.

[Bad]
```
import React, { useState } from 'react'

export const ConditionalRenderingBad = () => {
  const [showConditionOneText, setShowConditionOneText] = useState(false)

  const handleClick = () =>
    setShowConditionOneText(showConditionOneText => !showConditionOneText)

  return (
    <div>
      <button onClick={handleClick}>Toggle the text</button>
	{/* (역주) 이 경우 && 연산자를 활용하면 불필요하게 코드가 늘어납니다. */}
      {showConditionOneText && <p>The condition must be true!</p>}
      {!showConditionOneText && <p>The condition must be false!</p>}
    </div>
  )
}
```

[Good]
```
import React, { useState } from 'react'

export const ConditionalRenderingGood = () => {
  const [showConditionOneText, setShowConditionOneText] = useState(false)

  const handleClick = () =>
    setShowConditionOneText(showConditionOneText => !showConditionOneText)

  return (
    <div>
      <button onClick={handleClick}>Toggle the text</button>
	  {/* (역주) 삼항연산자를 활용하면 조건별 렌더링을 더 가시적으로 표현할 수 있습니다. */}
	  {showConditionOneText ? (
        <p>The condition must be true!</p>
        ) : (
        <p>The condition must be false!</p>
        )}
    </div>
  )
}
```
<br>
<br>
3. Boolean값을 Props로 넘길 때는 true를 생략하자

따로 값을 할당하지 않아도 prop명만으로 컴포넌트에 참으로 평가되는 값을 제공할 수 있는 경우가 있습니다. 이런 경우에 해당 prop값으로 true 를 굳이 명시할 필요가 없습니다. 가령 myTruthProp={true} 이런 식으로 작성할 필요는 없다는 뜻입니다.

[Bad]
```
import React from 'react'

const HungryMessage = ({ isHungry }) => (
  <span>{isHungry ? 'I am hungry' : 'I am full'}</span>
)

export const BooleanPropBad = () => (
  <div>
    <span>
      <b>This person is hungry: </b>
    </span>
	{/* (역주) isHungry의 값으로 굳이 true를 명시 */} 
    <HungryMessage isHungry={true} />
    <br />
    <span>
      <b>This person is full: </b>
    </span>
    <HungryMessage isHungry={false} />
  </div>
)
```

[Good]
```
import React from 'react'

const HungryMessage = ({ isHungry }) => (
  <span>{isHungry ? 'I am hungry' : 'I am full'}</span>
)

export const BooleanPropGood = () => (
  <div>
    <span>
      <b>This person is hungry: </b>
    </span>
	{/* (역주) isHungry의 값으로 굳이 true를 명시하지 않아도 됩니다. */}
    <HungryMessage isHungry />
    <br />
    <span>
      <b>This person is full: </b>
    </span>
    <HungryMessage isHungry={false} />
  </div>
)
```
<br>
<br>
4. 문자열 값을 Props로 넘길 때는 쌍따옴표를 이용하자

문자열 Prop값은 별도의 중괄호({}, curly brace)나 백틱(``, backticks)없이 그저 쌍따옴표만을 통해서도 전달할 수 있습니다.

[Bad]
```
import React from 'react'

const Greeting = ({ personName }) => <p>Hi, {personName}!</p>

export const StringPropValuesBad = () => (
  <div>
	{/* (역주) 문자열 prop값을 중괄호, 백틱, 쌍따옴표, 홑따옴표로 감싸 전달한 사례 */}
    <Greeting personName={"John"} />
    <Greeting personName={'Matt'} />
    <Greeting personName={`Paul`} />
  </div>
)
```

[Good]
```
import React from 'react'

const Greeting = ({ personName }) => <p>Hi, {personName}!</p>

export const StringPropValuesGood = () => (
  <div>
  	{/* (역주) 문자열 prop값은 그저 쌍따옴표만으로도 충분히 전달할 수 있습니다. */}
    <Greeting personName="John" />
    <Greeting personName="Matt" />
    <Greeting personName="Paul" />
  </div>
)
```
<br>
<br>
5. 인자가 Event 객체 뿐인 이벤트 핸들러 함수는 함수명만 입력하자.

만약 이벤트 핸들러가 오직 Event 객체 하나만을 인자로 받는다면, 그냥 이벤트 핸들러로 함수명만을 입력하면 됩니다. 즉, onChange={e => handleChange(e)} 이라고 쓸 필요없이 그냥 onChange={handleChange}라고 쓰면 된다는 뜻입니다.

[Bad]
```
import React, { useState } from 'react'

export const UnnecessaryAnonymousFunctionsBad = () => {
  const [inputValue, setInputValue] = useState('')

  const handleChange = e => {
    setInputValue(e.target.value)
  }

  return (
    <>
      <label htmlFor="name">Name: </label>
      {/* (역주) Event 객체 하나만 인자로 받는데 인자를 전달하는 함수형태로 작성 */}
      <input id="name" value={inputValue} onChange={e => handleChange(e)} />
    </>
  )
}
```

[Good]
```
import React, { useState } from 'react'

export const UnnecessaryAnonymousFunctionsGood = () => {
  const [inputValue, setInputValue] = useState('')

  const handleChange = e => {
    setInputValue(e.target.value)
  }

  return (
    <>
      <label htmlFor="name">Name: </label>
      {/* (역주) 그저 Event 객체 하나만 인자로 받는 함수는 함수명만을 입력 */}
      <input id="name" value={inputValue} onChange={handleChange} />
    </>
  )
}
```
<br>
<br>
6. 별도의 props가 없는 컴포넌트 전달할 때는 컴포넌트명만을 입력하자

어떤 컴포넌트(B)에 prop으로 또 다른 컴포넌트(A)를 전달하는 경우에, 전달되는 컴포넌트(A)가 아무 props를 받지 않는다면 굳이 함수로 감쌀 필요없이 컴포넌트명만을 전달해도 좋습니다.

[Bad]
```
import React from 'react'

const CircleIcon = () => (
  <svg height="100" width="100">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
  </svg>
)

const ComponentThatAcceptsAnIcon = ({ IconComponent }) => (
  <div>
    <p>Below is the icon component prop I was given:</p>
    <IconComponent />
  </div>
)

export const UnnecessaryAnonymousFunctionComponentsBad = () => (
  {/* (역주) CircleIcon은 아무런 인자를 받지 않는데도 함수로 감싸서 전달 */}
  <ComponentThatAcceptsAnIcon IconComponent={() => <CircleIcon />} />
)
```

[Good]
```
import React from 'react'

const CircleIcon = () => (
  <svg height="100" width="100">
    <circle cx="50" cy="50" r="40" stroke="black" stroke-width="3" fill="red" />
  </svg>
)

const ComponentThatAcceptsAnIcon = ({ IconComponent }) => (
  <div>
    <p>Below is the icon component prop I was given:</p>
    <IconComponent />
  </div>
)

export const UnnecessaryAnonymousFunctionComponentsGood = () => (
  {/* (역주) 아무런 인자를 받지 않는 CircleIcon를 함수로 싸지 않고 컴포넌트명으로 전달 */}
  <ComponentThatAcceptsAnIcon IconComponent={CircleIcon} />
)
```
<br>
<br>
7. Undefined Props

undefined props는 제외됩니다. 만약 어떤 props가 undefined로 제공되어도 컴포넌트 작동에 문제가 없다면, props값으로 undefined를 전달하는 것에 대한 대비책을 걱정할 필요는 없습니다.

[Bad]
```
import React from 'react'

const ButtonOne = ({ handleClick }) => (
  <button onClick={handleClick || undefined}>Click me</button>
)

const ButtonTwo = ({ handleClick }) => {
  const noop = () => {}

  return <button onClick={handleClick || noop}>Click me</button>
}

export const UndefinedPropsBad = () => (
  <div>
    <ButtonOne />
    <ButtonOne handleClick={() => alert('Clicked!')} />
    <ButtonTwo />
    <ButtonTwo handleClick={() => alert('Clicked!')} />
  </div>
)
```

[Good]
```
import React from 'react'

const ButtonOne = ({ handleClick }) => (
  <button onClick={handleClick}>Click me</button>
)

export const UndefinedPropsGood = () => (
  <div>
    <ButtonOne />
    <ButtonOne handleClick={() => alert('Clicked!')} />
  </div>
)
```
<br>
<br>
8. 이전 상태에 의존하는 상태를 갱신할 때는 updater 함수를 전달하자

만약 새로운 상태가 이전의 상태값에 의존한다면, 이전 state값을 이용한 함수(updater 함수)를 전달해야 합니다. React 상태 갱신은 일괄적으로 이뤄지므로 이런 식으로 갱신하지 않으면 예상치 못한 결과가 나올 수 있습니다.

[Bad]
```
import React, { useState } from 'react'

export const PreviousStateBad = () => {
  const [isDisabled, setIsDisabled] = useState(false)
  
  // (역주) 이전 값에 의존하는 상태갱신 함수에 갱신결과값만을 전달하면
  const toggleButton = () => setIsDisabled(!isDisabled)
  
  // (역주) 이 함수의 결과가 정상적으로 작동하지 않음을 알 수 있습니다.
  const toggleButton2Times = () => {
    for (let i = 0; i < 2; i++) {
      toggleButton()
    }
  }

  return (
    <div>
      <button disabled={isDisabled}>
        I'm {isDisabled ? 'disabled' : 'enabled'}
      </button>
      <button onClick={toggleButton}>Toggle button state</button>
      <button onClick={toggleButton2Times}>Toggle button state 2 times</button>
    </div>
  )
}
```

[Good]
```
import React, { useState } from 'react'

export const PreviousStateGood = () => {
  const [isDisabled, setIsDisabled] = useState(false)

  // (역주) 상태갱신 함수의 인자로 이전 값을 인자로 하는 updater 함수를 전달하면
  const toggleButton = () => setIsDisabled(isDisabled => !isDisabled)

  // (역주) 아래 함수가 의도한대로 동작함을 알 수 있습니다.
  const toggleButton2Times = () => {
    for (let i = 0; i < 2; i++) {
      toggleButton()
    }
  }

  return (
    <div>
      <button disabled={isDisabled}>
        I'm {isDisabled ? 'disabled' : 'enabled'}
      </button>
      <button onClick={toggleButton}>Toggle button state</button>
      <button onClick={toggleButton2Times}>Toggle button state 2 times</button>
    </div>
  )
}
```
<br>
<br>
✓ Honorable Mentions 언급하진 않았지만 중요한 것들

아래 내용은 React의 필수법칙은 아니지만 클린코드를 짜는 좋은 방법이 될 것입니다. 해당 문제에 대해서는 자바스크립트 뿐만 아니라 어떤 프로그래밍 언어에서든지 말입니다.

- 복잡한 로직을 명확한 이름의 함수로 뽑아내라.
- 매직넘버는 상수로 뽑아내라.
- 명확한 이름의 변수를 사용해라

<br>
<br>
[출처]
<br>
https://one-it.tistory.com/entry/%EB%B2%88%EC%97%AD-React-Clean-Code%EB%A5%BC-%EC%9C%84%ED%95%9C-%ED%8C%81
<br>
[관련 원문]
<br>
https://betterprogramming.pub/8-ways-to-write-clean-react-code-610c502ccf39