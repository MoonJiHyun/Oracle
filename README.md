# Oracle

#### (1) Table

특정한 종류의 데이터를 구조적 목록으로 묶은 것

데이터를 종류별로 구분하는 단위

행 (=row, =record) / 열(=컬럼, =속성) 



>  ERD (Entity Relationship Diagram)



#### (2) Data Type

CHAR(n) : n 크기 고정 문자

VARCHAR(n) : n 크기 가변 문자

NUMBER(n) : 숫자 타입

DATE : 날짜 + 시간



#### (3) SQL (Structed Query Language)

- 구조적 질의 언어
- 데이터베이스와의 통신을 위한 언어
- 데이터 조회, 정의, 조적을 위한 언어



#### (4) DML (Data Manipulation Langauge)

- 데이터 조작 언어
- 데이터를 조회하거나 검색, 등록, 수정, 삭제



#### (5) DDL (Data Definition Language)

- 데이터 정의 언어
- 테이블 생성, 수정, 변경, 삭제



#### (6) DCL (Data Control Language)

- 데이터베이스 접근 권한 제어 언어



#### (7) TCL (Transaction Control Language)

- 트랜잭션 (논리적 작업단위) 제어를 위한 언어



#### (8) 함수

NVL(bonus, 0) : bonus가 0이면 null

DECODE(컬럼명, 조건값, 조건과 같은 경우, 조건과 다른 경우)

COUNT, SUM, AVG, MAX, MIN, VARIANCE(분산), STDDEV(표준편차)



#### (9) 조인

| CROSS JOIN                         | 가능한 모든 행 조인                       |
| ---------------------------------- | ----------------------------------------- |
| EQUI JOIN                          | 조건이 일치하는 결과                      |
| NON-EQUI JOIN                      | 조건이 일치하지 않는 결과                 |
| OUTER JOIN (LEFT JOIN, RIGHT JOIN) | 양쪽 테이블의 한쪽만 조건이 일치해도 출력 |
| SELF JOIN                          | 자체 테이블에서 조인                      |



#### (10) 서브쿼리

- 단일 행 서브쿼리(=, !=, >, >=, <, <=)
- 다중 행 서브쿼리(ANY, ALL, IN, NOT IN)
- 스칼라 서브쿼리 : 컬럼 자리에 서브쿼리가 들어가는 경우

```sql
SELECT ename, depths, (SELECT dname FROM dept WHERE deptno=emp.deptno) dname
FROM emp; -- 스칼라 서브쿼리 --
```

- inline view 서브쿼리 : FROM 절 뒤에 들어가는 서브쿼리

```sql
SELECT ename, e.deptno, e.salary, v.salary
FROM emp e JOIN
	(SELECT deptno, AVG(salary) salary FROM emp GROUP BY deptno) v
ON e.deptno = v.deptno;
```



> 사용자 계정 생성
> 롤 : CONNEXT, RESOURCE



#### (11) 데이터 모델링

- 현실 세계에서 일어나는 사건들을 데이터화하는 과정
- 실제 현실은 너무 복잡하므로 개념화(추상화)하여 단순하게 표현
- 모델링을 하기 위해서는 고객과의 의사소통을 통해 고객 업무 프로세스 이해
- 업무 프로세스를 추상화하고 분석/설계하면서 점점 상세하게 설계
- 업무 프로세스를 이해하고, 규칙을 정의해서 데이터 모델로 표현
- 추상화, 단순화, 명확화 

- 개념적 모델링 -> 논리적 모델링 -> 물리적 모델링

- 개념적 모델링

  - 현실 세계에서 일어나는 사건들을 데이터 관점으로 표현
  - 개념적 모델링의 산출물인 개념적 ERD를 만드는 과정
  - 복잡하지 않고, 중요한 부분 위주로 모델링
  - 엔티티와 속성 도출

- 논리적 모델링

  - 개념적 모델링을 논리적 모델링으로 변환
  - 식별자 도출, 필요한 릴레이션 정의
  - 정규화 수행


#### (12) 엔티티 (Entity)

- 업무에서 관리해야 하는 데이터 집합의 의미
- 저장되고 관리되어야 하는 데이터
- 엔티티는 개념, 사건, 장소 등의 명사
- ex. 부서, 사원
- 유일한 식별자, 2개 이상의 인스턴스, 반드시 속성, 다른 엔티티와 최소 한 개 이상의 관계, 업무에서 관리되어야 하는 집합



#### (13) 속성 (Attribute)

- 데이터의 가장 작은 논리적 단위
- 하나의 엔티티는 한 개 이상의 속성으로 구성
- 엔티티의 특성, 상태 등을 기술
- 엔티티가 가지는 항목 (테이블의 컬럼)
- ex. 부서 엔티티의 속성 : 부서 번호, 부서명
- 분해여부 : 단일 속성, 복합 속성(주소, 시/군/구), 다중값 속성 (취미)
- 특성 : 기본 속성, 설계 속성(데이터 모델링 과정에서 발생되는 속성), 파생 속성 (합계, 평균 등)



#### (14) 관계

- 엔티티 간 관련성
- 존재 관계 : 엔티티 간 상태 (사원 - 부서)
- 행위 관계 : 엔티티 간의 어떤 행위가 있는 것 (고객 - 주문)
- 관계 차수 : 두 개의 엔티티 간의 관계에 참여하는 수



> 01 : 0 또는 1
> 1< : 1 이상
> 0< : 0 이상



#### (15) 식별 관계

- 엔티티의 기본키를 다른 엔티티의 기본키의 하나로 공유하는 것
- 고객과 계좌 엔티티에서 고객은 독립적으로 존재할 수 있는 강한 개체
- 강한 개체는 다른 엔티티에 의존하지 않고 독립적으로 존재 가능, 다른 엔티티와 관계를 가질 때 다른 엔티티에게 기본키를 공유



#### (16) 비식별 관계

- 강한 개체의 기본키를 다른 엔티티의 기본키가 아닌 일반 컬럼으로 관계를 가짐
- 점선으로 표현



#### (17) 식별자

- 엔티티 내에서 인스턴스를 구분할 수 있는 구분자
- 엔티티를 대표할 수 있는 유일성을 만족하는 속성



#### (18) 주식별자 (PK)

- 유일성과 최소성을 만족하는 키
- 엔티티를 대표할 수 있어야 함
- 엔티티의 인스턴스를 유일하게 식별



#### (19) 외래식별자 (FK)

- 관계가 있는 두 엔티티를 부모, 자식 엔티티로 구분
- 부모 엔티티의 주식별자 속성을 자식 엔티티의 속성으로 추가



#### (20) 물리적 모델링

- 데이터베이스를 선정하여 ERD 요소들을 실제 데이터베이스의 요소들로 변환

| 논리적 모델링 | 물리적 모델링 |
| ------------- | ------------- |
| 엔티티        | 테이블        |
| 속성          | 컬럼          |
| 주식별자      | 기본키        |
| 외래식별자    | 외래키        |
| 관계          | 관계          |



#### (21) SQL

```sql
CREATE TABLE emp_ex (
	empno number(5),
	ename varchar2(10)
);

ALTER TABLE emp_ex ADD (birthday date);
ALTER TABLE emp_ex MODIFY ename varchar2(20);
ALTER TABLE emp_ex DROP COLUMN birthday;
ALTER TABLE emp_ex RENAME TO emp_ex2;
RENAME emp_ex TO emp_ex2;

TRUNCATE TABLE emp_ex;
DROP TABLE emp_ex;
```



#### (22) commit

트랜잭션(작업 단위)를 정상적으로 데이터베이스에 적용

작업(INSERT, UPDATE, DELETE) 내용을 DB에 저장



#### (23) rollback

작업 중 문제 발생 시 현재 트랜잭션의 변경 내역을 취소하고, 종료 트랜잭션 발생 이전 시점으로 되돌림

작업(INSERT, UPDATE, DELETE) 내용을 취소



#### (24) 시퀀스

```sql
CREATE SEQUENCE emp_ex_seq
	START WITH 1
	INCREMENT BY 1
	MINVALUE 1
	MAXVALUE 99999;

SELECT 시퀀스명.CURRVAL FROM dual; -- 초기 1회 NEXTVAL 실행 후 사용 가능

SELECT 시퀀스명.NEXTVAL FROM dual;

INSERT INTO emp_ex (empno, ename, salary)
VALUES (emp_ex_seq.nextval, '유관순', 300);
```



#### (25) 뷰

- 실제로 존재하지 않는 논리적인 가상 테이블
- 뷰를 사용하는 이유
  - 복잡한 SELECT 문을 자주 사용해야 하는 경우
  - 조회속도를 높이기 위해

```sql
GRANT create view TO testuser; -- 뷰 생성 권한 추가

CREATE VIEW emp_view
AS
SELECT * FROM emp WHERE job = '사원';

DROP VIEW emp_view;
```



#### (26) 데이터 무결성

- 무결성 == 정확성 유지

- 데이터 무결성 제약 조건
  - 테이블에 부적절한 데이터가 입력되는 것을 방지하기 위해 테이블을 생성할 때, 각 컬럼에 적용하는 규칙

| NOT NULL    |                              |
| ----------- | ---------------------------- |
| UNIQUE      |                              |
| PRIMARY KEY | NOT NULL + UNIQUE            |
| FOREIGN KEY |                              |
| CHECK       | 데이터 값의 범위나 조건 지정 |
| DEFAULT     |                              |



```sql
ALTER TABLE dept MODIFY deptno number(2) PRIMARY KEY;
```



#### (27) 사용자 관리

Oracle DBMS에 접속할 수 있는 사용자 계정 추가

```sql
CREATE USER 사용자명 IDENTIFIED BY 비밀번호;
```



#### (28) 사용자 권한

- 사용자 생성 후 새로운 접속 시도 시 접속 안됨
- 사용자만 생성되고 접속 권한이 없기 때문

| 권한             | 설명                     |
| ---------------- | ------------------------ |
| CREATE USER      | 사용자 생성 권한         |
| DROP USER        | 사용자 삭제 권한         |
| CREATE SESSION   | 데이터베이스 접속 권한   |
| CREATE TABLE     | 테이블 생성 권한         |
| CREATE VIEW      | 뷰 생성 권한             |
| CREATE SEQUENCE  | 시퀀스 생성 권한         |
| CREATE PROCEDURE | 프로시저, 함수 생성 권한 |



```sql
GRANT 권한
TO 사용자명
[WITH ADMIN OPTION]; -- 해당 권한을 다른 사용자에게도 부여할 수 있는 권한을 함께 부여

GRANT create session
TO c##testuser2;

-- 객체별로 DML 사용할 수 있는 권한 부여
GRANT 권한
ON 객체명
TO 사용자;

-- create session 권한 부여를 했지만 데이터 조회는 불가한 상태 (객체 권한 미부여 상태)
-- 객체별로 DML 사용할 수 있는 권한 부여

GRANT select -- 여러개 동시에 지정 가능
ON testuser.dept
TO c##testuser2;
```



#### (29) 스키마

- 스키마란 객체를 소유한 사용자명
- 객체 앞에 사용자명 기술
- 자신 소유의 객체는 생략 가능하지만, 자신 소유가 아닌 객체를 사용하는 경우 반드시 스키마 지정 필요



#### (30) 사용자 권한 회수

```sql
REVOKE select
ON testuser.dept
FROM c##testuser2;
```



#### (31) 롤 (ROLE)

- 오라클에서 여러 권한을 묶어 놓은 것

- 롤을 하나의 그룹으로 묶어, 사용자에게 해당 롤에 대한 권한을 부여

- 사전 정의된 롤

  | CONNECT  | DB 접속에 관련된 권한                                  | CREATE SESSION, CREATE TABLE, CREATE VIEW   |
  | -------- | ------------------------------------------------------ | ------------------------------------------- |
  | RESOURCE | 객체(테이블, 뷰, 인덱스)를 생성할 수 있는 권한         | CREATE TABLE, CREATE VIEW, CREATE PROCEDURE |
  | DBA      | 데이터베이스 객체를 관리하고, 사용자 관리 등 모든 권한 | 데이터베이스 관리자 권한                    |

  ```sql
  -- c##testuser2 사용자에게 CONNECT, RESOURCE 롤 권한 부여
  GRANT connect, resource TO c##testuser2;
  
  -- c##testuser2 부여받은 롤 권한 확인
  SELECT * FROM user_role_privs;
  
  -- c##testuser2 부여받은 롤 권한 회수
  REVOKE connect, resource FROM c##testuser2;
  ```


#### (32) PL/SQL

- Procedural Language / SQL

- 비절차적 언어인 SQL을 확장한 절차적인 프로그래밍 언어

- 오라클에서만 사용 가능

- 변수, 상수 등을 이용하여 SQL과 절차형 언어 사용

- IF문을 사용하여 조건에 따른 문장 분기 실행

- LOOP문을 사용하여 반복 실행

- 커서를 사용하여 여러 행 검색

- 세 블록으로 구분됨

  | 블럭                   | 설명                                                     |
  | ---------------------- | -------------------------------------------------------- |
  | DECLARE (선언부)       | 변수나 상수 선언                                         |
  | BEGIN (실행부)         | SQL, 절차적 언어 (제어문, 반복문, 함수 등)를 이용한 로직 |
  | EXCEPTION (예외처리부) | 예외가 발생할 가능성이 있는 코드 처리                    |

  ```sql
  SET SERVEROUTPUT ON; -- 실행결과 화면 출력 설정
  
  BEGIN
  	DBMS_OUTPUT.PUT_LINE('hello world');
  END;
  ```


```sql
DECLARE
	VEMPNO NUMBER(4);
	VENAME VARCHAR2(10);
BEGIN
	VEMPNO := 1; -- 변수 할당
	VENAME := '홍길동';
	SELECT EMPNO, JOB INTO VEMPNO, VJOB
	FROM EMP WHERE ENAME='손흥민'; -- select로 가져오기
	-- IF
	IF MOD(VNUMBER, 2) = 0 THEN
		DBMS_OUTPUT.PUT_LINE('짝수');
    END IF; -- ELSIF, ELSE 
    
    -- LOOP
    LOOP
    	DBMS_OUTPUT.PUT_LINE(VNUMBER);
    	VNUMBER := VNUMBER + 1;
    	EXIT WHEN VNUMBER > 10;
    END LOOP;
    
    -- FOR LOOP
    FOR i IN 1..10 LOOP
    	DBMS_OUTPUT.PUT_LINE(i);
    END LOOP;
    
    -- WHILE LOOP
    WHILE VNUMBER <= 10 LOOP
    	DBMS_OUTPUT.PUT_LINE(VNUMBER);
    	VNUMBER := VNUMBER + 1;
    END LOOP;
    
	DBMS_OUTPUT.PUT_LINE('사원번호 : ' || VEMPNO);
	DBMS_OUTPUT.PUT_LINE('사원명 : ' || VENAME);
END;


-- 커서
DECLARE
	CURSOR cur IS
		SELECT empno, ename FROM emp;
BEGIN
	FOR r IN cur LOOP
		DBMS_OUTPUT.PUT_LINE(r.EMPNO || r.ENAME);
    END LOOP;
END;


-- 프로시저 생성 (아직 실행되기 전)
CREATE TABLE emp_test AS SELECT * FROM emp;
CREATE OR REPLACE PROCEDURE deleteAll
IS
BEGIN
	DELETE FROM emp_test;
	COMMIT;
END;

-- 프로시저 실행
EXECUTE deleteAll;

-- 프로시저 (파라미터) 생성
DROP TABLE emp_test;
CREATE TABLE emp_test AS SELECT * FROM emp;
CREATE OR REPLACE PROCEDURE deleteJob(vjob varchar2)
IS
BEGIN
	DELETE FROM emp_test WHERE JOB = vjob;
	COMMIT;
END;

-- in : 값 입력 (기본값)
-- out : 값 반환
-- in out : 값 입력 후 결과 값 반환
CREATE OR REPLACE PROCEDURE selectEmp
	(vempno in emp.empno%type,
    vename out emp.ename%type, vjob out emp.job%type)
IS BEGIN
	SELECT ename, job INTO vename, job
	FROM emp WHERE empno = vempno;
END;

variable vename varchar2; -- sql 창에서만 사용되는 변수
variable vjob varchar2;

execute selectEmp(1000, :vename, :vjob);

print vename;
print vjob;


-- 함수
CREATE OR REPLACE FUNCTION calSal (vempno in number)
RETURN number
IS
	vsal number;
	vbonus number;
BEGIN
	SELECT salary, bonus INTO vsal, vbonus
	FROM emp WHERE empno=vempno;
	RETURN vsal*12 + NVL(vbonus, 0);
END;

variable vsalary varchar2;
execute :vsalary := calSal(1000);
print vsalary;
```



#### (33) 프로시저와 함수

| 구분          | 프로시저                                               | 함수                                               |
| ------------- | ------------------------------------------------------ | -------------------------------------------------- |
| 실행          | Execute 명령어, 다른 PL/SQL 내                         | execute명령어, 다른 PL/SQL 내, SQL문에서 직접 실행 |
| 파라미터 모드 | 있을수도 없을수도 있음. IN, OUT, IN OUT                | 있을 수도, 없을 수도 있음.<br /> IN                |
| 값 반환       | 없을 수도 있고, OUT모드의 개수에 따라 여러개 반환 간으 | RETURN절을 이용해 하나의 값만 반환 가능            |



#### (34) 트리거

- 특정 조건을 만족하거나, 어떤 동작이 실행되면, 자동으로 수행되는 객체

- 프로시저, 함수는 사용자가 직접 호출하지만, 트리거는 자동으로 실행

- 사용자가 직접 실행 불가

- SQL문의 복잡도 감소

  ```sql
  CREATE OR REPLACE TRIGGER 트리거명
  BEFORE | AFTER
  INSERT | UPDATE | DELETE
  ON 테이블 명
  BEGIN
  	실행부;
  END;
  
  -- 예시
  CREATE TABLE emp2 AS SELECT * FROM emp;
  
  CREATE OR REPLACE TRIGGER emp_trigger
  BEFORE INSERT
  ON emp2
  BEGIN
  	DBMS_OUTPUT.PUT_LINE('신입사원 입사');
  END;
  
  INSERT INTO emp2 VALUES (~~~);
  
  -- INSERT 되기전 신입사원 입사 출력
  ```


#### (35) 오라클 아키텍처

- Oracle Server 접근 방식
  - Client -> listener -> database server (instance -> client, client -> database)
- Instance, Database
  - 메모리 : SGA (Shared Pool + Data Buffer Cache + Redo Log Buffer)
    - SGA (System Global Area) : 인스턴스 시작 시 SGA 영역 할당. 인스턴스별로 하나만 생성. 모든 사용자가 공유
    - PGA(Program Global Area) : 사용자 요청 데이터 정보가 처리되는 영역. 사용자 세션별로 독립적으로 생성
  - 프로세스 : SMON(System Monitor), PMON(Process Moniter), CKPT(Checkpoint process), DBW (Database writer), LGWR(Redo Log Writer)
  - 디스크 : Parameter File, Control File(CKPT), Database File(DBW), Redo Log File



#### (36) SQL 실행 순서

INSERT, UPDATE, DELETE (SELECT 보다 느림)

1. 문법 확인
2. 의미 검사
3. LGWR이 Redo Log Buffer에 저장
4. DBWR이 버퍼캐시에 기록 -> 데이터 파일에 저장



SELECT

1. 문법 확인
2. 의미 검사
3. DB버퍼 캐시에서 확인 (없으면 디스크에서 찾아 버퍼 캐시로 복사)
4. 조회 결과 데이터를 사용자 프로세스로 전송



#### (37) 데이터 저장소 구조

Physical Database : data files, control files, redo log files

Logical Database : Data blocks, Extents, Segments, Tablespaces

	Logical Storage         | Physical Storage 
		
	
	Schema > Database

		Tablespace <     DataFile  ——— filesystems, ASM, NFS, RAW

		Segments	   |	|

		Extent———----------|	|

		Oracle Data Block—Disk block

- 논리적 저장소

  - Tablespace > segment > extent > Data block

    | 단위       | 설명                                                         |
    | ---------- | ------------------------------------------------------------ |
    | Tablespace | 테이블이 모여있는 단위. 하나이상의 segment를 포함하는 저장단위 |
    | Segment    | 테이블, 인덱스 등 모든 데이터를 보유하고 있는 Extent의 집합  |
    | Extent     | Segment에 할당된 연속적인 Data Block의 집합                  |
    | Data Block | 데이터 파일에 할당되는 최소의 구조 단위                      |


#### (38) 인덱스

- 데이터의 빠른 검색을 위해 사용하는 색인 기술
- B-tree 자료구조를 이용하여 검색 속도 향상
- B-tree (Balaced Tree란 이진트리의 변형된 알고리즘).
  데이터를 빠르게 찾을 수 있도록 트리구조에 정렬한 상태로 보관하는 방식
  왼 : 나보다 작은거, 오른 : 나보다 큰거
- 장점 : 검색 속도가 빠름, 시스템 부하를 줄여 성능 향상
- 단점 : 추가 공간 필요, 인덱스 생성 시간 소요, Insert, Update, Delete 작업 시 성능 저하

```sql
CREATE INDEX 인덱스명 ON 테이블명(컬럼);
```

- 인덱스를 사용해야할 컬럼
  - WHERE절에서 자주 사용되는 컬럼
  - 조인시 조건에 사용되는 컬럼
  - 두 개 이상의 컬럼이 포함되는 조건인 경우 복합 인덱스로 지정
  - 복합 인덱스인 경우 조회 조건에 모든 컬럼이 동시에 사용되도록 지정
- 주의사항
  - PRIMARY KEY, UNIQUE KEY 제약조건에서는 자동 생성
  - 해당 컬럼을 가공하기 전 상태에서 조건 지정
  - 인덱스 여부까지 데이터 모델링 시 고려 필요
  - LIKE 연산은 인덱스 미적용
  - varchar x

- 실행 계획

```sql
EXPLAIN PLAN FOR SELECT * FROM emp3 WHERE job='사원';
SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);
```



