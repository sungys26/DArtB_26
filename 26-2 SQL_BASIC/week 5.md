# 📘 SQL_BASIC 5주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 날짜/시간 데이터와 조건문을 학습합니다. 특히 `CASE WHEN`은 SQL 문제 풀이와 데이터 분석에서 자주 사용되므로, 직접 분류 기준을 만들고 결과를 확인하는 연습을 해주세요.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_5th_TIL

### 섹션 5. 데이터 탐색 - 변환

### 4-4. 날짜 및 시간 데이터 이해하기

### 4-6. 조건문(CASE WHEN, IF)

---

## ✨ 선택 강의

- 4-5. 시간 데이터 연습문제: 날짜/시간 함수를 더 연습하고 싶을 때 선택 수강
- 4-7. 조건문 연습문제: CASE WHEN과 IF를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | ✅ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | ✅ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- DATE
- DATETIME
- TIMESTAMP
- EXTRACT
- DATETIME_TRUNC
- FORMAT_DATETIME
- CASE WHEN
- IF


## 4.4 날짜 및 시간 데이터 이해하기
### 01. DATE, DATETIME, TIMESTAMP 

```
✅ 세부적으로 나뉘는 시간 데이터 타입의 대표적 타입 이해
```

**[시간 데이터의 대표 타입]**
- **DATE** : 날짜만 표시하는 데이터 (ex. 2026-10-03)
- **DATETIME** : 날짜와 시간을 표시하는 데이터, timezone 정보 없음 (ex.2026-10-03 14:00:00)
- **TIMESTAMP** : 시간만 표시하는 데이터 (ex. 14:17:59)


**타임존의 개념** : 특정 지역의 표준 시간대 확인하기 위한 개념 
- GMT : 영국 그리니치 천문대 기준 (한국시간 GMT+9)
- UTC : 협정 세계시 (한국시간 UTC+9)
  - TIMESTAMP : UTC로부터 경과한 값을 보여주는 값 (ex. 2026-01-01 14:00:00 UTC)
- GMT, UTC 둘은 약간의 차이가 있으나, 그 차이가 매우 미미함


**정밀한 데이터 표기를 위한 개념** - millisecond, microsecond
- **millisecond** : 1/1,000초
- **microsecond** : 1/1,000ms

**쿼리에서의 활용** - 1704176819711ms / 2024-01-02 15:26:59
```sql
SELECT
 TIMESTAMP_MILLIS(1704176819711) AS milli_to_timestamp_value,
 TIMESTAMP_MICROS(170417681971000) AS micro_to_timestamp_value,
 DATETIME(TIMESTAMP_MICROS(170417681971000)) AS datetime_value,
 DATETIME(TIMESTAMP_MICROS(170417681971000), 'Asia/Seoul') AS datetime_value_asia;
```


### 02. 시간 데이터끼리의 변환 - TIMESTAMP와 DATETIME 비교

```
✅ 둘의 차이를 알고 변환할 수 있어야 table의 정보를 이해 확인 가능
```

**[TIMESTAMP vs DATETIME]**
| | TIMESTAMP | DATETIME |
| --- | --- | ---|
| 타임존 | UTC | T(Time을 의미)
| 시간 차이 | 한국시간 -9 | 한국zone 사용 시  한국과 동일 |

**코드 예시**
```sql
SELECT
 CURRENT_TIMESTAMP() AS timestamp_col,
 DATETIME(CURRENT_TIMESTAMP(), 'Asia/Seoul') AS datetime_col
```


### 03. DATETIME 함수(1) - CURRENT_DATETIME, EXTRACT

**CURRENT_DATETIME 함수**([time zone]) : 현재 DATETIME 출력
```sql
SELECT
 CURRENT_DATE() AS current_date,
 CURRENT_DATE("Asia/Seoul") AS asia_date,
 CURRENT_DATETIME() AS current_datetime,
 CURRENT_DATETIME("Asia/Seoul") AS current_datetime_asia;
```

**EXTRACT 함수** : DATETIME에서 일정 부분만 추출할 때 사용
```sql
EXTRAT(part FROM datetime_expression)
```
```sql
SELECT 
  EXTRACT(DATE FROM DATETIME "2024-01-02 14:00:00") AS date,
  EXTRACT(YEAR FROM DATETIME "2024-01-02 14:00:00") AS year,
  EXTRACT(MONTH FROM DATETIME "2024-01-02 14:00:00") AS month,
  EXTRACT(DAY FROM DATETIME "2024-01-02 14:00:00") AS day,
  EXTRACT(HOUR FROM DATETIME "2024-01-02 14:00:00") AS hour,
  EXTRACT(MINUTE FROM DATETIME "2024-01-02 14:00:00") AS minute,
```
**요일을 추출할 경우** : [1,7] 범위의 값을 변환
```sql
EXTRACT(DAYOFWEEK FROM datetime_col)
```

### 04.  DATETIME 함수(2) - DATETIME_TRUNC

**DEATETIME_TRUNC** : DATE와 HOUR만 남기고 자르기
```sql
SELECT
 DATETIME "2026-10-03 11:56:36" AS original_data,
 DATETIME_TRUNC(DATETIME "2026-10-03 11:56:36", DAY) AS day_trunc,
 DATETIME_TRUNC(DATETIME "2026-10-03 11:56:36", YEAR) AS year_trunc,
 DATETIME_TRUNC(DATETIME "2026-10-03 11:56:36", MONTH) AS month_trunc,
 DATETIME_TRUNC(DATETIME "2026-10-03 11:56:36", HOUR) AS hour_trunc;
```

### 05.  DATETIME 함수(3) - PARSE_DATETIME, FORMAT_DATETIME
**PARSE_DATETIME 함수** : 문자열로 저장된 것을 DATETIME으로 변환할 때 사용  
→ 기본 형식 [PARSE_DATETIME('문자열의 형태', 'DATETIME 문자') AS datetime]
```sql
SELECT
 PARSE_DATETIME('%Y-%m-%d %H:%m:%s', '2026-10-03 11:56:36') AS parse_datetime;
```
✅ Format Elements 문서를 확인하면 %Y 등의 요소들이 의미하는 바를 확인할 수 있음


**FORMAT_DATETIME 함수** : 특정 형태의 문자열 데이터로 변경하고 싶을 때 사용
```sql
SELECT
 FORMAT_DATETIME("%c", DATETIME "2026-10-03 11:56:36") AS formatted;
```
✅ 결과
<img width="1012" height="68" alt="image" src="https://github.com/user-attachments/assets/0a6f113c-816b-4493-a96a-a8b03ee87604" />


**💡PARSE vs FORMAT** - 어떤 걸 어떤 상황에 사용해야 할까?
- 문자열 ➡️ DATETIME : PARSE
- DATETIME ➡️ 문자열 : FORMAT


### 06. DATETIME 함수(4) - LAST_DAY, DATETIME_DIFF

**LAST_DAY 함수** : 자동으로 월의 마지막 날을 계산하는 함수
```sql
SELECT
LAST_DAY(DATETIME '2026-10-03 11:56:36') AS last_day,
LAST_DAY(DATETIME '2026-10-03 11:56:36', MONTH) AS last_day_month,
LAST_DAY(DATETIME '2026-10-03 11:56:36', WEEK) AS last_day_week,
LAST_DAY(DATETIME '2026-10-03 11:56:36',', WEEK(SUNDAY)) AS last_day_week_sun,
LAST_DAY(DATETIME '2026-10-03 11:56:36', WEEK(MONDAY)) AS last_day_week_mon
```
✅ 맨 아래 두 줄은 일요일 기준으로 마지막, 월요일 기준으로 마지막을 계산한 값  
✅ 상황에 따라 알맞은 코드를 적용


**DATETIME_DIFF** : 두 DATETIME의 차이를 계산하는 함수  
→ 기본 형식 [DATETIME_DIFF(첫 DATETIME, 두번째 DATETIME, 궁금한 부분)]  
```sql
SELECT
DATETIME_DIFF(first_datetime, second_datetime, DAY) AS day_diff1,
DATETIME_DIFF(second_datetime, first_datetime, DAY) AS day_diff2,
DATETIME_DIFF(first_datetime, second_datetime, MONTH) AS month_diff,
DATETIME_DIFF(first_datetime, second_datetime, WEEK) AS week_diff,
FROM (
SELECT
DATETIME "2024-04-02 10:20:00" AS first_datetime,
DATETIME "2021-01-01 15:30:00" AS second_datetime,
)
```

## 4.6 조건문 함수 
### 07. 조건문 함수 - CASE_WHEN, IF
```
✅ 데이터 분석에 있어 전처리를 위해 필요한 함수
✅ 조건에 따른 분기 처리가 필요하거나 다른 값을 표시하고 싶을 때 사용
```

**💡조건문이란?**   
→ 특정 조건이 충족될 경우, 특정한 행동을 하는 함수  
→ 데이터 분석에서 특정 카테고리를 하나로 합치는 전처리가 필요한 경우에 사용

**CASE_WHEN 함수** : 여러 조건이 있을 경우
```sql
SELECT
 CASE
  WHEN 조건1 THEN 조건1이 참일 때 결과,
  WHEN 조건2 THEN 조건2가 참일 때 결과,
  ELSE 그 외 조건일 때 결과,
END AS 새로운 컬럼_이름
```
✅ 조건 1,2에 모두 해당되면 앞선 순서를 따름
✅ 문자열 함수에서 이슈가 자주 발생하는 편  


**IF 함수** : 단일 조건일 경우
```sql
SELECT
 IF(1=1, '동일한 결과', '동일하지 않은 결과') AS result1,
 IF(1=2, '동일한 결과', '동일하지 않은 결과') AS result2)
```


---

# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
- 문제 풀이 정답 화면 캡처
- SQL 실행 결과 화면 캡처

<img width="490" height="532" alt="image" src="https://github.com/user-attachments/assets/cb34a8a1-04b5-4400-b46e-747573885848" />


---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [자동차 대여 기록에서 장기/단기 대여 구분하기](https://school.programmers.co.kr/learn/courses/30/lessons/151138)

풀이 과정:

```
- 장기/단기 대여를 나눈 기준: 30일 이상이면 장기, 미만이면 단기로 나누었다. 종료일-시작일로 나눈 후 날짜의 오차를 감안하여 +1 붙였다.
- 사용한 날짜 계산 방식: DATETIME_DIFF 사용하려 했으나, SQL에는 해당 함수가 없어 DATEDIFF로 변경하여 계산하였다.
- CASE WHEN으로 만든 컬럼: IF 문으로 만들어버림 ... RENT_TYPE
```
<img width="1068" height="693" alt="image" src="https://github.com/user-attachments/assets/b441c293-b917-4ea7-b3f3-1b9bc7a7d29a" />

## 🧩 문제 2

문제 링크: [한 해에 잡은 물고기 수 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/298516)

풀이 과정:

```
- 문제에서 요구한 연도:
- 사용한 날짜 조건:
- 집계한 대상:
```

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. -->

## 🧩 문제 3

문제 링크: [조건에 부합하는 중고거래 상태 조회하기](https://school.programmers.co.kr/learn/courses/30/lessons/164672)

풀이 과정:

```
- 날짜 조건:
- CASE WHEN으로 바꾼 값:
- ELSE에 해당하는 경우:
- 정렬 기준:
```

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. -->

## 🧩 문제 4

문제 링크: [자동차 평균 대여 기간 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/157342)

풀이 과정:

```
- GROUP BY 기준:
- 평균을 계산한 방식:
- HAVING에 사용한 조건:
- 처음 헷갈렸던 점:
```

<!-- 정답을 맞추게 되면, 정답입니다. 이 부분을 캡처해서 이 주석을 지우시고 첨부해주시면 됩니다. -->

---

# 4️⃣ 이번 주 회고

```
1. 날짜 함수 중 가장 헷갈린 함수:
2. CASE WHEN을 사용할 때 기억해야 할 문법:
3. 날짜/시간 데이터나 조건문을 활용해보고 싶은 분석 상황:
```

수고하셨습니다!



