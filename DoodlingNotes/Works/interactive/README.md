# 회사에서 프로젝트 처음으로 혼자서 처음부터 끝까지(feat.interactive)

회사에서 특정 프로젝트의 일부를 구현하는데 있어, DB 설계부터 Front-end까지 다 해볼 수 있는 기회를 주셨다. 많이 성장할 수 있을 것이라 판단되어 기록해보고자 한다.

<br />

---

> 요구사항 정리

### <strong>ToDo</strong>

- 관리자 로그인, 로그아웃, 패스워드 변경 기능
- 게시판(댓글, 대댓글)
- 위 기능에 필요한 데이터베이스 구축, Back-end 개발, Front-end 개발

<br />

### <strong>Requirements</strong>

- session을 사용한 로그인 기능 구현
- 패스워드 암호화 전송, 단방향 암호화 알고리즘 사용(SHA-256 -> Bcrypt)
- 게시판, 댓글, 대댓글의 익명성
- Sequence 필수
- 게시판 데이터베이스와 댓글 & 대댓글 데이터베이스의 분리
- 게시판 및 댓글 대댓글 작성시간은 timestamp로 관리

<br />

---

가장 먼저 해야할 일은 데이터베이스 설계이다.

데이터베이스 설계 순서

1. 요구 분석
1. 개념적 설계
1. 논리적 설계
1. 물리적 설계
1. 구현

<br />

### <strong>개념적 설계(정보 모델링, 개념화)</strong>

- 정보의 구조를 얻기 위해 현실 게계의 무한성과 계속성을 이해하고, 다른 사람과 통신하기 위해 현실 세계에 대한 인식을 추상적 개념으로 표현
- 스키마 모델링과 트랜잭션 모델링 병행
- 요구 분석 단계에서 나온 결과(요구 조건 명세)를 DBMS에 독립적인 E-R 다이어그램(r개체 관계도)으로 작성
- DBMS에 독립적인 개념 스키마를 설계.

<br />

### <strong>논리적 설계(데이터 모델링)</strong>

- 현실 세계의 자료를 컴퓨터가 처리할 수 있는 물리적 저장장치에 저장할 수 있도록 변환하기 위해 특정 DBMS가 지원하는 논리적 자료 구조로 변환
- 개념 세계의 데이터를 필드로 기술된 데이터 타입과 이 데이터 타입들 간의 관계로 표현되는 논리적 구조의 데이터로 모델화
- 개념적 설계 = 개념 스키마 설계
- 논리적 설계 = 개념 스키마 평가, 정제 그리고 특정 DBMS에 종속적인 논리적 스키마 설계
- 트랜잭션의 인터페이스를 설계
- 관계형 데이터베이스라면 테이블을 설계하는 단계

<br />

### <strong>물리적 설계(데이터 구조화)</strong>

- 논리적 설계 단계에서 논리적 구조로 표현된 데이터를 디스크 등의 물리적 저장장치에 저장할 수 있는 물리적 구조의 데이터베이스로 변환
- 데이터베이스 파일의 저장 구조, 레코드의 형식, 접근 경로
  트랜잭션 작성
- 물리적 설계 옵션 선택 시 고려사항
  : 반응 시간(Response Time), 공간 활용도(Space Utilization), 트랜잭션 처리량(Transaction Throughput)

<br />

> Notes: 해야되는게 굉장히 많다. 실제로 설계가 잘못되면 문제가 커진다. 하지만 나에게 주어진 시간은 많지 않다. 주의해야될 내용들을 숙지한 상태로 다음 단계를 진행해보자.

<br />

---

### 데이터베이스 설계 시 필요한 정보

- 로그인 관련 데이터베이스에서 필요한 정보
  - idx: 관리자 계정 인덱스 // integer, sequence auto increment
  - id: 관리자 아이디 // character varying
  - passwd: 관리자 패스워드 // character varying
  - connected_ip: 접속 IP // character varying

<br />

- 익명 게시판 관련 데이터베이스에서 필요한 정보
  - idx: 게시글 인덱스 // integer, sequence auto increment
  - writer: 익명의 작성자 // character varying
  - title: 게시글 제목 // character varying
  - content: 게시글 내용 // text
  - created_date: 작성된 날짜시간 // timestamp with timezone
  - updated_date: 업데이트된 날짜시간 // timestamp with timezone
  - passwd: 글의 수정, 삭제 시 필요 // character varying

<br />

- 익명 댓글 대댓글 관련 데이터베이스에서 필요한 정보
  - idx: 댓글 인덱스 // integer, sequence auto increment
  - writer: 익명의 작성자(무작위 문자열) // character varying
  - content: 댓글 내용 // text
  - post_num: 게시글 idx // integer
  - level: 댓글과 대댓글을 구분 // integer
  - order: 댓글과 대댓글 순서 구분 // integer
  - group_num: 댓글 그룹구분에 사용되며 댓글 인덱스를 부여, 대댓글의 경우 자신 대신 부모의 인덱스를 저장 => 특정 댓글에 종속되어있는 것을 표시 // integer
  - created_date: 작성된 날짜시간 // timestamp with timezone
  - updated_date: 업데이트된 날짜시간 // timestamp with timezone
  - passwd: 글의 수정, 삭제 시 필요 // character varying
