# Redis

## cli 설치

```bash
$ sudo apt install redis-server
```

```bash
$ netstat -nlpt | grep 6379
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
tcp        0      0 127.0.0.1:6379          0.0.0.0:*               LISTEN      -
tcp6       0      0 ::1:6379                :::*                    LISTEN
```

```bash
$ redis-cli // cli 실행
```

## Node.js + Redis

### chapter 1

#### hello.js

- import: 모듈 방식(ES6)
  - package.json에 추가 필요
    ```json
    "type": "module",
    // `"type": "module"`은 Node.js 프로젝트에서 ECMAScript 모듈 시스템을 사용하겠다는 것을 나타내는 설정입니다. 기존에는 CommonJS 형식이 기본이었지만, ECMAScript 2015 (ES6)부터 도입된 모듈 시스템을 사용하고자 할 때 이 설정을 추가합니다.
    // 이 설정을 사용하면, 파일 확장자 `.js` 파일도 기본적으로 ES 모듈로 취급됩니다. CommonJS 형식의 `require` 대신에 `import/export` 구문을 사용할 수 있게 됩니다. 이를 통해 더 모던하고 간결한 코드를 작성할 수 있습니다.
    ```

  - hello.js
    ```javascript
    import { createClient } from "redis"; // 1

    (async () => {
        const client = createClient(); // 2

        client.on('error', (err) => console.log('Redis Client Error', err));

        await client.connect();

        await client.set('my_key', 'hello world using node.js and Redis'); // 3

        const value = await client.get('my_key'); // 4
        console.log(value);

        client.quit();
      })();
    ```

- require: common js 방식
  - package.json에 위 module type 제거
  - hello.js
    ```javascript
    // 2
    const { createClient } = require('redis'); // 1
    (async () => {
        const client = createClient(); // 2

        client.on('error', (err) => console.log('Redis Client Error', err));

        await client.connect();

        await client.set('my_key', 'hello world using node.js and Redis'); // 3

        const value = await client.get('my_key'); // 4
        console.log(value);

        client.quit();
    })();
    ```

    ```javascript
    // 3
    const redis = require('redis'); // 1
    (async () => {
        const client = redis.createClient(); // 2

        client.on('error', (err) => console.log('Redis Client Error', err));

        await client.connect();

        await client.set('my_key', 'hello world using node.js and Redis'); // 3

        const value = await client.get('my_key'); // 4
        console.log(value);

        client.quit();
      })();
    ```

#### articles-popularity.js

- *showResult error*
  ```javascript
  async function showResults(id, recieveClient) {
    const client = await recieveClient;
    var headlineKey = "article:" + id + ":headline";
    var voteKey = "article:" + id + ":votes";
    client.mget([headlineKey, voteKey], function(err, replies) { // 1
      console.log('The article "' + replies[0] + '" has', replies[1], 'votes'); // 2
    });
  }
  ```

  ```javascript
  async function showResults(id, recieveClient) {
    const client = await recieveClient;
    var headlineKey = "article:" + id + ":headline";
    var voteKey = "article:" + id + ":votes";

    const replies = await new Promise((resolve, reject) => {
      client.mget([headlineKey, voteKey], (err, replies) => {
        if (err) {
          reject(err);
        } else {
          resolve(replies);
        }
      });
    });

    console.log("Headline Key:", headlineKey);
    console.log("Vote Key:", voteKey);
    console.log("Replies:", replies);

    console.log('The article "' + replies[0] + '" has', replies[1], 'votes');
  }
  ```

  > 위 결과: TypeError: client.mget is not a function

- 답변
  - `client` 객체가 `mget` 메서드를 지원하지 않기 때문에 발생. `mget` 메서드는 Redis 클라이언트의 기본 메서드 중 하나가 아님.
    ```javascript
    // client 객체를 사용하여 mget를 실행할 수 있도록 수정
    // Redis의 mget 메서드는 get 메서드를 여러 번 호출하는 것과 유사
    async function showResults(id, recieveClient) {
      const client = await recieveClient;
      var headlineKey = "article:" + id + ":headline";
      var voteKey = "article:" + id + ":votes";

      const [headline, votes] = await Promise.all([
        client.get(headlineKey),
        client.get(voteKey)
      ]);

      console.log("Headline Key:", headlineKey);
      console.log("Vote Key:", voteKey);
      console.log('The article "' + headline + '" has', votes, 'votes');
    }
    ```

  - 이렇게 수정하면 `client.get`을 사용하여 각 키에 대한 값을 얻어올 수 있음. 위 코드는 `Promise.all`을 사용하여 두 개의 비동기 작업을 병렬로 수행하고, 그 결과를 배열로 받아오게 됨. 이후 각 값에 접근하여 적절한 로그를 출력.

### export 파일에 함수를 선언과 동시에 실행하고 싶을 때

- 파일 내에서 함수가 선언되면 해당 함수는 그 자체의 스코프에 존재합니다. 따라서 파일 내에서 함수를 선언했다고 해서 자동으로 실행되지 않음.
- 즉시 실행 예시 코드 - 파일이 실행되면서 함수가 즉시 실행되고, 그 결과로 객체가 생성되어 export 됨.
  ```javascript
  import { createClient } from "redis";

  const myRedisModule = (() => {
    const client2 = async (param) => {
      const client = createClient();
      client.on('error', (err) => console.log('Redis Client Error', err));
      await client.connect();
      client.quit();
    };

    return {
      client2
    };
  })();

  export default myRedisModule;
  ```
