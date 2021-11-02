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

1. [Types](#types)
1. [References](#references)
1. [Objects](#objects)
1. [Arrays](#arrays)
1. Destructuring
1. Strings
1. Functions
1. Arrow Functions
1. Classes & Constructors
1. Modules
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

## Types

- <strong>1.1 원시 자료형(Primitive data type)</strong>

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

- <strong>1.2 참조 자료형(Reference data type)</strong>

  - call by reference, !불변, mutable
  - call by value와 동일하게 원본 값을 복사해서 사용하지만 원본 값이 가르키는 대상이 <strong>값</ strong>인지 <strong>주소값</strong>인지에 따라 다르며 주소값을 가르키는 경우, call by value와 다르게 원본에도 변경이 일어난다.
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

- 4.2 배열에 항목을 추가할 때 직접 할당 대신 Array.push를 사용하자.

  ```
  const someStack = [];

  // bad
  someStack[someStack.length] = 'abracadabra';

  // good
  someStack.push('abracadabra');
  ```

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

- 4.4 반복 가능한 객체를 배열로 변환하려면 `Array.from` 대신 `...`을 사용하자.

  ```
  const foo = document.querySelectorAll('.foo');

  // good
  const nodes = Array.from(foo);

  // best
  const nodes = [...foo];
  ```

- 4.5 배열과 유사한 객체를 배열로 변환하려면 `Array.from`을 사용하자.

  ```
  const arrLike = { 0: 'foo', 1: 'bar', 2: 'baz', length: 3 };

  // bad
  const arr = Array.prototype.slice.call(arrLike);

  // good
  const arr = Array.from(arrLike);
  ```

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
