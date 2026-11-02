# 📘 SQL_BASIC 6주차 정규 과제

SQL_BASIC 정규 과제는 매주 정해진 분량의 `초보자를 위한 BigQuery(SQL) 입문` 강의를 듣고, 핵심 개념을 정리한 뒤 간단한 SQL 문제를 직접 풀어보는 방식으로 진행합니다.

이번 주는 SQL 입문 과정의 핵심 고비인 `JOIN`을 학습합니다.

JOIN은 여러 테이블을 연결해서 분석 질문에 답하기 위해 반드시 필요한 개념입니다. 이번 주 과제에서는 정답 코드뿐 아니라 **어떤 테이블을 어떤 키로 연결했는지**를 꼭 기록해주세요.

완성된 과제는 Github에 업로드하고, 링크를 스프레드시트 'SQL' 시트에 입력해 제출해주세요.

**👀 수행 인증란은 필수입니다.**

---

## 📚 SQL_BASIC_6th_TIL

### 섹션 6. 다량의 자료를 연결 : JOIN

### 5-2. JOIN 이해하기

### 5-3. 다양한 JOIN 방법

### 5-4. JOIN 쿼리 작성하기

### 5-5. JOIN을 처음 공부할 때 헷갈리는 부분

---

## ✨ 선택 강의

- 5-6. JOIN 연습문제: JOIN 문제를 더 연습하고 싶을 때 선택 수강

---

## 🏁 전체 강의 수강 계획

| 주차 | 필수 강의 범위 | 선택 강의 | 완료 여부 |
| --- | --- | --- | --- |
| 1주차 | 1-1 ~ 2-1 | 1 | ✅ |
| 2주차 | 2-2 ~ 2-3 | 2-4 | ✅ |
| 3주차 | 2-5, 2-7 ~ 2-8 | 2-6 | ✅ |
| 4주차 | 3-2 ~ 4-3 | 3-4 | ✅ |
| 5주차 | 4-4 ~ 4-6 | 4-5, 4-7 | ✅ |
| 6주차 | 5-2 ~ 5-5 | 5-6 | ✅ |
| 7주차 | 필수 강의 없음 | 6-2, 6-3, 6-4, 6-5 | 🍽️ |

---

<br>

<!-- 여기까진 그대로 둬 주세요-->

---


## 5.2 JOIN 이해하기
## 01. SQL JOIN

```
✅ 서로 다른 데이터 테이블들을 연결하는 과정
✅ 정규화 과정을 보다 더 손쉽게 거칠 수 있음
```
**💡SQL JOIN이란?**  
- 서로 다른 데이터 테이블을 연결하는 과정
- 공통적으로 존재하는 컬럼(=KEY)가 있다면 JOIN 가능
- 일반적으로 id 값을 Key로 자주 사용, 특정 범위로도 가능함  

`이해를 위한 예시`   
```
포켓몬 데이터와 트레이너 데이터를 JOIN 한다고 가정해보자.
이때 두 데이터 테이블에는 공통된 컬럼이 존재하지 않지만, 
대신 두 데이터를 이어주는 <트레이너가 포획한 포켓몬> 데이터가 존재한다.
```
<img width="1310" height="621" alt="image" src="https://github.com/user-attachments/assets/e13eff9b-aa9a-44a2-be1f-3ddd70c61196" />

**1. 트레이너가 포획한 포켓몬 기준으로 트레이너 데이터 JOIN**

`트레이너가 포획한 포켓몬(편의상 테이블 A)`
| id | trainer_id | pokemon_id | catch_date | location |
|----|-----------|-----------|-----------|----------|
| 1 | 1 | 1 | 2023-01-14 | Seoul |
| 2 | 2 | 4 | 2023-02-10 | Busan |
| 3 | 3 | 3 | 2023-03-05 | Incheon |

`트레이너(편의상 테이블 B)`
| id | name | age | hometown | preferred_pokemon_type | badge_count | achievement_level |
|----|------|-----|----------|------------------------|-------------|-------------------|
| 1 | Ash | 16 | Seoul | Electric | 8 | Master |
| 2 | K | 18 | Busan | Water | 6 | Advanced |
| 3 | Peter | 20 | Gwangju | Rock | 7 | Expert |
| 4 | Maya | 15 | Incheon | Grass | 5 | Advanced |
| 5 | Gary | 17 | Daegu | Flying | 6 | Advanced |

`풀이과정`
1. 두 데이터의 공통된 KEY는 `trainer_id`와 `id`
2. 기준이 되는 것은 A이므로 `id`에 해당하는 row를 테이블 A 뒤로 이어붙이기
→ 이렇게 2개의 테이블을 붙일 경우 우측에 *컬럼을 추가*한다는 개념으로 이해
→ 그 외에도 이 추가한 테이블에 다른 테이블을 더 이어붙이기 가능

<br>

## 5.3 다양한 JOIN 방법
### 02. LEFT/RIGHT, INNER, CROSS JOIN

```
✅ 데이터 테이블들을 연결하는 방법
```

**JOIN의 대표적 4가지 방식**
- (INNER) JOIN : 두 테이블의 공통 요소만 연결
- LEFT/RIGHT JOIN : 왼쪽/오른쪽 테이블 기준으로 연결
- FULL (OUTER) JOIN : 양쪽 기준으로 연결
- CROSS JOIN : 두 테이블의 각각의 요소를 곱하기

`도식화 그림`
<img width="1307" height="630" alt="image" src="https://github.com/user-attachments/assets/b4b66a0c-cae0-4e61-947e-e4005f069f3e" />

`집합 관점으로 정리`
| JOIN 종류 | A만 | A ∩ B (교집합) | B만 |
|-----------|---|-------------|---|
| INNER JOIN | | ✅ | |
| LEFT JOIN | ✅ | ✅ | |
| RIGHT JOIN | | ✅ | ✅ |
| FULL JOIN | ✅ | ✅ | ✅ |

<br>

## 5.4 JOIN 쿼리 작성하기
### 03. JOIN 쿼리 작성법

**작성 흐름**
1. 테이블 확인 : 테이블에 저장된 데이터, 컬럼 확인
2. 기준 테이블 정의 : 가장 많이 참고할 기준 테이블 정의
3. JOIN KEY 찾기 : 여러 테이블과 연결할 KEY 찾기
4. 결과 예상하기 : 결과 테이블 예상해서 엑셀 등으로 작성
5. 쿼리 작성/검증 : 예상한 결과와 동일한 결과인지 확인

**💡작성 문법**
```sql
SELECT
    A.col1, #컬럼이름
    A.col2,
    B.col11,
    B.col12
FROM table1 AS A
LEFT JOIN table2 AS B
ON A.key = B.key # 테이블이 길어서 별칭(Alias ) 지칭 가능 
```
→ 항상 마지막에 `from`, `left/right`, `on` 들어가는 것 잊지 않기

**종류별 쿼리 작성 차이 비교표**
| JOIN 종류 | ON 필수 여부 | 쿼리 예시 |
|-----------|:-----------:|-----------|
| INNER JOIN | O | `FROM table_a AS A`<br>`INNER JOIN table_b AS B`<br>`ON A.key = B.key` |
| LEFT/RIGHT JOIN | O | `FROM table_a AS A`<br>`LEFT/RIGHT JOIN table_b AS B`<br>`ON A.key = B.key` |
| FULL JOIN | O | `FROM table_a AS A`<br>`FULL JOIN table_b AS B`<br>`ON A.key = B.key` |
| CROSS JOIN | X | `FROM table_a AS A`<br>`CROSS JOIN table_b AS B` |

---

# 2️⃣ 수행 인증란

아래 중 하나 이상을 첨부해주세요.

- 강의 수강 화면 캡처
- JOIN 문제 풀이 정답 화면 캡처
- JOIN 전후 결과 row 수를 비교한 캡처 또는 메모

<img width="1810" height="862" alt="image" src="https://github.com/user-attachments/assets/43f75ac0-9606-4fbf-8f50-11a1327f85f2" />


---

# 3️⃣ 확인 문제

프로그래머스는 로그인이 필요하므로, 로그인 후 문제 풀이를 진행해주세요.

## 🧩 문제 1

문제 링크: [조건에 맞는 도서와 저자 리스트 출력하기](https://school.programmers.co.kr/learn/courses/30/lessons/144854)

풀이 과정:
```
- 사용한 테이블: BOOK과 AUTHOR 테이블
- JOIN key: AUTHOR_ID를 JOIN 시켜서 하나의 테이블로 연결
- 날짜를 출력한 형식: DATE_FORMAT 문법을 이용하여 숫자로 되어있는 컬럼을 문자열의 형태로 변형하여 출
```

**사용한 코드**
```sql
SELECT
  B.BOOK_ID,
  A.AUTHOR_NAME,
  DATE_FORMAT(B.PUBLISHED_DATE, '%Y-%m-%d') AS PUBLISHED_DATE
FROM BOOK AS B
LEFT JOIN AUTHOR AS A
ON B.AUTHOR_ID = A.AUTHOR_ID
WHERE B.CATEGORY = '경제'
ORDER BY B.PUBLISHED_DATE ASC
```

<img width="1410" height="602" alt="image" src="https://github.com/user-attachments/assets/60fc323d-6357-4cac-87df-41d06c98481a" />



## 🧩 문제 2

문제 링크: [상품 별 오프라인 매출 구하기](https://school.programmers.co.kr/learn/courses/30/lessons/131533)

풀이 과정:

```
- 연결한 테이블:
- JOIN key:
- 집계한 값:
```

**사용한 코드**
```sql
SELECT
    P.PRODUCT_CODE,
    SUM(P.PRICE * O.SALES_AMOUNT) AS SALES
FROM PRODUCT AS P
INNER JOIN OFFLINE_SALE AS O
ON P.PRODUCT_ID = O.PRODUCT_ID
GROUP BY P.PRODUCT_CODE
ORDER BY SALES DESC, P.PRODUCT_CODE ASC
```

<img width="1572" height="761" alt="image" src="https://github.com/user-attachments/assets/38a25a55-a68a-4686-bfae-9eeec3aa3042" />

## 🧩 문제 3

문제 링크: [없어진 기록 찾기](https://school.programmers.co.kr/learn/courses/30/lessons/59042)

풀이 과정:

```
- 기준이 되는 왼쪽 테이블: 들어온 기록이 없는 동물을 가려내야 하므로 ANIMAL_OUT 테이블이 기준
- LEFT JOIN이 필요한 이유: LEFT_JOIN을 사용하면 기록이 없을 경우 NULL로 붙기 때문에 
- NULL이 발생하는 경우: 한쪽 테이블에서 조건이 맞는 행이 없을 때 
```

**사용한 코드**
```sql
SELECT
    O.ANIMAL_ID,
    O.NAME
FROM ANIMAL_OUTS AS O
LEFT JOIN ANIMAL_INS AS I
ON O.ANIMAL_ID = I.ANIMAL_ID
WHERE I.ANIMAL_ID IS NULL
ORDER BY O.ANIMAL_ID
```

<img width="1536" height="757" alt="image" src="https://github.com/user-attachments/assets/ba4175c6-d510-4cdc-b302-699621e0649d" />


## 🧩 문제 4

문제 링크: [있었는데요 없었습니다](https://school.programmers.co.kr/learn/courses/30/lessons/59043)

풀이 과정:

```
- 사용한 테이블: ANIMAL_INS와 ANIMAL_OUTS
- JOIN key: ANIMAL_ID
- 비교한 날짜 컬럼: 입소 기록과 출소 기록을 비교
- 정렬 기준: 오름차순으로 정
```

**사용한 코드**
```sql
SELECT
  I.ANIMAL_ID,
  O.NAME
FROM ANIMAL_INS AS I
LEFT JOIN ANIMAL_OUTS AS O
ON I.ANIMAL_ID = O.ANIMAL_ID
WHERE I.DATETIME > O.DATETIME
ORDER BY I.DATETIME ASC
```

<img width="1373" height="598" alt="image" src="https://github.com/user-attachments/assets/354c84c7-9e22-4e68-98b5-d157a278ae43" />

---

# 4️⃣ 참고 자료

JOIN 개념이 헷갈린다면 아래 자료를 함께 참고해도 좋습니다.

1. https://data-marketing-bk.tistory.com/entry/SQL-JOIN-%ED%95%9C-%EB%B0%A9%EC%97%90-%EC%A0%95%EB%A6%AC-%EA%B0%9C%EB%85%90%EB%B6%80%ED%84%B0-%EC%BD%94%EB%93%9C%EA%B9%8C%EC%A7%80-%EC%9D%B4%EA%B2%83%EB%A7%8C-%EB%B3%B4%EC%9E%90
2. https://velog.io/@wijoonwu/JOIN

---

# 5️⃣ 이번 주 회고

```
1. INNER JOIN과 LEFT JOIN의 차이를 어떻게 이해했는지: 단순하게 INNER JOIN은 교집합만, LEFT JOIN은 왼쪽에 있는 테이블을 기준으로 
2. JOIN 문제를 풀 때 가장 먼저 확인해야 할 것: 어떤 테이블을 이어 붙여야 하고, 그 둘 사이에 JOIN KEY가 무엇이 존재하는지 파악해야 한다
3. JOIN 결과가 예상과 달랐던 경험이 있다면: 
```

수고하셨습니다!




