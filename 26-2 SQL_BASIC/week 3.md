# 📘 SQL_BASIC 3주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 집계 함수와 `GROUP BY`, `HAVING`을 학습합니다.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_3rd_TIL

### 섹션 3. 데이터 탐색 - 조건, 추출, 요약

### 2-5. 집계(GROUP BY + HAVING + SUM/COUNT)

### 2-7. 정리

### 2-8. 새로운 집계 함수 소개(GROUP BY ALL, 2024-02-26에 나온 함수)

---

## ✨ 선택 강의

- 2-6. 연습 문제: 집계와 조건 조회를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | 🍽️ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | 🍽️ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | 🍽️ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---

# 1️⃣ 개념 정리

아래 키워드 중 중요하다고 생각한 개념을 2개 이상 골라 짧게 정리해주세요. 3개보다 더 많이 정리하고 싶다면 자유롭게 항목을 추가해도 좋습니다.

이번 주 키워드:
- COUNT
- SUM
- AVG
- MAX
- MIN
- GROUP BY
- HAVING
- 집계 기준

## 01.

```
개념 이름: GROUP BY
개념 설명: 특정 컬럼 값이 같은 행끼리 묶어 그룹별로 집계하는 구문.
집계 함수 없이 SELECT에 쓴 컬럼은 반드시 GROUP BY에 포함해야 함.
예시 쿼리: SELECT category, SUM(amount) FROM orders GROUP BY category;
```

## 02.

```
개념 이름: HAVING
개념 설명: GROUP BY로 묶은 뒤 집계 결과에 조건을 거는 구문.
WHERE는 집계 전 행을, HAVING은 집계 후 그룹을 거르므로 집계 함수는 HAVING에서만 쓸 수 있음.
예시 쿼리: SELECT category, SUM(amount) FROM orders GROUP BY category HAVING SUM(amount) >= 1000000;
```

## 03.

```
개념 이름: 집계 함수 (COUNT / SUM / AVG / MAX / MIN)
개념 설명: 여러 행을 하나의 값(개수, 합계, 평균, 최댓값, 최솟값)으로 요약하는 함수.
COUNT(*)는 전체 행을 세고, 나머지는 NULL을 제외하고 계산함.
예시 쿼리:ㅍSELECT COUNT(*), SUM(amount), AVG(amount), MAX(amount), MIN(amount) FROM orders;
```

---

# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
- 문제 풀이 정답 화면 캡처
- SQL 실행 결과 화면 캡처

<img width="516" height="901" alt="image" src="https://github.com/user-attachments/assets/e28ae1b8-30ff-4b9a-959a-7ec5f95a8a64" />


---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [최댓값 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/59415)

풀이 과정:

```
SELECT MAX(DATETIME) AS 시간
FROM ANIMAL_INS;
```

```
- 문제 요구사항: 가장 최근에 들어온 동물의 보호 시작일 하나만 조회
- 사용한 SQL 절: SELECT, MAX(), FROM
- 새로 배운 점: MAX는 숫자뿐 아니라 날짜/시간 컬럼에도 쓸 수 있고, 가장 늦은 값을 반환한다.
  ORDER BY DATETIME DESC LIMIT 1로도 풀 수 있다.
```
<img width="885" height="466" alt="image" src="https://github.com/user-attachments/assets/de538833-5263-4459-a7e0-f6d050daef5f" />


## 🧩 문제 2

문제 링크: [가장 비싼 상품 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131697)

풀이 과정:

```
SELECT MAX(PRICE) AS MAX_PRICE
FROM PRODUCT;
```

```
- 사용한 집계 함수: MAX()
- 집계 대상 컬럼: PRICE
- 결과를 검증한 방법: 예시 테이블에 쿼리를 적용해 결과가 22000 한 건으로 나오는지 확인했고,
<SELECT PRICE FROM PRODUCT ORDER BY PRICE DESC LIMIT 1>처럼 다른 방식으로 구한 최댓값과 일치하는지도 비교했다.
```

<img width="1110" height="753" alt="image" src="https://github.com/user-attachments/assets/8202a696-7538-437c-83c4-a9cc7e24b26e" />

## 🧩 문제 3

문제 링크: [고양이와 개는 몇 마리 있을까](https://school.programmers.co.kr/learn/courses/30/lessons/59040)

풀이 과정:

```
SELECT ANIMAL_TYPE, COUNT(*) AS count
FROM ANIMAL_INS
GROUP BY ANIMAL_TYPE
ORDER BY ANIMAL_TYPE;
```

```
` 그룹화 기준: ANIMAL_TYPE
WHERE와 HAVING 중 사용한 절: 둘 다 사용하지 않음. 전체 행을 종별로 세는 문제라 행을 걸러내는 WHERE도, 그룹을 걸러내는 HAVING도 필요 없었다.
처음 틀렸다면 틀린 이유: 해당 없음.
새로 배운 SQL 패턴: GROUP BY로 묶고 COUNT(*)로 세고 ORDER BY로 정렬하는 "종류별 개수 세기" 패턴. 
```

<img width="1390" height="687" alt="image" src="https://github.com/user-attachments/assets/21e1373b-9c69-412c-b25c-54e45d3367c9" />


---

# 4️⃣ 이번 주 회고

```
1. 문제를 SQL로 옮길 때 가장 어려웠던 부분: 문장으로 된 요구사항을 집계 함수(COUNT, MAX)와 GROUP BY로 바꾸는 부분.
특히 "고양이를 먼저 조회"라는 조건을 ORDER BY로 옮기는 게 헷갈렸다.

2. WHERE와 HAVING의 차이를 어떻게 이해했는지:WHERE는 그룹으로 묶기 전에 행을 걸러내고, HAVING은 GROUP BY로 묶은 뒤
집계 결과를 기준으로 그룹을 걸러낸다.

3. 다음 주에 더 연습하고 싶은 문제 유형: GROUP BY + HAVING 조합, 그리고 JOIN이 들어간 집계 문제.
```

수고하셨습니다!



