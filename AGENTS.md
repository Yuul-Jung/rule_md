# 🤖 AI 에이전트 필수 확인 지침

이 저장소(`rule_md`)는 Yuul-Jung 프로젝트의 **공통 작업 규칙**을 관리합니다.
코드 작성·HTML 제작·VS Code 작업 전에 **반드시 이 파일을 먼저 확인**하고 해당 규칙을 읽습니다.

---

## 1. 작업 유형별 필수 확인 파일

| 작업 유형 | 반드시 읽을 파일 |
|----------|----------------|
| HTML 학습안내서 제작·수정 | [`web/education-html/STANDARD.md`](web/education-html/STANDARD.md) |
| 소스코드 작성 (C·Verilog·Python·JS) | [`code/code-development-rules.md`](code/code-development-rules.md) |
| AI 코드 작성 판단 (Ponytail) | [`ponytail/AGENTS.md`](ponytail/AGENTS.md) |
| 방법론 채택 정책·충돌 처리 | [`code/methodology-policy.md`](code/methodology-policy.md) |
| AI 코딩 작업 방식 (Karpathy 4원칙) | [`karpathy/CLAUDE.md`](karpathy/CLAUDE.md) |
| 에이전트 실패 패턴 체크 | [`context-engineering/anti-patterns.md`](context-engineering/anti-patterns.md) |
| VS Code 작업 환경 | [`vscode/vscode-rules.md`](vscode/vscode-rules.md) |
| 플로우차트·구조도 제작 | [`common/flowchart-rules.md`](common/flowchart-rules.md) |
| 코드 주석·들여쓰기·코드 박스 | [`common/code-style-rules.md`](common/code-style-rules.md) |
| FPGA/SoC RTL 해설서 | [`fpga-soc/MBV_SOC_rules.md`](fpga-soc/MBV_SOC_rules.md) |

---

## 2. 규칙 운영 원칙

### ① 기본 규칙 (확정 · 고정)
- **HTML 학습안내서**: `web/education-html/STANDARD.md`
- 기존 디자인·화면 구성·학습 절차·코드 표현·배포 형식을 그대로 준수합니다.
- 임의 변경 금지. 새로운 도구·방법이 등장해도 자동으로 변경하지 않습니다.

### ② 추가 규칙 (병렬 적용 · 지속 개선)
- **코드 작성·개발 최적화**: `code/code-development-rules.md`
- **VS Code 작업 환경**: `vscode/vscode-rules.md`
- 충분히 검증된 개선이라도 ①에 자동 편입하지 않습니다.
- ①과 ②가 충돌하면 **①을 우선**합니다.

---

## 3. 작업 전 체크리스트

```
[ ] 작업 유형에 맞는 규칙 파일을 읽었는가?
[ ] HTML 학습안내서 작업이라면 STANDARD.md를 확인했는가?
[ ] Ponytail 사다리: 이 코드가 정말 필요한가? (ponytail/AGENTS.md)
[ ] 가정을 명시적으로 선언했는가? 불확실하면 먼저 질문한다. (Karpathy Think Before Coding)
[ ] 파일을 충분히 읽었는가? 일부만 읽고 전체를 안다고 가정하지 않는다. (Anti-Pattern: The 7% Read)
[ ] 기존 정상 동작 코드를 임의 변경하지 않는가?
[ ] 검증하지 않은 변경은 '미검증'으로 표시할 준비가 됐는가?
[ ] 원격 URL을 읽을 수 없을 때 추정 적용하지 않는가?
[ ] 커밋은 하나의 논리적 목적만 담고 있는가? (Atomic Commits)
```

---

## 4. 저장소 구조

```
rule_md/
├── AGENTS.md                           ← 지금 이 파일 (AI 에이전트 필수 확인)
├── README.md                           ← 사람용 안내
├── common/
│   ├── code-style-rules.md             ← 공통 코드 작성·주석·코드 박스 표준
│   └── flowchart-rules.md              ← 플로우차트·구조도 작성 표준
├── ponytail/
│   └── AGENTS.md                       ← Ponytail 결정 사다리 (MIT, DietrichGebert)
├── code/
│   ├── code-development-rules.md       ← ② AI 코드 개발·최적화·검증 규칙 (Ponytail 포함)
│   └── methodology-policy.md           ← 방법론 채택 정책·충돌 분석·우선순위
├── karpathy/
│   └── CLAUDE.md                       ← Karpathy 4원칙 (Lean + Plan-First, forrestchang 포크)
├── context-engineering/
│   └── anti-patterns.md                ← AI 에이전트 실패 패턴 11종 (travisdrake 포크, CC BY 4.0)
├── vscode/
│   └── vscode-rules.md                 ← VS Code 작업 환경 규칙
├── web/
│   └── education-html/
│       └── STANDARD.md                 ← ① HTML 학습안내서 작성 표준 (확정)
└── fpga-soc/
    └── MBV_SOC_rules.md                ← FPGA/SoC RTL 전용 규칙
```
