## MongoDB

- NoSQL 데이터베이스, JSON과 유사한 형식의 데이터를 저장하는 데 사용됨
- Database > Collection > Document
  - Database : 하나 이상의 collection을 가질 수 있는 저장소, SQL에서의 database와 유사
  - Collection : 하나 이상의 Document가 저장되는 공간, SQL에서의 table과 유사, 하지만 collection이 document의 구조를 정의하지 않음
  - Document : MongoDB에 저장되는 자료, SQL에서 row와 유사하지만 구조제약 없이 유연하게 저장 가능, JSON과 유사한 BSON을 사용하여 다양한 자료형을 지원
    - Document > ObjectID
    - 각 document의 유일한 키 값, SQL의 primary key와 유사, 하나씩 증가하는 값이 아닌 document를 생성할 때 자동으로 생성되는 값

## Mongoose

- Node.js 환경에서 MongoDB와 상호 작용하기 위한 객체 모델링 도구

### Mongoose ODM(Object Data Modeling)

- MongoDB의 Collection에 집중하여 관리하도록 도와주는 패키지
- Collection을 모델화하여, 관련 기능들을 쉽게 사용할 수 있도록 도와줌
- 연결관리
  - MongoDB의 기본 Node.js 드라이버는 연결상태 관리 어려움
  - Mongoose를 사용하면 간단하게 데이터베이스와의 연결상태를 관리해줌
- 스키마 관리
  - 스키마를 정의하지 않고 데이터를 사용할 수 있는 것은 NoSQL의 장점
  - 하지만 데이터 형식을 미리 정의해야 코드 작성과 프로젝트 관리에 유용함
  - Mongoose는 Code-Level에서 스키마를 정의하고 관리할 수 있게 해 줌
- Populate
  - MongoDB는 기본적으로 Join을 제공하지 않음
  - Join과 유사한 기능을 사용하기 위해선 aggregate라는 복잡한 쿼리를 해야함
  - Mongoose는 populate를 사용하여 간단하게 구현가능
- Mongoose ODM 사용 순서
  1. 스키마 정의
  2. 모델 만들기
  3. 데이터베이스 연결
  4. 모델 사용
