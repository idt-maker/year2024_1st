## Express 프레임워크 소개 및 설치

Express는 Node.js를 위한 빠르고 간편한 웹 애플리케이션 프레임워크입니다.

### 주요 특징

- **미들웨어:** 요청-응답 주기를 관리하는 함수들
- **라우팅:** URL에 따른 요청 처리 관리
- **템플릿 엔진 지원:** 동적 콘텐츠 생성 지원 (예: Pug, EJS)
- **정적 파일 제공:** CSS, 이미지 등의 정적 파일 서비스 용이

### 설치 방법

1. 프로젝트 폴더 생성 및 이동
2. `npm init` 실행하여 `package.json` 파일 생성
3. Express 설치:

```bash
npm install express --save
//npm 5.0 이후 에서는 필요없다. --save
```

4. `app.js` 파일 생성 및 기본 코드 작성:

```javascript
const express = require('express');
const app = express();
const port = 3000;

app.get('/', (req, res) => {
  res.send('Hello World!');
});

app.listen(port, () => {
  console.log(`Example app listening on port ${port}`);
});
```

5. `package.json`에 start 스크립트 추가:

```json
"scripts": {
  "app": "node app.js"
}
```

6. 애플리케이션 실행:

```bash
npm run app
```

