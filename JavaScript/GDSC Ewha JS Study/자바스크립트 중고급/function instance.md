# 생성자 함수

- new 연산자와 함께 인스턴스를 생성하는 함수
    - new Book()에서 Book()이 생성자 함수이다.
- new 연산자
    - 인스턴스 생성을 제어한다.
    - 생성자 함수를 호출한다.
- 생성자 함수
    - 인스턴스를 생성하고 반환한다.
    - 인스턴스에 초깃값을 설정한다.
- 코딩 관례로 생성자 함수의 첫 문자는 대문자를 쓴다.

## 생성자 함수 실행 과정

- new 연산자로 인스턴스 생성을 제어하고 생성자 함수인 Book()으로 인스턴스를 생성하여 반환한다.

# constructor 프로퍼티

```jsx
Book function 오브젝트: {
	prototype: {
		constructor: Book
	}
}
```

- 생성하는 function 오브젝트를 참조한다.
    - function 오브젝트를 생성할 때 설정한다.
    - prototype에 연결되어 있다.
- constructor가 없더라도 인스턴스가 생성되지만 필요하지 않은 것은 아니다.
    - ES5에서는 constructor를 변경할 수 없기 때문에 생성자를 활용할 수 없다.
    - ES6에서는 constructor를 변경할 수 있어 활용성이 높다.

# constructor 비교

```jsx
var Book = function(){};
var result = Book === Book.prototype.constructor;
console.log("1:", result);

var obj = new Book();
console.log("2:", Book === obj.constructor);

console.log("3:", typeof Book);
console.log("4:", typeof obj); 
// 1:true
// 2:true
// 3:function
// 4:object
```

1. Book 오브젝트와 Book.prototype.constructor가 타입까지 같다.
    - Book 오브젝트를 생성할 때 Book.prototype.constructor가 Book 오브젝트를 참조하기 때문
2. Book === obj.consructor;
    - obj의 constructor가 Book 오브젝트를 참조하므로 2번에 true가 출력된다.
3. function 오브젝트로 인스턴스를 생성했더니 object로 타입이 변경되었다.
    - 이는 [[Constructor]]가 실행될 때 생성한 오브젝트의 [[Class]]에 ‘Object’를 설정하기 때문이다.
4. 오브젝트 타입이 바뀐다는 것은 **오브젝트 성격과 목적이 바뀐 것을 뜻한다.**

# prototype, 상속

## prototype 오브젝트 목적

- prototype에 프로퍼티를 연결하여 prototype을 확장하기 위함
    - Book.prototype.getPoint = function(){}
- 프로퍼티를 공유하기 위함
    - 생성한 인스턴스에서 원본 prototype의 프로퍼티를 공유
    - var obj = new Book(123); obj.getPoint();
- 인스턴스 상속(Inheritance)
    - function 인스턴스를 연결하여 상속한다.
    - Point.prototype = new Book();
    - JS에서 상속은 ptototype의 확장을 의미하기도 한다.

## 인스턴스 상속

### 인스턴스 상속 방법

- ptototype에 연결된 프로퍼티로 인스턴스를 생성하여 상속받을 prototype에 연결한다.
- 그래서 prototype-based 상속이라고도 한다.
- JS에서 prototype은 상속보다 프로퍼티 연결이 의미가 더 크다.
    - 인스턴스 연결도 프로퍼티 연결의 하나이다.
- ES5 상속은 OOP의 상속 기능이 부족하다. ES6에서 Class로 상속이 가능하다.
- 

# prototype 확장

## prototype 확장 방법

- prototype에 프로퍼티를 연결하여 작성한다.
    - prototype.name = value 형태
- name에 프로퍼티 이름을 작성한다.
- value에 JS 데이터 타입을 작성한다. 일반적으로 function을 사용한다.
- prototype에 null을 설정하면 더 이상 확장이 불가능하다.

## 프로퍼티 연결 고려사항

- prototype에 연결할 프로퍼티가 많을 때
    - Book.prototype.name1, 2, 3 ~ N 형태는 Book.prototype을 반복해서 작성해야 하므로 번거롭다.
    - Book.prototype = {name1: value, ...} 형태로 작성한다.
- 위처럼 한꺼번에 할당하면 constructor가 지워진다.
    - {name1: value,...} 형태로 설정한 후 prototype에 constructor를 다시 연결한다.

## constructor 연결

```jsx
function Book(){};
Book.prototype = {
	constructor: Book,
	setPoint: function(){}
};
var obj = new Book();
console.log(obj.constructor); // function Book(){}
```

- 오브젝트 리터럴{}을 사용하여 프로퍼티를 연결할 때는 constructor가 지워지는 것을 고려해야 한다.
- constructor가 없어도 인스턴스가 생성되지만 constructor가 연결된 것이 정상이므로 constructor에 Book function을 할당한다.

# this와 prototype

## this로 인스턴스 참조

- this로 메소드를 호출한 인스턴스를 참조한다.
- 인스턴스에서 메소드 호출 방법
    - prototype에 연결된 프로퍼티가 __proto__에 설정되며 인스턴스 프로퍼티가 된다.
    - this.prototype.setPoint() 형태가 아닌 this.setPoint() 형태로 호출된다.

## prototype 메소드 직접 호출

```jsx
function Book(point) {
	this.point = point;
};
Book.prototype.getPoint = function(){
	return this.point;
};
var obj = new Book(100);
console.log(obj.getPoint()); // 100
console.log(Book.prototype.getPoint()); // undefined
```

- Book.prototype.getPoint();
    - 인스턴스를 생성하지 않고 직접 메소드를 호출한다.
- Book.prototype을 getPoint()에서 this로 참조한다.
- obj 인스턴스에는 point가 있지만 Book.prototype에 point가 없으므로 undefined를 반환한다.
    - 인스턴스를 생성하여 메소드를 호출하는 것과 직접 prototype을 작성하여 호출하는 것의 차이

# prototype 프로퍼티 공유 시점

## 프로퍼티 공유 시점

- 사용하는 시점, 즉 메소드를 호출하는 시점에 prototype의 프로퍼티를 공유한다.
- prototype의 프로퍼티로 인스턴스를 생성하지만, 인스턴스의 프로퍼티는 원본 prototype의 프로퍼티를 참조한다.
    - 복사하여 인스턴스에 갖고 있는 개념이 아니다.
- 인스턴스의 메소드를 호출하면 원본 prototype의 메소드를 호출한다.
- 원본 prototype에 메소드를 추가하면 생성된 모든 인스턴스에서 추가한 메소드를 사용할 수 있다.
    - 원본 prototype의 메소드를 호출하기 때문이다.

# 인스턴스 프로퍼티

```jsx
obj 인스턴스 = {
	point: 100,
	getPoint: function(){},
	__proto__: {
		getPoint: function(){}
	}
}
```

- prototype에 연결된 프로퍼티도 인스턴스 프로퍼티가 된다.
    - 직접 인스턴스에 연결된 프로퍼티와 차이가 있다.
- 인스턴스의 프로퍼티를 prototype으로 만든 인스턴스 프로퍼티보다 먼저 사용한다.
- 인스턴스마다 값을 다르게 가질 수 있다. → 인스턴스를 사용하는 중요한 목적!
