---
과목2 SQL 기본 및 활용
2장 SQL 활용
---

# 표준 조인
1. 스탠다드 SQL 개요
   - 대부분 객체 관계형 데이터베이스를 사용하고 있다
   - ANSI/ISO SQL 표준을 통해 표준조인을 포함하여 DBMS 같에 평준화를 이루어 가고 있다
   - 일반 집합 연산자
     - UNION
       - 수학적 합집합을 제공하고 공통 교집합의 중복을 없애기 위한 사전 작업
     - INTERSECTION
       - 교집합
     - DIFFERENCE
       - 차집합
     - PRODUCT
       - JOIN 조건이 없는 경우 생길 수 있는 모든 데이터의 조합을 말한다
   - 순수 관계 연산자
     - SELECT
       - WHERE 절로 구현
     - PROJECT
       - SELECT 절로 구현
     - JOIN
       - 다양한 JOIN 기능으로 구현
     - DIVIDE
       - deprecated

2. FROM 절 JOIN 형태
   - INNER JOIN
   - NATURAL JOIN - USING 조건절
   - ON 조건절
   - CROSS JOIN
   - OUTER JOIN 
3. INNER JOIN
   - JOIN의 디폴트 옵션
   - `INNER`는 생략 가능
   - JOIN 조건에 동일한 값이 있는 행만 반환
   - CROSS JOIN, OUTER JOIN과는 같이 사용할 수 없다
   - 첫번째 테이블과 두번째 테이블의 칼럼들이 테이블 순서대로 출력된다
4. NATURAL JOIN
   - INNER JOIN의 하위 개념
   - 두 테이블 간의 동일한 이름을 갖는 모든 칼럼들에 대해 EQUI(=)JOIN을 수행한다
   - 별도의 JOIN 칼럼을 지정하지 않아도 된다
   - ALIAS나 테이블 명같은 접두사를붙일수 없다
5. USING 조건절
   - FROM 절의 USING 조건 절을 이용하면 같은 이름을 가진 칼럼들 중에서 원하는 칼럼에 대해서만 선택적으로 EQUI 조인을 할 수 있다
   - 별도의 칼럼 순서를 지정하지 않으면 USING 조건절의 기준이 되는 칼럼이 다른 칼럼보다 먼저 출력된다
   - USING (hey) 이러면 hey가 첫번째 칼럼이 된다
   - NATURAL JOIN과 마찬가지로 JOIN 칼럼에 대해서는 ALIAS나 테이블 이름과 같은 접두사를 붙일 수 없다
6. ON 조건절
   - NATURAL JOIN 처럼 JOIN 조건이 숨어 있지 않고, 명시적으로 JOIN 조건을 구분할 수 있다
   - NATURAL JOIN이나 USING 조건절처럼 칼럼명이 같아야한다는 제약이 없다
   - 상호 다르더라도 JOIN 조건으로 사용할 수 있다는 뜻
   - 
   - FROM 절에 테이블이 많이 사용될수록 복잡하게 보이고 가독성이 떨어진다
7. CROSS JOIN
   - JOIN 조건이 없는경우 생길 수 있는 모든 데이터의 조합을 말한다
8. OUTER JOIN
   - JOIN 조건에서 동일한 값이 없는 행도 반환할 떄 사용할 수 있다
   - 조인할 테이블의 조인 데이터 외에도 모든 데이터를 표시하고 싶은 경우 사용한다
9.  INNER vs OUTER vs CROSS JOIN 비교



# 집합 연산자

# 계층형 질의와 셀프 조인
1. 계층형 질의
2. 셀프 조인

# 서브쿼리
1. 단일행 서브쿼리
2. 다중행 서브쿼리
3. 다중 칼럼 서브쿼리
4. 연관서브쿼리
5. 그 밖에 위치에서 사용하는 서브쿼리
6. 뷰

# 그룹 함수
1. 데이터분석 개요
2. ROLLUP 함수
3. CUBE 함수
4. GROUPING SETS 함수

# 윈도우 함수
1. WINDOW FUNCTION 개요
2. 그룹 내 순위 함수
3. 일반 집계 함수
4. 그룹 내 행 순서 함수
5. 그룹 내 비율 함수

# DCL
1. DCL 개요
2. 유저와 권한
3. Role을 이용한 권한 부여


# 절차형 SQL
1. 절차형 SQL 개요
2. PL/SQL 개요
3. T-SQL 개요
4. Procedure의 생성과 활용
5. User Defined Function의 생성과 활용
6. Trigger의 생성과 활용
7. 프로시저와 트리거의 차이점