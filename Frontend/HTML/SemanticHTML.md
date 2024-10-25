# Semantic HTML

Semantic HTML: 웹 페이지의 콘텐츠 의미를 전달하기 위해 HTML 마크업을 사용하는 것

- Semantic HTML 태그를 사용하면 웹 페이지의 구조와 의미를 명확히 할 수 있어 접근성과 SEO에 도움이 됨
- 각 요소의 목적이 명확하기 때문에 코드의 가독성과 유지 관리가 더 쉬워짐

### Header

웹 페이지의 상단 섹션을 표시하는 데 사용  
일반적으로 주요 제목이나 로고, 탐색 링크 및 사이트의 모든 페이지에서 공통적으로 사용되는 다른 요소들이 포함됨

```html
<!-- Non-semantic header -->
<div class="header">
  <h1>My Site</h1>
  <nav>
    <a href="#">Home</a>
    <a href="#">About</a>
    <a href="#">Contact</a>
  </nav>
</div>

<!-- Semantic header -->
<header>
  <h1>My Site</h1>
  <nav>
    <ul>
      <li><a href="#">Home</a></li>
      <li><a href="#">About</a></li>
      <li><a href="#">Contact</a></li>
    </ul>
  </nav>
</header>
```

### Navigation

웹 페이지에서 탐색 링크를 포함하는 섹션을 표시하는 데 사용

```html
<!-- Non-semantic navigation -->
<div class="navigation">
  <a href="#">Home</a>
  <a href="#">About</a>
  <a href="#">Contact</a>
</div>

<!-- Semantic navigation -->
<nav>
  <ul>
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```

### Main

웹 페이지의 주요 콘텐츠 영역을 표시하는 데 사용

```html
<!-- Non-semantic main content -->
<div class="main-content">
  <h2>About Us</h2>
  <p>Welcome to our website. We are a company that specializes in widgets.</p>
</div>

<!-- Semantic main content -->
<main>
  <h2>About Us</h2>
  <p>Welcome to our website. We are a company that specializes in widgets.</p>
</main>
```

### Article

블로그 게시물, 뉴스 기사, 제품 리뷰와 같은 독립적인 콘텐츠를 나타내는 데 사용  
`<article>` 태그 내의 콘텐츠는 독립적이고 의미가 있어야 하며, 제목, 단락, 이미지 및 기타 유형의 콘텐츠를 포함할 수 있음

```html
<!-- Non-semantic article -->
<div class="article">
  <h2>How to Make a Widget</h2>
  <p>Widgets are great. Here's how to make one.</p>
</div>

<!-- Semantic article -->
<article>
  <h2>How to Make a Widget</h2>
  <p>Widgets are great. Here's how to make one.</p>
</article>
```

### Aside

웹 페이지의 주요 콘텐츠와 관련되지만, 그 내용의 핵심적인 부분은 아닌 콘텐츠를 표시하는 데 사용  
보충 정보, 광고, 관련 기사 등과 같은 요소가 포함될 수 있음

```html
<div>
  <article>
    <h2>Article Title</h2>
    <p>Article content goes here</p>
  </article>
  <aside>
    <h3>Related Articles</h3>
    <ul>
      <li><a href="#">Article 1</a></li>
      <li><a href="#">Article 2</a></li>
      <li><a href="#">Article 3</a></li>
    </ul>
  </aside>
</div>
```

### Section

웹 페이지의 주제가 함께 그룹화된 섹션을 표시하는 데 사용  
긴 기사에서의 장이나 섹션, 또는 제품 페이지의 다양한 부분 등을 포함할 수 있음

```html
<section>
  <h2>Section Title</h2>
  <p>Section content goes here</p>
</section>
```

### Footer

웹 페이지의 하단 섹션을 표시하는 데 사용  
저작권 정보, 연락처 세부정보, 소셜 미디어 프로필 링크와 같은 요소들이 포함될 수 있음

```html
<!-- Non-semantic footer -->
<div class="footer">
  <p>&copy; 2021 My Site</p>
</div>

<!-- Semantic footer -->
<footer>
  <p>&copy; 2021 My Site</p>
</footer>
```

### Details and Summary

접을 수 있는 콘텐츠 섹션을 표시하는 데 사용  
`<summary>`태그는 해당 섹션의 제목을 나타내며, 사용자가 클릭하면 섹션의 내용을 표시하거나 숨길 수 있음  
`<details>`태그는 실제 콘텐츠를 포함하는 부분으로, 이 두 태그를 함께 사용하여 인터랙티브한 요소를 생성할 수 있음

```html
<details>
  <summary>Click to expand</summary>
  <p>Content goes here</p>
</details>
```

### Figure and Figcaption

웹 페이지의 주요 콘텐츠에서 참조되는 독립적인 콘텐츠 조각을 표시하는 데 사용  
`<figure>`태그는 이미지, 그래프, 다이어그램 등의 콘텐츠 자체를 마크업하는 데 사용  
`<figcaption>`태그는 해당 콘텐츠에 대한 설명이나 캡션을 표시하는 데 사용

```html
<figure>
  <img src="image.jpg" alt="Image description" />
  <figcaption>Image caption</figcaption>
</figure>
```

### Mark

어떤 이유로 강조된 텍스트를 표시하는 데 사용

```html
<p>Here is some <mark>highlighted</mark> text.</p>
```

### Time

날짜나 시간을 표시하는 데 사용

```html
<p>
  The event will take place on
  <time datetime="2021-01-01">January 1st, 2021</time>.
</p>
```

### Progress

진행 상태 표시줄을 표시하는 데 사용

```html
<progress value="50" max="100"></progress>
```

### <div>, <span>

`<div>`와 `<span>` 태그는 시맨틱 태그가 아님  
이 태그들은 일반적인 콘텐츠 영역을 표시하는 데 사용되며, 특정한 의미를 전달하지 않음  
콘텐츠의 구조를 명확하게 표현하기 위한 다른 시맨틱 태그가 없는 경우에만 사용하는 것이 좋음

## 참고

https://cs.fyi/guide/writing-semantic-html
