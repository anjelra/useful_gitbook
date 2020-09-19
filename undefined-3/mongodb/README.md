# mongodb

{% embed url="https://poiemaweb.com/mongoose" %}

{% embed url="https://www.mongodb.com/download-center/community?jmp=nav" caption="puppy912000@naver.com song anjelra " %}

### mongodb 설치하기

![](../../.gitbook/assets/image%20%2815%29.png)

{% embed url="https://velog.io/@rohkorea86/MongoDB%EC%84%A4%EC%B9%98-%EB%A7%A5MAC%EC%97%90%EC%84%9C-%EB%AA%BD%EA%B3%A0%EB%94%94%EB%B9%84-%EC%84%A4%EC%B9%98" %}

{% embed url="https://kimhc999.tistory.com/62" %}

#### 중요!!!!! 처음에 잘 안됐던 이유!! data/db 폴더를 생성하고, 서버가 구동되는 폴더 경로를 재 설정 한다.\(--dbpath 사용\)

#### mongod --dbpath /Users/song-anjelra/database/data

숨김파일 찾으려면 폴더로 이동을 보면 됨 -&gt; 단축키: command + shift + G 누르고나서 다 안쳐도 탭 누르면 자동완성됨.

![](../../.gitbook/assets/image%20%288%29.png)

### mongodb 기본 사용방법\(user 추가\)

{% embed url="https://datamod.tistory.com/28" %}

### mongodb 실행

1. mongo -&gt; 명령어를 치면 mongo db 가 실행됨.
2. use tasks -&gt; tasks 라는 데이터베이스를 사용하겠음.

* db -&gt; 현재 사용하고 있는 데이터 베이스를 확인.
* show dbs -&gt; 서버 안의 데이터 베이스 리스트를 확인. 그러나, 방금 만든 tasks 데이터베이스는 없을 수도 있음. 이유는 해당 데이터베이스에 최소 한개의 Document 가 존재해야 show dbs를 통해 확인할 수 있음.

### database 제거

* db.dropDatabase\(\) -&gt; 이 명령어는 use tasks 처럼 지울 데이터베이스가 선택되어 있어야 함.

### Collection 생성: db.createCollection\(\)

* db.createCollection\(name \[,options\]\) -&gt; collection을 생성할 때 사용. name은 Collection의 이름을 지정하는 인자이고, options는 Collection의 설정을 변경해주는 인자임. Collection을 만드는 것은 Document를 생성하는 insert 메소드를 통해서도 할 수 있지만, createCollection 메소드를 사용하는 이유는 options 때문임.

![](../../.gitbook/assets/image%20%286%29.png)

1. tasks 데이터베이스에 deploy 컬렉션을 옵션없이 생성

* use tasks
* db.createCollection\("deploy"\) -&gt; 이렇게 하면 최소 한개의 Document 가 있으므로 show dbs;라는 명령어를 치면 tasks가 보이는 것을 확인할 수 있음.

2. tasks 데이터베이스에 deploy 컬렉션을 옵션과 함께 생성

* db.createCollection\("deploy", {

  capped: true,

* size: 4135000,
* max: 10000
* }\) -&gt;  이런 식으로 할 수 있음.

### db user 확인

* db.getUsers\(\) 

### db user 추가

1. 관리자 생성

```text
use admin
db.createUser(
    {
        user: "root",
        pwd: "samsung2!",
        roles: [ {role: "userAdminAnyDatabase", db: "admin"} ]
    }
)
```

2. 계정 생성

```text
use tasks
db.createUser(
    {
        user: "tasks",
        pwd: "itdnsdud",
        roles: [ {role: "readWrite", db: "tasks"} ]
    }
)
```

### db user 삭제

```text
use tasks
db.dropUser("anjelra");
```

### db collection

* show collections -&gt; 컬렉션 리스트 확인
* db.컬렉션명.drop\(\) -&gt; 해당 이름을 가진 컬렉션을 제거
* db.OLD컬렉션명.renameCollection\("NEW컬렉션명"\) -&gt; 이름변

### db document\(data 라고 생각하면 됨\)

* db.컬렉션명.insert\(document\) -&gt; document 추가. 
* db.컬렉션명.find\(\[query, projection\]\) -&gt; collection의 document list 조회.
  * 전체 document list를 조회하고 싶으면, ex\) db.deploy.find\( {} \)
* db.컬렉션명.find\(\[query, projection\]\).pretty\(\) -&gt; collection의 document list 조.\(json이 이쁘게 나옴\)
  * query : document 타입. Optional 이며, document를 조회할 때 기준을 정한다. 모든 document를 조회할 때는 이 매개변수를 비우거나, {}를 전달하면 됨.
  * projection: document 타입. Optional 이며, document를 조회할 때 보여질 field를 정함. 
    * ex: db.articles.find\({ }, { "\_id": false, "title": true, "content": true }\)
* db.컬렉션명.remove\(criteria\[, justOne\]\) -&gt; document 제거
  * criteria: document 타입. 데이터의 기준 값으로서 일치하면 기본적으로 다 삭제함. 이 값이 { }이면 컬렉션의 모든 데이터를 제거함. 반드시 넣어야 함.
  * justOne boolean타입. Optional 매개변수이며, 이 값이 true면 1개의 document만 제거함. 이 매개변수가 생략되면 기본값은 false이고 criteria에 해당되는 모든 document를 제거함.
* db.컬렉션명.deleteOne\({ name: 'anjelra'}\) -&gt; name이 anjelra이 한 개의 데이터를 지.
* db.컬렉션명.deleteMany\({name:'anjelra'}\) -&gt; name이 anjelra인 모든 도큐멘트를 지.
* db.컬렉션명.count\(\) -&gt; document 갯수를 출력. 
* db.컬렉션명.update\(

  {"makeDataDate": "2020/04/16 10:07:13"},{$set: {"makeDataDate": "2020/04/16 10:07:13", "diffItem" : \[ { "filePath" : "/ria/common/resource/ModuleCar.js", "lastModified" : "Tue, 14 Apr 2020 01:41:04 GMT", "status" : "modified", "version" : { "modified" : "2020-04-14 10:31:18", "deploy" : "2020-04-14 10:31:26", "hash" : "c8ec4134d305dfac37b71daab4002eb75e595bc7W" } } \] } }

\)  -&gt; 변경할 도큐먼트, 변경할 값을 넣으면 해당 document가 변경됨.

{% embed url="https://sjh836.tistory.com/100" %}

### mongodb의 권한이 설정되어 있다면?

1. admin 으로 변경\(mongo -u root -p "1234"\)
2. 사용하고자 하는 db로 변경\(use tasks\)
3. 권한 추가 \( db.createUser\( {user: "anjelra", pwd: "samsung2!",  roles: \[{ role: "readWrite", db: "tasks"}\] } \) \)
4. command + C로 mongo 종료
5. mongo 명령어 사용해서 mongodb로 진입\(mongo\)
6. use tasks -&gt; tasks database 로 이동\(왜냐하면, api user는 다른 데이터베이스에는 권한이 없기 때문에\)
7. 아직 사용자가 없음. 만약 admin으로 사용자를 입력해서 들어오게 되면, 사용자가 많다고 하면서 에러를 뱉으니 일단 mongo로만 진입한 다음, db.auth\("api", "itdnsdud"\); 로 사용자를 로그인.
8. 그리고 collection을 만듦. -&gt; db.createCollection\("deploy"\)

### mongodb find \(select\)

{% embed url="https://pro-self-studier.tistory.com/59" %}

{% embed url="https://minimilab.tistory.com/43" %}

### mongoose

{% embed url="https://mongoosejs.com/docs/connections.html" %}





