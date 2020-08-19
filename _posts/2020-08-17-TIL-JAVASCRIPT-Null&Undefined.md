---
layout: post
title: "TIL-JAVASCRIPT"
subtitle: "JAVASCRIPT - Null&Undefined"
background: '/img/posts/02.jpg'
---

> Undefined
값이 대입되지 않은 변수 혹은 속성을 사용하려고 할 때
```JAVASCRIPT
typeof null //'object'
```

> Null
객체가 없음
```JAVASCRIPT
typeof undefined // 'undefined'
```

비록 undefined가 '없음'을 나타내는 값일지라도, 대입한 적 없는 변수 혹은 속성과, 명시적으로 '없음'을 나타내는 경우를 구분을 할 수 있어야 코드의 의미가 명확해 질 것입니다. 프로그래머의 입장에서 명시적으로 부재를 나타내고 싶다면 항상 null을 사용하는 것이 좋습니다.

## Null Check
null check는 간단히 등호를 이용해서 할 수 있습니다.
```JAVASCRIPT
function printIfNotNull(input) {
  if (input !== null && input !== undefined) {
    console.log(input);
  }
}

// 아래 세 개의 식은 완전히 같은 의미입니다.
input !== null && input !== undefined;
input != null;
input != undefined;

// 아래 세 개의 식은 완전히 같은 의미입니다.
input === null || input === undefined;
input == null;
input == undefined;
```

## ===, == 차이 (strict equality comparison operator, abstract equality comparison operator)
대개 ===는 값이 정확히 같을 때 true라는 결과값을 반환하고, ==는 그렇지 않을 때가 많습니다.
그래서 **보통의 경우 ===를 사용하는 것이 권장되는 편**입니다.

다만 null check를 할 때 만큼은 ==를 쓰는 것이 편리합니다.
```JAVASCRIPT
null === undefined; // false
null == undefined;  // true

null == 1       // false
null == 'hello' // false
null == false   // false

undefined == 1       // false
undefined == 'hello' // false
undefined == false   // false
```
즉, == 연산자는 한 쪽 피연산자에 null 혹은 undefined가 오면, 다른 쪽 피연산자에 null 혹은 undefined가 왔을 때만 true를 반환하고, 다른 모든 경우에 false를 반환합니다.

따라서 null check를 할 때 만큼은 ==를 사용하는 것이 편합니다. 