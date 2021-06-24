# Array api

# map

지정된 콜백 함수를 호출하면서 각각의 요소들을 함수를 거쳐서 다시 새로운 값으로 변환하는 것. 우리가 전달한 콜백 함수가 어떤 일을 하냐에 따라 각 요소들이 다른 값으로 매핑되어 만들어질 것이다.

```
// 예시 1
const result = students.map((student) => student.score));
```

```
// 예시 2
const array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

# some

배열의 요소 중에서 콜백 함수가 true를 return하는 요소가 있는지 없는지를 확인한다.
