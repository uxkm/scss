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