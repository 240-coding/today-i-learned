# Arrow Function

- 코드 형태: `(param) => {함수 코드}`
- `function(){}` 의 축약 형태이지만 고려할 사항이 있다.
    - this 참조가 다르다.

# 함수 블록 사용

- 함수 블록과 return 작성 생략
    - ⇒ 앞에서 줄을 분리하면 에러가 나지만 뒤에서는 줄을 분리할 수 있다.

```jsx
const total = (one, two) => one + two;
log(total(1, 2)); // 3
```

- 함수 블록{}만 작성한 형태
    - `undefined` 를 반환한다.
    - 함수 블록에 return을 작성하지 않은 것과 같다.
    - return을 작성하지 않으면 디폴트로 `undefined` 를 반환한다. (JS 문법)

```jsx
const total = (one) => {};
log(total(1)); // undefined
```

- `{key: value}` 를 반환하는 형태
    - {key: value}를 소괄호()로 감싸면 {key: value}를 반환한다.
    - 소괄호를 작성하지 않으면 `undefined` 를 반환한다.

```jsx
const point = (param) => ({book: param});
const result = point("책");
for (const key in result) {
	log(key + ": " + result[key]);
};
// book: 책
```

# 파라미터 사용

- 파라미터가 하나이면 `(param)` 에서 소괄호를 생략할 수 있다.
- 파라미터가 없으면 소괄호만 작성한다.

# 화살표 함수 구조

- 화살표 함수는 일반 함수와 구조가 다르다.
    - `prototype` 과 `constructor` 가 없다.
    - prototype에 메소드를 연결하여 확장할 수 없다.
    - prototype이 없으므로 그만큼 가볍다.
    - `new` 연산자로 인스턴스를 생성할 수 없다.

# arguments 사용 불가

- arguments를 사용할 수 없다.
- arguments 대신에 rest 파라미터를 사용한다.

# 화살표 함수와 this

- strict 모드에서 함수를 호출할 때 함수 앞에 오브젝트 작성은 필수이다.
    - 화살표 함수로 해결할 수 있다.
- 화살표 함수에서 this가 글로벌 오브젝트 참조
    - this 값이 undefined

# this가 정적 스코프 참조

- 화살표 함수에서 정적 스코프의 this를 사용한다.
- 정적 스코프란 엔진이 해석할 때 화살표 함수를 만나면 function 오브젝트를 생성하고 화살표 함수가 속한 스코프를 생성한 오브젝트에 바인딩한다.
- 오브젝트에 바인딩된 스코프의 this를 화살표 함수에서 this로 사용한다.

# 화살표 함수와 인스턴스

- 인스턴스에서 화살표 함수의 작성 위치에 따라 this가 참조하는 오브젝트가 다르다.

# 화살표 함수 특징

- prototype이 없으므로 함수가 가볍다.
- constructor가 없으므로 new 연산자로 인스턴스를 생성할 수 없다.
- 화살표 함수에 this가 없다.
    - 화살표 함수로 Function 오브젝트를 생성할 때 정적으로 화살표 함수가 속한 스코프의 this를 화살표 함수에 바인딩한다.
    - 바인딩된 this 참조가 바뀌지 않으며, 화살표 함수에서 this로 사용한다.
    - 일반 함수는 call() 등으로 바꿀 수 있다.
- **메소드보다 함수로 사용하는 것이 효율성이 높다.**
-
