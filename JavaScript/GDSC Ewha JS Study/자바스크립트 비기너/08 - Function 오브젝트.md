# 1. 프로퍼티 리스트, Function 인스턴스 생성

## new Function()

- Function 인스턴스를 생성한다.
- 파라미터에 문자열로 함수의 파라미터와 함수 코드를 작성한다.

```js
var obj = new Function("book", "return book");
obj("JS 책"); // book에 파라미터 값을 넘겨준다.
```

- 파라미터 수에 따라 인스턴스 생성 기준이 다르다.

### 파라미터 2개 이상 작성한 경우

- 마지막 파라미터에 함수에서 실행할 함수 코드를 작성한다.
- 마지막을 제외한 파라미터에 이름을 작성한다.

### 파라미터 하나 작성한 경우

- 함수에서 실행할 함수 코드를 작성한다.
- 파라미터가 없을 때 사용한다.

```js
var obj = new Function("return 1+2;");
console.log(obj()); // 3
```

### 파라미터 작성하지 않은 경우

- 함수 코드가 없는 빈 Function 인스턴스를 생성한다.

<br>

## Function()

- new 연산자를 사용하지 않고 Function 인스턴스를 생성하는 것
- 처리 방법과 파라미터 작성이 new Function()과 같다.

<br>

# 2. 함수 생명 주기

## 함수 분류

### function 분류

- 빌트인 Function 오브젝트
- function 오브젝트
- function 인스턴스(new 연산자 사용)

### function 오브젝트 생성 방법

- function 키워드 사용
- `function getBook(title) {return title};`

### JS 엔진이 function 키워드를 만나면

- 이름이 `getBook`인 function 오브젝트를 생성한다.

<br>

## 함수 생명 주기

```js
function getBook(title) {
  return title;
}
var result = getBook("JS북");
console.log(result);
```

### 함수 호출

- `getBook("JS북");`
- 함수 호출하면서 파라미터 값을 넘겨준다.

### 함수 코드 실행

- JS 엔진 컨트롤(스펙에 작성된 용어, JS 엔진이 현재 처리하고 있는 위치)이 함수의 처음으로 이동한다.
- 파라미터 이름에 넘겨 받은 파라미터 값 매핑한다.
- 함수 코드를 실행한다.
- return 작성에 관계없이 반환 값을 갖고 함수를 호출한 곳으로 돌아간다. (return 값이 없으면 undefined를 가지고 갈 것)

<br>

## length 프로퍼티

- 함수의 파라미터 수가 생성되는 function 오브젝트에 설정된다.
- 함수를 호출한 곳에서 보낸 파라미터 수가 **아니다.**

```js
function add(one, two) {
  return one + two;
}
add(1, 2, 3, 4);
console.log(add.length); // 4가 아니라 2!
// JS는 호출하는 함수의 파라미터 수와 호출받는 함수의 파라미터 수가 갖지 않아도 된다. 또한 타입이 달라도 된다.
```

- JS 엔진이 자동으로 설정한다.

<br>

# 3. 함수 형태, 함수 선언문, 함수 표현식

## 함수 형태

### 함수 선언문

- Function Declaration
- function getBook(book) {...}

### 함수 표현식

- Function Expression
- var getBook = function(book) {...}
- `getBook`은 함수 이름이자 function 오브젝트이다.

<br>

## 함수 선언문

- `function getBook(title){함수 코드}` 형태
- function 키워드, 함수 이름, 블록{}은 핖수로 작성한다.
- 파라미터, 함수 코드는 선택이다.
- 함수 이름ㅇ르 생성한 function 오브젝트의 이름으로 사용한다.

<br>

## 함수 표현식

- `var getBook = function(title) {...}`
- function 오브젝트를 생성하여 변수에 할당한다.
- 변수 이름이 function 오브젝트 이름이 된다.
- 식별자 위치의 함수 이름은 생략이 가능하다.
  - `var name = function abc(){}`에서 `abc`가 식별자 위치의 함수 이름이다.

```js
var getBook = function inside(value) {
  if (value == 102) {
    return value;
  }
  console.log(value);
  return insdie(value + 1);
};
getBook(100);
```

<br>

### 왜 함수 형태가 두 가지일까?

함수 선언문이 먼저 function 오브젝트를 만들고 표현식으로 function 오브젝트를 만든다.  
순서가 다름에 따라 동반되는 처리도 달라진다.

<br>

# 4. 함수 호출

## call()

- `함수명.call(this, 10, 20);`
- 첫 번째 파라미터
  - 호출된 함수에서 this로 참조할 오브젝트
  - 일반적으로 this를 사용하지만 다른 오브젝트를 작성할 수도 있다.

<br>

## apply()

- `함수명.apply(this, [10, 20]);`
- call()과 유사하지만 두 번째 파라미터에 **배열**을 사용한다는 차이점이 있다.
- 파라미터 수가 **유동적일 때** 사용한다.
- call(), apply()의 부가적인 목적?
  - 첫 번째 파라미터에 호출된 함수에서 this로 참조할 오브젝트 사용

<br>

## toString()

- 거의 모든 빌트인 오브젝트에 toString()이 있지만 오브젝트마다 반환되는 형태가 다르다.
- function 오브젝트의 toString()은 함수 코드를 문자열로 반환한다.

<br>

# 5. Argument 오브젝트

## Argument 오브젝트

- 함수가 호출되어 함수 안으로 이동했을 때 arguments 이름으로 생성되는 오브젝트
- 빌트인 오브젝트이다.
- 함수 호출한 곳에서 넘겨준 값을 순서대로 저장한다.
- 호출된 함수에 파라미터 작성한 경우 호출된 함수의 파라미터에도 값을 설정하고 argument 오브젝트에도 저장한다.
  - apply()와 아규먼트 오브젝트 -> 데이터 처리에 유용하다
- 파라미터라고 부른 것은 아규먼트 오브젝트와 구분하기 위한 것이다.

```js
functiong getTotal(one) {
  return one + arguments[1] + arguments[2];
};
var result = getTotal(10, 20, 30); // 10, 20, 30이 arguments에 순서대로 설정된다
console.log(result); // 60

// apply()와 아규먼트 오브젝트
// 사용사례: checkbox로 선택한 수가 유동적일 때
functiong getTotal(one) {
  return one + arguments[1] + arguments[2];
};
var result = getTotal.apply(this, [10, 20, 30]);
console.log(result); // 60
```
