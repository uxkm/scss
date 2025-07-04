# 🧩 VSCode에서 SCSS 컴파일 완전 가이드

Visual Studio Code에서 SCSS를 자동으로 컴파일하는 방법에 대해 다음 3가지를 중심으로 정리합니다:

1. **Dart Sass Compiler 플러그인 사용법**
2. **Live Sass Compiler 플러그인과의 비교**
3. **tasks.json을 활용한 .css + .min.css 동시 생성**

---

## 1️⃣ Dart Sass Compiler (VSCode 확장)

이 플러그인은 **Dart Sass**를 기반으로 SCSS를 자동 컴파일할 수 있는 VSCode 확장 도구입니다.

### 🔧 설치 방법
- 이름: `Dart Sass Compiler`
- 설치: VSCode 확장 마켓에서 설치

### 🚀 사용 방법
- `.scss` 파일 열기 → `Ctrl+Shift+P` → `DartSass: Sass Watch` 실행
- 저장 시 자동 컴파일
- `.css` 또는 `.min.css` 출력 지원

### ⚙️ 주요 설정

| 설정 키 | 설명 |
|--------|------|
| `dartsass.autoPrefixBrowsersList` | Autoprefixer 브라우저 대상 설정 |
| `dartsass.disableAutoPrefixer` | 접두사 비활성화 여부 |
| `dartsass.disableSourceMap` | `.map` 생성 여부 |
| `dartsass.outputFormat` | CSS 출력 형식 (`expanded`, `compressed`) |
| `dartsass.targetDirectory` | 결과 CSS 저장 경로 |
| 기타 설정 | includePath, nodeExePath, sassBinPath 등 다양함 |

### 🧭 명령어 예시
- `DartSass: Sass Watch` / `Unwatch`
- `QuikSass: Compile Current File`
- `QuikSass: Clear All Watchers`

---

## 2️⃣ Dart Sass vs Live Sass Compiler 비교

| 항목                         | Dart Sass Compiler (🔧)                                 | Live Sass Compiler (🧩)                                       |
|------------------------------|--------------------------------------------------------|---------------------------------------------------------------|
| **기반 엔진**               | Dart Sass (공식)                                      | Node Sass (LibSass 기반)                                     |
| **설정 유연성**             | 매우 높음 (고급 옵션 지원)                            | 낮음 (간단한 사용에 적합)                                     |
| **출력 포맷 제어**          | `expanded` / `compressed` 가능                         | `.css` / `.min.css` 설정 가능                                 |
| **출력 위치 설정**          | 자유롭게 가능 (`targetDirectory`)                     | 항상 `./css/` 하위에 저장됨                                   |
| **유지보수 상태**           | ✅ 최신 지원 중                                        | ❌ LibSass 중단됨 (2020)                                       |
| **추천 대상**               | 개발자, 팀 프로젝트, CI/CD                            | 퍼블리셔, 빠른 시안 확인용                                    |

📌 결론:  
- 퍼블리싱이나 개인 프로젝트 → Live Sass Compiler  
- 협업/빌드 통합/대규모 프로젝트 → Dart Sass Compiler

---

## 3️⃣ `.css` + `.min.css` 동시 생성 (tasks.json)

### 📁 파일 구조 예시

```
your-project/
├── src/
│   └── style.scss
├── dist/
│   └── style.css
│   └── style.min.css
└── .vscode/
    └── tasks.json  ✅
```

### 🧾 tasks.json 내용

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile SCSS (Expanded)",
      "type": "shell",
      "command": "sass",
      "args": ["src/style.scss:dist/style.css", "--style=expanded"],
      "group": "build",
      "problemMatcher": []
    },
    {
      "label": "Compile SCSS (Compressed)",
      "type": "shell",
      "command": "sass",
      "args": ["src/style.scss:dist/style.min.css", "--style=compressed"],
      "group": "build",
      "problemMatcher": []
    },
    {
      "label": "Build SCSS (Both)",
      "dependsOn": ["Compile SCSS (Expanded)", "Compile SCSS (Compressed)"],
      "group": { "kind": "build", "isDefault": true }
    }
  ]
}
```

### ▶️ 실행 방법
- `Ctrl + Shift + B` → 기본 빌드 실행
- 또는 `Tasks: Run Task` → 원하는 작업 선택

### 💡 포터블 VSCode도 완벽 지원
- `.vscode/tasks.json` 구조만 지키면 동일하게 작동

---

## ✅ 요약

| 목적 | 도구 | 방식 |
|------|------|------|
| 빠른 테스트, 퍼블리싱 | Live Sass Compiler | GUI 기반, 간단 설정 |
| 빌드 자동화, 확장성 | Dart Sass Compiler | 고급 설정 가능, 최신 Sass 지원 |
| 결과물 분리 출력 | tasks.json | `.css`, `.min.css` 동시 생성 |