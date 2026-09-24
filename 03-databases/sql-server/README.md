# SQL server-for-beginner

<li>스키마란?</li>
-명세서 개념<br>
-DB를 어떻게 구성할지 <br>
-일종의 설계도<br>
https://www.youtube.com/watch?v=RcxXlBKBKmQ <br>

<br>

<table>
  <tr>
    <th>MS-SQL</th>
    <th>HOW-TO-USE</th>
  </tr>
  <tr>
    <td>GO</td>
    <td>쿼리를 끝맺을 때</td>
  </tr>
  <tr>
    <td>USE [master]</td>
    <td>master 테이블로 이동</td>
  </tr>
  <tr>
    <td>
      CREATE DATABASE [table] ON  PRIMARY
      <li>CREATE DATABASE [table] : 테이블 생성</li>
      <li>ON PRIMARY : PRIMARY 그룹에 저장</li>
    </td>
    <td>
      <li>https://docs.microsoft.com/ko-kr/sql/relational-databases/databases/create-a-database?view=sql-server-2017</li>
      <li>http://www.sqler.com/index.php?mid=bSQLQA&page=7&document_srl=502186</li>
      <hr>
      <li>https://mozi.tistory.com/293</li>
    </td>
  </tr>
  <tr>
    <td>
      ALTER DATABASE [table] SET
      <br><i>(ex)ALTER DATABASE [table] SET COMPATIBILITY_LEVEL = 100</i>
      <br><i>(ex)ALTER DATABASE [table] SET ANSI_NULLS OFF</i>
    </td>
    <td>
      데이터베이스 옵션 설정
      <li>(MSSQL)https://docs.microsoft.com/ko-kr/sql/t-sql/statements/alter-database-transact-sql-set-options?view=sql-server-2017</li>
      <li>(ORACLE)http://www.gurubee.net/lecture/1086</li>
    </td>
  </tr>
  <tr>
    <td colspan=2>
      <br>https://docs.microsoft.com/ko-kr/sql/t-sql/statements/alter-database-transact-sql-compatibility-level?view=sql-server-2017
      <li>SET COMPATIBILITY_LEVEL : 호환성 수준</li>
      <br>https://docs.microsoft.com/ko-kr/sql/t-sql/statements/set-ansi-null-dflt-on-transact-sql?view=sql-server-2017
      <li>SET ANSI_NULL_DEFAULT : 기본 null허용 여부보다 우선 적용</li>
      <br>https://ellieya.tistory.com/54
      <li>SET ANSI_NULLS : null, 0 반환 관련</li>
      <br>http://time2relax.net/wp/?p=372
      <li>SET ANSI_PADDING : 공백</li>
      <br>https://m.blog.naver.com/PostView.nhn?blogId=b1ackjean&logNo=220329283248&proxyReferer=&proxyReferer=https%3A%2F%2Fwww.google.com%2F
      <li>SET ANSI_WARNINGS</li>
      <br>http://www.taeyo.net/Forum/Content.aspx?SEQ=1334&TBL=KNOWHOW
      <li>SET ARITHABORT</li>
      <br>https://vstarmanv.tistory.com/175
      <li>SET AUTO_CLOSE</li>
  </tr>
  <tr>
    <td>sp_fulltext_database</td>
    <td>
      이전 버전과 호환 유지
      <li>https://docs.microsoft.com/ko-kr/sql/relational-databases/system-stored-procedures/sp-fulltext-database-transact-sql?view=sql-server-2017</li>
    </td>
  </tr>
  <tr>
    <td>FULLTEXTSERVICEPROPERT</td>
    <td>
      전체 텍스트 엔진의 속성과 관련된 정보를 반환
      <li>https://docs.microsoft.com/ko-kr/sql/t-sql/functions/fulltextserviceproperty-transact-sql?view=sql-server-2017</li>
    </td>
  </tr>
  <tr>
    <td>CREATE USER [user_name] FOR LOGIN [user_name] WITH DEFAULT_SCHEMA=[dbo]</td>
    <td>
      현재 데이터베이스에 사용자를 추가
      <li>https://docs.microsoft.com/ko-kr/sql/t-sql/statements/create-user-transact-sql?view=sql-server-2017</li>
    </td>
  </tr>
  <tr>
    <td>CREATE TABLE [dbo].[table_name]( .... )ON [PRIMARY]</td>
    <td>테이블 생성</td>
  </tr>
  <tr>
    <td>
      <li>sp_addextendedproperty : 확장속성 추가</li>
      <li>sp_updateextendedproperty : 확장속성 수정</li>
      <li>sp_dropextendedproperty : 확장속성 삭제</li>
    </td>
    <td>
      <li>https://m.blog.naver.com/PostView.nhn?blogId=islove8587&logNo=220611473304&proxyReferer=https%3A%2F%2Fwww.google.com%2F</li>
    </td>
  </tr>
  <tr>
    <td></td>
    <td></td>
  </tr>
</table>  
