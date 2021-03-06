---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript
- TypeScript에서 프로그램 작성을 위해 기본 제공하는 데이터 타입
- 사용자가 만든 타입은 결국은 이 기본 자료형들로 쪼개진다.
- JavaScript 기본 자료형을 포함
  - ECMAScript 표준에 따른 기본 자료형은 6가지
    - Boolean
    - Number
    - String
    - Null
    - Undefined
    - Symbol(ECMAScript 6에 추가)
    - Array: object 형
  - 프로그래밍을 도울 몇가지 타입이 더 제공된다.
    - Any
    - Void
    - Never
    - Enum
    - Tuple: object 형

### Primitive Type
- 오브젝트와 레퍼런스 형태가 아닌 실제 값을 저장하는 자료형
- 프리미티브 형의 내장 함수를 사용 가능한 것은 자바스크립트 처리 방식 덕분
```JAVASCRIPT
let name = 'mark';
name.toString();
```

### literal ?
- 값자체가 변하지 않는 값을 의미합니다.
- 상수와 다른 것은 상수는 가리키는 포인터가 고정이라는 것이고, 리터럴은 그 자체가 값이자 그릇입니다.
```JAVASCRIPT
35; // number 리터럴
'mark' //string 리터럴
true //boolean 리터럴

//object 리터럴
{
  name: 'mark',
  age: 35
}
```

### Boolean / boolean
- 가장 기본적인 데이터 타입
- 단순한 true 혹은 false 값 입니다.
- JavaScript / TypeScript에서 'boolean'이라고 부른다.

### Number / number
- JavaScript와 같이, TypeScript의 모든 숫자는 부동 소수점 값입니다.
- TypeScript는 16진수 및 10진수 리터럴 외에도, ECMAScript 2015에 도입된 2진수 및 8진수를 지원합니다.
```JAVASCRIPT
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010; 
let octal: number = 0o744;
```

### String / string

### Template String
- 행에 걸쳐 있거나, 표현식을 넣을 수 있는 문자열
- 이 문자열은 backtick (=backquote) 기호에 둘러쌓여 있습니다.
- 포함된 표현식은 `#{expr}`와 같은 형태로 사용합니다.

### undefined & Null
- 'void'와 마찬가지로, undefined와 null은 그 자체로는 쓸모가 없습니다.
- 둘 다 소문자만 존재

### undefined & null are subtypes of all other types
- 기본 설정
- number에 null또는 undefined를 할당할 수 있다는 의미
- 하지만, 컴파일 옵션에서 `--strictNullChecks`사용하면, null과 undefined는 void나 자기 자신들에게만 할당할 수 있습니다.
  - 이 경우, null과 undefined를 할당할 수 있게 하려면, union type을 이용해야 합니다.

### null in JavaScript
- null이라는 값으로 할당된 것을 null이라고 합니다.
- 무언가가 있는데, 사용할 준비가 덜 된 상태.
- 런타임에서 typeof 연산자를 알아내면, undefined입니다.

### void
- 타입이 없는 상태
- `any`와 반대의 의미
- 소문자!
- 주로 함수의 리턴이 없을때 사용

### Any
- 어떤 타입이어도 상관없는 타입
- 이걸 최대한 쓰지 않는게 핵심
- 컴파일 타임에 타입 체크가 정상적으로 이뤄지지 않기 때문
- 컴파일 옵션 중 any를 쓰면 오류를 뱉도록 하는 옵션도 있음 `noImplicitAny`

### Tuple
- 배열인데 타입이 한 가지가 아닌 경우
- 마찬가지로 객체
- 꺼내 사용할때 주의가 필요
- 대신 interface로 사용하기도 함

### Enum
```
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
```

### Symbol
- ECMAScript 2015의 Symbol입니다
- 프리미티브 타입의 값을 담아서 사용합니다
- 고유하고 수정불가능한 값으로 만들어줍니다
