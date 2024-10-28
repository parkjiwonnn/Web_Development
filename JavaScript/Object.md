## 객체

```jsx
const superman = {
  name: "clark",
  age: 33,
};

// 프로퍼티: key와 value로 구성
// 각 프로퍼티는 쉼표로 구성
// 마지막 프로퍼티는 쉼표가 없어도 되지만,
// 있는 게 수정, 삭제, 이동에 용이
```

```jsx
// 접근

superman.name; // 'clark'
superman["age"]; // 33

// 추가

superman.gender = "male";
superman["hairColor"] = "black";

// 삭제

delete superman.hairColor;
```

```jsx
// 단축 프로퍼티

const name = "clark";
const age = 33;

const superman = {
  name: name,
  age: age,
  gender: "male",
};

const superman = {
  name, // name: name
  age, // age: age
  gender: "male",
};
```

```jsx
// 프로퍼티 존재 여부 확인

const superman = {
  name: "clark",
  age: 33,
};

superman.birthDay;
// undefined (에러x, if문에서 false로 인식)

"birthDay" in superman; // false

"age" in superman; // true

// 어떤 값이 넘어올 지 확신할 수 없을 때 사용
// 함수의 인자로 받거나,
// API 통신을 통해 데이터를 받아올 때
```

```jsx
// for ... in 반복문
// 객체를 순회하며 값을 얻어올 수 있음

for (let key in superman) {
  console.log(key);
  console.log(superman[key]);
}
```

```jsx
// method: 객체 프로퍼티로 할당 된 함수

const superman = {
	name: 'clark',
	age: 33,
	// method
	fly: function() {
		console.log('날아갑니다.')
	}
	// 단축 구문
	fly() {
		console.log('날아갑니다.')
	}
}

superman.fly(); // 날아갑니다.
```

```jsx
// this

let boy = {
	name: 'Mike',
	sayHello,
}

let girl = {
	name: 'Jane'.
	sayHello,
}

sayHello: function() {
	console.log(`Hello, I'm ${this.name}`);
}

// this는 런타임(실행하는 시점)에 결정
boy.sayHello(); // I'm Mike
girl.sayHello(); // I'm Jane
```

```jsx
// this와 화살표 함수

sayHello() => {
	console.log(`Hello, I'm ${this.name}`);
}

boy.sayHello(); // I'm ???
girl.sayHello(); // I'm ???

// 화살표 함수는 일반 함수와는 달리 자신만의 this를 가지지 않음
// 화살표 함수 내부에서 this를 사용하면, 그 this는 외부에서 값을 가져옴

let boy = {
	name: 'Mike',
	sayHello() => {
		console.log(this); // 전역객체
	}
}

boy.sayHello(); // this != boy

// 브라우저 환경에서 전역객체: window
// Node js에서 전역객체: global
```
