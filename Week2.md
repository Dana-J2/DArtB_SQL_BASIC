# SQL_BASIC 2주차 정규 과제 

📌SQL_BASIC 정규과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고 간단한 문제를 풀면서 학습하는 것입니다. 이번주는 아래의 **SQL_Basic_2nd_TIL**에 나열된 분량을 수강하고 `학습 목표`에 맞게 공부하시면 됩니다.

**2주차 과제**는 1주차 과제처럼 SQL의 필요성이나 느낀점 위주가 아닌, **실제 강의 내용을 바탕으로 개념을 정리하고 학습한 내용을 집중적으로 기록**해주세요. 완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요. 

**👀(수행 인증샷은 필수입니다.)** 

## SQL_BASIC_2nd

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

### 2-4. SELECT 연습문제

### 2-5. 집계 (Group By + Having + Sum/Count)



## 🏁 강의 수강 (Study Schedule)

| 주차  | 공부 범위              | 완료 여부 |
| ----- | ---------------------- | --------- |
| 1주차 | 섹션 **1-1** ~ **2-2** | ✅         |
| 2주차 | 섹션 **2-3** ~ **2-5** | ✅         |
| 3주차 | 섹션 **2-6** ~ **3-3** | 🍽️         |
| 4주차 | 섹션 **3-4** ~ **4-4** | 🍽️         |
| 5주차 | 섹션 **4-4** ~ **4-9** | 🍽️         |
| 6주차 | 섹션 **5-1** ~ **5-7** | 🍽️         |
| 7주차 | 섹션 **6-1** ~ **6-6** | 🍽️         |

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념정리 

## 2-3. 데이터 탐색 (SELECT, FROM, WHERE)

~~~
✅ 학습 목표 :
* SQL 쿼리 구조를 이해할 수 있다. 
* SELECT, FROM, WHERE의 핵심 문법을 설명할 수 있다. 
~~~

### [ **SQL 기본 쿼리 구조 : *SELECT, FROM, WHERE***]
~~~sql
SELECT
    Col1 as new_name,    
    Col2
    Col3
FROM Datatset.Table
WHERE
    Col1 = 1    
~~~

1. **`FROM`** : 어떤 테이블에서 데이터를 확인할 것인가  
    ex) basic.pokemon : 데이터셋은 basic, 테이블은 pokemon
2. **`WHERE`** : 원하는 조건이 있다면 어떤 조건인가
    - WHERE 아래에 조건문 걸기
3. **`SELECT`** : 테이블의 어떤 컬럼을 선택(출력)할 것인가
    - **as** : Col1의 이름을 new_name으로 바꾸겠다 
    - **\*** : 모든 컬럼을 출력하겠다 (단, 비용이 많이 들 수 있음에 주의)
    - **\* EXPECT** : 제외할 컬럼  (ex: 컬럼 50개 중에 2개만 제외하고 싶을 때)


✅ 문법 순서는 'SELECT > FROM > WHERE'이지만   
**해석, 실행 순서는 'FROM > WHERE > SELECT'**  

⚠️ <u>*데이터가 여러 장소에 저장되어 있는 경우*</u>  
: 특정 Table에 있는 데이터를 각각 추출 후, **연결하기(JOIN)**

<br>

### [ 💻 코드 실습 ]
~~~SQL
SELECT 
  id AS pokemon_id, 
  kor_name, 
  type1,
  total
FROM `exercise-bigquery-489314.Basic.pokemon` 
WHERE 
  type1 = "Fire"; 
~~~

- `SELECT`절 AS 뒤에 오는 컬럼이름에 따옴표 넘어주지 않음!
- `exercise-bigquery-489314` : 프로젝트 ID
- `Basic` : dataset
- `pokemon` : table
- 프로젝트ID는 프로젝트가 단일인 경우 필요없을 수 있음 
- 단, 프로젝트를 여러개 사용한다면 명시하는 것이 좋음  
  &nbsp; <=> 쿼리를 실행할 때 어떤 프로젝트인지 확인하는 과정이 존재
- 프로젝트 ID를 제외하고 작성할 때는 ``(backthick) 없어도 괜찮음
- 데이터 활용 목적에 따라 SELECT문에서 볼 컬럼 선택해야 한다   

<br>

~~~SQL
SELECT 
  id AS pokemon_id,  # AS는 별칭을 지어줄 때 사용, 컬럼이름에 따옴표 넘어주지 않음!
  kor_name, 
  type1,
  total
FROM `exercise-bigquery-489314.Basic.pokemon` 
WHERE 
  type1 = "Fire";

SELECT 
  id
FROM `exercise-bigquery-489314.Basic.pokemon`;
~~~
- 2개의 쿼리 동시에 실행할 때, **각각의 쿼리를 *`;`*로 마무리**
- 여러개의 쿼리 중 **특정 쿼리만 실행**하고 싶을때 `드래그 + command + Enter`

<br>

## 2-4. SELECT 연습문제

### 문제 1️⃣ trainer 테이블에 있는 모든 데이터를 보여주는 SQL 쿼리?
~~~sql
SELECT 
    *
FROM Basic.trainer
~~~

### 문제 2️⃣ trainer 테이블의 name 컬럼을 보여주는 SQL 쿼리?
~~~sql
SELECT 
    name
FROM Basic.trainer
~~~

### 문제 3️⃣ trainer 테이블의 name, age 컬럼을 보여주는 SQL 쿼리?
~~~sql
SELECT
  name,
  age
FROM Basic.trainer;
~~~

### 문제 4️⃣ trainer 테이블에서 id가 3인 트레이너의 name, age, hometown을 출력하는 쿼리? 
~~~sql
SELECT
  name,
  age,
  hometown
FROM Basic.trainer
WHERE 
  id = 3 ;
~~~


### 문제 5️⃣
~~~sql
SELECT
  hp,
  attack
FROM Basic.pokemon
WHERE 
  kor_name = "피카츄";
~~~


<br>


## 2-5. 집계 (Group By / HAVING / SUM,COUNT)

~~~
✅ 학습 목표 :
* 데이터를 집계하고 그룹화하는 방법을 설명할 수 있다.
* GROUP BY, HAVING, ORDER BY, 집계함수(SUM/COUNT 등)을 활용하는 방법을 설명할 수 있다.
* having과 where의 차이에 대해서 설명할 수 있다.
~~~

###  [**집계**]
***"집계하다"*** : 모아서(***그룹화***) 계산하다  
\>> **계산** : 더하기, 빼기 / 최대값, 최솟값 / 평균 / 갯수 세기

### `GROUP BY` 
: 같은 값끼리 모아서 그룹화 한다  
- 특정 컬럼을 기준으로 모으면서 **다른 컬럼에서는 집계 가능**  
    ex) 포켓몬 타입 기준으로 그룹화해서 평균 공격력, 타입별 포켓몬 수 집계

~~~SQL
SELECT 
    집계할컬럼
    집계함수(COUNT,MAX,MIN 등)
FROM Table
GROUP BY 
    집계할컬럼
~~~
- 집계할 컬럼을 SELECT에 명시하고 그 컬럼을 **꼭 GROUP BY에 작성**
 
|  도형 ID | 색상 |          
| ------- | --- |          
| 1      | RED | 
| 2      | RED | 
| 3      | BLUE | 
| 4      | BLUE | 
| 5      | GREEN | 
| 6     | PINK | 

➡️ 색상 기준으로 **GROUP BY**한 결과
| 색상 |          
| --- |          
| RED | 
| BLUE | 
|  GREEN | 
| PINK | 

<br> 

### `DISTINCT` 
: 여러 값 중에 **Unique** 한 것만 보고싶은 경우 사용  
 &nbsp; &nbsp;   => **중복을 제거**하는 것
~~~SQL
SELECT 
    집계할컬럼
    COUNT(DISTINCT count할컬럼)
FROM Table
GROUP BY 
    집계할컬럼
~~~

𝑸. <u>*메인 페이지의 view수와 메인페이지 view한 유저의 수를 구하라*</u>  

| user_id  | event            | event_date |
| ----- | ---------------------- | --------- |
| 1 | view_main_page | 2024-04-02  |
| 1 | view_main_page | 2024-04-02  |
| 2 | view_main_page | 2024-04-02  |
| 3 | view_main_page | 2024-04-02 |

- *메인 페이지의 view수*  
    : COUNT(user_id)
- *메인페이지 view한 유저의 수*  
    : COUNT(**DISTINCT** user_id) 

<br>

### `HAVING` 
⚠️ `WHERE`와의 차이  
- `WHERE`는 table의 **raw data**에 바로 조건을 설정하고 싶은 경우
- `HAVING` **GROUP BY한 후**에 조건을 설정하고 싶은 경우 (즉, GROUP BY랑 같이 쓰임)
~~~sql
SELECT 
    컬럼1, 컬럼2,
    COUNT(컬럼1 AS col1_count)
FROM Table
GROUP BY 컬럼1, 컬럼2
HAVING 
    col1_count > 3
~~~

### ➕ **서브쿼리**
: SELECT문 안에 존재하는 SELECT 쿼리  
- FROM 절에 또 다른 SELECT문 넣을 수 있음 
- 괄호로 묶어서 사용
- 서브쿼리작성 후 서브쿼리 바깥에서 WHERE 조건 설정 = 서브쿼리에서 HAVING 쓰는 것

<br>

### `ORDER BY`
: 데이터 정렬하기
~~~sql
SELECT 
    컬럼
FROM Table
ORDER BY <컬럼> <순서>
~~~

- `DESC` : 내림차순 / `OSC` : 오름차순(일반적으로 default)
- 쿼리의 맨 마지막(아래)에 두고, 쿼리의 맨 마지막에만 작성하면 됨
- 중간에 있어봤자 연산만 느려지는 격

### `LIMIT`
: 쿼리문 **결과 row 수를 제한**하고 싶은 경우 사용  
~~~sql
SELECT 
    컬럼
FROM Table
LIMIT 10
~~~
- 쿼리문의 제일 마지막에 작성

<br>
<br>


# 2️⃣ 학습 인증란
### 강의수강
![week2-3](https://github.com/Dana-J2/DArtB_SQL_BASIC/blob/main/images/week2_3.png)
### 8강 실습
![week2_1](https://github.com/Dana-J2/DArtB_SQL_BASIC/blob/main/images/week2_1.jpg)
### 9강 실습
![week2-2](https://github.com/Dana-J2/DArtB_SQL_BASIC/blob/main/images/week2_2.jpg)


<br><br>



---

# 3️⃣ 확인문제

## 문제 1

> **🧚Q. 포켓몬 마스터 진아는 포켓몬 데이터 조회하는 SQL문에 재미를 느껴서 혼자서 데이터를 조회하는 쿼리문을 짰습니다. 하지만 세 가지의 오류로 다음 코드가 실행이 안된다고 하는데, 각 오류의 위치와 이유를 설명하고, 올바른 쿼리문으로 수정해보세요.**

~~~sql
# 진아의 SQL Query문 
SELECT name. type
FROM pokemon;
WHERE type = Electric;
~~~



~~~
1. SELECT 절에서 컬럼의 나열은 ',' 기호를 사용해야 한다
2. FROM 절 마지막에 있는 ';'기호는 쿼리 마지막에 사용해야하므로 쿼리 중간에 등장하는 것은 옳지 않다.
3. WHERE 절에서 컬럼의 특정값을 조건으로 걸고자 하는 경우로, 여기서 해당 특정값은 문자 형태이므로 'Electric'과 같이 적어주어야 한다.
~~~
~~~sql
# 올바른 쿼리문  
SELECT 
    name,
    type
FROM pokemon
WHERE type = 'Electric' ; 
~~~



## 문제 2

> **🧚Q. 앞서 SQL Query의 오류를 해결한 진아는 기분 좋게 이번에는 포켓몬 데이터에서 타입별 평균 공격력이 60 이상인 타입만 조회하려는 쿼리를 작성하려고 했습니다. 하지만 이번에도 실수를 하여 쿼리문이 실행되지 않거나 잘못된 결과가 나오고 있는데, 쿼리에서 잘못된 부분이 무엇인지 설명하고, 올바르게 수정한 쿼리를 작성해보세요.**

~~~sql
SELECT type, AVG(attack) AS avg_attack
FROM pokemon
WHERE AVG(attack) >= 60
GROUP BY type;
~~~



~~~
WHERE절은 원본데이터에 적용하는 것으로 현재 원본데이터에는 AVG값이 존재하지 않는다
GROUP BY 결과에 조건을 걸고 싶은 경우 HAVING을 사용하는 것이 적절하다
~~~
~~~SQL
SELECT type, AVG(attack) AS avg_attack
FROM pokemon
GROUP BY type
HAVING avg_attack >= 60;
~~~



### 🎉 수고하셨습니다.
