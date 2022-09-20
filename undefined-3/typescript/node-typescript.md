# node에 typescript

* node가 설치되어 있다는 가정하에 터미널에 node typescript를 설치한다.

```typescript
$ yarn add @types/node, @types/express
```

#### 빌드 설정

```typescript
// 터미널에 아래 명령어를 치게 되면 tsconfig.json 파일이 생성된다.
$ npx tsc -init
```

#### 주의할 점// 아래와 같이 입력하게 되면, require는 any type이기 때문에

```typescript
// typescript의 기능을 제대로 사용할 수 없다.
const expess = require('express');

// 따라서, 아래와 같이 쓰면 좋다.
import * as express from 'express';
```

###
