# SPA

- Single Page Application
- 하나의 페이지 요청으로 전체 웹앱을 사용하는 방식
- 유저는 웹페이지를 사용하며 모바일 앱 같은 경험을 느낌
- MPA
  - Multi Page Application
  - 서버에 미리 여러 페이지를 두고, 유저가 네비게이션 시 요청에 적합한 페이지를 전달
  - 미리 서버에서 전체 페이지를 빌드해 브라우저로 전송됨
  - 서버에 라우팅을 처리하는 기능이 있고, 서버에서 여러 페이지를 관리함
  - 페이지 요청마다 모든 리소스를 다시 받아오므로, 페이지 간 데이터를 재활용하기 힘듦

## SPA의 특징

- Client-side routing 기술을 활용, 페이지 진입 시 리로드없이 라우팅함
- AJAX 기술을 활용, 페이지 이동 시 서버에 데이터만 요청하여 자바스크립트로 페이지를 만듦
- MPA와 다르게, 여러 페이지를 하나의 앱의 구성요소로 보고 여러 페이지 간의 스타일, 컴포넌트를 재활용하는 방향으로 구현
- 자바스크립트만을 활용해 전체 페이지를 만들기에, 첫 요청 시 빈 페이지를 받게 됨

## SPA의 장점

- 매번 페이지 요청을 할 필요가 없어 네트워크 요청이 줄어듦
- 웹 사이트를 개별 페이지보다는 하나의 앱으로 보는 설계로 고도의 소프트웨어 설계(상태관리, 라우팅, 컴포넌트 재사용, 훅을 통한 로직 재사용)와 패턴을 적용할 수 있음

## SPA의 단점

- MPA방식 보다는 SEO(Search Engine Optimization)에 불리함
- 여러 페이지를 전송받는 것 보다, 하나의 거대한 자바스크립트 앱을 전송받아야 하므로 코드가 많아질수록 로드 속도가 느려짐

## SPA에서의 라우팅

- 리액트는 SPA로 html이 하나만 있는 단일 페이지이기 때문에 웹사이트를 구성하는 웹페이지가 여러 개라면 페이지마다 경로 설정 필요
- 라우팅 : 경로마다 해당 페이지를 브라우저 화면에 출력하는 것
- a 태그를 사용하면 페이지 전체가 새로 로딩 되는데 화면 깜빡임이 필수적으로 발생하고 이는 사용자 경험을 떨어뜨리는 큰 요인이기 때문에 라우팅을 통해 부드러운 화면 전환을 꾀할 수 있음
- 리액트는 UI를 그리는 라이브러리이기 때문에 Routing 기능이 내장되어 있지 않음
- react-router, reach-router 등의 라이브러리를 활용하면, 라우팅 관련 기능을 쉽게 사용할 수 있음

# react-router

- 사용자가 입력한 주소를 감지하는 역할을 하며, 여러 환경에서 동작할 수 있도록 여러 종류의 라우터 컴포넌트를 제공함

```jsx
import { 라우터 컴포넌트 명 } from 'react-router-dom';
```

- React 컴포넌트를 특정 path와 연결하면, 해당하는 path로 진입 시 컴포넌트를 랜더링하게 함
- query, path variable 등 URL parameter를 얻어 활용함

## react-router 컴포넌트

- BrowserRouter
  - HTML5의 History API를 사용하여, UI와 URL의 싱크를 맞추는 역할
  - 모든 URL에 대해 동작하게 하기 위해서는 서버 설정 필요
  - 모든 path 앞의 basename을 지정할 수 있음 (ex) basename=”/ko”
  - forceRefresh로, 페이지 이동 시 리프레시할 것인지 지정할 수 있음
- Switch
  - 여러 Route 중 매치되는 Route 위에서부터 하나 선택하여 랜더링함
  - 매칭되는 Route가 없으면 아무것도 보여주지 않음
  - fallback용으로 404 Not Found Page를 추가함
  - path=”/”의 경우 모든 path에 매칭되므로 exact 키워드를 추가하거나 가장 아래로 내림
- Route
  - path와 컴포넌트를 매칭함
  - 매칭되는 컴포넌트는 children으로 넣어주거나 component prop으로 넘김
  - exact 키워드로 정확하게 매칭되는 path를 설정함
  - Route로 렌더링 되는 최상위 컴포넌트는 match, location, history를 prop으로 받음
  - render prop으로, 매칭되었을 때 실제 어떤 컴포넌트를 렌더링할지 통제함
- BrowserRouter
  - 전체를 감싸줌
- Routes
  - url에 따라 변동되는 부분을 감싸줌
  - Routes 외부는 모든 페이지에 공통으로 노출됨을 의미함(Header, Footer)
- Route
  - 사용자의 브라우저 주소 경로에 따라 해당되는 컴포넌트를 보여줌
  - Route 컴포넌트는 Routes 컴포넌트 내부에서 사용되어야 함
  - <Route path="주소규칙" element={<보여줄 컴포넌트 명/>} />

```jsx
const Router = () => {
  return (
    <BrowserRouter>
      <Header />
      <Routes>
        <Route path="/login" element={<Login />} />
        <Route path="/main" element={<Main />} />
      </Routes>
    </BrowserRouter>
  );
};
```
