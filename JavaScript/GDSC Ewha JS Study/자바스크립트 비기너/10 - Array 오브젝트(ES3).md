# 1. Array 오브젝트(ES3)

ES3는 프로그래밍 언어로서 배열의 기본을 다룬다면, ES5는 활용하는 측면이 강하다.

<br>

## Array 오브젝트 개요

- 빌트인 오브젝트이다.
- Array(배열) 형태
  - Array 오브젝트는 `배열 오브젝트`라고 불러도 무방하다.
  - ex. `[123, "ABC", "가나다"]`
  - 대괄호 안에콤마로 구분하여 값을 작성한다.
- 배열 엘리먼트
  - `[123, "ABC"]`에서 `123`, `"ABC"` 각각을 엘리먼트 또는 요소라고 부른다.
  - 배열 안에 작성할 수 있는 엘리먼트의 수는 2의 32승 - 1개이다.
- 인덱스(Index)
  - 엘리먼트 위치를 뜻한다.
  - 왼쪽부터 0번 인덱스, 1번 인덱스...
- 배열 특징
  - 엘리먼트 작성이 **순서**를 갖고 있다.
  - 배열 전체를 작성한 순서로 읽거나 인덱스로 값을 추출할 수 있다.
    - 인덱스는 순서를 액세스하는 역할을 한다.

<br>

## 배열 생성 방법

- `new Array()`로 생성
  - `var book = new Array();`
- `Array()`로 생성
  - `var book = Array();`
- 대괄호로 생성
  - `var book = [];`
  - `Array 리터럴`이라고 한다.
  - 일반적으로 이 형태를 사용한다.

<br>

## 엘리먼트 작성 방법

- `var book = ["책1", '책2'];`
- 대괄호 안에 콤마로 구분하여 여러 개를 작성할 수 있다.
- `String` 타입은 큰 따옴표, 작은 따옴표 모두 사용 가능하다.
- JS의 모든 타입의 값, 오브젝트, 인스턴스를 사용할 수 있다.
- 값을 작성하지 않고 콤마만 작성하면 `undefined`가 설정된다.
  - 값을 정의하지 않았다는 의미

<br>

## 배열 차원

- 대괄호의 수가 차원의 기준이 된다.
- 1차원 배열
  - 대괄호 하나에 엘리먼트 작성
  - `[12, 34, 56]`
- 2차원 배열
  - 배열 안에 1차원 배열 작성
  - `[[12, 34, 56]]`
- 3차원 배열
  - 배열 안에 2차원 배열 작성
  - `[[[12, 34, 56]]]`

<br>

# 2. Array 인스턴스 생성

## new Array()

- Array 인스턴스 생성 및 반환
- 배열 생성 기준
  - 파라미터에 따라 배열 생성 기준이 다르다.
  - 파라미터를 작성하지 않으면 빈 배열을 반환한다.
  - 작성한 순서로 엘리먼트에 설정된다.
  - `new Array(3)`처럼 파라미터에 숫자를 작성하면 3개의 엘리먼트가 생성된다.
    - 처음부터 n개의 엘리먼트를 저장하겠다는 의도가 강하게 포함되어 있다.
    - 배열의 값들이 메모리 내에 산발적으로 저장되어 메모리에 부담을 주는 것을 방지할 수 있다. -> 속도가 빠르다.
    - 최근에는 컴퓨터 사양이 좋아졌기 때문에 크게 신경쓰지 않아도 된다.

```js
// 빈 배열
var obj = new Array();
console.log(typeof obj); // object
console.log(obj.length); // 0

var one = new Array(10, 20);
console.log(one); // [10, 20]
// 파라미터를 배열로 작성하면 1차원을 더한 차원이 된다.
var two = new Array([30, 40]);
console.log(two); // [[30, 40]]

// 숫자 하나 작성
var obj = new Array(3);
console.log(obj); // [undefined, undefined, undefined]
```

<br>

## Array()

- Array 인스턴스 생성 및 반환
  - `new Array()`와 생성 방법 및 기능이 같다.
- 인스턴스 생성 논리
  - `new Array()`는 `new` 연산자에서 생성자 함수를 호출하여 인스턴스를 생성한다.
    - prototype에 연결되어 있는 `constructor`가 호출된다.
  - `Array()`는 직접 생성자 함수를 호출하여 인스턴스를 생성한다.
    - `Array()`가 생성자 함수라고 볼 수 있다.

<br>

## length 프로퍼티

- 배열 `[1, 2, 3]`에서
  - `length` 값은 3
  - Array 오브젝트에 `{length: 3}` 형태로 설정된다.
  - 처음 인덱스는 0, 마지막 인덱스는 2이다.
- 열거/삭제는 할 수 없지만 개발자가 임의로 변경은 가능하다.
- length 값을 변경하면 배열의 엘리먼트 수가 변경된다.

```js
var value = [1, 2, 3];
value.length = 5;
console.log(value); // [1, 2, 3, undefined, undefined]

// length 값을 작게 변경하면 뒤의 엘리먼트가 삭제된다.
var value = [1, 2, 3];
value.length = 2;
console.log(value); // [1, 2]
```

<br>

# 3. 엘리먼트 추가, 삭제 메커니즘

## 엘리먼트 추가

- 배열에 엘리먼트 추가하는 방법
  - 삽입할 위치에 인덱스 지정
  - 표현식으로 인덱스 지정

```js
// 삽입할 위치에 인덱스 지정
// 값을 설정하지 않은 추가된 엘리먼트에는 undefined가 설정된다.
var value = [1, 2];
value[4] = 5;
console.log(value); // [1, 2, undefined, undefined, 5]

// 표현식으로 인덱스 지정
var value = [1, 2];
value[value.length + 2] = 5; // 인덱스에 값을 더해 인덱스로 사용
console.log(value); // [1, 2, undefined, undefined, 5]
```

<br>

## delete 연산자

- 연산자이기 때문에 배열에 속하는 것은 아니다.
- 삭제에 성공하면 `true`, 실패하면 `false`를 반환한다.
- var 변수는 삭제할 수 없다.
- 글로벌 변수는 삭제할 수 있다. (var 키워드를 사용하지 않은 글로벌 변수)
- `{name: value}` 삭제 방법
  - 삭제할 프로퍼티 이름을 작성한다
  - ES5에서 삭제 불가를 설정할 수 있다.

```js
// 오브젝트 프로퍼티 삭제
var book = {title: "책"};
console.log(delete book.title); // true
console.log(book.title); // undefined
// 삭제한 변수는 접근하면 에러가 나지만
// 프로퍼티로 접근하면 undefined가 출력된다.

// 오브젝트 전체 삭제
// var 변수에 오브젝트 할당시 오브젝트 전체 삭제 불가능
var book = {title: "책"};
console.log(delete book); // false

sports = {item: "축구"};
console.log(delete sports); // true
```

- 인덱스로 배열의 엘리먼트를 삭제할 수 있다.

```js
// 배열 처리 매커니즘으로 인해
// 엘리먼트를 삭제해도 length가 변하지 않는다.
var value = [1, 2, 3, 4];
console.log(delete value[1]); // true
console.log(value.length); // 4
```

<br>

## 배열 엘리먼트 삭제 메커니즘

- 삭제된 인덱스에 `undefined`를 설정한다.
  - 배열을 읽을 때 제외시켜야 한다.
  - 앞으로 하나씩 당겨서 엘리먼트를 이동하면 처리 시간이 소요되기 때문이다.

```js
var value = [1, 2, 3, 4];
delete value[1];
console.log(value); // [1, undefined, 3, 4]

for (var k = 0; k < value.length; k++) {
  console.log(value[k]);
}
```

<br>

# 4. 엘리먼트 삽입, 첨부

## unshift()

- 0번 인덱스에 파라미터 값을 삽입한다.
- 배열에 있던 엘리먼트는 뒤로 이동한다.

<br>

## push()

- 배열 끝에 파라미터 값을 첨부한다.

<br>

## concat()

- 배열에 파라미터 값을 연결하여 반환한다.
- 파라미터가 1차원 배열이면 값만 반영한다.

```js
var value = [1, 2];
var result = value.concat([3], [4]);
console.log(result); // [1, 2, 3, 4]
```

<br>

# 5. 엘리먼트 복사

## slice()

- 배열의 일부를 복사하여 **배열**로 반환한다.
  - 첫 번째 파라미터의 인덱스부터 두 번째 인덱스 **직전까지**
    - 끝 인덱스의 디폴트 값이 `length`이기 때문
- true, false를 숫자로 반환한다.

```js
var value = [1, 2, 3, 4, 5];
console.log(value.slice(true, 3)); // [2, 3]
console.log(value.slice(false, 3)); // [1, 2, 3]
```

- 첫 번째 파라미터만 작성하면 끝까지 반환한다.
- 첫 번째 파라미터 값이 두 번째 파라미터 값보다 크면 빈 배열을 반환한다.
- 파라미터에 음수를 작성하면 `length` 값을 더한다.

```js
var value = [1, 2, 3, 4, 5];
// -4 + 5 = 1
// -2 + 5 = 3
console.log(value.slice(-4, -2)); // [2, 3]
```

<br>

# 6. 엘리먼트 값을 문자열로 변환

## join()

- 엘리먼트와 분리자를 하나씩 결합하여 문자열로 연결한다.
  - 분리자는 선택사항이고, 디폴트 값은 콤마(,)이다.
- 마지막 엘리먼트는 분리자를 연결하지 않는다.

```js
var value = [1, 2, 3];
var result = value.join("##");
console.log(result); // 1##2##3
console.log(typeof result); // string
```

- 파라미터를 작성하지 않으면 콤마로 분리한다.
- 파라미터에 빈 문자열을 작성하면 엘리먼트 값만 연결하여 반환한다.
  - 사용 빈도수가 높다.
  - 데이터로 HTML의 마크업을 만들어 한 번에 표시할 때 사용한다. (ex. `<table>`)

```js
var value = [1, 2, 3];
var result = value.join("");
console.log(result); // 123
```

<br>

## toString()

- 배열의 엘리먼트 값을 문자열로 연결한다.
  - 콤마로 엘리먼트를 구분한다.

```js
var result = ["A", "B", "C"].toString();
console.log(result); // A,B,C
// 2차원 배열의 각 엘리먼트 값을 1차원 배열로 펼치고
// 다시 1차원 배열을 문자열로 연결하여 반환한다.
console.log([["가"], ["다"]].toString()); // 가,다
```

<br>

## toLocaleString()

- 엘리먼트 값을 **지역화 문자**로 반환한다.
  - 문자열을 콤마로 연결하여 반환한다.

<br>

# 8. 엘리먼트 삭제

## shift()

- 배열의 첫 번째 엘리먼트를 삭제한다
- 삭제한 엘리먼트 값이 `undefined`로 남지 않고 완전히 삭제된다.
  - `length` 값이 하나 줄어든다.
- 삭제한 엘리먼트를 반환한다.
  - 빈 배열이면 `undefined`가 반환된다.

<br>

## pop()

- 배열의 마지막 엘리먼트를 삭제한다.
- 삭제되는 엘리먼트의 위치를 제외한 나머지는 `shift()`와 동일하다.

<br>

## splice()

- 엘리먼트를 삭제하고 삭제한 엘리먼트를 반환한다.
- 삭제한 위치에 세 번째 파라미터를 삽입한다.
- 파라미터를 작성하지 않으면 아무것도 삭제하지 않는다.
  - 삭제한 것이 없으므로 빈 배열을 반환한다.

```js
// 파라미터 모두 작성한 경우
// 파라미터: 시작 인덱스(디폴트: 0), 삭제할 엘리먼트 수
var value = [1, 2, 3, 4, 5];
console.log(value.splice(1, 3)); // [2, 3, 4]
console.log(value); // [1, 5]

// 세 번째 파라미터 작성한 경우
var value = [1, 2, 3, 4, 5];
console.log(value.splice(1, 3, "A", "B")); // [2, 3, 4]
console.log(value); // [1, A, B, 5]
```

<br>

# 9. sort(분류)

## sort()

- 엘리먼트 값을 오름차순으로 정렬한다.
- 정렬 기준은 엘리먼트 값의 Unicode이다.
  - 코드 포인트가 작으면 앞에 오고 크면 뒤에 온다.
- **주의:** sort 대상 배열도 정렬된다.
  - 정렬되지 않은 값이 필요하다면 원본 배열을 미리 복사해둬야 한다.

```js
var value = [4, 3, 2, 1];
console.log(value.sort()); // [1, 2, 3, 4]
console.log(value); // [1, 2, 3, 4]
```

- 값이 `undefined`이면 끝으로 이동한다.

```js
var value = [, , 1, 2];
console.log(value.sort()); // [1, 2, undefined, undefined]
```

<br>

## sort()와 unicode

- 숫자에 해당하는 Unicode의 code point로 정렬한다.

```js
// 우리가 생각하는 일반적인 정렬은 [7, 26, 101, 1234]이다.
// 그러나 코드 포인트로 비교하여 정렬하기 때문에 다음과 같은 결과가 나온다.
var value = [101, 26, 7, 1234];
console.log(value.sort()); // [101, 1234, 26, 7]
```

- 이를 해결하려면 `sort()`의 파라미터에 콜백함수를 작성하고 콜백함수 내에서 정렬해야 한다.

<br>

# 10. sort 알고리즘

```js
var value = [101, 26, 7, 1234];
value.sort(function (one, two) {
  return one - two;
});
console.log(value); // [7, 26, 101, 1234]
```

- sort()를 반복할 때마다 JS 엔진이 콜백함수를 호출해준다.
- `one(101) - two(26)`의 결과는 양수이고, 이 값이 반환된다.
  - 이때 0보다 큰 값이 반환되면 배열에서 값의 위치를 바꾼다.
  - 0보다 작거나 같으면 값의 위치를 바꾸지 않는다.
- 위치가 바뀌는 것이 하나도 없을 때까지 반복하면서 엘리먼트 위치를 조정한다.

<br>

## reverse()

- 배열의 엘리먼트 **위치**를 역순으로 바꾼다.
  - 엘리먼트 값이 아니라 **인덱스** 기준이다.
  - 대상 배열도 바뀐다.

```js
var value = [1, 3, 7, 5];
console.log(value.reverse()); // [5, 7, 3, 1]
```
