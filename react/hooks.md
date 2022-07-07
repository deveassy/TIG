# Hooks

> react 16.8v부터 새롭게 추가된 요소로, 기존 **class 바탕의 코드를 작성할 필요 없이** 상태값과 여러 react의 기능을 사용할 수 있도록 도와주는 치트키이다.

hook의 종류에 따른 각각의 사용법을 정리하기보다, hook의 사용 규칙, 같은 카테고리에 있는 종류들을 비교하며 올바르고 **효율적이게 사용하는 법**에 대해 고민해보려고 한다.

## 📍사용 규칙

1. **react 함수 내**에서만 사용해야 한다.
2. **최상위(Top of the level)에서 호출**해야 한다.<br />
   => 반복문, 조건문, 중첩된 함수 안에서 사용해서는 안된다.<br />
   => 컴포넌트가 렌더링 될 때마다 항상 동일한 순서로 hook이 호출 되는 것을 보장하기 위해서

---

## useState와 useRef

#### 공통점

두가지 모두 컴포넌트의 상태값을 동적으로 관리할 수 있다는 점이다.

#### 차이점

- useState

  - 값과 그 값을 변경할 수 있는 setter 함수를 가진 배열을 반환
  - state의 변경이 가능<br />
    => 때문에 컴포넌트의 리랜더링이 발생할 수 있다.
  -

- useRef

  - 하나의 데이터만 반환
  - useRef를 통해 반환된 객체는 컴포넌트 생애 주기 내내 변화하는 값을 가리킨다.
  - 값에 접근하기 위해서는 `current`프로퍼티를 통해 값을 조회
  - 값을 변경하여도 리렌더링이 되지 않음
    => 때문에 컴포넌트에 영향을 미치지 않는다.

    ```javascript
    import React, { useRef } from "react";

    function RefTest() {
      const letter = useRef("");

      const handleClick = () => {
        letter.current = "letter 변경!";
        console.log(letter.current);
      };

      return (
        <div>
          <button onClick={handleClick}>CliCK</button>
        </div>
      );
    }
    ```

    위 코드를 실행하면 console창에는 `letter 변경!`이 출력된다.<br />
    하지만 이는 단지 letter라는 변수에 저장된 값을 변경한 것일 뿐이기 때문에, 컴포넌트의 리랜더링은 일어나지 않고 화면에도 변경점이 없다.

  - e.g., DOM에 접근(input에 포커스를 주기)

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

## useMemo와 useCallback

---

> 참고하였습니다 :)

- [React 공식문서 - hook](https://ko.reactjs.org/docs/hooks-intro.html)
- [React 공식문서 - useLayoutEffect](https://ko.reactjs.org/docs/hooks-reference.html#uselayouteffect)
- [React 공식문서 - useRef](https://ko.reactjs.org/docs/hooks-reference.html#useref)
- [[React] useState vs useRef](https://medium.com/humanscape-tech/react-usestate-vs-useref-4c20713f7ef)
- [useLayoutEffect 훅에 대하여](https://merrily-code.tistory.com/46)
