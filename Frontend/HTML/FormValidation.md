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

```html
<form
  name="myForm"
  action="/action_page.php"
  onsubmit="return validateForm()"
  method="post">
  Name: <input type="text" name="fname" />
  <input type="submit" value="Submit" />
</form>
```

- `required`: 폼 필드가 제출되기 전에 반드시 채워져야 하는지 여부를 지정
- `minlength`, `maxlength`: 텍스트 데이터(문자열)의 최소 및 최대 길이를 지정
- `min`, `max`: 숫자 입력 유형의 최소 및 최대 값을 지정
- `type`: 데이터가 숫자, 이메일 주소 또는 다른 특정 유형이어야 하는지를 지정
- `pattern`: 입력된 데이터가 따라야 하는 패턴을 정의하는 정규 표현식을 지정

폼 필드에 입력된 데이터가 위 속성에서 지정한 모든 규칙을 따르면 유효한 것으로 간주, 그렇지 않으면 무효로 간주

유효한 요소일 경우:

- 요소는 :valid CSS 의사 클래스에 일치하여 유효한 요소에 특정 스타일을 적용할 수 있음
- 사용자가 데이터를 전송하려고 하면, 다른 방해 요소(JavaScript 등)가 없다면 브라우저가 폼을 제출

무효한 요소일 경우:

- 요소는 :invalid CSS 의사 클래스 및 때에 따라 오류에 따른 다른 UI 의사 클래스(:out-of-range 등)에 일치하여 무효한 요소에 특정 스타일을 적용할 수 있음
- 사용자가 데이터를 전송하려고 하면 브라우저가 폼 제출을 차단하고 오류 메시지를 표시

## JavaScript validation

```javascript
function validateForm() {
  let x = document.forms["myForm"]["fname"].value;
  if (x == "") {
    alert("Name must be filled out");
    return false;
  }
}
```

폼이 제출될 때 validateForm() 함수가 호출되어 입력 필드가 비어 있는지 확인하고, 비어 있을 경우 경고 메시지를 띄운 뒤 폼 제출을 막음

### Constraint Validation API

```html
<form>
  <label for="mail">
    I would like you to provide me with an email address:
  </label>
  <input type="email" id="mail" name="mail" />
  <button>Submit</button>
</form>
```

```javascript
const email = document.getElementById("mail");

email.addEventListener("input", (event) => {
  if (email.validity.typeMismatch) {
    email.setCustomValidity("I am expecting an email address!");
  } else {
    email.setCustomValidity("");
  }
});
```

1. 유효성 검사
   `validity.typeMismatch` 속성을 사용하여 입력된 이메일 주소가 유효한 형식을 따르는지 확인  
   만약 `typeMismatch`가 true를 반환하면, 입력된 값이 이메일 주소의 올바른 형식이 아님

2. 사용자 정의 오류 메세지 설정
   `typeMismatch`가 true일 경우, `setCustomValidity()` 메서드를 사용하여 사용자 정의 오류 메시지를 설정  
   이로 인해 입력 필드가 유효하지 않게 되며, 폼 제출을 시도할 때 제출이 실패하고, 설정한 오류 메시지가 표시됨

3. 빈 문자열로 오류 메세지 초기화
   반대로, `typeMismatch`가 false일 경우 `setCustomValidity()`에 빈 문자열을 전달  
   이렇게 하면 필드가 유효하다고 간주되어, 폼을 제출할 수 있음

## 참고

https://developer.mozilla.org/en-US/docs/Learn/Forms/Form_validation

https://www.w3schools.com/js/js_validation.asp
