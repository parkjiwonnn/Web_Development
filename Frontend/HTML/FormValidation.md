# Form Validation

client-side form validation: 서버에 데이터를 제출하기 전에 모든 필수 입력란이 올바른 형식으로 채워졌는지 확인하는 것

- 브라우저에서 수행하는 유효성 검사는 client-side validation, 서버에서 수행하는 유효성 검사는 server-side validation
- 제출된 데이터가 각 입력란의 요구 사항을 충족하도록 도움
- 클라이언트 측에서 잘못된 데이터를 잡아주면 사용자가 즉시 수정할 수 있음
- 만약 서버로 잘못된 데이터가 전달되어 거부되면, 서버와 클라이언트 간의 왕복 시간 때문에 사용자에게 데이터 수정 요청이 전달되는 데 눈에 띄는 지연이 발생하게 됨
- 정보가 올바른 형식일 경우 애플리케이션은 데이터를 서버에 제출하고 데이터베이스에 저장할 수 있게 허용

- 사용자의 데이터가 잘못된 형식으로 저장되거나 틀리거나 누락되면 애플리케이션이 제대로 작동하지 않을 수 있음
- 사용자의 데이터 보호를 위해 보안성이 높은 비밀번호를 요구함으로써 계정 정보를 쉽게 보호가능
- 보호되지 않은 양식은 악의적인 사용자가 여러 방식으로 악용하여 애플리케이션에 피해를 줄 수 있음

1. Built-in form validation
   HTML 폼 유효성 검사 기능을 사용하는 방법, JavaScript가 거의 필요하지 않으며 성능이 JavaScript에 비해 우수하지만, 커스터마이징이 JavaScript만큼 자유롭지 않음

2. JavaScript validation
   JavaScript로 직접 코딩하여 수행하는 방식, 완전한 커스터마이징이 가능하지만, 모든 코드를 작성하거나 라이브러리를 사용해야 함

## Built-in form validation

## JavaScript validation

## 참고

https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation

https://www.w3schools.com/js/js_validation.asp
