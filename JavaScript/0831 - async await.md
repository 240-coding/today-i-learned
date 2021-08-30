# async, await

async와 await을 이용하면 동기식으로 코드를 작성하는 것처럼 간편하게 작성할 수 있다.
기존의 promise 위에 조금 더 간편한 api를 제공하는 것(syntactic sugar - 다른 기능이 추가된 것이 아님!).

```js
// async & await
// clear style of using promise

// 1. async
function fetchUser() {
    return new Promise((resolve, reject) => {
        // do network request in 10 secs...
        resolve('ellie'); // return 'ellie';
    });
}

// async 사용한 경우
// promise를 더 간편하게 사용
async function fetchUser() {
    // do network request in 10 secs...
    return 'ellie';
}
const user = fetchUser();
user.then(console.log);
console.log(user);
// 오래 걸리는 명령들은 비동기적으로 처리해야 한다.

// 2. await
function delay(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
}

async function getApple() {
    await delay(3000); // await - delay가 끝날 때까지 기다림
    return '🍎';
}

async function getBanana() {
    await delay(3000);
    return '🍌';
}

async function pickFruits() {
    // 사과와 바나나의 promise를 먼저 만듦
    const applePromise = getApple();
    const bananaPormise = getBanana();
    // 동시에 delay가 실행된 후 각각 기다림
    const apple = await applePromsie;
    const banana = await bananaPromise;
    return `${apple} + ${banana}`;
}

// promise 사용하는 경우 - chaining 필요
function getBanana() {
    return delay(3000);
    .then(() => '🍌');
}

function pickFruits() {
    return getApple()
    .then(apple => {
        return getBanana()
        .then(banana => `${apple} + ${banana}`);
    });
}

pickFruits().then(console.log);

// 3. useful Promise APIs
function pickAllFruits() {
    return Promise.all([getApple(), getBanana()])
    .then(fruits => fruits.join(' + '));
}
pickAllFruits().then(console.log);

function pickOnlyOne() {
    return Promise.race([getApple(), getBanana()]);
}

pickOnlyOne().then(console.log);
```
