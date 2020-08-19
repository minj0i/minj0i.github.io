---
layout: post
title: "TIL-JAVASCRIPT - Map"
subtitle: "JAVASCRIPT - Map"
background: '/img/posts/02.jpg'
---

# Map
맵(Map)은 키가 있는 데이터를 저장한다는 점에서 객체와 유사합니다. 다만, 맵은 **키에 다양한 자료형을 허용한다는 점**에서 차이가 있습니다. 또한 맵은 객체와 다르게 삽입 순서를 기억합니다.

맵에는 다음과 같은 주요 메서드와 프로퍼티가 있습니다.

- new Map() – 맵을 만듭니다.
- map.set(key, value) – key를 이용해 value를 저장합니다.
- map.get(key) – key에 해당하는 값을 반환합니다. key가 존재하지 않으면 undefined를 반환합니다.
- map.has(key) – key가 존재하면 true, 존재하지 않으면 false를 반환합니다.
- map.delete(key) – key에 해당하는 값을 삭제합니다.
- map.clear() – 맵 안의 모든 요소를 제거합니다.
- map.size – 요소의 개수를 반환합니다.

```JAVASCRIPT
let map = new Map();

map.set('1', 'str1');   // 문자형 키
map.set(1, 'num1');     // 숫자형 키
map.set(true, 'bool1'); // 불린형 키

//체이닝
map.set('1', 'str1')
  .set(1, 'num1')
  .set(true, 'bool1');

// 맵은 키의 타입을 변환시키지 않고 그대로 유지합니다.
alert( map.get(1)   ); // 'num1'
alert( map.get('1') ); // 'str1'

alert( map.size ); // 3
```

**map[key]는 Map을 쓰는 바른 방법이 아닙니다.**
```
map[key] = 2로 값을 설정하는 것 같이 map[key]를 사용할 수 있긴 합니다. 하지만 이 방법은 map을 일반 객체처럼 취급하게 됩니다. 따라서 여러 제약이 생기게 되죠.

map을 사용할 땐 map전용 메서드 set, get 등을 사용해야만 합니다.
```

> map 메소드
- map.keys() – 각 요소의 키를 모은 반복 가능한(iterable, 이터러블) 객체를 반환합니다.
- map.values() – 각 요소의 값을 모은 이터러블 객체를 반환합니다.
- map.entries() – 요소의 [키, 값]을 한 쌍으로 하는 이터러블 객체를 반환합니다. 이 이터러블 객체는 for..of반복문의 기초로 쓰입니다.
```JAVASCRIPT
let recipeMap = new Map([
  ['cucumber', 500],
  ['tomatoes', 350],
  ['onion',    50]
]);

// 키(vegetable)를 대상으로 순회합니다.
for (let vegetable of recipeMap.keys()) {
  alert(vegetable); // cucumber, tomatoes, onion
}

// 값(amount)을 대상으로 순회합니다.
for (let amount of recipeMap.values()) {
  alert(amount); // 500, 350, 50
}

// [키, 값] 쌍을 대상으로 순회합니다.
for (let entry of recipeMap) { // recipeMap.entries()와 동일합니다.
  alert(entry); // cucumber,500 ...
}

// 각 (키, 값) 쌍을 대상으로 함수를 실행
recipeMap.forEach( (value, key, map) => {
  alert(`${key}: ${value}`); // cucumber: 500 ...
});

// 키-값 쌍인 배열이나 이터러블 객체를 맵으로 만들기
let obj = {
  name: "John",
  age: 30
};

let map = new Map(Object.entries(obj));
alert( map.get('name') ); // John

// 맵을 객체로 만들기
let map = new Map();
map.set('banana', 1);
map.set('orange', 2);
map.set('meat', 4);

let obj = Object.fromEntries(map.entries()); // 맵을 일반 객체로 변환
let obj = Object.fromEntries(map); // .entries()를 생략함도 가능

// 맵이 객체가 되었습니다!
// obj = { banana: 1, orange: 2, meat: 4 }

alert(obj.orange); // 2
```