# HTTP

HTTP(The Hypertext Transfer Protocol)는 월드 와이드 웹 기반이며 하이퍼텍스트 링크를 사용하여 웹 페이지를 로드하는 데 사용됨  
HTTP는 네트워크 장치 간에 정보를 전송하도록 설계된 **애플리케이션 계층** 프로토콜이며, 네트워크 **프로토콜** 스택의 최상위 계층에서 실행됨  
HTTP를 통한 일반적인 흐름에는 클라이언트 시스템에서 서버에 요청한 다음 서버에서 응답 메세지를 보내는 작업이 포함됨

## HTTP request

HTTP 요청은 웹 브라우저와 같은 인터넷 통신 플랫폼이 웹사이트를 로드하는 데 필요한 정보를 요청하는 방식  
인터넷을 통해 요청할 때마다 다양한 유형의 정보를 전달하는 일련의 인코딩된 데이터가 함께 제공됨

- HTTP version type
- a URL
- an HTTP method
- HTTP request headers
- Optional HTTP body

### HTTP method

HTTP 메서드는 HTTP 요청이 쿼리된 서버에서 기대하는 작업을 나타냄  
가장 일반적인 두 가지 HTTP 메서드는 'GET', 'POST'  
'GET' 요청은 응답으로 정보를 기대하는 반면, 'POST' 요청은 일반적으로 클라이언트가 웹 서버에 정보를 제출하고 있음을 나타냄

### HTTP request headers

HTTP 헤더에는 키값 쌍에 저장된 텍스트 정보가 포함되어 있으며 헤더는 모든 HTTP 요청에 포함됨  
헤더는 클라이언트가 사용하는 브라우저 및 요청되는 데이터와 같은 핵심 정보를 전달함

### HTTP request body

요청의 본문은 요청에서 전송되는 정보의 본문을 포함하는 부분  
HTTP 요청의 본문에는 웹 서버에 제출되는 모든 정보가 포함됨

## HTTP response

HTTP 응답은 웹 클라이언트에서 HTTP 요청에 대한 응답으로 인터넷 서버로부터 수신하는 응답  
HTTP 요청에서 요청된 내용을 기반으로 중요한 정보를 전달

- an HTTP status code
- HTTP response headers
- optional HTTP body

### HTTP status code

HTTP 상태 코드는 HTTP 요청이 성공적으로 완료되었는지 여부를 나타내는 데 가장 자주 사용되는 3자리 코드  
XX는 00에서 99사이의 다른 숫자들을 나타냄

- 1XX 정보 제공
- 2XX 성공
- 3XX 리디렉션
- 4XX 클라이언트 오류
- 5XX 서버 오류

### HTTP response headers

HTTP 응답에는 응답 본문에서 전송되는 데이터의 언어 및 형식과 같은 중요한 정보를 전달하는 헤더가 함께 제공됨

### HTTP response body

'GET'요청에 대한 성공적인 HTTP 응답에는 일반적으로 요청된 정보가 포함된 본문이 있음  
대부분의 웹 요청의 경우 이는 웹 브라우저에서 웹 페이지로 변환되는 HTML 데이터

## DDoS attack

DoS 또는 DDoS 공격의 컨텍스트에서 대량의 HTTP 요청을 사용하여 대상 디바이스에 대한 공격을 개시할 수 있으며 이는 애플리케이션 계층 공격 또는 계층 7 공격의 일부로 간주됨

## 참고

https://www.cloudflare.com/learning/ddos/glossary/hypertext-transfer-protocol-http/
