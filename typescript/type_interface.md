# Type vs Interface

Typescript에서 타입을 지정하기 위해 사용하는 키워드가 두가지 있다.<br />
이 두가지는 매우 비슷하기 때문에 어떤 차이를 가지고 사용하는지에 대한 개념이 필요할 것 같아 정리를 해본다.

## 차이점

#### Type

- IDE에서 Type으로 정의한 타입에 커서를 올리면 `내부 프로퍼티를 확인`할 수 있기 때문에 디버깅에 용이하다.
- 중복작성이 불가능하고 타입 확장을 위해서는 `&` 키워드를 사용한다.<br />

```typescript
type Test = {
  name: string;
};

type Test = {
  age: number;
};

// Duplicate identifier 'Test'

// &를 사용한 타입 확장법
type Test2 = Test & {
  age: number;
};
```

#### Interface

- IDE에서 Interface로 정의한 타입에 커서를 올리면 해당 `타입명만 확인`이 가능하다.
- 중복 작성이 가능하며 확장성에 용이하다.<br />

```typescript
interface Test {
  name: string;
}

interface Test {
  age: number;
}

const mainTest: Test = {
  name: "james",
  age: 20,
};

// extends를 통한 타입 확장법
interface Test2 extends Test {
  id: number;
}
```

- `객체`에만 사용이 가능하다. => 리터럴 타입에는 사용이 불가능

## 기존에 정의한 타입에서 특정 타입을 사용하기

기존 객체형 타입의 `key값`에 접근하여 특정 타입을 사용할 수 있다.

```typescript
interface Person {
  name: string;
  age?: number;
  job?: string;
}

interface Developer extends Person {
  skill: string[];
}

// 원시형 데이터 예시
type Student = Person["name"]; // string type
const student: Student = "eassy";

// 객체형 데이터 예시
interface Student {
  result: Person["name"] | Person["age"]; // string or number type
}
const student: Student = { result: 20 };
```
