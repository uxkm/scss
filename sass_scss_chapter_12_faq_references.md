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
| 협업 문서화              | `README.md` + Style guide 병행 |

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