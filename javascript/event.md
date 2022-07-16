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

---

> 참고했습니다 :)

- [[JAVASCRIPT.INFO] 버블링과 캡쳐링](https://ko.javascript.info/bubbling-and-capturing)
- [이벤트 버블링, 이벤트 캡쳐 그리고 이벤트 위임까지](https://joshua1988.github.io/web-development/javascript/event-propagation-delegation/)
