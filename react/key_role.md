# React에서 key의 역할

## key란?

> React가 **어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕는 역할**을 한다. `key`는 엘리먼트에 안정적인 **고유성**을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 한다.

- 통용되는 규칙<br />
  Key를 선택하는 가장 좋은 방법은 리스트의 다른 항목들 사이에서 해당 항목을 고유하게 식별할 수 있는 문자열을 사용하는 것이다. 대부분의 경우 데이터의 `ID`를 key로 사용하곤 한다.
- 렌더링 한 항목에 대한 안정적인 ID가 없다면 최후의 수단으로 항목의 `index`를 key로 사용할 수 있긴 하지만, 항목의 순서가 변경될 가능성이 있을 경우엔 권장하지 않는다.<br />
  ➔ 이로 인해 성능이 저하되거나, state와 관련되어 에러가 발생할 수 있기 때문.

컴포넌트 내에서 어떤 배열을 map함수를 사용하여 리스트를 랜더링 한다고 가정했을 경우, `key`를 사용하지 않으면 경고가 뜬다.

```javascript
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) => (
    <li key={number.toString()}>{number}</li>
  ));
  return <ul>{listItems}</ul>;
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById("root")
);
```

`key`값은 엘리먼트 리스트를 만들 때 필수로 필요한 특수한 문자열 어트리뷰트이다.

## 왜 key가 필요할까?

React의 작동원리인 `virtual DOM`의 랜더링과 관련이 있다.

DOM 노드의 자식들을 재귀적으로 처리할 때, React는 기본적으로 동시에 두 리스트를 순회하고 **차이점이 있으면 변경을 생성**합니다.

예를 들어, 자식의 끝에 엘리먼트를 추가하는 코드를 확인해보자

```javascript
// before
<ul>
  <li>first</li>
  <li>second</li>
</ul>

// after
<ul>
  <li>first</li>
  <li>second</li>
  <li>third</li>
</ul>
```

➔ 이 경우, virtual DOM에선 마지막에 추가된 부분만 변경된 부분으로 인식하여 트리에 추가하게 된다.<br />
하지만, 순서가 일정하게 유지되지 않을 경우엔 같은 리스트에서 한가지만 변경되더라도 전체 리스트를 새로 랜더링해야 하는 문제가 발생한다.

```javascript
// before
<ul>
  <li>Duke</li>
  <li>Villanova</li>
</ul>

// after
<ul>
  <li>Connecticut</li>
  <li>Duke</li>
  <li>Villanova</li>
</ul>
```

---

> 참고하였습니다 :)

- [리스트와 Key](https://ko.reactjs.org/docs/lists-and-keys.html)
- [[React]Key 이해하기](https://developer-talk.tistory.com/102)
- [자식에 대한 재귀적 처리](https://ko.reactjs.org/docs/reconciliation.html#recursing-on-children)
