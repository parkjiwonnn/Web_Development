# Token authentication

토큰 기반 인증: 사용자가 자신의 신원을 확인하고, 이에 대한 보상으로 고유한 접근 토큰을 받는 프로토콜

- 토큰이 유효한 동안에는 해당 토큰이 발급된 웹사이트나 앱에 다시 접속할 때마다 자격 증명을 재입력할 필요 없이 접근할 수 있음
- 동일한 웹 페이지, 앱, 또는 해당 토큰으로 보호된 리소스에 반복적으로 접근할 수 있게 해줌
- 사용자는 토큰이 유효한 동안 접근 권한을 유지하며, 사용자가 로그아웃하거나 앱을 종료하면 토큰 무효화
- 토큰 기반 인증은 기존의 비밀번호 기반 또는 서버 기반 인증 방식과 다름
- 토큰은 추가적인 보안 계층을 제공하며, 관리자는 각 작업과 거래에 대한 세부적인 제어 권한을 가질 수 있음

## A History of Authentication Tokens

인증(Authentication)과 권한 부여(Authorization)는 서로 다른 개념

인증 토큰이 등장하기 전에는 비밀번호와 서버를 사용하여 적합한 사람이 적절한 시점에 적합한 리소스에 접근할 수 있도록 전통적인 방식으로 보안을 유지했음

(ex) 비밀번호  
User generation: 사용자가 문자, 숫자, 특수 문자를 조합하여 비밀번호를 생성
Memory: 사용자는 이 고유한 조합을 기억  
Repetition: 사용자가 접근할 때마다 비밀번호를 입력

- 비밀번호를 기억하기 위해 적어두거나 같은 비밀번호를 여러 곳에 반복하여 사용하면 도난이 발생하기 쉬움
- 비밀번호 기반 인증은 서버 인증을 요구함
- 사용자가 로그인할 때마다 컴퓨터가 해당 거래를 기록하며, 서버의 메모리 사용량이 증가함

**토큰 인증**

토큰 인증에서는 별도의 서비스가 서버 요청을 확인함  
확인이 완료되면 서버는 토큰을 발급하고 요청에 응답

- 여전히 사용자가 기억해야 할 비밀번호가 하나 있을 수 있지만, 토큰은 훨씬 도난당하기 어려운 또 다른 접근 방법을 제공함
- 세션 기록이 서버에 저장되지 않아 서버 메모리의 부담이 없음

## 3 Authentication Token Types

모든 인증 토큰은 접근을 허용하지만, 각 유형마다 작동 방식에 약간의 차이가 있음

- 연결형(Connected): 키, 디스크, 드라이브와 같은 물리적 장치가 시스템에 연결되어 접근 권한을 부여함
  - (ex) USB 장치나 스마트카드를 사용해 시스템에 로그인한 경험
- 비접촉형(Contactless): 장치가 서버와 통신할 수 있을 만큼 가까이 있지만, 직접 연결되지는 않음
  - (ex) Microsoft 'magic ring'
- 비연결형(Disconnected): 장치가 다른 장치에 물리적으로 접촉하지 않더라도 멀리 떨어진 서버와 통신할 수 있음
  - (ex) 휴대폰을 사용하여 이중 인증 절차 완료

이 세 가지 방법 모두에서 사용자는 인증 과정을 시작하기 위해 무언가를 해야 함(비밀번호를 입력하거나 질문에 답하는 것 등)  
하지만 이러한 초기 단계들을 완벽하게 수행해도, 접근 토큰 없이는 접근할 수 없음

## Token Authentication in 4 Easy Steps

토큰 기반 인증 시스템을 사용하면 방문자는 자격 증명을 한 번만 확인받음  
그 후 일정 기간 동안 액세스할 수 있는 토큰을 발급받게 됨

- 요청(Request): 사용자가 서버 또는 보호된 리소스에 대한 접근을 요청함
  - 비밀번호를 입력하는 로그인일 수도 있고, 사용자가 설정한 다른 방식일 수도 있음
- 검증(Verification): 서버는 사용자가 접근 권한이 있는지 확인
  - 사용자 이름과 비밀번호를 대조하는 방식이거나, 다른 검증 절차일 수 있음
- 토큰(Token): 서버는 인증 장치(반지, 키, 휴대폰 등)와 통신하여 검증 후 토큰을 발급해 사용자에게 전달
- 저장(Storage): 토큰은 사용자가 작업을 진행하는 동안 브라우저 내에 저장됨

사용자가 서버의 다른 영역에 접근하려고 할 때, 토큰이 서버와 다시 통신하여 접근 허가 여부가 결정됨  
관리자는 토큰의 사용 제한을 설정할 수 있음  
사용자가 로그아웃하면 즉시 삭제되는 일회용 토큰을 허용하거나, 특정 시간이 지나면 자동 삭제되도록 설정할 수도 있음

## 참고

https://www.okta.com/identity-101/what-is-token-based-authentication/