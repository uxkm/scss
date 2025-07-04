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