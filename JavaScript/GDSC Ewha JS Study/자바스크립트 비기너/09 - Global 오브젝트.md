# 1. Global 오브젝트 개요, Global 함수, 변수

## Global 오브젝트 개요

- 모든 `<script>`를 통해 하나만 존재한다.
  - new 연산자로 인스턴스를 생성할 수 없다. (하나만 존재하기 때문에 애초에 생성할 필요가 없다.)
  - 모든 코드에서 공유된다. (여러 파일에서 사용할 수 있다. 파일이 달라도 전체가 하나!)
- 이름(Global)은 있지만 오브젝트 실체가 없고 오브젝트를 작성 및 사용할 수 없다.

<br>

## Global 오브젝트 함수, 변수

- Global 오브젝트의 함수, 변수를 **Global 함수, Global 변수**라고 부른다.
- 함수 안에 작성한 것을
  - 지역 함수, 로컬 함수라고 부른다.
  - 지역 변수, 로컬 변수라고 부른다.
- 일반적으로 그냥 함수는 함수 안에 작성한 것을 의미한다.
- 확실히 구분을 하기 위해서는 Global 함수, 지역 함수라고 명시하는 게 좋다.
- `전역 객체`라고 부르기도 하지만 Global은 오브젝트 이름이다. 여기서는 글로벌 오브젝트라고 표기한다.

<br>

# 2. Global 프로퍼티, 프로퍼티 리스트

- NaN, infinity, parseInt(), parseFloat(), eval(), encodeURI() 등
- eval() 함수는 문자열을 JS 코드로 간주한 후에 **실행**까지 한다. 문자열 안에 악의적인 코드를 넣는다면 문제가 될 수 있다. 이런 보안 관련 문제 때문에 eval() 함수는 되도록 쓰지 않는 것이 좋다.

<br>

## Global 프로퍼티

### Global 프로퍼티 종류

- NaN: Not-a-Number
- Infinity: 무한대
- undefined: undefined

<br>

- 상수 개념으로 사용된다.
  - 외부에서 프로퍼티 값 변경할 수 없다.
- `delete 연산자`로 삭제할 수 없다.

```js
console.log(NaN); // NaN
console.log(Infinity); // Infinitiy
console.log(undefined); // undefined
```

- `Number.MAX_VALUE`처럼 프로퍼티 앞에 오브젝트 이름을 작성해야 하지만 글로벌 오브젝트는 실체가 없으므로 프로퍼티 이름만 작성한다.
- 오브젝트 이름을 작성하지 않으면 글로벌 프로퍼티로 인식한다.
- 이들은 Window 오브젝트에 저장되어 있다.

<br>

# 3. Global과 window의 관계

## Global과 window의 관계

### Global과 window 오브젝트 주체

- 글로벌 오브젝트는 JS가 주체
- window 오브젝트는 window가 주체
  - JS 스펙에서 정의된 것이 아니다.

<br>

- 주체는 다르지만 글로벌 오브젝트의 프로퍼티와 함수가 `window 오브젝트`에 설정된다.
  - 글로벌 오브젝트는 실체가 없는데 어딘가에 프로퍼티, 함수가 저장되어야 하기 때문
- Host 오브젝트 개념이 밑바탕에 활용되기 때문에 가능한 것이다.
  - 브라우저 안에 있는 오브젝트를 JS에서 마치 자기 것처럼 쓰는 개념

<br>

# 4. 정수, 실수 변환

## parseInt()

- 값을 정수로 변환하여 반환한다.
  - ex. 123.56 -> 123
  - 소수 제외하고 정수만 반환
- 값이 "123px"이면 123을 반환한다.
  - 이 용도로 많이 사용된다.
  - String 타입이라도 값이 숫자이면 변환된다.
- 0 또는 빈 문자열을 제외시킨다.
- 진수를 적용하여 값을 변환한다.

```js
console.log(parseInt("-123.45")); // -123
console.log(parseInt("123px")); // 123
console.log(parseInt("12AB34")); // 12
console.log(parseInt("0012")); // 12
console.log(parseInt("  123")); // 123, 앞의 공백 무시
console.log(parseInt()); // NaN, 파라미터를 숫자(Number) 개념으로 처리하기 때문
console.log(parseInt(13, 16)); // 19, 13을 16진수로 변환 (16 + 3)
console.log(parseInt("0x13")); // 19, 13을 16진수로 변환
```

<br>

# parseFloat()

- 값을 실수로 변환하여 반환한다.
  - 그런데 JS는 기본적으로 **실수로 처리**한다.
  - 따라서 실수로 변환하는 것은 의미가 없지만 **문자열**의 실수 변환은 의미가 있다.
- 지수, 공백 변환

```js
console.log(parseFloat("1.2e3")); // 1200
console.log(parseInt()); // NaN
```

<br>

# 5. NaN, 유한대 체크 함수

## isNaN()

- 값의 NaN 여부 반환
- 숫자 값이 아니면 true, 숫자 값이면 false를 반환한다.
  - 값이 숫자로 변환되면 숫자로 인식한다.

```js
console.log(isNaN(null)); // null은 숫자로 변환하면 0이기 때문에 false이다.
```

- `NaN === NaN`의 결과는 false 이다.
  - 이는 설계 실수이다.
  - ES6의 `Object.is()`를 사용한다.

```js
// NaN을 비교할 때는 Object.is()를 사용하는 것이 안전하다.
console.log(NaN === NaN); // false
console.log(Object.is(NaN, NaN)); // true
```

<br>

## isFinite()

- 값이 `Infinity`, `NaN`이면 false를 반환한다.
- 그렇지 않으면, 즉 finite(유한)이면 true를 반환한다.
- 값이 숫자로 변환되면 숫자로 인식한다.

```js
// NaN
console.log(isFinite(0 / 0)); // false
// Infinity
console.log(isFinite(1 / 0)); // false
console.log(isFinite("ABC")); // false

// true가 되는 경우
console.log(isFinite(123));
console.log(isFinite("123"));
console.log(isFinite(false)); // 숫자로 변환되면 0이기 때문
```

<br>

# 6. 인코딩, 디코딩

## encodeURI()

- URI를 인코딩하여 반환한다.
  - Uniform Resource Idetifier
  - 인코딩 제외 문자를 제외하고 "%16진수%16진수" 형태로 변환한다.
- **인코딩 제외 문자**
  - 영문자, 숫자
  - \# ; / ? : @ & = + $ , - \_ . ! ~ \* () 따옴표

<br>

## encodeURIComponent()

- encodeURI()와 같다.
  - 다만 제외 문자가 더 적다.
  - ; / ? : @ & = + $ 를 인코딩한다.

<br>

## decodeURI()

- 인코딩을 디코딩하여 반환한다.
- 사람이 읽기 쉬운 형태로 바꾸기 위함.
- 파라미터에 encodeURI()로 인코딩한 문자열을 작성한다.

<br>

## decodeURIComponent()

- decodeURI()와 같다.
  - 단, 파라미터에 `encodeURIComponent()`로 인코딩한 문자열을 작성한다.

<br>

# 7. eval() 함수

## eval()

- 파라미터의 문자열을 JS 코드로 간주하여 **실행**한다.
  - 실행 결과를 반환 값으로 사용한다.
  - 값을 반환하지 않으면 `undefined`를 반환한다.

```js
var result = eval("parseInt('-123.45')");
console.log(result); // -123
```

- 보안에 문제가 있다고 알려져 있기 때문에 사용을 권장하지 않는다.
