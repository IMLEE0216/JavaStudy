```sql
1. MEMBER 테이블 만들기 
	    항목 : 회원번호(no), 아이디(id), 패스워드(password), 이메일(email), 등급(type), 적립금(point)
 	    제약조건 : 
		Primary key 는 회원번호다.
		아이디는 중복이면 안된다. (UNIQUE) 
		이메일도 중복이면 안된다. (UNIQUE) 
		아이디는 누락되면 안된다. (NOT NULL)
		등급은 1 ~ 4가 있고 기본값은 1이다.
		적립금은 1000원이 기본값이고 음수일 수 없다.

CREATE TABLE member (
	no INT PRIMARY KEY AUTO_INCREMENT,
	id VARCHAR(30) NOT NULL UNIQUE,
	password VARCHAR(30),
	email VARCHAR(40) UNIQUE,
	type INT(1),
	point INT(9) DEFAULT 1000 CHECK (point > 0)
	);
		
```

```sql
2. QNA 테이블 만들기 
	    항목 : 질문번호(no), 글쓴이번호(writer_no), 질문 내용(content), 등록일자(regdate)
	    제약조건 : 
		Primary key 는 질문번호다.
		글쓴이번호는 MEMBER 테이블의 회원번호를 참조한다. (FOREIGN KEY)
		글쓴이 회원이 삭제되면 해당 질문도 삭제된다. (CASCADE)	
		질문 내용은 누락되면 안된다.
		등록일자는 기본값이 현재 시간이다. 
		
CREATE TABLE QNA (
	no INT PRIMARY KEY AUTO_INCREMENT,
	writer_no INT(9),
	content VARCHAR(100) NOT NULL,
 	regdate DATETIME DEFAULT CURRENT_TIMESTAMP,
	FOREIGN KEY(writer_no) REFERENCES member(no) ON DELETE CASCADE
	);
```

```sql
MEMBER
INSERT INTO member VALUES(NULL, 'zzz', 'ABC123', 'zzz@naver.com', 1, 1000);
INSERT INTO member VALUES(NULL, 'ABC', 'ABC123', 'ABC@naver.com', 2, 2000);
INSERT INTO member VALUES(NULL, 'KIM', 'kim123', 'kim@naver.com', 1, 1200);
INSERT INTO member VALUES(NULL, 'park', 'park123', 'park01@naver.com', 3, 3000);

MariaDB [homeworkdb]> SELECT * FROM member;
+----+------+----------+------------------+------+-------+
| no | id   | password | email            | type | point |
+----+------+----------+------------------+------+-------+
|  1 | zzz  | ABC123   | zzz@naver.com    |    1 |  1000 |
|  2 | ABC  | ABC123   | ABC@naver.com    |    2 |  2000 |
|  3 | KIM  | kim123   | kim@naver.com    |    1 |  1200 |
|  4 | park | park123  | park01@naver.com |    3 |  3000 |
+----+------+----------+------------------+------+-------+
```

```sql
QNA
INSERT INTO QNA VALUES(NULL, 1, '회원탈퇴 방법 좀...', DEFAULT);
INSERT INTO QNA VALUES(NULL, 2, '포인트 누락', DEFAULT);
INSERT INTO QNA VALUES(NULL, 4, '회원가입 방법', DEFAULT);
INSERT INTO QNA VALUES(NULL, 4, '회원 정보 수정', DEFAULT);
INSERT INTO QNA VALUES(NULL, 3, '포인트 사용 방법', DEFAULT);

MariaDB [homeworkdb]> SELECT * FROM QNA;
+----+-----------+---------------------+---------------------+
| no | writer_no | content             | regdate             |
+----+-----------+---------------------+---------------------+
|  1 |         1 | 회원탈퇴 방법 좀... | 2020-12-09 22:14:54 |
|  2 |         2 | 포인트 누락         | 2020-12-09 22:16:01 |
|  3 |         4 | 회원가입 방법       | 2020-12-09 22:16:21 |
|  4 |         4 | 회원 정보 수정      | 2020-12-09 22:16:45 |
|  5 |         3 | 포인트 사용 방법    | 2020-12-09 22:17:27 |
+----+-----------+---------------------+---------------------+
```

```sql
실습
MariaDB [homeworkdb]> DELETE FROM member WHERE no = 2;
Query OK, 1 row affected (0.000 sec)

MariaDB [homeworkdb]> SELECT * FROM member;
+----+------+----------+------------------+------+-------+
| no | id   | password | email            | type | point |
+----+------+----------+------------------+------+-------+
|  1 | zzz  | ABC123   | zzz@naver.com    |    1 |  1000 |
|  3 | KIM  | kim123   | kim@naver.com    |    1 |  1200 |
|  4 | park | park123  | park01@naver.com |    3 |  3000 |
+----+------+----------+------------------+------+-------+

MariaDB [homeworkdb]> SELECT * FROM QNA;
+----+-----------+---------------------+---------------------+
| no | writer_no | content             | regdate             |
+----+-----------+---------------------+---------------------+
|  1 |         1 | 회원탈퇴 방법 좀... | 2020-12-09 22:14:54 |
|  3 |         4 | 회원가입 방법       | 2020-12-09 22:16:21 |
|  4 |         4 | 회원 정보 수정      | 2020-12-09 22:16:45 |
|  5 |         3 | 포인트 사용 방법    | 2020-12-09 22:17:27 |
+----+-----------+---------------------+---------------------+
```

