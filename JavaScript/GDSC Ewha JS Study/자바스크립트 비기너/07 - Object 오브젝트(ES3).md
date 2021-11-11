# 1. 자바스크립트 오브젝트 구분, 네이티브/호스트 오브젝트, 오브젝트와 인스턴스

## 자바스크립트의 오브젝트

- 빌트인 오브젝트
- 네이티브 오브젝트
- 호스트 오브젝트

## 네이티브 오브젝트

### 빌트인 오브젝트

- 사전에 만들어 놓은 오브젝트
- 빌트인 Number 오브젝트, String 오브젝트
- ES5 기준 11개의 오브젝트가 있다.

### 네이티브 오브젝트

- JS 스펙에서 정의한 오브젝트
- 빌트인 오브젝트가 포함된다.
- JS 코드를 실행할 때 만드는 오브젝트
- 예: Argument 오브젝트 (함수 호출되면 함수 안에서 만들어지고 함수를 빠져나오면 JS 엔진이 지워준다. 빌트인 성격이지만 사용성에 차이가 있다.)

<br>

빌트인 오브젝트는 네이티브 오브젝트에 포함되므로 자바스크립트의 오브젝트는 **빌트인 오브젝트와 네이티브 오브젝트**로 구분할 수 있다. (ES5 기준, ES6에서는 더 세밀하게 구분)

<br>

## 호스트 오브젝트

- 빌트인, 네이티브 오브젝트를 **제외한** 오브젝트
- 예: window, DOM 오브젝트
  - `document.querySelector()` 같은 DOM 함수는 JS 스펙에 작성된 함수가 아니라 DOM 스펙에서 작성된 함수이다.
  - DOM에서 제공하는 오브젝트를 호스트 오브젝틑라고 한다.
  - JS는 호스트 오브젝트를 JS 함수처럼 사용할 수 있다.
- JS는 **호스트 환경**에서 브라우저의 모든 요소 기술을 연결하고 융합하여 이를 제어한다. \* JS 개발자는 JS뿐 아니라 호스트 오브젝트에 해당되는 것들을 계속해서 배워야 한다.

<br>

## 오브젝트와 인스턴스

- 여기에서 **오브젝트**는 new 연산자를 사용하지 않고 빌트인 오브젝트로 만든 오브젝트를 지칭한다.

<br>

# 2. 빌트인 Object 프로퍼티(ES3)

- new Object(): 인스턴스 생성. 파라미터 값의 타입에 따라 인스턴스를 만들기도 한다.
- valueOf(), hasOwnProperty(), propertyIsEnumerale(), isPrototypeOf(), toString(), toLocaleString() 은 빌트인 오브젝트로 인스턴스를 만드는 오브젝트에 모두 포함된다. 인스턴스를 만들 수 없는 오브젝트에는 포함되지 않는다. (ES3의 특징)

<br>

# 3. Object 인스턴스 생성, 프리미티브 값 구하기

## new Object()

- 인스턴스를 생성하여 반환한다.
- 파라미터의 데이터 타입에 따라 생성할 인스턴스 타입이 결정된다.

```js
var newObjt = new Object(123);
console.log(typeof newObj); // object
console.log(newObj + 100); // 223
// 원래라면 object는 키:값 쌍으로 이루어져 있어 100을 더하면 이상한 값이 나와야 하지만 정상적으로 계산이 된다.
// newObj의 프리미티브 값은 123이다
```

- 파라미터 값이 `undefined`, `null`이면 빈 Object 인스턴스를 반환한다.

```js
var newObj = new Object();
console.log(newObj); // {}
```

<br>

## Object()

- Object 인스턴스를 생성한다. (`new 연산자`를 사용해서 생성하지 않은 것)
- 파라미터는 `{name: value}` 형태이다.

```js
var emptyObj = Object(); // new Object()와 같다.
console.log(emptyObj); // {}
```

<br>

## Object 생성 방법

- `var abc = {};`
  - `var abc = Object()`와 같다.
  - 즉, `var abc = {}`를 실행하면 Object 인스턴스가 생성된다.
  - 그래서 `Object()`를 사용하지 않고 `{}`를 사용하여 간단하게 인스턴스를 생성한다.
- {} 표기를 `오브젝트 리터럴`이라고 한다.

<br>

## valueOf()

- data 위치에 작성한 Object 인스턴스의 프리미티브 값을 반환한다.

```js
var obj = { key: "value" };
console.log(obj.valueOf());
```

<br>

# 4. 빌트인 오브젝트 구조, prototype

## 빌트인 오브젝트 구조

- 오브젝트 이름(Object, String, Number...)
- 오브젝트.prototype
  - 인스턴스 생성 가능 여부의 기준이다. (Math 오브젝트에는 prototype이 없다. 따라서 Math는 인스턴스를 만들 수 없다.)
  - 프로퍼티를 연결하는 오브젝트이다.
  - 안에 내용은 별게 없지만 중요한 의미를 가진다.
- 오브젝트.prototype.constructor
  - 오브젝트의 생성자
  - 실질적으로 인스턴스를 생성하는 역할을 한다.
  - prototype이 없으면 존재하지 않는다. 반대로 prototype이 있으면 디폴트로 따라온다.
- 오브젝트.prototype.method
  - 메소드 이름과 함수를 작성한다.  
    \* ES5에서는 constructor를 변경할 수 없지만 ES6에서는 변경 가능하다.

<br>

# 5. 함수와 메소드 연결, 함수, 메소드 호출

## 함수와 메소드 연결

- 함수
  - 오브젝트에 연결한다.
  - Object.create()
- 메소드 - 오브젝트의 prototype에 연결한다. - Object.prototype.toString()

  <br>

\* ES6에서는 `static method`가 추가되었다.

<br>

## 함수, 메소드 호출

### 함수 호출 방법

- Object.create()

```js
// 함수의 존재 여부 확인
console.log(Object.create); // function create() { ... }
console.log(Object.prototype.create); // undefined
```

### 메소드 호출 방법

- Object.prototype.toString();
- 또는 인스턴스를 생성하여 호출한다.

### 함수와 메소드를 구분해야 하는 이유

- JS 코드 작성 방법이 다르기 때문이다.
- 함수는 파라미터에 값을 작성하고 메소드는 메소드 앞에 값을 작성하기 때문이다.

```js
// 함수 앞에 여러 개의 값(배열)로 값을 ㅈ가성하면 Array 오브젝트의 함수가 호출된다.
// 따라서 String 오브젝트의 함수를 호출하면서 파라미터에 값을 작성해야 한다.
console.log(String.fromCharCode(49, 65));
```

<br>

# 6. 프로퍼티 처리 메소드

## hasOwnProperty()

- 인스턴스에 파라미터 이름이 존재하면 `true`, 존재하지 않으면 `false`를 반환한다.
- 자신이 만든 것이 아니라 상속받은 프로퍼티이면 `false`를 반환한다.

```js
// undefined가 값이지만 false로 인식된다.
// 하지만 값은 체크하지 않고 존재 여부만 체크하므로 true를 반환한다.
var obj = { value: undefined };
var own = obj.hasOwnProperty("value");
console.log(own); // true
```

## propertyIsEnumerable()

- 오브젝트에서 프로퍼티를 열거할 수 있으면 `true`, 그렇지 않으면 `false`를 반환한다.

```js
// 열거 가능한 경우
var obj = { sports: "축구" };
console.log(obj.propertyIsEnumerable("sports")); // true

// 열거 불가능한 경우
var obj = { sports: "축구" };
Object.defineProperty(obj, "sports", {
  enumerable: false, // 열거 불가 설정
});
console.log(obj.propertyIsEnumerable("sports")); // false
// for-in문으로 열거할 수 없다. (결과 출력되지 않음)
```

# 7. Object와 prototype, 빌트인 Object 특징

## 빌트인 Object 특징

- 인스턴스를 만들 수 있는 **모든 빌트인 오브젝트**의 `__proto__`에 `Object.prototype`의 6개 메소드가 설정된다.
- 따라서 빌트인 오브젝트로 만든 인스턴스에도 6개 메소드들이 존재한다.

<br>

## isPrototypeOf()

- 파라미터에 작성한 오브젝트에 object 위치에 작성한 prototyp이 존재하면 `true`, 그렇지 않으면 `false`를 반환한다.

<br>

## toString()

- 인스턴스 타입을 문자열로 표시한다.
- 오브젝트에 toString()이 있으면 호출되고 그렇지 않으면 Object의 toString()이 호츨된다.

```js
var point = { book: "책" };
// 빌트인 오브젝트의 toString()을 부른다.
console.log(point.toString()); // [object Object]
// object는 인스턴스, Object는 빌트인 Object를 나타낸다.

var obj = new Number(123);
// call(): prototype에 연결되어 있는 메소드를 직접 인스턴스 만들지 않고 호출할 때 사용
console.log(Object.prototype.toString.call(obj)); // [object Number]
```

<br>

## toLocaleString()

- 지역화 문자 변환 메소드 대체 호출
- Array, Number, Date 오브젝트의 toLocaleString()이 먼저 호출되고 이들이 아닐 때에는 빌트인 Object의 toLocaleString()이 호출된다.
