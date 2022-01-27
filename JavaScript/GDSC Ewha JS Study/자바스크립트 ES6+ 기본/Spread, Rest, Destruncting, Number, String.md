# Spread, Rest

## Spread

```jsx
const list = [21, 22];
log([11, ...list, 12]); // [11, 21, 22, 12]
```

- [...Iterable]
    - [...]처럼 [] 안에 . 3개를 작성하고 이어서 이터러블 오브젝트를 작성한다.
- 이터러블 오브젝트를 하나씩 전개한다.
- {key: value}의 Object가 이터러블 오브젝트는 아니지만 전개할 수 있다.

## Array Spread

```jsx
const one = [21, 22];
const two = [31, 32];
const result = [11, ...one, 12, ...two];
log(result); // [11, 21, 22, 12, 31, 32]
log(result.length); // 6

result = [11, 12, ...one];
log(result); // [11, 12, 11, 12]
// 앞에 11, 12가 있지만 값을 대체하지 않고 ...을 작성한 위치에 전개한다
```

- spread 대상 배열을 작성한 위치에 엘리먼트 단위로 분리한다.
- 값이 대체되지 않고 전개된다.

## String spread

- spread 대상 문자열을 작성한 위치에 문자 단위로 전개한다.

## Object spread

```jsx
const one = {key1: 11, key2: 22};
const result = {key3: 33, ...one};
log(result); // {key3: 33, key1: 11, key2: 22}
```

- spread 대상 Object를 작성한 위치에 프로퍼티 단위로 전개한다.
- 프로퍼티 이름이 같으면 값을 대체한다.

## push(...spread)

```jsx
let result = [21, 22];
const five = [51, 52];
result.push(...five);
log(result); // [21, 22, 51, 52]

result.push(..."abc");
log(result); // [21, 22, 51, 52, a, b, c]
```

- push() 파라미터에 spread 대상을 작성한다.
- 배열 끝에 대상을 분리하여 첨부한다.

## function spread

```jsx
function add(one, two, three) {
	log(one + two + three);
};

const values = [10, 20, 30];
add(...values); // 60
```

- 호출하는 함수의 파라미터에 spread 대상 작성한다.
- 처리 순서 및 방법
    - 함수가 호출되면 우선 파라미터의 배열을 엘리먼트 단위로 전개한다.
    - 전개한 순서대로 파라미터의 배열을 엘리먼트 단위로 전개한다.
    - 전개한 순서대로 파라미터 값으로 넘겨준다.
    - 호출받는 함수의 파라미터에 순서대로 매핑된다.

## rest 파라미터

```jsx
function point(...param) {
	log(param);
	log(Array.isArray(param));
};
const values = [10, 20, 30];
point(...values);
// [10, 20, 30]
// true
```

- function(param, paramN, ...name)
- 분리하여 받은 파라미터를 배열로 결합한다.
    - spread: 분리, rest: 결합
- 작성 방법
    - 호출 받는 함수의 파라미터에 ...에 이어서 파라미터 이름을 작성한다.
    - 호출한 함수에서 보낸 순서로 매핑된다.

### 파라미터와 Rest 파라미터 혼합 사용

```jsx
function point(ten, ...rest) {
	log(ten);
	log(rest);
};
const values = [10, 20, 30];
point(...values);
// 10
// [20, 30]
```

## Array-like

```jsx
const values = {0: "가", 1: "나", 2: "다", length: 3};
for (let k = 0; k < values.length; k++) {
	log(values[k]);
};
// 가
// 나
// 다
// length 프로퍼티는 전개되지 않는다.
// for-in문으로 전개하면 length 프로퍼티도 전개된다.
```

- Object 타입이지만 배열처럼 이터러블 가능한 오브젝트
- for문으로 전개할 수 있다.
- 작성 방법
    - 프로퍼타 key 값을 0부터 1씩 증가하면서 프로퍼티 값을 작성한다.
    - length에 전체 프로퍼티 수를 작성한다.

## rest와 arguments 차이

- Argument 오브젝트
    - 파라미터 작성에 관계없이 전체를 설정한다.
    - Array-like 형태
    - Array 메소드를 사용할 수 없다.
    - **__proto__가 Object**
- rest 파라미터
    - 매핑되지 않은 나머지 파라미터만 설정한다.
    - Array 오브젝트 형태
    - Array 메소드 사용 가능
    - __proto__가 Array

# Destructing (분할 할당)

```jsx
let one, two, three;
const list = [1, 2, 3];
[one, two, three] = list;
log(list); // [1, 2, 3]
```

## Array 분할 할당

- 배열의 엘리먼트를 분할하여 할당
    - 인덱스에 해당하는 변수에 할당
    - 할당받을 변수 수가 적은 경우
        - 왼쪽의 변수 인덱스에 맞추어 값을 할당한다.
    - 할당받을 변수 수가 많을 경우
        - 왼쪽에 값을 할당할 수 없는 변수에 `undefined` 가 설정된다.
    - 배열 차원에 맞추어 분할 할당하는 경우
        - 배열 차원이 변환된다.
    - 매치되는 인덱스에 변수가 없으면 값을 할당하지 않는다.
- spread와 같이 사용할 수 있다.
    - 나머지를 전부 할당할 수 있다.
    - 인덱스를 반영한 나머지 할당

## Object 분할 할당

- Object의 프로퍼티를 분할하여 할당한다.
- 프로퍼티 이름이 같은 프로퍼티에 값을 할당한다.
- 프로퍼티 이름을 별도로 작성하는 경우에는 전체를 소괄호 안에 작성해야 한다.
- 프로퍼티 값 위치에 변수 이름을 작성한 경우
    
    ```jsx
    let five, six;
    ({one: five, two: six}) = {one: 5, two: 6});
    log(five); // 5
    log(six); // 6
    // log(one); - ReferenceError
    // five, six의 변숫값을 구하는 것이 목적
    ```
    
- Object 구조에 맞추어 값 할당하는 경우
- 나머지를 Object로 할당하는 경우

## 파라미터 분할 할당

- 호출하는 함수에서 Object 형태로 넘겨준 파라미터 값을 호출받는 함수의 파라미터에 값을 할당한다.
- Object 구조에 맞추어 값을 할당하는 경우

## Object 오퍼레이션

- 같은 프로퍼티 이름을 사용하는 경우
    
    ```jsx
    const value = {book: 10, book: 20};
    log(value); // {book: 20}
    ```
    
    - ES5 strict 모드에서는 프로퍼티 이름이 같으면 에러가 난다.
    - ES6에서는 strict 모드와 관계없이 에러가 발생하지 않는다. 뒤에 작성한 프로퍼티 값으로 대체된다.
- Shorthand property names
    
    ```jsx
    const one = 10, two = 20;
    const values = {one, two};
    log(values); // {one: 10, two: 20}
    ```
    

## 프로퍼티 이름 조합

- 문자열을 프로퍼티 이름으로 사용하는 경우
    - [] 안에 문자열로 이름을 작성한다.
    - 문자열을 + 연산자로 연결하여 프로퍼티 이름으로 사용한다.
- 변숫값을 프로퍼티 이름으로 사용하는 경우
    - 대괄호 안에 변숫값을 넣어서 작성한다.
    - 변숫값과 문자열을 연결할 수 있다.
    - 프로퍼티 이름에 공백을 넣을 수도 있다.
    - 함수로 호출할 수 있다.
        - 변숫값에 따라 함수 이름으로 정의할 수 있다.
- 분할 할당을 조합한 형태
    - 변숫값을 프로퍼티 이름으로 사용하고 분할 할당한 형태

# default value

```jsx
const [one, two, five = 50] = [10, 20, 70];
log(five); // 70
```

- 값을 할당하지 않으면 사전에 정의된 값을 할당하는 것.
- 할당할 값이 없으면 디폴트 값을 할당한다.
- 할당할 값이 있으면 디폴트 값을 무시한다.
- Object는 프로퍼티 이름으로 체크한다.
- 디폴트 값은 왼쪽에서 오른쪽으로 적용한다.

# for-of문

- for (variable of iterable){ }
- 이터러블 오브젝트를 반복한다.
- iterable
    - 이터러블 오브젝트를 작성한다.
    - 표현식을 작성하면 평과 결과를 사용한다.
- variable
    - 변수 이름을 작성한다.
    - 이터러블 오브젝트를 반복할 때마다 variable에 값이 할당된다.
- 배열
    - 배열을 반복하면서 엘리먼트를 하나씩 전개한다.
- String
    - 문자열을 반복하면서 문자를 하나씩 전개한다.
- NodeList
    - NodeList를 반복하면서 엘리먼트를 하나씩 전개한다.

## for-in, for-of 차이

### for-in

- 열거 가능한 프로퍼티가 대상
- {key: value} 형태는 디폴트가 enumberable: true
- Object.defineProperty()는 디폴트가 enumberable: false

### for-of

- 이터러블 오브젝트가 대상
- Object는 전개되지 않는다.
- prototype의 프로퍼티도 전개되지 않는다.

## for-of, Object

- Object는 이터러블 오브젝트가 아니므로 for-of를 사용할 수 없다.
- Object를 for-of로 전개하는 방법
    - Object.keys()로 프로퍼티 이름을 배열로 만들고 만든 배열을 for-of로 전개한다.
# 연산자, 기타

## Trailing commas

- Object 끝에 콤마 사용
    - } 앞에 콤마 사용 가능
- 배열 끝에 콤마 사용
    - ] 앞에 콤마 사용 가능

## 거듭 제곱

- 거듭제곱은 우결합성

## try-catch

- try-catch의 catch(error)에서 (error)를 생략할 수 있다.
    - ES2019에서 나옴

## 함수 작성 형태

- Object에서 함수를 작성할 때 function 키워드를 작성하지 않아도 된다.
- Object에 함수를 작성하는 이유
    - 함수에서 this로 Object 전체를 참조할 수 있다.
    - new 연산자로 인스턴스를 생성하지 않는다. 메소드가 아닌 함수로 접근한다.
    - Object 전체가 하나의 묶음이기 때문에 접근성, 가독성이 좋다.
    - 시맨틱을 부여할 수 있으며 다른 오브젝트와 이름과 프로퍼티 이름이 충돌되지 않는다.

# getter, setter

## getter

- getter로 선언된 함수를 자동으로 호출한다.
    - 값을 반환하는 시맨틱을 갖고 있으므로 getter 함수에서 값을 반환해야 한다.
- ES6 장점
    - ES5와 다르게 프로퍼티의 속성 구조가 아니다.
    - 작성이 편리하다.
    - 다수의 getter를 사용할 수 있다.

## setter

- 프로퍼티에 값을 할당하면 setter로 선언된 함수가 자동으로 호출된다.
    - setter 함수에서 값을 설정해야 한다.

# Number 오브젝트

## Number.EPSION

- 아주 작은 값
- 2^-52
- 사용 사례
    - 미세한 값 차이 형태
    - 미세한 값 차이를 같은 값으로 간주
    - 0/0으로 NaN가 되는 것을 방지

## Number 함수

- isNaN()
    - NaN 값의 여부를 체크
    - Number.isNaN()
    - 글로벌 오브젝트의 isNan()은 값 타입이 Number가 아닌 것을 체크한다.
- isInteger()
- isSafeInteger()
- isFinite()
    - 글로벌 오브젝트의 isFinite()와 체크 결과가 다르다.

# String 오브젝트

## Unicode 함수

- fromCodePoint()
- codePointAt()
- normalize()

## 시작/끝 체크, 복제

- startsWith()
- endsWith()
- repeat()
- includes()
- raw()

## 길이 늘리기, 공백 삭제

- padStart()
- padEnd()
- trimStart()
- trimEnd()
