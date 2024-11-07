# Flexbox

## justify-content

- flex-start: 요소들을 컨테이너의 왼쪽으로 정렬
- flex-end: 요소들을 컨테이너의 오른쪽으로 정렬
- center: 요소들을 컨테이너의 가운데로 정렬
- space-between: 요소들 사이에 동일한 간격
- space-around: 요소들 주위에 동일한 간격

## align-items

- flex-start: 요소들을 컨테이너의 꼭대기로 정렬
- flex-end: 요소들을 컨테이너의 바닥으로 정렬
- center: 요소들을 컨테이너의 세로선 상의 가운데로 정렬
- baseline: 요소들을 컨테이너의 시작 위치에 정렬
- stretch: 요소들을 컨테이너에 맞도록 늘림

## flex-direction

- row: 요소들을 텍스트의 방향과 동일하게 정렬
- row-reverse: 요소들을 텍스트의 반대 방향으로 정렬
- column: 요소들을 위에서 아래로 정렬
- column-reverse: 요소들을 아래에서 위로 정렬

## example

1.  column-reverse 또는 row-reverse를 사용하면 요소들의 start와 end의 순서도 뒤바뀜

```css
// (ex) . . . G Y R
#pond {
  display: flex;
  flex-direction: row-reverse; // . . . R Y G
  justify-content: flex-end; // R Y G
}
```

2. Flex의 방향이 column일 경우 justify-content의 방향이 세로로, align-items의 뱡향이 가로로 바뀜

```css
// (ex) G Y R . .
#pond {
  display: flex;
  flex-direction: column;
  // G
  // Y
  // R
  // .
  // .
  justify-content: flex-end;
  // G
  // Y
  // R
}
```

3. order: flex 요소의 순서 지정 <integer> ( ... -1, 0 (default), 1, ...)

```css
// (ex) G Y R
#pond {
  display: flex;
}

.yellow {
  order: 1; // G R Y (Y 순서 변경)
}
```

```css
// (ex) G G G R G
#pond {
  display: flex;
}

.red {
  order: -1; // R G G G G
}
```

4. align-self: 개별 요소에 적용할 수 있는 또 다른 속성

- align-items가 사용하는 값들을 인자로 받으며, 그 값들은 지정한 요소에만 적용
- 지정된 align-items 값을 무시하고 Flex 요소를 세로선 상에서 정렬

```css
// (ex) G G Y G G
#pond {
  display: flex;
  align-items: flex-start;
}

.yellow {
  align-self: flex-end;
  // G G   G G
  //     Y
}
```

## 참고

https://flexboxfroggy.com/#ko
