# Chapter 2. 환경 설정 및 도입

## 2.1 SCSS 개발 환경 개요

SASS(SCSS)를 사용하기 위해선 컴파일 환경이 필요합니다. Sass는 CSS로 변환되는 전처리기이기 때문에, 브라우저는 직접 SCSS 파일을 인식하지 못합니다. 이를 위해 **Node.js 기반의 컴파일러**를 사용하거나 **Webpack, Vite, Next.js 등 빌드 도구**와 연동해야 합니다.

---

## 2.2 Vue 프로젝트에서 SCSS 사용하기

### 1단계: Sass 설치

```bash
npm install -D sass
```

### 2단계: SCSS 사용 예시

```vue
<!-- Button.vue -->
<template>
  <button class="btn">Click me</button>
</template>

<style lang="scss" scoped>
$primary: #42b983;

.btn {
  background: $primary;
  color: #fff;
  padding: 1rem;
}
</style>
```

### 3단계: 전역 SCSS 불러오기 (vite.config.ts)

```ts
// vite.config.ts
css: {
  preprocessorOptions: {
    scss: {
      additionalData: `@use "@/styles/_variables.scss" as *;`
    }
  }
}
```

---

## 2.3 React에서 SCSS 사용하기

### 1단계: Sass 설치

```bash
npm install sass
```

### 2단계: SCSS 모듈 적용

```scss
/* Button.scss */
$primary: #61dafb;

.button {
  background-color: $primary;
  border: none;
  padding: 12px 20px;
  color: white;
}
```

```jsx
// Button.jsx
import './Button.scss';

export default function Button() {
  return <button className="button">Click</button>;
}
```

### 3단계: 모듈 방식으로 SCSS 사용

```scss
/* Button.module.scss */
$primary: #61dafb;

.button {
  background: $primary;
}
```

```jsx
import styles from './Button.module.scss';

<button className={styles.button}>Click</button>
```

---

## 2.4 Next.js에서 SCSS 적용

Next.js는 기본적으로 Sass를 지원합니다.

### 1단계: Sass 설치

```bash
npm install sass
```

### 2단계: SCSS 모듈 작성

```scss
// styles/Button.module.scss
$primary: #0070f3;

.button {
  background-color: $primary;
  padding: 10px 16px;
  border-radius: 4px;
}
```

### 3단계: 컴포넌트 연결

```tsx
// components/Button.tsx
import styles from '../styles/Button.module.scss';

export default function Button() {
  return <button className={styles.button}>Next.js Button</button>;
}
```

---

## 2.5 전역 스타일 구조 설계 팁

- `src/styles/` 또는 `src/assets/scss/` 폴더에 공통 SCSS 배치
- `_variables.scss`, `_mixins.scss`, `_reset.scss` 등 partial 파일 구성
- 전역 스타일은 설정 파일에서 자동으로 불러오기 설정 권장 (Vite, Webpack 등에서 `additionalData` 활용)

```ts
additionalData: `@use "@/assets/scss/common/variables" as *;`
```

---



---

## 2.6 SCSS 컴파일 방식: CLI vs GUI

SCSS는 브라우저에서 바로 인식되지 않기 때문에 CSS로 변환(컴파일)해야 하며, 이 과정은 CLI 또는 GUI 방식으로 수행할 수 있습니다.

### ✅ CLI 방식 (명령어 기반)

**설치 예시:**

```bash
npm install -g sass
```

**SCSS → CSS 변환:**

```bash
sass scss/style.scss css/style.css
```

**변경 자동 반영:**

```bash
sass --watch scss:css
```

📌 *CLI 방식은 자동화, 배포, CI/CD와 궁합이 좋습니다.*

---

### ✅ GUI 방식 (Live Compiler 등 시각적 설정)

#### 🔹 VSCode + Live Sass Compiler

1. 확장 마켓에서 `Live Sass Compiler` 설치
2. `.scss` 파일 열고 하단 “Watch Sass” 클릭
3. 자동으로 `css/style.css` 생성

```json
// .vscode/settings.json 예시
{
  "liveSassCompile.settings.formats": [
    { "format": "expanded", "extensionName": ".css", "savePath": "/css" }
  ]
}
```

#### 🔹 WebStorm 설정

- `Preferences > File Watchers > SCSS` 추가
- `sass --watch scss/style.scss style.css` 설정 가능

```bash
project/
├── scss/style.scss
└── style.css (자동 생성)
```

---

| 구분    | CLI                            | GUI                                 |
|---------|--------------------------------|--------------------------------------|
| 난이도  | 명령어 숙지 필요               | 클릭 기반, 쉬움                     |
| 자동화  | 고급 빌드에 최적               | 퍼블리셔, 시안 작업에 적합          |
| 확장성  | Vite, Webpack과 연동 가능       | 실험적 용도, 빠른 결과 확인         |
| 추천    | 개발자, 빌드 파이프라인         | 퍼블리셔, 디자이너, 빠른 개발환경   |

## 2.6 정리

- SCSS는 Vue, React, Next.js에서 모두 간단한 설치로 적용 가능
- 공통 변수/믹스인은 전역 설정을 통해 프로젝트 전체에 반영 가능
- 모듈화와 전역 스타일 전략을 병행하는 것이 실무에서 가장 유연함

➡️ 다음 장에서는 SCSS 문법의 기본 요소(변수, 중첩, 믹스인 등)를 하나씩 학습합니다.