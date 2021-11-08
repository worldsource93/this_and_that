# Airbnb JavaScript Style Guide

Javascript에 대한 가장 합리적인 접근 방식 소개

> #### 😎이 문서는 회사의 좋은 개발문화를 위해 만들어졌습니다. Javascript 개발자들의 협업 혹은 개인 코드 작성 시 표준으로 사용되는 [Airbnb Javscript Style Guide](https://github.com/airbnb/javascript)의 목차 및 내용을 인용하였으며, 설명이 부족한 부분이라고 생각되는 부분은 내용을 추가하였습니다. 설명이 잘못되어 수정이 필요하거나 내용 추가가 필요한 경우 issue 등록해주시면 감사하겠습니다.😎
>
> ##### Author : 서세원 연구원([worldsource93](https://github.com/worldsource93))
>
> ##### reference : [Airbnb Javscript Style Guide](https://github.com/airbnb/javascript)
>
> ##### 참고: Airbnb Javascript Style Guide는 `babel`을 사용하고 있다고 가정하며, `babel-preset-airbnb` 또는 동등한 환경을 사용해야 한다.

---

## 목록

1. [Doodling Notes](#📝doodling-notes)
1. [Types](#types)
1. [References](#references)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. [Destructuring](#destructuring)
1. [Strings](#strings)
1. [Functions](#functions)
1. [Arrow Functions](#arrow-functions)
1. [Classes & Constructors](#classes-&-constructors)
1. [Modules](#modules)
1. Iterators and Generators
1. Properties
1. Variables
1. Hoisting
1. Comparison Operators & Equality
1. Blocks
1. Control Statements
1. Comments
1. Whitespace
1. Commas
1. Semicolons
1. Type Casting & Coercion
1. Naming Conventions
1. Accessors
1. Events
1. jQuery
1. ECMAScript 5 Compatibility
1. ECMAScript 6+ (ES 2015+) Styles
1. Standard Library
1. Testing
1. Performance
1. Resources
1. In the Wild
1. Translation
1. The JavaScript Style Guide Guide
1. Chat With Us About JavaScript
1. Contributors
1. License
1. Amendments

---

## 📝Doodling Notes

🙊단어 및 개념정리

- ### 문(Statement)과 표현식(Expressions)

  - 자바스크립트에서 `Statement`와 `Expression`은 아주 중요한 차이가 있으므로 명확하게 구분해야한다.

    <img src="https://media.vlpt.us/images/_uchanlee/post/b935aaa6-02ff-49e4-8086-407d813c1387/statement_expression-diagram.svg" width=150>

  <br />

  > ## Statement
  >
  > - 문
  > - 실행 가능한 최소의 독립적인 코드 조각
  > - statement는 흔히 한 개 이상의 expression 이나 프로그래밍 키워드를 포함하는 경우가 많다.
  > - 모든 문은 완료 값을 가진다. 값이 undefined 일수도 있다.

  <br />

  ```
  for (let i = 0; i < 10; i++) {} // for statement

  while (true) {} // while statement

  if (true) {} // if statement

  let a; // declaration statement

  function b() {} // function declaration statement
  ```

  <br />
  <br />

  > ## Expression
  >
  > - 표현식
  > - 특정 결과값이 계산되는 것

  <br />

  ```
  let a = 3 * 5; // 1번
  let b = a; // 2번
  b; // 3번
  ```

  1.  - `3 * 5`는 15라는 값으로 평가되는 표현식이다. <br />
      - `let a = 3 * 5;` 문은 변수를 선언하므로 선언문(Declaration Statement)이라 한다.
      - 앞에 변수형태를 적지 않는다면, 할당 표현식(Assignment Expression)이라고 한다. ex) `a = 3 * 5;`

  1.  - `let b = a;`문도 변수를 선언하므로 선언문이다.
      - a라는 표현식은 당시 변수들에 저장된 값으로 평가되므로 15라는 값으로 평가되고 역시 b는 15가 된다.
  1.  - b가 표현식의 전부지만 이것만으로도 완전한 문이다.
      - 일반적으로 이런 문은 표현식 문(Expression Statement)라고 부른다.

<br />
<br />

- ### Error Call Stack
  - FIXME: 내용 정리 필요

<br />
<br />

- ### Call Site
  - FIXME: 내용 정리 필요

<br />
<br />

- ### Syntactic sugar

  - 문법에 설탕을 뿌려 더 달콤하게 사용한다는 의미이다. 문법적으로 더 읽기 쉽고 이해하기 편하도록 표현되어지는 것을 말하는 것으로 적절하게 사용되면 가독성을 높이기 매우 좋다.
  - 대표적인 예
    - Javascript의 ES6부터 추가된 Class의 표현법
    - 람다식의 간결한 표현
    - Syntactic sugar의 장점은 ES6부터 추가된 Class의 경우에서 쉽게 찾아볼 수 있다. ES6의 Class가 기존 javascript의 함수체계와 다른 새로운 객체지향모델을 제공하는것이 아니라 기존 함수패턴의 Syntactic sugar로써 클래스 기반 언어에 익숙한 프로그래머들도 보다 빨리 학습하고 알아보기 쉽게하며 더욱 직관적인 표현이 가능해진다.

<br />
<br />

☝ [목록으로 돌아가기](#목록)

---

## Types

- 1.1 원시 자료형(Primitive data type)

  - call by value, 불변, immutable
  - 원본 값을 복사해서 사용하는 개념, 값을 전달받은 함수나 단락(block)에서 값을 변경해도 복사해서 가져온 값이 수정될 뿐, 원본에는 아무런 영향이 없다.
  - 원시 자료형의 종류

    - `string`
    - `number`
    - `symbol`
    - `bigint`
    - `boolean` : true || false
    - `null` : 의도적으로 비어있음을 표현한다.
    - `undefined` : 변수가 정의되지 않았음을 의미한다. 직접 할당하는 행위 X

    <br />

    > Note: `symbol`과 `bigint`는 타겟 브라우저가 이를 지원하는지 확인하고 사용해야한다.

    ```
    const foo = 1;
    let bar = foo;

    bar = 9;

    console.log(foo, bar); // => 1, 9
    ```

  <br />

- 1.2 참조 자료형(Reference data type)

  - call by reference, !불변, mutable
  - call by value와 동일하게 원본 값을 복사해서 사용하지만 원본 값이 가르키는 대상이 <strong>값</strong>인지 <strong>주소값</strong>인지에 따라 다르며 주소값을 가르키는 경우, call by value와 다르게 원본에도 변경이 일어난다.
  - 참조 자료형의 종류

    - `object`
    - `array`
    - `function`

    <br />

    ```
    const foo = [1, 2];
    const bar = foo;

    bar[0] = 9;

    console.log(foo[0], bar[0]); // => 9, 9
    ```

☝ [목록으로 돌아가기](#목록)

---

## References

- 2.1 모든 참조에 `const`를 사용하고 `var`사용을 피하자. eslint: <a href="https://eslint.org/docs/rules/prefer-const.html" target="_blank">`prefer-const`</a>, <a href="https://eslint.org/docs/rules/no-const-assign.html" target="_blank">`no-const-assign`</a>

  > `var`를 사용을 피해야하는 이유는 다음과 같다. <br /> 1. 참조를 재할당 할 수 없다. <br /> 2. 예상치 못한 사이드 이펙트를 일으킨다. <br /> 3. scope가 다르기때문에 코드를 이해하는데 어려움을 증가시킨다.

  ```
  // bad
  var a = 1;
  var b = 2;

  // good
  const a = 1;
  const b = 2;
  ```

  <br />

- 2.2 참조를 재할당해야하는 경우 `var` 대신 `let`을 사용하자. eslint: <a href="https://eslint.org/docs/rules/no-var.html" target="_blank">`no-var`</a>

  > `var`처럼 function-scoped가 아닌 block-scoped로 사용하자.

  ```
  // bad
  var count = 1;
  if (true) {
    count += 1;
  }

  // good, use the let.
  let count = 1;
  if (true) {
    count += 1;
  }
  ```

  <br />

- 2.3 `let`과 `const`는 block-scoped인 반면, `var`은 function-scoped이다.

  ```
  // const and let only exist in the blocks they are defined in.
  {
    let a = 1;
    const b = 1;
    var c = 1;
  }
  console.log(a); // ReferenceError
  console.log(b); // ReferenceError
  console.log(c); // Prints 1
  ```

  > `a`와 `b`는 block scoped이므로 block 밖에서 호출되지 않는다. 반면, `c`는 function scoped이므로 hoisting이 일어나 블록 밖에서 호출이 가능하다.

☝ [목록으로 돌아가기](#목록)

---

## Objects

- 3.1 Object 생성 시, literal syntax를 사용하자. eslint: <a href="https://eslint.org/docs/rules/no-new-object.html" target="_blank">`no-new-object`</a>

  ```
  // bad
  const item = new Object();

  // good
  const item = {};
  ```

  <br />

- 3.2 dynamic property를 사용한 Object 생성 시, computed property name을 사용하자.

  > 왜 computed property name을 사용해야하는가? 한 장소에서 객체를 정의할 수 있기 때문이다. <br />
  > computed property name은 객체의 key값을 표현식(변수, 함수 등을 이용)을 통해 지정하는 것을 지칭한다.

  ```
  function getKey(k) {
    return `a key named ${k}`;
  }

  // bad
  const obj = {
    id: 5,
    name: 'San Francisco',
  };
  obj[getKey('enabled')] = true;

  // good
  const obj = {
    id: 5,
    name: 'San Francisco',
    [getKey('enabled')]: true,
  };
  ```

  <br />

- 3.3 객체 메서드 표현을 짧게하자. eslint: <a href="https://eslint.org/docs/rules/object-shorthand.html" target="_blank">`object-shorthand`</a>

  ```
  // bad
  const atom = {
    value: 1,

    addValue: function (value) {
      return atom.value + value;
    },
  };

  // good
  const atom = {
    value: 1,

    addValue(value) {
      return atom.value + value;
    },
  };
  ```

  <br />

- 3.4 property value 사용 시 짧게 쓸 수 있다면 짧게 쓰자. eslint: <a href="https://eslint.org/docs/rules/object-shorthand.html" target="_blank">`object-shorthand`</a>

  > 간단명료하며 묘사적이다.

  ```
  const lukeSkywalker = 'Luke Skywalker';

  // bad
  const obj = {
    lukeSkywalker: lukeSkywalker,
  };

  // good
  const obj = {
    lukeSkywalker,
  };
  ```

  <br />

- 3.5 선언 시, shorthand properties는 그룹화 및 최상단에 위치시키자.

  > 그룹화 및 최상단에 위치시켜 코드의 가독성을 높인다.

  ```
  const anakinSkywalker = 'Anakin Skywalker';
  const lukeSkywalker = 'Luke Skywalker';

  // bad
  const obj = {
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    lukeSkywalker,
    episodeThree: 3,
    mayTheFourth: 4,
    anakinSkywalker,
  };

  // good
  const obj = {
    lukeSkywalker,
    anakinSkywalker,
    episodeOne: 1,
    twoJediWalkIntoACantina: 2,
    episodeThree: 3,
    mayTheFourth: 4,
  };
  ```

  <br />

- 3.6 사용할 수 없는 식별자만 quote를 사용하자. eslint: <a href="https://eslint.org/docs/rules/quote-props.html" target="_blank">`quote-props`</a>

  > 더 쉽게 JS 엔진에 의해 최적화되며 syntax highlighting을 개선하고, 일반적으로 읽기 쉽다.

  ```
  // bad
  const bad = {
    'foo': 3,
    'bar': 4,
    'data-blah': 5,
  };

  // good
  const good = {
    foo: 3,
    bar: 4,
    'data-blah': 5,
  };
  ```

  <br />

- 3.7 `hasOwnProperty`, `propertyIsEnumerable`, `isPrototypeOf`와 같은 `Object.prototype` 메서드를 직접 호출하지말자. eslint: <a href="https://eslint.org/docs/rules/no-prototype-builtins" target="_blank">`no-prototype-builtins`</a>

  > 객체에 `Object.prototype` 메서드를 직접 사용하지않는 이유 <br /> <strong>1. Object.create(null)</strong> <br /> Object.create() 메소드에 null을 인자로 주어 객체를 생성하게 되면 Object.prototype을 상속받지 않게 된다. 위와 같이 만들어진 객체에 builtin 메소드를 직접 호출하게 되면 에러가 발생한다.
  >
  > <strong>2. 속성이 builtin 메서드와 이름이 같은 경우를 방지</strong> <br /> 객체에 builtin으로 제공되는 메서드와 같은 이름의 키를 객체가 가지고 있다면 예상한 대로 동작하지 않을 수 있다. 이런 이유로 no-prototype-builtins 규칙은 builtin 메서드 사용 시 Object.prototype을 활용하도록 권장한다.

  ```
  // bad
  console.log(object.hasOwnProperty(key));

  // good
  console.log(Object.prototype.hasOwnProperty.call(object, key));

  // best
  const has = Object.prototype.hasOwnProperty; // cache the lookup   once, in module scope.
  console.log(has.call(object, key));
  /* or */
  import has from 'has'; // https://www.npmjs.com/package/has
  console.log(has(object, key));
  ```

  <br />

- 3.8 얕은 객체 복사 시 `Object.assign`보다 객체 스프레드 구문이 좋다. object rest operator를 사용해 특정 속성을 생략한 새 객체를 가져올 수 있다. eslint: <a href="https://eslint.org/docs/rules/prefer-object-spread" target="_blank">`prefer-object-spread`</a>

  ```
  // very bad
  const original = { a: 1, b: 2 };
  const copy = Object.assign(original, { c: 3 }); // this mutates   `original` ಠ_ಠ
  delete copy.a; // so does this

  // bad
  const original = { a: 1, b: 2 };
  const copy = Object.assign({}, original, { c: 3 }); // copy => { a: 1,   b: 2, c: 3 }

  // good
  const original = { a: 1, b: 2 };
  const copy = { ...original, c: 3 }; // copy => { a: 1, b: 2, c: 3 }

  const { a, ...noA } = copy; // noA => { b: 2, c: 3 }
  ```

  > Note: 원본을 변형시키는 코드는 지양

☝ [목록으로 돌아가기](#목록)

---

## Arrays

- 4.1 배열 생성 시, literal syntax를 사용하자. eslint: <a href="https://eslint.org/docs/rules/no-array-constructor.html" target="_blank">`no-array-constructor`</a>

  ```
  // bad
  const items = new Array();

  // good
  const items = [];
  ```

  <br />

- 4.2 배열에 항목을 추가할 때 직접 할당 대신 Array.push를 사용하자.

  ```
  const someStack = [];

  // bad
  someStack[someStack.length] = 'abracadabra';

  // good
  someStack.push('abracadabra');
  ```

  <br />

- 4.3 배열 복사 시, 배열 스프레드를 사용하자.

  ```
  // bad
  const len = items.length;
  const itemsCopy = [];
  let i;

  for (i = 0; i < len; i += 1) {
    itemsCopy[i] = items[i];
  }

  // good
  const itemsCopy = [...items];
  ```

  <br />

- 4.4 반복 가능한 객체를 배열로 변환하려면 `Array.from` 대신 `...`을 사용하자.

  ```
  const foo = document.querySelectorAll('.foo');

  // good
  const nodes = Array.from(foo);

  // best
  const nodes = [...foo];
  ```

  <br />

- 4.5 배열과 유사한 객체를 배열로 변환하려면 `Array.from`을 사용하자.

  ```
  const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

  // bad
  const arr = Array.prototype.slice.call(arrLike);

  // good
  const arr = Array.from(arrLike);
  ```

  <br />

- 4.6 반복가능한 매핑의 경우 스프레드 대신 `Array.from`을 사용하자.

  ```
  // bad
  const baz = [...foo].map(bar);

  // good
  const baz = Array.from(foo, bar);
  ```

  > `Array.from`의 목적은 유사배열을 배열로 복사하는 것이며, 복사본에 모든 배열의 메서드를 사용할 수 있다.(`map()`, `forEach()`, `filter()`, `.splice()`, `.sort()`, `.push()` 등등...) <br /> 유사배열을 스프레드를 사용하여 배열로 사용하는 것보다 `Array.from`으로 변환 하는 것이 훨씬 효율적이다.

  ```
  const a = () => [{"count": 3},{"count": 4},{"count": 5}].map(item =>   item.count);
  const b = () => Array.from([{"count": 3},{"count": 4},{"count": 5}], x   => x.count);

  let iterations = 1000000;
  console.time('Function #1');
  for(let i = 0; i < iterations; i++ ){
      b();
  };
  console.timeEnd('Function #1') // Function #1: 520.591064453125ms

  console.time('Function #2');
  for(let j = 0; j < iterations; j++ ){
      a();
  };
  console.timeEnd('Function #2'); // Function #2: 33.622802734375ms
  ```

  <br />

- 4.7 배열 메서드 콜백에서 `return`을 사용하자. 함수 본문이 부작용 없이 식을 반환하는 단일문장으로 구성되어 있다면 반환을 생략해도 된다. eslint: <a href="https://eslint.org/docs/rules/array-callback-return" target="_blank">`array-callback-return`</a>

  ```
  // good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });

  // good
  [1, 2, 3].map((x) => x + 1);

  // bad - no returned value means `acc` becomes undefined after the   first iteration
  [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
    const flatten = acc.concat(item);
  });

  // good
  [[0, 1], [2, 3], [4, 5]].reduce((acc, item, index) => {
    const flatten = acc.concat(item);
    return flatten;
  });

  // bad
  inbox.filter((msg) => {
    const { subject, author } = msg;
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee';
    } else {
      return false;
    }
  });

  // good
  inbox.filter((msg) => {
    const { subject, author } = msg;
    if (subject === 'Mockingbird') {
      return author === 'Harper Lee';
    }

    return false;
  });

  let bool = false;

  // bad
  foo(() => bool = true);

  // good
  foo(() => {
    bool = true;
  });
  ```

  <br />

- 4.8 배열이 여러 줄로 이루어져 있다면, 열린 직후와 닫기 직전에 줄바꿈을 한다.

  ```
  // bad
  const arr = [
    [0, 1], [2, 3], [4, 5],
  ];

  const objectInArray = [{
    id: 1,
  }, {
    id: 2,
  }];

  const numberInArray = [
    1, 2,
  ];

  // good
  const arr = [[0, 1], [2, 3], [4, 5]];

  const objectInArray = [
    {
      id: 1,
    },
    {
      id: 2,
    },
  ];

  const numberInArray = [
    1,
    2,
  ];
  ```

  > Note: `objectInArray`는 좋은 컨벤션이라고 생각하고, 이외 컨벤션은 팀끼리 상의해서 맞추면 될 것 같다.

☝ [목록으로 돌아가기](#목록)

---

## Destructuring

- 5.1 객체에서 여러 속성을 사용하는 경우, 객체 접근 시 구조 분해를 사용하자. eslint: <a href="https://eslint.org/docs/rules/prefer-destructuring" target="_blank">`prefer-destructuring`</a>

  > 구조 분해를 사용하면 해당 속성에 대한 임시 참조를 만들어 객체의 반복적인 접근을 방지할 수 있다. 반복적인 객체 접근은 더 많은 중복된 코드를 생성하고 더 많은 리소스를 필요로 하며 실수 빈도를 높인다. 또한 객체 구조 분해는 블록에서 사용되는 객체 구조에 대한 single site of definition(정의된 하나의 물리적 영역)이 제공되므로 사용할 항목을 정하기 위해 블록 전체를 읽을 필요가 없게된다.

  ```
  // bad
  function getFullName(user) {
    const firstName = user.firstName;
    const lastName = user.lastName;

    return `${firstName} ${lastName}`;
  }

  // good
  function getFullName(user) {
    const { firstName, lastName } = user;
    return `${firstName} ${lastName}`;
  }

  // best
  function getFullName({ firstName, lastName }) {
    return `${firstName} ${lastName}`;
  }
  ```

  <br />

- 5.2 배열 구조 분해를 사용하자. eslint: <a href="https://eslint.org/docs/rules/prefer-destructuring" target="_blank">`prefer-destructuring`</a>

  ```
  const arr = [1, 2, 3, 4];

  // bad
  const first = arr[0];
  const second = arr[1];

  // good
  const [first, second] = arr;
  ```

  <br />

- 5.3 복수의 값 반환(return multiple values)을 위해서는 배열 구조 분해가 아닌 객체 구조 분해를 사용하자.

  > call sites(<a href="https://en.wikipedia.org/wiki/Call_site" target="_blank">`call site`</a>: 함수가 호출되는 영역, 위치)를 중단하지 않고 때에 따라 새로운 속성을 추가하거나 순서를 변경할 수 있다. <br />
  >
  > <p color="red">FIXME: call site에 대한 개념이 명확하게 이해가 되지 않아 다시 정리할 것</p>

  ```
  // bad
  function processInput(input) {
    // then a miracle occurs
    return [left, right, top, bottom];
  }

  // the caller needs to think about the order of return data
  const [left, __, top] = processInput(input);

  // good
  function processInput(input) {
    // then a miracle occurs
    return { left, right, top, bottom };
  }

  // the caller selects only the data they need
  const { left, top } = processInput(input);
  ```

☝ [목록으로 돌아가기](#목록)

---

## Strings

- 6.1 문자열에는 single quotes를 사용하자. eslint: <a href="https://eslint.org/docs/rules/quotes.html" target="_blank">`quotes`</a>

  ```
  // bad
  const name = "Capt. Janeway";

  // bad - template literals should contain interpolation or newlines
  const name = `Capt. Janeway`;

  // good
  const name = 'Capt. Janeway';
  ```

  <br />

- 6.2 100자 이상의 문자열을 여러 줄에 걸쳐서 연결하면 안된다.

  > 끊어진 문자열은 성가시고 코드 검색성이 떨어진다.

  ```
  // bad
  const errorMessage = 'This is a super long error that was thrown   because \
  of Batman. When you stop to think about how Batman had anything to   do \
  with this, you would get nowhere \
  fast.';

  // bad
  const errorMessage = 'This is a super long error that was thrown   because ' +
    'of Batman. When you stop to think about how Batman had anything   to do ' +
    'with this, you would get nowhere fast.';

  // good
  const errorMessage = 'This is a super long error that was thrown   because of Batman. When you stop to think about how Batman had   anything to do with this, you would get nowhere fast.';
  ```

  <br />

- 6.3 문자열을 프로그래밍 방식으로 구성할 때, 연결 대신 템플릿 문자열을 사용하자. eslint: <a href="https://eslint.org/docs/rules/prefer-template.html" target="_blank">`prefer-template`</a>, <a href="https://eslint.org/docs/rules/template-curly-spacing" target="_blank">`template-curly-spacing`</a>

  > 템플릿 문자열은 간결한 구문을 제공하고, 적절한 줄바꿈과 보간 기능을 제공한다.

  ```
  // bad
  function sayHi(name) {
    return 'How are you, ' + name + '?';
  }

  // bad
  function sayHi(name) {
    return ['How are you, ', name, '?'].join();
  }

  // bad
  function sayHi(name) {
    return `How are you, ${ name }?`;
  }

  // good
  function sayHi(name) {
    return `How are you, ${name}?`;
  }
  ```

  <br />

- 6.4 문자열에 `eval()`을 사용하면 안된다. 많은 취약성을 야기시킨다. eslint: <a href="https://eslint.org/docs/rules/no-eval" target="_blank">`no-eval`</a>

  <br />

- 6.5 문자열의 문자를 불필요하게 이탈시키지말자.

  > 백슬래쉬는 가독성을 손상시키므로 필요한 경우에만 사용해야 한다.

  ```
  // bad
  const foo = '\'this\' \i\s \"quoted\"';

  // good
  const foo = '\'this\' is "quoted"';
  const foo = `my name is '${name}'`;
  ```

☝ [목록으로 돌아가기](#목록)

---

## Functions

- 7.1 함수 선언식 대신 명명된 함수 표현식을 사용하자.

  > 함수 선언식은 호이스팅되기 때문에 파일에서 함수를 정의하기 전에 참조할 수 있고, 이는 가독성과 유지보수성을 해친다. 함수의 정의가 파일의 나머지 부분을 이해하는데 방해 혹은 간섭이 될정도로 크거나 복잡하다면, 함수를 자체 모듈로 추출해야한다. 표현식을 담고있는 변수에서 이름이 추론되는지 여부에 상관없이 표현식에 명시적 이름을 붙이는 것을 잊지말자. 이렇게 하면 Error call stack에 대한 모든 가정을 없앨 수 있다. <br />
  >
  > <p color="red">FIXME: Error call stack에 대한 모든 가정을 없앨 수 있다는 의미는 무엇인지 좀 더 찾아서 다시 정리</p>

  ```
  // bad
  function foo() {
    // ...
  }

  // bad
  const foo = function () {
    // ...
  };

  // good
  // lexical name distinguished from the variable-referenced   invocation(s)
  const short = function longUniqueMoreDescriptiveLexicalFoo() {
    // ...
  };
  ```

  <br />

- 7.2 IIFE(immediately invoked function expressions, 즉시실행함수)를 괄호로 묶자. eslint: <a href="https://eslint.org/docs/rules/wrap-iife.html" target="_blank">`wrap-iife`</a>

  > IIFE는 단일 단위이므로 이를 포장하여 깔끔하게 표현하자. 거의 모든 IIFE는 모듈로 대체 가능하다.

  ```
  // immediately-invoked function expression (IIFE)
  (function () {
    console.log('Welcome to the Internet. Please follow me.');
  }());
  ```

  <br />

- 7.3 함수블록이 아닌 곳(`if`, `while`, etc...)에 함수를 선언하지마라. 대신 함수를 변수에 할당하자. 브라우저는 우리가 그렇게 할 수 있도록 해주지만 안타깝게도 브라우저 별로 다르게 해석한다. eslint: <a href="https://eslint.org/docs/rules/no-loop-func.html" target="_blank">`no-loop-func`</a>

  <br />

- 7.4 ECMA-262는 `block`을 문(statement)의 한 종류로 정의하고 있다. 함수 선언은 문이 아닙니다. Doodling notes: [Statement](#statement), [Expression](#expression)

  ```
  // bad
  if (currentUser) {
    function test() {
      console.log('Nope.');
    }
  }

  // good
  let test;
  if (currentUser) {
    test = () => {
      console.log('Yup.');
    };
  }
  ```

  <br />

- 7.5 매개변수 이름을 `arguments`라 지정하지 말자. 이는 모든 함수 범위에 주어진 `arguments` 객체보다 우선한다.

  ```
  // bad
  function foo(name, options, arguments) {
    // ...
  }

  // good
  function foo(name, options, args) {
    // ...
  }
  ```

  <br />

- 7.6 `arguments`를 사용하지말고 rest 구문인 `...`를 대신 사용하자. eslint: <a href="https://eslint.org/docs/rules/prefer-rest-params" target="_blank">`prefer-rest-params`</a>

  > `...`는 원하는 것을 명백하게 표현할 수 있다. 또한, 나머지 parameter는 유사 배열이 아닌 실제 배열이다.

  ```
  // bad
  function concatenateAll() {
    const args = Array.prototype.slice.call(arguments);
    return args.join('');
  }

  // good
  function concatenateAll(...args) {
    return args.join('');
  }
  ```

  <br />

- 7.7 변형되는 함수 parameter 대신 기본 매개 변수 구문을 사용하자.

  ```
  // really bad
  function handleThings(opts) {
    // No! We shouldn’t mutate function arguments.
    // Double bad: if opts is falsy it'll be set to an object which   may
    // be what you want but it can introduce subtle bugs.
    opts = opts || {};
    // ...
  }

  // still bad
  function handleThings(opts) {
    if (opts === void 0) {
      opts = {};
    }
    // ...
  }

  // good
  function handleThings(opts = {}) {
    // ...
  }
  ```

  <br />

- 7.8 기본 변수 설정의 side effects를 회피하자.

  > side effects는 판단에 혼란을 준다.

  ```
  var b = 1;
  // bad
  function count(a = b++) {
    console.log(a);
  }
  count();  // 1
  count();  // 2
  count(3); // 3
  count();  // 3
  ```

  <br />

- 7.9 항상 기본값 설정은 마지막에 하자. eslint: <a href="https://eslint.org/docs/rules/default-param-last" target="_blank">`default-param-last`</a>

  ```
  // bad
  function handleThings(opts = {}, name) {
    // ...
  }

  // good
  function handleThings(name, opts = {}) {
    // ...
  }
  ```

  <br />

- 7.10 Function constructor를 사용하여 새로운 함수를 생성하지 마라. eslint: <a href="https://eslint.org/docs/rules/no-new-func" target="_blank">`no-new-func`</a>

  > 이러한 방식으로 새로운 함수를 생성하는 것은 `eval()`과 유사하게 문자열을 평가하여 취약성이 생기게된다.

  ```
  // bad
  var add = new Function('a', 'b', 'return a + b');

  // still bad
  var subtract = Function('a', 'b', 'return a - b');
  ```

  <br />

- 7.11 function signature는 띄어쓰자. eslint: <a href="https://eslint.org/docs/rules/space-before-function-paren" target="_blank">`space-before-function-paren`</a>, <a href="https://eslint.org/docs/rules/space-before-blocks" target="_blank">`space-before-blocks`</a>

  > 일관성이 있고 이름을 수정할 때, 공백을 추가하거나 제거할 필요가 없다.

  ```
  // bad
  const f = function(){};
  const g = function (){};
  const h = function() {};

  // good
  const x = function () {};
  const y = function a() {};
  ```

  <br />

- 7.12 매개변수를 변형시키지 마라. eslint: <a href="https://eslint.org/docs/rules/no-param-reassign.html" target="_blank">`no-param-reassign`</a>

  > 매개변수로 전달된 객체를 조작하는 것은 원본에 의도치 않은 side effects를 발생 시킬 수 있다.

  ```
  // bad
  function f1(obj) {
    obj.key = 1;
  }

  // good
  function f2(obj) {
    const key = Object.prototype.hasOwnProperty.call(obj, 'key') ? obj.key : 1;
  }
  ```

  <br />

- 7.13 매개변수를 재할당하지마라. eslint: <a href="https://eslint.org/docs/rules/no-param-reassign.html" target="_blank">`no-param-reassign`</a>

  > 매개변수를 재할당하는 것은 예기치 않은 동작으로 연결될 수 있다.(특히, `arguments` object에 접근할 때) 이것은 최적화 문제를 발생시킬 수 있다. (특히, <a href="https://engineering.huiseoul.com/  %EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8%EB%8A%94-%EC%  96%B4%EB%96%BB%EA%B2%8C-%EC%9E%91%EB%8F%99%ED%95%98%EB%8A%94%EA%B0%8  0-v8-%EC%97%94%EC%A7%84%EC%9D%98-%EB%82%B4%EB%B6%80-%EC%B5%9C%EC%A0%  81%ED%99%94%EB%90%9C-%EC%BD%94%EB%93%9C%EB%A5%BC-%EC%9E%91%EC%84%B1%  EC%9D%84-%EC%9C%84%ED%95%9C-%EB%8B%A4%EC%84%AF-%EA%B0%80%EC%A7%80-%E  D%8C%81-6c6f9832c1d9" target="_blank">`V8`</a>에서)

  ```
  // bad
  function f1(a) {
    a = 1;
    // ...
  }

  function f2(a) {
    if (!a) { a = 1; }
    // ...
  }

  // good
  function f3(a) {
    const b = a || 1;
    // ...
  }

  function f4(a = 1) {
    // ...
  }
  ```

  <br />

- 7.14 가변인자 함수를 호출하려면 스프레드 구문인 `...`을 사용하는 것이 좋다.

  > 더 깔끔하고 컨텍스트를 제공할 필요가 없다.

  ```
  // bad
  const x = [1, 2, 3, 4, 5];
  console.log.apply(console, x);

  // good
  const x = [1, 2, 3, 4, 5];
  console.log(...x);

  // bad
  new (Function.prototype.bind.apply(Date, [null, 2016, 8, 5]));

  // good
  new Date(...[2016, 8, 5]);
  ```

  <br />

- 7.15 여러줄의 signatures 또는 invocation이 있는 함수의 경우, 모든 멀티라인 목록과 동일하게 들여써야 한다. eslint: <a href="https://eslint.org/docs/rules/function-paren-newline" target="_blank">`function-paren-newline`</a>

  ```
  // bad
  function foo(bar,
               baz,
               quux) {
    // ...
  }

  // good
  function foo(
    bar,
    baz,
    quux,
  ) {
    // ...
  }

  // bad
  console.log(foo,
    bar,
    baz);

  // good
  console.log(
    foo,
    bar,
    baz,
  );
  ```

☝ [목록으로 돌아가기](#목록)

---

## Arrow Functions

- 8.1 인라인콜백을 전달할 때와 같이 익명 함수를 사용해야 하는 경우, 화살표 함수 표기법을 사용하자. eslint: <a href="https://eslint.org/docs/rules/prefer-arrow-callback.html" target="_blank">`prefer-arrow-callback`</a>, <a href="https://eslint.org/docs/rules/arrow-spacing.html" target="_blank">`arrow-spacing`</a>

  > 해당 컨텍스트에서 실행되는 함수를 만들고 보다 간결한 구문이다.

  > 만약, 상당히 복잡한 함수를 가지고 있다면 로직을 분리해서 명명함수로 뽑아낼 수 있다.

  ```
  // bad
  [1, 2, 3].map(function (x) {
    const y = x + 1;
    return x * y;
  });

  // good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });
  ```

  <br />

- 8.2 함수 본문이 side effects 없이 식(expression)을 반환하는 단일 문으로 구성된 경우, 중괄호를 생략하고 암시적 반환을 사용한다. 다른 방법으로는 중괄호를 사용하고 문(statement)을 반환하자. eslint: <a href="https://eslint.org/docs/rules/arrow-parens.html" target="_blank">`arrow-parens`</a>, <a href="https://eslint.org/docs/rules/arrow-body-style.html" target="_blank">`arrow-body-style`</a>

  > [`Syntactic sugar`](#syntactic-sugar). 여러 함수가 함께 체인될 때, 더 잘 읽힌다.

  ```
  // bad
  [1, 2, 3].map((number) => {
    const nextNumber = number + 1;
    `A string containing the ${nextNumber}.`;
  });

  // good
  [1, 2, 3].map((number) => `A string containing the ${number + 1}.`);

  // good
  [1, 2, 3].map((number) => {
    const nextNumber = number + 1;
    return `A string containing the ${nextNumber}.`;
  });

  // good
  [1, 2, 3].map((number, index) => ({
    [index]: number,
  }));

  // No implicit return with side effects
  function foo(callback) {
    const val = callback();
    if (val === true) {
      // Do something if callback returns true
    }
  }

  let bool = false;

  // bad
  foo(() => bool = true);

  // good
  foo(() => {
    bool = true;
  });
  ```

  <br />

- 8.3 식이 여러줄에 걸쳐 있는 경우, 읽기 쉽도록 괄호로 묶자.

  > 괄호로 묶는 것은 함수의 시작과 끝을 명확하게 보여준다.

  ```
  // bad
  ['get', 'post', 'put'].map((httpMethod) => Object.prototype.  hasOwnProperty.call(
      httpMagicObjectWithAVeryLongName,
      httpMethod,
    )
  );

  // good
  ['get', 'post', 'put'].map((httpMethod) => (
    Object.prototype.hasOwnProperty.call(
      httpMagicObjectWithAVeryLongName,
      httpMethod,
    )
  ));
  ```

  <br />

- 8.4 명확하고 일관성 있기위해 항상 `arguments` 주위에 괄호를 넣자. eslint: <a href="https://eslint.org/docs/rules/arrow-parens.html" target="_blank">`arrow-parens`</a>

  > arguments를 추가하거나 제거할 때, 변경을 최소화한다.

  ```
  // bad
  [1, 2, 3].map(x => x * x);

  // good
  [1, 2, 3].map((x) => x * x);

  // bad
  [1, 2, 3].map(number => (
    `A long string with the ${number}. It’s so long that we don’t want   it to take   up space on the .map line!`
  ));

  // good
  [1, 2, 3].map((number) => (
    `A long string with the ${number}. It’s so long that we don’t want   it to take   up space on the .map line!`
  ));

  // bad
  [1, 2, 3].map(x => {
    const y = x + 1;
    return x * y;
  });

  // good
  [1, 2, 3].map((x) => {
    const y = x + 1;
    return x * y;
  });
  ```

  <br />

- 8.5 화살표 함수 구문의 `=>`와 비교 연산자의 `<=`, `>=`를 헷갈리지 말자. eslint: <a href="https://eslint.org/docs/rules/no-confusing-arrow" target="_blank">`no-confusing-arrow`</a>

  ```
  // bad
  const itemHeight = (item) => item.height <= 256 ? item.largeSize : item.smallSize;

  // bad
  const itemHeight = (item) => item.height >= 256 ? item.largeSize : item.smallSize;

  // good
  const itemHeight = (item) => (item.height <= 256 ? item.largeSize : item.smallSize);

  // good
  const itemHeight = (item) => {
    const { height, largeSize, smallSize } = item;
    return height <= 256 ? largeSize : smallSize;
  };
  ```

  <br />

- 8.6 화살표 함수의 본문에 암시적 반환값을 위치시키자. eslint: <a href="https://eslint.org/docs/rules/implicit-arrow-linebreak" target="_blank">`implicit-arrow-linebreak`</a>

  ```
  // bad
  (foo) =>
    bar;

  (foo) =>
    (bar);

  // good
  (foo) => bar;
  (foo) => (bar);
  (foo) => (
     bar
  )
  ```

☝ [목록으로 돌아가기](#목록)

---

## Classes & Constructor

- 9.1 항상 `class`를 사용해라. 직접 `prototype`을 다루는 것을 피해라.

  > `class` 구문이 더 간결하고 추론하기 쉽다.

  ```
  // bad
  function Queue(contents = []) {
    this.queue = [...contents];
  }
  Queue.prototype.pop = function () {
    const value = this.queue[0];
    this.queue.splice(0, 1);
    return value;
  };

  // good
  class Queue {
    constructor(contents = []) {
      this.queue = [...contents];
    }
    pop() {
      const value = this.queue[0];
      this.queue.splice(0, 1);
      return value;
    }
  }
  ```

<br />

- 9.2 상속에는 `extends`를 사용하자.

  > `extends`는 `instanceof`를 파괴하지 않고 프로토타입 기능을 상속할 수 있는 기본 제공 방법이다.

  ```
  // bad
  const inherits = require('inherits');
  function PeekableQueue(contents) {
    Queue.apply(this, contents);
  }
  inherits(PeekableQueue, Queue);
  PeekableQueue.prototype.peek = function () {
    return this.queue[0];
  };

  // good
  class PeekableQueue extends Queue {
    peek() {
      return this.queue[0];
    }
  }
  ```

<br />

- 9.3 메서드는 메서드 체이닝을 도울 수 있도록 이 값을 반환할 수 있다.

  ```
  // bad
  Jedi.prototype.jump = function () {
    this.jumping = true;
    return true;
  };

  Jedi.prototype.setHeight = function (height) {
    this.height = height;
  };

  const luke = new Jedi();
  luke.jump(); // => true
  luke.setHeight(20); // => undefined

  // good
  class Jedi {
    jump() {
      this.jumping = true;
      return this;
    }

    setHeight(height) {
      this.height = height;
      return this;
    }
  }

  const luke = new Jedi();

  luke.jump()
    .setHeight(20);

  console.log(luke); // Jedi { jumping: true, height: 20 }
  ```

<br />

- 9.4 커스텀 `toString()`메서드를 작성해도 괜찮다. 성공적으로 작동하는지, side effects를 일으키지 않는지 확인하자.

  ```
  class Jedi {
    constructor(options = {}) {
      this.name = options.name || 'no name';
    }

    getName() {
      return this.name;
    }

    toString() {
      return `Jedi - ${this.getName()}`;
    }
  }
  ```

  <br />

- 9.5 클래스는 지정되지 않은 경우, 기본 생성자를 가진다. 빈 생성자 함수 또는 부모 클래스에 위임하는 함수만 사용할 수 있다. eslint: <a href="https://eslint.org/docs/rules/no-useless-constructor" target="_blank">`no-useless-constructor`</a>

  ```
  // bad
  class Jedi {
    constructor() {}

    getName() {
      return this.name;
    }
  }

  // bad
  class Rey extends Jedi {
    constructor(...args) {
      super(...args);
    }
  }

  // good
  class Rey extends Jedi {
    constructor(...args) {
      super(...args);
      this.name = 'Rey';
    }
  }
  ```

<br />

- 9.6 class members의 중복을 피하자.

  > 중복된 class member 선언은 마지막 선언을 자동으로 호출한다. 중복이 있는 것은 버그와 다름없다.

  ```
  // bad
  class Foo {
    bar() { return 1; }
    bar() { return 2; }
  }

  // good
  class Foo {
    bar() { return 1; }
  }

  // good
  class Foo {
    bar() { return 2; }
  }
  ```

<br />

- 9.7 외부 라이브러리 또는 프레임워크에서 특정 non-static 메서드 사용을 요구하지 않는 경우, 클래스 메서드는 `this`를 사용하거나 static 메서드로 만들어야한다. 인스턴스 메서드는 receiver의 속성에 따라 다르게 동작한다는 것을 나타내야 한다. eslint: <a href="" target="_blank">`class-methods-use-this`</a>

> `receiver`라는 개념은 오직 property에 접근했을 때, 임의 코드를 실행할 수 있는 경우에만 관련이 있다. `Accessor properties`를 의미하며, `receiver`는 일반적으로 속성을 정의한 객체나 속성을 상속하는 다른 객체를 의미한다.

> FIXME: doodling notes에 `prototype`과 `instance` 정리 후 연관지어서 내용 수정하기
> <br />

```
// bad
class Foo {
  bar() {
    console.log('bar');
  }
}

// good - this is used
class Foo {
  bar() {
    console.log(this.bar);
  }
}

// good - constructor is exempt
class Foo {
  constructor() {
    // ...
  }
}

// good - static methods aren't expected to use this
class Foo {
  static bar() {
    console.log('bar');
  }
}
```

☝ [목록으로 돌아가기](#목록)

---

## Modules
