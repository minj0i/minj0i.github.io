---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript

www.typescriptlang.org/play/index.html

에서 ES5랑 비교 가능

## var
- ES5
- 변수의 유효 범위: 함수 스코프
- 호이스팅(o)
- 재선언가능

## let
```
let a: string = '에이';
let b = '비이';
```
- a는 명시적으로 지정된 타입인 string
- b는 타입추론에 의한 타입인 string
- 경우 거의 없음

## const
```
const c: string = '씨이';
cosnt d = '디이';
```
- c는 명시적으로 지정된 타입인 string
- d는 타입추론에 의한 타입인 리터럴타입 "디이"
- 문자열 자체가 타입으로 들어옴

## Type assertions
- 형 변환과는 다릅니다
    - 형변화는 실제 데이터 구조를 바꿔줍니다.
- '타입이 이것이다'라고 컴파일러에게 알려주는 것을 의미
    - 그래서 행동에 대해서 작성자가 100%신뢰하는 것이 중요
- 문법적으로는 두가지 방법이 존재
    - 변수 as 강제할타입
    - <강제할타입> 변수

```
//sample code
let someValue: any = "this is a string";

//주로 넓은 타입에서 좁은 타입으로 강제하는 경우가 많다.
let strLength: number = (<string>someValue).length;

//jsx에서는 as를 쓴다.
let strLength: number = (someValue as string).length;
```

## 타입 별칭(별명)
- 인터페이스랑 비슷해보임
- primitive, union type, tuple
- 기타 직접 작성해야 하는 타입을 다른 이름으로 지정할 수 있음
- 만들어진 타입의 refer로 사용하는 것이지 타입을 만드는 것이 아님

```JAVASCRIPT
//Aliasing Union Type
let a: any;
let b: string | number;


b = '스트링';
b = 0; //가능


function test(arg: string | number): string | number {
    return arg;
}

//위를 type을 지정하면
type StringOrNumber = string | number;

let b: StringOrNumber;

function test(arg: StringOrNumber): StringOrNumber {
    return arg;
}
```

```JAVASCRIPT
//Alliasing Tuple
let person: [string, number] = ['Mark', 35];

type PersonTuple = [string, number];

let another: PersonTuple = ['Anna', 24];
```

## interface와의 차이점
```JAVASCRIPT
type Alias = { num: number};

interface Interface {
    num: number;
}

declare function aliased(arg: Alias): Alias;
declare function interfaced(arg: Inteface): Inteface;

```
1. type alias는 object literal type로
2. interface는 interface로
3. interface처럼 쓸 수 있지만, interface처럼 얘가 상속받는 구조는 되지만 얘는 다른 애를 상속 못함 (위 1, 2문제로 쓰지않는다.)

* 인터페이스의 특징: 인터페이스 부분은 소스코드에 뜨지않음