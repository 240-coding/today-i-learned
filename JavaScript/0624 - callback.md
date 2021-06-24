# 1. 동기와 비동기

- JavaScript is synchronous.
- hoisting이 된 이후부터 코드가 작성한 순서에 맞춰서 하나씩 동기적으로 실행된다.
- hoisting : var, function declaration이 자동적으로 제일 위로 올라가는 것.

- asynchronous : 코드가 언제 실행될지 예측할 수 없는 것.
  ex) `setTimeOut()` 함수는 지정한 시간이 지나면 우리가 전달한 콜백 함수를 호출한다.

# 2. 콜백 함수

우리가 전달한 함수를 나중에 불러달라고 하는 것. 보통 `arrow function`을 사용해서 표현한다.

### Synchronous callback

```
function printImmediately(print) {
    print();
}
printImmediately(() => console.log('hello'));
```

### Asynchronous callback

```
function printWithDelay(print, timeout) {
    setTimeout(print, timeout);
}
printWithDelay(() => console.log('async callback'), 2000);
```
