---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript

TypeScript = Language

* 타입스크립트는 `프로그래밍 언어`입니다.
* 타입스크립트는 `Compiled Language`입니다.
  - 전통적인 Compiled Language와 다른 점이 많아 'Transpile'이라는 용어를 사용하기도 합니다.
* 자바스크립트는 Interpreted Language 입니다(읽으면서 실행)

<table style="width:100%">
<tr>
  <th style="width:50%"><h2>Compiled</h2></th>
  <th style="width:50%"><h2>Interpreted</h2></th>
</tr>
<tr>
  <td>컴파일, 컴파일러, 컴파일하는 시점(컴파일 타임) 필요 O</td>
  <td>컴파일, 컴파일러, 컴파일하는 시점 필요 X</td>
</tr>
<tr>
  <td>컴파일된 결과물을 실행, 컴파일된 결과물을 실행하는 시점</td>
  <td>코드를 실행하는 시점 O = 런타임</td>
</tr>
</table>


> ## 타입스크립트 개요
* 마이크로소프트에서 구현한 JavaScript의 슈퍼셋(Superset, 상위) 프로그래밍 언어. 확장자로는 .ts를 사용하며, 컴파일의 결과물로 JavaScript 파일인 .js를 출력한다. 최종적으로 런타임에서는 이렇게 출력된 JavaScript 코드를 구동시키게 된다.
* 개발 도구(IDE나 컴파일러 등)에게 개발자가 의도한 변수나 함수 등의 목적을 더욱 명확하게 전달할 수 있고, 그렇게 전달된 정보를 기반으로 코드 자동 완성이나 잘못된 변수/함수 사용에 대한 에러 알림 같은 풍부한 피드백을 받을 수 있게 되므로 순수 자바스크립트에 비해 어마어마한 생산성 향상을 꾀할 수 있다. 즉, `'자바스크립트를 실제로 사용하기 전에 있을만한 타입 에러들을 미리 잡는 것'` 이 타입스크립트의 사용 목적이다.

> ## 개발 환경 구축 및 컴파일러 사용
* .bin 안에 있는 파일은 경로 안붙이고 사용 가능
```
tsc --init
//tsc 초기 세팅을 하겠다
tsconfig.json 파일이 생성됨
```

```
//tsconfig.json
"target": "es5", 
"module": "commonjs", 
```

tsconfig.json이 있는 상태에서는 터미널에서 tsc만 입력해도 폴더 내에서 컴파일 활동이 진행됨

