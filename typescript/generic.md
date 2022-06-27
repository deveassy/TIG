# Generic(제네릭)

> `데이터의 타입을 일반화(Generalize)`한다는 의미로, 자료형을 특정하지 않고 여러 타입을 사용할 수 있도록 해준다.<br />
> => 즉 선언시점이 아닌, `생성 시점에 타입을 명시`하여 하나의 타입에 한정되는 것이 아닌 여러 타입을 사용할 수 있도록 해주는 기법.

## generic, 왜 사용할까?

제네릭을 사용하지 않을 경우엔 두가지 방법이 있다.

```typescript
// 1. the indentify function a specific type
const indentify = (arg: number): number => {
  return arg;
};

// 2. any type
const indentify = (arg: any): any => {
  return arg;
};
```

- 1번의 경우엔 확실한 타입 지정/체크가 가능하지만, 범용성이 떨어진다.<br />
  => arg와 리턴값에는 number 타입만 가능
- 2번의 경우엔 데이터의 타입을 제한할 수 없으며, indentify 함수를 통해 어떤 타입의 값이 반환되는지 알 수 없다.<br />
  => 불필요한 타입 변환을 하기 때문에 프로그램 성능에도 영향을 끼치게 된다.

때문에 제네릭을 사용하게 되면 따로 타입 변환을 할 필요가 없어서 프로그램 성능이 향상된다.

## generic, 어떻게 쓸까?

> 어떤 값이 반환되는지 표시하기 위해 인수의 타입을 캡쳐하는 방법이 필요하다. 값이 아닌 타입에 적용되는 `타입변수`를 사용해서 타입지정을 한다.<br />
> => 관용적으로 변수타입(type)의 알파벳 `T`를 사용한다.

```typescript
const indentify<T> = (arg: T):T => {
    return arg;
}
```

indentify()에 `T라는 타입변수`를 추가함으로서 `T`는 유저가 준 인수의 타입을 캡쳐한 후 이 정보를 추후에 사용할 수 있도록 기억하고 반환타입으로 다시 사용하게 된다.

이 함수는 타입을 불문하고 동작하기 때문에 `제네릭`이라고 할 수 있다. any 타입을 사용하는 것과는 달리 인수와 반환 타입에 number 타입을 사용한 위의 예제만큼 정확하다.(어떤 정보도 잃지 않는다는 것)

#### 호출방법

1. 함수에 타입 인수를 포함하여 모든 인수를 전달

```typescript
const output = identify<string>("myString"); // 출력타입 = string
```

2. 타입인수 추론 => 사용자가 전달하는 인수에 따라 컴파일러가 자동으로 type값을 정하게 하는 것

```typescript
const output = identify("myString"); // 출력타입 = string
```

=> 컴파일러가 인수 `"myString"`을 보고 타입을 `string`으로 지정한다. 인수추론은 코드를 간결하게 하지만 복잡한 코드에서 컴파일러가 타입을 유추하기 힘든 경우엔 **명시적인 타입 인수 전달**이 필요하다.

---

> 참고하여 작성하였습니다 :) <br />

- [Generic](https://www.typescriptlang.org/ko/docs/handbook/2/generics.html#handbook-content)
- [[typescript]Generic 제네릭](https://velog.io/@edie_ko/TypeScript-Generic-%EC%A0%9C%EB%84%A4%EB%A6%AD-feat.-TypeScript-%EB%91%90-%EB%8B%AC%EC%B0%A8-%ED%9B%84%EA%B8%B0)
