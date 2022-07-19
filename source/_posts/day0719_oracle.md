---
title: "Day-19 Oracle Basic"
categories:
- Oracle
- lecture
output:
 html_document:
   keep_md: true
date: '2022-07-19'
---

# day0719

- SQL vs PL/SQL
- SQL (분석가90% + 개발자 30%)
    - 프로그래밍 성격이 얕다
- PL/SQL (분석가10% + 개발자70% +DBA)
- DB분석

```python
SELECT 컬럼명
FROM 테이블명
WHERE 조건식
ORDER BY 정렬기준
```

- 사용자 설정 제약조건 확인

```python
SELECT constraint_name
       , constraint_type
       , table_name
       , search_condition
FROM user_constraints
WHERE table_name = 'EX2_6';
```

![Untitled](/images/day07/day0719/oracle1.png)
- 테이블 정보 확인

```python
DESC 컬럼명;
```

![Untitled](/images/day07/day0719/oracle2.png)

### 제약조건

- NOT NULL  :  결측치 허용 X
- UNIQUE  : 중복값 허용 X
- Primary Key
    - 기본키
    - UNIQUE, NOT NULL
    - 테이블당 1개의 기본키만 가능
- 외래키
    - 테이블간의 참조 데이터 무결성 위한 제약 조건
    - 참조 무결성을 보장한다 -> 잘못된 정보가 입력되는 것을 방지
- Check
    - 컬럼에 입력되는 데이터를 체크해 특정 조건에 맞는 데이터만 입력
- Default
    - 값을 넣지 않아도 자동으로 입력

### 테이블 변경

- 컬럼명 변경

```python
ALTER TABLE 테이블명 RENAME COLUMN 바꾸고싶은 컬럼명 TO 변경후 컬럼명;
```

- 타입변경

```python
ALTER TABLE 테이블명 MODIFY 컬럼명 타입;
```

- 컬럼 추가

```python
ALTER TABLE 테이블명 ADD 컬럼명 타입;
```

- 컬럼 삭제

```python
ALTER TABLE 테이블명 DROP COLUMN COL3;
```

- 제약조건 추가하기

```python
ALTER TABLE 테이블명 ADD CONSTRAINTS 제약조건이름 PRIMARY KEY (컬럼명);
```

- 제약조건 삭제

```python
ALTER TABLE 테이블 명 DROP CONSTRAINTS 제약조건이름;
```

- 테이블 복사

```python
CREATE TABLE 테이블명 AS
SELECT * FROM 복사당할 테이블명;
```

### 뷰

- 테이블이나 또다른 뷰를 참조하는 객체
- 뷰생성

```python
CREATE OR REPLACE VIEW 테이블명 AS
SELECT 컬럼명
FROM 테이블명
WHERE 조건식
```

- 뷰 삭제

```python
DROP VIEW 테이블명
```