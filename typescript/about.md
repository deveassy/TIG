# Typescript

> Javascript의 대체 언어의 하나로서 `Javascript의 Superset(상위확장)`으로, `Javascript에 타입을 부여`한 언어

`suerset이란?`<br />
타입스크립트는 **자바스크립트의 모든 기능의 사용이 가능**하며, 더나아가 타입스크립트만의 **class, interface 등 객체지향 프로그래밍 패턴이 사용 가능**한, `상위확장`의 개념이다.

## 핵심원리

값이 가지는 형태에 초점을 맞추는 타입체킹<br />
=> 결국 타입이 필요한 이유는 `메모리를 절약하기 위해서`이다. 메모리에 저장된 것을 읽어들일때, 값을 메모리에 저장할때, 값이 저장되어 있는 것을 참조할 때의 크기들을 알아야 하기 때문이다.

## 작동원리

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://user-images.githubusercontent.com/58814562/175862687-194e108a-808a-4b90-b1ab-ce54c54c7613.png">
</div>

- AST(Abstract Syntax Tree) - `추상화 문법트리`<br />
  프로그래밍언어는 컴파일러를 통해 파싱하여 AST의 자료구조 형태의 코드로 만들어진다.

## 특징

<div align="center">
<img width="367" alt="스크린샷 2022-06-27 오후 1 52 46" src="https://velog.velcdn.com/images%2Fggob_2%2Fpost%2F162f7362-ee80-445a-babb-156b3b10359b%2FTS%20vs%20JS.png">
</div>

- `Javascript`는 `동적타입의 interprter 언어`로 run time에서 오류를 발견하는 반면에,<br />
  `Typescript`는 `정적타입의 compile 언어`로, 타입스크립트 컴파일러 또는 바벨을 통해 javascript로 변환되는 과정을 거치며 코드 작성 단계에서 오류를 발견할 수 있다. - 미리 타입을 지정하기 때문에 코드의 가독성이 높아진다. - 자바스크립트의 단점인 타입 안정성을 보장해준다. - 객체나 변수를 선언할 때마다 매번 타입 지정이 필요하다. - 타입 지정을 위한 코드의 추가로 인한 코드량이 증가한다. => 컴파일 시간이 늘어남
- `객체지향 프로그래밍`을 지원한다.<br />
  => ES6에서 새롭게 사용된 문법을 포함하고 있으며 class, interface, 상속, 모듈 등과 같은 객체 지향 프로그래밍 패턴을 제공한다.
