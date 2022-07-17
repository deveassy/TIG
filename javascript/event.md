# event-bubbling

> 한 요소에 이벤트 발생 시, 이 요소에 할당된 이벤트 핸들러가 동작하는데 이어서, 이 요소를 감싸고 있는 부모 요소의 핸들러까지 동작하게 된다.<br />
> => 가장 최상단의 요소를 만날 때 까지 이 과정이 반복되면서 각 요소에 할당된 핸들러가 모두 동작한다.

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://joshua1988.github.io/images/posts/web/javascript/event/event-bubble.png">
</div>

### 예시

```javascript
<form onClick="alert('form')">
  <div onClick="alert('div')">
    <p onClick="alert('p')"></p>
  </div>
</form>
```

위의 코드에서 가장 안쪽의 `<p>`를 클릭하면 다음과 같이 동작한다.

1. `<p>`에 할당된 핸들러(onClick)가 동작
2. `<p>`를 감싼 `<div>`에 할당된 핸들러(onClick)가 이어서 동작
3. `<div>`를 감싼 `<form>`에 할당된 핸들러(onClick)가 이어서 동작
4. `document` 객체를 만날 때 까지 각 요소에 할당된 핸들러가 동작

⚠️ 각 태그마다 **이벤트가 등록**되어 있기 때문에 상위 요소로 이벤트가 전달되는 것이다. 만약 이벤트가 `<p>` 태그에만 달려 있다면 위와 같은 동작 결과는 확인할 수 없다.

# event-capturing

> 이벤트 버블링과는 반대로, 특정 이벤트가 발생했을 때 최상위 요소인 body 태그에서 해당 태그를 탐색해 내려가는 동작방법

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://joshua1988.github.io/images/posts/web/javascript/event/event-capture.png">
</div>

이벤트 캡쳐링은 실제로 자주 쓰이진 않지만, `addEventListener()`에 옵션을 설정해서 사용할 수 있다. 그러면 이벤트 버블링과 반대방향으로 탐색하게 된다.

```javascript
div.addEventListener("click", 실행함수, {
  capture: true,
});
```

# event-delegation

> 하위 요소에 각각 이벤트를 붙이지 않고 상위 요소에서 하위 요소의 이벤트들을 제어하는 방식

### 예시

todo list를 만든다고 가정했을 때, checkbox를 만드는 `input` 엘리먼트를 생성할 때마다 이벤트를 추가해야 한다면 굉장히 비효율적일 것이다.<br />
때문에, `<input>`의 상위요소인 `<ul>`에 이벤트 리스너를 달아놓고, 하위에서 발생한 클릭 이벤트를 감지하도록 설정하면 된다. <br />

두가지 방법을 비교해보자.

```html
<div>
  <h1>Todo-list</h1>
  <ul class="itemList">
    <li>
      <input type="checkbox" id="item1" />
      <label for="item1">리스트 1</label>
    </li>
    <li>
      <input type="checkbox" id="item2" />
      <label for="item2">리스트 2</label>
    </li>
  </ul>
</div>
```

1. 화면 내에 있는 모든 `<input>`에 각각 이벤트리스너 추가하는 방법

   ```javascript
   var inputs = document.querySelectorAll("input");
   inputs.forEach(function (input) {
     input.addEventListener("click", function (evnet) {
       alert("clicked!");
     });
   });
   ```

2. `<input>`를 감싸고 있는 `<ul>`에 이벤트리스너를 달아놓은 후, 하위에서 발생하는 이벤트를 감지하도록 하는 방법

   ```javascript
   var itemList = document.querySelector(".itemList");
   itemList.addEventListener("click", function (event) {
     alert("clicked!");
   });
   ```

1번의 경우, 새롭게 `<input>`가 추가될 경우엔, 추가할 때마다 일일이 이벤트리스너 또한 추가하는 작업이 필요하다. <br />
하지만 2번의 경우엔 `<input>`를 포함한 `<ul>`에 이벤트리스너를 달아 새롭게 `<input>`이 추가되더라도 상위요소에서 이벤트를 감지하기 때문에, 새로 추가해야 하는 작업이 필요 없게 된다.

---

> 참고했습니다 :)

- [[JAVASCRIPT.INFO] 버블링과 캡쳐링](https://ko.javascript.info/bubbling-and-capturing)
- [이벤트 버블링, 이벤트 캡쳐 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
