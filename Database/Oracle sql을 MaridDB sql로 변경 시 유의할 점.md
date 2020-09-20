# Oracle sql -> MaridDB sql로 변경 시 유의할 점

- CREATE 구문 시 타입

  \- NUMBER -> INT
  \- VARCHAR2 -> VARCHAR
  \- DATE -> DATETIME (참고로 SQL Server도 DATETIME)

- 함수

    \- NVL -> IFNULL
    
\- NVL2(expr, expr1, expr2) -> CASE
     \- expr의 값이 null이 아닐 경우 expr1값 리턴, null 인경우 expr2 리턴
    
    \- SYSDATE -> NOW()
     ex) Oracle: SELECT SYSDATE FROM DUAL;
        MariaDB: SELECT NOW(); 또는 SELECT SYSDATE();
    
    \- TRUNC -> CURDATE, MySQL에서 TRUNC 하면 시간이 없는 일자만 나옴.
     ex) Oracle: SELECT TRUNC(SYSDATE) FROM DUAL;
    MariaDB: SELECT CURDATE() ;
    
    \- DECODE -> CASE
    
\- TO_NUMBER -> CAST
    
    \- CAST
       \- CAST('' AS VARCHAR(1)) 사용 불가
   \- CAST('' AS CHAR) 수정
    
\- DECODE()
       \- MariaDB에서 DECODE는 암호화 예약어로 쓰임
   \- CASE문으로 대체해서 사용해야 함
    
- 시퀀스 (MariaDB 버전에 따라 다르다)

- Outer join

  - `(+)`  ->  `LEFT JOIN.. ON..` 



등등..