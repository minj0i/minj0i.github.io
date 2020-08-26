---
layout: post
title: "TIL-TypeScript"
subtitle: "TypeScript"
background: '/img/posts/02.jpg'
---

# TypeScript
(강의3: https://www.inflearn.com/course/%ED%83%80%EC%9E%85%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%94%EB%A6%AC%EC%95%84-1705-%EA%B8%B0%EC%B4%88-%EC%84%B8%EB%AF%B8%EB%82%98/lecture/6803?tab=curriculum)

(강의록 정리 블로그: https://feel5ny.github.io/2017/11/15/Typescript_03/)

- tslint
- TSconfig: http://json.schemastore.org/tsconfig
  - 버전 업 됨에 따라 많아지는 중
  - 필요없는애 : noLib ...

- 최상위 프로퍼티
  - compileOnSave
  - extends
  - compileOptions
  - files
  - include
  - exclude

> ### compileOnSave
- true / fase(default false)
- 파일을 저장하면 자동으로 compile

> ### extends
- 한 파일을 만들어 놓고 상속받아서 작은 부분만 바꿔서 쓸 때

> ### file, include, exclude
- 셋다 설정이 없으면 , 전부다 컴파일
- files
  - 상대 혹은 절대 경로의 리스트 배열.
  - 파일별 부분 컴파일이 된다.
  - exclude 보다 쎕니다. (exclude가 해놓아도 files 에 있으면 컴파일 실행된다는 뜻)
  - 특정 폴더를 exclude가 있어도 컴파일 된다.
- include, exclude
  - glob 패턴 (마치 .gitignore)
  - include
      - exclude 보다 약하다.
      - 같은걸 사용하면 , .ts / .tsx / .d.ts 만 include (allowJS)
  - exclude
    - 설정 안하면 4가지 (node_modules, bower_components, - jspm_packages, )를 default 로 제외한다 .
    - <outDir>은 항상 제외합니다 . (include 에 있어도 )

> ## @types (중요 !)
TypeScript `2.0` 부터 사용 가능해진 내장 type definition 시스템으로 이전 버전에서는 사용하지 못한다.

이전 버전은 TSD(deprecated) / typings

요즘 추세는 @types 지원, 아니면 프로젝트 안에 존재

- 아무 설정을 안하면 ?
  - node_modules/@types 라는 모든 경로를 찾아서 사용
- typeRoots 를 사용하면 ?
  - 배열 안에 들어있는 경로들 아래서만 가져옵니다 .
- types 를 사용하면 ?
  - 패키지 이름입니다.
- 배열 안의 모듈 혹은 ./node_modules/@types/ 안의 모듈 이름에서 찾아옵니다 .
- [] 빈 배열을 넣는다는건 이 시스템을 이용하지 않겠다는 것입니다 .
- typeRoots 와 types 를 같이 사용하지 않습니다 .
  - 만약 하나도 안쓸 경우라면, types에 빈 배열 넣으면 됨(그럴일은 없음)

```JAVASCRIPT
// compiileOptions : type
{
  "type": "object",
  "description": "Instructs the TypeScript compiler how to compile .ts files.",
  "properties": {
    "typeRoots": {
      "description":
        "Specify list of directories for type definition files to be included. Requires TypeScript version 2.0 or later.",
      "type": "array",
      "items": {
        "type": "string"
      }
    },
    "types": {
      "description":
        "Type declaration files to be included in compilation. Requires TypeScript version 2.0 or later.",
      "type": "array",
      "items": {
        "type": "string"
      }
    }
  }
}
```
> ## compileOptions

> ### target과 lib
```JAVASCRIPT
{
  "type": "object",
  "description": "Instructs the TypeScript compiler how to compile .ts files.",
  "properties": {
    "target": {
      "description":
        "Specify ECMAScript target version. Permitted values are 'es3', 'es5', 'es2015', 'es2016', 'es2017' or 'esnext'.",
      "type": "string",
      "default": "es3",
      "anyOf": [
        {
          "enum": [
            "es3",
            "es5",
            "es2015",
            "es2016",
            "es2017",
            "esnext" // 확정은 아니지만 곧 확정될 것 같은 문법들을 모아둔
          ]
        },
        {
          "pattern": "^([eE][sS]([356]|(201[567])|[nN][eE][xX][tT]))$"
        }
      ]
    },
    "lib": {
      "description":
        "Specify library file to be included in the compilation. Requires TypeScript version 2.0 or later.",
      "type": "array",
      "items": {
        "type": "string",
        "enum": [
          "es5",
          "es6",
          "es2015",
          "es7",
          "es2016",
          "es2017",
          "esnext",
          "dom",
          "dom.iterable",
          "webworker",
          "scripthost",
          "es2015.core",
          "es2015.collection",
          "es2015.generator",
          "es2015.iterable",
          "es2015.promise",
          "es2015.proxy",
          "es2015.reflect",
          "es2015.symbol",
          "es2015.symbol.wellknown",
          "es2016.array.include",
          "es2017.object",
          "es2017.sharedmemory",
          "esnext.asynciterable"
        ]
      }
    },
    "noLib": {
      "description": "Do not include the default library file (lib.d.ts).",
      "type": "boolean"
    }
  }
}
```
**target**

- 빌드의 결과물을 어떤 버전으로 할 것이냐
- 지정을 안하면 es3 입니다.

**lib**

- 기본 type definition 라이브러리를 어떤 것을 사용할 것이냐 (잘 정의하지 않으면 빨간줄 야기)
- lib 를 지정하지 않을 때 ,
  - target 이 ‘es3’ 이고, 디폴트로 lib.d.ts 를 사용합니다.
  - target 이 ‘es5’ 이면 , 디폴트로 dom, es5, scripthost 를 사용합니다 .
  - target 이 ‘es6’ 이면, 디폴트로 dom, es6, dom.iterable, scripthost 를 사용합니다.
    - es5 이후에는 문법별 쪼개서도 설정 가능하다 .

- lib 를 지정하면 그 lib 배열로만 라이브러리를 사용합니다.
  - ​ 빈 [] => ‘no definition found 어쩌구’ 혹은 "noLib" : true로 바꾸면 된다.

> ### compileOptions: outDir, outFile

파일을 다 모아서 하나의 컴파일된 하나의 파일로 모으고 싶을 때 outFile을 사용

소스디렉토리에 그대로 똑같이 구조를 컴파일된 상태로 옮길 때 outDir 를 사용한다 .

```JAVASCRIPT
{
  "type": "object",
  "description": "Instructs the TypeScript compiler how to compile .ts files.",
  "properties": {
    "outFile": {
      "description": "Concatenate and emit output to single file.",
      "type": "string"
    },
    "outDir": {
      "description": "Redirect output structure to the directory.",
      "type": "string"
    },
    "rootDir": {
      "description":
        "Specifies the root directory of input files. Use to control the output directory structure with --outDir.",
      "type": "string"
    }
  }
}
```
> ### compileOptions: module

**module**
모듈 시스템을 말하는 것 (commonJS, amd(requireJS), systemJS)
- 컴파일 된 모듈의 결과물을 어떤 모듈 시스템으로 할지를 결정
- target 이 ‘es6’ 이면 es6 가 디폴트이고,
- target 이 ‘es6’ 가 아니면 commonjs 가 디폴트 입니다.
- AMD 나 System 와 사용하려면, outFile 이 지정되어야 합니다.
- ES6 나 ES2015 를 사용하려면, target 이 es5 이하여야 합니다.

**moduleResolution**
- ts 소스에서 모듈을 사용하는 방식을 지정해야 합니다.
- Classic 아니면 Node 입니다.
- commonJS 일때만 node 라고 생각하시면 됩니다.

**paths 와 baseUrl**
- 상대경로 방식이 아닌 baseUrl 로 꼭지점과 paths 안의 키/ 밸류로 모듈을 가져가는방식입니다 .
- rootDirs: 배열 안에서 상대 경로를 찾는 방식입니다.
```JAVASCRIPT
{
  "type": "object",
  "description": "Instructs the TypeScript compiler how to compile .ts files.",
  "properties": {
    "module": {
      "description":
        "Specify module code generation: 'none', 'CommonJS', 'Amd', 'System', 'UMD', or 'es2015'.",
      "enum": ["commonjs", "amd", "umd", "system", "es6", "es2015", "none"]
    },
    "moduleResolution": {
      "description":
        "Specifies module resolution strategy: 'node' (Node) or 'classic' (TypeScript pre 1.6) .",
      "type": "string",
      "pattern": "^(([Nn]ode)|([Cc]lassic))$",
      "default": "classic"
    },
    "baseUrl": {
      "description": "Base directory to resolve non-relative module names.",
      "type": "string"
    },
    "paths": {
      "description":
        "Specify path mapping to be computed relative to baseUrl option.",
      "type": "object"
    },
    "rootDirs": {
      "description":
        "Specify list of root directories to be used when resolving modules.",
      "type": "array",
      "items": {
        "type": "string"
      }
    }
  }
}
```

해당 블로거가 쓴 글


현재 플젝 tsconfig.json
처음보는 옵션들이 있어서 정리해보았다 . 참고 : 타입스크립트 공식 페이지

allowSyntheticDefaultImports: true

Allow default imports from modules with no default export. This does not
affect code emit, just typechecking.
리엑트에서 컴포넌트를 import 할 때 주로 쓰는 import Something from './Something'을 사용할 수 있다 .
noImplicitAny: false

Raise error on expressions and declarations with an implied any type.
암시적으로 선언되었는데 any 로 추론되면 에러를 알려줍니다 . false이면 무시됨.
preserveConstEnums: true

Do not erase const enum declarations in generated code. See const enums documentation for more details.
enum 변수선언을 유지한다는 것 같은데 정확히 잘 모르겠다.
allowJs : false

include 에 있는 파일 경로들에 존재하는 모든 .ts, .tsx파일들이 컴파일되는데 ,
allowJs를 true 로 하면 .js와 .jsx 파일도 컴파일 대상이 된다 .
sourceMap : true

Generates corresponding .map file.
트랜스파일을 거치는 많은 모듈들이 디버깅을 위해서 기본적으로 source map 출력을 지원한다 .
noImplicitReturns : true

Report error when not all code paths in function return a value.
제대로 리턴 다 안되면 에러 -> 오류에 대해 강력하게 체크한다는 뜻입니다.
noUnusedParameters : true

Report errors on unused parameters.
사용하지 않는 파라미터가 있으면 에러를 알려줍니다.
noUnusedLocals : true

Report errors on unused locals.
사용 안하는 로컬 변수가 있으면 에러를 알려줍니다 .
