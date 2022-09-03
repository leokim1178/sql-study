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
9. INNER vs OUTER vs CROSS JOIN 비교

# 집합 연산자

- 두 개 이상의 테이블에서 조인을 사용하지 않고 연관데이터를 조회하는 또다른 방법
- Set Operator
- FROM 절에 검색하고자 하는 테이블을 나열
- WHERE절에 조인 조건을 기술
- SELECT 절의 칼럼 수가 동일하고 호환가능해야 한다

1. UNION
   - 여러 개의 SQL문의 결과에 대한 합집합
   - 모든 중복된 행은 하나의 행으로 만듬
2. UNION ALL
   - 여러 개의 SQL문 결과에 대한 합집합
   - 중복된 행도 그대로 표시된다
   - 단순히 결과만 합쳐놓은 것
   - 질의 결과가 상호 배타적일때 많이 사용
   - SQL문의 결과가 서로 중복되지 않는 경우에는 UNION과 결과가 동일
3. INERTSECT
   - 여러개의 SQL문의 결과에 대한 교집합
   - 중복된 행은 하나의 행으로 처리
4. EXCEPT
   - 앞의 SQL문의 결과에서 뒤의 SQL문의 결과에 대한 차집합
   - 중복된 행은 하나의 행으로 처리

- 집합 연산자 사용 예문

```sql
SELECT PLAYER_NAME 선수명, BACK_NO 백넘버
FROM PLAYER
WHERE TEAM_ID = 'K02'
//
UNION
//여기에서 집합연산자 사용
SELECT PLAYER_NAME 선수명, BACK_NO 백넘버
FROM PLAYER
WHERE TEAM_ID = 'K07'
ORDER BY 1;
```

- 집합 연산자는 여러개의 SELECT 문을 연결하는 것에 지나지 않는다
- ORDERBY는 최종 결과에 대한 정렬 처리이므로 가장 마지막에 한번만 기술한다

# 계층형 질의와 셀프 조인

1. 계층형 질의
   - 테이블에 계층형 데이터가 존재하는 경우 데이터 조회를 위한 질의이다
   - 계층형 데이터
     - 동일 테이블에 계층적으로 상위와 하위 데이터가 포함된 데이터
   - 오라클에서의 계층형 질의
     - 예문
     ```sql
     SELECT
     FROM 테이블
     WHERE condition AND condition...
     START WITH condition
     CONNECT BY [NOCYCLE] condition AND condition
     ....
     ```
     - START WITH
       - 계층 구조 전개의 시작위치를 지정하는 구문
       - 루트 데이터를 지정한다
       - CONNECT BY절에 주어진 조건을 만족해야한다
     - CONNECT BY
       - 다음에 전개될 자식 데이터를 지정하는 구문
       - 자식-부모 부모-자식 순으로 전개하도록 만들수 있다
       - 이미 나타낫던 데이터가 전개중에 다시 나타난다면 사이클 형성(사이클이 발생한 데이터는 런타임 오류)
       - 이를 NOCYCLE로 막을 수 있다
     - SYS_CONNECT_BY_PATH
       - 루트 데이터부터 현재 전개할 데이터까지의 경로를 표시한다
     - CONNECT_BY_ROOT
       - 현재 전개할 데이터의 루트 데이터를 표시한다 단항 연산자다
   - SQL 서버에서의 계층형 질의
2. 셀프 조인
   - 동일 테이블 사이의 조인
   - FROM 절에 동일 테이블이 두번 이상 나타난다
   - 동일하기 때문에 ALIAS를 사용해야 한다
   - 예문
   ```sql
   SELECT E1.사원, E1.관리자, E2.관리자 차상위_관리자
   FROM 사원 E1, 사원 E2
   WHERE E1.관리자 = E2.사원
   ORDER BY E1.사원;
   ```

# 서브쿼리

- 서브쿼리란 하나의 SQL문 안에 포함되어 있는 또 다른 SQL문을 의미한다
- 알려지지 않은 기준을 이용한 검색을 위해 사용한다
- 메인쿼리가 서브쿼리를 포함하는 종속적인 관계다
- 서브쿼리는 메인쿼리의 칼럼을 모두 사용할 수 있지만 메인쿼리는 서브쿼리의 칼럼을 사용할 수 없다
- 주의사항
  - 서브쿼리는 괄호로 감싸서 사용한다
  - 단일 행 또는 복수 행 비교 연산자와 함께 사용 가능하다
  - 서브쿼리에서는 ORDERBY를 사용하지 못한다
    - 메인쿼리에 마지막에 위치해야 한다
  - 비연관 서브쿼리 vs 연관 서브쿼리
    - 메인쿼리 칼럼을 가지고 있으면, 연관 없으면 비연관

1. 단일행 서브쿼리

   - 서브쿼리의 실행 결과가 항상 1건 이하인 서브쿼리
   - 단일 행 비교 연산자(<,>,<=,=> 등)과 함께 사용된다
   - 2건 이상이면 런타임 오류 발생

2. 다중행 서브쿼리
   - 실행 결과가 여러 건인 서브쿼리를 의미한다
   - 다중 행 비교 연산자(IN,ALL,ANY,SOME,EXISTS)와 함께 사용된다
3. 다중 칼럼 서브쿼리
   - 실행 결과로 여러 칼럼을 반환한다
   - 메인쿼리의 조건절에 여러 칼럼을 동시에 비교할 수 있다
   - 서브쿼리와 메인쿼리에서 비교하고자 하는 칼럼 개수와 칼럼의 위치가 동일해야 한다
4. 연관서브쿼리
   - 서브 쿼리 내에 메인쿼리 칼럼이 사용된 서브쿼리
   - EXISTS 서브쿼리는 항상 연관 서브쿼리로 사용된다
5. 그 밖에 위치에서 사용하는 서브쿼리
   - SELECT 절의 서브쿼리
     - 스칼라 서브쿼리라고 한다
     - 칼럼을 쓸수 있는 대부분의 곳에서 사용할 수 있다
     - 스칼라 서브쿼리는 메인쿼리의 결과 건수만큼 반복 수행된다
   - FROM 절의 서브쿼리
     - 인라인 뷰라고 한다
     - 동적으로 생성된 테이블인 것처럼 사용할 수 있다
     - 그래서 동적 뷰라고 하기도 한다
   - HAVING 절의 서브쿼리
     - 그룹함수와 함께 사용될 때 그룹핑된 결과에 대해 부가적인 조건을 주기 위해 사용
     - 평균키가 삼성 블루윙즈팀의 평균키보다 작은 팀의 이름과 해당 팀의 평균키를 구하는 SQL문
     ```sql
     SELECT P.TEAM_ID 팀코드, T.TEAM_NAME 팀명, AVG(P.HEIGHT) 평균키 FROM PLAYER P, TEAM T
     WHERE P.TEAM_ID = T.TEAM_ID
     GROUP BY P.TEAM_ID, T.TEAM_NAME
     HAVING AVG(P.HEIGHT) <(SELECT AVG(HEIGHT)
     FROM PLAYER
     WHERE TEAM_ID ='K02')
     ```
     - 결과
     ```js
     [
       { 팀코드: "K13", 팀명: "강원FC", 평균키: 173.667 },
       { 팀코드: "K15", 팀명: "대구FC", 평균키: 176.333 },
       { 팀코드: "K14", 팀명: "제주유나이티드", 평균키: 169.5 },
     ];
     ```
6. 뷰
   - 뷰는 실제 데이터를 가지고 있지 않지만 테이블의 역할을 수행한다
   - 가상테이블이라고도 한다
   - 독립성
     - 테이블의 구조가 변경되어도 뷰를 사용하는 응용 프로그램은 변경하지 않아도 된다
   - 편리성
     - 복잡한 질의를 뷰로 생성함으로써 관련 질의를 단순하게 작성할 수 있다
   - 보안성
     - 직원의 급여정보와 같이 숨기고 싶은 정보가 존재하면 뷰를 생성할 때 해당 칼럼을 빼고 생성함으로써 사용자에게 정보를 감출 수 있다
   - `CREATE VIEW`를 통해 생성할 수 있다
   - `DROP VIEW`를 통해 제거한다

# 그룹 함수

1. 데이터분석 개요
   - aggergate 함수
     - 그룹 함수의 한 분류
     - count,sum,avg 같은 집계함수들이 포함
   - group 함수
     - 롤업
     - 그룹
     - 큐브
     - 그루핑 셋
   - window 함수
     - 분석함수나 순위 함수로 알려져있다
     - 데이터웨어하우스에서 발전된 기능
2. ROLLUP 함수

   - GROUP BY의 확장된 형태로 사용한다
   - 병렬로 수행되기 때문에 효과적이다
   - - 시간,지역 같은 계층적 분류에 적합하다
   - 일반적인 그룹 바이 함수에 롤업함수를 다음과 같이 사용한다
   - 예문

   ```sql
   SELECT DNAME, JOB,
   COUNT(*) "Total Empl",
   SUM(SAL) "Total Sal" FROM EMP, DEPT
   WHERE DEPT.DEPTNO = EMP.DEPTNO
   GROUP BY ROLLUP (DNAME, JOB)
   ORDER BY DNAME, JOB ;
   ```

3. CUBE 함수
   - 결합 가능한 모든 값에 대하여 다차원적인 집계를 생성한다
   - 다양한 데이터를 얻는 장점이 있다
   - 시스템 부하를 많이 주는 단점이 있다
4. GROUPING SETS 함수
   - 원하는 소게만 손쉽게 추출할 수 있는 장점이 있다

# 윈도우 함수

1. WINDOW FUNCTION 개요
   - 복잡한 프로그램을 하나의 SQL문장으로 쉽게 해결할 수 있다
   - 인라인 뷰 이후 SQL의 중요한 기능이 추가된 기능
   - OVER 문구가 키워드로 필수 포함된다
   - 예문
   ```sql
   SELECT WINDOW_FUNCTION (ARGUMENTS) OVER
   ( [PARTITION BY 칼럼] [ORDER BY 절] [WINDOWING 절] )
   FROM 테이블 명;
   ```
2. 그룹 내 순위 함수
   - RANK 함수
     - ORDER BY를 포함한 쿼리문에서 특정 항목에 대한 순위를 구하는 함수다
     - 특정 범위 내에서 순위를 구할수도 있고 전체 데이터에 대한 순위를 구할 수도 있다
     - 동일한 값에 대해서는 동일한 순위를 부여하게 된다
     ```sql
     SELECT JOB, ENAME, SAL,
     RANK( ) OVER (ORDER BY SAL DESC) ALL_RANK,
     RANK( ) OVER (PARTITION BY JOB ORDER BY SAL DESC) JOB_RANK
     FROM EMP;
     ```
     - 먼저 들어간 ORDER BY로 출력순서가 정해진다
     - PARTITION BY ~ 는 파티션으로 구분한 범위내에서의 순위를 부여한다
   - DENSE_RANK 함수
     - RANK와 흡사
     - 동일한 순위를 하나의 건수로 취급한다
     - 예를 들어 2등이 중복될 경우 4등이 아닌 3등으로 표시한다
   - ROW_NUMBER 함수
     - 동일한 값이라도 고유 순위를 부여한다
     - 동일한 순위를 배제하기 때문에 유니크한 순위를 정한다
3. 일반 집계 함수
   - SUM 함수
     - 파티션별 윈도우의 합을 구할 수 있다
     - 예문
     ```sql
     SELECT MGR, ENAME, SAL, SUM(SAL) OVER (PARTITION BY MGR) MGR_SUM
     FROM EMP;
     ```
   - MAX 함수
     - 파티션별 윈도우의 최댓값을 구할 수 있다
     ```sql
     SELECT MGR, ENAME, SAL, MAX(SAL) OVER (PARTITION BY MGR) as MGR_MAX
     FROM EMP;
     ```
   - MIN 함수
     - 파티션별 윈도우의 최솟값을 구할수 있다
     - 예문은 MAX랑 비슷
   - AVG 함수
     - 원하는 조건에 맞는 데이터에 대한 통계값을 구할 수 있다
     - 예문
     ```sql
     SELECT MGR, ENAME, HIREDATE, SAL,
     ROUND (AVG(SAL) OVER (PARTITION BY MGR ORDER BY HIREDATE ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)) as MGR_AVG
     FROM EMP;
     ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING :
     현재 행을 기준으로 파티션 내에서 앞의 한 건, 현재 행, 뒤의 한 건을 범위로 지정한다. (ROWS는 현재 행의 앞뒤 건수를 말하는 것임)
     ```
   - COUNT 함수
     - 파티션별 윈도우를 이용해 원하는 조건에 맞는 데이터에 대한 통계값을 구할 수 있다
     - 예문
     ```sql
     SELECT ENAME, SAL,
     COUNT(*) OVER (ORDER BY SALRANGE BETWEEN 50 PRECEDING AND 150 FOLLOWING) as SIM_CNT FROM EMP;
     RANGE BETWEEN 50 PRECEDING AND 150 FOLLOWING :
     현재 행의 급여값을 기준으로 급여가 -50에서 +150의 범위 내에 포함된 모든 행이 대상이 된다. (RANGE는 현재 행의 데이터 값을 기준으로 앞뒤 데이터 값의 범위를 표시하는 것임)
     ```
4. 그룹 내 행 순서 함수
   - FIRST_VALUE 함수
     - 파티션별 가장 먼저 나온값을 구한다
     - MIN으로 해도 같은 결과를 얻을 수도 있다
     - [예문] 부서별 직원들을 연봉이 높은 순서부터 정렬하고, 파티션 내에서 가장 먼저 나온 값을 출력
     ```sql
     SELECT DEPTNO, ENAME, SAL,
     FIRST_VALUE(ENAME)
     OVER (PARTITION BY DEPTNO ORDER BY SAL DESC ROWS UNBOUNDED PRECEDING) as DEPT_RICH FROM EMP;
     RANGE UNBOUNDED PRECEDING :
     현재 행을 기준으로 파티션 내의 첫 번째 행까지의 범위를 지정한다.
     ```
   - LAST_VALUE 함수
     - 파티션별 가장 마지막에 나온 값을 구한다
     - 공동 등수를 인정하지 않는다
   - LAG 함수
     - 파티션별 윈도우에서 이전 행의 값을 가져올수 있다
     - [예문]
     ```sql
     SELECT ENAME, HIREDATE, SAL,
     LAG(SAL, 2, 0) OVER (ORDER BY HIREDATE) as PREV_SAL FROM EMP
     WHERE JOB = 'SALESMAN'
     LAG(SAL, 2, 0)의 기능은 두 행 앞의 SALARY를 가져오고, 가져올 값이 없는 경우는 0으로 처리한다.
     default는 1이다
     ```
   - LEAD 함수
     - 파티션별 윈도우에서 이후 행의 값을 가져올 수 있다
     - [예문]
     ```sql
     SELECT ENAME, HIREDATE,
     LEAD (HIREDATE, 1) OVER (ORDER BY HIREDATE) as "NEXTHIRED"
     FROM EMP;
     ```
5. 그룹 내 비율 함수

   - RATIO_TO_REPORT 함수

     - 파티션 내 전체 SUM값에 대한 행별 칼럼 값의 백분율 즉 퍼센티지를 구할 수 있다
     - 결과값은 0 초과 1이하의 값을 가진다
     - 개별 RATIO의 값을 합하면 1이 된다
     - [예문]

     ```sql
     SELECT ENAME, SAL, ROUND(RATIO_TO_REPORT(SAL) OVER (), 2) as R_R FROM EMP
     WHERE JOB = 'SALESMAN';
     ```

   - PRCENT_RANK 함수
     - 파티션별 제일먼저 나오는것을 0 제일 나중에 나오는 것을 1로 하여 값이 아닌 행의 순서별 백분율을 구한다
     - 예문
     ```sql
     SELECT DEPTNO, ENAME, SAL,
     PERCENT_RANK() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) as P_R FROM EMP;
     ```
   - CUME_DIST 함수
     - 파티션별 윈도우의 전체건수에서 현재 행보다 작거나 같은 건수에 대한 `누적백분율`을 구한다
     - [예문] 같은 부서 소속 사원들의 집합에서 본인의 급여가 누적 순서상 몇 번째 위치쯤에 있 는지 0과 1 사이의 값으로 출력한다.
     ```sql
     SELECT DEPTNO, ENAME, SAL,
     CUME_DIST() OVER (PARTITION BY DEPTNO ORDER BY SAL DESC) as CUME_DIST FROM EMP;
     ```
   - NTILE 함수
     - 파티션별 전체 건수를 인수값으로 N등분 한 결과를 구한다
     - [예문] 전체 사원을 급여가 높은 순서로 정렬하고, 급여를 기준으로 4개의 그룹으로 분류한다.
     ```sql
     SELECT ENAME, SAL, NTILE(4) OVER (ORDER BY SAL DESC) as QUAR_TILE FROM EMP
     4가 바로 등분할 인수
     ```

# DCL

1. DCL 개요
   - 유저를 생성하고 권한을 제어할 수 있는 DCL이 있다
2. 유저와 권한
   - 오라클
     - SCOTT
       - 오라클 테스트용 샘플 유저
       - 디폴트 패스워드 : TIGER
     - SYS
       - DBA ROLE을 부여받은 유저
     - SYSTEM
       - 데이터베이스의 모든 시스템 권한을 받은 DBA 유저
   - DROP [USER]
     - 유저 삭제
     - CASCADE 옵션을 주면 해당 유저가 생성한 오브젝트를 먼저 삭제한 후 유저를 삭제한다
3. Role을 이용한 권한 부여
   - 유저마다 ROLE을 생성하고 ROLE에 각종 권한들을 부여한다
   - 그 ROLE을 다른 ROLE이나 유저에게 부여할 수 있다
   - REVOKE
     - 권한 취소
   - GRANT
     - 권한 부여

# 절차형 SQL

1. 절차형 SQL 개요
   - SQL문의 연속적인 실행이나 조건에 따른 분기처리를 이용하여 특정 기능을 수행하는 저장 모듈을 생성할 수 있다
   - 프로시져, 유저 디파인드 펑션, 트리거등을 만들수 있다
2. PL/SQL 개요
   - BLOCK 구조로 되어있다
   - 절차적 프로그래밍을 가능하게 하는 트랜잭션 언어다
   - 다양한 저장 모듈을 개발할 수 있다
   - 일종의 SQL 컴포넌트 프로그램
   - 독립적으로 실행되거나 다른 프로그램으로부터 실행될 수 있는 완전한 실행 프로그램이다
   - DECLARE : BEGIN ~ END 절에서 사용될 변수와 인수에 대한 정의 및 데이터 타입을 선언하는 선언부이다.
   - BEGIN ~ END : 개발자가 처리하고자 하는 SQL문과 여러 가지 비교문, 제어문을 이용하여 필요한 로직을 처리하는 실행부이다.
   - EXCEPTION : BEGIN ~ END 절에서 실행되는 SQL문이 실행될 때 에러가 발생하면 그 에러를 어떻게 처리할 것 이지를 정의하는 예외 처리부이다.
   - 예문
   ```sql
   CREATE [OR REPLACE] Procedure [Procedure_name] ( argument1 [mode] data_type1,argument2 [mode] date_type2, ... ... )
   IS [AS]... ...
   BEGIN ... ...
   EXCEPTION ... ...
   END;
   ```
   ```sql
   DROP Procedure [Procedure_name];
   -> 프로시저 삭제 명령어
   ```
   - 프로시져
     - 프로시저 는 개발자가 자주 실행해야 하는 로직을 절차적인 언어를 이용하여 작성한 프로그램 모듈이다
     - [OR REPLACE] 절은 데이터베이스 내에 같은 이름의 프로시저가 있을 경우, 기존의 프로시저를 무시하고 새로운 내용으로 덮어쓰기 하겠다는 의미
     - [mode] 부분에 지정할 수 있는 매개 변수의 유형
       - IN은 운영 체제에서 프로시저로 전달될 변수의 MODE
       - OUT은 프로시저에서 처리된 결과가 운영 체제로 전달되는 MODE
       - INOUT MODE가 있는데 이 MODE는 IN과 OUT 두 가지의 기능을 동시에 수행하는 MODE이다.
       - 마지막에 있는 슬래쉬 (“/”)는 데이터베이스에게 프로시저를 컴파일하라는 명령어이다.
3. T-SQL 개요
   - ANSI/ISO 표준 SQL에 약간의 기능을 추가해 보완적으로 만든 것
   - 구조는 PL/SQL과 유사하다
4. User Defined Function의 생성과 활용
   - 절차형 SQL을 로직과 함께 데이터베이스 내에 미리 저장해놓은 명령문의 집합
   - 사용자가 만든 별도의 함수다
   - 프로시져랑 다른 점은 리턴을 사용해서 하나의 값을 반드시 되돌려줘야한다는 점이다
5. Trigger의 생성과 활용
   - INSERT,UPDATE,DELETE와 같은 DML문이 수행되었을 때, 데이터베이스에서 자동으로 동작하도록 만든 프로그램
6. 프로시저와 트리거의 차이점
   - 프로시저
     - CREATE procedure 문법사용
     - EXECUTE 명령어로 실행
     - COMMIT,ROLLBACK 가능
   - 트리거
     - CREATE trigger 문법사용
     - 생성한후에는 자동적으로 실행
     - COMMIT,ROLLBACK 불가
