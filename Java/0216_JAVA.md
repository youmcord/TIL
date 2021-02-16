# 0216

## DataBase vs DBMS (DataBase Management System)

> 정보 vs 정보 관리 시스템

- Oracle: Dataset을 만들어낸다 (Database), 오라클에서는 이 DB를 스키마라고 부른다

  | Client              | Presentation                                      | Service  | Resource                                                     |
  | ------------------- | ------------------------------------------------- | -------- | ------------------------------------------------------------ |
  | 사람, 응용 프로그램 | Action 수행(?), 대면할 수 있는 화면 (결과의 표현) | biz 부분 | Database (일의 진행 중 사용되는 데이터)  / 이를 관리하는 DBMS |

- 개념적인 내용을 물리적으로 가시화 하는 작업을 모델링이라고 한다. DB Admin은 모델링 하는 사람.
- 우리는 Database의 SQL을 사용해서 CRUD를 할 것



### Data

1. 데이터의 무결성
   - 데이터에 오류가 있어서는 안 된다.
2. 데이터의 독립성
3. 보안
4. 데이터 중복 최소화
   - 중복 방지
5. 응용 프로그램 제작 및 수정이 쉬워짐
6. 데이터의 안전성 향상



### Enterprise

- 동시에 많은 사용자가 사용.
- Server 속도보다 안정성이 중요함 -> Java
- DBMS는 RDBMS



### 관계형 DBMS

- 데이터베이스가 테이블이라는 최소 단위로 구성되어 있음
- 여러 개의 테이블로 저장 -> 공간 낭비 줄이고 데이터 저장의 효율성 보장



## SQL

### select

``` sql
select * from employees; --스키마 이름은 생략 가능

select department_name, DEPARTMENT_ID from DEPARTMENTS;
/*
열은 적은 순서대로 출력됨
열거는 콤마로 함
*/
```



``` sql
select * from EMPLOYEES where first_name like 'A%'; -- 첫번째 글자가 A인 사람
select * from EMPLOYEES where first_name like '_a%'; -- 두번째 글자가 a인 사람 (대소문자 구분 됨)
select * from EMPLOYEES where first_name like '%a%' -- 이름에 a가 포함된 사람 모두 나옴

```



### Order by

> 원하는 순서대로 정렬

``` sql
select * from EMPLOYEES where first_name like '%a%' order by salary; -- 샐러리 순으로 오름차순
select * from EMPLOYEES where first_name like '%a%' order by salary desc; -- 샐러리 순으로 내림차순
select * from EMPLOYEES where first_name like '%a%' order by EMPLOYEE_ID asc; --ID 순으로 올림차순
select * from EMPLOYEES where first_name like '%a%' order by salary desc, EMPLOYEE_ID asc; -- 샐러리 순으로 내림차순, 샐러리가 같은 경우 ID 순으로 올림차순

```



### Distinct

> 중복된 것은 하나만 남김

``` sql
select DISTINCT HIRE_DATE from EMPLOYEES; -- 입사일 중복될 경우 한개만 남겨줌
```



### Insert

> 행 추가

``` sql
insert into MEMBERTBL values('JES','전은수','경기 부천시 오정동'); -- 행 추가됨 (열 이름 생략하고)

-- 생략 안 할 경우?
insert into MEMBERTBL (MEMBERID, MEMBERNAME, MEMBERADDRESS) values('JES','전은수','경기 부천시 오정동');

-- 열 이름을 넣는 이유? 순서를 바꿀 수 있기 때문
insert into MEMBERTBL (MEMBERNAME, MEMBERADDRESS, MEMBERID) values('이영숙','서울 구로구','Lee');
```

- 열 이름을 생략하면 테이블 만들 때의 열 순서대로 들어감
- 근데 순서가 기억이 안 날 수도 있잖아!
  - 그럴때 앞에 열 이름을 생략하지 않고 써주면 해당 열에 해당 데이터가 들어가게 된다



### Update

``` sql
update PRODUCTTBL set AMOUNT=100 where PRODUCTNAME='컴퓨터';
-- 컴퓨터의 amount를 100으로 변경
```

+) commit 한 후에는 롤백이 안됨, 신중하게!



### Delete

``` sql
delete from PRODUCTTBL where PRODUCTNAME='컴퓨터'; -- 컴퓨터 행 삭제
```



### CRUD

- C: Create / Insert
- R: Read / Select
- U: Update / Update
- D: Delete /Delete

EX.

- 회원가입: insert (insert into memberTBL (id, pw, name) values ('a','b','전은수');
- 로그인: select (select * from memberTBL where id='a' and pw='b');
- 회원 수정: update (update memberTBL set pw='c' where id='a');
- 탈퇴: delete (delete from memberTBL where id='a';)