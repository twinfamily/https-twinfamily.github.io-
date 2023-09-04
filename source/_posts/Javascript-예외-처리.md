title: Javascript 예외 처리
author: Daehan Kang
tags:
  - javascript
categories:
  - javascript
date: 2023-09-04 14:47:00
subTitle:
---
1. try ~ catch 처리

throw 키워드 : 예외를 발생시키는 데 사용한다.

예외를 잡아내기 위해서는 try 블록으로 코드를 감싼다음 catch 키워드를 사용한다.
try 블록 안의 코드에서 예외가 발생하면, 예외 값이 바인딩된 괄호 안의 이름(error)을 사용해서 catch 블록이 처리된다.
catch 블록이 완료되거나 try 블록이 문제없이 완료되면 프로그램은 try/catch 문 이후 코드가 진행된다.

[예시]
```
function transfer(from, amount){
	if(accounts[from] < amount) return;
	let progress = 0;
	try {
		accounts[from] -= amount;
		progress = 1;
		accounts[getAccount()] += amount;
		progress = 2;
	} finally {
		if(progress == 1){
			accounts[from] += amount;
		}
	}
}
```

이 함수에서는 이체 진행 상황을 추적하고, 이체가 완료되는 시점에 프로그램 상태가 일치하지 않는 지점에서 중단이 발견되면, 진행된 문제를 복구하는 과정을 나타낸다.
try 블록에서 예외가 발생해서 finally 코드가 실행되더라도 예외 처리는 방해받지 않는다.
finally 블록이 실행된 후, 스택 풀기는 계속 진행된다.

2. 선택적 예외 처리

새로운 오류 클래스를 정의하고 Error를 확장하는 방식으로 예외를 더 정확하게 잡아낼 수 있다.

```
//새로운 빈 오류 클래스를 정의하고 확장함.
class InputError extends Error{}

function promptDirection(question){
	let result = prompt(question);
	if(result.toLowerCase() == "left") return "L";
	if(result.toLowerCase() == "right") return "R";
	throw new InputError("에러 확인: " + result);
}
```

이 클래스는 고유의 생성자를 정의하지 않고 문자열 메세지를 인수로 받는 Error 생성자를 상속한다. 해당 클래스는 아무것도 정의되지 않고 비어있다. InputError 객체는 Error와 다른 클래스로 구별되는 점을 제외하면 Error 객체와 동일하게 작동한다.

```
for(;;){
	try{
		let dir = promptDirection('Where?');
		console.log('You chose', dir);
		break;
	} catch(e) {
		if(e instanceof InputError){
			console.log("Try again");
		} else {
			throw e;
		}
	}
}
```

해당 반복문에서는 InputError의 인스턴스만 잡아내고 관련없는 예외는 통과시키는 과정을 설명한다.
오류 식별에는 instanceof를 사용해서 식별하였다.