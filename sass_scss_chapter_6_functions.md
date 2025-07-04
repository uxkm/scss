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