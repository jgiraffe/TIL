# npm

## npm이란

- JavaScript 패키지 매니저
- npm은 [Node Package Manager의 약어가 아니라고한다,,,](https://github.com/npm/cli#is-npm-an-acronym-for-node-package-manager)

## 설치

- 주로 [nvm](https://github.com/nvm-sh/nvm)을 사용해 Node.js 및 npm을 설치 (권장)
  - 노드 설치 시 npm은 자동 설치
- 윈도우나 맥에서는 [Node.js installer](https://nodejs.org/en/download)를 사용하기도 한다.
- 그 외의 노드 버전 매니저 : n, nodsit, nvm-windows

```bash
$ nvm use 16
Now using node v16.9.1 (npm v7.21.1)
$ node -v
v16.9.1
$ nvm use 14
Now using node v14.18.0 (npm v6.14.15)
$ node -v
v14.18.0
$ nvm install 12
Now using node v12.22.6 (npm v6.14.5)
$ node -v
v12.22.6
```

## node_modules

- npm으로 설치한 패키지는 `node_modules`에 들어간다.
- 로컬 설치 : 현재 패키지의 루트 디렉토리의 `./node_modules`
- 글로벌 설치 (-g) : 노드가 설치된 곳에 설치
- 중복 제거를 위해 상위 디렉토리에 동일 패키지가 있다면 설치하지 않는다.
  - 패키지를 찾을 때 까지 상위 디렉토리의 `node_modules` 를 탐색
  - 의존성 트리가 복잡해지는 단점이 있다.

## package.json

json 포맷으로 구성되는 의존성 관리 파일

### 기본적인 구성

- 패키지에 대한 기본적인 정보를 기입
- [그 외 필드들은 여기 참고](https://docs.npmjs.com/cli/v9/configuring-npm/package-json)

```json
{
  "name": "{{ 패키지명 }}",
  "version": "{{ 패키지 버전 }}",
  "description": "{{ 패키지 설명 }}",
  "main": "{{ 기본 진입점, 디폴트는 index.js }}",
  "author": "{{ 작성자 }}",
  "license": "{{ 라이센스 }}",
  "scripts": "{{ lifecycle 이벤트명 : 수행할 명령 }}"
}
```

### dependencies

- `dependencies`에 명시된 버전을 참조해 패키지들을 설치한다.

```json
{
  "dependencies": {
    "foo": "1.0.0 - 2.9999.9999",
    "bar": ">=1.0.2 <2.1.2",
    "baz": ">1.0.2 <=2.3.4",
    "boo": "2.0.1",
    "qux": "<1.0.0 || >=2.3.1 <2.4.5 || >=2.5.2 <3.0.0",
    "asd": "http://asdf.com/asdf.tar.gz",
    "til": "~1.2",
    "elf": "~1.2.3",
    "two": "2.x",
    "thr": "3.3.x",
    "lat": "latest",
    "dyl": "file:../dyl"
  }
}
```

### devDependencies

- 개발에만 필요한 의존성들 (빌드, 테스팅 등)
  - 사용자한텐 필요없는 의존성 구분이 가능하다.
- `-D` 옵션으로 추가 가능

### peerDependencies

- `require`하지 않지만, 특정 패키지에서 호환성을 필요로할 때 그 것을 표시하기 위해 사용
- `npm@7`부터는 peerDependencies 가 기본적으로 설치된다.
  - `npm@7`부터는 peerDependencies 호환성이 맞지 않으면 패키지 설치를 막아버린다.

> 예시

```json
{
  "name": "tea-latte",
  "version": "1.3.5",
  "peerDependencies": {
    "tea": "2.x"
  }
}
```

```bash
# package.json이 위와 같을 때 tea-latte를 설치하면
$ npm install tea-latte

# 의존성 그래프는 아래와 같다
# ├── tea-latte@1.3.5
# └── tea@2.2.0
```

## 레퍼런스

- npm Docs : https://docs.npmjs.com/
- npm cli github : https://github.com/npm/cli
- nvm github : https://github.com/nvm-sh/nvm
