# ⚙️ VSCode `tasks.json`: .css + .min.css 같은 폴더에 출력하는 구성

SCSS 파일을 컴파일할 때, `.css`와 `.min.css` 파일을 **동일한 디렉토리(dist/ 등)** 에 생성하는 방법입니다. 이 방식은 파일 이름을 명확히 지정해야 하며, 자동 디렉토리 변환(`src:dist`)은 사용할 수 없습니다.

---

## 📁 폴더 구조 목표

```
project/
├── src/
│   ├── style.scss
│   └── layout.scss
├── dist/
│   ├── style.css
│   ├── style.min.css
│   ├── layout.css
│   └── layout.min.css
└── .vscode/
    └── tasks.json
```

---

## ✅ `tasks.json` 예제

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile style.scss (expanded)",
      "type": "shell",
      "command": "sass",
      "args": ["src/style.scss:dist/style.css", "--style=expanded"],
      "group": "build"
    },
    {
      "label": "Compile style.scss (compressed)",
      "type": "shell",
      "command": "sass",
      "args": ["src/style.scss:dist/style.min.css", "--style=compressed"],
      "group": "build"
    },
    {
      "label": "Compile layout.scss (expanded)",
      "type": "shell",
      "command": "sass",
      "args": ["src/layout.scss:dist/layout.css", "--style=expanded"],
      "group": "build"
    },
    {
      "label": "Compile layout.scss (compressed)",
      "type": "shell",
      "command": "sass",
      "args": ["src/layout.scss:dist/layout.min.css", "--style=compressed"],
      "group": "build"
    },
    {
      "label": "Build SCSS All (.css + .min.css)",
      "dependsOn": [
        "Compile style.scss (expanded)",
        "Compile style.scss (compressed)",
        "Compile layout.scss (expanded)",
        "Compile layout.scss (compressed)"
      ],
      "group": {
        "kind": "build",
        "isDefault": true
      }
    }
  ]
}
```

---

## ▶️ 실행 방법

- `Ctrl + Shift + B` → 모든 작업 한 번에 실행
- 또는 `Ctrl + Shift + P` → `Tasks: Run Task` → 개별 빌드 선택

---

## ✅ 장점

- 파일 이름을 명확히 지정할 수 있어 `.min.css` 확장자 유지 가능
- `dist/` 내에서 모든 결과물 관리 → 배포 폴더로 직접 사용 가능
- 실무 빌드/압축 워크플로우에 유리

---

## ⚠️ 주의사항

- 이 방식은 `.scss` 파일이 추가될 때마다 `tasks.json`에 **수동으로 항목 추가**해야 합니다
- 자동 스캔(`src:dist`) 방식은 `.min.css` 확장자 출력을 지원하지 않음

---

## 📦 대체 전략 (Node 스크립트)

파일이 많아질 경우, `node-sass`, `sass`, 또는 `style-dictionary` 등을 활용한 **자동 빌드 스크립트화**를 고려해도 좋습니다.