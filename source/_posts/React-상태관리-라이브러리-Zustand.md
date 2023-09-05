title: React 상태관리 라이브러리 - Zustand
author: Daehan Kang
tags:
  - React
categories:
  - React
date: 2023-09-05 00:08:00
subTitle:
---
Redux가 아직까지 많이 사용되고 있지만 Redux를 대체하고 여러 상태관리 라이브러리들을 적용하는 분명한 단점도 존재합니다.
그것은 바로 보일러플레이트 코드 때문입니다. 이것을 극복하고 최소한의 코드로 상태 관리 하는 방법을 찾아보게 되었는데 그것은 바로 Zustand입니다.

Zustand의 사용법에 대해서 간단히 알아보기 위해서 포스팅 합니다.
Jotai를 만든 개발진들이 Zustand도 만든 것으로 알려져 있습니다.
Zustand가 가진 아주 강력한 장점은 굉장히 쉽다는 것입니다. 보일러플레이트가 거의 없다 싶을 정도로 간단한 코드만 필요로 하고요. 아주 쉽게 연결할 수 있습니다. 또한 Redux Devtools를 사용할 수 있어서 Debugging을 하는데도 아주 용이합니다.
<br>
### Zustand 사용법
<br>
1. Zustand 설치

```
npm i zustand # or yarn add zustand
```
<br>
2. store 생성

```
// store.js

import create from 'zustand' // create로 zustand를 불러옵니다.

const useStore = create(set => ({
  bears: 0,
  increasePopulation: () => set(state => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 })
}))

export default useStore
```
bears 라는 초기값을 선언한다.
그 값을 조작하는 increasePopulation(bears를 1씩 증가)과 removeAllBears(bears를 0으로 리셋)를 선언합니다. 이때는 set을 활용합니다.
<br>
3. store에 생성한 useStore를 불러와서 사용하기

```
// App.js

import useStore from '../store.js'

const App = () => {
  const { bears, increasePopulation, removeAllBears } = useStore(state => state)
  
  return (
    <>
      <h1>{bears} around here ...</h1>
      <button onClick={increasePopulation}>one up</button>
      <button onClick={removeAllBears}>remove all</button>
    </>
  )
}
```
store에 선언한 값과 메서드를 useStore를 통해 불러와서 아주 간단하게 사용할 수 있습니다. 코드 작성은 이게 끝이고 이제 devtool 연결을 통한 디버깅 설정을 합니다.
<br>
### Devtools를 통해 상태 Debugging하기
<br>
먼저 Redux DevTools를 Chrome 웹 스토어에서 설치해줍니다.
이후에는 위에 2에서 생성한 store에서 devtools를 불러온 후에 연결을 해줍니다. 그리고 현재 내가 작업하고 있는 애플리케이션을 브라우저로 띄운 다음 개발자 도구 창에서 Redux DevTools를 확인해보세요. store의 상태를 확인하실 수 있을 것입니다.

```
// store.js

import create from 'zustand'
import { devtools } from 'zustand/middleware'

const store = (set) => ({
  bears: 0,
  increasePopulation: () => set(state => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 })
})

const useStore = create(devtools(store))

export default useStore
```
<br>

### production일 때와 development일 때 분기처리

```
// store.js

import create from 'zustand'
import { devtools } from 'zustand/middleware'

const store = (set) => ({
  bears: 0,
  increasePopulation: () => set(state => ({ bears: state.bears + 1 })),
  removeAllBears: () => set({ bears: 0 })
})

const useStore = create(
  process.env.NODE_ENV !== 'production' ? devtools(store) : store
)

export default useStore
```

개발환경에서는 상태를 Debugging하고 실제 배포시에는 분기처리를 통해 설정할 수 있습니다.

[참고자료]
https://github.com/pmndrs/zustand
https://blacklobster.tistory.com/3
