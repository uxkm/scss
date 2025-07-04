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