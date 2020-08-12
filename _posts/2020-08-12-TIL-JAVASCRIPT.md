---
layout: post
title: "TIL-JAVASCRIPT"
subtitle: "JAVASCRIPT - ECMA6"
background: '/img/posts/02.jpg'
---

# ECMA6

## 객체 프로퍼티 기능 확장

>## 프로퍼티 축약 표현

```JAVASCRIPT
// ES5
var x = 1, y = 2;

var obj = {
  x: x,
  y: y
};

console.log(obj); // { x: 1, y: 2 }

// ES6
let x = 1, y = 2;

const obj = { x, y };

console.log(obj); // { x: 1, y: 2 }
```

>## 프로퍼티 키 동적 생성- 계산된 프로퍼티 이름(Computed property name)

```JAVASCRIPT
// ES5
var prefix = 'prop';
var i = 0;

var obj = {};

obj[prefix + '-' + ++i] =l i;
obj[prefix + '-' + ++i] = i;
obj[prefix + '-' + ++i] = i;

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}

// ES6
const prefix = 'prop';
let i = 0;

const obj = {
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i,
  [`${prefix}-${++i}`]: i
};

console.log(obj); // {prop-1: 1, prop-2: 2, prop-3: 3}
});
```

>## 메소드 축약 표현
```JAVASCRIPT
// ES5
var obj = {
  name: 'Lee',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee

// ES6
const obj = {
  name: 'Lee',
  // 메소드 축약 표현
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

obj.sayHi(); // Hi! Lee
```

>## 메소드 축약 표현
ES5에서 객체 리터럴을 상속하기 위해서는 Object.create() 함수를 사용한다. 이를 프로토타입 패턴 상속이라 한다.<br/>
ES6에서는 객체 리터럴 내부에서 __proto__ 프로퍼티를 직접 설정할 수 있다. 이것은 객체 리터럴에 의해 생성된 객체의 __proto__ 프로퍼티에 다른 객체를 직접 바인딩하여 상속을 표현할 수 있음을 의미한다.
```JAVASCRIPT
// ES5
var parent = {
  name: 'parent',
  sayHi: function() {
    console.log('Hi! ' + this.name);
  }
};

// 프로토타입 패턴 상속
var child = Object.create(parent);
child.name = 'child';

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child

// ES6
const parent = {
  name: 'parent',
  sayHi() {
    console.log('Hi! ' + this.name);
  }
};

const child = {
  // child 객체의 프로토타입 객체에 parent 객체를 바인딩하여 상속을 구현한다.
  __proto__: parent,
  name: 'child'
};

parent.sayHi(); // Hi! parent
child.sayHi();  // Hi! child
```

## REACT를 위한 ES6 문법
- https://www.youtube.com/watch?v=IpGNWFFsjA4&t=732s (ES6 문법 액기스(1))
- (Do it! 리액트 프로그래밍 정석) 작가

>## (1) 템플릿 문자열
- 백틱(`), ${ } 활용

```JAVASCRIPT
//ES5
var string1 = '안녕';
var string2 = '반갑습니다';

var greeting = string1 + ' ' + string2;
var multiline = '문자열1\n문자열2';

//ES6 
var greeting = `${string1} ${string2}`;
var multiline = `
문자열1
문자열2
`;
```

>## 전개 연산자(spread operator)
- 배열이나 객체, 변수명 앞에 ...를 활용
- ES5
  - 인덱스 활용하거나 concat을 활용하여 배열을 합침
- ES6
  - ...array1 이라고 하면 배열 안에 있는 것을 나열 형태로 활용 가능
```JAVASCRIPT
//ES6
var array1 = ['one', 'two'];
var array2 = ['three', 'four'];

var combined = [...array1, ...array2]; //['one', 'two', 'three', 'four']

//값 추출도 가능
var [first, second] = array1;
console.log(first, second); //one two

var array1 = ['one', 'two', 3, 4, 5, 6, 7];
var [first, ...other] = array1;
console.log(first, other); //one ['two', 3, 4, 5, 6, 7]

//함수에서도 가능
//ES5
function func() {
  console.log(arguments); // [Arguments] {'0': 1, '1':2, '2':3}
  console.log(Array.prototype.slice.call(arguments)); // [1, 2, 3]
}

func(1,2,3);

//ES6
function func(...args) {
  console.log(first); //1
  console.log(args); //[2, 3]
}

func(1,2,3);

//function func(first, ...args, last) 은 추출방식에서 사용 불가능!
//항상 마지막에 전개연산자 가능
```
- 객체도 가능
```JAVASCRIPT
var object1 = {one: 1, two: 2, other: 0};

//변수를 키값으로 선언하면 값을 받을 수 있음
var{ one } = object1;
console.log(one); //1

//변수가 위에 선언되어있다면 다른 이름으로 받을 수 있음
var one = 'one';
var{ one: myOne } = object1;
console.log(myOne); //1
```

>## (2) 가변 변수와 불변 변수
- 가변변수: let (ES5의 var로 생각하면 됨)
- 불변변수: const
  - const로 하고 []선언 후 push나 splice로 하면 배열이 변경됨
  - immer, immutable.js를 활용해서 수정하기도 함

* 규칙1. 배열 가변 내장 함수(push, splice, pop, shift) 항목 할당식 (a[0] = 1) **사용하지 않는다**
* 규칙2. 배열 불변 내장 함수 concat().slice()로 대신 구현한다.
<table>
<tr><th>가변내장함수</th><th>무결성 내장 함수</th></tr>
<tr>
  <td>push(...items)</td>
  <td>concat(...items)</td>
</tr>
<tr>
  <td>splice(s, c, ...items)</td>
  <td>slice(0, s)<br/>.concat(...items, slice(s+c))</td>
</tr>
<tr>
  <td>pop()</td>
  <td>slice(0, len - 1)</td>
</tr>
<tr>
  <td>shift()</td>
  <td>slice(1)</td>
</tr>
</table>

* 규칙3. 객체 할당 표현식 obj.a = '새 값'은 전개 연산자 {...obj.a: '새 값'}으로 대신 구현한다.
```JAVASCRIPT
const obj = {
  a: 1,
  b: 2,
}
const obj2 = {
  ...obj
  a: 3
}
console.log(obj2); //{ a: 3, b: 2 }
```