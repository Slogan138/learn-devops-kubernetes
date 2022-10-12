# Building Containers

- 컨테이너 이미지를 빌드하기 위해선 Docker Engine 을 사용할 수 있음
    - 혹은 강의에서 제공해주는 docker 가 설치된 vagrant devops-box 를 이용할 수 있음

# Dockerfile

간단한 NodeJS 앱을 도커라이징 하기 위해선 몇몇 파일들이 필요함

- Dockerfile

```dockerfile
FROM node:4.6
WORKDIR /app
ADD ./app
RUN npm install
EXPOSE 3000
CMD npm start
```

- index.js

```javascript
var express = require('express');
var app = express();

app.get('/', function (req, res) {
    res.send('Hello World!');
});

var server = app.listen(3000, function () {
    var host = server.address().address;
    var port = server.address().port;

    console.log('Example app listening at http://%s:%s', host, port);
})
```

- package.json

```json
{
    "name": "myapp",
    "version": "0.0.1",
    "private": true,
    "scripts": {
        "start": "node index.js"
    },
    "engines": {
        "node": "^4.6.1"
    },
    "dependencies": {
        "express": "^4.1.0"
    }
}
```

- 프로젝트를 빌드하기 위해서 `docker build` 커맨드를 이용해서 직접 빌드할 수 있음
- 수동으로 도커 이미지를 빌드할 수 있지만 Jenkins 와 같은 CI/CD 소프트웨어로 빌드할 수 있음