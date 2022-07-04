# 브라우저의 렌더링 과정

> HTML, CSS, JS 등 개발자가 작성한 문서들을 브라우저가 화면에 그려주는 과정<br />
> 각 브라우저는 렌더링을 하기 위해 각 렌더링 엔진을 가지고 있으며, 브라우저마다 종류가 다를 수 있다.

1. <span style="background-color: purple">[Parsing] DOM(<span style="color: gray">Document Object Model</span>)과 CSSOM(<span style="color: gray">CSS Object Model</span>) 생성</span><br />
   입력받은 문자열이 정해진 문법을 모두 따르는지 확인하는 과정

- 가장 먼저 서버로부터 받은 `HTML, CSS`파일을 다운로드 받는다.
- 단순 텍스트파일들이기 때문에, 관리가 용이하도록 `object model`로 생성한다.

2. <span style="background-color: purple">렌더트리 구축

- 이전 단계에서 생성된 DOM, SSSOM을 이용하여 Render tree를 구축한다.
- 텍스트로만 된 이전단계와는 달리, Render tree에는 `스타일정보`가 설정되어있다.
- `실제화면에 표현되는 노드`들로만 구성된다.<br />
  => `display: none`과 같이 화면에 공간을 차지하지 않는 속성이 설정된 노드는 Render tree 구축 과정에서 제외된다. (`visibility: invisible`은 공간은 차지하나 요소가 보이지 않는 것이기 때문에 Render tree에 포함됨)

3. <span style="background-color: purple">[Layout] 렌더트리 배치

- 브라우저의 `뷰포트` 내에서 각 노드들의 정확한 위치와 크기를 계산한다.<br />
  `%, vh, vw` 등의 상대적인 단위들을 실제 화면에 그려지는 `px`단위로 변환한다.
- 뷰포트(그래픽이 표시되는 브라우저의 영역)가 달라질 때마다 매번 계산을 다시 해야 함(상대적인 계산을 사용할 경우)

4. <span style="background-color: purple">[Paint] 렌더트리 그리기

- 이전 단계에서 계산된 Render tree를 이용해 실제 px값으로 채워넣는다.
- 텍스트, 색상, 이미지, 그림자 효과 등의 스타일링이 처리되어 그려진다.
- 스타일이 복잡해질수록 소요시간이 늘어난다.

## 💡렌더링 최적화하기

> 웹 성능을 최적화하기 위한 방법으로, 렌더링을 줄이는 것이 있다.<br />
> Reflow, Repaint 줄이기!

> 추가하기

## DOM 생성중에 `<script>`를 만난다면?

> HTML파서가 DOM 생성 중에 `<script>`태그 등의 **외부 태그**를 만나게 되면, DOM 프로세스를 멈추고 **자바스크립트 엔진**에게 제어 권한을 넘긴다.<br />

다음과 같은 순서로 브라우저 실행이 이루어진다.

1. `<script>`태그를 만나면 웹페이지의 파싱을 일시중지

2. src attribute에 정의된 javascript 파일을 로드 -> 파싱 후 실행

3. 1에서 중단되었던 웹페이지의 파싱을 재실행

이로 인해 `<script>`태그의 위치에 따라서 DOM 생성이 지연될 수 있다는 것을 알 수 있다.<br />

### 해결책은?

때문에 `<body>`태그 가장 마지막에 위치시키는 것을 권장했다. 하지만 이 방법도 완벽한 해결책이 아니다.<br />
=> `<script>`태그를 해석하는 도중에 사용자가 버튼을 클릭하거나 텍스트를 입력해서 제출하는 등의 웹과의 상호작용을 시도하게 되면 스크립트 코드가 해석되지 않은 상태이기 때문에 제대로 동작하지 않는다.

브라우저가 스크립트 파일을 `병렬`로 불러오는 방식을 사용하여 DOM 렌더 과정을 멈추지 않게 선언하는 방법이 있다.
<img width="636" alt="스크린샷 2022-06-20 오후 5 39 09" src="https://t1.daumcdn.net/cfile/tistory/99176A3F5A5C02980A">

- `defer` : 스크립트가 **웹페이지 파싱 완료 직후** 실행

- `async` : 스크립트가 **다운로드 완료 직후** 실행

---

> 참고하였습니다 :)

- https://wormwlrm.github.io/2021/03/27/How-browsers-work.html
- https://pureainu.tistory.com/287
