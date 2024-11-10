# Responsive Web Design

반응형 디자인: 다양한 기기들의 화면 크기와 창 크기에 맞춰 웹 콘텐츠를 조정하는 웹 디자인 접근 방식

## Responsive Web Design vs Adaptive Design

Responsive Web Design

- 단일 페이지 버전의 렌더링을 조정
- 기기에 상관없이 사용자가 동일한 기본 파일에 접근하고, css 코드가 화면 크기에 맞춰 레이아웃을 조정하여 다르게 렌더링

Adaptive Design

- 같은 페이지의 여러 다른 버전을 제공
- 스크립트가 화면 크기를 확인한 후 해당 기기에 맞춘 템플릿에 접근

## Are WordPress Sites Responsive?

- WordPress 사이트가 반응형인지 여부는 사용하는 테마에 따라 달라짐
- WordPress 테마는 정적 웹사이트의 템플릿과 같은 역할을 하며, 콘텐츠의 디자인과 레이아웃을 제어함
- 기본 WordPress 테마(ex: Twenty Twenty)를 사용하면 디자인이 반응형이지만, 단일 열 디자인이기 때문에 화면마다 차이를 쉽게 알아차리기 어려울 수 있음
- 다른 WordPress 테마를 사용할 경우, 다양한 기기에서 어떻게 보이는지 비교하거나 Chrome 개발자 도구를 이용해 반응형인지 테스트할 수 있음

## The Building Blocks of Responsive Web Design

반응형 웹사이트 디자인의 구성요소:

- CSS and HTML
- Media Queries
- Fluid Layouts
- Flexbox Layout
- Responsive Images
- Speed

### Media Queries

- 미디어 쿼리: CSS3의 중요한 기능으로, 화면 크기나 해상도와 같은 다양한 조건에 맞게 콘텐츠를 조정할 수 있게 해줌

- 미디어 쿼리는 일부 프로그래밍 언어에서 "if 문"처럼 작동함  
  화면의 뷰포트가 충분히 넓거나 너무 넓은지 확인한 후, 적절한 코드를 실행

(ex) 화면이 최소 780픽셀 이상일 경우, "full-width-img" 클래스의 이미지는 화면의 90%를 차지하고, 너비가 같은 여백을 사용하여 자동으로 중앙에 배치됨

```css
@media screen and (min-width: 780px) {
  .full-width-img {
    margin: auto;
    width: 90%;
  }
}
```

### Fluid Layouts

- 유동적 레이아웃은 고정된 값 대신 뷰포트 너비의 백분율과 같은 동적인 값을 사용함
- 화면 크기에 따라 다양한 컨테이너 요소들의 크기가 동적으로 증가하거나 감소하게 만들어, 다양한 화면 크기에서 적절한 레이아웃을 유지할 수 있도록 해줌

```css
.container {
  width: 80%; /* 화면 너비의 80% */
}
```

### Flexbox Layout

- Flexbox: 콘텐츠 크기가 알려지지 않은 상황에서도 여러 요소를 효율적으로 배치할 수 있도록 설계된 CSS 모듈
- Flexbox 컨테이너는 항목들을 확장하여 사용 가능한 공간을 채우거나, 오버플로우를 방지하기 위해 항목을 축소시킴
- Flexbox 컨테이너에는 justify-content와 같은 고유한 속성이 있어, 일반 HTML 요소로는 조정할 수 없는 특성들이 있음

### Responsive Images

- 반응형 이미지의 가장 기본적인 구현은 유동적 레이아웃과 같은 개념을 따르며, 동적인 단위를 사용하여 너비나 높이를 제어

```css
img {
  width: 100%;
}
```

- 이때 % 단위는 뷰포트의 너비나 높이에 대한 비율을 나타내며, 이미지가 화면 크기에 맞게 비율을 유지하도록 만듦
- 모든 사용자가 모바일에서도 전체 크기의 이미지를 다운로드해야 한다는 문제점이 있음
- 다양한 장치에 맞게 크기가 조정된 이미지를 제공하려면, srcset 속성을 사용해야 함
- 이를 통해 여러 크기의 이미지를 지정하여 사용자가 적절한 크기의 이미지를 선택할 수 있도록 함

```html
<img
  srcset="large-img.jpg 1024w, middle-img.jpg 640w, small-img.jpg 320w"
  src="small.jpg" />
```

- WordPress는 게시물이나 페이지에 포함된 이미지에 대해 이 기능을 자동으로 사용함
- 이를 통해 웹사이트가 다양한 장치에서 더 효율적으로 이미지를 제공할 수 있음

### Speed

- 웹사이트의 반응형 디자인을 만들 때, 로딩 속도는 최우선 고려사항이 되어야 함
- 페이지가 2초 만에 로드되면 평균적으로 9%의 이탈률을 보이지만, 페이지가 5초가 걸리면 이탈률은 38%로 급증
- 반응형 디자인을 구현할 때, 페이지의 첫 번째 렌더링을 지연시키거나 차단하지 않도록 해야 함
- 불필요한 렌더링 지연을 최소화하는 것이 중요

- 페이지를 더 빠르게 만드는 방법: 이미지 최적화, 캐시 구현, 파일 축소(minification), 더 효율적인 CSS 레이아웃 사용, 렌더링을 차단하는 JavaScript 피하기, 중요한 렌더링 경로 개선 등

## Common Responsive Breakpoints

- 미디어 쿼리를 사용할 때, "반응형 브레이크포인트" 또는 화면 크기 브레이크포인트를 결정해야 함
- 브레이크포인트: 새로운 CSS 스타일을 적용하기 위해 미디어 쿼리를 사용하는 화면의 너비를 의미
- 브레이크포인트는 다양한 화면 크기에서 웹사이트가 적절하게 표시되도록 하기 위해 설정
- 모바일, 태블릿, 데스크탑 화면에 맞게 디자인을 변경하려면 각 화면 크기에서 브레이크포인트를 설정하고, 해당 화면 크기에 맞는 스타일을 적용하는 미디어 쿼리를 작성해야 함

```css
/* 모바일 (최대 600px) */
@media (max-width: 600px) {
  /* 모바일 스타일 */
}

/* 태블릿 (최소 601px, 최대 1024px) */
@media (min-width: 601px) and (max-width: 1024px) {
  /* 태블릿 스타일 */
}

/* 데스크탑 (최소 1025px) */
@media (min-width: 1025px) {
  /* 데스크탑 스타일 */
}
```

### Common screen sizes

- Mobile: 360 x 640
- Mobile: 375 x 667
- Mobile: 360 x 720
- iPhone X: 375 x 812
- Pixel 2: 411 x 731
- Tablet: 768 x 1024
- Laptop: 1366 x 768
- High-res laptop or desktop: 1920 x 1080

- 모바일 우선 접근 방식을 채택하여 디자인할 경우, 단일 열과 작은 글꼴 크기를 기준으로 시작하면, 모바일 브레이크포인트를 포함할 필요가 없음
- 모바일 우선 방식은 기본적으로 모든 화면 크기에서 잘 작동하는 디자인을 제공하므로, 특정 모델에 최적화하려는 경우가 아니라면 모바일 브레이크포인트는 필요하지 않음
- 기본 반응형 디자인을 만들 때, 태블릿용과 랩탑 및 데스크탑용 두 개의 브레이크포인트만으로 충분히 설계할 수 있음

### Bootstrap’s Responsive Breakpoints

- Bootstrap: 가장 먼저 등장한 인기 있는 반응형 프레임워크 중 하나
- 정적인 웹 디자인을 벗어나 모바일 우선 디자인을 산업 표준으로 자리잡게 하는 데 중요한 역할을 함
- 그 결과, 많은 디자이너들이 여전히 부트스트랩의 화면 너비 브레이크포인트를 따름
- 이들은 미디어 쿼리를 사용하여 다음과 같은 화면 크기에서 디자인을 최적화함
  - landscape phones (모바일): 576px
  - tablets: 768px
  - laptops: 992px
  - extra large desktop screens: 1200px

## 참고

https://kinsta.com/blog/responsive-web-design/
