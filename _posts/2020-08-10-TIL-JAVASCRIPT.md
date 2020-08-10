---
layout: post
title: "TIL-JAVASCRIPT"
subtitle: "JAVASCRIPT - ECMA6"
background: '/img/posts/02.jpg'
---

# ECMA6

## let, const와 블록 레벨 스코프
## let
- let 키워드로 선언된 변수는 블록 레벨 스코프를 따른다.
- var 키워드와 다르게 중복 변수 선언할 수 없다(SyntaxError)
- 호이스팅이 발생해도 선언문 이전에 참조하면 참조 에러(ReferenceError)가 발생한다. **일시적 사각지대(Temporal Dead Zone; TDZ)** 에 빠지기 때문이다.(var의 경우 undefined)
![TDZ](https://poiemaweb.com/img/let-lifecycle.png)
- 클로저

```JAVASCRIPT
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 전역 변수다.
for (var i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다.
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
//실행결과 기댓값: 0, 1, 2
//실제 결과: 3이 세번
//이유: for 루프의 var i가 전역 변수이기 때문
```
```JAVASCRIPT
//아래처럼 해야 원하는 값이 나옴
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 전역 변수다.
for (var i = 0; i < 3; i++) {
  (function (index) { // index는 자유변수다.
    funcs.push(function () { console.log(index); });
  }(i));
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  funcs[j]();
}
```
```JAVASCRIPT
//let을 활용하면 동일학 작동을 한다.
var funcs = [];

// 함수의 배열을 생성하는 for 루프의 i는 for 루프의 코드 블록에서만 유효한 지역 변수이면서 자유 변수이다.
for (let i = 0; i < 3; i++) {
  funcs.push(function () { console.log(i); });
}

// 배열에서 함수를 꺼내어 호출한다
for (var j = 0; j < 3; j++) {
  console.dir(funcs[j]);
  funcs[j]();
}
```
- var의 경우 전역 객체로 window.변수명 으로 사용 가능하지만 let은 window. 으로 접근 할 수 없다.(개념적인 블록 내 존재)

## const
상수(변하지 않는 값)를 위해 사용된다.
- const는 재할당 자유로우나 const는 재할당 금지
- const는 반드시 선언과 동시에 할당이 이루어져야 한다는 것이다. 그렇지 않으면 문법 에러(SyntaxError)가 발생
- 재할당이 금지된다는 것은 객체에 대한 참조를 변경하지 못한다는 것을 의미한다. 하지만, **객체의 프로퍼티는 변경 가능**하다.
```JAVASCRIPT
const user = { name: 'Lee' };

// const 변수는 재할당이 금지된다.
// user = {}; // TypeError: Assignment to constant variable.

// 객체의 내용은 변경할 수 있다.
user.name = 'Kim';

console.log(user); // { name: 'Kim' }
```

## 정리

var와 let, 그리고 const는 다음처럼 사용하는 것을 추천한다.

- ES6를 사용한다면 var 키워드는 사용하지 않는다.
- 재할당이 필요한 경우에 한정해 let 키워드를 사용한다. 이때 변수의 스코프는 최대한 좁게 만든다.
- 변경이 발생하지 않는(재할당이 필요 없는 상수) 원시 값과 객체에는 const 키워드를 사용한다.
- const 키워드는 재할당을 금지하므로 var, let 보다 안전하다.

참고사이트: (https://poiemaweb.com/es6-block-scope)


## [오늘의 꿀 TIP!] - ${기술명} CheatSheet
공부를 충분히 하지 않았음에도 기술을 사용해야하는 경우
${기술명} CheatSheet 라는 것을 검색해보세요
CheatSheet라는 것은 치트키를 모아놓은 것처럼
유용하게 잘 쓰이는 것들을 요약해놓은 것입니다!
공부를 처음해야할 때도 빠르게 살펴보기 좋습니다!
> ${hosting} CheatSheet 검색을 통해 발견한 깃헙
Modern JavaScript Cheatsheet
https://github.com/mbeaudru/modern-js-cheatsheet