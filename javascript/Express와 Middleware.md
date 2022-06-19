## Express

　JavaScript 생태계에서 인기 있는 프레임워크의 앞글자를 따서 MERN stack (MongoDB, Express, React, Node) 로 부른다. 이 중 Express.js는 Node.js 를 위한 
 빠르고 개방적인 간결한 웹 프레임워크 중 하나로, 라우팅/세션과리 등 골치아픈 부분을 해결하여 쉽게 웹 서버를 구축할 수 있게 도와준다.

### express 설치

```javascript
// packages.json 파일 내 dependencies 목록에 추가
$ npm install express --save
```

### express 서버 생성
Hello world 예제는 공식문서를 참조하여 가장 간단하게 만들어볼 수 있는 서버이다.

```javascript
const express = require('express')
const app = express()
const port = 3000

app.get('/', (req, res) => {
  res.send('Hello World!')
})

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`)
})
```

### 라우팅: 메서드와 url에 따라 분기(Routing)하기

메서드와 url(/lower, /upper 등)로 분기점을 만드는 것을 라우팅(Routing)이라고 합니다.

클라이언트는 특정한 HTTP 요청 메서드(GET, POST 등)와 함께 서버의 특정 URI(또는 경로)로 HTTP 요청을 보냅니다. 
라우팅은 클라이언트의 요청에 해당하는 Endpoint에 따라 서버가 응답하는 방법을 결정하는 것입니다.

```javascript
const router = express.Router()

router.get('/lower', (req, res) => {
  res.send(data);
})

router.post('/lower', (req, res) => {
  // do something
})
```

## 미들웨어

자동차 공장에서는 컨베이어 벨트 위에 올려진 자동차의 뼈대에, 각 공정마다 부품을 추가합니다. 모든 부품이 추가되면 완성된 자동차가, 어딘가 문제가 있다면 불량품이 결과물로 나오게 됩니다. 미들웨어(Middleware)는 자동차 공장의 공정과 비슷합니다. 컨베이어 벨트 위에 올라가 있는 요청(Request)에 필요한 기능을 더하거나, 문제가 발견된 불량품을 밖으로 걷어내는 역할을 합니다. 미들웨어는 express의 가장 큰 장점이라고 할 수 있습니다.

### 자주 사용하는 미들웨어

미들웨어를 사용하는 상황<br>
1.POST 요청 등에 포함된 body(payload)를 구조화할 때(쉽게 얻어내고자 할 때)<br>
2.모든 요청/응답에 CORS 헤더를 붙여야 할 때<br>
3.모든 요청에 대해 url이나 메서드를 확인할 때<br>
4.요청 헤더에 사용자 인증 정보가 담겨있는지 확인할 때

미들웨어는 app.use와 함께 사용된다
app.use()

### case 1: POST 요청 등에 포함된 body(payload)를 구조화할 때

Node.js로 HTTP body(payload)를 받을 때에는 Buffer를 조합해서 다소 복잡한 방식으로 body를 얻을 수 있습니다.
body-parser 미들웨어를 사용하면 이 과정을 간단하게 처리할 수 있습니다.

```javascript
const bodyParser = require('body-parser');
const jsonParser = bodyParser.json();

// 생략
app.post('/users', jsonParser, function (req, res) {

})
```
Express v4.16.0 부터는 body-parser를 따로 설치 하지 않고, Express 내장 미들웨어인 express.json()을 사용합니다.

```javascript
const jsonParser = express.json();

// 생략
app.post('/api/users', jsonParser, function (req, res) {

})
```

### case 2: 모든 요청/응답에 CORS 헤더를 붙일 때

Node.js HTTP 모듈을 이용한 코드에 CORS 헤더를 붙이려면, 응답 객체의 writeHead 메서드를 이용할 수 있습니다. 
Node.js에서는 이 메서드 등을 이용하여 라우팅마다 헤더를 매번 넣어주어야 합니다. 그뿐만 아니라, OPTIONS 메서드에 대한 라우팅도 따로 구현해야 했지만 
cors 미들웨어를 사용하면 이 과정을 간단하게 처리할 수 있습니다.


```javascript
npm install cors//npm으로 cors를 설치

const cors = require('cors')

// 생략
app.use(cors()) // 모든 요청에 대해 CORS 허용
const cors = require('cors')

// 생략
// 특정 요청에 대해 CORS 허용
app.get('/products/:id', cors(), function (req, res, next) {
  res.json({msg: 'This is CORS-enabled for a Single Route'})
})
```

### case 3: 모든 요청에 대해 url이나 메서드를 확인할 때

미들웨어는 말 그대로 프로세스 중간에 관여하여 특정 역할을 수행합니다. 수많은 미들웨어가 있지만, 가장 단순한 미들웨어 로거(logger)를 예로 들겠습니다. 로거는 디버깅이나, 서버 관리에 도움이 되기 위해 console.log로 적절한 데이터나 정보를 출력합니다. 데이터가 여러 미들웨어를 거치는 동안 응답할 결과를 만들어야 한다면, 미들웨어 사이사이에 로거를 삽입하여 현재 데이터를 확인하거나, 디버깅에 사용할 수 있습니다. 이런 미들웨어는 일반적으로 다음과 같은 구성을 가집니다.

<img width="1023" alt="auEpUwrE7-1600964704103" src="https://user-images.githubusercontent.com/56382506/174470232-947c0d78-51bc-4204-a516-fd4bcf083228.png">

위 그림은 endpoint가 /이면서, 클라이언트로부터 GET 요청을 받았을 때 적용되는 미들웨어입니다. 파라미터의 순서에 유의해야 합니다. req, res는 우리가 잘 아는 요청(request), 응답(response)이고 next는 다음 미들웨어를 실행하는 역할을 합니다.

만약 특정 enpoint가 아니라, 모든 요청에 동일한 미들웨어를 적용하려면 어떻게 해야 할까요? 메서드 app.use 를 사용하면 됩니다. 아래 코드를 직접 실행해 보세요. 모든 요청에 대해 LOGGED가 출력되는 걸 확인할 수 있습니다.


```javascript
const express = require('express');
const app = express();

const myLogger = function (req, res, next) {
  console.log('LOGGED');
  next();
};

app.use(myLogger);

app.get('/', function (req, res) {
  res.send('Hello World!');
});

app.listen(3000);
```

### case 4: 요청 헤더에 사용자 인증 정보가 담겨있는지 확인할 때

다음은 HTTP 요청에서 토큰이 있는지를 판단하여, 이미 로그인한 사용자일 경우 성공, 아닐 경우 에러를 보내는 미들웨어 예제입니다.

```javascript
app.use((req, res, next) => {
  // 토큰이 있는지 확인, 없으면 받아줄 수 없음.
  if(req.headers.token){
    req.isLoggedIn = true;
    next();
  } else {
    res.status(400).send('invalid user')
  }
})
```






