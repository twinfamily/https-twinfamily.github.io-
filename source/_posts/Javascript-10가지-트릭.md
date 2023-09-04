title: Javascript 10가지 Tip!
author: Daehan Kang
date: 2023-09-04 12:23:48
tags:
  - javascript
subTitle:
---
1. 구조 분해 할당을 이용한 변수 swap
- ES6의 구조 분해 할당 문법을 사용하여 두 변수를 swap 할 수 있다

```jsx
let a = 5, b = 10;
[a.b] = [b,a];
console.log(a,b); // 10, 5
```
<br>
2. 배열 생성으로 루프 제거하기
- 보통 단순히 범위 루프를 돌고 싶다면 다음과 같이 코드를 작성한다.

```jsx
let sum = 0;
for (let i = 5; i < 10; i += 1) {
    sum += i;
}
```

- 만약 범위 루프를 함수형 프로그래밍 방식으로 사용하고 싶다면 배열을 생성해서 사용할 수 있다.

```jsx
const sum = Array
    .from(new Array(5), (_, k) => k + 5)
    .reduce((acc, cur) => acc + cur, 0);
```
<br>
3. 배열 내 같은 요소 제거하기
- `Set`을 이용할 수 있습니다.

```jsx
const names = ['Lee', 'Kim', 'Park', 'Lee', 'Kim'];
const uniqueNamesWithArrayFrom = Array.from(new Set(names));
const uniqueNamesWithSpread = [...new Set(names)];
```
<br>
4. Spread 연산자를 이용한 객체 병합
- 두 객체를 별도 변수에 합쳐줄 수 있다

```jsx
const person = {
    name: 'Lee Sun-Hyoup',
    familyName: 'Lee',
    givenName: 'Sun-Hyoup'
};

const company = {
    name: 'Cobalt. Inc.',
    address: 'Seoul'
};

const leeSunHyoup = { ...person, ...company };
console.log(leeSunHyoup);
// {
//   address: “Seoul”
//     familyName: “Lee”
//   givenName: “Sun-Hyoup”
//   name: "Cobalt. Inc." // 같은 키는 마지막에 대입된 값으로 정해진다.
// }
```
<br>
5. &&와 || 활용
- &&와 ||는 조건문 외에서도 활용될 수 있다

```jsx
/// ||
// 기본값을 넣어주고 싶을 때 사용할 수 있습니다.
// participantName이 0, undefined, 빈 문자열, null일 경우 'Guest'로 할당됩니다.
const name = participantName || 'Guest';

/// &&
// flag가 true일 경우에만 실행됩니다.
flag && func();

// 객체 병합에도 이용할 수 있습니다.
const makeCompany = (showAddress) => {
  return {
    name: 'Cobalt. Inc.',
    ...showAddress && { address: 'Seoul' }
  }
};
console.log(makeCompany(false));
// { name: 'Cobalt. Inc.' }
console.log(makeCompany(true));
// { name: 'Cobalt. Inc.', address: 'Seoul' }
```
<br>
6. 구조 분해 할당 사용하기
- 객체에서 필요한 것만 꺼내 쓰는 것이 좋다.

```jsx
const person = {
    name: 'Lee Sun-Hyoup',
    familyName: 'Lee',
    givenName: 'Sun-Hyoup'
    company: 'Cobalt. Inc.',
    address: 'Seoul',
}

const { familyName, givenName } = person;
```
<br>
7. 객체 생성시 키 생략방법
- 객체를 생성할 때 프로퍼티 키를 변수 이름으로 생략할 수 있다.

```jsx
const name = 'Lee Sun-Hyoup';
const company = 'Cobalt';
const person = {
  name,
  company
}
console.log(person);
// {
//   name: 'Lee Sun-Hyoup'
//   company: 'Cobalt',
// }
```
<br>
8. 비구조화 할당 사용하기
- 함수에 객체를 넘길 경우 필요한 것만 꺼내 쓸 수 있다.

```jsx
const makeCompany = ({ name, address, serviceName }) => {
  return {
    name,
    address,
    serviceName
  }
};
const cobalt = makeCompany({ name: 'Cobalt. Inc.', address: 'Seoul', serviceName: 'Present' });
```
<br>
9. 동적 속성 이름
- ES6에 추가된 기능으로 객체의 키를 동적으로 생성 할 수 있다.

```jsx
const nameKey = 'name';
const emailKey = 'email';
const person = {
  [nameKey]: 'Lee Sun-Hyoup',
  [emailKey]: 'kciter@naver.com'
};
console.log(person);
// {
//   name: 'Lee Sun-Hyoup',
//   email: 'kciter@naver.com'
// }
```
<br>
10. !! 연산자를 사용하여 Boolean 값으로 바꾸기
- !! 연산자를 이용하여 `0, null, 빈 문자열, undefined, NaN`을 `false`로 그 외에는 `true`로 변경할 수 있습니다.