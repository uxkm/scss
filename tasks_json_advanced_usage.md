# ⚙️ VSCode `tasks.json` 고급 사용법: SCSS `.css` + `.min.css` 자동화 & Watch

이 문서는 VSCode에서 SCSS 파일을 컴파일할 때 `.css` + `.min.css`를 동시 생성하고, **여러 파일 처리**, **Watch 모드**, **디렉토리 전체 변환** 등 실무 확장을 위한 `tasks.json` 활용 방법을 정리합니다.

---

## 📁 기본 구조: tasks.json 위치

```
project/
├── src/
│   ├── style.scss
│   └── layout.scss
├── dist/
│   └── style.css
│   └── layout.css
├── dist-min/
│   └── style.css (압축)
│   └── layout.css (압축)
└── .vscode/
    └── tasks.json
```

---

## ✅ 1. 기본 + 압축 `.css` 동시 생성

```json
{
  "label": "Build SCSS (Both)",
  "dependsOn": ["Compile SCSS (Expanded)", "Compile SCSS (Compressed)"],
  "group": { "kind": "build", "isDefault": true }
}
```

- 각각의 작업을 순차 실행하여 `.css`, `.min.css` 출력

---

## ✅ 2. 여러 SCSS → 전체 CSS 자동 컴파일

```json
{
  "label": "Sass Build Expanded",
  "type": "shell",
  "command": "sass",
  "args": ["src:dist", "--style=expanded"],
  "group": "build"
},
{
  "label": "Sass Build Compressed",
  "type": "shell",
  "command": "sass",
  "args": ["src:dist-min", "--style=compressed"],
  "group": "build"
}
```

- `src` 폴더 내 모든 `.scss` 파일 → `dist` 및 `dist-min`에 각각 컴파일

---

## ✅ 3. Watch 모드: 변경 자동 감지

```json
{
  "label": "Sass Watch",
  "type": "shell",
  "command": "sass",
  "args": ["--watch", "src:dist"],
  "isBackground": true,
  "problemMatcher": []
}
```

- 실시간 자동 컴파일이 필요한 로컬 개발에 적합
- `Ctrl + Shift + P` → `Run Task` → `Sass Watch` 실행

---

## 🧠 실무 추천 전략

| 목적                        | 설정 방식 |
|-----------------------------|-----------|
| `.css` + `.min.css`         | `dependsOn` 빌드 구성 |
| 전체 폴더 변환             | `src:dist` 단축 경로 사용 |
| 실시간 감시 + 자동 변환     | `"--watch"` + `"isBackground": true` |
| 퍼블리셔 or 프론트엔드 협업 | 압축 포맷 별도 저장(`dist-min/`) |
| CI/CD 대응                 | `sass:build` npm 스크립트 + 이 task 병행 |

---

## 💡 사전 준비

```bash
npm install -g sass
```

> ⚠️ Windows의 경우 `sass.cmd` 경로를 `"command"`에 직접 지정 가능

---

## ▶️ 실행 요약

| 명령어             | 설명 |
|--------------------|------|
| `Ctrl + Shift + B` | 기본 빌드: `.css` + `.min.css` |
| `Run Task` 메뉴    | Watch / Build 선택 실행 |
| `Ctrl + C`         | Watch 종료 (터미널에서) |