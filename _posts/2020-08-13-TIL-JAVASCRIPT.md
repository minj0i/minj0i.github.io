---
layout: post
title: "TIL-JAVASCRIPT"
subtitle: "JAVASCRIPT - ECMA6"
background: '/img/posts/02.jpg'
---

# ECMA6

## REACT를 위한 ES6 문법
- https://www.youtube.com/watch?v=IpGNWFFsjA4&t=732s (ES6 문법 액기스(3)~)
- (Do it! 리액트 프로그래밍 정석) 작가

>## (3) 클래스 표현식

```JAVASCRIPT
//ES5
function Shape(x, y) {
  this.name = 'Shape';
  this.move(x, y);
}
Shape.prototype.move = function(x, y) {
  this.x = x;
  this.y = y;
};
Shape.prototype.area = function() {
  return 0;
};

Shape.create = function(x, y) {
  return new Shape(x, y);
}

function Circle(x, y, radius) {
  Shape.call(this, x, y);
  this.radius = radius;
}

//ES6
//전개 연산자를 쓰고 추가 함
Circle.prototype = {
  ...Shape.prototype,
  area: function() {
    return this.radius * this.radius * Math.PI;
  },
}
const c = new Circle(0,0,5); //면적 계산됨

class Shape {
  static create(x, y) { return new Shape(x, y)}
  //constructor에서 this.name 대신
  name = 'Shape';
  constructor(x, y) {
    this.move(x, y);
  }
  move(x, y) {
    this.x = x;
    this.y = y;
  }
  area() {
    return 0;
  }
}

class Circle extends Shape {
  constructor(x, y, radius) {
    //super - 부모의 constructor 함수를 호출 = Shape.call
    super(x, y);
    this.radius = radius;
  }
  area() {
    return this.radius * this.radius * Math.PI;
  }
}

const c = new Circle(0, 0, 10);
console.log(c.area());

//staic 확인
const s1 = Shape.create(0, 0);
console.log(s1.area())

//ES7 리액트에 사용되는 표현
class Shape {
  static create(x, y) { return new Shape(x, y)}

  //constructor - 생성자 역할
  constructor(x, y) {
    this.name = 'Shape';
    this.move(x, y);
  }
  move(x, y) {
    this.x = x;
    this.y = y;
  }
  area() {
    return 0;
  }
}

class Circle extends Shape {
  constructor(x, y, radius) {
    //super - 부모의 constructor 함수를 호출 = Shape.call
    super(x, y);
    this.radius = radius;
  }
  area() {
    return this.radius * this.radius * Math.PI;
  }
}

const c = new Circle(0, 0, 10);
console.log(c.area());

//staic 확인
const s1 = Shape.create(0, 0);
console.log(s1.area())
```


>## (4) 화살표 함수
- 함수 표현식을 간결히 하고
- 이후 배우게 될 커링(currying)과 같은 디자인 패턴에서 사용되는 함수를 반환 할 때 '계단형 함수 선언'과 같은 구조가 만들어지지 않게 해준다는 장점이 있음

```JAVASCRIPT
//ES5
function add(first, second) {
  return first + second;
}

//typeof add === 'function'
//익명함수(함수의 이름이 없고 add에 할당)
var add = function(first, second) {
  return first + second;
}l
//typeof add === 'function'


//ES6
var add = (first, second) => {
  return first + second;
}
//중괄호와 return 없이 사용 가능
var add = (first, second) => first + second;

//ES5
function addNumber(num) {
  return function (value) {
    return num + value;
  };
}
//ES6
var addNumber = (num) => {
  return (value) => {
    return num + value;
  };
}
//최종
var addNumber = (num) => (value) => num + value;
```

>## 화살표 함수 - this의 범위
- 함수에서는 bind라는 것을 활용하여 this의 범위를 설정

```JAVASCRIPT
function runAddThis2(func) {
  func(1, 2);
}

class Circle extends Shape {
  constructor(x, y, radius) {
    super(x, y);
    this.radius = radius;
    /*
    이렇게 하면 this 때문에 에러 발생
    var addThis2 = function (first, second) {
      return this.radius + this + second;
    }
    */
     var addThis2 = function (first, second) {
      return this.radius + this + second;
    }.bind(this)
    runAddThis2(addThis2);
  }
  area() {
    return this.radius * this.radius * Math.PI;
  }
}

//아니면 지역변수 _this 생성하여 활용
function runAddThis2(func) {
  func(1, 2);
}

class Circle extends Shape {
  constructor(x, y, radius) {
    super(x, y);
    this.radius = radius;
    var _this = this;
    var addThis2 = function (first, second) {
      return _this.radius + this + second;
    }
    runAddThis2(addThis2);
  }
  area() {
    return this.radius * this.radius * Math.PI;
  }
}
```

>## 객체 확장 표현식과 구조 분해 할당
```JAVASCRIPT
//ES5
var obj = {};
var ram = 'other';
obj. a = 1;
obj['a'+ram] = 1; //{a: 1, aother: 1}

//ES6
obj[`a${ram}`] = 1; //{a: 1, aother: 1}도 가능

//ES5
var ram = 'other';
var obj = {
  a: 1,
  ['a'+ram] : 1
}
//ES6
var ram = 'other';
var obj = {
  a: 1,
  [`a${ram}`] : 1
}

```