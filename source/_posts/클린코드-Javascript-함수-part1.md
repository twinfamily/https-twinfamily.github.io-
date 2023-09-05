title: '클린코드 - Javascript 함수 [part1]'
author: Daehan Kang
tags:
  - javascript
categories:
  - javascript
date: 2023-09-05 15:35:00
subTitle:
---
### 1. 함수의 복잡한 인자 관리하기

udemy 강의 중 클린코드 자바스크립트를 듣고 정리한 내용입니다.

```
//함수 파라미터에 객체분해 할당으로 값을 넘기는 방법
//es2015+ 이후에는 객체분해 할당으로 파라미터에 선언 가능하다
//필수로 입력값을 지정 할 경우 객체분해 할당에서 빼고 바로 파라미터에 넣을 수 있게 함
function createCar(name, {brand,color,type}) {
	return {
		name,
		brand,
		color,
		type
	};
}

//인자 값이 없을 경우 에러 처리 예시
function createCar(name, {brand,color,type}) {
	if(!name) {
		throw new Error('name is a required');
	}

	if(!brand) {
		throw new Error('brand is a required');
	}
}
```
return으로 바로 값을 넘겨 받을 수 있고 순서에 영향을 받지 않는다.
<br>

### 2. 함수의 default value 정의

```
const required = (argName) => {
	throw new Error('required is ' + argName);
}

//값이 없을 경우 해당 에러 표시
function createCar({
	name = required('name'),
	brand = required('brand'),
	color = required('color'),
	type = false,
} = {}){
	return {
		brand,
		color,
		type
	};
} 
```
