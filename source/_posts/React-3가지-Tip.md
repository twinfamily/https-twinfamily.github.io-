title: React 3가지 Tip!
author: Daehan Kang
date: 2023-09-04 12:45:56
categories: [React]
tags: [React]
subTitle:
---
1. React props 간편하게 전달하기

react의 compoent를 생성한 뒤 props를 전달하다 보면 반복된 내용을 쓰게 되는 경우가 많다.

```
const {title, name, contnets} = data;
const onOtherNameFunc = () => alert('Click!');

// bad
<Component title={title} name={name} contents={contents} onClick={onOtherNameFunc} />

// good
<Component {...{title, name, contents}} onClick={onOtherNameFunc} />
```

<br>
<br>
2. Map props 효율적으로 전달하기

map을 사용할 때 하나의 id와 같은 하나의 props를 위해 구조 분해 할당을 하기에는 번거로울 때가 있다.

```
// bad
{list.map((data) => (
  <Components {...data} key={data?.id} />
))}

// good
{list.map(({ id, ...listData }) => (
  <Components {...{ id, ...listData }} key={id} />
))}
```

<br>
<br>
3. 객체나 배열에 조건부 할당하기

객체나 배열을 생성할 때 한 가지 정도가 조건에 따라 할당되거나 변경되는 경우 가 많은데 그 경우 분기를 통해 아예 다시 생성하는 경우가 많다.

```
// bad
let data = {
	id,
	title,
    contents,
};
if(custom) data.type = 'custom'
if(status) data.status = 'good';

// good
const data = {
	id,
	title,
    contents,
  ...(custom && {type : 'custom'}),
  ...(status && { status: 'good' }),
};
```