---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript

## interface
```JAVASCRIPT
interface Perseon {
    name: string;
    age?: number; //?를 붙이면 있을 수도 있고 없을 수도 있음
}

const person:Person = {
    name: 'Mark',
    age: 35 //age 지우면 에러 뜸
};

function hello(p: Person): void {
    console.log(`안녕하세요 ${p.name} 입니다.`);
}
```
```JAVASCRIPT
// indexable type
interface Person {
    name: string;
    [index: string]: string; //person.아무거나 받아도 string
 }

 const person: Person = {
     name: 'Mark'
 }

 person.anybody = "Anna";

 function hello(p: Person): void {
     console.log(`안녕하세요 ${p.name} 입니다.`);
 }
```
```JAVASCRIPT
interface Person {
    name: string;
    hello(): string;
}

const person: Person = {
    name: 'Mark',
    hello(): string {
        return 'Hello';
    }
    //위 아래 같음
    hello: (): string => {
        return 'Hello';
    }
};

function hello(p: Person): void {
    console.log(`안녕하세요 ${p.name}입니다.`);
}
```

### class implement
```JAVASCRIPT
interface IPerson {
    name: string;
    hello(): void;
}

class Person implements IPerson {
    name: String = null;

    constructor(name: string) {
        this.name = name;
    }

    hello(): void {
        console.log(``);
    }

    public hi(): void {
        console.log('hi');
    }
}

const Person: Person = new Person('Mark');
//person.hi, hello 할 수 있음

const Person: IPerson = new Person('Mark');
//Person.hello();
```

- `인터페이스 끼리는 상속이 됨`
- 함수는 타입 체크가 할당할 때가 아니라 사용할 때 한다는 점을 명심