# about_SQL
sql을 공부하다가 알게 된 것을 기록하는 저장소입니다.


# Foreign Key 사용 장단점

- 외래키는 테이블의 특정 컬럼(데이터)이 다른 특정한 곳에도 존재함을 보증해주는 역할을 한다. 
- 그렇게 함으로 데이터가 규칙에 어긋나지 못하게 해준다. 
- 검증사항을 컴퓨터에게 맡기는 셈이지만, 그렇기에 DBMS는 매번 제약사항을 검증해야하기에 성능이 떨어질 수 있다. 

https://dba.stackexchange.com/questions/168590/not-using-foreign-key-constraints-in-real-practice-is-it-ok
https://dataedo.com/blog/why-there-are-no-foreign-keys-in-your-database-referential-integrity-checks
<br/><br/>


# MYSQl
### insert into tableName set var = value;
- mysql 확장sql문 
-> set 으로 하면 필드명에 값을 저장해 놓으니 가독성이 높아짐.

### ifnull() 
- ex) select ifnull(name, '값이 없음') from test
- test 테이블의 name필드 값이 null 일때 '값이 없음'을 리턴하는 함수.
<br/><br/>

# JOIN
- 조인은 여러 개의 릴레이션을 사용해서 새로운 릴레이션을 만드는 과정.

## 문법
- A.a INNER JOIN B == A JOIN B
- INNER JOIN의 where 절에서 = 을 사용하면 EQUI JOIN, 의외의 연산자를 사용하면 NON EQUI JOIN
``` java
// EQUI JOIN (⊂ INNER JOIN)
SELECT [A.]col, [B.]col
FROM A [INNER] JOIN B 
ON A.col = B.col; // [INNER]JOIN ~ ON 사용

// 위 아래 동일 결과

SELECT [A.]col, [B.]col 
FROM A, B
WHERE A.col = B.col; // 콤마 ~ where ~ = 사용
// AND A.col2 = 1  < -- 추가 조건 시 AND 사용
```
<br/>

- A LEFT JOIN B == A LEFT OUTER JOIN B
- 왼쪽 테이블을 다 출력 후 ON 조건에 일치하는 오른쪽 테이블 붙이기
``` java
// LEFT [OUTER] JOIN 
SELECT [A.]col, [B.]col
FROM A LEFT [OUTER] JOIN B 
ON A.col = B.col; // LEFT [OUTER] JOIN ~ ON 사용

// 위 아래 동일 결과

SELECT [A.]col, [B.]col 
FROM A, B
WHERE A.col = B.col(+); // 콤마 ~ where ~ = ~ (+) 사용
```
<br/>

- A RIGHT JOIN B == A RIGHT OUTER JOIN B
- 오른쪽 테이블을 다 출력 후 ON 조건에 일치하는 왼쪽 테이블 붙이기
``` java
// RIGHT [OUTER] JOIN 
SELECT [A.]col, [B.]col
FROM A RIGHT [OUTER] JOIN B 
ON A.col = B.col; // RIGHT [OUTER] JOIN ~ ON 사용

// 위 아래 동일 결과

SELECT [A.]col, [B.]col 
FROM A, B
WHERE A.col (+)= B.col; // 콤마 ~ where ~ (+)= ~  사용
``` 
<br/>

- A FULL JOIN B == A FULL OUTER JOIN B
``` java
// FULL [OUTER] JOIN 
SELECT [A.]col, [B.]col
FROM A FULL [OUTER] JOIN B 
ON A.col = B.col;
```
<br/>



## JOIN의 구별

### FROM 절의 JOIN 형태에 따른 분류
- (1) INNER JOIN : JOIN 조건에서 값이 일치하는 행만 반환
-> 둘다 빈 값이 없음
- (2) OUTER JOIN: JOIN 조건에서 한쪽 값이 없더라도 행을 반환. 
-> 한 쪽에 빈 값이 있을 수 있음
### 연산자에 따른 분류 (INNER JOIN)
- **INNER JOIN은 EQUI JOIN과 NON EQUI JOIN으로 구분.**
- (1-1) EQUI JOIN: 두 테이블 간의 칼럼 값들이 서로 일치하는 경우("=" 연산자 사용)
- (1-2) NON EQUI JOIN: 두 테이블간의 칼럼 값들이 정확하게 일치하지 않는 경우 (비교 연산자 사용) 
