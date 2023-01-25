# Core JavaScript

---

### 01. 데이터 타입

1. 데이터 타입의 종류

   - primitive type(기본형)

     - `number`
     - `string`
     - `boolean`
     - `null`
     - `undefined`
     - `Symbol`
       <br>

   - reference type(참조형)

     - object
     - Array
     - Function
     - Date
     - RegExp
     - Map
     - WeakMap
     - Set
     - WeakSet
     - etc
       <br>

     ```
     Q. 어떤 기준으로 기본형과 참조형을 구분하는가?
     A. 기본형은 값이 담긴 주솟값을 바로 복제, 참조형은 값이 담긴 주솟값들로 이루어진 묶음을 가리키는 주솟값을 복제
     ```

   - 기본형은 불변성(immutability)를 띈다.
     <a href="https://narup.tistory.com/268" target="blank">불변성</a>에 대해 알아보자.

   <br>

1. 데이터 타입에 관한 배경지식

   - 변수(variable), 변할 수 있는 데이터
   - 식별자(identifier), 어떤 데이터를 식별하는데 사용하는 이름, 변수명

   <br>

1. 변수 선언과 데이터 할당

   <br>

1. 기본형 데이터와 참조형 데이터

   - 불변값

     - 변수와 상수를 구분하는 성질은 '변경 가능성'
     - 바꿀 수 있으면 변수, 바꿀 수 없으면 상수
     - 변수와 상수를 구분 짓는 변경 가능성의 대상은 변수 영역 메모리
     - 불변성 여부를 구분할 때의 변경 가능성의 대상은 데이터 영역 메모리

   - 가변값
   - 변수 복사 비교

   <br>

1. 불변 객체

   - 불변 객체를 만드는 간단한 방법
     - 새로운 객체를 만드는 도구(immutable.js, immer.js, ES6의 spread operator, `Object.assign`)
   - 얕은 복사와 깊은 복사
     - 얕은 복사(shallow copy)는 바로 아래의 값만 복사
     - 깊은 복사(deep copy)는 내부의 모든 값들을 하나하나 찾아서 전부 복사
     - 재귀함수(recursive function), `JSON.parse(JSON.stringify(target))`,

   <br>

1. undefined와 null
   - `typeof null`은 `object`, 자바스크립트 자체 버그 - JavaScript에서는 ==(동등연산자, equality operator) 보단 `===`(일치 연산자, identity operator)를 쓰자

---

### 02. 실행 컨텍스트

1. 실행 컨텍스트란?

   - <a href="https://developer.mozilla.org/ko/docs/Glossary/Hoisting" target="blank">호이스팅</a>
   - VariableEnvironment: 현재 컨텍스트 내 식별자 정보, 외부 환경 정보, 선언시점의 LE 스냅샷, 변경 사항 미반영
   - LexicalEnvironment: 초기값 VariableEnvironment, 변경 사항 실시간 반영
   - ThisBinding: this 식별자 대상 객체

1. VariableEnvironment

1. LexicalEnvironment

   - environmentRecord와 호이스팅

     - environmentRecord에는 현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장
     - 순서대로 수집
     - 엔진의 실제 동작 방식 대신에 '자바스크립트 엔진은 식별자들을 최상단으로 끌어올려 놓은 다음 실제 코드를 실행한다'라고 생각해도 문제될 것이 없다. 여기서 호이스팅이라는 개념이 등장
     - 자바스크립트 엔진이 실제로 끌어올리지는 않지만 편의상 끌어올린 것으로 간주하자는 것

     - 함수 선언문과 함수 표현식
       - 선언문은 함수 전체가 호이스팅이 일어남
       - 표현식은 변수명(식별자)만 호이스팅이 일어남
       - '선언한 후에야 호출할 수 있다'라는 편이 훨씬 자연스럽다.

   - 스코프, 스코프 체인, outerEnvironmentReference
     - 스코프란 식별자에 대한 유효범위
     - ES5까지의 자바스크립트는 전역공간을 제외하면 오직 함수에 의해서만 스코프가 생성
     - ES6에서는 블록에 의해서도 스코프 경계가 발생하게 함
     - '식별자의 유효범위'를 안에서부터 바깥으로 차례로 검색해나가는 것을 스코프 체인(scope chain)이라 함
     - 이를 가능케 하는 것이 LE의 두 번째 수집 사료인 outerEnvironmentReference
     - outerEnvironmentReference는 연결리스트 형태
     - 무조건 스코프 체인 상에서 가장 먼저 발견된 식별자에만 접근 가능

1. this
   - this에는 실행 컨텍스트를 활성화하는 당시에 지정된 this가 저장, 함수를 호출하는 방법에 따라 값이 달라지는데, 지정되지 않은 경우 전역 객체가 저장

### 03. this

1. 상황에 따라 달라지는 this
   this는 함수를 호출할 때 결정된다.

   - 전역 공간에서의 this

     - 전역 공간에서 this는 전역 객체를 가리킵니다. 개념상 전역 컨텍스트를 생성하는 주체가 바로 전역 객체이기 때문
     - 자바스크립트의 모든 변수는 특정 객체의 프로퍼티로 동작
     - 전역변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로 할당

   - 메서드로서 호출할 때 그 메서드 내부에서의 this
     - 함수와 메서드를 구분하는 유일한 차이는 <strong>독립성</strong>
