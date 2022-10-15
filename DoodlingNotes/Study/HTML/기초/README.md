## HTML

---

### HTML은 왜 중요한가?

- 웹페이지에 보이는 모든 것들은 HTML을 통해 표현되기 때문에 중요
- 웹페이지를 통해 전달하고자는 모든 정보를 가지고 있는 정보 콘텐츠의 집합체
- 문서의 구조와 정보 위계가 명확하게 보이는 HTML 코드를 작성
- Semantic Markup, 검색 엔진 최적화, SEO(Search Engine Optimization)

--- 

### HTML을 시멘틱하게 작성해야 하는 이유

- 브라우저가 제대로 정보의 위계질서를 파악하여 검색 엔진 최적화, SEO
- HTML은 웹개발의 기초 기반 본질

---

### 제목과 문단, Heading & Paragraph

```
    <h1></h1>, <h2></h2>, <h3></h3>, <h4></h4>, <h5></h5>, <h6></h6> 제목
    <p></p> 문단
```

---

### 강조, Emphasis

```
    <em>text</em>, <strong>text</strong>
    두 태그의 차이는 따로 없음
    사용하고 싶은 태그를 사용하면 된다.
    같은 태그안에 있는 텍스트중 강조하고 싶은 부분에 사용하고, 브라우저는 해당 부분을 중요하게 인식한다.
```

---

### 링크, Anchor

```
    <a href="">link</a>
    현 위치에서 다른 위치로 이동해야할 때 사용
    href 속성 필수(hypertext reference)

    href 속성의 여러 사용방법
        1. 웹 URL(전체, 상대경로)
        2. href="#id 속성값", 이동하고 싶은 태그에 id 속성값 부여
        3. href="mailto:email@example.com", 메일로 연결
        4. href="tel:010-1234-5678", 모바일에서 통화로 연결

    target 속성
        target="_blank"
        링크를 누를 때, 새탭을 열어서 연결하고 싶은 경우에 사용
```

---

### 이미지, image

```
    <img src="#" alt="" />

    src 속성에는 이미지의 상대경로, 혹은 이미지 경로를 넣어줌
    alt 속성은 alternative text, 대체 텍스트라는 의미
        - 이미지를 불러오지 못했을 때, 정상적인 경우 어떤 이미지가 보여지는 지 설명을 적는 곳
        - 스크린 리더(시각 장애인들이 웹페이지를 볼 때 사용)에서도 사용됨
```

---

### 목록, lists

```
    <ol>
        <li></li>
    </ol>,
    <ul>
        <li></li>
    </ul>

    ol, 순서가 중요한 목록(ordered list)

    ul, 순서가 중요하지 않은 목록(unordered list)

    li, 목록 내 항목을 나타낼 때 사용(list)

    ol, ul 태그 안에서는 li 태그만 자식요소로 가질 수 있다.
    li 태그 내에서는 다른 태그를 사용해도 무관함
    ol, ul 태그 안에서 li 이외 다른 태그를 사용 시, 표준에 어긋남
```

---

### 정의 목록, Description List

```
    <dl>
        <dt></dt>
        <dt>
            <dfn></dfn>
        </dt>
        <dd></dd>
    </dl>

    dl(description list)
        1. 용어를 정의할 때 사용
        2. key-value로 정보를 제공할 때 사용
        * dl 태그의 자식요소로는 div, dt, dd만 올 수 있음
    
    dt(description term)
        - key-value로 정보를 제공할 때, key에 해당, 용어
        - 사전적인 의미를 좀 더 구체적으로 정의 내리고 싶을 때에는 dfn 태그를 dt 태그안에 사용
    
    dd(description data)
        - key-value로 정보를 제공할 때, value에 해당

    dfn(definition)
        - 정의를 하겠다는 의미의 태그
```

---

### 인용, Quotations

```
    <blockquote cite="출처 url">
        인용내용
        <cite>출처</cite>
    </blockquote>,
    <q></q>

    blockquote 태그와 p태그와 차이점은 들여쓰기(indent)
    blockquote 태그는 브라우저가 인용문임을 인지할 수 있음

    cite 속성을 통해 출처의 url, cite 태그를 통해 출처를 밝힐 수 있다.

    q 태그는 문단 안에서 일부 인용문을 사용할 때 사용한다.
    q 태그를 사용 시 쌍따옴표가 생긴다.
    q 태그보다는 blockquote를 대체로 많이 사용한다.
```

---

### 아무런 의미가 없는 태그, Div & Span

```
    <div></div>, <span></span>

    스타일링 시, 요소를 묶어야할 때 사용한다.
```

---

### Form(1) - 기본 구조

```
    <form action="API 주소" method="method 타입"></form>

    form 태그는 사용자로부터 정보를 받고싶을 때 사용
    method 타입은 GET과 POST, 둘 중 하나를 선택할 수 있음
```

### Form(2) - input, 입력창

```
    <input type=""></input>
    
    type에 따라 input 태그의 형태가 정해진다.
    type="text", type="email", type="password", type="number", type="file"

    type에 상관없이 input 태그에서 공통적으로 사용하는 속성
    placeholder, maxlength, minlength, required, disabled

    <input type="text" minlength="5" maxlength="13" required disabled value="기본 값"/>

    placeholder: 값이 아무것도 없을 때 보여줄 도움 텍스트
    maxlength: 값의 최대 길이를 제한
    minlength: 값의 최소 길이를 제한
    required: 필수 입력을 강제함
    disabled: 해당 input 태그 비활성화
    value: 기본 값
```

```
    <input type="email" placeholder="이메일을 입력하세요." />
    type="email"을 사용 시, @가 들어가 있는 이메일 형식이 아닌 경우 경고
```

```
    <input type="password" placeholder="비밀번호를 입력하세요." />
    텍스트가 노출되지 않고 *로 치환되어 표시
```

```
    <input type="number" placeholder="나이를 입력하세요.(12세 이상 123세 이하" min="12" max="123"/>
    숫자를 제외한 나머지는 입력 불가
    min, max는 최소최대값을 강제함
```

```
    <input type="file" accept=".png, .jpg" />
    accept: 파일첨부를 허용할 확장자 명시
```

### Form(3) - Label

```
    <label for="인풋 id">라벨</label>
    <input id="인풋 id" type="text /> 
    
    label 태그는 form 양식에 이름을 붙이는 태그
    for 속성값과 label 태그를 이용해 이름을 붙일 태그의 id값은 일치해야한다.

    label 태그 사용 시 얻을 수 있는 효용으로는 label을 클릭한 경우 연결된 input으로 포커스가 잡힌다.
```

### Form(4) - Radio & Checkbox

```
    <input type="radio" name="subscription" id="subscribe" value="subscribe" />
    <label for="subscribe">구독</label>
    <input type="radio" name="subscription" id="unsubscribe" value="unsubscribe" />
    <label for="unsubscribe">미구독</label>

    type="radio"의 name 속성은 그룹핑 역할을 함
    동일한 name 속성을 가진 경우에 그룹으로 묶어지며, 같은 name 속성을 가진 라디오 버튼은 선택이 1개만 가능하다.   
    value 속성을 설정해야 서버로 전송 시 파라미터로 name=value 형태로 전달된다.
```

```
    <input type="checkbox" name="skills" value="html" id="html" />
    <label for="html">HTML</label>
    <input type="checkbox" name="skills" value="css" id="css" />
    <label for="css">CSS</label>
    <input type="checkbox" name="skills" value="js" id="js" />
    <label for="js">JavaScript</label>

    type="checkbox"의 name, value 속성은 type="radio"와 동일한 개념으로 사용하지만 한 그룹에서 여러 항목을 선택할 수 있다.
    서버에 전달 시, name=value1&name=value2와 같은 형태로 전달된다.
```

### Form(5) - Select & Option

```
    <select name="skill" id="" >
        <option value="html" >HTML</option>
        <option value="css" >CSS</option>
        <option value="js" >JavaScript</option>
    </select>

    select 태그 내에 목록을 생성하기 위해서는 option 태그를 사용한다.
    select 태그의 name 속성은 option 태그의 value 속성과 name=value 형태로 묶여 서버에 전달된다.

    multiple 속성을 부여하는 경우 여러개를 선택할 수 있다.
```

### Form(6) - Textarea

```
    <textarea rows="40" cols="50" ></textarea>

    여러줄에 걸쳐서 많은 양의 글을 받을 때 사용한다.
    input 태그는 여러줄의 글을 받아들일 수 없다.

    rows: 줄
    cols: 칸
    rows나 cols는 css로도 조정이 가능하니 굳이 쓰지 않아도 된다.

    label 태그 붙일 수 있음
    placeholder, disabled 속성 사용가능
```

### Form(7) - Button

```
    <button type="">버튼이름</button>

    button 태그의 경우 type을 반드시 명시해야한다.
    
    type="button"
        그저 버튼

    type="submit"
        버튼이 form을 제출하는데 사용될 때 사용

    type="reset"
        버튼이 form을 리셋하는데 사용될 때 사용
        실무에서 사용할 일이 있는지는 모르겠다.
```

---

### Table

```
    <table>
        <thead>
            <tr>
                <th>ID</th>
                <th>이름</th>
                <th>개발분야</th>
                <th>기타</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>00001</td>
                <td>김아무개</td>
                <td>풀스택</td>
                <td></td>
            </tr>
            <tr>
                <td>00002</td>
                <td>서아무개</td>
                <td>프론트엔드</td>
                <td></td>
            </tr>
        </tbody>
    </table>

    table 태그는 데이터를 담은 표를 만들 때 사용한다.
    thead, tbody는 사용하지 않아도 되지만 사용하면 브라우저에 명시적으로 전달하고 작성하는 입장에서도 보기 편해진다.
    tr 태그는 테이블 행을 만들 때 사용한다.
    th 태그는 테이블 열의 카테고리를 의미한다.(테이블 헤더)
    td 태그는 카테고리에 해당하는 값을 의미한다.(테이블 데이터)
```

```
    rowspan, colspan 속성을 통해 테이블 셀을 병합할 수 있다.
    rowspan: 값만큼 행을 병합하여 영역을 차지한다.
    colspan: 값만큼 열을 병합하여 영역을 차지한다.

    scope 속성은 th 태그에만 사용할 수 있는 속성이다.
    scope 속성은 "row" 또는 "col" 값을 설정할 수 있는데, 이는  가로줄의 헤더인지 세로줄의 헤더인지 브라우저에게 알려주는 역할을 한다. 
```

---

### Media, 미디어 파일

```
    <audio src="파일경로/파일이름.확장자" controls></audio>
    <audio src="파일경로/파일이름.확장자" loop autoplay></audio>
    
    audio 태그에서 src 속성은 필수이다.(태그로 사용하는 방법도 있음)
    controls 속성이 있어야만 audio 컨트롤러가 생성된다. controls 속성이 없는 경우 아무것도 생성되지 않는다.
    하지만 페이지에 들어가자마자 재생을 시키고 싶은 경우, autoplay 속성을 명시하면 페이지 로드와 동시에 audio 파일이 재생된다.
    loop 속성을 명시하는 경우 무한 반복실행한다.


    <audio>
        <source src="파일경로/파일이름.wav" type="audio/wav" />
        <source src="파일경로/파일이름.mp4" type="audio/mpeg" />
        <source src="파일경로/파일이름.ogg" type="audio/ogg" />
    </audio>
    
    audio 태그에서 src 속성을 사용하는 대신 source 태그를 사용할 수 있다.
    type 속성값은 본인이 필요한 파일타입을 검색을 통해 찾아서 명시한다.

    audio 태그에서 src 속성을 직접 쓰는 방식은 유저에게 1가지 소스만 제공할 수 있지만 source 태그를 사용한 방식의 차이는 여러가지 소스를 유저에게 제공할 수 있을 때 사용한다.
```

```
    <video src="상대경로 혹은 절대경로/파일이름.확장자" controls></video>

    video 태그의 기본적인 사용방법은 audio 태그와 동일하다.
    autoplay, loop 속성 사용가능

    <video>
        <source src="파일경로/파일이름.mov" type="video/mp4" />
        <source src="파일경로/파일이름.ogg" type="video/ogg" />
        <source src="파일경로/파일이름.mp4" type="video/mp4" />
    </video>
```

```
    iframe 태그는 정의상으로는 HTML에 다른 HTML을 Embed 하고싶은 경우 사용한다.
    
    iframe 태그는 통상 유튜브에서 share를 선택하고 embed 기능을 사용하였을 때 처럼 동영상을 가져와서 심는 경우 등에 많이 사용한다.
```

---

### 기타 태그

```
    <abbr title="풀네임">약어</abbr>
    <p>
        너... 혹시 <abbr title="Attention Deficit Hyperactivity Disorder">ADHD</abbr>니?
    </p>

    abbr 태그는 약자, 약어를 나타낼 때 사용한다.(abbreviation)
```

```
    <address>연릭처</address>
    address 태그는 연락처에 관한 정보를 마크업할 때 사용한다.

    address 태그안에서 주로 사용하는 정보
        1. (물리적)주소
        2. URL
        3. email 주소
        4. 전화번호
        5. SNS
```

```
    <pre></pre>
    <code></code>

    pre 태그와 code 태그를 동일하게 생각하는 경우가 많은데 조금 다르다.

    pre 태그는 텍스트를 입력한대로 보여준다. p 태그의 경우에는 줄바꿈 등이 바로 적용되어 나오지 않지만 pre 태그는 들여쓰기나 엔터 등이 바로 적용된다.(preformatted text)

    code 태그는 코드를 작성할 때 사용한다.

    pre 태그와 code 태그가 같이 다닐 필요는 없지만, 들여쓰기 엔터 등이 바로 적용되도록 코드를 작성하고 싶다면 다음과 같이 작성한다.

    <pre>
        <code>
            function sumWithArray(array) {
                return array.reduce((a, c) => a + c);
            }
        </code>
    </pre>
```

---

### Doctype & Document Structure

```
    HTML에도 기본 규격이라는게 존재한다.
    HTML을 작성할 때 가장 먼저해야하는게 Doctype을 선언하는 것이다.

    <!DOCTYPE html>
        - 이 문서는 HTML5버전으로 작성된 문서임을 브라우저에게 알리는 역할(가장 최신의 표준에 맞추어 작성된 문서니까 오류없이 잘 렌더링 해달라고 브라우저에게 알림)
```

```
    <html>
        <head>
        </head>
        <body>
            <h1>제목</h1>
            <p>문단</p>
        </body>
    </html>

    html 태그안에는 head 태그와 body 태그 두개만 자식요소로 사용할 수 있다.
```

---

### Title, Link, Style & Script

```
    <!DOCTYPE html>
    <html lang="en">
        <head>
            <meta charset="UTF-8" />
            <title>HTML 제목</title>
            <link rel="stylesheet" href="style.css">
        </head>
        <body>
        </body>
    </html>
```

```
    title 태그는 html 문서에 보여지는 대제목을 입력하는데 사용한다.
    필수적으로 사용되는 태그, 검색 최적화에 매우 중요

    검색 최적화를 위해 title 태그를 잘 쓰는 방법
        1. 키워드 단순 나열은 비추천
        2. 문서에서 보여줄 내용에 따라서 그에 알맞게 변경
        3. 무엇에 관한 내용인지 단어보단 약간 길이가 있게 작성하지만 또, 센스있게 함축적으로 적는다.
```

```
    link 태그는 보통은 CSS 스타일 시트를 HTML에 추가할 때 사용한다.
    font, icon 등 cdn 사용 시에도 많이 사용됨
```

```
    style 태그는 HTML 문서 내에 CSS 코드를 작성할 때 사용한다.
    비추천
```

```
    script 태그는 HTML 문서 내에 JavaScript 파일을 첨부할 때 사용한다.
    또, 직접 body 태그안에서 script 태그를 사용해서 문서 내에서 바로 작성 및 적용할 수 있다.

    script 태그는 head 안에 넣지않고 body 태그안에 넣는 이유는 link 태그 등은 로드가 제대로 되지 않더라도 건너뛰고 진행하지만, script 태그는 건너뛰지 않고 멈추기 때문에 body 태그 제일 하단에 위치시켜 모든 컨텐츠가 로딩된 후 script를 가져오도록 하는 것이 좋다. 
```

---

### Meta, 메타데이터

```
    <meta name="메타데이터 종류" content="메타데이터 값">

    meta 태그에는 head 태그 내에서 사용하는 다른 태그들에서 가질 수 없는 정보들을 표시하는데 사용한다. meta 태그에는 name 속성과 content 속성이 필수다.

    meta 태그에서 가장 중요한 요소는 name="viewport"이다.
    
    viewport는 반응형 웹과 관련이 있다. name="viewport" 속성을 가진 meta 태그가 없다면 반응형 웹을 만들 수 없다. 
    디바이스 사이즈에 따라서 반응하여 사이즈를 변경할 수 있는 반응형 웹을 만드는데 필수요소이다.

    <meta name="viewport" content="width=device-width, initial-scale=1.0">
```

```
    <meta name="author" content="아무개">
    작성자를 명시하는 meta 태그의 name="author" 속성이다.
```

```
    <meta name="keywords" content="키워드1, 키워드2, ...">
    웹페이지의 콘텐츠 키워드를 적는다.
    검색최적화에 도움
```

```
    <meta name="description" content="설명내용">
    웹페이지에 대한 설명을 적는다.
```