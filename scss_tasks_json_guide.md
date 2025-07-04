# ⚙️ VSCode `tasks.json`을 이용한 SCSS `.css` + `.min.css` 자동 생성

SCSS 파일을 저장하거나 명령으로 실행할 때, VSCode의 `tasks.json`을 이용하여 **동시에 `.css`와 `.min.css` 파일을 생성**할 수 있습니다.

---

## 📁 파일 위치

`tasks.json`은 다음 위치에 생성됩니다:

```
your-project/
├── src/
│   └── style.scss
├── dist/
│   └── style.css
│   └── style.min.css
└── .vscode/
    └── tasks.json  ✅
```

✅ VSCode 포터블 환경에서도 **`.vscode/tasks.json`** 은 동일하게 작동합니다.

---

## 🧾 tasks.json 예시

```json
{
  "version": "2.0.0",
  "tasks": [
    {
      "label": "Compile SCSS (Expanded)",
      "type": "shell",
      "command": "sass",
      "args": [
        "src/style.scss:dist/style.css",
        "--style=expanded"
      ],
      "group": "build",
      "problemMatcher": []
    },
    {
      "label": "Compile SCSS (Compressed)",
      "type": "shell",
      "command": "sass",
      "args": [
        "src/style.scss:dist/style.min.css",
        "--style=compressed"
      ],
      "group": "build",
      "problemMatcher": []
    },
    {
      "label": "Build SCSS (Both)",
      "dependsOn": [
        "Compile SCSS (Expanded)",
        "Compile SCSS (Compressed)"
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

1. `Ctrl + Shift + P` → `Tasks: Run Task`
2. 또는 `Ctrl + Shift + B` → `Build SCSS (Both)` 실행

---

## 🛠 사전 준비

- Dart Sass 전역 설치 필요:
  ```bash
  npm install -g sass
  ```

- Windows 사용 시 `sass.cmd` 경로 직접 지정 가능:
  ```json
  "command": "C:/Users/yourname/AppData/Roaming/npm/sass.cmd"
  ```

---

## ✅ 요약

| 항목            | 설명 |
|-----------------|------|
| 사용 목적       | `.css`, `.min.css` 동시 생성 |
| 작업 정의 방식  | `.vscode/tasks.json` |
| 실행 방식       | 단축키 또는 명령어 |
| 포터블 지원     | ✅ 경로 구조 동일하게 작동 |