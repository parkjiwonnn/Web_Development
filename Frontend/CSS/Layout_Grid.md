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

#### 1. grid-column-start 와 grid-column-end를 같이 사용할때, 시작 값보다 마지막 값이 더 크지 않아도 됨

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

#### 2. 그리드 왼쪽의 기준이 아닌 오른쪽으로 기준을 하고싶다면, grid-column-start 와 grid-column-end를 음수로 설정

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

#### 3. 그리드 선의 시작과 끝 위치를 기준으로 그리드 항목을 정의하는 대신, span을 이용하여 열(column)의 넓이를 지정 가능

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

## grid-row

그리드 요소의 행(row) 위치 지정  
`<grid-row-start> / <grid-row-end>`

- flexbox와 별개로 CSS 그리드를 설정하면 컬럼과 행 두가지 측면에서 쉽게 그리드 항목을 배치 가능
- grid-row-start는 grid-column-start 수직선을 제외하곤 동일하게 작동

## grid-area

`<grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>`

## order

그리드 요소의 순서 지정  
`<integer>`

- 그리드 요소들이 grid-area, grid-column, grid-row, 기타 등을 사용하지 않고, 표시될 경우 소스코드에 기입된 순서대로 표기됨
- table 레이아웃에 비해 grid 시스템의 장점인 order 속성을 이용하면 재정의 가능
- 기본적으로, 그리드의 모든 요소들은 order의 값이 0이지만, z-index와 같이 양수와 음수의 값 모두 설정 가능

## grid-template

그리드 요소의 행(row)과 열(column) 크기와 명칭 지정
`<grid-template-rows> / <grid-template-columns>`

### grid-template-columns

그리드의 열(column) 크기와 명칭 지정  
`<length> <percentage> <flex> max-content min-content minmax(min,max)`

- 백분율 같은 값뿐만 아니라, 픽셀 및 em과 같은 길이 단위도 허용
- 서로 다른 단위를 함께 사용 가능

(ex)  
grid-template-columns: 20% 20% 20% 20% 20%;  
grid-template-rows: 20% 20% 20% 20% 20%;  
각 속성에는 5개의 열을 만드는 5개 값이 있으며, 각 열은 정원의 20% 너비 설정

### repeat

(ex)  
grid-template-columns: 20% 20% 20% 20% 20%;  
-> grid-template-columns: repeat(5, 20%);

### fractional fr

#### 1. 각 fr 단위들은 사용가능한 공간을 하나로 공유하여 할당

```css
#garden {
  display: grid;
  grid-template-columns: 1fr 5fr;
  grid-template-rows: 20% 20% 20% 20% 20%;
}
```

두개의 element들을 1fr과 5fr로 설정 -> 공간이 6개의 동일한 크기로 공유됨  
첫번째 element는 사용가능한 공간의 1/6 크기, 두번째 element는 5/6 크기를 차지

#### 2. 열(column)을 pixel, percentage, 혹은 em으로 설정시, fr로 설정된 다른 열(column)의 남은 공간으로 나뉘어짐

```css
#garden {
  display: grid;
  grid-template-columns: 50px 1fr 1fr 1fr 50px
  grid-template-rows: 20% 20% 20% 20% 20%;
}
```

### grid-template-rows

그리드의 행(row) 크기와 명칭 지정  
`<length> <percentage> <flex> max-content min-content minmax(min,max)`

```css
/* 상단의 50px를 제외하고 물 주기, 물이 5번째 행(row)만 설정되어있으므로, 5개의 행(row)을 생성해야함 */
#garden {
  display: grid;
  grid-template-columns: 20% 20% 20% 20% 20%;
  grid-template-rows: 50px 0 0 0 1fr;
}

#water {
  grid-column: 1 / 6;
  grid-row: 5 / 6;
}
```

## 참고

https://cssgridgarden.com/#ko (28단계 완료)
