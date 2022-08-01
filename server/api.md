# API(Application Programming Interface)

> API 맥락에서의 `applictaion`은 고유한 기능을 가진 모든 소프트웨어라고 말할 수 있다. <br />따라서, `application`을 서로 연결하여 통신할 수 있게 해주는, `Interface`를 뜻한다.

## 그럼 SDK는 뭐야?

> SDK(Software Development Kit)는 **소프트웨어 개발도구 모음**으로, 프로그램 및 응용프로그램 개발의 복잡성을 줄여주는 강력한 기능 집합을 말한다. SDK에는 API, IDE, 문서, 라이브러리, 코드 샘플 및 기타 유틸리티가 포함되어있다.

## API의 작동방법

- SOAP(<span style="color: #888">Simple Object Access Protocol</span>) API<br />
  다른 언어로 다른 플랫폼에서 빌드된 애플리케이션이 통신할 수 있도록 설계된 최초의 `표준 프로토콜`로, 클라이언트와 서버가 XML을 사용하여 메세지를 교환한다.

- RPC(<span style="color: #888">Remote Procedure Call</span>) API<br />
  원격에 위치한 프로그램을 로컬에 있는 프로그램처럼 사용할 수 있게 해주며, 클라이언트가 서버에서 함수나 프로시저를 완료하면 서버가 출력을 클라이언트로 다시 전송한다.

- Websocket API<br />
  JSON 객체를 사용하여 데이터를 전달하는 최신 웹 API로, 클라이언트앱과 서버간의 양방향 통신을 지원한다.

- REST API<br />
  클라이언트가 서버에 요청을 데이터로 전송하고, 서버는 클라이언트의 입력을 사용하여 내부 함수를 시작하고 출력데이터를 다시 클라이언트에 반환한다.

### REST란?

> REpresentational State Transfer의 약자로, 자원을 이름(자원(resource)의 표현(presentation))으로 구분하여 해당 자원의 상태를 주고받는 모든 것<Br />
> = HTTP URI(Uniform Resource Identifier)를 통해 자원을 명시하고, `HTTP Method`(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 `CRUD(Create, Read, Update, Delete) Operation`을 적용하는 것을 의미한다.

REST는 자원 기반의 구조(ROA - Resource Oriented Architecture) 설계의 중심에 Resource가 있고, HTTP Method를 통해 Resource를 처리하도록 설계 된 아키텍쳐를 의미한다.<br />
웹 사이트의 이미지, 텍스트, DB 내용 등의 모든 자원에 고유한 id인 HTTP URI를 부여한다.

#### REST의 특징

- Server-Client 구조
- Stateless(무상태)
- Cacheable(캐시 처리 가능)
- Layered System(계층화)
- Uniform Interface(인터페이스 일관성)

#### REST의 장단점

- 장점
  - HTTP 프로토콜의 인프라를 그대로 사용하기 때문에 별도의 인프라 구축이 필요하지 않음
  - HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능
  - REST API 메세지가 의도하는 바를 명확하게 나타내기 때문에, 의도하는 바를 쉽게 파악할 수 있음
  - 서버와 클라이언트의 역할을 명확하게 분리
- 단점
  - 표준 자체가 존재하지 않아 정의가 필요
  - 사용 가능한 HTTP 메소드가 4가지로 제한적
  - 브라우저를 통한 테스트가 잦은 서비스라면 URL보다 Header 정보의 값을 처리해야 하기 때문에 전문성이 요구된다
  - 구형 브라우저에서는 호환되지 않아 지원되지 않는 동작도 존재

데이터 요청이 REST API로 전송될 때, 일반적으로 `HTTP`를 통해 이루어지는데, 이 요청을 수신하면 <span style="color: orange">REST용으로 설계된 API가 HTML, XML, 텍스트, JSON 등의 다양한 형식으로 메세지를 반환할 수 있게 된다.</span><br />
특히, JSON(<span style="color: #888">Javascript Object Notation</span>)은 어떤 프로그래밍 언어로든 읽을 수 있고, 인간과 기계가 모두 읽기 가능하며 경량화 되어있기 때문에 선호되는 형식이다. 이런 이유들로 인해 RESTful API는 보다 유연하고 설정이 쉽다는 장점이 있다.

### REST API의 특징

- REST 기반으로 시스템을 분산해 확장성과 재사용성을 높여 유지보수 및 운용을 편리하게 한다.
- REST는 HTTP 표준을 기반으로 구현하기 때문에 HTTP를 지원하는 프로그램 언어로 클라이언트, 서버를 구현할 수 있다.
- REST API를 제작하면 클라이언트 뿐 아니라 자바, C#, 웹 등을 통해 클라이언트를 제작할 수 있다.

### RESTful이란?

> REST 원리를 따르는 시스템을 RESTful이란 용어로 지칭한다.

#### RESTful의 목적

- 이해하기 쉽고, 사용하기 쉬운 REST API를 만드는 것
- RESTful하지 못한 경우를 예로 들어보자면,
  - CRUD기능을 모두 `POST`로만 처리하는 API
  - route에 resource, id 외의 정보가 들어가는 경우

> 추가 정리가 필요함

---

> 참고하였습니다 :)

- [[AWS]API](https://aws.amazon.com/ko/what-is/api/)
- [REST와 SOAP 비교](https://www.redhat.com/ko/topics/integration/whats-the-difference-between-soap-rest)
- [SDK, API의 개념과 차이점](https://doozi0316.tistory.com/entry/SDK-API%EC%9D%98-%EA%B0%9C%EB%85%90%EA%B3%BC-%EC%B0%A8%EC%9D%B4%EC%A0%90)
- [REST란? REST API란? RESTful이란?](https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html)
