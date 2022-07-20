---
title: "Day-19 SQL Developer"
categories:
- Development Settings
output:
 html_document:
   keep_md: true
date: '2022-07-19'
---


# SQL Developer

- 참조 : [https://dschloe.github.io/sql/oracle_basic_settings/](https://dschloe.github.io/sql/oracle_basic_settings/)
- sqlplus에서 system으로 로그인

![Untitled](/images/day07/sql_devel/Untitled.png)

- C:\oracle\oradata\파일이름\myts.dbf

```sql
CREATE TABLESPACE myts DATAFILE 'C:\oracle\oradata\ORCL\myts.dbf' SIZE 100M AUTOEXTEND ON NEXT 5M;
```

![Untitled](/images/day07/sql_devel/Untitled%201.png)

- 사용자 생성
- ora_user라는 이름으로 사용자설정비번을 가진다


- 유저에게 권한주기
    - DBA권한 부여
        - DBA : 관리자권한

![Untitled](/images/day07/sql_devel/Untitled%203.png)

- 유저로 로그인하기
    - connect ID/PASSWORD
- 현재 사용자명 확인
- sqpdeveloper 실행 후 ‘수동으로 접속 생성’ 클릭

![Untitled](/images/day07/sql_devel/Untitled%204.png)

- SID를 처음 설치 이름인 orcl로 바꾸고

![Untitled](/images/day07/sql_devel/Untitled%205.png)

### 샘플 스키마 설치

- C 드라이브 - oracle - backup 폴더를 생성해 내려 받은 파일을 위치시킨다.

![Untitled](/images/day07/sql_devel/Untitled%206.png)

- cmd를 연다
- 방금 만든 oracle의 backup폴더로 들어간다

![Untitled](/images/day07/sql_devel/Untitled%207.png)

![Untitled](/images/day07/sql_devel/Untitled%208.png)

- 파일 가져오기

```sql
imp ora_user/evan file=expall.dmp log=empall.log ignore=y grants=y rows=y indexes=y full=y
```



```sql
imp ora_user/evan file=expcust.dmp log=expcust.log ignore=y grants=y rows=y indexes=y full=y
```



## VSCode와 Oracle 연동하기

- 참조  :  [https://dschloe.github.io/sql/vscode_oracle/](https://dschloe.github.io/sql/vscode_oracle/)