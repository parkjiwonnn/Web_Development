# Class

- 객체를 생성하기 위한 템플릿
- 원하는 구조의 객체 틀을 짜놓고, 비슷한 모양의 객체를 공장처럼 찍어낼 수 있음
- 클래스 내에 정의된 함수를 method라고 부름
- 클래스를 통해 생성된 객체를 인스턴스라고 부름
- 클래스도 함수처럼 호출하기 전까지는 코드가 실행되지 않음
- constructor : class에서 필요한 기초 정보를 세팅하는 곳
  - 객체를 new로 생성할 때 가장 먼저 자동으로 호출됨
  - this는 본인 객체를 의미

```jsx
class Korean {
  constructor(name, age) {
    this.name = name;
    this.age = age;
    this.country = "Korea";
  }

  addAge(age) {
    return this.age + age;
  }
}
```

### 클래스 상속

- extend 키워드를 사용하면 자식 클래스에서 부모 클래스의 값을 사용할 수 있음

```jsx
class Pet {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }
  eat() {
    return `${this.name} is eating!`;
  }
}

class Cat extends Pet {
  meow() {
    return "MEOWWWW";
  }
}

class Dog extends Pet {
  bark() {
    return "WOOF";
  }
}

let boksil = new Dog("Boksil", 5);

boksil.eat(); // Boksil is eating!
```

- super 키워드를 사용해서 부모 클래스의 값을 상속받고, 추가적으로 자식만의 값을 사용할 수 있음
- 자식 클래스에서 this를 이용하여 새로운 프로퍼티를 부여하거나 상속받은 프로퍼티를 수정하고 싶다면 super()를 이용하여 부모 클래스의 기존 프로퍼티 값을 호출해야 함

```jsx
class Pet {
  constructor(name, age) {
    console.log("IN PET CONSTRUCTOR!");
    this.name = name;
    this.age = age;
  }
  eat() {
    return `${this.name} is eating!`;
  }
}

class Cat extends Pet {
  constructor(name, age, livesLeft = 9) {
    console.log("IN CAT CONSTRUCTOR!");
    super(name, age);
    this.livesLeft = livesLeft;
  }
  meow() {
    return "MEOWWWW";
  }
}

const monty = new Cat("monty", 9);
// IN CAT CONSTRUCTOR!
// IN PET CONSTRUCTOR!

console.log(monty); // Cat {name: 'monty', age: 9, livesLeft: 9}
```
