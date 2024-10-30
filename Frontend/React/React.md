# 리액트 동작 원리

- 리액트 : 자바스크립트 UI 라이브러리
- 상태값이 변경되거나, 부모 컴포넌트가 재랜더링 될 때마다 UI를 자동으로 업데이트해주는 JS 라이브러리
- 가상 DOM을 통해 변경된 부분만 효율적으로 업데이트
  - 컴포넌트의 상태값이 변경되면, 새로운 가상 DOM 객체를 만들고, 이전 가상DOM 객체와 비교
  - 최종적으로 바뀐 부분이 있을 경우, 해당 부분만 실제 DOM에 반영하여 UI를 업데이트

## VirtualDOM

- 실제 DOM의 구조를 분석하여, 아래와 같은 형태로 메모리에 저장하고 관리하는 자바스크립트 객체

```jsx
{
    type: 'div',
    props: {
        children: [
            {
                type: button,
                props: {
                    children: "버튼입니다",
                    onClick: ()=>{}
                }
            },
            {
                type: input,
                props: {children: "인풋입니다."}
            },
            {
                type: CountButton,
                props: {children: "리액트컴포넌트입니다"}
            }
        ]
    }
}
```

## 리액트 UI 업데이트 단계

- Render Phase
  - 랜더링 할 때마다 매번 새로운 가상 DOM을 만들고, 이전 가상 DOM과 비교하여 바뀐 부분을 탐색하고, 실제 DOM에 반영할 부분 결정
- Commit Phase
  - 랜더 단계를 거쳐 바꾸기로 결정된 부분만 실제 DOM에 반영
  - 브라우저는 변경된 실제 DOM을 화면에 paint (didMount, didUpdate가 완료되어 useEffect가 호출되는 시점)
