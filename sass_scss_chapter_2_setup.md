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

## 2.6 정리

- SCSS는 Vue, React, Next.js에서 모두 간단한 설치로 적용 가능
- 공통 변수/믹스인은 전역 설정을 통해 프로젝트 전체에 반영 가능
- 모듈화와 전역 스타일 전략을 병행하는 것이 실무에서 가장 유연함

➡️ 다음 장에서는 SCSS 문법의 기본 요소(변수, 중첩, 믹스인 등)를 하나씩 학습합니다.