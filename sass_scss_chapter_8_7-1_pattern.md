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