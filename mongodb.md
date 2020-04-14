# mongodb

{% embed url="https://poiemaweb.com/mongoose" %}

{% embed url="https://www.mongodb.com/download-center/community?jmp=nav" caption="puppy912000@naver.com song anjelra " %}

### mongodb 설치하기

![](.gitbook/assets/image%20%2815%29.png)

{% embed url="https://velog.io/@rohkorea86/MongoDB%EC%84%A4%EC%B9%98-%EB%A7%A5MAC%EC%97%90%EC%84%9C-%EB%AA%BD%EA%B3%A0%EB%94%94%EB%B9%84-%EC%84%A4%EC%B9%98" %}

{% embed url="https://kimhc999.tistory.com/62" %}

#### 중요!!!!! 처음에 잘 안됐던 이유!! data/db 폴더를 생성하고, 서버가 구동되는 폴더 경로를 재 설정 한다.\(--dbpath 사용\)

숨김파일 찾으려면 폴더로 이동을 보면 됨 -&gt; 단축키: command + shift + G 누르고나서 다 안쳐도 탭 누르면 자동완성됨.

![](.gitbook/assets/image%20%288%29.png)

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

![](.gitbook/assets/image%20%286%29.png)

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

