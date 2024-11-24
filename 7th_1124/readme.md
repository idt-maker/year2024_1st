**7주차: 풀스택 개발 기초**

- Vue.js와 Node.js/Express 연동
- Axios를 이용한 HTTP 통신
- CORS (Cross-Origin Resource Sharing)
- 실습: Vue.js 애플리케이션과 Node.js/Express API 서버 연동


## 1. Vue.js와 Node.js/Express 연동


Vue.js와 Node.js/Express를 연동하여 풀스택 애플리케이션을 구축하는 방법을 알아봅니다. Vue.js는 프론트엔드에서 사용자 인터페이스를 담당하고, Node.js/Express는 백엔드에서 API 서버 역할을 수행하여 데이터를 처리합니다.

### 1.1 Vue.js란?

**Vue.js**는 사용자 인터페이스를 만들기 위한 자바스크립트 프레임워크입니다. 컴포넌트 기반으로 설계되어 있어 재사용 가능한 UI 요소를 쉽게 만들 수 있습니다. Vue는 데이터 바인딩, 반응형 시스템 등을 통해 사용자 경험을 향상시키며, 현대적인 웹 애플리케이션 개발에 적합한 도구입니다.

### 1.2 Node.js/Express란?

**Node.js**는 서버 사이드 자바스크립트 런타임 환경으로, 비동기 이벤트 기반 구조 덕분에 고성능 서버 애플리케이션을 구축할 수 있습니다. **Express**는 Node.js에서 사용할 수 있는 경량 웹 프레임워크로, 간단한 API 서버부터 복잡한 웹 애플리케이션까지 다양한 서버 애플리케이션을 쉽게 구축할 수 있도록 도와줍니다.

---

### 1.3 예제: Vue.js와 Express 연동

이제 Vue.js와 Express를 연동하는 기본적인 예제를 살펴보겠습니다.

#### Step 1: Express API 서버 생성

1. **Express 설치 및 프로젝트 설정**
   ```bash
   mkdir express-api
   cd express-api
   npm init -y
   npm install express cors
   ```

2. **간단한 API 서버 작성** (`index.js` 파일)
   ```javascript
   const express = require('express');
   const cors = require('cors');
   const app = express();

   // CORS 허용 설정
   app.use(cors());

   // JSON 데이터 파싱 설정
   app.use(express.json());

   // 간단한 GET API 엔드포인트 생성
   app.get('/api/message', (req, res) => {
     res.json({ message: 'Hello from Express!' });
   });

   app.listen(3000, () => {
     console.log('API 서버가 포트 3000에서 실행 중입니다.');
   });
   ```

3. **서버 실행**
   ```bash
   node index.js
   ```
   
#### Step 2: Vue 프로젝트에서 Axios로 API 호출

1. **Vue 프로젝트 생성**
   ```bash
   vue create vue-app
   cd vue-app
   npm install axios
   ```

2. **Vue 컴포넌트에서 Axios로 API 호출** (`App.vue` 파일)
   
   ```vue
   <template>
     <div id="app">
       <h1>{{ message }}</h1>
       <button @click="fetchMessage">메시지 가져오기</button>
     </div>
   </template>

   <script>
   import axios from 'axios';

   export default {
     data() {
       return {
         message: '메시지를 가져오세요!'
       };
     },
     
     methods: {
       fetchMessage() {
         axios.get('http://localhost:3000/api/message')
           .then(response => {
             this.message = response.data.message;
           })
           .catch(error => {
             console.error("API 요청 중 오류 발생:", error);
           });
       }
     }
   };
   </script>

   <style>
   #app {
     font-family: Avenir, Helvetica, Arial, sans-serif;
     text-align: center;
     margin-top: 60px;
   }
   </style>
   ```

3. **Vue 애플리케이션 실행**
   
    ```bash
    npm run serve
    ```

이제 브라우저에서 `http://localhost:8080`에 접속하여 "메시지 가져오기" 버튼을 클릭하면 Express 서버로부터 "Hello from Express!" 메시지를 받아볼 수 있습니다.

---

### 요약

이 예제에서는 **Vue.js**와 **Node.js/Express**를 연동하여 풀스택 애플리케이션을 구축하는 방법을 배웠습니다. 프론트엔드(Vue)에서 Axios를 사용해 백엔드(Express)로 HTTP 요청을 보내고, CORS 설정을 통해 두 서버 간의 통신을 원활하게 처리했습니다.


## 2. Axios를 이용한 HTTP 통신

### 2.1 Axios란?
**Axios**는 브라우저와 Node.js에서 모두 사용할 수 있는 Promise 기반의 HTTP 클라이언트입니다. 주로 RESTful API와 통신할 때 사용되며, GET, POST, PUT, DELETE 등의 요청을 쉽게 보낼 수 있습니다. Axios는 JSON 데이터를 자동으로 변환하고, 비동기 요청을 쉽게 처리할 수 있도록 도와줍니다.

### 2.2 Axios 설치
Axios는 npm 또는 yarn을 통해 설치할 수 있습니다.

```bash
npm install axios
```

---

### 2.3 Axios 메서드별 사용 예제

#### 1. **GET 요청**: 데이터를 서버에서 가져올 때 사용합니다.

```javascript
import axios from 'axios';

axios.get('https://api.example.com/users')
  .then(response => {
    console.log(response.data); // 서버에서 받은 데이터 출력
  })
  .catch(error => {
    console.error('Error fetching data:', error);
  });
```
- **GET** 요청은 주로 데이터를 조회할 때 사용됩니다.
- 같은 요청을 여러 번 반복해도 결과가 동일합니다(멱등성).

#### 2. **POST 요청**: 서버에 새로운 데이터를 생성할 때 사용합니다.

```javascript
axios.post('https://api.example.com/users', {
    name: 'John Doe',
    email: 'john@example.com'
  })
  .then(response => {
    console.log('User created:', response.data);
  })
  .catch(error => {
    console.error('Error creating user:', error);
  });
```
- **POST**는 새로운 데이터를 서버에 전송하여 생성하는 데 사용됩니다.
- 같은 요청을 여러 번 반복해도 결과가 달라질 수 있습니다(비멱등성).

#### 3. **PUT 요청**: 기존 데이터를 수정할 때 사용합니다.

```javascript
axios.put('https://api.example.com/users/1', {
    name: 'Jane Doe',
    email: 'jane@example.com'
  })
  .then(response => {
    console.log('User updated:', response.data);
  })
  .catch(error => {
    console.error('Error updating user:', error);
  });
```
- **PUT**은 기존 리소스를 완전히 교체하거나 수정하는 데 사용됩니다.
- 여러 번 호출해도 결과가 동일하게 유지됩니다(멱등성).

#### 4. **DELETE 요청**: 서버에서 데이터를 삭제할 때 사용합니다.

```javascript
axios.delete('https://api.example.com/users/1')
  .then(response => {
    console.log('User deleted:', response.data);
  })
  .catch(error => {
    console.error('Error deleting user:', error);
  });
```
- **DELETE**는 서버에서 특정 리소스를 삭제하는 데 사용됩니다.
- 여러 번 호출해도 결과가 동일하게 유지됩니다(멱등성).

---

### 요약

Axios를 사용하면 다양한 HTTP 메서드를 통해 서버와 통신할 수 있습니다. 각 메서드는 다음과 같은 목적에 맞게 사용됩니다:
- **GET**: 데이터 조회 (멱등성 있음)  
  * 데이터를 조회하는 메서드로, 여러 번 요청하더라도 서버의 상태는 변하지 않습니다  

- **POST**: 데이터 생성 (비멱등성)  
  * 데이터를 생성하는 메서드로, 같은 요청을 여러 번 보내면 매번 새로운 리소스가 생성될 수 있습니다.  
- **PUT**: 데이터 수정 (멱등성 있음)  
  * 리소스를 생성하거나 수정하는 메서드로, 같은 요청을 여러 번 보내더라도 결국 리소스는 동일한 상태로 덮어씌워집니다.  
 
- **DELETE**: 데이터 삭제 (멱등성 있음)  
  * 리소스를 삭제하는 메서드로, 첫 번째 요청에서 리소스가 삭제되고 이후 동일한 요청을 보내더라도 이미 삭제된 상태가 유지되므로 서버의 상태는 변하지 않습니다.  

---

## 3. CORS (Cross-Origin Resource Sharing)

### 3.1 CORS란?

CORS(Cross-Origin Resource Sharing)는 웹 브라우저에서 다른 출처(도메인, 프로토콜, 포트)를 가진 리소스를 요청할 때 발생하는 보안 메커니즘입니다. 기본적으로 브라우저는 동일 출처 정책(Same-Origin Policy, SOP)에 따라 다른 출처의 리소스 요청을 차단합니다. 이로 인해, 클라이언트가 API 서버와 같은 도메인이 아니거나 다른 포트를 사용하는 경우 CORS 에러가 발생할 수 있습니다.

CORS는 이러한 문제를 해결하기 위해 서버에서 특정 헤더를 설정하여 클라이언트가 다른 출처의 리소스에 접근할 수 있도록 허용하는 방법입니다. 서버가 응답 헤더에 `Access-Control-Allow-Origin`을 포함하면 브라우저는 해당 출처에서의 요청을 허용합니다.

### 3.2 CORS 문제 해결 방법

Node.js/Express 환경에서는 **CORS 미들웨어**를 사용하여 쉽게 CORS 문제를 해결할 수 있습니다. 이를 통해 서버에서 허용할 출처를 명시하거나 모든 출처에 대해 요청을 허용할 수 있습니다.

---

### 예제: Express에서 CORS 설정

#### Step 1: `cors` 미들웨어 설치

먼저, Express 프로젝트에 `cors` 패키지를 설치해야 합니다.

```bash
npm install cors
```

#### Step 2: 간단한 Express API 서버 작성

다음은 `cors` 미들웨어를 사용하여 CORS 문제를 해결하는 간단한 예제입니다. 이 예제에서는 모든 출처에서의 요청을 허용합니다.

```javascript
const express = require('express');
const cors = require('cors');
const app = express();

// 모든 출처에서의 요청 허용
app.use(cors());

app.get('/api/data', (req, res) => {
  res.json({ message: 'CORS 설정이 완료되었습니다!' });
});

app.listen(3000, () => {
  console.log('서버가 포트 3000에서 실행 중입니다.');
});
```

#### Step 3: 특정 출처만 허용하기

모든 출처에서의 요청을 허용하는 대신, 특정 도메인만 허용하고 싶다면 `cors()` 함수에 옵션을 전달할 수 있습니다.

```javascript
const corsOptions = {
  origin: 'http://localhost:8080', // 허용할 도메인 명시
};

app.use(cors(corsOptions));
```

이 설정은 `http://localhost:8080`에서 오는 요청만 허용하게 됩니다. 다른 도메인에서의 요청은 여전히 차단됩니다.

---

### CORS 동작 과정

1. **클라이언트가 HTTP 요청을 보낼 때**: 브라우저는 요청 헤더에 `Origin` 필드를 포함하여 서버로 전송합니다. 이 필드는 요청이 발생한 출처(도메인)를 나타냅니다.
   
   ```http
   GET /api/data HTTP/1.1
   Host: api.example.com
   Origin: http://localhost:8080
   ```

2. **서버 응답**: 서버는 응답 헤더에 `Access-Control-Allow-Origin`을 포함하여 클라이언트에게 어떤 출처에서의 요청을 허용할지 명시합니다.
   
   ```http
   HTTP/1.1 200 OK
   Access-Control-Allow-Origin: http://localhost:8080
   Content-Type: application/json
   ```

3. **브라우저 검증**: 브라우저는 응답 헤더의 `Access-Control-Allow-Origin` 값을 확인하고, 요청을 보낸 출처(`Origin`)와 일치하는지 비교합니다. 만약 일치한다면 응답 데이터를 사용할 수 있지만, 일치하지 않으면 CORS 에러가 발생하고 응답이 차단됩니다.

---

### 요약

- **CORS**는 브라우저에서 다른 출처로부터 리소스를 요청할 때 발생하는 보안 메커니즘입니다.
- **Node.js/Express**에서는 `cors` 미들웨어를 사용하여 쉽게 CORS 문제를 해결할 수 있습니다.
- 특정 도메인만 허용하거나 모든 도메인에 대해 접근을 허용하는 방식으로 설정할 수 있습니다.  
- 
---

## 4. 실습: Vue.js 애플리케이션과 Node.js/Express API 서버 연동

이번 실습에서는 **Vue.js** 프론트엔드 애플리케이션과 **Node.js/Express** 백엔드 API 서버를 연동하는 방법을 배웁니다. 백엔드에서는 간단한 API를 제공하고, 프론트엔드에서는 Axios를 사용하여 API로부터 데이터를 가져옵니다.

### 4.1 Node.js/Express API 서버 설정

먼저, 간단한 **Node.js/Express** API 서버를 설정하고, 이후 **Vue.js** 애플리케이션에서 이 API를 호출하는 방식으로 진행하겠습니다.

---

### Step 1: Node.js/Express 프로젝트 생성 및 설정

1. **프로젝트 폴더 생성 및 Express 설치**

   먼저, Express 프로젝트를 생성합니다.

   ```bash
   mkdir express-api
   cd express-api
   npm init -y
   npm install express cors
   ```

   - `npm init -y`: 기본 설정으로 `package.json` 파일을 생성합니다.
   - `npm install express cors`: Express와 CORS 미들웨어를 설치합니다.

2. **간단한 Express API 서버 작성**

   프로젝트 디렉토리에 `index.js` 파일을 생성하고 아래 코드를 추가합니다.

   ```javascript
   const express = require('express');
   const cors = require('cors');
   const app = express();

   // CORS 허용 설정 (모든 출처에서의 요청 허용)
   app.use(cors());

   // JSON 데이터 파싱 설정
   app.use(express.json());

   // 간단한 GET API 엔드포인트 생성
   app.get('/api/message', (req, res) => {
     res.json({ message: 'Hello from Express!' });
   });

   // 서버 실행
   app.listen(3000, () => {
     console.log('API 서버가 포트 3000에서 실행 중입니다.');
   });
   ```

3. **서버 실행**

   다음 명령어로 서버를 실행합니다.

   ```bash
   node index.js
   ```

   이제 Express API 서버가 `http://localhost:3000`에서 실행 중입니다. 브라우저에서 `http://localhost:3000/api/message`에 접속하면 다음과 같은 JSON 응답을 확인할 수 있습니다:

   ```json
   {
     "message": "Hello from Express!"
   }
   ```

---

### Step 2: Vue.js 애플리케이션에서 Axios로 API 호출

이제 Vue.js 애플리케이션을 생성하고, Axios를 사용해 위에서 만든 Express API로부터 데이터를 가져옵니다.

1. **Vue 프로젝트 생성**

    Vue CLI가 설치되어 있지 않다면 먼저 설치합니다:

    ```bash
    npm install -g @vue/cli
    ```

    그 후에 Vue 프로젝트를 생성합니다:

    ```bash
    vue create vue-app
    cd vue-app
    ```

2. **Axios 설치**

    Vue 프로젝트 디렉토리에서 Axios를 설치합니다:

    ```bash
    npm install axios
    ```

3. **App.vue 파일 수정**

    `src/App.vue` 파일을 열고 다음과 같이 수정하여 Axios로 API 데이터를 가져오는 기능을 추가합니다:

    ```vue
    <template>
      <div id="app">
        <h1>{{ message }}</h1>
        <button @click="fetchMessage">메시지 가져오기</button>
      </div>
    </template>

    <script>
    import axios from 'axios';

    export default {
      data() {
        return {
          message: '메시지를 가져오세요!'
        };
      },
      
      methods: {
        fetchMessage() {
          axios.get('http://localhost:3000/api/message') // Express API 호출
            .then(response => {
              this.message = response.data.message; // 응답 데이터를 message에 저장
            })
            .catch(error => {
              console.error("API 요청 중 오류 발생:", error);
            });
        }
      }
    };
    </script>

    <style>
    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      text-align: center;
      margin-top: 60px;
    }
    </style>
    ```

4. **Vue 애플리케이션 실행**

    다음 명령어로 Vue 애플리케이션을 실행합니다:

    ```bash
    npm run serve
    ```

5. **브라우저에서 확인**

    이제 브라우저에서 `http://localhost:8080`에 접속하여 "메시지 가져오기" 버튼을 클릭하면, Express 서버로부터 데이터를 받아와 화면에 표시됩니다.

---

### 결과 확인

- **Express 서버**는 `http://localhost:3000/api/message` 경로에서 "Hello from Express!"라는 메시지를 반환하는 간단한 API를 제공합니다.
- **Vue 애플리케이션**은 Axios를 사용하여 이 API에 GET 요청을 보내고, 받은 메시지를 화면에 표시합니다.

---

### 요약

이 실습에서는 다음 작업을 수행했습니다:
1. **Node.js/Express**로 간단한 API 서버를 구축하고 CORS 문제를 해결했습니다.
2. **Vue.js** 프론트엔드 애플리케이션에서 Axios를 사용해 백엔드 API와 통신했습니다.

이 과정은 풀스택 웹 개발의 기본적인 흐름을 이해하는 데 도움이 됩니다. 프론트엔드(Vue)와 백엔드(Express)가 서로 통신하는 구조를 이해하고, CORS 문제 해결 방법도 배웠습니다.