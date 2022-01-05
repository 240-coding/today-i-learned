### ✔️ 생각의 전환

- 함수가 호출되면 엔진은 함수의 변수와 함수를 {name: value} 형태로 실행 환경을 설정하고 함수 코드를 실행한다.
- {name: value} 형태로 생각을 전환해야 JS의 아키텍처와 매커니즘을 쉽게 이해할 수 있다.
- function() {} 코드를 보면 함수의 변수와 함수가 {name: value} 형태로 연상되어야 한다.

# function 오브젝트 생성 과정

1. function sports() {...} 형태 과정에서 function 키워드를 만나면
2. 오브젝트를 생성하고 저장한다.
    - {sports: {...}}
    - sports는 function 오브젝트 이름
    - 오브젝트 {...}에 프로퍼티가 없는 상태
3. 이제부터 빈 오브젝트를 채운다.
4. sports 오브젝트에 prototype 오브젝트 첨부
5. prototype에 constructor 프로퍼티 첨부
    - prototype.constructor가 sports 오브젝트 참조
6. prototype에 __proto__ 오브젝트 첨부
    - ES5 스펙에 __proto__가 기술되어 있지 않으며 ES6 스펙에 기술되어 있다.
    - 엔진이 사용한다는 뉘앙스
7. sports 오브젝트에 __proto__ 오브젝트 첨부
    - sports.__proto__ 구조가 된다.
8. 빌트인 Function.prototype의 메소드로 function 인스턴스를 생성하여 sports.__proto__에 첨부
9. sports 오브젝트 프로퍼티에 초기값 설정
    - arguments, caller, length, name 프로퍼티

```jsx
sports = {
	arguments: {}.
	caller: {},
	length: {},
	name: "sports",
	prototype: {
		constructor: sports
		__proto__: Object.prototype
	},
	__proto__: Function.prototype
}
```

## function 오브젝트 구조

- function 오브젝트에 prototype이 있으며
    - constructor가 연결된다.
    - __proto__가 연결되어 있으며 Object 인스턴스가 연결된다.
- function 오브젝트에 __proto__가 있으며
    - Function 인스턴스가 연결된다.
    - Array이면 Array 인스턴스가 연결되고, String이면 String 인스턴스가 연결된다. 즉, 오브젝트 타입에 따라 바뀔 수 있다.

# function 실행 환경 저장

## 함수 실행 환경 인식

- 함수 실행 환경 인식이 필요한 이유?
    - 함수가 호출되었을 때 실행될 환경을 알아야 실행 환경에 맞추어 실행할 수 있기 때문이다.
- 실행 환경 설정 시점
    - function 키워드를 만나 function 오브젝트를 생성할 때
- 설정하는 것
    - 실행 영역(함수가 속한 스코프)
    - 파라미터, 함수 코드 등

## 함수 실행 환경 저장

- function 오브젝트를 생성하고 바로 실행하지 않으므로 함수가 호출되었을 때 사용할 수 있도록 환경을 저장해야 한다.
    - **생성한 function 오브젝트에 저장된다.**
- 인식한 환경을 function 오브젝트의 내부 프로퍼티에 설정한다.
    - {name: value} 형태

## 내부 프로퍼티

- 엔진이 내부 처리에 사용하는 프로퍼티
- 스펙 표기로 외부에서 사용할 수 없다.
- 스펙 표기: [[]] 형태 (예: [[Scope]])

# 내부 프로퍼티 분류

- 공통 프로퍼티
    - 모든 오브젝트에 공통으로 설정되는 프로퍼티
    - 모든 오브젝트란 빌트인 오브젝트로 만드는 오브젝트를 뜻한다.
- 선택적 오브젝트
    - 오브젝트에 따라 선택적으로 설정되는 프로퍼티
    - 해당되는 오브젝트에만 설정된다.

# 엔진 해석 방법

## 엔진 해석 순서

- 자바스크립트는 스크립팅 언어이다.
- 스크립팅 언어는 작성된 코드를 위에서부터 한 줄씩 해석하고 실행한다.
    - 그러나 자바스크립트는 중간에 있는 코드가 먼저 해석될 수도 있다.
1. 함수 선언문을 순서대로 해석
    - function sports(){};
2. 표현식을 순서대로 해석
    - var value = 123;
    - var book = function(){}; // 함수 표현식

# 함수 코드 해석 순서

```jsx
function book() {
	debugger;
	var title = "JS책";
	function getBook() {
		return title;
	};
	var readBook = function(){};
	getBook();
};
book();
```

1. 함수 선언문 해석
    - function getBook(){};
2. 변수 초기화
    - var title = undefined;
    - var readBook = undefined;
    - 여기까지 하면 식별자 해결에는 문제가 없다.
3. 코드 실행
    - var title = “JS책”;
    - var readBook = function(){};
    - getBook();

### 1️⃣ 함수 선언문 해석

1. 마지막 줄에서 book() 함수를 호출한다.
2. 엔진 제어가 book 함수의 첫 번째 줄로 이동한다.
    - debugger를 실행하지 않는다.
3. 함수 안에서 선언문을 찾는다.
    - 위에서 아래로 내려가면서 하나씩 검색한다.
4. function getBook(){} 이 함수 선언문이므로 function 오브젝트를 생성한다.
5. 더 이상 함수 선언문이 없으므로 다시 함수의 첫 번째 줄로 이동한다.

### 2️⃣ 변수 초기화

1. debugger를 실행하지 않는다.
2. var title=”JS책”;
    - title 변수에 undefined를 할당한다.
    - “JS책”을 할당하지 않는다.
3. function getBook(){} 은 초기화를 했으므로 초기화를 하지 않는다.
4. var readBook = function(){};
    - readBook 변수에 undefined를 할당한다.
    - 함수 표현식은 변수를 선언만 한다.
5. 여기까지가 **초기화 단계**이며, 다시 함수의 첫 번째 줄로 이동한다.

### 3️⃣ 코드 실행

1. debugger를 실행하며, 실행이 멈춘다.
2. var title=”JS책”;
    - title 변수에 “JS책”을 할당한다.
3. function getBook(){return title};
    - 실행이 아닌 선언이므로 다음 줄로 이동한다.
4. var readBook = function(){};
    - function 오브젝트를 생성하여 readBook 변수에 할당한다.
    - readBook이 function 오브젝트가 되므로 이제 readBook 함수를 호출할 수 있다.
5. getBook() 함수를 호출한다.
    - 지금까지와 같은 순서와 방법으로 getBook() 함수의 함수와 변수를 초기화하고 코드를 실행한다.

# 호이스팅

## 함수 앞에서 호출

- 함수 선언문은 초기화 단계에서 function 오브젝트를 생성하므로 어디에서도 함수를 호출할 수 있다.
- 함수 앞에서 호출 가능하다는 것을 호이스팅(Hoisting)이라고 한다.
    - 용어보다 개념으로 접근하기!
- 초기화 단계에서 값이 있으면 초기화하지 않는다.

```jsx
var result = book();
console.log(result); // 호이스팅
function book() {
	return "호이스팅";
};
// 에러가 발생하지 않는다!

var result = book();
console.log(result); // 호이스팅
function book() {
	return "호이스팅";
};
book = function() {
	return "함수 표현식";
};
// book에 이미 값이 할당되어 있기 때문에 초기화가 되지 않는다.
```

# 오버로딩(Overloading)

### 오버로딩 형태

```jsx
function book(one){};
function book(one, two){};
function book(one, two, three){};

book(one, two);
```

- 함수 이름이 같더라도 파라미터 수 또는 값 타입이 다르면 각각 존재한다.
- 함수를 호출하면 파라미터 수와 값 타입이 같은 함수가 호출된다.
- **JS는 오버로딩을 지원하지 않는다.**
    - 파라미터 수와 값 타입을 구분하지 않고 {name: value} 형태로 저장하기 때문이다.

## 오버로딩 미지원: 함수 선언문 초기화

```jsx
function book() {
	function getBook(){
		return "책1";
	};
	getBook();
	function getBook(){
		return "책2";
	};
};
book();
```

1. 마지막 줄에서 book() 함수를 호출하면
2. function getBook(){return “책1”;}을 만나 getBook 오브젝트를 생성한다.
3. getBook()을 호출하지 않고 아래로 내려간다.
4. function getBook(){return “책2”;}를 만나 getBook 오브젝트를 생성한다.
    - 2번의 오브젝트와 이름이 같으므로 여기서 생성한 getBook 오브젝트로 대체된다.
5. **{name: value}** 형태에서 이름이 같으므로 값이 변경된다.

## 오버로딩 미지원: 변수 초기화

1. book 함수의 첫 번째 줄로 이동한다.
2. 함수 표현식과 변수에 undefined를 설정하지만 설정할 대상이 없다.
3. 다시 book 함수의 첫 번째 줄로 이동한다.

## 오버로딩 미지원: 코드 실행

1. function getBook(){return “책1”;}
    - 함수 선언문이므로 아래로 내려간다.
2. getBook()을 호출한다.
3. return “책2”;의 getBook 함수가 호출된다.
    - 함수 이름이 같으므로 위의 함수가 아래 함수로 대체되었기 때문이다.
    - “책2”가 출력된다.
4. 호출한 함수로 돌아와 다음 코드를 수행한다.
5. function getBook(){return “책2”;}
    - 함수 선언문이므로 처리하지 않는다.
