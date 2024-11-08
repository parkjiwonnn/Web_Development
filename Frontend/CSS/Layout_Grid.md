# Grid

## grid-column

그리드 요소의 열(column) 위치 지정  
`<grid-column-start> / <grid-column-end>`

```css
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}

#water {
  grid-column: 2 / span 3;
}
```

### grid-column-start

그리드 요소의 시작 열(column) 위치 지정  
`<integer> span <integer>`

### grid-column-end

- grid-column-start이 단독으로 사용될때는, 한개의 그리드 열(column)을 나타냄
- grid-column-end 속성을 같이 사용하면 여러 열(column)에 걸쳐 확장이 가능

1. grid-column-start 와 grid-column-end를 같이 사용할때, 시작 값보다 마지막 값이 더 크지 않아도 됨

```css
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}

#water {
  grid-column-start: 5;
  grid-column-end: 2;
}
```

2. 그리드 왼쪽의 기준이 아닌 오른쪽으로 기준을 하고싶다면, grid-column-start 와 grid-column-end를 음수로 설정  
   (ex) -1로 오른쪽 첫뻔재 세로선을 지정 가능

```css
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}

#water {
  grid-column-start: 1;
  grid-column-end: -2;
}
```

3. 그리드 선의 시작과 끝 위치를 기준으로 그리드 항목을 정의하는 대신, span을 이용하여 열(column)의 넓이를 지정 가능  
   span은 양수만 설정 가능

```css
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}

#water {
  grid-column-start: 2;
  grid-column-end: span 2;
  /* grid-column-end: 4 와 같음 */
}
```

```css
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 20% 20% 20% 20% 20%;
}

#water {
  grid-column-start: span 3;
  /* grid-column-start: 3 과 같음 */
  grid-column-end: 6;
}
```

## 참고

https://cssgridgarden.com/#ko (28단계)
