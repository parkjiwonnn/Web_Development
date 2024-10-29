# DOM

- Document Object Model
- HTML요소를 JavaScript Object처럼 조작할 수 있는 모델
- html의 작은 부분까지 접근할 수 있는 구조로, DOM을 이용하여 html로 구성된 웹페이지를 동적으로 움직이게 만들 수 있음
- dom의 구조는 트리구조로 body가 가장 상위에 있고, 아래에 여러 구성요소가 부모-자식 관계를 가지고 있음
- 자바스크립트와 같은 스크립팅 언어를 사용해 dom 수정이 가능함

## defer, async 스크립트

- 브라우저는 HTML 파일을 읽어온 후, 위에서부터 아래로 한 줄씩 해석을 시작함
- 스크립트 파일을 마주하는 경우에는, 해당 파일을 모두 해석하기 전까지 나머지 HTML 렌더를 일시적으로 멈춤
- async와 defer를 사용해면 브라우저가 스크립트 파일을 병렬로 불러오는 방식으로 DOM 렌더 과정을 막지 않게 선언할 수 있음

### async

- DOM이나 다른 스크립트에 의존성이 없고, 실행 순서가 중요하지 않은 경우에 사용
- DOM 렌더 과정을 방해하지 않도록 병렬로 로드함

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/5758e720-50f1-4ed8-a3e6-5617aa5e2838/5b8a5d62-adb2-48d4-bb2d-e2ba32454856/Untitled.png)

```jsx
<script src="analytics.js" async></script>
```

- 브라우저가 DOM을 구성하는 동시에 백그라운드에서 스크립트를 불러올 수 있음을 의미함
- async 속성 적용하면 스크립트를 불러오는 과정에서 DOM 렌더를 차단하지 않도록 보장함
- 하지만 async 스크립트는 오직 파일을 불러오는 것만 병렬로 실행함
- 실행 순서가 보장되지 않음
- 스크립트의 실행 순서를 조정할 수 없기 때문에, 만약 두 스크립트가 서로 의존성이 있다면 제대로 동작하지 않을 수 있음

### defer

- DOM이나 다른 스크립트에 의존성이 있고, 실행 순서가 중요한 경우에 사용
- defer 스크립트도 DOM 렌더를 방해하지 않고 병렬로 로드함
- 로드가 완료된 후 즉시 그 내용이 실행되는 async 스크립트와 다르게, defer 스크립트는 모든 DOM이 로드된 후에야 실행됨

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/5758e720-50f1-4ed8-a3e6-5617aa5e2838/1c347ece-8532-4415-a639-4aeb1cfdfdc1/Untitled.png)

```jsx
<script src="jquery.js" defer></script>
```

- 선언한대로 실행 순서가 보장됨
- 더 빨리 로드되는 스크립트가 있더라도, 실행은 항상 선언한 순서대로 실행됨

## 이벤트 버블링

- 이벤트가 발생하면 이 요소에 할당된 핸들러가 동작하고, 이어서 부모 요소의 핸들러가 동작하고, 최상단의 부모 요소를 만날 때까지 반복되면서 핸들러가 동작하는 현상

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/5758e720-50f1-4ed8-a3e6-5617aa5e2838/82a36efc-7170-48a4-9c64-ea26b95e95c2/Untitled.png)

- 거의 모든 이벤트는 버블링 됨
- focus 이벤트와 같이 버블링 되지 않은 이벤트도 존재
- 원하는 타겟에서만 이벤트를 발생하게 하고 싶을 때

```jsx
const clickEvent = (e) => {
  e.stopPropagation();
  console.log(e.currentTarget.className);
};
```

## 이벤트 캡처링

- 최상위 태그에서 이벤트가 발생한 태그까지 찾아 내려감

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/5758e720-50f1-4ed8-a3e6-5617aa5e2838/50bf8fa2-52c6-4eea-8616-d13acf0c0e18/Untitled.png)

- 캡처링을 이용하는 경우는 흔하지 않음
- 캡처링 단계에서 이벤트를 잡아내려면 addEventListener의 capture 옵션을 true로 설정해야 함

```jsx
elem.addEventListener(..., {capture: true})
elem.addEventListener(..., true)
```
