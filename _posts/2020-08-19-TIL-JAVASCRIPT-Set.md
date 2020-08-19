---
layout: post
title: "TIL-JAVASCRIPT - Set"
subtitle: "JAVASCRIPT - Set"
background: '/img/posts/02.jpg'
---

# Set
셋(Set)은 중복을 허용하지 않는 값을 모아놓은 특별한 컬렉션입니다. 셋에 키가 없는 값이 저장됩니다.

주요 메서드는 다음과 같습니다.

- new Set(iterable) – 셋을 만듭니다. 이터러블 객체를 전달받으면(대개 배열을 전달받음) 그 안의 값을 복사해 셋에 넣어줍니다.
- set.add(value) – 값을 추가하고 셋 자신을 반환합니다.
- set.delete(value) – 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환합니다.
- set.has(value) – 셋 내에 값이 존재하면 true, 아니면 false를 반환합니다.
- set.clear() – 셋을 비웁니다.
- set.size – 셋에 몇 개의 값이 있는지 세줍니다.
셋 내에 동일한 값(value)이 있다면 set.add(value)을 아무리 많이 호출하더라도 아무런 반응이 없을 겁니다. 셋 내의 값에 중복이 없는 이유가 바로 이 때문이죠.

방문자 방명록을 만든다고 가정해 봅시다. 한 방문자가 여러 번 방문해도 방문자를 중복해서 기록하지 않겠다고 결정 내린 상황입니다. 즉, 한 방문자는 '단 한 번만 기록’되어야 합니다.

이때 적합한 자료구조가 바로 셋입니다.

```JAVASCRIPT
let set = new Set();

let john = { name: "John" };
let pete = { name: "Pete" };
let mary = { name: "Mary" };

// 어떤 고객(john, mary)은 여러 번 방문할 수 있습니다.
set.add(john);
set.add(pete);
set.add(mary);
set.add(john);
set.add(mary);

// 셋에는 유일무이한 값만 저장됩니다.
alert( set.size ); // 3

for (let user of set) {
  alert(user.name); // // John, Pete, Mary 순으로 출력됩니다.
}
```

> 반복 작업
```JAVASCRIPT
let set = new Set(["oranges", "apples", "bananas"]);

for (let value of set) alert(value);

// forEach를 사용해도 동일하게 동작합니다.
// valueAgain을 쓴 이유는 맵과의 호환성 때문 - 맵의 forEach에 쓰인 콜백이 세 개의 인수를 받을 때를 위해서.
set.forEach((value, valueAgain, set) => {
  alert(value);
});
```

> Set 메소드
- set.keys() – 셋 내의 모든 값을 포함하는 이터러블 객체를 반환합니다.
- set.values() – set.keys와 동일한 작업을 합니다. 맵과의 호환성을 위해 만들어진 메서드입니다.
- set.entries() – 셋 내의 각 값을 이용해 만든 [value, value] 배열을 포함하는 이터러블 객체를 반환합니다. 맵과의 호환성을 위해 만들어졌습니다.

## Map, Set 요약
> Map

맵은 키가 있는 값이 저장된 컬렉션입니다.

- new Map([iterable]) – 맵을 만듭니다. [key,value]쌍이 있는 iterable(예: 배열)을 선택적으로 넘길 수 있는데, 이때 넘긴 이터러블 객체는 맵 초기화에 사용됩니다.
- map.set(key, value) – 키를 이용해 값을 저장합니다.
- map.get(key) – 키에 해당하는 값을 반환합니다. key가 존재하지 않으면 undefined를 반환합니다.
- map.has(key) – 키가 있으면 true, 없으면 false를 반환합니다.
- map.delete(key) – 키에 해당하는 값을 삭제합니다.
- map.clear() – 맵 안의 모든 요소를 제거합니다.
- map.size – 요소의 개수를 반환합니다.

일반적인 객체와의 차이점:

키의 타입에 제약이 없습니다. 객체도 키가 될 수 있습니다.
size 프로퍼티 등의 유용한 메서드나 프로퍼티가 있습니다.

> Set

셋은 중복이 없는 값을 저장할 때 쓰이는 컬렉션입니다.

- new Set([iterable]) – 셋을 만듭니다. iterable 객체를 선택적으로 전달받을 수 있는데(대개 배열을 전달받음), 이터러블 객체 안의 요소는 셋을 초기화하는데 쓰입니다.
- set.add(value) – 값을 추가하고 셋 자신을 반환합니다. 셋 내에 이미 value가 있는 경우 아무런 작업을 하지 않습니다.
- set.delete(value) – 값을 제거합니다. 호출 시점에 셋 내에 값이 있어서 제거에 성공하면 true, 아니면 false를 반환합니다.
- set.has(value) – 셋 내에 값이 존재하면 true, 아니면 false를 반환합니다.
- set.clear() – 셋을 비웁니다.
- set.size – 셋에 몇 개의 값이 있는지 세줍니다.
맵과 셋에 반복 작업을 할 땐, 해당 컬렉션에 요소나 값을 추가한 순서대로 반복 작업이 수행됩니다. 따라서 이 두 컬렉션은 정렬이 되어있지 않다고 할 수 없습니다. 그렇지만 컬렉션 내 요소나 값을 재 정렬하거나 (배열에서 인덱스를 이용해 요소를 가져오는 것처럼) 숫자를 이용해 특정 요소나 값을 가지고 오는 것은 불가능합니다.