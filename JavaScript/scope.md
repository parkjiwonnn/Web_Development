# 스코프

- 참조 대상 식별자(identifier, 변수, 함수의 이름과 같이 어떤 대상을 다른 대상과 구분하여 식별할 수 있는 유일한 이름)을 찾아내기 위한 규칙
- 식별자는 자신이 어디에서 선언됐는지에 의해 자신이 유효한(다른 코드가 자신을 참조할 수 있는) 범위를 가짐
- 스코프가 없다면 식별자 이름은 충돌을 일으키므로 프로그램 전체에서 하나밖에 사용할 수 없음

## 전역 스코프

- 전역에 변수를 선언하면 이 변수는 어디서든 참조할 수 있는 전역 스코프를 갖는 전역 변수가 됨
- var로 선언한 전역 변수 : 전역 객체 window의 프로퍼티

```jsx
var global = "global";

function foo() {
  var local = "local";
  console.log(global);
  console.log(local);
}
foo();

console.log(global);
console.log(local); // Uncaught ReferenceError: local is not defined
```

- C언어의 경우 main 함수가 시작점이 되기 때문에 대부분의 코드는 main 함수 내에 포함됨
- C언어에서 전역 변수를 선언하기 위해서는 의도적으로 main 함수 밖에 변수를 선언해야 함

```c
#include <stdio.h>

/* global variable declaration */
int g;

int main () {

  // local variable declaration
  int a, b;

  // actual initialization
  a = 10;
  b = 20;
  g = a + b;

  printf ("value of a = %d, b = %d and g = %d\n", a, b, g);

  return 0;
}
```

- 자바스크립트는 C-family language와는 달리 특별한 시작점이 없으며 코드가 나타나는 즉시 해석되고 실행됨
  - 따라서 전역에 변수나 함수를 선언하기 쉽고, 전역 변수를 남발하게 하는 문제가 발생할 수 있음

⇒ 전역 변수의 사용은 변수 이름이 중복될 수 있고, 의도치 않은 재할당에 의한 상태 변화로 코드를 예측하기 어렵게 만드므로 사용을 억제해야 함

- 최소한의 전역변수 사용
  - 전역 변수 사용을 최소화하기 위해 전역 변수 객체 하나를 만들어서 사용하는 방법
  ```jsx
  var MYAPP = {};

  MYAPP.student = {
    name: "Lee",
    gender: "male",
  };

  console.log(MYAPP.student.name);
  ```
- 즉시실행함수를 이용한 전역변수 사용 억제
  - 즉시 실행 함수는 즉시 실행되고 그 후 전역에서 바로 사라짐
  ```jsx
  (function () {
    var MYAPP = {};

    MYAPP.student = {
      name: "Lee",
      gender: "male",
    };

    console.log(MYAPP.student.name);
  })();

  console.log(MYAPP.student.name);
  ```

## 자바스크립트 스코프의 특징

- 대부분의 C-family language는 블록 레벨 스코프를 따름
- 블록 레벨 스코프 : 코드 블록({…})내에서 유효한 스코프
- 자바스크립트는 함수 레벨 스코프를 따름
- 함수 레벨 스코프
  - 함수 코드 블록 내에서 선언된 변수는 함수 코드 블록 내에서만 유효하고 함수 외부에서는 유효하지 않음
  ```jsx
  var x = 0;
  {
    var x = 1;
    console.log(x); // 1
  }
  // 블록 내에서 선언된 변수는 블록 밖에서도 접근 가능
  console.log(x); // 1

  // ECMAScript6에서 도입된 let을 사용하면 블록 레벨 스코프 적용
  let y = 0;
  {
    let y = 1;
    console.log(y); // 1
  }
  // 블록 내에서 선언된 변수는 블록 외부에서 접근 불가능
  console.log(y); // 0
  ```
  - 내부 함수의 경우, 전역 변수는 물론 상위 함수에서 선언한 변수에 접근/변경이 가능
  - 중첩 스코프는 가장 인접한 지역을 우선하여 참조
  ```jsx
  var x = 10;

  function foo() {
    var x = 100;
    console.log(x); // 100

    function bar() {
      // 내부함수
      x = 1000;
      console.log(x); // 1000
    }

    bar();
  }
  foo();
  console.log(x); // 1000
  ```
- 비 블록 레벨 스코프
  - 자바스크립트는 블록 레벨 스코프를 사용하지 않으므로 함수 밖에서 선언된 변수는 코드 블록 내에서 선언되었다할지라도 모두 전역 스코프를 가짐
  ```jsx
  if (true) {
    var x = 5; // 변수 x는 전역변수
  }
  console.log(x);
  ```
- 렉시컬 스코프
  - 동적 스코프 : 함수의 호출 시점으로 상위 스코프를 결정
  - 렉시컬 스코프 or 정적 스코프 : 함수의 선언 시점으로 상위 스코프를 결정
  - 자바스크립트를 비롯한 대부분의 프로그래밍 언어는 렉시컬 스코프를 따름
  - 동적 스코프를 따를 경우 함수 bar의 상위 스코프는 함수 foo와 전역
  - 렉시컬 스코프를 따를 경우 함수 bar의 스코프는 전역
  ```jsx
  var x = 1;

  function foo() {
    var x = 10;
    bar();
  }

  function bar() {
    console.log(x);
  }

  foo(); // 1
  bar(); // 1
  ```

## 암묵적 전역

- 선언하지 않은 식별자에 값을 할당하면 전역 객체의 프로퍼티가 됨
- 변수 선언없이 단지 전역 객체의 프로퍼티로 추가된 경우 변수가 아니기 때문에 변수 호이스팅이 발생하지 않음
- 변수가 아닌 프로퍼티는 delete 연산자로 삭제 가능
- 전역 변수는 프로퍼티이지만 delete 연산자로 삭제 불가능

```jsx
// 전역 변수 x는 호이스팅이 발생
console.log(x); // undefined
// 전역 변수가 아니라 단지 전역 프로퍼티인 y는 호이스팅이 발생하지 않음
console.log(y); // ReferenceError: y is not defined

var x = 10; // 전역 변수

function foo() {
  // 선언하지 않은 식별자
  // window.y = 20으로 해석하여 프로퍼티를 동적 생성함
  y = 20;
  console.log(x + y);
}

foo(); // 30
```
