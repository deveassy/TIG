# Webpack

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://joshua1988.github.io/webpack-guide/assets/img/webpack-bundling.e79747a1.png">
</div>

> `모듈 번들러` (= 빌드) <br />
> 필요한 다수의 자바스크립트 파일을 하나의 자바스크립트 파일로 만들어주는 도구

개발자가 코딩할 때 편의를 위해서 여러 단위로 모듈을 나눠 작업하게 되는데, 브라우저에서 파일 단위의 모듈시스템을 사용하는 것은 네트워크 비용 낭비를 유발할 수 있다.

그렇기 때문에 여러개의 모듈을 하나의 파일로 묶어서 보낼 `모듈 번들러`로서 `webpack`을 사용한다.

### 속성

1.  `Entry`<br />
    webpack에서 웹 자원을 변환하기 위해 필요한 `최초의 진입점`(= `자바스크립트 파일 경로`)<br />
    `entry`를 통해 모듈을 로딩하고 하나의 파일로 묶는다.

    ```javascript
    // webpack.config.js
    module.exports = {
      entry: "./src/index.js",
    };

    // 웹팩 실행 시 index.js를 대상으로 웹팩이 빌드를 수행하는 코드
    ```

    - `entry`속성에 지정된 파일에는 웹 어플리케이션의 전반적인 구조와 내용이 담겨있어야 한다. 웹팩이 이를 통해 모듈들의 연관관계를 이해하고 분석하기 때문
    - 위 코드처럼 엔트리 포인트가 1개인 경우는 SPA 서비스, 멀티 페이지 어플리케이션에서는 특정 페이지로 진입 시 서버에서 해당 정보를 내려주는 형태이기 때문에 엔트리 포인트가 여러개일 수 있다.

      ```javascript
      entry: {
          login: './src/LoginView.js',
          main: './src/MainView.js'
      }
      ```

2.  `Output`<br />
    entry로 묶은 모듈의 결과물을 반환할 위치

    ```javascript
    // webpack.config.js
    module.exports = {
      output: {
        filename: "bundle.js",
      },
    };

    // 객체 형태로 옵션들을 추가해야 함
    ```

    - 최소 `filename` 지정 필요
    - 일반적으로 `path` 속성을 함께 정의하곤 한다.

      ```javascript
      // webpack.config.js
      var path = require('path');

      module.exports = {
          output = {
              filename: 'bundle.js',
              path: path.resolve(__dirname, './dist') // path.resolve() -> 인자로 넘어온 경로들을 조합하여 유효한 파일 경로를 만들어주는 Node.js API
          }
      }
      ```

3.  `Loader`<br />
    webpack은 기본적으로 자바스크립트와 JSON만 빌드가 가능한데, 자바스크립트가 아닌 다른 자원(HTML, CSS, Image ...)을 빌드할 수 있도록 도와주는 속성

    ```javascript
    // webpack.config.js
    module.exports = {
      module: {
        rules: [],
      },
    };
    ```

    - 필요한 이유<br />
      아래의 코드들만으로 웹팩으로 빌드한다고 하면, 아래와 같이 에러가 발생한다.

      ```javascript
      // app.js
      import "./common.css";

      console.log("css loaded");
      ```

      ```javascript
      /* common.css */
      p {
          color: red;
      }
      ```

      ```javascript
      // webpack.config.js
      module.exports = {
        entry: "./app.js",
        output: {
          filename: "bundle.js",
        },
      };
      ```

        <p style="color: red">
        Error in ./common.css<br />
        Module parse failed. Unexpected token<br />
        You may need an approciate loader to handle this file type, currently no loaders are configured to process this file.
        </p>

      - 적용법<br />
        css loader 적용법을 예로 들어본다면, 우선 npm으로 css loader를 설치한 후 웹팩 파일 설정을 변경해주면 된다.

        ```
        npm i css-loader -D
        ```

        ```javascript
        //webpack.config.js
        module.exports = {
          entry: "./app.js",
          output: {
            filename: "bundle.js",
          },
          module: {
            rules: [
              {
                test: /\.css$/,
                use: ["css-loader"],
              },
            ],
          },
        };
        ```

        - `test`: loader를 적용할 파일의 유형 (일반적으로는 정규 표현식을 사용)
        - `use`: 해당 파일에 적용할 loader의 이름

4.  `Plugin`<br />
    webpack의 기본적인 동작 외에 추가적인 기능을 제공하는 속성. loader가 파일을 해석하고 변환하는 과정에 관여하는 반면 plugin은 **결과물의 형태를 바꾸는 역할**을 한다.

    ```javascript
    // webpack.config.js
    module.exports = {
      plugin: [],
    };
    ```

    ➔ plugin의 배열에는 생성자 함수로 생성한 **객체 인스턴스**만 추가될 수 있다.

    ```javascript
    // webpack.config.js
    var webpack = require("webpack");
    var HtmlWebpackPlugin = require("html-webpack-plugin");

    module.exports = {
      plugins: [new HtmlWebpackPlugin(), new webpack.ProgressPlugin()],
    };
    ```

    - `HtmlWebpackPlugin`: 웹팩으로 빌드한 결과물, HTML파일을 생성해주는 plugin
    - `ProgressPlugin`: 웹팩의 빌드 진행률을 표시해주는 plugin

# Babel

> `자바스크립트 컴파일러`<br />
> 브라우저가 이해할 수 있는 문법으로 변환해 주는 도구<br />
> => 최신 ES6 버전을 구버전인 ES5 버전으로 변환해주는 것

- 설치법<br />
  ```
  npm i @babel/core -D
  ```
  - `@babel/core`: babel 사용 시 항상 필요한 패키지
- 예시<br />

  ```javascript
  // ES6부터 도입된 arrow function 사용 시, 에러 발생
  [1, 2, 3].map((n) => n + 1);

  // SyntaxError: Unexpected token
  ```

  이를 babel을 사용하게 되면 일반 function 문법을 사용하도록 변환해준다.

  ```javascript
  // babel을 사용하면 변환되는 코드
  [1, 2, 3].map(function (n) {
    return n + 1;
  });
  ```

## Polyfill

> `최신 ECMAScript 환경을 만들어주는 도구`<br />
> babel이 ES6 => ES5로 변환할 수 있는 것들만 변환하는 작업을 하는데, 대상이 없을 경우엔 에러가 발생하게 된다. 이때 빈 부분을 채워주는 것이 Polyfill이다.

- 추가하는 방법

1.  전역에 폴리필 추가하기<br />
    babel 7.4.0부터 `@babel/polyfill`은 deprecated되고 `core-js`와 `regenerator-runtime`을 직접 사용하는 방법을 제안한다.

    ```javascript
    // index.html
    <script src="https://unpkg.com/core-js-bundle@3.1.4/index.js"></script>
    <script src="https://unpkg.com/regenerator-runtime@0.13.3/runtime.js"></script>
    ```

    ➔ 전역 스코프에 폴리필이 추가되면서 IE 하위 브라우저에서도 `Promise, Map, Set, Object.assign, Array, find` 등의 메서드의 사용이 가능해진다.

2.  Webpack에 포함하고 전역에 폴리필 추가하기<br />
    `entry`파일에서 import해주면 전역 스코프에 폴리필을 추가하는 코드가 함께 번들링된다.

    ```javascript
    npm i --save core-js regenerator-runtime
    ```

    ```javascript
    import "core-js/stable";
    import "regenerator-runtime/runtime";
    ```

---

> 참고하였습니다 :)<br />

- [웹팩 핸드북](https://joshua1988.github.io/webpack-guide/concepts/entry.html#entry)
- [BABEL](https://babeljs.io/docs/en/)
- [바벨(Babel 7) 기본 사용법](https://www.daleseo.com/js-babel/)
