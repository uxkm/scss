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