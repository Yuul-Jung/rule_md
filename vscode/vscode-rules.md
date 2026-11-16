# VS Code 작업 환경 규칙

**적용 대상:** Claude Code, Codex CLI, VS Code 직접 편집  
**상태:** 점진적 개선 (② 추가 규칙)

---

## 1. 작업 시작 전 확인

VS Code에서 코드를 작성하거나 수정하기 전에 다음을 확인합니다:

```
[ ] AGENTS.md를 읽었는가? (저장소 루트)
[ ] 작업 유형에 맞는 규칙 파일을 읽었는가?
     - HTML 학습안내서 → web/education-html/STANDARD.md
     - 소스코드 → code/code-development-rules.md
[ ] 수정 대상 파일의 현재 상태를 확인했는가?
[ ] 변경 범위가 명확한가?
```

---

## 2. 권장 확장 프로그램

### 필수
| 확장 | 용도 |
|------|------|
| `ms-vscode.cpptools` | C/C++ 언어 지원 |
| `ms-python.python` | Python 언어 지원 |
| `ms-python.pylance` | Python 타입 검사·자동완성 |

### FPGA/RTL 작업
| 확장 | 용도 |
|------|------|
| `mshr-h.veriloghdl` | Verilog/SystemVerilog 문법 강조 |
| `teros-technology.teroshdl` | TerosHDL — RTL 문서화·구조도 |

### HTML/웹 작업
| 확장 | 용도 |
|------|------|
| `esbenp.prettier-vscode` | HTML·CSS·JS 서식 정리 |
| `ritwickdey.liveserver` | 로컬 서버 미리보기 |

---

## 3. 작업 디렉터리 규칙

- 저장소 루트를 VS Code 작업 폴더로 열고 하위 폴더를 직접 열지 않습니다.
- `.vscode/settings.json`에 프로젝트 공통 설정을 기록합니다.
- 개인 환경 설정(경로·폰트 등)은 `.vscode/settings.json`에 넣지 않고 사용자 설정에 보관합니다.

### 권장 `.vscode/settings.json` 항목
```json
{
  "editor.tabSize": 4,
  "editor.insertSpaces": true,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true,
  "editor.rulers": [100],
  "[html]": {
    "editor.tabSize": 2
  },
  "[css]": {
    "editor.tabSize": 2
  },
  "[javascript]": {
    "editor.tabSize": 2
  }
}
```

---

## 4. Claude Code / AI 에이전트 사용 규칙

### 작업 범위 지정
- 수정할 파일과 목적을 명확하게 지정합니다.
- "전체 저장소를 개선해 줘"처럼 범위가 넓은 요청은 피합니다.
- 작업을 단계별로 나눠서 요청합니다.

### 확인 순서
```
1. 관련 규칙 파일을 먼저 읽도록 지정합니다.
   예: "AGENTS.md와 code/code-development-rules.md를 읽고 작업하세요."
2. 수정 전 현재 파일 상태를 확인합니다.
3. 변경 사항을 검토한 뒤 커밋합니다.
```

### 금지 사항
```
❌ 규칙 파일 없이 임의로 코드 스타일 변경
❌ 정상 동작하는 기존 파일 전체 재작성
❌ 커밋 전 테스트·검증 생략
❌ HTML 학습안내서 디자인 임의 변경 (STANDARD.md 필수 확인)
```

---

## 5. 파일 저장·커밋 규칙

- 저장 시 후행 공백 제거, 파일 끝 빈 줄 추가를 적용합니다.
- 한 커밋에 하나의 목적만 담습니다.
- 커밋 메시지는 한글로 작성하고 변경 목적을 명시합니다.
  ```
  예: feat: 코드 개발 규칙 파일 추가
      fix: UART 명령 문자열 오류 수정
      docs: HTML 표준 체크리스트 보완
  ```
- 비밀번호·토큰·이메일·로컬 경로·내부 화면 캡처를 커밋에 포함하지 않습니다.

---

## 6. HTML 학습안내서 작업 (VS Code)

HTML 학습안내서를 편집할 때는 반드시 [`../web/education-html/STANDARD.md`](../web/education-html/STANDARD.md)를 먼저 읽습니다.

- Live Server로 실제 화면을 확인합니다 (데스크톱·모바일 폭 모두).
- 코드 복사 버튼·목차 탐색·모바일 메뉴 동작을 직접 테스트합니다.
- 색상·글꼴·레이아웃은 STANDARD.md의 시각 규칙을 따릅니다.
- 디자인을 임의로 변경하지 않습니다.
