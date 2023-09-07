title: Javascript - generator
author: Daehan Kang
tags:
  - javascript
categories:
  - javascript
date: 2023-09-08 01:42:00
subTitle:
---
비동기 코드 문제를 다루는 방법으로 프로미스를 대신해서 사용 가능한 ES6 명세에 포함된 문법이다.

```
//제너레이터 생성 함수 바로 뒤에 *를 붙인다.
function* gen(){
	return 'first';
}
```
<br>

제너레이터의 값을 가져오는 방법으로는
```
//.next() 함수로 상태를 호출가능
let generatorResult = gen();

generatorResult.next().value
// >'first'

generatorResult.next().value
// >undifind
```
<br>
next 함수를 사용하여 값을 호출 시에는 재사용이 불가능하여 한번만 호출하여 사용 가능하고 재호출하면 해당 값은 비어있는 상태가 되기 때문에 undifined가 반환된다.

이를 해결하기 위해서,
yield 키워드라는 제너레이터 함수의 키워드를 사용한다.
yield 키워드는 함수를 정지모드로 하며 값을 반환한다. 정지된 곳에서 다시 yield 키워드를 사용하여 다음 라인의 값을 반환 할 수 있다.

```
function* generatorSequence() {
  yield 'first';
  yield 'second';
  yield 'third';
}

let generatorSequenceResult = generatorSequence();

console.log('First time sequence value',generatorSequenceResult.next().value)
console.log('Second time sequence value',generatorSequenceResult.next().value)
console.log('thrid time sequence value',generatorSequenceResult.next().value)

// >First time sequence value
// >Second time sequence value
// >thrid time sequence value
```
<br>

#### 제너레이터의 done 속성

제너레이터 next 호출 할 때마다 객체에 done 속성으로 next의 값이 전부 사용 됐는지 확인 할수 있다.

```
//next 함수 호출 시 다음과 같은 객체를 반환한다.
{value: 'value', done: false}

let generatorSequenceResult = generatorSequence();

console.log('First time sequence value',generatorSequenceResult.next())
console.log('Second time sequence value',generatorSequenceResult.next())
console.log('thrid time sequence value',generatorSequenceResult.next())

// >First time sequence value {value: 'first', done: false}
// >Second time sequence value {value: 'second', done: false}
// >thrid time sequence value {value: 'thrid', done: false}

console.log('재호출하면... ',generatorSequenceResult.next())
// >'재호출하면... ' {value: undifined, done: true}
```

제너레이터의 값을 모두 사용했음을 done을 통해 확인 가능하다.
