# useState와 useRef

## 공통점

두가지 모두 컴포넌트의 상태값을 동적으로 관리할 수 있다는 점이다.

## 차이점

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

---

> 참고하였습니다 :)

- [[React] useState vs useRef](https://medium.com/humanscape-tech/react-usestate-vs-useref-4c20713f7ef)
- [React 공식문서 - useRef](https://ko.reactjs.org/docs/hooks-reference.html#useref)
