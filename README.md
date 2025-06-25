# 🔥 Firebase MCP Demo

Firebase MCP (Model Context Protocol) 연동을 통한 Firestore 데이터베이스 CRUD 웹 애플리케이션

## 📋 프로젝트 개요

이 프로젝트는 Firebase MCP를 사용하여 Firestore 데이터베이스와 상호작용하는 웹 애플리케이션입니다. 실시간 데이터 추가, 조회, 개별 삭제 기능을 제공합니다.

## 🚀 배포된 사이트

**라이브 데모**: https://mcp-demo-2024.web.app

## ✨ 주요 기능

- ✅ **실시간 데이터 추가**: 입력 즉시 화면에 표시
- ✅ **데이터 조회**: Firestore에서 실시간 데이터 로드
- ✅ **개별 삭제**: 각 항목별 선택적 삭제 기능
- ✅ **전체 삭제**: 모든 데이터 일괄 삭제
- ✅ **반응형 디자인**: 모바일/데스크톱 지원
- ✅ **에러 처리**: 사용자 친화적인 상태 메시지

## 🛠️ 기술 스택

- **Frontend**: HTML5, CSS3, JavaScript (ES6+)
- **Backend**: Firebase Firestore
- **Hosting**: Firebase Hosting
- **Tools**: Firebase CLI, MCP Tools

## 📁 프로젝트 구조

```
vibe_firebase/
├── public/                 # Firebase Hosting 배포 폴더
│   └── index.html         # 프로덕션용 HTML (자동 설정)
├── .firebase/             # Firebase 캐시
├── env.example            # 환경변수 예시 파일
├── firebase.json          # Firebase 설정
├── firestore.rules        # Firestore 보안 규칙
├── firestore.indexes.json # Firestore 인덱스 설정
├── index.html             # 개발용 HTML (하드코딩 설정)
├── index-hosting.html     # Hosting용 HTML 소스
└── README.md
```

## 🔧 설치 및 실행

### 1. 프로젝트 클론

```bash
git clone https://github.com/YOUR_USERNAME/vibe_firebase.git
cd vibe_firebase
```

### 2. Firebase CLI 설치

```bash
npm install -g firebase-tools
```

### 3. Firebase 로그인

```bash
firebase login
```

### 4. 로컬 개발 서버 실행

```bash
# 로컬에서 개발용 HTML 파일 열기
start index.html

# 또는 Firebase 로컬 서버 실행
firebase serve
```

### 5. 배포

```bash
firebase deploy
```

## 🔐 환경 설정

### 개발 환경

`index.html` 파일에서 Firebase 설정이 하드코딩되어 있습니다. 실제 프로덕션에서는 다음 방법들 중 하나를 사용하세요:

### 1. Firebase Hosting (추천)

Firebase Hosting을 사용하면 자동으로 설정이 주입됩니다:

```javascript
// 자동 설정 가져오기
const response = await fetch('/__/firebase/init.json');
const firebaseConfig = await response.json();
```

### 2. 환경변수 사용

`.env` 파일을 생성하고 `env.example`을 참고해서 설정:

```bash
cp env.example .env
# .env 파일을 편집해서 실제 값 입력
```

## 🔒 보안 규칙

현재 Firestore는 **테스트 모드**로 설정되어 있습니다 (2025년 7월 25일까지):

```javascript
// firestore.rules
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /{document=**} {
      allow read, write: if request.time < timestamp.date(2025, 7, 25);
    }
  }
}
```

⚠️ **프로덕션에서는 적절한 보안 규칙을 설정하세요!**

## 🎯 주요 구현 사항

### Firebase MCP 연동

이 프로젝트는 Firebase MCP (Model Context Protocol)를 사용하여:

- Firebase 프로젝트 자동 생성
- Firestore 데이터베이스 초기화
- 웹앱 등록 및 설정
- 호스팅 배포 자동화

### 실시간 UI 업데이트

```javascript
// 데이터 추가 시 즉시 UI 업데이트
const docRef = await addDoc(collection(db, 'messages'), newData);
addDataToUI(docRef.id, newData); // 페이지 새로고침 없이 즉시 표시
```

### 개별 삭제 기능

```javascript
// 각 아이템마다 삭제 버튼 생성
<button class="delete-btn" onclick="deleteItem('${docId}')">삭제</button>
```

## 🐛 디버깅

브라우저 개발자 도구(F12)의 Console 탭에서 다음 로그들을 확인할 수 있습니다:

- `addData 함수 호출됨`
- `입력값: [name] [message]`
- `addDataToUI 호출됨: [docId] [data]`

## 📝 개발 히스토리

1. **Firebase 프로젝트 생성**: `mcp-demo-2024`
2. **Firestore 데이터베이스 설정**: 테스트 모드로 초기화
3. **웹앱 개발**: CRUD 기능 구현
4. **UI/UX 개선**: 실시간 업데이트, 개별 삭제 기능
5. **호스팅 배포**: Firebase Hosting으로 배포
6. **보안 강화**: 환경변수 및 자동 설정 구현

## 🔮 향후 계획

- [ ] 사용자 인증 (Firebase Auth) 추가
- [ ] 실시간 리스너로 다중 사용자 지원
- [ ] 데이터 검색 및 필터링 기능
- [ ] 파일 업로드 (Firebase Storage) 연동
- [ ] PWA (Progressive Web App) 기능 추가

## 🤝 기여하기

1. 이 리포지토리를 Fork 하세요
2. 새로운 브랜치를 만드세요 (`git checkout -b feature/amazing-feature`)
3. 변경사항을 커밋하세요 (`git commit -m 'Add some amazing feature'`)
4. 브랜치에 푸시하세요 (`git push origin feature/amazing-feature`)
5. Pull Request를 열어주세요

## 📄 라이선스

이 프로젝트는 MIT 라이선스 하에 있습니다.

## 👨‍💻 개발자

- **개발**: Claude (AI Assistant) & danmu
- **Firebase MCP**: Firebase Tools Team
- **호스팅**: Firebase Hosting

---

⭐ 이 프로젝트가 도움이 되셨다면 스타를 눌러주세요! 