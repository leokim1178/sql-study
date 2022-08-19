---
과목2 SQL 기본 및 활용
1장 SQL 기본
---

# 관계형 데이터베이스 개요

1. 데이터베이스
   - 넓은 의미 : 일상적인 정보들을 모아 놓은 것 자체
   - 일반적인 의미 : 특정 기업이나 조직 또는 개인이 필요에 의해 데이터를 일정한 형태로 저장해 놓은 것
   - 쏟아져 나오는 다양한 정보들을 수집, 처리, 분석, 응용하는 것의 필요성이 높아지면서 발생
   - 데이터베이스의 발전
     - 1960s : 플로우차트 중심의 개발
     - 1970s : 데이터베이스 관리 기법이 처음 태동
     - 1980s : 오라클, 시베이스 등의 RDB 상용화
     - 1990s : 기존의 제품들이 향상됨, 객체 RDB로 발전
   - RDB
     - 1970년 코드 박사의 논문에서 처음 소개
     - 오라클을 선발로 여러 회사에서 상용화 제품을 출시
     - 계층형,망형 데이터베이스를 대체하며 주력 DB로 성장
     - 데이터의 중복을 피하고 정합성을 보장하기 위해 RDB가 사용되기 시작했다
     - RDB는 메타 데이터를 총괄 관리할수 있기 때문에 성격,속성 또는 표현 방법 등을 체계화 할 수 있다
     - 데이터 표준화를 통해 데이터 품질을 확보할 수 있다
     - 갑작스런 장애로부터 데이터가 정상적으로 반영될 수 있도록 보장해준다
     - 시스템 다운, 재해 등의 상황에서도 데이터를 회복,복구할 수 있는 능력이 있다
2. SQL

   - RDB에서 데이터 정의, 데이터 조작, 데이터 제어를 하기 위해 사용되는 언어
   - ANSI/ISO를 통해 표준화되고 정의되어 오고 있다
   - 일반적인 프로그래밍 언어와 달리, RDB에 대한 전담 접속용도로 사용되어 독립되어있다
   - 수학의 집합 논리에 입각한 언어다
   - DDL,DML,DCL로 나뉜다 (나중에 다룸)

3. TABLE
   - 데이터베이스의 기본 단위
   - 어느 특정한 주제와 목적으로 만들어지는 일종의 `집합`
   - 테이블
     - 행과 칼럼의 2차원 구조를 가진 데이터의 저장 장소이며, 데이터베이스의 가장 기본적인 개념
   - 칼럼/열
     - 2차원 구조를 가진 테이블에서 세로 방향으로 이루어진 하나하나의 특정 속성
   - 행
     - 2차원 구조를 가진 테이블에서 가로 방향으로 이루어진 연결된 데이터
   - 정규화
     - 이 테이블을 분할하여 불필요한 중복을 줄이는 것
     - 입력/수정/삭제 시 발생할 수 있는 이상현상을 방지하기 위한 매우 중요한 프로세스
   - 기본키와 외부키
     - 기본키 : 테이블에 존재하는 각 행을 한가지 의미로 특정할 수 있는 한개 이상의 칼럼
     - 외부키 : 다른 테이블의 기본키로 사용되고 있는 관계를 연결하는 칼럼
4. ERD
   - 다른 테이블과의 관계의 의미를 직관적으로 표현할 수 있는 수단
   - Entity-Relation Diagram, 즉 엔티티와 관계를 설명하는 그림이다

# DDL(DATA DEFINITION LANGUAGE)

1. 데이터 유형

   - 자료를 입력할때 자료를 받아들일 공간을 자료의 유형별로 나누는 기준
   - 특정 칼럼을 정의할때 선언한 데이터 유형은 그 칼럼이 받아들일 자료의 유형을 규정한다
   - 선언한 유형과 다른 종류의 데이터가 들어오면 에러를 리턴한다
   - 대표적인 4가지의 데이터 유형
     - CHARACTER(s)
       - 고정 길이 문자열 정보
       - s는 기본 길이 1바이트 최대 길이 2000~8000바이트
       - s만큼 최대 길이를 갖고 고정 길이를 가지고 있으므로 할당된 변수 값의 길이가 s보다 작을 경우 그 차이 길이만큼 공간으로 채워진다
     - VARCHAR(s)
       - Character Varying의 약자
       - 가변 길이 문자열 정보
       - s는 최소 길이 1바이트, 최대 길이 4000~8000바이트
       - s만큼 최대 길이를 갖지만 가변 길이로 조정이 되기 떄문에 할당된 변수값의 바이트만 적용된다
     - NUMERIC
       - 정수, 실수 등 숫자 정보(오라클은 NUMBER만, SQL Server는 10가지 이상의 숫자타입을 가지고 있음)
       - 오라클은 처음에 전체 자리 수를 지정하고 그다음 소수 부분의 자리 수를 지정한다
       - ex) 'NUMBER(8,2)' : 정수 부분이 6자리이고 소수점 부분이 2자리
     - DATETIME
       - 날짜와 시각 정보
       - 오라클은 1초단위, SQL 서버는 3.33ms 단위로 관리
   - CHAR과 VARCHAR의 차이
     - VARCHAR는 가변길이므로 필요한 영역은 실제 데이터 크기뿐이다
       - 따라서 길이가 다양한 칼럼과 정의된 길이와 실제 데이터 길이에 차이가 있는 칼럼에 적합하다
     - 저장 측면에서도 CHAR 유형보다 작은 영역에 저장할 수 있다
     - CHAR에서는 문자열을 비교할 때 공백(BLANK)을 채 워서 비교하는 방법을 사용
       - 예) CHAR 유형 'AA' = 'AA '
     - VARCHAR 유형에서 는 맨 처음부터 한 문자씩 비교하고 공백도 하나의 문자로 취급하므로 끝의 공백이 다르면 다른 문자로 판단한다
       - 예) VARCHAR 유형 'AA' ≠ 'AA '
       -

2. CREATE TABLE
   - 테이블 생성에 대해 배우는 섹션
   - 테이블과 칼럼 정의
     - 데이터를 고유하게 식별할 수 있으면서 반드시 값이 존재해야하는 단일 칼럼이나 칼럼의 조합들 중 하나를 선정하여 기본키로 지정한다
       - 단일 칼럼이 아닌 여러개의 칼럼으로 만들어질 수 있다
       - 테이블간의 관계는 PK와 FK를 통해 정의한다
   - CREATE TABLE
     - 테이블을 생성하는 SQL문이다

```sql
CREATE TABLE 테이블이름 (
 칼럼명1 DATATYPE [DEFAULT 형식],
  칼럼명2 DATATYPE [DEFAULT 형식],
   칼럼명2 DATATYPE [DEFAULT 형식]
    );
```

- 테이블 생성시 주의해야할 규칙
  - 테이블명은 객체를 의미할 수 있는 적절한 이름을 사용
  - 다른 테이블과 이름이 중복X
  - 한 테이블 내에서는 칼럼명 중복X
  - 테이블 이름을 지정하고 각 칼럼들은 `()`로 묶어 지정한다
  - 각 칼럼들은 `,`로 구분되고 테이블 생성문의 끝은 항상 세미콜론 `;`로 끝난다
  - 칼럼에 대해서는 데이터 표준화 관점에서 일관성 있게 사용하는 것이 좋다
  - 칼럼 뒤에 데이터 유형은 반드시 지정되어야한다
  - 사전에 정의한 예약어는 쓸 수 없다
  - 테이블명, 칼럼명은 반드시 문자로 시작해야한다
  - 벤더별로 길이에 대한 한계가 있다
  - A-Z, a-z, 0-9, \_, $, # 문자만 허용된다.
- 예문

```sql
CREATE TABLE PLAYER (
PLAYER_ID CHAR(7) NOT NULL,
PLAYER_NAME VARCHAR(20) NOT NULL,
TEAM_ID CHAR(3) NOT NULL,
E_PLAYER_NAME VARCHAR(40),
NICKNAME VARCHAR(30),
JOIN_YYYY CHAR(4),
POSITION VARCHAR(10),
BACK_NO TINYINT,
NATION VARCHAR(20),
BIRTH_DATE DATE,
SOLAR CHAR(1),
HEIGHT SMALLINT
WEIGHT SMALLINT
CONSTRAINT PLAYER_PK PRIMARY KEY (PLAYER_ID),
CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID) );
```

- 추가적인 주의사항

  - 테이블 생성시 대/소문자 구분은 하지 않는다(기본적으로 대문자)
  - DATETIME은 별도로 크기를 지정하지 않는다
  - 반드시 가질 수 있는 최대 길이를 표시해야한다
  - 칼럼과 칼럼의 구분은 콤마로 하되, 마지막 칼럼은 콤마를 찍지 않는다
  - 칼럼에 대한 제약조건은 `CONSTRAINT`로 추가할 수 있다

- 제약조건 (`CONSTRAINT`)

  - 데이터 무결성을 유지하기 위한 보편적인 방법
  - 특정 칼럼에 설정하는 제약
  - 초기 테이블 생성 시점부터 적합한 제약조건을 검토해야한다

  1. PRIMARY KEY
     1. 지정된 행 데이터를 고유하게 식별하기 위한 키를 정의
     2. 하나의 테이블에는 하나의 기본키 제약만 정의할수 있다
     3. 제약을 정의하면 자동으로 유니크 인덱스를 생성한다
     4. 기본키에는 NULL을 입력할 수 없다
  2. UNIQUE KEY
     1. 고유키를 정의
     2. NULL은 고유키 제약대상은 아니다
  3. NOT NULL
     1. NULL의 입력을 금지한다
     2. 모든 칼럼의 디폴트는 NULL이지만 이 제약을 지정하면 해당 칼럼은 필수 입력값이 된다
  4. CHECK
     1. 입력할 수 있는 값의 범위를 제한한다
     2. TRUE or FALSE로 평가할 수 있는 논리식을 지정한다
  5. FOREIGN KEY
     1. 테이블 간의 관계 정의를 위해 기본키를 다른 테이블의 외래키로 복사할때 생성된다
     2. 무결성 제약 옵션을 선택할 수 있다

- NULL의 의미

  - 공백이나 0과 다른 값
  - 공집합과 다른 값
  - 아직 정의되지 않은 미지의 값 || 현재 데이터를 입력하지 못하는 경우

- DEFAULT의 의미

  - 기본값을 사전에 설정해줄 수 있다
  - 명시된 값을 지정하지 않을 경우에 NULL값이 입력된다
  - 정의했다면, NULL이 아닌 설정한 기본값이 자동으로 입력된다

- 생성된 테이블 구조 홥인

  - 생성한 테이블의 구조를 확인하려면 `DESCRIBE 테이블명` 혹은 `DESC 테이블명` 명령어를 사용하면 된다

- SELECT 문장을 통한 테이블 생성 사례
  - DML 문장 중에 SELECT 문장을 활용해 테이블을 생성할 수 있는 방법이 있다
  - CTAS: Create Table ~ As Select ~
    - 이 방법을 통해 복제 테이블을 생성할 수 있다
    - 단, 제약조건은 사라진다
    - 이를 추가하기 위해서는 ALTER TABLE 기능을 사용해야 한다
  - Select ~ Into ~ 를 활용하여 테이블을 생성할 수 있다

3. ALTER TABLE
   - 한번 생성된 테이블은 구조변경을 하기전까지 유지된다
   - 이 구조를 유지하는 것이 최선
   - 그러나 구조를 변경해야 할때는 ALTER TABLE을 사용한다

- ADD COLUMN

  - 기존 테이블에 필요한 칼럼을 추가하는 명령이다

  ```sql
  ALTER TABLE 테이블명
  ADD 추가할 칼럼명 데이터 유형;
  ```

  - 예문

  ```sql
  ALTER TABLE PLAYER
  ADD ADDRESS VARCHAR(80);
  ```

- DROP COLUMN

  - 필요 없는 칼럼을 삭제할 수 있으며, 데이터가 있건 없건 삭제 가능하다
  - 한번에 하나의 칼럼만 삭제할수 있다
  - 칼럼 삭제 후 최소 하나의 칼럼이 테이블에 존재해야한다
  - 한번 삭제된 칼럼은 복구가 불가능하다

  ```sql
  ALTER TABLE 테이블명
  DROP COLUMN 삭제할 칼럼명;
  ```

  - 예문

  ```sql
  ALTER TABLE PLAYER
  DROP COLUMN ADDRESS;
  ```

- MODIFY COLUMN

  - 데이터 유형, 디폴트 값, NOT NULL 제약조건에 대해 변경할 수 있다

  ```sql
  ALTER TABLE 테이블명
  ALTER (칼럼명1 데이터 유형 [DEFAULT 식] [NOT NULL],
  칼럼명2 데이터 유형 ...);
  ```

  - 예문
    - TEAM 테이블의 ORIG_YYYY 칼럼의 데이터 유형을 CHAR(4)→VARCHAR2(8)으로 변경
    - 향후 입력되는 데이터의 DEFAULT 값으로 '20020129'을 적용
    - 모든 행의 ORIG_YYYY 칼럼에 NULL이 없으므로 제약조건을 NULL → NOT NULL로 변경

  ```sql
  ALTER TABLE TEAM_TEMP
  ALTER COLUMN ORIG_YYYY VARCAHR(8) NOT NULL;

  ALTER TABLE TEAM_TEMP
  ADD CONSTRAINT DF_ORIG_YYYY DEFAULT '20020129' FOR ORIG_YYYY;
  ```

  - 주의해야 할 점

    - 해당 칼럼의 크기를 늘릴 수는 있지만 줄이지 못한다
      - NULL 값만 가지고 있거나 테이블에 아무 행도 없으면 칼럼의 폭을 줄일 수 있다
    - 해당 칼럼이 NULL 값만 가지고 있다면 데이터 유형도 변경할 수 있다
      - 그렇지 않다면 변경할 수 없다
    - DEFAULT 값을 변경하면, 변경작업 이후에 발생하는 행 삽입에만 영향을 미친다
    - NULL값이 없을 경우에만 NOT NULL 제약조건을 추가할 수 있다

- RENAME COLUMN

  - 칼럼명을 변경해야 할 경우 쓰이는 문구다
  - ANSI/ISO 에 명시된 기능이 아니며 오라클 등 일부 DBMS에서만 지원한다

  ```sql
  ALTER TABLE 테이블명
  RENAME COLUMN 변경해야 할 칼럼명 TO 새로운 칼럼명;
  ```

- DROP CONSTRAINT

  - 테이블 생성 시 부여했던 제약조건을 삭제하는 구문

  ```sql
  ALTER TABLE 테이블명
  DROP CONSTRAINT 제약조건명;
  ```

  - 예문

  ```sql
  ALTER TABLE PLAYER
  DROP CONSTRAINT PLAYER_FK;
  ```

- ADD CONSTRAINT

  - 생성 이후에 필요할때 제약조건을 추가하는 구문

  ```sql
  ALTER TABLE 테이블명
  ADD CONSTRAINT 제약조건명 제약조건 (칼럼명);
  ```

  - 예문

  ```sql
  ALTER TABLE PLAYER
  ADD CONSTRAINT PLAYER_FK FOREIGN KEY (TEAM_ID) REFERENCES TEAM(TEAM_ID);
  ```

- RENAME TABLE

  - 테이블의 이름을 변경할 수 있다

  ```sql
  RENAME 변경전 테이블명
  TO 변경후 테이블명;
  ```

  - 예문

  ```sql
  RENAME TEAM
  TO TEAM_BACKUP;
  ```

- DROP TABLE

  - 테이블이 필요없을 경우 삭제한다
  - 본 구문은 테이블의 모든 데이터 및 구조를 삭제한다
  - CASCADE CONSTRAINT 옵션은 해당 테이블과 관계가 있던 참조되는 제약조건에 대해서도 삭제한다는 것을 의미한다

  ```sql
  DROP TABLE 테이블명 [CASCADE CONSTRAINT];
  ```

  - 예문

  ```sql
  DROP TABLE PLAYER;
  ```

- TRUNCATE TABLE
  - 테이블이 자체가 삭제되는 것이 아니라,
  - 해당 테이블에 들어있던 모든 행들이 제거되고 저장 공간을 재사용 가능하도록 해제한다
  - DROP TABLE은 테이블 자체가 없어지기 때문에 테이블 구조를 확인할 수 없다
  - 한편, 트렁케이트 테이블은 테이블 구조를 냅두고 데이터만 전부 삭제하는 기능이다
  - DELETE TABLE보다 시스템 부하가 적다(권고한다)
  - 주기적으로 테이블 정보를 초기화해야할때 유용할듯
  - 예문
  ```sql
  TRUNCATE TABLE PLAYER;
  ```

# DML(DATA MANIPULATION LANGUAGE )

- 만들어진 테이블에 관리하기 원하는 자료들을 입력,수정,삭제,조회하는 SQL

1. INSERT

   - 테이블에 데이터를 입력하는 구문이다
   - 해당 칼럼명과 입력되어야 하는 값을 1:1로 매핑해서 입력한다
   - 문자 유형일 경우 `''`로 입력한다
   - 숫자일 겨웅 `''`을 붙이지 않는다
   - 다음과 같이 두가지 유형이 있다

   ```sql
   ▶ 첫번째 유형
   INSERT INTO 테이블명 (COLUMN_LIST)
   VALUES (COLUMN_LIST에 넣을 VALUE_LIST);
   ▶ 두번째 유형
   INSERT INTO 테이블명
   VALUES (전체 COLUMN에 넣을 VALUE_LIST);
   ```

   - 첫번째 유형
     - 테이블의 칼럼을 정의할 수 있다
     - 이 때, 테이블의 칼럼 순서와 매치할 필요는 없다
     - 정의하지 않은 칼럼은 디폴트값으로 `NULL`이 입력된다
     - PK나 NOT NULL인 칼럼은 `NULL`이 허용되지 않는다
     - 예문
     ```sql
     INSERT INTO PLAYER(PLAYER_ID, PLAYER_NAME, TEAM_ID, POSITION, HEIGHT, WEIGHT, BACK_NO)
     VALUES ('2002007', '박지성', 'K07', 'MF', 178, 73, 7);
     ```
   - 두번째 유형
     - 테이블 상의 칼럼 순서대로 빠짐없이 데이터가 입력되어야한다
     - 예문

   ```sql
   INSERT INTO PLAYER
   VALUES ('2002010','이청용','K07','','BlueDragon','2002','MF','17',NULL, NULL,'1',180,69);
   ```

   - 이 유형에서 정의되지 않은 미지의 값의 경우 `''`으로 표현하거나 NULL로 표현한다

2. UPDATE

   - 정보를 수정해야 할 때 사용하는 구문이다
   - UPDATE 뒤에 테이블명, SET 뒤에 수정할 칼럼명과 수정값을 다음과 같이 표현한다

   ```sql
   UPDATE 테이블명
   SET 수정되어야 할 칼럼명 = 수정되기를 원하는 새로운 값;
   ```

   - 예문 : 선수 테이블의 백넘버를 일괄적으로 99로 수정하는 예문이다

   ```sql
   UPDATE PLAYER
   SET BACK_NO = 99;
   ```

3. DELETE

   - 데이터를 삭제하는 구문이다

   ```sql
   DELETE [FROM] 삭제를 원하는 정보가 들어있는 테이블명;
   ```

   - 예문 : 선수 테이블의 데이터를 전부 삭제한다

   ```sql
   DELETE FROM PLAYER;
   ```

   - DDL은 데이터베이스의 테이블에 직접적으로 영향을 미친다
     - 따라서 해당하는 작업이 즉시(AUTO COMMIT) 완료된다
   - DML은 조작하려는 테이블을 메모리 버퍼에 올려놓고 작업한다
     - 이는 테이블에 실시간으로 영향을 미치지 않는다
     - 따라서 버퍼에서 처리한 DML을 테이블에 반영하기 위해서는 `COMMIT` 명령어를 통해 트랜잭션을 종료해야한다
   - SQL 서버는 DML도 `AUTO COMMIT`으로 처리한다
     - 따라서 따로 `COMMIT`을 입력할 필요는 없다
   - 테이블의 전체 데이터를 삭제하는 경우, 시스템 활용측면에서 `DELETE`보다는 `TRUNCATE`를 권고한다
     - `DELETE` : 삭제된 데이터를 로그로 저장한다
     - `TRUNCATE` : 삭제된 데이터의 로그가 없으므로 `ROLLBACK`이 불가능하다

4. SELECT
   - 입력한 자료들을 조회하는 구문이다
   ```sql
   SELECT [ALL/DISTINCT] 보고 싶은 칼럼명, 보고 싶은 칼럼명, ...
   FROM 해당 칼럼들이 있는 테이블명;
   ```
   - ALL : Default 옵션이므로 별도로 표시하지 않아도 된다. 중복된 데이터가 있어도 모두 출력한다.
   - DISTINCT : 중복된 데이터가 있는 경우 1건으로 처리해서 출력한다.
   - 예문 : 선수들의 데이터 조회
   ```sql
   SELECT PLAYER_ID, PLAYER_NAME, TEAM_ID, POSITION, HEIGHT, WEIGHT, BACK_NO
   FROM PLAYER;
   ```
   - 예문 : 선수들의 포지션 종류 조회 ( `DISTINCT`로 중복되는 값을 1건으로 처리하여 조회)
   ```sql
   SELECT DISTINCT POSITION
   FROM PLAYER;
   ```
   - 예문 : `*` 와일드카드를 사용해 조회
     - `*` (애스터리스크)를 사용하면 테이블의 모든 칼럼 데이터를 조회할 수 있다
   ```sql
   SELECT *
   FROM 테이블명;
   ```
   - 예문 : ALIAS 부여하기
   - 조회된 결과에 일종의 별명을 부여해서 칼럼 레이블을 변경할 수 있다
   - `ALIAS`
     - 칼럼의 별명
     - 칼럼명 바로 뒤에 온다
     - 칼럼명과 `ALIAS` 사이에 AS,as 키워드를 사용할 수도 있다
     - 쌍따옴표 `""`는 ALIAS가 공백,특수문자를 포함할 경우와 대소문자 구분이 필요할 경우 사용된다
   - 다음은 입력한 선수들의 정보를 칼럼 별명을 이용하여 출력하는 예문이다
   ```sql
   SELECT PLAYER_NAME 선수명, POSITION 위치, HEIGHT 키, WEIGHT 몸무게
   FROM PLAYER;
   > 공백이 들어갈 경우 `""`, `''`,`[]`등으로 별명을 부여할 수 있다
   SELECT PLAYER_NAME "선수 이름", POSITION "그라운드 포지션", HEIGHT "키", WEIGHT "몸무게"
   FROM PLAYER;
   ```
5. 산술 연산자와 합성 연산자
   - 산술 연산자
     - NUMBER와 DATE 자료형에 대해 적용된다
     - 수학에서의 4칙 연산과 동일하다
     - 우선순위를 위한 괄호 적용이 가능하다
     - 적절한 ALIAS를 새롭게 부여하는 것이 좋다
     - 예문 : 선수들의 BMI를 측정한다
     ```sql
     SELECT PLAYER_NAME 이름, ROUND(WEIGHT/((HEIGHT/100)*(HEIGHT/100)),2) "BMI 비만지수"
     FROM PLAYER;
     ```
   - 합성 연산자
     - 문자와 문자를 연결하는 연산자다
     - SQL 문장만으로도 유용한 리포트를 출력할 수 있다
     - 문자와 문자를 연결하는 경우
       - 오라클 : 2개의 수직바 `||`에 의해 이루어진다
       - SQL 서버 : `+`에 의해 이루어진다
       - `CONCAT(string1,string2)` 함수를 사용할 수 있다
       - 칼럼과 문자 또는 다른 칼럼과 연결시킨다
       - 문자 표현식의 결과에 의해 새로운 칼럼을 생성한다
     - 다음과 같은 결과값이 얻고 싶은 상황이다
     ```
     출력 형태) 선수명 선수, 키 cm, 몸무게 kg
     예) 박지성 선수, 176 cm, 70 kg
     ```
     - 예문(sql서버)
     ```sql
     SELECT PLAYER_NAME +'선수, '+ HEIGHT +'cm, '+ WEIGHT +'kg'체격정보
     FROM PLAYER;
     ```
     - 근데 이 sql문은 실제로 해보니 잘 되지 않는다. 다음과 같은 에러가 뜨는데, 나중에 다시 시도해봐야겠다
     ```
     Truncated incorrect DOUBLE value: '박지성'
     Truncated incorrect DOUBLE value: '선수'
     ```

# TCL(TRANSACTION CONTROL LANGUAGE)

# WHERE 절

1. where 조건절 개요
   - 원하는 자료를 검색하기 위한 조건절이다
   - where 절에서는 두 개 이상의 테이블에 대한 조인 조건이나 결과를 제한하기 위한 조건을 기술할 수도 있다
   - where절은 조회하려는 데이터에 특정 조건을 부여할 목적으로 사용하기 때문에 다음과 같이 FROM절 뒤에 오게 된다

```sql
SELECT [DISTINCT/ALL] 칼럼명 [ALIAS명]
FROM 테이블명
WHERE 조건식;
```

- WHERE 절의 조건식은 아래 내용으로 구성된다
  - 칼럼명(보통 조건식의 좌측 위치)
  - 비교 연산자
  - 문자,숫자,표현식(보통 조건식의 우측에 위치)
  - 비교 칼럼명(JOIN사용시)

2. 연산자의 종류

- 비교 연산자

  - `=`
    - 같다
  - `>`
    - 보다 크다
  - `>=`
    - 보다 크거나 같다
  - `<`
    - 보다 작다
  - `<=`
    - 보다 작거나 같다

- SQL 연산자
  - `BETWEEN a AND b`
    - a와 b의 값 사이에 잇으면 된다(a와 b값 포함)
  - `IN(list)`
    - 리스트에 있는 값 중에서 어느 하나라도 일치하면 된다
  - `LIKE`
    - 비교문자열과 형태가 일치하면 된다.(%,\_사용)
  - `IS NULL`
    - NULL 값인 경우
- 논리 연산자
  - `AND`
    - 앞에 있는 조건과 뒤에 오는 조건이 참이되면 결과도 참이 된다 즉 앞의 조건과 뒤의 조건을 동시에 만족해야한다
  - `OR`
    - 앞의 조건이 참이거나 뒤의 조건이 참이 되어야 결과도 결과도 참이 된다. 즉 앞뒤 조건 중 하나만 참이면 된다
  - `NOT`
    - 뒤에 오는 조건에 반대되는 결과를 돌려준다
- 부정 비교 연산자
  - `!=`
    - 같지 않다
  - `^=`
    - 같지 않다
  - `<>`
    - 같지 않다(ISO 표준, 모든 운영체제에서 사용 가능)
  - `NOT 칼럼명 =`
    - ~와 같지 않다
  - `NOT 칼럼명 >`
    - ~보다 크지 않다
- 부정 SQL 연산자
  - `NOT BETWEEN a AND b`
    - a와 b의 값 사이에 있지 않다( a,b값을 포함하지 않는다)
  - `NOT IN`
    - list 값과 일치하지 않는다
  - `IS NOT NULL`
    - NULL 값을 갖지 않는다
- 연산자의 우선순위
  1. 괄호
  2. NOT 연산자
  3. 비교 연산자, SQL 비교연산자
  4. AND
  5. OR

3. 비교 연산자
   - 칼럼들을 특정한 값들과 조건을 비교하는데 사용할 수 있었다
   - 예문
   ```sql
   SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
   FROM PLAYER
   WHERE TEAM_ID = 'KO2'
   WHERE POSITION = 'MF'
   ```
   - 문자 유형의 칼럼은 다음과 같이 ''처리를 해줘야 한다
   - 숫자 유형의 칼럼은 숫자로 변환이 가능한 문자열과 비교되면 상대 타입을 숫자 타입으로 바꾸어 비교한다
4. SQL 연산자

   - SQL 문장에서 사용하도록 예약되어있는 연산자
   - 모든 데이터 타입에 있어서 다음과 같은 종류가 있다
     - `BETWEEN a AND b`
       - a와 b의 값 사이에 잇으면 된다(a와 b값 포함)
     - `IN(list)`
       - 리스트에 있는 값 중에서 어느 하나라도 일치하면 된다
     - `LIKE`
       - 비교문자열과 형태가 일치하면 된다.(%,\_사용)
     - `IS NULL`
       - NULL 값인 경우
   - `IN` 연산자 활용
     - 예문
     ```sql
     SELECT ENAME,JOB,DEPTNO
     FROM EMP
     WHERE (JOB,DEPTNO) IN (('MANAGER',20),('CLERK',30))
     ```
     - 다중 리스트를 이용한 `IN` 연산자는 SQL 문장을 짧게 만들어 주면서 성능 측면에서도 장점을 가질 수 있는 연산자다
   - `LIKE` 연산자 활용
     - 예문
     ```sql
       SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
       FROM PLAYER
       WHERE PLAYER_NAME LIKE '장%'
     ```
     - 다음 예문은 '장'씨 성을 가진 선수들의 정보를 조회하는 WHERE 절을 작성한 것이다
     - `%` 와일드카드를 사용하면 다음과 같이 '장'으로 시작하는 이름을 가진 선수들의 정보를 조회할 수 있다
     - 와일드카드
       - 한개 혹은 0개 이상의 문자를 대신해서 사용하기 위한 특수 문자를 의미한다
       - SQL 문장에서 사용하는 STRING 값으로 용이하게 사용할 수 있다
       - `%` 와일드카드
         - 0개 이상의 어떤 문자를 의미한다
       - `_` 와일드카드
         - 1개인 단일 문자를 의미한다
   - `BETWEEN a AND b` 연산자
     - 예문
       ```sql
        SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
        FROM PLAYER
        WHERE HEIGHT BETWEEN 170 AND 180;
       ```
     - 다음 예문에서 범위는 170과 180을 포함하는 것을 의미한다
   - `IS NULL`
     - `NULL`은 값이 존재하지 않는 것
     - 확정되지 않은 값을 표현할때 사용한다
     - 공백이나 0과 같은 값과 비교 자체가 불가능한 값이다
       - `NULL` 값과의 수치연산은 NULL 값을 리턴한다
       - `NULL` 값과의 비교연산은 거짓(`FALSE`)을 리턴한다
       - 어떤 값과 비교할 수도 없다
       - 특정값보다 크다 적다라는 표현을 할 수도 없다
     - 따라서 NULL 값의 비교는 비교연산자를 통해서 비교할 수 없다
     - 비교한다 해도 `FALSE`를 리턴한다
     - NULL 값의 비교 연산은 `IS NULL` 혹은 `IS NOT NULL`이라는 정해진 문구를 사용해야 제대로 된 결과를 얻을 수 있다
     - 예문

   ```sql
    SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
    FROM PLAYER
    WHERE POSTION = NULL;
    ## 다음 구문은 선택된 레코드가 없다는 메시지를 출력한다

    SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
    FROM PLAYER
    WHERE POSTION IS NULL;
    ## 한편 다음과 같이 IS NULL 연산자를 사용한다면 포지션값이 없는 선수의 데이터를 조회할 수 있는 것이다
   ```

5. 논리 연산자

   - 논리 연산자는 비교 연산자나 SQL 연산자로 이루어진 여러 개의 **조건**들을 논리적으로 연결시키기 위해 사용되는 연산자다
   - 논리 연산자
     - `AND`
       - 앞에 있는 조건과 뒤에 오는 조건이 참이되면 결과도 참이 된다 즉 앞의 조건과 뒤의 조건을 동시에 만족해야한다
     - `OR`
       - 앞의 조건이 참이거나 뒤의 조건이 참이 되어야 결과도 결과도 참이 된다. 즉 앞뒤 조건 중 하나만 참이면 된다
     - `NOT`
       - 뒤에 오는 조건에 반대되는 결과를 돌려준다
   - 예문

   ```sql
   SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
   FROM PLAYER
   WHERE TEAM_ID = 'KO2' OR TEAM_ID = 'K07'
   AND HEIGHT >= 170
   AND POSTION = 'MF';
   ```

   - 다음 예문에서는 팀 아이디에 대한 `OR` 연산자 사용에 있어서 괄호 처리를 안했기 때문에 팀 아이디가 해당 값인 정보들이 전부 불러와지면서 이후의 `AND` 연산이 의미가 없어졌다
   - 논리 연산자의 처리 우선순위는 `()`,`NOT`,`AND`,`OR`이기 때문에 위의 경우 괄호처리를 다음과 같이 해줘야한다
   - 수정 예문

   ```sql
   SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
   FROM PLAYER
   WHERE (TEAM_ID = 'KO2' OR TEAM_ID = 'K07')
   AND HEIGHT >= 170
   AND POSTION = 'MF';
   ```

   - 이 부분은 typeORM에서는 bracket을 활용하면 되지 않을까 싶다

6. 부정 연산자
   - ![](부정연산자종류.png)
   - 비교 연산자, SQL 비교 연산자에 대한 부정 표현을 부정 연산자로 할 수 있다
   - 예문
   ```sql
   SELECT PLAYER_NAME, POSITION, BACK_NO, HEIGHT
   FROM PLAYER
   WHERE TEAM_ID = 'KO2'
   AND NOT HEIGHT BETWEEN 175 AND 185
   AND NOT POSTION = 'MF';
   ## 포지션이 미드필더가 아니고 키가 175 이상 185 이하가 아닌 선수들의 자료를 조회하는 구문
   ```
7. ROWNUM, TOP 사용

   - `ROWNUM`
     - 오라클의 `ROWNUM`은 칼럼과 비슷한 성격의 Pseudo Column으로 SQL 처리 결과 집합의 각 행에 대해 임시로 부여되는 일련번호다
     - 테이블이나 집합에서 원하는 만큼의 행만 가져오고 싶을 때 WHERE 절에서 행의 개수를 제한하는 목적으로 사용된다
     - 예문

   ```sql
   SELECT PLAYER_NAME
   FROM PLAYER
   WHERE ROWNUM=1;
   혹은
   WHERE ROWNUM<=1;

   ## N건의 행을 가져오고 싶을 떄는
   WHERE ROWNUM<=N;
   ```

   - 위와 같이 출력되는 행의 한계를 지정할 수 있다
   - 추가적으로 테이블 내의 고유한 키나 인덱스 값을 만들 수 있다

- `TOP`
  - 결과 집합으로 출력되는 행의 수를 제한할수 있다
  - 사용법
    ```sql
    TOP (Expression) [PERCENT][WITH TIES]
    ```
    - Expression
      - 반환할 행의 수를 지정하는 숫자
    - PERCENT
      - 쿼리 결과의 집합에서 처음 Expression의 행만 반환됨을 나타낸다
    - WITH TIES
      - `ORDER BY`절이 지정된 경우에만 사용할 수 있으며, `TOP N`의 마지막 행과 같은 값이 있는 경우 추가 행이 출력되도록 지정할 수 있다
  - 한건의 행만 가져오고 싶을 때 예문
    ```sql
    SELECT TOP(1) PLAYER_NAME
    FROM PLAYER
    ```
  - 두건 이상의 N 행을 가져오고 싶을 때 예문
    ```sql
    SELECT TOP(N) PLAYER_NAME
    FROM PLAYER
    ```

# 함수(FUNCTION)

# GROUP BY, HAVING 절

# 조인(JOIN)
