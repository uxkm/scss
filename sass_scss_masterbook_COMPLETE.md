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

---

## 1.2 SCSS란 무엇인가?

SCSS는 SASS의 최신 구문으로, **기존 CSS 문법과 호환되도록 설계**되었습니다.  
CSS와 같은 중괄호(`{}`)와 세미콜론(`;`) 문법을 사용하므로 기존 CSS를 그대로 가져와 사용할 수 있습니다.

| 항목      | SASS 문법 예              | SCSS 문법 예              |
|-----------|---------------------------|----------------------------|
| 스타일     | 들여쓰기 기반              | 중괄호 + 세미콜론 사용       |
| 변수       | `$primary: #f00`          | `$primary: #f00;`          |
| 선택자 중첩| `.nav
  ul
    li`      | `.nav { ul { li { ... }}}` |
| 사용성     | 초기 버전                 | 현재 표준 (CSS 친화적)       |

```scss
// SCSS 예시
$primary-color: #3498db;

.button {
  background: $primary-color;
  &:hover {
    background: darken($primary-color, 10%);
  }
}
```

---

## 1.3 왜 SCSS를 사용하는가?

| 기능             | 순수 CSS | SCSS |
|------------------|----------|------|
| 변수             | ❌       | ✅   |
| 조건문/반복문    | ❌       | ✅   |
| 믹스인/상속       | ❌       | ✅   |
| 모듈화 구조       | 제한적   | 강력 |

SCSS는 다음과 같은 이유로 실무에서 필수 도구로 자리잡았습니다.

- 디자인 시스템 구성 시 일관성 유지
- 다크모드, 반응형 등 스타일 분기 처리 용이
- 유지보수, 리팩토링에 유리한 구조화 가능

---

## 1.4 SCSS의 진화

- 2006년: SASS 최초 릴리스 (`.sass` 확장자)
- 2010년: SCSS 구문 도입 (`.scss` 확장자)
- 2020년: `@use`, `@forward` 등 모듈 시스템 도입
- 현재: Dart Sass가 공식 구현체, LibSass는 중단됨

---

## 1.5 어떤 프로젝트에 적합한가?

| 프로젝트 유형         | SCSS 활용 이유 |
|----------------------|----------------|
| 컴포넌트 기반 UI      | 재사용성, 모듈화 |
| 디자인 시스템 구축    | 변수/토큰 관리 |
| 반응형/다크모드 지원 | 조건별 스타일 분기 |
| 대규모 팀 협업        | 7-1 구조, 네임스페이스 |
| 퍼블리싱 & 문서화     | 구조적 스타일 관리 |

---

## 1.6 정리

- SASS는 CSS를 코드로 발전시킨 전처리기이다.
- SCSS는 그 최신 문법이며 CSS와 호환된다.
- 모듈화, 반복 제거, 다크모드 설계 등 실무에서 광범위하게 쓰인다.

➡️ 다음 장에서는 다양한 프레임워크에서 SCSS를 설정하고 통합하는 방법을 다룬다.

---

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

---

# Chapter 3. 기본 문법 완전 정복

이 장에서는 SCSS의 핵심 문법들을 실전 예제와 함께 학습합니다.

---

## 3.1 변수 (Variables)

### ✅ 개념
SCSS에서는 `$` 기호를 사용하여 변수를 정의합니다. 색상, 폰트 크기, 간격 등 자주 쓰이는 값을 저장하고 재사용할 수 있습니다.

### ✅ 예제
```scss
$primary-color: #3498db;
$font-size-base: 16px;

.button {
  background-color: $primary-color;
  font-size: $font-size-base;
}
```

### ❌ 잘못된 예
```scss
.button {
  background-color: #3498db;
}

.alert {
  background-color: #3498db; // 중복 선언
}
```

### 🧠 팁
- 변수 이름에는 의미를 담자: `$text-color-default`, `$spacing-md`
- 테마 색상은 `theme/` 폴더에 따로 관리

---

## 3.2 중첩 (Nesting)

### ✅ 개념
SCSS는 선택자 내부에 선택자를 중첩할 수 있어 구조가 명확합니다.

### ✅ 예제
```scss
.navbar {
  ul {
    list-style: none;

    li {
      display: inline-block;

      a {
        text-decoration: none;
        color: inherit;
      }
    }
  }
}
```

### ❌ 잘못된 예
```scss
.wrapper {
  .container {
    .box {
      .inner {
        .element {
          color: red;
        }
      }
    }
  }
}
```

### 🧠 팁
- 중첩은 3단계 이하로 유지하세요
- BEM 방식과 함께 쓰면 중첩을 줄일 수 있습니다

---

## 3.3 Partials & @use

### ✅ 개념
Partial은 `_`로 시작하는 파일로, SCSS에서 직접 컴파일되지 않습니다. `@use`는 이러한 파일을 로드하는 새로운 방식입니다.

### ✅ 예제
```scss
// _variables.scss
$primary: #e91e63;

// main.scss
@use 'variables' as *;

.btn {
  color: $primary;
}
```

### ✅ 폴더 구조 예시
```
scss/
├── abstracts/
│   └── _variables.scss
└── main.scss
```

---

## 3.4 믹스인 (Mixins)

### ✅ 개념
믹스인은 재사용 가능한 스타일 블록입니다. 함수처럼 호출하며 인자를 받을 수 있습니다.

### ✅ 예제
```scss
@mixin flex-center($gap: 1rem) {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: $gap;
}

.container {
  @include flex-center(2rem);
}
```

---

## 3.5 상속 (Extend)

### ✅ 개념
공통 스타일을 추상 셀렉터(`%`)로 정의한 뒤 다른 클래스가 이를 상속받을 수 있습니다.

### ✅ 예제
```scss
%card-base {
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 0 5px rgba(0,0,0,0.1);
}

.card {
  @extend %card-base;
  background: #fff;
}
```

---

## 3.6 연산

### ✅ 개념
숫자, 단위 간 연산이 가능합니다. `%`, `+`, `-`, `*`, `/` 등의 연산을 지원합니다.

### ✅ 예제
```scss
.container {
  width: 100% - 20px;
  font-size: 14px + 2px; // 16px
}
```

---

## 3.7 주석

### ✅ 예제
```scss
// 이 주석은 컴파일 시 제거됨
/* 이 주석은 CSS에 포함됨 */
```

---

## 3.8 정리

| 기능     | 키워드       | 주요 목적                  |
|----------|--------------|----------------------------|
| 변수     | `$`          | 반복 값 관리               |
| 중첩     | `{}`         | 구조적 스타일링            |
| Partial  | `_filename`  | 파일 분리 및 모듈화        |
| @use     | 모듈 호출    | 변수, 믹스인 명시적 로드   |
| Mixin    | `@mixin`     | 반복 구조화 및 유연성 확보 |
| Extend   | `@extend`    | 공통 스타일 상속           |
| 연산     | `+ - * / %`  | 크기 계산 등               |

➡️ 다음 장에서는 조건문, 반복문 등 **로직 기반 스타일링**을 다룹니다.

---

# Chapter 4. 고급 기능 마스터

이 장에서는 SCSS의 로직 기반 고급 기능들을 다룹니다. SCSS는 단순한 스타일 정의를 넘어, 조건 분기, 반복, 데이터 구조 활용 등을 지원합니다.

---

## 4.1 조건문 (@if, @else, @else if)

### ✅ 개념
조건문은 특정 변수나 조건에 따라 스타일을 다르게 적용할 수 있도록 합니다.

### ✅ 예제
```scss
$theme: dark;

body {
  @if $theme == light {
    background-color: #fff;
    color: #000;
  } @else if $theme == dark {
    background-color: #000;
    color: #fff;
  } @else {
    background-color: gray;
  }
}
```

---

## 4.2 반복문 (@for, @each, @while)

### ✅ @for 문
```scss
@for $i from 1 through 3 {
  .m-#{$i} {
    margin: $i * 4px;
  }
}
```

### ✅ @each 문
```scss
$colors: red, blue, green;

@each $color in $colors {
  .text-#{$color} {
    color: $color;
  }
}
```

### ✅ @while 문
```scss
$i: 1;

@while $i <= 3 {
  .p-#{$i} {
    padding: $i * 2px;
  }
  $i: $i + 1;
}
```

---

## 4.3 리스트와 맵 (List & Map)

### ✅ 리스트 예제
```scss
$spacings: 4px, 8px, 12px;

.card {
  margin-top: nth($spacings, 2); // 8px
}
```

### ✅ 맵 예제
```scss
$theme-colors: (
  primary: #3498db,
  danger: #e74c3c,
  success: #2ecc71
);

.btn-danger {
  background-color: map-get($theme-colors, danger);
}
```

### ✅ 맵 반복
```scss
@each $key, $value in $theme-colors {
  .bg-#{$key} {
    background-color: $value;
  }
}
```

---

## 4.4 오류와 경고

### ✅ @error
```scss
@function divide($a, $b) {
  @if $b == 0 {
    @error "0으로 나눌 수 없습니다.";
  }
  @return $a / $b;
}
```

### ✅ @warn
```scss
$font-size: 30px;

@if $font-size > 20px {
  @warn "폰트가 너무 큽니다.";
}
```

---

## 4.5 실전 예제: 반응형 마진 클래스 자동 생성

```scss
$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px
);

@each $name, $bp in $breakpoints {
  @for $i from 1 through 5 {
    .m-#{$name}-#{$i} {
      @media (min-width: $bp) {
        margin: $i * 4px;
      }
    }
  }
}
```

---

## 4.6 정리

| 기능     | 키워드     | 설명                          |
|----------|------------|-------------------------------|
| 조건문   | `@if`, `@else` | 조건에 따라 스타일 분기         |
| 반복문   | `@for`, `@each`, `@while` | 다수 클래스 자동 생성       |
| 리스트   | `()`       | 순서 있는 값 집합              |
| 맵       | `(key: val)` | 키-값 쌍을 가진 데이터 구조     |
| 오류 처리| `@error`   | 컴파일 중단 및 메시지 출력      |
| 경고     | `@warn`    | 경고 메시지 출력 (컴파일은 계속됨) |

➡️ 다음 장에서는 Sass의 모듈 시스템(@use, @forward)과 @import와의 차이점, Stylus/LESS와의 비교를 학습합니다.

---

# Chapter 5. 모듈 시스템 심화

Sass는 코드의 재사용성과 구조화를 위해 모듈 시스템을 제공합니다. 이 장에서는 `@use`, `@forward`의 구조적 사용법과 `@import`와의 차이, Stylus 및 LESS와의 비교를 다룹니다.

---

## 5.1 @use와 @forward

### ✅ @use
- 다른 SCSS 파일의 변수, 믹스인, 함수 등을 가져옴
- **네임스페이스 기반** → 명시적 접근 필요
- 중복 로딩 방지

```scss
// _variables.scss
$primary: #3498db;

// main.scss
@use 'variables';

.button {
  background-color: variables.$primary;
}
```

### ✅ @use as *
- 네임스페이스 없이 가져오기
```scss
@use 'variables' as *;

.alert {
  color: $primary;
}
```

### ✅ @forward
- 다른 파일로 전달하여 모듈화 레이어 구성

```scss
// abstracts/_index.scss
@forward 'variables';
@forward 'mixins';

// main.scss
@use 'abstracts' as *;
```

---

## 5.2 Sass 1.23 이후 모듈 시스템 변화

| 구분       | @import (구형) | @use/@forward (신형) |
|------------|----------------|----------------------|
| 중복 로딩   | O              | X                    |
| 전역 오염   | O              | X                    |
| 네임스페이스 | X              | O                    |
| 유지보수성  | 낮음           | 높음                 |
| 상태 관리   | 불가           | 모듈 단위 제어 가능   |

### ❌ @import 예제 (지양)
```scss
@import 'variables';
@import 'variables'; // 중복 로드됨
```

### ✅ @use 예제 (권장)
```scss
@use 'variables'; // 1회만 로드, 격리됨
```

---

## 5.3 Stylus 및 LESS와의 비교

| 항목          | SCSS           | LESS        | Stylus        |
|---------------|----------------|-------------|----------------|
| 변수          | `$var`         | `@var`      | `var`          |
| 믹스인         | `@mixin`       | `.mixin()`  | 함수 스타일    |
| 조건문         | `@if`, `@else` | `when`      | `if`           |
| 중첩           | ✅              | ✅           | ✅              |
| 모듈 시스템    | `@use`, `@forward` | 없음        | 없음           |
| CSS와의 호환성 | 매우 높음      | 높음        | 낮음 (자유 문법)|
| 유지보수       | 쉬움           | 보통        | 어려움         |

### SCSS 예
```scss
$color: red;
.button { color: $color; }
```

### LESS 예
```less
@color: red;
.button { color: @color; }
```

### Stylus 예
```stylus
color = red
.button
  color color
```

---

## 5.4 실무 적용 전략

- 추상 레이어(abstracts/)에 `@forward`만 선언된 `_index.scss`를 둔다
- 사용 측에서는 `@use 'abstracts' as *`로 전체 import 가능
- 변수 네임스페이스가 겹치지 않아 팀 간 충돌 방지

---

## 5.5 정리

- `@use`는 명시적인 스타일 구조화를 가능케 함
- `@forward`는 재배포를 위한 모듈 공유 방식
- 기존 `@import` 방식은 중복, 오염 문제로 비권장
- SCSS는 Stylus, LESS 대비 확장성과 호환성에서 가장 강력함

➡️ 다음 장에서는 다양한 **Sass 내장 함수**들을 색상, 숫자, 문자열, 리스트/맵별로 정리합니다.

---

# Chapter 6. 빌트인 함수 총망라

Sass는 다양한 내장 함수를 제공하여 색상, 수치, 문자열, 리스트, 맵 등을 효율적으로 처리할 수 있습니다. 이 장에서는 자주 사용되는 빌트인 함수들을 분류별로 정리하고, 실전 활용 예제와 함께 설명합니다.

---

## 6.1 색상 함수 (Color Functions)

### ✅ 주요 함수

| 함수명         | 설명                                |
|----------------|-------------------------------------|
| `lighten()`    | 색상을 더 밝게 만듬                  |
| `darken()`     | 색상을 더 어둡게 만듬                |
| `mix()`        | 두 색상을 혼합                       |
| `rgba()`       | 투명도 값을 포함한 색상 반환         |
| `adjust-hue()` | 색상(Hue) 조정                      |

### ✅ 예제
```scss
$primary: #3498db;

.btn {
  background: $primary;
  &:hover {
    background: lighten($primary, 10%);
  }
}

.card {
  background: mix(#fff, $primary, 50%);
}
```

### ✅ 다크모드 연계 예제
```scss
$bg-light: #fff;
$bg-dark: #121212;

body {
  background: $bg-light;

  @media (prefers-color-scheme: dark) {
    background: $bg-dark;
  }
}
```

---

## 6.2 숫자/단위 관련 함수

| 함수명         | 설명                                   |
|----------------|----------------------------------------|
| `percentage()` | 소수를 백분율로 변환                   |
| `unit()`       | 값의 단위를 문자열로 반환              |
| `unitless()`   | 값이 단위를 가지고 있는지 여부 반환     |
| `ceil()`       | 올림 처리                              |
| `floor()`      | 내림 처리                              |
| `round()`      | 반올림                                |

### ✅ 예제
```scss
$width: 0.25;
$size: 16px;

.sidebar {
  width: percentage($width); // 25%
  font-size: $size + 4px; // 20px
}

@if unitless(16) {
  @error "단위 없는 값입니다";
}
```

---

## 6.3 문자열 함수

| 함수명     | 설명                             |
|------------|----------------------------------|
| `quote()`  | 문자열을 따옴표로 감쌈            |
| `unquote()`| 따옴표 제거                      |
| `str-length()` | 문자열 길이 반환             |
| `to-upper-case()` | 대문자 변환 (Dart Sass 전용) |
| `to-lower-case()` | 소문자 변환 (Dart Sass 전용) |

### ✅ 예제
```scss
$family: unquote("Helvetica Neue");

body {
  font-family: $family, sans-serif;
}
```

---

## 6.4 리스트 함수

| 함수명     | 설명                         |
|------------|------------------------------|
| `length()` | 리스트 요소 개수 반환         |
| `nth()`    | n번째 값 반환                 |
| `join()`   | 두 리스트 연결                |
| `append()` | 리스트에 값 추가              |

### ✅ 예제
```scss
$gaps: 4px, 8px, 16px;

.grid {
  gap: nth($gaps, 2); // 8px
}
```

---

## 6.5 맵 함수

| 함수명        | 설명                         |
|---------------|------------------------------|
| `map-get()`   | 키에 해당하는 값 반환         |
| `map-merge()` | 맵 결합                       |
| `map-remove()`| 키 제거                       |
| `map-keys()`  | 모든 키 반환                  |

### ✅ 예제
```scss
$theme: (
  primary: #3498db,
  danger: #e74c3c
);

.alert {
  background: map-get($theme, danger);
}
```

---

## 6.6 실무 활용 예시

### ✅ 반응형 폰트 크기 설정
```scss
$breakpoints: (sm: 576px, md: 768px);

@each $key, $bp in $breakpoints {
  .text-#{$key} {
    @media (min-width: $bp) {
      font-size: if($key == sm, 14px, 16px);
    }
  }
}
```

---

## 6.7 정리

- Sass는 단순 변수 이상으로 **로직 중심의 디자인 제어 도구**
- 내장 함수는 **조건 분기, 색상 관리, 리스트 기반 스타일링**을 간편하게 만들어 줌
- `@use`와 함께 활용하면 더욱 강력한 **유틸리티 함수 기반 설계 가능**

➡️ 다음 장에서는 조건/연산 논리를 활용한 계산 및 연산 심화 전략을 다룹니다.

---

# Chapter 7. 계산 및 연산 심화

Sass는 단순 연산뿐만 아니라 조건 기반의 연산 로직, 동적 스타일 계산, 단위 자동 처리 등을 통해 복잡한 스타일을 간결하게 구현할 수 있습니다. 이 장에서는 Sass에서 제공하는 계산 관련 고급 문법을 학습합니다.

---

## 7.1 산술 연산자

| 연산자 | 의미      | 예제            |
|--------|-----------|-----------------|
| `+`    | 덧셈      | `10px + 5px`    |
| `-`    | 뺄셈      | `20px - 4px`    |
| `*`    | 곱셈      | `8px * 2`       |
| `/`    | 나눗셈    | `32px / 2`      |
| `%`    | 나머지    | `13 % 5`        |

### ✅ 예제
```scss
$padding: 12px;
$double-padding: $padding * 2; // 24px
```

> ⚠️ `*`와 `/` 연산은 단위(unit)에 주의하세요. `px / px` = unitless.

---

## 7.2 조건부 계산 (@if + 연산)

```scss
$direction: rtl;

.container {
  padding-#{if($direction == rtl, right, left)}: 1rem;
}
```

- `if()` 함수는 조건식을 삼항 연산자처럼 사용 가능
- `#{}`는 문자열 보간 처리

---

## 7.3 동적 단위 조작

```scss
$value: 10px;

.unitless-value {
  width: if(unitless($value), $value * 1px, $value);
}
```

- `unit()` → 단위 추출 (`px`, `%`, 등)
- `unitless()` → 단위 없음 여부 확인

```scss
@function to-rem($px) {
  @if unit($px) != "px" {
    @error "px 단위만 허용됩니다.";
  }
  @return $px / 16 * 1rem;
}

.title {
  font-size: to-rem(32px); // 2rem
}
```

---

## 7.4 실전 예제: 계산형 유틸리티 클래스 생성

```scss
$scale: 0.25;

@for $i from 1 through 5 {
  .gap-#{$i} {
    gap: $i * $scale * 1rem;
  }
}
```

### ✅ 결과
```css
.gap-1 { gap: 0.25rem; }
.gap-2 { gap: 0.5rem; }
.gap-3 { gap: 0.75rem; }
...
```

---

## 7.5 calc()와 Sass 계산의 차이

- Sass 계산은 **컴파일 타임**에서 실행됨
- CSS `calc()`는 **런타임 브라우저 계산**

### 예시
```scss
$width: 100%;
$gap: 20px;

.container {
  width: calc(#{$width} - #{$gap});
}
```

---

## 7.6 정리

- Sass는 단위/숫자/조건 기반 계산을 강력하게 지원함
- 실시간 변수 계산은 CSS 변수 + `calc()` 병행 활용이 필요
- 유틸리티 기반 프레임워크에서도 Sass 계산은 여전히 유용

➡️ 다음 장에서는 Sass 구조화를 위한 7-1 패턴과 그 실무 설계 방법을 학습합니다.

---

# Chapter 8. 프로젝트 구조화: 7-1 패턴

SCSS는 파일이 많아질수록 유지보수의 어려움이 증가합니다. 이를 해결하기 위한 가장 널리 알려진 구조가 바로 **7-1 패턴**입니다. 이 장에서는 7개의 폴더 + 1개의 main.scss로 구성된 SCSS 폴더 구조의 철학과 실무 적용 전략을 설명합니다.

---

## 8.1 7-1 패턴이란?

“7-1” 패턴은 SCSS 프로젝트를 다음과 같이 **7개의 기능별 디렉토리**와 **1개의 진입점 파일**로 구성하는 설계 구조입니다.

```
scss/
├── abstracts/    // 변수, 믹스인, 함수 등 추상 유틸리티
├── base/         // reset, typography 등 전역 규칙
├── components/   // 버튼, 카드 등 UI 컴포넌트
├── layout/       // header, footer, sidebar 등 구조
├── pages/        // 페이지별 스타일링
├── themes/       // 다크모드, 브랜드 테마
├── vendors/      // 외부 라이브러리 스타일
└── main.scss     // 모든 SCSS 파일의 엔트리
```

---

## 8.2 폴더별 역할 정리

| 폴더명      | 내용 및 사용 예시 |
|-------------|------------------|
| abstracts/  | `_variables.scss`, `_mixins.scss`, `_functions.scss` |
| base/       | `_reset.scss`, `_typography.scss`, `_base.scss` |
| components/ | `_button.scss`, `_card.scss`, `_modal.scss` |
| layout/     | `_header.scss`, `_footer.scss`, `_grid.scss` |
| pages/      | `_home.scss`, `_about.scss` |
| themes/     | `_theme-light.scss`, `_theme-dark.scss` |
| vendors/    | `_normalize.scss`, `_swiper.scss` |
| main.scss   | 위 모든 파일을 `@use`로 불러오는 진입점 |

---

## 8.3 main.scss 구성 예시

```scss
// main.scss
@use 'abstracts' as *;
@use 'base/reset';
@use 'base/typography';
@use 'components/button';
@use 'layout/header';
@use 'pages/home';
@use 'themes/dark';
```

> ✅ 각 폴더 내에는 `_index.scss`를 만들고, 해당 폴더의 모든 SCSS를 `@forward`로 정리하면 깔끔하게 관리할 수 있습니다.

---

## 8.4 실전 전략: 팀 협업을 위한 확장

- 기능 단위로 **폴더 내 하위 폴더 분할** 가능 (`components/form/`, `components/modal/` 등)
- `abstracts/`는 공통 디자인 토큰 저장소로 활용
- `themes/`는 다크모드 전환 및 브랜드별 스타일 분리
- `vendors/`는 외부 스타일 변경 위험을 줄이기 위해 최하위 우선순위 배치

---

## 8.5 7-1 패턴 도입 시 고려할 점

| 항목            | 권장 방식 |
|-----------------|-----------|
| 파일 네이밍      | BEM 방식 + 기능 중심 명명 |
| 전역 변수 호출   | `@use 'abstracts' as *` 활용 |
| 재사용성 높은 구조 | 믹스인, 함수 분리 |
| 유지보수         | index.scss → 모듈 라우팅 |
| 프레임워크 대응   | Vue, React에서도 CSS 모듈 구조와 병행 가능 |

---

## 8.6 구조화와 퍼포먼스

- SCSS 자체는 병합되어 하나의 CSS 파일로 컴파일됨 → 요청 수 증가 없음
- 불필요한 import 최소화가 유지보수성과 속도 양쪽에 유리
- 구조가 잘 잡힌 프로젝트일수록 **온보딩 속도 및 작업 정확도 향상**

---

## 8.7 정리

- 7-1 패턴은 유지보수 가능한 스타일 시스템을 위한 정석 구조
- 각 역할에 맞는 디렉토리 구성과 `@use`, `@forward`로 확장
- 모든 SCSS는 `main.scss`로 통합되어 하나의 CSS로 컴파일됨

➡️ 다음 장에서는 버튼, 그리드, 다크모드 등 실제 프로젝트 예제를 작성합니다.

---

# Chapter 9. 실전 예제와 적용

지금까지 배운 SCSS 기능을 바탕으로, 실제 프로젝트에서 자주 사용되는 UI 패턴을 작성해보겠습니다. 이 장에서는 버튼 컴포넌트, 반응형 그리드 시스템, 다크모드 테마 구현을 중심으로 실전 예제를 구성합니다.

---

## 9.1 버튼 컴포넌트 스타일링

### ✅ SCSS 코드
```scss
$btn-padding: 10px 16px;
$btn-radius: 4px;
$btn-color: #fff;
$btn-colors: (
  primary: #3498db,
  danger: #e74c3c,
  success: #2ecc71
);

@mixin btn-base($color) {
  background-color: $color;
  color: $btn-color;
  padding: $btn-padding;
  border: none;
  border-radius: $btn-radius;
  cursor: pointer;
  transition: 0.2s;

  &:hover {
    background-color: darken($color, 10%);
  }
}

@each $name, $color in $btn-colors {
  .btn-#{$name} {
    @include btn-base($color);
  }
}
```

### ✅ HTML 예시 (React/Vue 동일)
```html
<button class="btn-primary">Primary</button>
<button class="btn-danger">Danger</button>
```

---

## 9.2 반응형 그리드 시스템

### ✅ SCSS 코드
```scss
$columns: 12;

@for $i from 1 through $columns {
  .col-#{$i} {
    width: percentage($i / $columns);
    float: left;
  }
}
```

### ✅ 추가: 행/열 정렬 유틸리티
```scss
.row {
  display: flex;
  flex-wrap: wrap;
  gap: 16px;
}
```

### ✅ HTML 예시
```html
<div class="row">
  <div class="col-4">4칸</div>
  <div class="col-8">8칸</div>
</div>
```

---

## 9.3 다크모드 토글

### ✅ CSS 변수 기반 테마
```scss
:root {
  --bg-color: #fff;
  --text-color: #000;
}

[data-theme="dark"] {
  --bg-color: #121212;
  --text-color: #f5f5f5;
}

body {
  background: var(--bg-color);
  color: var(--text-color);
}
```

### ✅ 자바스크립트 토글 예시
```js
const toggleTheme = () => {
  const current = document.documentElement.getAttribute("data-theme");
  document.documentElement.setAttribute("data-theme", current === "dark" ? "light" : "dark");
};
```

---

## 9.4 반응형 유틸리티 클래스 자동 생성

```scss
$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px
);

@each $name, $width in $breakpoints {
  @for $i from 1 through 5 {
    .p-#{$name}-#{$i} {
      @media (min-width: $width) {
        padding: $i * 4px;
      }
    }
  }
}
```

---

## 9.5 정리

- 실전 컴포넌트 구성은 믹스인 + 반복문을 활용하면 생산성과 일관성이 높음
- 다크모드는 CSS 변수와 JS 토글을 통해 유연하게 구현 가능
- 반응형 유틸리티는 반복문과 맵을 조합하면 자동화 가능

➡️ 다음 장에서는 SASS와 SCSS의 문법적 차이를 심화 비교합니다.

---

# Chapter 10. SASS와 SCSS의 차이점 심화

이 장에서는 SASS와 SCSS의 문법적 차이, 사용성, 역사적 배경을 비교하고 어떤 상황에서 어떤 문법을 선택하는 것이 좋은지에 대해 알아봅니다.

---

## 10.1 문법 차이 요약

| 요소         | SCSS 문법                   | SASS 문법                     |
|--------------|-----------------------------|-------------------------------|
| 기본 구조     | CSS 유사 문법               | 들여쓰기 기반 문법             |
| 중괄호 사용   | 사용 `{}`                   | 미사용 (들여쓰기로 구분)       |
| 세미콜론     | 필요 `;`                    | 불필요                         |
| 확장자       | `.scss`                    | `.sass`                        |
| 가독성       | CSS에 익숙한 사람에게 유리   | Python과 유사                  |

### ✅ SCSS 예시
```scss
$primary: #3498db;

.button {
  background: $primary;
  &:hover {
    background: darken($primary, 10%);
  }
}
```

### ✅ SASS 예시
```sass
$primary: #3498db

.button
  background: $primary
  &:hover
    background: darken($primary, 10%)
```

---

## 10.2 역사 및 도입 배경

- **SASS**: 2006년 출시, Ruby 기반, 들여쓰기 문법 중심
- **SCSS**: 2010년 출시, CSS 호환을 위해 등장, 현재 표준
- 현재 공식 구현은 **Dart Sass**이며, SCSS만을 중심으로 발전 중

---

## 10.3 왜 SCSS가 표준이 되었는가?

| 요소                 | 이유 |
|----------------------|------|
| CSS와의 호환성       | 기존 CSS를 그대로 가져올 수 있음 |
| 도입 진입 장벽 낮음   | CSS와 매우 유사 |
| 도구 호환성           | 모든 CSS 도구에서 거의 그대로 작동 |
| 유지보수 측면         | CSS와 동일한 규칙 기반으로 협업 가능 |

---

## 10.4 언제 SASS를 고려할 수 있는가?

| 조건                                | 설명 |
|-------------------------------------|------|
| 개인 프로젝트 또는 단독 작업        | 들여쓰기 선호 시 가독성 향상 |
| CSS를 거의 사용하지 않는 독립적인 코드베이스 | CSS 혼합 부담 없음 |

---

## 10.5 공식 입장

- [sass-lang.com 공식 문서](https://sass-lang.com)에서는 **SCSS를 기본 예제로 제공**
- Dart Sass는 `.scss` 파일 중심으로 개발되며, `.sass`는 점진적 비권장 문법

---

## 10.6 결론

- **SCSS는 현재 Sass의 주력 문법이며**, 거의 모든 프로젝트에서 사용됨
- `.sass` 문법은 학습이나 실험 목적으로는 의미 있으나 **실무에서는 권장되지 않음**
- 문법 선택은 **프로젝트 규모, 협업 인원, 도구 호환성**을 고려해야 함

➡️ 다음 장에서는 Sass의 한계와 병행 전략, 유지보수 팁을 다룹니다.

---

# Chapter 11. 한계와 보완 전략

SCSS는 강력한 스타일링 전처리기이지만, 모든 상황에 완벽하진 않습니다. 이 장에서는 SCSS의 구조적 한계를 살펴보고, CSS 변수, JS 연동 등과의 병행 전략을 통해 실무에서 어떻게 이를 극복할 수 있는지 제안합니다.

---

## 11.1 SCSS의 주요 한계

### ❌ 런타임 동작 불가

- SCSS는 **컴파일 타임**에 모든 스타일을 결정합니다.
- 브라우저 상에서 조건적으로 값을 바꾸는 **런타임 반응**이 어렵습니다.

> ✅ 해결: CSS 변수(`--var`)와 `calc()`를 병행하여 동적 스타일 구성

---

### ❌ JS 데이터 연동 불가

- JS의 변수나 상태를 SCSS에서 직접 사용할 수 없음
- 반응형 테마, 모드 변경 등에 한계

> ✅ 해결: JS에서 CSS 변수를 변경하거나 HTML 속성(`data-theme`)을 활용

```js
document.documentElement.setAttribute("data-theme", "dark");
```

---

### ❌ 복잡한 중첩과 전역 오염

- 깊은 중첩은 디버깅과 유지보수를 어렵게 만듦
- `@import` 사용 시 변수, 믹스인 전역 오염 문제

> ✅ 해결:
- `@use`로 네임스페이스 관리
- 중첩은 최대 3~4단계로 제한

---

### ❌ 타입 시스템 부재

- 숫자, 색상 등은 타입 검사가 없고 실수 유입 가능

> ✅ 해결:
- `@function` 내부에 `@if unitless()` 등 조건문 적극 활용

```scss
@function px-to-rem($px) {
  @if unit($px) != "px" {
    @error "px 단위만 허용됩니다.";
  }
  @return $px / 16 * 1rem;
}
```

---

## 11.2 CSS 변수와 병행 전략

```scss
:root {
  --gap: 1rem;
}

.container {
  gap: var(--gap);
}
```

> 디자인 토큰을 CSS 변수로 정의하고 SCSS에서는 fallback 또는 로직용으로 활용

---

## 11.3 유지보수 전략

| 전략 항목       | 제안 방식 |
|----------------|-----------|
| 전역 변수 관리 | `abstracts/_variables.scss` 분리 |
| 복잡한 믹스인  | 용도별로 분해 및 주석화 |
| 레거시 @import 제거 | `@use` / `@forward` 구조로 이관 |
| 문서화         | 폴더별 README, 주석, Storybook 등 연동 |

---

## 11.4 SCSS vs CSS-in-JS

| 항목         | SCSS              | CSS-in-JS (예: styled-components) |
|--------------|-------------------|-----------------------------------|
| 런타임 제어   | ❌ 컴파일 시 결정   | ✅ JS 변수, 조건에 따라 실시간 제어 |
| 글로벌 관리   | ✅ 쉬움             | ❌ 어려움 (스코프 좁음)           |
| 성능          | ✅ 빠름            | ⚠️ 컴포넌트 수 많으면 느릴 수 있음 |
| 도입 난이도   | 낮음               | 중간~높음                          |

---

## 11.5 결론

- SCSS는 매우 강력하지만, **JS 반응성이나 타입 안정성**에서는 한계가 있음
- 이를 보완하기 위해 **CSS 변수와 JS 속성 제어**를 병행하는 전략이 필요
- 프로젝트 규모가 커질수록 모듈화, 문서화, 설계 규칙이 중요해짐

➡️ 다음은 마지막 장, 자주 묻는 질문과 참고자료입니다.

---

# Chapter 12. FAQ & 참고자료

이 장에서는 SCSS를 학습하고 사용하는 과정에서 자주 접하는 질문들과, 학습에 도움이 되는 참고 자료들을 정리합니다.

---

## 12.1 자주 묻는 질문 (FAQ)

### ❓ SCSS와 CSS는 함께 쓸 수 있나요?
✅ 예. SCSS는 CSS로 컴파일되기 때문에 기존 CSS와 함께 사용해도 무방합니다.

### ❓ SCSS 파일을 브라우저에서 직접 불러올 수 있나요?
❌ 아닙니다. SCSS는 브라우저가 인식하지 못하므로, 반드시 CSS로 컴파일된 후 사용해야 합니다.

### ❓ SCSS 변수는 JS에서 읽을 수 있나요?
❌ 직접 읽을 수는 없습니다. 다만, CSS 변수(`--var`)를 SCSS에서 병행하여 선언하고 JS에서 제어할 수 있습니다.

### ❓ @import는 정말 사용하지 말아야 하나요?
🟡 점진적 폐지 예정이며, Dart Sass에서는 `@use` 및 `@forward`로 전환할 것을 권장합니다.

### ❓ CSS-in-JS보다 SCSS가 좋은가요?
⚖️ 각각 장단점이 있으며, 프로젝트 성격과 팀 구조에 따라 결정합니다. SCSS는 디자인 토큰과 유틸리티 구성에, CSS-in-JS는 상태 기반 동적 스타일에 적합합니다.

### ❓ SCSS에서 다크모드 구현은 어떻게 하나요?
✅ HTML에 `data-theme` 속성을 설정하고, SCSS에서 해당 속성에 따라 CSS 변수를 바꾸는 방식으로 구현합니다.

---

## 12.2 실무 팁 요약

| 항목                     | 권장 전략 |
|--------------------------|-----------|
| 다크모드 테마            | CSS 변수 + `data-theme` |
| 전역 스타일 설정         | Vite/Webpack에서 `additionalData` 사용 |
| 스타일 네이밍            | BEM 또는 컴포넌트 기반 구조 |
| 모듈 구성                | 7-1 패턴 기반 폴더 관리 |
| 외부 스타일 통합         | `vendors/` 폴더 분리 관리 |
| 믹스인/함수 관리         | `abstracts/` 폴더 내 `_mixins.scss`, `_functions.scss` |
| 협업 문서화              | README.md + Style guide 병행 |

---

## 12.3 참고 자료

### 📚 공식 문서
- Sass 공식 홈페이지: https://sass-lang.com
- Dart Sass GitHub: https://github.com/sass/dart-sass

### 🛠 실무 가이드
- 7-1 패턴 설계: https://gist.github.com/rveitch/84cea9650092119527bc
- CSS Tricks의 Sass 가이드: https://css-tricks.com/sass-techniques/

### 🎓 강의 및 튜토리얼
- MDN Sass 소개: https://developer.mozilla.org/en-US/docs/Web/CSS/Sass
- Frontend Masters Sass 강의
- Udemy / YouTube의 무료 SCSS 강좌

---

## 12.4 정리

이 책의 내용을 기반으로 SCSS의 구조적 설계, 유틸리티 생성, 조건 제어, 테마 관리 등을 자유롭게 구현할 수 있게 되었을 것입니다.  
이제 프로젝트의 복잡도에 따라 SCSS를 유연하게 활용하며 유지보수성과 확장성을 확보해보세요.

🎉 감사합니다. — Happy Styling!

---