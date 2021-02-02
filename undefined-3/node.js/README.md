# node.js

### node js 자동화를 위한 참고 페이지

{% embed url="https://medium.com/stackfame/how-to-run-shell-script-file-or-command-using-nodejs-b9f2455cb6b7" %}

{% embed url="https://stackabuse.com/executing-shell-commands-with-node-js/" %}

{% embed url="http://magic.wickedmiso.com/143" %}

### get방식으로 url에 파라미터가 들어온 경우에는?

* req.query 로 해당 파라미터를 조회할 수 있다. 이 때 req.query를 사용하려면 반드시 body-parser 모듈을 사용해야 한다.

### async, await 

* async와 await는 같은 함수 안에 있어야 사용할 수 있다.
* mongodb의 insertOne과 같은 메소드는 promise를 반환해 주기 때문에 then을 사용할 수 있고, 마찬가지로 async, await 가 따로 promise 의 구현이 필요 없이 사용이 가능하다.
* async 함수는 무조건 Promise를 반환한다.
* await 도 무조건 Promise를 반환하게 만들어야 한다.
* 만약, async 함수의 return 값을 가지고 무엇을 작업하고 싶다면, async 함수는 Promise를 return 하기 때문에 then을 써서 그 다음에 원하는 작업을 해 주어야 한다.

```javascript
async function test() {
    const insertUer = await mongodb.collection('user')
    .insertOne({id: userid, name: username, password: userid});
    
    return insertUser.result.ok;
}

test()
.then((result) => {
    if (result == 1) {
        alert('추가 되었습니다.');
    }
})

```

### 사용중인 node 서버 찾기 및 kill

* sudo lsof -i : {port} -&gt; port번호가 사용중인 process ID를 얻기.
* sudo kill -9 :{PID} -&gt; kill

### REST API 에러 처리

{% embed url="https://velog.io/@smooth97/Node.js-Restful-API-wok2wqo7yu" %}

{% embed url="https://developer.mozilla.org/ko/docs/Web/HTTP?Status" %}

{% embed url="https://sanghaklee.tistory.com/61" %}

### address already in use 해결방법

```javascript
// 1.해당 포트번호를 찾는다.
$ lsof -i TCP: port번호

// 2.1번에서 검색된 PID를 사용한다.
$ kill -9 PID
```

