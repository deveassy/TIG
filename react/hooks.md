# Hooks

> react 16.8v부터 새롭게 추가된 요소로, 기존 **class 바탕의 코드를 작성할 필요 없이** 상태값과 여러 react의 기능을 사용할 수 있도록 도와주는 치트키이다.

hook의 종류에 따른 각각의 사용법이나 정의를 정리하기보다, 같은 카테고리에 있는 종류들을 비교하며 **효율적으로 사용하는 법**에 대해 고민해보려고 한다.

## useState와 useRef

## useEffect와 useLayoutEffect

`useEffect`와 `useLayoutEffect`는 형태가 완전히 동일하다. 그런데 왜 나눠서 만들었을까?<br />
공식문서에도 그렇고, 왠만하면 `useEffect`만 사용하라고 권장한다. 하지만 더 효율적인 hook 사용을 위해 이 둘이 어느 시점에 적용되는지, 어떤 방식으로 동작하는지에 대해 정리해보려 한다.

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FKbBel%2FbtqXb2au60P%2FTqfo1tzjyaTAMEKzctxiSk%2Fimg.png">
</div>

- `useEffect`<br />

  > side effect를 수행하기 위한 hook으로, 데이터 가져오기, 구독 설정하기, 수동으로 DOM을 수정하는 작업을 처리할 수 있다.<br />
  > => class형 컴포넌트의 라이프사이클 메소드인 `componentDidMount`, `componentDidUpdate`, `componentWillUnmount`를 합쳐서 사용 가능한 hook

  - 컴포넌트가 `paint` 된 이후 실행
  - 비동기적(asynchronous) 실행
  - 컴포넌트의 상태값이 useEffect에 의존할 경우 화면 깜빡임 문제가 발생한다.

  ```javascript
  function Effect() {
    const [name, setName] = useState("");

    useEffect(() => {
      setName("eassy");
    }, []);
    return <div>My name is {name}!</div>;
  }
  ```

  위와 같이 코드를 작성하게 되면, 아래와 같은 순서로 코드가 실행된다.

  1. 첫 렌더링 시에 `<div>My name is {name}!</div>` 페인트
  2. 브라우저에 `My name is !` 렌더링
  3. useEffect 실행 후 setName함수 호출되면서 `{name}`자리에 `eassy`가 setting
  4. 브라우저에 리렌더링 -> `My name is eassy!`

     => 이 때, useEffect로 인한 state값이 변경되기 때문에 화면이 깜빡이며 리랜더링이 발생

- `useLayoutEffect`<br />

  > 화면 렌더링 이후에 useEffect가 적용된 후 다시 UI가 변경될 경우 화면 깜빡이는 문제를 해결할 수 있다.

  - DOM 변경(`layout단계 후`)이후 실행
  - 동기적(synchronous) 실행
  - SSR방식을 사용할 경우엔, useEffect도, useLayoutEffect도 자바스크립트가 모두 다운되기 이전에 실행되지 않기 때문에 유의해서 사용해야 한다.

  ```javascript
  function LayoutEffect() {
    const [name, setName] = useState("");

    useLayoutEffect(() => {
      setName("eassy");
    }, []);
    return <div>My name is {name}!</div>;
  }
  ```

  위와 같이 코드를 작성하게 되면, 아래와 같은 순서로 코드가 실행된다.

  1. useLayoutEffect 실행되면서 setName함수 호출
  2. `<div>My name is {name}!</div>` 페인트
  3. 브라우저에 `My name is eassy!` 렌더링

     => DOM이 화면에 그려지기 이전에 useLayoutEffect가 실행되기 때문에, state값이 setting된 채로 첫렌더링이 됨
