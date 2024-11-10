## NPM (Node Package Manager)

NPM은 Node.js의 패키지 관리 도구입니다. JavaScript 라이브러리를 쉽게 설치하고 관리할 수 있게 해줍니다.

### NPM이란?

NPM은 Node.js의 기본 패키지 관리자로, 세계 최대의 소프트웨어 레지스트리입니다. JavaScript 개발자들이 코드 패키지를 공유하고 재사용할 수 있게 해줍니다.

### NPM의 주요 구성 요소

1. **웹사이트**: 패키지 검색, 프로필 설정, 기타 NPM 관련 기능을 제공합니다.
2. **명령줄 인터페이스(CLI)**: 터미널에서 NPM을 사용할 수 있게 해주는 도구입니다.
3. **레지스트리**: JavaScript 소프트웨어와 메타 정보를 포함하는 대규모 공개 데이터베이스입니다.

### NPM의 주요 기능

- 코드 패키지를 앱에 적용하거나 통합할 수 있습니다.
- 독립 실행형 도구를 다운로드하여 즉시 사용할 수 있습니다.
- npx를 사용하여 패키지를 설치하지 않고 실행할 수 있습니다.
- 코드를 다른 NPM 사용자와 공유할 수 있습니다.
- 특정 개발자들에게 코드 접근을 제한할 수 있습니다.
- 조직을 만들어 패키지 유지보수, 코딩, 개발자들을 관리할 수 있습니다.

### 패키지 설치 방법

```bash
# 일반 설치
npm install <package>

# 전역 설치
npm install -g <package>

# 특정 버전 설치
npm install <package-name>@<version>
```

### 주요 NPM 명령어

1. `npm init`: 새 NPM 패키지를 초기화합니다.
2. `npm install`: `package.json`에 명시된 모든 의존성을 설치합니다.
3. `npm uninstall <package-name>`: 특정 패키지를 제거합니다.
4. `npm update`: 모든 패키지를 최신 버전으로 업데이트합니다.
5. `npm outdated`: 오래된 패키지 목록을 표시합니다.
6. `npm run <script-name>`: `package.json`에 정의된 스크립트를 실행합니다.

### package.json 파일

`package.json` 파일은 NPM 프로젝트의 핵심으로, 프로젝트의 메타데이터, 의존성, 스크립트 등 중요한 정보를 포함합니다.

### 의존성 관리

NPM은 시맨틱 버저닝(Semantic Versioning)을 사용하여 패키지 버전을 관리합니다. 이를 통해 개발자들은 패키지를 자동으로 업데이트하면서도 원치 않는 주요 변경사항을 피할 수 있습니다.
