# Flexbox

## justify-content

Flex 요소들을 가로선 상에서 정렬

- flex-start: 요소들을 컨테이너의 왼쪽으로 정렬
- flex-end: 요소들을 컨테이너의 오른쪽으로 정렬
- center: 요소들을 컨테이너의 가운데로 정렬
- space-between: 요소들 사이에 동일한 간격
- space-around: 요소들 주위에 동일한 간격

## align-items

Flex 요소들을 세로선 상에서 정렬

- flex-start: 요소들을 컨테이너의 꼭대기로 정렬
- flex-end: 요소들을 컨테이너의 바닥으로 정렬
- center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬
- baseline: 요소들을 컨테이너의 시작 위치에 정렬
- stretch: 요소들을 컨테이너에 맞도록 늘림

## flex-direction

정렬할 방향 지정

- row: 요소들을 텍스트의 방향과 동일하게 정렬
- row-reverse: 요소들을 텍스트의 반대 방향으로 정렬
- column: 요소들을 위에서 아래로 정렬
- column-reverse: 요소들을 아래에서 위로 정렬

#### 1. column-reverse 또는 row-reverse를 사용하면 요소들의 start와 end의 순서도 뒤바뀜

```css
/* (ex) . . . G Y R */
#pond {
  display: flex;
  flex-direction: row-reverse; /* . . . R Y G */
  justify-content: flex-end; /* R Y G */
}
```

#### 2. Flex의 방향이 column일 경우 justify-content의 방향이 세로로, align-items의 뱡향이 가로로 바뀜

```css
/* (ex) G Y R . . */
#pond {
  display: flex;
  flex-direction: column;
  /* G
     Y
     R
     .
     . */
  justify-content: flex-end;
  /* G
     Y
     R */
}
```

## order

Flex 요소의 순서 지정  
`<integer>` ( ... -1, 0 (default), 1, ...)

```css
/* (ex) G Y R */
#pond {
  display: flex;
}

.yellow {
  order: 1; /* G R Y */
}
```

```css
/* (ex) G G G R G */
#pond {
  display: flex;
}

.red {
  order: -1; /* R G G G G */
}
```

## align-self

지정된 align-items 값을 무시하고 Flex 요소를 세로선 상에서 정렬  
align-items가 사용하는 값들을 인자로 받으며, 그 값들은 지정한 요소에만 적용

```css
/* (ex) G G Y G G */
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
  align-self: flex-end;
  /* G G   G G 
         Y     */
}
```

```css
/* (ex) Y G Y G G */
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
  align-self: flex-end;
  /*   G   G G
     Y   Y     */
  order: 1 /* G G G
                    Y Y */;
}
```

## flex-wrap

Flex 요소들을 한 줄 또는 여러 줄에 걸쳐 정렬

- nowrap: 모든 요소들을 한 줄에 정렬
- wrap: 요소들을 여러 줄에 걸쳐 정렬
- wrap-reverse: 요소들을 여러 줄에 걸쳐 반대로 정렬

## flex-flow

flex-direction과 flex-wrap이 자주 같이 사용되기 때문에, flex-flow가 이를 대신할 수 있음  
공백문자를 이용하여 두 속성의 값들을 인자로 받음  
`<flex-direction> <flex-wrap>`

## align-content

세로선 상에 여분의 공간이 있는 경우 Flex 컨테이너 사이의 간격을 조절

- flex-start: 여러 줄들을 컨테이너의 꼭대기에 정렬
- flex-end: 여러 줄들을 컨테이너의 바닥에 정렬
- center: 여러 줄들을 세로선 상의 가운데에 정렬
- space-between: 여러 줄들 사이에 동일한 간격
- space-around: 여러 줄들 주위에 동일한 간격
- stretch: 여러 줄들을 컨테이너에 맞도록 늘림

align-content는 여러 줄들 사이의 간격을 지정하며, align-items는 컨테이너 안에서 어떻게 모든 요소들이 정렬하는지를 지정  
한 줄만 있는 경우, align-content는 효과를 보이지 않음

## 참고

https://flexboxfroggy.com/#ko (24단계 완료)
