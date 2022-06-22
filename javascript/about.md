# Javascript

> HTML, CSS파일로 만들어진 정적인 웹페이지를 동적으로 작동할 수 있도록 변경해주는 객체 기반의 언어로 HTML 문서 내에 기술되고 함께 수행된다.

## 특징

- `싱글스레드`로 동작하는 언어이다. <br />
  => 메인스레드가 하나의 스레드로 되어 있어서, 한번에 하나의 작업만 수행이 가능<br />
- 코드 진행이 `비동기적`으로 처리된다.<br />
  => 특정 코드의 연산에서 시간이 걸릴 경우, 해당 연산이 끝날 때까지 코드의 실행을 멈추지 않고 다음 코드를 먼저 실행하는 특성

### 자바스크립트는 정말 싱글스레드가 맞나?

한개의 스레드에서 작업을 처리하기 때문에 싱글스레드가 맞다. <br />
처리 순서대로 정리를 해보자<br />

1. 함수를 호출하면 `call stack`에는 stack이 하나씩 쌓이게 된다.
2. stack은 `LIFO(Last In First Out)`형식으로 처리되는데, 나중에 들어온 stack이 먼저 처리된다.<br />
3. 이때 `call stack`에서 불러온 함수 중에 비동기적인 함수가 있을 경우엔 `web API`가 이것의 Run함수를 호출한다.<br />
   => DOM, AJAX, setTimeout이 해당된다
4. `web API`에서 처리를 마친 함수는 `callback queue`로 이동시킨다.
5. `callback queue`에 모인 비동기함수들은 `event loop`의 감시를 받는다.<br />
   => 동시에 `call stack`도 감시하면서 `call stack`이 비워지면 다음 단계를 처리한다.
6. queue는 `FIFO(First In First Out)`형식으로 처리된다. 때문에 `call stack`이 비워지면 `callback queue`에 가장 먼저 들어온 함수가 call stack으로 보내진다 = `tick`

event loop를 통해 함수의 실행순서가 결정되고, 단일 스레드지만 event loop를 통해 동시 다발적인 실행처럼 보여진다.
