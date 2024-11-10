## 실습: 간단한 Node.js/Express 서버 작성

이 부분은 이미 위의 Express 설치 및 기본 서버 작성 과정에서 다루었습니다. 학습자들은 이 기본 서버를 확장하여 추가적인 라우트를 만들거나, 미들웨어를 사용해볼 수 있습니다.

예를 들어, 새로운 라우트 추가:

새로운 프로젝트 작성
```  
npm init -y
npm install express

```

app.js 작성  

```  
// 필요한 모듈 불러오기
const express = require('express');
const fs = require('fs');
const path = require('path');

// Express 애플리케이션 생성
const app = express();
const port = 3000;

// 미들웨어 설정
app.use(express.json());

// 루트 경로 핸들러
app.get('/', (req, res) => {
    res.send('Node.js와 Express를 사용한 간단한 서버입니다!');
});

// 비동기 파일 읽기 예제 (이벤트 루프 활용)
app.get('/read-file', (req, res) => {
    const filePath = path.join(__dirname, 'example.txt');
    
    fs.readFile(filePath, 'utf8', (err, data) => {
        if (err) {
            console.error('파일 읽기 오류:', err);
            return res.status(500).send('파일을 읽는 중 오류가 발생했습니다.');
        }
        res.send(data);
    });
});

// 서버 시작
app.listen(port, () => {
    console.log(`서버가 http://localhost:${port} 에서 실행 중입니다.`);
});

// 사용자 정의 모듈 예제
const customModule = require('./customModule');
app.get('/custom', (req, res) => {
    res.send(customModule.getMessage());
});

```


모듈 사용할수 있게 js 작성
```
// 사용자 정의 모듈 예제
module.exports = {
    getMessage: () => '이것은 사용자 정의 모듈에서 온 메시지입니다!'
};

```
간다하게 txt파일 작성
```
이것은 example.txt 파일의 내용입니다. 파일 시스템 모듈을 통해 읽혀집니다.
```

서버실행  
```
node app.js
```

```
http://localhost:3000, 
http://localhost:3000/read-file, 
http://localhost:3000/custom에
```


템플릿 사용한 방법 (네비게이션)  
```
npm install ejs
```


