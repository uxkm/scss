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