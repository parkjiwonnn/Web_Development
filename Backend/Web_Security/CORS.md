# CORS

## What is CORS?

(ex) localhost:8000에서 웹사이트를 실행하고 있고, JavaScript 코드가 로드되면서 localhost:9000에서 실행 중인 서버로 요청을 보냄 -> CORS 오류 발생

라우저가 동일 출처 정책(Same-Origin Policy)을 따르며, 하나의 출처에서 로드된 문서나 스크립트가 다른 출처의 리소스와 상호작용하는 방식을 제한하기 때문

- 동일한 출처에 있는 서버로의 요청은 브라우저에서 허용됨
- 다른 출처로의 요청(크로스-오리진 요청)은 기본적으로 브라우저에서 차단되며, 이때 CORS 오류가 발생

CORS: Cross-Origin Resource Sharing(교차 출처 리소스 공유)의 약자로, 서버가 HTTP 헤더를 통해 브라우저에 다른 출처의 리소스와 상호작용을 허용할지를 알릴 수 있는 메커니즘

CORS 메커니즘은 브라우저와 서버 간의 안전한 교차 출처 요청 및 데이터 전송을 지원함  
현대 브라우저는 XMLHttpRequest나 Fetch 같은 API에서 CORS를 사용하여 교차 출처 HTTP 요청의 위험을 완화함

## How does it work?

브라우저가 크로스-오리진 요청을 보낼 때, 요청 메시지에 Origin 헤더를 추가함  
서버는 응답 메시지에 Access-Control-Allow-Origin 헤더를 추가하여 응답함  
=> 이때, 응답 헤더의 값이 요청의 Origin 헤더 값과 일치하면 문제가 없지만, 일치하지 않을 경우 브라우저는 응답 데이터를 클라이언트와 공유하지 않으며 CORS 오류가 발생

GET, POST, HEAD 메서드를 사용하는 요청이 아닌 경우나, 비표준 헤더를 포함한 요청은 사전 요청(Pre-flight Request)이 필요함  
이런 요청이 발생하면 브라우저는 OPTIONS HTTP 메서드를 사용하여 사전 요청을 보내고, 서버는 Access-Control-Allow-Origin 및 Access-Control-Allow-Methods 헤더로 응답함  
=> 이 두 헤더의 값이 요청의 Origin 및 메서드와 일치하면 실제 요청이 실행됨

크로스-오리진 요청은 서버 데이터에 영향을 미칠 가능성이 있기 때문에 사전 요청을 통해 미리 확인하는 과정을 거침  
Q. POST 메서드도 서버 데이터를 변경할 수 있는데 왜 사전 요청이 필요하지 않을까?  
A. CORS가 등장하기 전부터 브라우저가 표준 헤더를 사용하는 크로스-오리진 POST 요청을 이미 허용해왔기 때문

CORS는 이전 방식의 요청을 변경하지 않으려 했음  
대신, 예상치 못한 새로운 종류의 요청으로부터 서버를 보호하는 데 초점을 맞춤

## How to fix CORS errors?

localhost:8000에서 실행 중인 클라이언트 앱이 localhost:9000에서 실행 중인 서버로 요청을 보낼 때, CORS가 제대로 설정되지 않았다면 요청이 실패하고 브라우저 콘솔에 다음과 같은 오류가 표시됨

```
Access to fetch at http://localhost:9000/api/endpoint' from origin
'http://localhost:8000' has been blocked by CORS policy.
```

개발자 도구의 네트워크 탭을 열어 확인해야 할 것

- Access-Control-Allow-Origin 응답 헤더가 존재하는지, 그리고 요청의 Origin 헤더 값과 일치하는지 확인
- 만약 사전 요청(Preflight Request)이라면, 응답에 Access-Control-Allow-Methods 헤더가 포함되어 있고, 실제 요청에서 사용되는 HTTP 메서드 값이 포함되어 있는지 확인

=> 응답 헤더에 누락된 값이 있거나 잘못된 값을 확인한 후에는 서버를 업데이트하여 적절한 헤더를 반환하도록 수정

```javascript
// ExpressJS에서는 cors 미들웨어를 사용하여 쉽게 설정 가능
const cors = require("cors");
app.use(cors());
```

CORS 오류 디버깅 시 중요한 점: CORS 오류는 Postman이나 curl 같은 도구를 사용할 때는 발생하지 않음, 브라우저에서 CORS 오류가 발생하더라도 동일한 요청이 이러한 도구에서는 정상적으로 동작할 수 있음

- 이러한 도구는 크로스-오리진 요청을 하지 않음, 네트워크 요청을 최상위 레벨에서 직접 보냄(브라우저의 새 탭에서 URL을 여는 것과 비슷한 방식)
- CORS는 서버 측에서 설정되지만, 이를 따를지는 클라이언트의 결정에 달려 있음
- 대부분의 브라우저는 보안상의 이유로 이를 강제하지만, 개발자 도구(Postman, curl 등)는 이를 신경 쓰지 않음

## 참고

https://rbika.com/blog/understanding-cors
