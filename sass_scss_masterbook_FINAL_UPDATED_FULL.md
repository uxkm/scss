# SASS & SCSS 마스터북 📘

# Chapter 1. SASS와 SCSS의 개요

## 1.1 SASS란 무엇인가?

SASS는 “Syntactically Awesome Style Sheets”의 약자로, CSS를 **더 프로그래밍스럽게 작성할 수 있도록 확장한 전처리기**입니다. SASS는 반복을 줄이고, 코드 재사용성을 높이며, 구조적으로 스타일을 관리할 수 있도록 다양한 기능을 제공합니다.

- **2006년** Hampton Catlin이 고안하고 Natalie Weizenbaum이 개발
- Ruby 언어로 작성되었고, 이후 Dart로 이식됨
- SCSS 문법을 포함하며, 다양한 CSS 확장 문법을 지원함

SASS는 다음과 같은 이유로 널리 사용됩니다:

- 변수, 믹스인, 조건문, 반복문 등을 지원
- 코드 중복 최소화
- 스타일시트 모듈화 가능
- CSS와 완전 호환되는 SCSS 문법

# 📎 부록: 실전 SCSS 코드 베이스 & 설계 전략

이 부록은 책 본문에서 다룬 주요 전략을 실무에서 바로 사용할 수 있도록 코드 샘플, 설계 구조, 자동화 예시 등으로 정리한 참고 자료입니다.

---

## 1. 실전 코드 베이스 구조

```
scss/
├── abstracts/
│   ├── _variables.scss
│   ├── _functions.scss
│   └── _mixins.scss
├── base/
│   ├── _reset.scss
│   └── _typography.scss
├── components/
│   ├── _button.scss
│   ├── _modal.scss
│   └── _card.scss
├── layout/
│   ├── _header.scss
│   └── _footer.scss
├── pages/
│   └── _home.scss
├── themes/
│   ├── _theme-light.scss
│   └── _theme-dark.scss
├── vendors/
│   └── _normalize.scss
└── main.scss
```

---

## 2. SCSS 코드 스타일 가이드

- 변수: `$type-context-property` 예) `$color-primary-background`
- 믹스인: 기능 중심 이름 부여 → `@mixin flex-center`
- 중첩 깊이: 최대 3단계
- 함수명: 동사+명사 조합 → `px-to-rem()`
- 주석: 컴포넌트 시작 시 블럭 주석, 내부는 인라인 주석

```scss
// [Button Component]
.button {
  @include flex-center;
  background: $color-button-bg; // 기본 배경
}
```

---

## 3. Dark Mode: CSS 변수 기반 전략

```scss
:root {
  --color-bg: #ffffff;
  --color-text: #222222;
}

[data-theme="dark"] {
  --color-bg: #111111;
  --color-text: #f4f4f4;
}

body {
  background: var(--color-bg);
  color: var(--color-text);
}
```

> JS에서 `document.documentElement.setAttribute("data-theme", "dark")`로 변경

---

## 4. 디자인 토큰 연동 팁 (Figma → SCSS)

### ✅ 디자인 시스템에서 토큰 추출

예: Figma Style Tokens → JSON 변환

```json
{
  "color": {
    "primary": "#3498db",
    "danger": "#e74c3c"
  },
  "fontSize": {
    "base": "16px",
    "xl": "24px"
  }
}
```

### ✅ SCSS 자동 변환 예시

```scss
$color-primary: #3498db;
$color-danger: #e74c3c;
$font-size-base: 16px;
$font-size-xl: 24px;
```

---

## 5. @use 기반 자동화 예시

```scss
// abstracts/_index.scss
@forward "variables";
@forward "mixins";
@forward "functions";

// main.scss
@use "abstracts" as *;
```

> 컴포넌트별 구조화된 `@use` 사용으로 **전역 오염 없이 모듈 단위 스타일링 가능**

---

✅ 이 부록은 SCSS 프로젝트를 구조화하고 디자인 시스템을 확장하기 위한 기반 지침입니다.

---

## 4-1. 디자인 토큰 변환 자동화 (Style Dictionary 예시)

### 📁 토큰 JSON 예 (tokens/color.json)
```json
{
  "color": {
    "primary": {
      "value": "#3498db"
    },
    "danger": {
      "value": "#e74c3c"
    }
  }
}
```

### ⚙️ 설정 파일 예 (config.json)
```json
{
  "source": ["tokens/**/*.json"],
  "platforms": {
    "scss": {
      "transformGroup": "scss",
      "buildPath": "scss/tokens/",
      "files": [
        {
          "destination": "_tokens.scss",
          "format": "scss/variables"
        }
      ]
    }
  }
}
```

### 🛠 build.js (Node 실행용)
```js
const StyleDictionary = require('style-dictionary').extend('./config.json');
StyleDictionary.buildAllPlatforms();
```

### 💡 실행 방법
```bash
node build.js
```

### 📦 출력 결과 (_tokens.scss)
```scss
$color-primary: #3498db;
$color-danger: #e74c3c;
```

---

## 4-2. GitHub Actions 자동화 예시

```yaml
name: Sync Design Tokens

on:
  push:
    paths:
      - 'tokens/**'

jobs:
  build-tokens:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - uses: actions/setup-node@v3
        with:
          node-version: 18
      - run: npm install
      - run: node build.js
      - run: git add . && git commit -m "Auto-update tokens" && git push
```

---

📌 이렇게 하면 디자이너가 Figma에서 토큰을 수정하고 JSON만 커밋하면, 개발자는 최신 SCSS 토큰을 자동으로 받게 됩니다.
---

## 6. Preprocessor GUI Tool 사용 (VSCode, WebStorm 등)

SCSS는 CLI나 빌드 도구 외에도 GUI 기반으로 컴파일 설정을 구성할 수 있습니다.

### ✅ 6-1. VSCode에서 SCSS 자동 컴파일

**필수 확장 프로그램:**
- [Live Sass Compiler](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass)

**설정 방법:**
1. VSCode에서 `.scss` 파일 열기
2. 하단의 **"Watch Sass"** 버튼 클릭
3. 변경 시마다 `.css` 파일이 자동으로 생성됨

**실행 결과:**
```bash
your-folder/
├── scss/
│   └── style.scss
├── css/
│   └── style.css (자동 생성)
```

**설정 커스터마이징:**
```json
// .vscode/settings.json
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

---

### ✅ 6-2. WebStorm에서 SCSS 자동 컴파일

**설정 방법:**
1. `Preferences > Languages & Frameworks > Stylesheets > SCSS` 메뉴 이동
2. SCSS 파일 디렉토리 지정
3. `File Watchers`에서 SCSS 추가 (자동 실행됨)
4. 저장할 때마다 `.css` 자동 생성

**예시 경로 구조:**
```
project/
├── scss/style.scss
└── style.css (자동 출력)
```

**추가 팁:**
- File Watchers에서 명령어 직접 지정 가능 (`sass --watch`)
- 외부 빌드 도구 없이 SCSS 프로토타이핑 가능

---

📌 이 GUI 기반 설정 방식은 빠르게 결과를 확인해야 하는 퍼블리싱 단계나 디자인 시안 구현 시 특히 유용합니다.