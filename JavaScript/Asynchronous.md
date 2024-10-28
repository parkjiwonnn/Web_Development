# 비동기 함수

- 자바스크립트는 싱글스레드이기 때문에 한 번에 하나의 작업만 수행 가능 ⇒ 이를 해결하기 위해 비동기 사용
- 비동기 : 특정 코드의 처리가 끝나기 전에 다음 코드를 실행할 수 있는 것
- 즉시 처리하지 못하는 이벤트들을 이벤트 루프에 모아 놓고 먼저 처리해야하는 이벤트를 실행

```jsx
console.log("Start");

setTimeout(function () {
  console.log("5초 후 실행");
}, 5000);

console.log("End");

// 실행 결과
// 'start'
// 'end'
// '5초 후 실행'
```

## Callback 함수

- 콜백 함수는 하나만 썼을 때는 간단하지만, 비동기로 함수의 매개 변수에 다른 콜백함수가 중첩되어 사용된다면 그 코드를 보기에 굉장히 어렵고 유지보수도 힘들어짐
- 각 콜백 함수마다 에러 처리를 써야하는데 코드량도 어마어마해짐

```jsx
step1(function (err, value1) {
  if (err) {
    console.log(err);
    return;
  }
  step2(function (err, value2) {
    if (err) {
      console.log(err);
      return;
    }
    step3(function (err, value3) {
      if (err) {
        console.log(err);
        return;
      }
      step4(function (err, value4) {
        // ,...
      });
    });
  });
});
```

## Promise

- 콜백 함수의 error, success의 처리를 간단하게 하기 위해 사용

### Promise 생성 및 상태

- new Promise()로 생성 가능
- 종료될 때 세 가지 상태를 가짐
  - Pending(대기) : 이행하거나 거부되지 않은 초기 상태
  - Fulfilled(이행) : 완료되어 프로미스가 결과 값을 반환해준 상태
  - Rejected(거부) : 실패하거나 오류가 발생한 상태
- resolve와 reject 2개의 인자를 받으며, 비동기 처리가 성공하면 resolve가 호출되고, 실패하면 reject가 호출됨

```jsx
const promise = new Promise((res, rej) => {
  setTimeout(() => {
    res("성공");
  }, 1000);
});
```

### Promise Chaining

- .then()을 이용해서 여러 개의 Promise를 이을 수 있음

```jsx
new Promise(function (resolve, reject) {
  setTimeout(function () {
    resolve(0);
  }, 2000);
})
  .then(function (result) {
    console.log(result); // output: 0
    return result + 10;
  })
  .then(function (result) {
    console.log(result); // output: 10
    return result + 20;
  })
  .then(function (result) {
    console.log(result); // output: 30
  });
```

- 에러 처리를 위해 catch() 사용

```jsx
const promise = new Promise((res, rej) => {
  setTimeout(() => {
    rej("에러 발생");
  }, 1000);
});

promise.then((res) => console.log(res)).catch((err) => console.error(err));
// output: 에러 발생
```

```jsx
console.log("hi");

setTimeout(function () {
  console.log("0.1");
}, 100);

Promise.resolve()
  .then(function () {
    console.log("first");
  })
  .then(function () {
    console.log("second");
  });

setTimeout(function () {
  console.log("0");
}, 0);

console.log("end");

// 실행 결과
// hi
// end
// first
// second
// 0
// 0.1
```

- setTimeout()과 Promise는 모두 비동기 함수이지만, setTimeout은 태스크 큐이고, Promise는 비동기 중에서도 먼저 실행되는 마이크로태스크 큐에 들어있기 때문에 먼저 실행됨
- 이벤트 루프는 콜 스택이 비면 먼저 마이크로테스크 큐에서 대기하고 있는 함수를 실행하고, 이후에 태스크 큐에서 대기하고 있는 함수를 가져와 실행함

## async await

- Promise의 메서드 체이닝을 더 깔끔한 코드를 작성할 수 있게끔 만들어진 것
- 함수 앞에 async를 붙이고, 비동기 처리할 코드 앞에 await을 붙임

```jsx
const asyncFunc = async () => {
  console.log("calling");
  await setTimeout(() => console.log("resolved"), 2000);
};

asyncFunc();

// 실행 결과
// calling
// resolved
```

- try와 catch로 성공 및 에러 여부 감지 가능
- async await을 사용하면 코드를 더 깔끔하게 작성 가능

```jsx
// Promise
const promise = new Promise((res, rej) => {
  console.log("first");
  setTimeout(() => {
    res("2초 후");
  }, 2000);
  console.log("end of function");
});

promise.then((res) => console.log(res)).catch((err) => console.error(err));
```

```jsx
// async await
const asyncFunc = async () => {
  try {
    console.log("first");
    await setTimeout(() => console.log("2초 후"), 2000);
  } catch (err) {
    console.log(err);
  }
  console.log("end of function");
};

asyncFunc();
```

[자바스크립트의 비동기 프로그래밍](https://www.howdy-mj.me/javascript/asynchronous-programming)

## JSON

- Javascript object notation
- 자바스크립트 객체 표기법으로 데이터를 쉽게 교환하고 저장하기 위한 텍스트 기반의 데이터 교환 표준
- JSON은 텍스트 기반이기 때문에 다양한 프로그래밍 언어에서 데이터를 읽고 사용가능
- JSON의 형태는 key와 value의 쌍으로 이루어져 있는 구조이고, key와 value 사이에는 콜론이 들어감
- 데이터를 나열할 경우 쉼표를 사용
- 객체는 중괄호로 묶어서 표현하고, 배열은 대괄호로 묶어서 표현
- 객체를 문자열로 변환하고(JSON.stringify), 문자열을 다시 객체로 변환하는(JSON.parse) 메소드를 제공
