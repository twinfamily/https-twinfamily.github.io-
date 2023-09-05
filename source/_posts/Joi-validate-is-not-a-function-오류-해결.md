title: Joi.validate is not a function 오류 해결
author: Daehan Kang
tags:
  - error
categories:
  - error
date: 2023-09-04 23:58:00
subTitle:
---
출간된지 오래된 책들을 보면
```
const result = Joi.validate(body, schema);
```
Joi를 이런 방식의 문법으로 안내하고 있다.

하지만 바뀌었는지 계속 Joi.validate is not a function 이란 오류만 내고 있다.
새로운 문법으로 바뀐것 같아서 API 제공 문서를 보니 버전이 업데이트 되면서 변경 되었다고 한다.

관련 API 문서 (https://joi.dev/api/?v=17.9.1)

```
const validation = schema.validate(body);
```
이런식으로 schema에 validate함수를 실행하고, 인자로 body를 넣는다.
항상 사용하고 있는 라이브러리나 프레임워크의 버전 업데이트를 확인 해보자.
이것 때문에 몇시간을 허비했는데 허무하다.

