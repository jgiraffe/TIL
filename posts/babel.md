# Babel

## 바벨이란

- 최신 표준 JavaScript를 이전 버전의 JavaScript로 변환해주는 `컴파일러`
- `ES6+`, `JSX`, `TypeScript`, `Flow` 의 변환을 지원
- 모듈화되어있음
- 플러그인으로 만들어짐
  - 자신만의 변환 파이프라인을 구성하거나, 플러그인 제작도 가능

## 원리

### Parse

- 추상 구문 트리(abstract syntax tree, AST)를 만들어내는 `분석` 단계
- `어휘 분석 (Lexical Analysis)`을 통해 코드 문자열을 토큰 스트림으로 바꾸고,  
  `구문 분석 (Syntactic Analysis)`을 통해 토큰 스트림을 AST로 변환
- [@babel/parser](https://babeljs.io/docs/babel-parser) (구 babylon)

### Transform

- AST를 탐색하여 노드들을 추가, 업데이트, 제거하는 `변환` 단계
- 해당 과정에서 플러그인이 수행된다.

### Generate

- 최종 AST를 깊이 우선 탐색해서 코드 문자열과 소스맵을 `생성`하는 단계
- [@babel/generator](https://babeljs.io/docs/babel-generator)

## 주요 패키지

> 빌드 시 필요하므로 패키지는 개발 의존성으로 설치할 것

- `@babel/core` : 바벨 컴파일러 코어
- `@babel/cli` : 바벨 CLI
- 플러그인
  - [플러그인 목록](https://babel.dev/docs/plugins-list)
- 공식 프리셋 (플러그인 묶음)
  - [@babel/preset-env](https://babeljs.io/docs/babel-preset-env) for compiling ES2015+ syntax
  - [@babel/preset-react](https://babeljs.io/docs/babel-preset-react)
  - [@babel/preset-typescript](https://babeljs.io/docs/babel-preset-typescript)
  - [@babel/preset-flow](https://babeljs.io/docs/babel-preset-flow)

## 사용해보기 (CLI)

> ES6+ 프리셋을 이용해 index.js 컴파일

```bash
$ npx babel index.js --presets=@babel/preset-env
```

> package.json script로 등록하는 경우 (--out-dir 는 -d 로 축약 가능)

```json
"scripts": { "build": "babel src --out-dir dist" }
```

### Config Files

- 매번 플러그인/프리셋을 지정해주는건 까다로우므로 설정 파일을 사용한다.
- `babel.config.*`
  - Project-wide
- `.babelrc.*`
  - File-relative (monorepo에서 적합)
  - 바벨 키 사용하는 경우
- 확장자 : `.json`, `.js`, `.cjs`, `.mjs`, `.cts`

> babel.config.json 또는 .babelrc.json

```json
{
  "presets": [ ... ],
  "plugins": [ ... ],
}
```

> .babelrc.json 설정을 바벨 키를 사용해 packge.json에서 구성하기

```json
{
  "name": "my-package",
  "version": "1.0.0",
  "babel": {
    "presets": [ ... ],
    "plugins": [ ... ],
  }
}
```

## 레퍼런스

- 바벨 공식 사이트 : https://babeljs.io/
- 바벨 핸드북 : https://github.com/jamiebuilds/babel-handbook
- ast 위키피디아 : https://wikipedia.org/wiki/Abstract_syntax_tree
