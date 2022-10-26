## 보일러플레이트 제작기

> Q. 왜 보일러플레이트를 만들게 되었는가?<br>
> 1. CRA(Create React App)는 필요로 하지 않는 디펜던시를 포함하고 있어 개선하고 싶었다.
> 1. 회사에서 프로젝트를 새로 시작하는 경우, 매번 처음부터 세팅해야하는 것이 불편했다. 그래서 회사에서 많이 사용하는 형태의 보일러플레이트를 제작하고 이를 공유해야겠다는 생각을 했다.
> 1. 사수 혹은 선임자가 "이거 내려받아서 쓰면 됩니다."에 끝나는 것이 아닌 "왜 이렇게 사용하는지?"가 궁금했고 프로젝트 설정에 대해 자세하게 알고 사용하고 싶었다.

---

### 목차

1. Project
    - Create project
    - Project initialize
1. React
    - Install
1. TypeScript
    - Install
    - Config
1. Webpack
    - Install
    - Config
1. Eslint & Prettier
    - Install
    - Config

---

### 1.Project

1. Create project
    ```
    // 프로젝트 생성 위치로 이동
    cd /../work

    // boilerplate 폴더 생성
    md boilerplate
    
    // 생성한 boilerplate 폴더로 이동
    cd boilerplate
    ```

1. Project initialize
    ```
    // 프로젝트 초기화
    npm init -y
    ```

---

### 2. React

1. Install
    ```
    // 리액트 설치
    npm install --save react react-dom
    ```

---

### 3. TypeScript

1. Install

    ```
    // 타입스크립트 설치
    npm install -D typescript @types/react @types/react-dom
    ```

1. Config

    ```
    // tsconfig 생성
    npx tsc --init 
    ```

    ```
    // tsconfig.json
    // jsconfig.json
    ```

---

### 4. Webpack

1. Install
    ```
    // webpack 설치
    npm install -D webpack webpack-cli webpack-dev-server

    // webpack 플러그인 설치
    npm install -D html-webpack-plugin copy-webpack-plugin webpack-bundle-analyzer mini-css-extract-plugin

    // webpack 로더 설치
    npm install -D babel-loader ts-loader style-loader css-loader postcss-loader sass-loader sass

    // webpack 설정 병합 패키지 설치
    npm install -D webpack-merge

    // CSS 후처리 패키지 설치
    npm install autoprefixer
    ```

1. Config
    ```
    // webpack.common.js
    // webpack.dev.js
    // webpack.prod.js

    // .babel.rc
    ```

    ```
    // postcss.config.js
    ```

### 5. Eslint & Prettier
1. Install
    ```
    // eslint 설치
    npm install -D @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint
    
    // prettier설치
    npm install -D prettier
    ```

1. Config
    ```
    // .eslintrc.json
    ```