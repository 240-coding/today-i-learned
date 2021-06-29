# Promise

자바스크립트 안에 내장되어 있는 object. 비동기적인 것을 수행하기 위해 콜백함수 대신 사용된다.

## 1. state : 상태

- 무거운 operation을 수행하고 있는지, 혹은 기능 수행이 완료되어서 성공했는지 혹은 실패했는지와 같은 상태를 이해하는 것이 중요하다.
- pending : operation을 실행 중인 상태
- fulfilled : operation을 성공적으로 마침
- rejected : 파일을 찾을 수 없거나 네트워크에 문제가 생겼을 때

## 2. producer와 consumer의 차이점 이해

### producer

```
// when new Promise is created, the executor runs automatically.
const promise = new Promise((resolve, reject) => {
    // doing some heavy work (network, read files)
    console.log('doing something...');
    setTimeout(() => {
        resolve('ellie');
        // reject(new Error('no network'));
    }, 2000);
});
```

- 사용자가 요구했을 때만 네트워크 요청을 해야 되는 경우라면 위와 같은 코드는 불필요한 네트워크 통신이 이루어질 수 있다.

### consumer

- then, catch, finally 이용해서 값을 받아옴.

```
// then : promise가 정상적으로 수행되어서 resolve() 콜백함수로 전달된 값이 value의 parameter로 전달되어서 들어온다.
// promise의 then을 호출하면 이는 결국 똑같은 promise를 리턴하기 때문에 그 리턴된 promise의 catch를 다시 호출할 수 있는 것.
// finally : 성공, 실패에 관련없이 무조건 호출됨

promise //
    .then((value) => {
        console.log(value);
    })
    .catch(error => {
        console.log(error);
    })
    .finally(() =>{
        console.log('finally');
    });


```
