# React의 Lifecycle

React에서 component의 lifecycle은 페이지 랜더링 전 준비과정에서부터 페이지가 사라질 때 끝나게 된다.<br />
총 세가지 카테고리로, mount, update, unmount로 나뉘어진다.<br />

- Mount
  > DOM이 생성되고 웹 브라우저 상에 나타내는 때
- Update
  > 컴포넌트가 업데이트 되는 때
  - props가 변경될 때
  - state가 변경될 때
  - 부모 컴포넌트가 리렌더링 될 때
  - this.forceUpdate를 통해 강제로 렌더링을 트리거 할 때
- Unmount
  > DOM에서 컴포넌트를 제거할 때

불필요한 업데이트를 하지 않기 위해서, 클래스형 컴포넌트에서는 `라이프사이클 메서드`를, 함수형 컴포넌트에서는 `hook`을 사용해서 효율적인 작업 처리를 해보자.

---

## class형 컴포넌트의 lifecycle

> lifecycle이 **컴포넌트 자체**에 중점이 맞춰져있다.

#### Mount

1. **constructor**<br />
   컴포넌트 생성 시 마다 호출하는 클래스 생성자 메서드 (state, context, defaultProps 저장)
2. **getDerivedStateFromProps**<br />
   props의 값을 state에 넣을 때 호출하는 메서드
3. **render**<br />
   UI를 렌더링하는 메서드
4. **componentDidMount**<br />
   컴포넌트가 브라우저상에 나타난 이후에 호출하는 메서드<br />
   ➔ DOM에 접근이 가능함 = Ajax나 setTimeout 등의 비동기 작업이 가능

#### Update

1. **getDerivedStateFromPorps**<br />
   mount 때 호출되어 업데이트 시작 전에 실행됨<br />
   ➔ props의 변화에 따라 state도 변화를 주고 싶을 때 사용
2. **shouldComponentUpdate**<br />
   컴포넌트가 리렌더링될 지 결정하는 메서드<br />
   ➔ **성능 최적화 작업**을 위한 메서드, true를 반환하면 다음 사이클로, false를 반환하면 작업 중지
3. **render**<br />
4. **getSnapshotBeforeUpdate**<br />
   컴포넌트의 변화를 DOM에 반영하기 직전에 호출하는 메서드
5. **componentDidUpdate**<br />
   컴포넌트의 업데이트 작업 직후 호출하는 메서드

#### Unmount

- **componentWillUnmount**<br />
  컴포넌트가 소멸될 때 호출하는 메서드<br />
  ➔ 여기선 주로 이전에 연결되었던 이벤트 리스너들을 제거하는 작업을 한다.

## function형 컴포넌트의 lifecycle

> lifecycle이 **특정 데이터**에 중점이 맞춰져있다.

hook 중에서 side effect를 수행하기 위해 사용되는 `useEffect`를 통해 클래스형 컴포넌트의 라이프사이클을 어느 정도 구현할 수 있다.<br />
클래스형 컴포넌트에서는 componentDidMount, componentDidUpdate, componentWillUnmount 메서드를 한 컴포넌트에서 한번씩만 사용했다면, 함수형 컴포넌트에서는 useEffect의 개수만큼 사용할 수 있다.<br />
`useEffect = componentDidMount + componentDidUpdate + componentWillUnmount`

#### Mount

`useEffect`의 2번째 인자인 배열을 비운 채로 두면, 컴포넌트가 마운트되었을 때에만 `useEffect` 내부의 작업이 실행된다.

```javascript
useEffect(() => {
  console.log("Mount 되었을 때에만!");
}, []);
```

#### Update

`useEffect`의 2번째 인자인 배열에 넣은 값에 따라 라이프사이클을 정할 수 있다.<br />
➔ 컴포넌트가 처음 렌더링 될 때 실행되고, 값의 변화에 따라 실행된다. = `componentDidMount` + `componentDidUpdate` 한 것과 같다.

```javascript
const [count, setCount] = useState(0); // count라는 state 생성

...

useEffect(() => {
    console.log("Update 되었을 때에!"); // 첫 마운트 시에 찍히고, count가 업데이트 될 때마다도 찍힘
}, [count]);
```

#### Unmount

`componentWillUnmount`의 역할을 하기 위해서, `return` 함수를 제공하면 된다.<br />
이 때는 주로, setInterval이나 setTimeout을 사용해서 mount 시에 등록했던 작업을 제거할 때, 즉 clearInterval이나 clearTimeout과 같은 작업을 한다.<br />
➔ 클리너함수, 뒷정리 함수라고 이해하면 된다.

```javascript
useEffect(() => {
  console.log("Mount 되었을 때에만!");
  return () => {
    console.log("Unmount 될 때");
  };
}, []);
```
