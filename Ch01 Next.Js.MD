작업하다 실수로 파일 날려서 챕터 1,2 는 짧게 요약하겠다.. 흑흑

## 챕터 01 넥스트(Next.js)

- Next.js 를 왜 사용하는가? 리액트의 단점 때문

    - SPA와 SSR(Server-Side-Rendering)의 단점을 해결하기 위해서 리액트(SPA)에 서버 사이드 렌더링의 기능을 더하였다.

    - 리액트에 서버 사이드 렌더링 기능을 추가하려면 웹 서버를 만들어주고, 웹팩 설정, 데이터 로딩, 코드 스플리팅 등 복잡한 과정을 필요로 하는데, 넥스트를 사용한다면 이러한 것들을 설정하지 않고 사용할 수 있게 된다. 개발 환경을 설정하는 번거로움을 줄일 수 있다.


    - 사전 렌더링 및 서버 사이드 렌더링

    - Hot Code Reloading을 지원하는 개발 환경 ( 개발 모드일 때 소스 코드를 저장하면 오른쪽 하단에 다음과 같은 삼각형 애니메이션이 생긴다.)

    - 자동 코드 분할 ( 코드의 모든 가져오기가 번들로 묶여 각 페이지와 함께 제공, 불필요한 코드가 페이지에 로드되지 않게 된다.)

    - 설정이 필요 없다. (웹팩과 바벨을 사용하고 있고, 서버 사이드 렌더링 및 개발에 필요한 설정이 이미되어 있다.)

    - 타입스크립트 내장

    - 파일기반 내비게이션 기능

    - styles-jsx 지원

***

### CNA 를 사용하여 넥스트 설치하기

```
$ npx create-next-app
```
> 프로젝트 이름을 입력하고 진행하자.

- package.json 에 만들어진 scripts 명령어 들을 설명하면 다음과 같다.

    - next dev: 개발 환경의 넥스트 실행, 핫 코드 리로딩 지원
   
    - next build : 넥스트 애플리케이션 번들을 만든다.

    - next start: 빌드된 넥스트 애플리케이션을 실행한다.


## 넥스트 수동 설치하기

```
mkdir next-app
cd next-app

yarn init-y

yarn add next react react-dom
```

- Eslint 및 Prettier 설치하자. 책 참조

```
$ npm install -g eslint

```

_.eslintrc.js_
```javascript
module.exports = {
  env: {
    browser: true,
    es6: true,
  },
  extends: ["airbnb"],
  globals: {
    Atomics: "readonly",
    SharedArrayBuffer: "readonly",
  },
  parser: "@typescript-eslint/parser",
  parserOptions: {
    ecmaFeatures: {
      jsx: true,
    },
    ecmaVersion: 2018,
    sourceType: "module",
  },
  plugins: ["react", "@typescript-eslint"],
  rules: {
    quotes: ["error", "double"], //더블 쿼터 사용
    "@typescript-eslint/quotes": ["error", "double"], //더블 쿼터 사용
    "no-unused-vars": "off", //사용안한 변수 경고 중복
    "@typescript-eslint/no-unused-vars": "warn", //사용안한 변수는 경고
    "jsx-a11y/control-has-associated-label": "off", // 상호작용하는 엘리먼트에 label을 넣는다
    "react/no-array-index-key": "off", // key값으로 index를 사용할수 있다.
    "comma-dangle": "off", // 마지막에 , 을 넣어주지 않는다.
    "arrow-body-style": "off", //화살표 함수 안에 return을 사용 할 수 있다.
    "react/no-unescaped-entities": "off", //문자열 내에서 " ' > } 허용
    "react/prop-types": "off", //proptypes를 사용하지 않는다.
    "object-curly-newline": "off", // { 다음 줄 바꿈을 강제로 사용하지 않는다.
    "react/jsx-one-expression-per-line": "off", //한라인에 여러개의 JSX를 사용 할 수 있다.
    "implicit-arrow-linebreak": "off", // 화살표 함수 다음에 줄 바꿈을 사용할 수 있다.
    "no-shadow": "off", //파일 내에서 중복 이름을 사용 할 수 있다.
    "spaced-comment": "off", //주석을 뒤에 달 수 있다.
    "operator-linebreak": "off", //연산자 다음 줄 바꿈을 사용 할 수 있다.
    "react/react-in-jsx-scope": "off", // jsx를 사용하여도 React를 꼭 import 하지 않아도 된다.
    "react/jsx-props-no-spreading": "off", //props를 스프래드 할 수 있다.
    "jsx-a11y/anchor-is-valid": "off", // next js에서는 a에 href없이 사용
    "global-require": "off", //함수 내에서 require 사용가능
    "jsx-a11y/label-has-associated-control": "off", //label htmlFor을 사용하지 않아도 된다.
    "import/prefer-default-export": "off", //export default 를 사용하라.
    "no-param-reassign": "off",
    "react/jsx-curly-newline": "off", // jsx안에 }를 새로운 라인에 사용할 수 있다.
    "no-use-before-define": "off", // 선언하기 전에 사용할수 없다. 중복
    "@typescript-eslint/no-use-before-define": ["warn"], // 선언하기 전에 사용 한다면 경고
    "no-case-declarations": "off", // case문 안에서 변수 선언 사용하기
    "react/jsx-filename-extension": [
      1,
      { extensions: [".js", ".jsx", ".tsx"] }, //jsx사용가능한 확장자 설정
    ],
    "import/extensions": [
      "error",
      "ignorePackages",
      {
        js: "never",
        jsx: "never",
        ts: "never",
        tsx: "never",
      }, //import 시 확장자명은 사용하지 않는다.
    ],
  },
  settings: {
    "import/resolver": {
      node: {
        extensions: [".js", ".jsx", ".ts", ".tsx", ".d.ts"],
      },
    },
  },
};
```




