# 브라우저의 렌더링 과정

> HTML, CSS, JS 등 개발자가 작성한 문서들을 브라우저가 화면에 그려주는 과정<br />
> 각 브라우저는 렌더링을 하기 위해 각 렌더링 엔진을 가지고 있으며, 브라우저마다 종류가 다를 수 있다.

1. <span style="background-color: purple">DOM(<span style="color: gray">Document Object Model</span>)과 CSSOM(<span style="color: gray">CSS Object Model</span>) 생성

- 가장 먼저 서버로부터 받은 `HTML, CSS`파일을 다운로드 받는다.
- 단순 텍스트파일들이기 때문에, 관리가 용이하도록 `object model`로 생성한다.

2. <span style="background-color: purple">렌더트리 구축

- 이전 단계에서 생성된 DOM, SSSOM을 이용하여 Render tree를 구축한다.
- 텍스트로만 된 이전단계와는 달리, Render tree에는 `스타일정보`가 설정되어있다.
- `실제화면에 표현되는 노드`들로만 구성된다.<br />
  => `display: none`과 같이 화면에 공간을 차지하지 않는 속성이 설정된 노드는 Render tree 구축 과정에서 제외된다. (`visibility: invisible`은 공간은 차지하나 요소가 보이지 않는 것이기 때문에 Render tree에 포함됨)

3. <span style="background-color: purple">렌더트리 배치(Layout)

- 브라우저의 `뷰포트` 내에서 각 노드들의 정확한 위치와 크기를 계산한다.<br />
  `%, vh, vw` 등의 상대적인 단위들을 실제 화면에 그려지는 `px`단위로 변환한다.
- 뷰포트(그래픽이 표시되는 브라우저의 영역)가 달라질 때마다 매번 계산을 다시 해야 함(상대적인 계산을 사용할 경우)

4. <span style="background-color: purple">렌더트리 그리기(Paint)

- 이전 단계에서 계산된 Render tree를 이용해 실제 px값으로 채워넣는다.
- 텍스트, 색상, 이미지, 그림자 효과 등의 스타일링이 처리되어 그려진다.
- 스타일이 복잡해질수록 소요시간이 늘어난다.

## 💡렌더링 최적화하기

> 웹 성능을 최적화하기 위한 방법으로, 렌더링을 줄이는 것이 있다.<br />
> Reflow, Repaint 줄이기!

> 추가하기
