###  1. 등록일자가 2020/01/01 이전인 포켓몬들의 번호, 이름, 등록일자 알려줘

```sql
MariaDB [testdb]> SELECT no, name, regdate FROM pokemon WHERE regdate  < '2020/01/01';
```

###  2. 레벨이 5 이상 10 이하인 포켓몬들의 모든 정보 알려줘 

```sql
MariaDB [testdb]> SELECT * FROM pokemon WHERE level >=5 AND level <=10;
```


###  3. 모든 포켓몬들의 레벨 보여줘

```sql
MariaDB [testdb]> SELECT level FROM pokemon;
```

###  4. 모든 포켓몬들의 레벨 보여줘. 중복 제거 해줘. (DISTINCT)  

```sql
MariaDB [testdb]> SELECT DISTINCT level FROM pokemon;
```


###  5. 모든 포켓몬들의 이름, 레벨 보여줘. 이름 오름차순으로 보여줘  (ORDER BY) 

```sql
MariaDB [testdb]> SELECT name, level FROM pokemon ORDER BY name;
```


###  6. 모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로 보여줘  (ORDER BY) 

```sql
ASC오름차  (자동으로 오름차 됨)
DESC내림차
MariaDB [testdb]> SELECT name, level FROM pokemon ORDER BY level DESC;
```


###  7. 레벨이 3이상인 모든 포켓몬들의 이름, 레벨 보여줘. 레벨 많은 순으로, 같은 레벨이면 이름 오름차순으로 보여줘  (ORDER BY)

```sql
MariaDB [testdb]> INSERT INTO pokemon VALUES(NULL, '거북왕', 100, 1200, 200, DEFAULT);
거북왕 추가
MariaDB [testdb]> SELECT name, level FROM pokemon WHERE level >=3 ORDER BY level, name;
```


###   8. 레벨이 100 미만인 포켓몬들의 레벨을 1씩 증가해줘

```sql
MariaDB [testdb]> UPDATE pokemon SET level = level+1 WHERE level <100;
```


###  9. 포켓몬 중 레벨이 100 인 포켓몬들을 삭제해줘

```sql
MariaDB [testdb]> DELETE FROM pokemon WHERE level = 100;
```


###  10. 레벨이 짝수인 포켓몬들의 레벨을 두배로 변경해줘

```sql
MariaDB [testdb]> UPDATE pokemon SET level = level*2 WHERE level%2=0;
```


###  11. 체력이 레벨의 100배보다 큰 포켓몬들의 레벨을 체력의 1/100로 수정해줘

```sql
MariaDB [testdb]> UPDATE pokemon SET level = hp*1/100 WHERE hp > level*100;

```
