## this 동적 바인딩

- 자바스크립트는 함수 호출 방식에 의해 this에 바인딩 할 특정한 객체가 동적으로 결정됨
- 일반 함수 호출 시
  - 전역 객체에 바인딩
  ```jsx
  function foo() {
    console.log(this); // this === window(전역 객체)
  }

  foo();
  ```
- 객체의 메서드 호출 시
  - 객체에 바인딩
  ```jsx
  const person = {
    name: "steven",
    age: 99,
    gender: "Male",
    sayStack: function () {
      console.log(`${this.name} can use HTML, CSS, JS`);
    },
  };

  person.sayStack(); // steven can use HTML, CSS, JS
  ```
- 내부 함수 호출 시
  - 전역 객체 window에 바인딩
  ```jsx
  let age = 1;
  const animal = {
    name: "tiger",
    age: 5,
    showAge: function () {
      console.log(`${this.name} is ${this.age} years old`);

      function plusAge() {
        this.age++;
        console.log(`in this func, ${this.name} is ${this.age} years old`);
      }
      plusAge();
    },
  };

  animal.showAge();
  /*
  tiger is 5
  in this func,  is 2 years old
  */
  ```
  - 외부 함수의 this를 사용하기 위한 방법
    1. 외부 함수 내에서 객체에 바인딩 된 this를 새로운 변수에 담아주고, 내부 함수에서 접근
    2. 화살표 함수 사용
       - 화살표 함수는 this가 원래 존재하지 않음
       - 자바스크립트는 어떤 변수를 찾을 때 현재 스코프 또는 환경에서 해당 변수가 없으면 상위 환경을 탐색함
- 클래스 내부 생성자 함수 호출 시
  - 생성자 함수를 호출하려면 생성자 함수의 인스턴스를 만들어서 그 인스턴스를 통해 값 프로퍼티 또는 메서드에 접근하면 해당 값을 반환할 수 있음
  - 생성자 함수의 인스턴스에 바인딩
- 콜백 함수 호출 시
  - 전역 객체에 바인딩

## this 정적 바인딩

- this를 정적으로 고정하기 위해서는 화살표 함수를 사용하거나, bind(), call(), apply() 메서드를 사용할 수 있음
- bind 함수를 이용하여 수동적으로 바인딩 할 수 있음
- call 메서드는 인수 목록을 받고, apply 메서드는 인수 배열을 하나 받음
  - `call(this, var1, var2, var3, …)`
  - `apply(this, [ el, el2, el3, … ])`
- 화살표 함수는 생성 시점의 렉시컬 환경에서의 this를 기억하고 고정함
- 화살표 함수에서 this는 자신을 감싼 정적 범위
- call, bind, apply를 사용해도 바뀌지 않음
- 화살표 함수 밖에서 제일 근접한 스코프를 this가 가리킴
