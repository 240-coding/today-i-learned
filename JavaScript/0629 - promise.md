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

# 3. Promise chaining (added on 2 July)

```
const fetchNumber = new Prommise((resolve, reject) => {
    setTimeout(() => resolve(1), 1000);
})

// then은 값을 바로 전달해도 되고 또 다른 비동기인 Promise를 전달해도 된다.
fetchNumber
    .then(num => num * 2)
    .then(num => num * 3)
    .then(num => {
        return new Promise((resolve, reject) => {
            setTimeout(() => resolve(num - 1), 1000);
    })
})
.then(num => console.log(num));
```

# 4. Error Handling

```
const getHen = () =>
    new Promise((resolve ,reject) => {
        setTimeout(() => resolve('🐓'), 1000);
});
const getEgg = hen =>
    new Promise((resolve, reject) => {
        setTimeout(() => reject(new Error(`error! ${hen} => 🥚`)), 1000);
});
const cook = egg =>
    new Promise((resolve, reject) => {
        setTimeout(() => resolve(`${egg} => 🍳`), 1000);
});

getHen()
    .then(hen => getEgg(hen))
    .then(egg => cook(egg))
    .then(meal => console.log(meal));

// 한 가지만 받아서 그대로 전달하는 경우에는 생략 가능.
// then에서 받아온 value를 함수에 암묵적으로 전달해서 호출 가능.
getHen() //
    .then(getEgg)
    .catch(error => {
        return '🥖';
    })
    .then(cook)
    .then(console.log)
    .catch(console.log);
// result : 🥖 => 🍳
// 계란을 받아오는 것은 실패했지만 빵을 대신 전달해주었기 때문에 promise chain이 실패하지 않음.
```
