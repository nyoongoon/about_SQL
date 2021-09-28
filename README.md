# about_SQL
sql을 공부하다가 알게 된 것을 기록하는 저장소입니다.

# MYSQl
### insert into tableName set var = value;
- mysql 확장sql문 
-> set 으로 하면 필드명에 값을 저장해 놓으니 가독성이 높아짐.

### ifnull() 
- ex) select ifnull(name, '값이 없음') from test
- test 테이블의 name필드 값이 null 일때 '값이 없음'을 리턴하는 함수.
