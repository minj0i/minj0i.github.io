---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript

> ## Obejct와 Enum의 차이
1. 객체는 (별다른 처리를 해주지 않았다면) 속성을 자유로이 변경할 수 있는데 반해, enum의 속성은 변경할 수 없습니다.
2. 객체의 속성은 (별다른 처리를 해주지 않았다면) 리터럴의 타입이 아니라 그보다 넓은 타입으로 타입 추론이 이루어집니다. enum은 항상 리터럴 타입이 사용됩니다.
3. 객체의 속성 값으로는 JavaScript가 허용하는 모든 값이 올 수 있지만, enum의 속성 값으로는 문자열 또는 숫자만 허용됩니다.

정리하자면, 같은 ‘종류’를 나타내는 여러 개의 숫자 혹은 문자열을 다뤄야 하는데, 각각 적당한 이름을 붙여서 코드의 가독성을 높이고 싶다면 enum을 사용하세요. 그 외의 경우 상수, 배열, 객체 등을 사용하시면 됩니다.
- 출처: https://medium.com/@seungha_kim_IT/typescript-enum%EC%9D%84-%EC%82%AC%EC%9A%A9%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0-3b3ccd8e5552
- (아직 잘모르겠지만..Compile시 달라지는 부분) : https://jaeyeophan.github.io/2018/06/16/TS-8-enum-vs-const-enum/

> ## interface와 type의 차이점
예전에는 interface 타입과 객체 자체에 대한 type 별칭은 많은 점이 비슷하지만, type 별칭보다 더 많은 것을 할 수 있기에 interface를 사용하는 것을 일반적으로 권장되었음
- interface만 extends, implements가 가능했었으나, 현재는 type 안에 union이 사용되는 경우는 제외하고 extends, implements 모두 interface와 같이 동작함
- interface는 여러 번 선언해도 병합 될 수 있지만, type은 안됨

### *Interface의 Declaration Merging이 가장 큰 차이이다*

interface는 같은 이름으로 여러 번 선언을 해도 컴파일 시점에서 합쳐지기 때문에 확장성이 좋다.

따라서 일반적으로는 interface를 사용하고 union, tuple 등이 필요한 경우에만 type 별칭을 사용하라는 TypeScript Handbook의 내용은 현재에도 유효하다.

declaration merging으로 확장할 수 있기 때문에, 외부에 노출해야 하는 public API에 사용되는 타입은 항상 interface를 사용하여 작성해야 한다.

type 별칭으로 작성된 타입은 조금 더 제한적이기 때문에 private API같이 외부에 노출할 필요가 없는 경우에 사용하는 것이 좋다.

### *React Component의 Props와 State의 타입을 기술하려면 어떤 것이 좋을까?*

일반적으로는 interface를 사용해도 무리가 없다.

React component를 사용하는데 declaration merging이나 implements는 필요 없다.

interface는 union이 사용되었다면 extends 할 수 없기 때문에 해당 경우에는 type 별칭을 사용해서 타입을 기술해야 한다.

- 출처: https://joonsungum.github.io/post/2019-02-25-typescript-interface-and-type-alias/

> ## 선택적 프로퍼티 Optional Property
인터페이스의 프로퍼티가 특정한 조건 하에 존재하거나 아예 존재하지 않을 수 있다.

Interface의 일부가 아닌 속성의 사용을 방지하면서, 사용 가능한 속성을 설명할 수 있다.

예를 들면 createSquare에서 color 속성 이름을 잘못 입력하면 다음과 같은 오류 메세지가 발생함.

```JAVASCRIPT
interface SquareConfig {
	color?: string;
	width?: number;
}
function createSquare(config: SquareConfig): {color: string; area: number){
	let newSquare = { color: "white", area: 100};
	if(config.colr){
    //Error: Property 'clor' does not exist on type 'SquareConfig'
		newSquare.color = config.colr;
	}
	if(config.width){
		newSquare.area = config.width * config.width;
	}
	reutnr newSquare;
}
let mySquare = createSquare({ color: "black"});
```