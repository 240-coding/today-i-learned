# 1. Array 오브젝트(ES5)

## isArray()

- 체크하는 대상이 배열이면 `true`, 아니면 `false`를 반환한다.
- `isArray()`는 함수이다.
  - `Array.isArray()` 형태로 호출해야 한다.

### `isArray()`가 필요한 이유

```js
console.log(typeof { a: 1 }); // object
console.log(typeof [1, 2]); //object
console.log(typeof null); // object
```

- `typeof` 연산자로 위와 같은 값들의 데이터 타입을 구하면 모두 `object`가 나오기 때문에 배열 여부를 체크할 수 없다.
- `[1, 2]`는 `Array.isArray()`를 사용하여 데이터 타입을 체크한다.
- `null`은 `Object.is()`를 사용하여 체크한다.
- 서버에서 JSON 데이터를 읽을 때 많이 사용한다.

<br>

# 2. index 처리 메소드

## indexOf()

- 파라미터 값과 같은 엘리먼트의 인덱스를 반환한다.
  - 왼쪽에서 오른쪽으로 검색한다.
  - 값이 같은 엘리먼트가 있으면 더이상 검색하지 않고 종료한다.
  - 데이터 타입까지 체크한다.
  - 같은 값이 없으면 -1을 반환한다.
- 두 번째 파라미터의 인덱스부터 검색한다.

## `String`과 `Array`의 `indexOf()` 차이

```js
console.log("ABCBC".indexOf("C", -2)); // 2
var list = ["A", "B", "C", "B", "C"];
console.log(list.indexOf("C", -2)); // 4
```

- 두 번째 파라미터에 음수를 작성했을 때 검색 방법이 다르다.
- String 오브젝트는 0으로 간주하여 처음부터 검색한다.
- Array 오브젝트는 음수에 `length`를 더해 시작 인덱스로 사용한다.

<br>

## lastIndexOf()

- 파라미터 값과 같은 엘리먼트의 마지막 인덱스를 반환한다.
  - 오른쪽에서 왼쪽으로 검색한다는 의미이기도 하다.
- 다른 처리 방법은 `indexOf()`와 같다.

```js
var value = [1, 2, 5, 2, 5];
console.log(value.lastIndexOf(5)); // 4
```

<br>

# 3. 콜백 함수를 가진 Array 메소드

- **시맨틱과 독립성**을 생각하자!

## forEach()

- 배열의 엘리먼트를 하나씩 읽어가면서 콜백 함수를 호출한다.
- 콜백 함수의 파라미터는 **엘리먼트 값, 인덱스, 배열 전체**이다.
- `break`, `continue`는 사용할 수 없다.
  - 반드시 처음부터 끝까지 돌아야 한다.
  - `throw`는 사용 가능하다.
- 콜백 함수 분리(독립성)

```js
var list = ["A", "B", "C"];
list.forEach(function (el, index, all) {
  console.log(el + ":" + index + ":" + all);
});
// A:0:A,B,C
// B:1:A,B,C
// C:2:A,B,C

// 콜백 함수 분리
// 코드 중복을 피하기 위함
var list = ["A", "B", "C"];
var fn = function (el, index, all) {
  console.log(el + ":" + index + ":" + all);
};

list.forEach(fn);
// 콜백함수를 분리했을 뿐 위의 forEach문과 코드가 같다.
```

- `this`로 오브젝트를 참조한다.

```js
var list = [1, 2];
var fn = function (el, indexl, all) {
  console.log(el + this.ten);
};

list.forEach(fn, { ten: 10 });
// 11
// 12
```

<br>

# 4. for()와 forEach()의 차이

## forEach()

- forEach()를 시작할 때 반복 범위를 결정한다.
- 반복 도중에 엘리먼트를 추가하면 처리하지 않는다.
- 현재 인덱스보다 큰 인덱스의 값을 변경하면 변경된 값을 사용한다.
  - 현재 인덱스보다 작은 인덱스의 값을 변경하면 처리하지 않는다.
- 현재 인덱스보다 큰 인덱스의 엘리먼트를 삭제하면 배열에서 삭제되므로 반복에서 제외한다.
  - 추가는 처리하지 않지만 삭제는 반영된다!

<br>

## for()와 forEach()

- forEach()는 **시맨틱 접근**
  - 처음부터 끝까지 반복한다는 시맨틱
  - 반복 중간에 끝나지 않는다는 시맨틱
  - 시맨틱으로 소스 코드의 가독성이 향상된다.
- for()는 함수 코드를 읽어야 의미를 알 수 있다.
  - 시맨틱 접근이 아니다.
  - break, continue를 사용할 수 있기 때문
- forEach()는 반복만 하여 콜백 함수에서 기능 처리, `this`를 사용할 수 있다.
- forEach()는 인덱스 0부터 시작한다.
  - for()와 같이 인덱스 증가 값을 조정할 수 없다.
  - 뒤에서 앞으로 읽을 수 없다.
    - **시맨틱 접근**

<br>

# 5. true, false를 반환하는 메소드

## every()

- forEach()와 같은 시맨틱 접근
- 배열의 엘리먼트를 하나씩 읽어가면서 **false를 반환할 때까지** 콜백 함수를 호출한다.
  - 즉 `false`가 반환되면 반복을 종료한다.
  - `false`를 반환하지 않으면 `true`를 반환한다.
- `false`가 되는 조건이 배열의 앞에 있으면 효율성이 높다.

```js
var value = [20, 10, 30, 40];
var fn = function(el, index, all) {
    console.log(el);
    return el > 15;
});
var result = value.every(fn);
console.log("결과: ", result);
// 실행 결과
// 20
// 10
// 결과: false
```

<br>

## some()

- every()처럼 시맨틱 접근
- 단, **true를 반환할 때까지** 콜백 함수를 호출한다.
  - 즉, `true`가 반환되면 반복을 자동으로 종료한다.
  - `true`를 반환하지 않으면 `false`를 반환한다.
- `true`가 되는 조건이 배열의 앞에 있을 때 효율성이 높다.

<br>

# 6. 필터, 매핑

## filter()

- forEach()처럼 시맨틱 접근
- 배열의 엘리먼트에서 하나씩 읽어가면서 콜백 함수에서 `true`를 반환하면 현재 읽은 엘리먼트를 반환한다.
  - 다수를 반환할 수 있으므로 반환되는 엘리먼트를 배열에 첨부한다.
- 조건에 맞는 엘리먼트를 추려낼 때 유용하다.

```js
var value = [10, 20, 30, 40];
var fn = function (el, index, all) {
  return el > 15;
};
var result = value.filter(fn);
console.log(result); // [20, 30, 40]
// true가 하나도 없으면 빈 배열이 result 변수에 할당된다.
```

<br>

## map()

- forEach()처럼 시맨틱 접근
- 배열의 엘리먼트를 하나씩 읽어가면서 콜백 함수에서 반환한 값을 새로운 배열에 첨부하여 반환한다.
- forEach()와 map()은 반환 여부의 차이가 있다.
  - 사용 목적 역시 다르다.

```js
var value = [10, 20, 30];
var fn = function (el, indexl, all) {
  return el + this.add;
};

var point = { add: 100 };
var result = value.map(fn, point);
console.log(result); // [110, 120, 130]
```

<br>

# 7. 반환 값을 파라미터 값으로 사용

## reduce()

- forEach()처럼 시맨틱 접근
- 배열 끝까지 콜백 함수 호출
  - 파라미터 작성 여부에 따라 처리가 다르다.
  - 첫 번째 파라미터에 콜백 함수를 전달하고 두 번째 파라미터에는 초깃값을 전달할 수 있다.

### 콜백 함수만 작성한 경우 (즉, 파라미터를 하나만 작성한 경우)

```js
var value = [1, 3, 5, 7];
var fn = function (prev, curr, index, all) {
  console.log(prev + "," + curr);
  return prev + curr;
};
var result = value.reduce(fn);
console.log("결과:", result);
// 실행 결과
// 1,3
// 4,5
// 9,7
// 결과:16
```

- 처음 콜백 함수를 호출할 때
  - 인덱스 [0]의 값을 직전 값에 설정한다.
  - 인덱스 [1]의 값을 현재 값에 설정한다.
  - 인덱스에 1을 설정한다.
- 두 번째로 콜백 함수를 호출할 때
  - 콜백 함수에서 반환된 갑승ㄹ 직전 값에 설정한다.
  - 인덱스 [2]의 값을 현재 값에 설정한다.
- 위의 코드가 4번이 아니라 3번 반복한 것은 처음 시작할 때 인덱스가 1이기 때문이다.

### 두 번째 파라미터를 작성한 경우

```js
var value = [1, 3, 5, 7];
var fn = function (prev, curr, index, all) {
  console.log(prev + "," + curr);
  return prev + curr;
};
var result = value.reduce(fn, 7);
console.log("반환:", result);
// 실행 결과
// 7,1
// 8,3
// 11,5
// 반환:16
```

- 처음 콜백 함수를 호출할 때
  - 두 번째 파라미터 값을 직전 값에 설정한다.
  - 인덱스 [0]의 값을 현재 값에 설정한다.
  - 인덱스에 0을 설정한다.
- 두 번째로 콜백 함수를 호출할 때
  - 콜백 함수에서 반환된 값을 직전 값에 설정한다.
  - 인덱스 [1]의 값을 현재 값에 설정한다.

<br>

## reduceRight()

- `reduce()`와 처리 방법이 같다.
- 단, 배열 **끝에서 앞으로** 하나씩 읽어가면서 콜백 함수에서 반환한 값을 반환한다.

```js
var value = [1, 3, 5, 7];
var fn = function(prev, curr, index, all) {
var fn = function(prev, curr, index, all) {
    console.log(prev + "," + curr);
    return prev + curr;
};
var result = value.reduceRight(fn);
console.log("반환:", result);
```
