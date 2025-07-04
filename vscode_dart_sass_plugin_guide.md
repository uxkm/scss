# 🧩 VSCode Dart Sass Compiler Plugin 사용법 정리

이 플러그인은 **Dart Sass**를 기반으로 SCSS를 자동 컴파일할 수 있는 Visual Studio Code용 확장 도구입니다.

---

## 🔧 설치 방법

### 1. VSCode 내 확장 마켓에서 설치
- 이름: `Dart Sass Compiler`
- 또는 Marketplace 링크: [Dart Sass Compiler - Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=...)

---

## 🚀 기본 사용법

- SCSS 파일 열기 → `Ctrl+Shift+P` → `DartSass: Sass Watch` 명령 실행
- 저장 시 자동 컴파일
- `.css` 또는 `.min.css` 출력 지원

---

## ⚙️ 설정 항목별 상세 설명

| 설정 키 | 설명 |
|--------|------|
| `dartsass.autoPrefixBrowsersList` | autoprefixer에 사용할 브라우저 대상 (예: `['last 2 versions']`) |
| `dartsass.disableAutoPrefixer` | 자동 벤더 접두사 기능 비활성화 (기본: false) |
| `dartsass.disableSourceMap` | `.map` 파일 생성 비활성화 (기본: false) |
| `dartsass.disableCompileOnSave` | 파일 저장 시 자동 컴파일 중지 |
| `dartsass.enableStartWithUnderscores` | `_파일.scss`도 감지 대상으로 포함할지 여부 |
| `dartsass.includePath` | `@use` 경로 기준 설정 |
| `dartsass.nodeExePath` | Node.js 실행 파일 경로 수동 지정 |
| `dartsass.outputFormat` | 출력 형식: `expanded`, `compressed` |
| `dartsass.pauseInterval` | 파일 변경 감지 대기 시간 (ms) |
| `dartsass.sassBinPath` | sass 실행 파일 경로 지정 |
| `dartsass.targetDirectory` | 결과 CSS를 저장할 디렉토리 경로 (상대 or 절대) |

---

## 🧭 메뉴 & 명령어

### 📂 명령 팔레트 (Ctrl+Shift+P)
- `DartSass: Sass Watch` → 변경 감지 시작
- `DartSass: Sass Unwatch` → 감지 중지
- `QuikSass: Compile Current File` → 현재 파일 1회 컴파일
- `QuikSass: Sass Compiler Version` → 사용 중인 Sass 버전 확인
- `QuikSass: View Watcher List` → 현재 감시 중인 파일 목록 보기
- `QuikSass: Clear All Watchers` → 감시 대상 전체 해제

---

## 💻 플랫폼 지원

| 운영체제 | 지원 여부 | 비고 |
|----------|-----------|------|
| Windows  | ✅         | 설치 경로 자동 탐지 |
| Linux    | ✅         | `sass` 경로 직접 지정 가능 |

---

## 🧩 주요 기능

- Dart Sass 기반 컴파일
- AutoPrefixer 지원
- SourceMap 생성/비활성화 선택 가능
- 특정 폴더에 컴파일 결과 저장 가능
- underscore(`_`)로 시작하는 파일 무시 or 포함 선택

---

## ❓ FAQ

| 질문 | 답변 |
|------|------|
| CSS 파일 자동 생성 안 되면? | 파일 저장 이벤트 발생 여부 확인 |
| 결과 폴더를 바꾸고 싶다면? | `dartsass.targetDirectory` 사용 |
| 소스맵 제거 방법? | `dartsass.disableSourceMap: true` 설정 |

---

## 📜 License / ChangeLog / Contributing

- MIT License
- GitHub 저장소 내 `CHANGELOG.md` 참조
- PR 기여 가능

---

## 🙌 Credits

- 플러그인 개발자 및 Dart Sass 공식 팀