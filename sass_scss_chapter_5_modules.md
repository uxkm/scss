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