# 🥊 Dart Sass Compiler vs Live Sass Compiler (VSCode 확장 비교)

Sass/SCSS 파일을 컴파일할 때 VSCode에서 가장 많이 쓰이는 두 가지 확장 프로그램의 기능을 비교합니다.

---

## 📋 주요 비교표

| 항목                         | Dart Sass Compiler (🔧)                                 | Live Sass Compiler (🧩)                                       |
|------------------------------|--------------------------------------------------------|---------------------------------------------------------------|
| **기반 엔진**               | 공식 Dart Sass (`sass` CLI 기반)                      | Node Sass (구버전 LibSass 기반)                              |
| **출력 방식**               | `.scss → .css` (확장된 설정 지원)                    | `.scss → .css` or `.min.css`                                  |
| **설치 경로 지정**         | Node.js 및 Sass 실행 파일 경로 설정 가능              | 불필요 (내부에 Sass 포함)                                     |
| **브라우저 접두사 자동화** | Autoprefixer + 설정 가능 (`dartsass.autoPrefixBrowsersList`) | 자동 적용되나 설정 불가능                                     |
| **Source Map 설정**        | `disableSourceMap` 가능                                | `.map` 항상 생성됨                                            |
| **파일 감지**              | `.scss`, `_*.scss` 포함 여부 설정 가능                | `_` 파일 자동 무시                                            |
| **출력 포맷**              | `expanded`, `compressed` 명시 가능                    | 기본 압축(`compressed`) / 비압축(`expanded`) 선택 가능        |
| **대상 폴더 지정**         | `targetDirectory`로 출력 CSS 경로 설정                | 항상 `.css/` 폴더에 저장됨 (`scss/` 기준 상대 경로로 생성)   |
| **명령어 제어**            | `DartSass: Watch`, `Unwatch`, `Compile`, `Version` 등 | `Watch Sass`, `Stop Watching Sass` 등 간단한 명령 제공       |
| **성능**                   | 빠름 (Dart Sass 최신 성능 유지)                       | 빠르지만 LibSass 구버전으로 제한                              |
| **확장성**                 | 고급 설정 많고 CI/CD에 적합                           | 빠른 시안 및 퍼블리셔에게 적합                                 |
| **개발 지속성**           | Dart Sass 기반으로 Sass 공식 지원                     | LibSass는 더 이상 유지보수되지 않음 (2020년 공식 종료)       |
| **실무 적용 추천**         | ✅ 실개발 프로젝트, 협업, 빌드 통합                    | ⚠️ 프로토타입, 개인 퍼블리싱 시안                             |
| **GitHub/CI 통합**         | 가능 (설정 공유, Watch 자동화 가능)                   | 제한적 (로컬 GUI 동작 위주)                                   |

---

## 💻 설정 예시

### Dart Sass Compiler

📄 `.vscode/settings.json`
```json
{
  "dartsass.targetDirectory": "./public/css",
  "dartsass.outputFormat": "compressed",
  "dartsass.disableSourceMap": true,
  "dartsass.autoPrefixBrowsersList": ["last 2 versions", "> 1%"]
}
```

📁 폴더 구조
```
project/
├── scss/
│   └── main.scss
├── public/
│   └── css/
│       └── main.css
```

---

### Live Sass Compiler

📄 `.vscode/settings.json`
```json
{
  "liveSassCompile.settings.formats": [
    {
      "format": "expanded",
      "extensionName": ".css",
      "savePath": "/css"
    }
  ]
}
```

📁 폴더 구조
```
project/
├── scss/
│   └── style.scss
├── css/
│   └── style.css
```

---

## ✅ 결론 요약

| 사용자 유형         | 추천 컴파일러         | 이유 |
|--------------------|------------------------|------|
| 퍼블리셔, 디자이너  | **Live Sass Compiler** | 빠르고 간단함. 저장만으로 결과 확인 가능 |
| 프론트엔드 개발자   | **Dart Sass Compiler** | 최신 엔진 기반, 고급 설정 가능, 유지보수됨     |
| 협업 팀, CI 사용팀  | **Dart Sass Compiler** | 설정 공유, 폴더 구조 분리, Git 연동에 유리     |