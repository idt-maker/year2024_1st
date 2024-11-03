# 5주차: Node.js 기초

## Node.js 소개 및 설치

![alt text](5imgremade/image-2.png)
### Node.js란?

Node.js는 "Chrome V8 JavaScript 엔진으로 빌드된 JavaScript 런타임"입니다. 이는 JavaScript를 서버 사이드에서 실행할 수 있게 해주는 플랫폼입니다. 과거에는 JavaScript가 주로 웹 브라우저에서만 동작하는 프론트엔드 언어로 사용되었지만, Node.js의 등장으로 백엔드 개발에도 사용할 수 있게 되었습니다.

### Node.js의 동작 방식

Node.js는 비동기 이벤트 기반 아키텍처를 사용합니다. 이를 설명하기 위해 티켓 예매 시나리오를 살펴보겠습니다:

**일반 서버의 경우:**
1. 첫 번째 손님이 티켓 1장을 요청하고 받습니다.
2. 두 번째 손님은 첫 번째 손님의 처리가 끝날 때까지 기다린 후 티켓을 요청합니다.
3. 세 번째 손님이 200장을 요청하면, 서버는 이 요청을 처리하는 동안 다른 모든 요청을 대기시킵니다.

**Node.js 서버의 경우:**
- 모든 요청을 동시에 받아들이고, 처리 속도가 빠른 순서대로 결과를 반환합니다.
- 이는 Node.js의 **Non-blocking I/O** 특성 때문입니다.

### Node.js의 강점

1. **실시간 애플리케이션에 적합:** SNS, 채팅 서비스 등 많은 요청을 처리해야 하는 애플리케이션에 적합합니다.
2. **빠른 개발:** 코드가 간결하여 빠른 개발과 피봇팅이 가능합니다.
3. **대규모 서비스에서의 검증:** 에어비엔비, 넷플릭스, 페이팔 등 대규모 서비스에서 사용되어 안정성과 보안성이 검증되었습니다.

### Node.js의 단점

- CPU 집약적인 작업에는 적합하지 않습니다. 이미지/비디오 처리, 대규모 데이터 처리 등에는 다른 언어나 플랫폼이 더 적합할 수 있습니다.

### 설치 방법

1. [Node.js 공식 웹사이트](https://nodejs.org/)에서 설치 파일을 다운로드합니다.
2. 설치 파일을 실행하고 안내에 따라 설치를 진행합니다.
![alt text](5imgremade/image-3.png)


3. 설치가 완료되면 명령 프롬프트(cmd)에서 다음 명령어로 설치를 확인할 수 있습니다:



```bash
node --version
npm --version
```

설치 확인  
![alt text](5imgremade/image-4.png)