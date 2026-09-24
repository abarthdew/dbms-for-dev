# MongoDB

- MongoDB(NoSQL)
  - json 형태 저장
  - 관계형으로 데이터를 저장하지 않음
  - insert, select 위주
  - 데이터를 스토리지 파일로 내보냄 <-> RDBMS : 데이터 파일 용량이 크기 때문에, 확장을 할 때는 데이터를 통째로 옮겨야 함(export)
  - 키워드 : 로드발란싱, 클러스터링
  
---
  
- 개념 및 명령어
  - collection - inventory(table과 같은 개념, 분류해줌)
  - show collections
  - db.inventory.find()
  - db.locker.insertOne({name:'locker'})
  - insertMany([{name:test1}, {name:test2}])
  
<table>
  <tr>
    <td></td>
    <td>SQL</td>
    <td>MongoDB</td>
  </tr>
  <tr>
    <td>INSERT</td>
    <td>insert into users ("name","city") values("terry","seoul")</td>
    <td>db.users.insert({_id:"terry",city:"seoul"})</td>
  </tr>
  <tr>
    <td>SELECT</td>
    <td>select * from users where id="terry"</td>
    <td>db.users.find({_id:"terry"})</td>
  </tr>
  <tr>
    <td>UPDATE</td>
    <td>update users set city="busan" where _id="terry"</td>
    <td>db.users.update({_id:"terry"}, {$set:{city:"Busan"}})</td>
  </tr>
  <tr>
    <td>DELETE</td>
    <td>delete from users where _id="terry"</td>
    <td>db.users.remove({_id:"terry"})</td>
  </tr>
</table>  
  
---

- MongoDB Compass
![ex_screenshot](https://raw.githubusercontent.com/abarthdew/dbms-for-dev/main/MongoDB/images/MongoDB_Compass.png)

---
  
- 환경변수 등록
![ex_screenshot](https://raw.githubusercontent.com/abarthdew/dbms-for-dev/main/MongoDB/images/환경변수.png)

---

- reference
  - https://docs.mongodb.com/manual/crud/
  - https://docs.mongodb.com/manual/tutorial/insert-documents/
  - https://docs.mongodb.com/manual/tutorial/query-documents/
  - https://javacpro.tistory.com/64
  - https://bcho.tistory.com/742
  - https://plugins.jetbrains.com/plugin/7141-mongo-plugin/
