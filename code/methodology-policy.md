# AI 코딩 방법론 채택 정책

**상태:** ② 추가 규칙 (점진적 개선)  
**최종 업데이트:** 2026-11-16 (4종으로 확장)  
**목적:** Ponytail 외 채택된 방법론의 적용 범위·우선순위·충돌 처리 방식을 정의합니다.

---

## 1. 방법론 채택 현황

### 채택 기준

| 기준 | 설명 |
|------|------|
| Ponytail과 충돌 없음 | 결정 사다리와 직접 모순되지 않을 것 |
| 적용 도메인이 다름 | Ponytail이 다루지 않는 영역을 보완할 것 |
| 공개 출처 명확 | GitHub 공개 저장소에서 직접 확인 가능한 원본이 있을 것 |
| 실용적 단순성 | 규칙 자체가 복잡하지 않을 것 |

---

### 채택된 방법론 (4종)

#### ① Atomic Commits — 원자 단위 커밋
> **출처:** github.com/Baneeishaque/ai-agent-rules (`git-atomic-commit-construction-rules.md`, 공개 저장소, 직접 확인)

**핵심 원칙:**
- 하나의 커밋은 하나의 논리적 목적만 가진다.
- 기능 변경 커밋과 코드 정리(들여쓰기·주석·리팩터링) 커밋을 분리한다.
- 커밋 메시지는 "무엇을"이 아니라 "왜"를 설명한다.
- AI 에이전트가 작성한 커밋은 `Co-Authored-By:` 태그로 표시한다.

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail은 코드 작성 판단에만 적용되며 git 워크플로에는 관여하지 않는다.

---

#### ② Code + Proof — 코드와 검증 증거 동시 제시
> **출처:** Ponytail 원문 Testing 섹션 확장 (`ponytail/AGENTS.md` 직접 보유)

**핵심 원칙:**
- 코드를 제시할 때는 실행 가능한 최소 검증(컴파일 로그·실행 결과·assert)을 함께 제시한다.
- "동작할 것 같습니다"라는 추측 표현은 사용하지 않는다.
- 검증하지 않은 항목은 반드시 `미검증`으로 명시한다.
- 비자명한 로직에만 적용한다. (한 줄짜리 명백한 코드는 검증 불필요)

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail 원문의 "Lazy code without its check is unfinished"를 실무적으로 확장한 것이다.

---

#### ③ Karpathy 4원칙 — Lean + Plan-First
> **출처:** github.com/Yuul-Jung/andrej-karpathy-skills (`CLAUDE.md`, forrestchang/andrej-karpathy-skills 포크, 직접 보유)
> **기반:** Andrej Karpathy의 LLM 코딩 관찰 (2024)

**핵심 원칙:**
1. **Think Before Coding** — 가정을 명시적으로 선언하고, 불명확하면 질문한다.
2. **Simplicity First** — 요청한 것만 구현한다. 추측성 기능·추상화 금지.
3. **Surgical Changes** — 필요한 부분만 변경한다. 무관한 코드에 손대지 않는다.
4. **Goal-Driven Execution** — 다단계 작업 전에 간단한 계획을 제시하고 검증 기준을 먼저 정의한다.

**Ponytail과의 관계:** 🟡 부분 충돌 → Ponytail 우선  
Simplicity First / Think Before Coding / Surgical Changes는 Ponytail과 같은 방향. 단, Goal-Driven Execution의 "Refactor X → Ensure tests pass before and after"는 Ponytail의 "Trivial changes need none"과 충돌. **충돌 시 Ponytail 우선**: trivial 리팩터링에는 테스트 불필요, non-trivial 로직(branch·loop·parser·보안)에만 테스트 적용.

---

#### ④ Anti-Pattern Catalog — 명명된 실패 패턴 목록
> **출처:** github.com/Yuul-Jung/context-engineering (`anti-patterns.md`, travisdrake/context-engineering 포크, CC BY 4.0, 직접 보유)

**핵심 패턴 (11종):**
- The Spot Check (부분 체크 후 완료 선언)
- The Trailing Off (뒤로 갈수록 품질 저하)
- The Silent Deferral (사용자 허락 없이 항목 연기)
- The Courtesy Cut ("간결성을 위해" 임의 생략)
- The Pass-Through (서브에이전트 결과를 검증 없이 전달)
- The Confident Declaration (재독을 테스트로 오인)
- The Parse Check (문법은 맞지만 로직이 틀림)
- The Unchecked Merge (서브에이전트 결과를 검증 없이 병합)
- The Vague Completion (부분 구현 후 완료 표시)
- The Category Skip (일부 카테고리 무시)
- The 7% Read (파일 7%만 읽고 전체를 안다고 판단)

**Ponytail과의 관계:** 🟢 완전 호환  
Anti-Pattern은 "에이전트 프로세스 품질" 레이어, Ponytail은 "코드 최소화 판단" 레이어. 완전히 다른 차원.

---

## 2. Ponytail과 충돌 분석 요약

| 방법론 | 적용 도메인 | Ponytail 도메인 | 충돌 여부 | 처리 방식 |
|--------|------------|----------------|----------|----------|
| Atomic Commits | Git 워크플로 | 코드 작성 판단 | 🟢 없음 | 병렬 적용 |
| Code + Proof | 검증 절차 | 테스트 필요성 판단 | 🟢 없음 | Ponytail 확장 |
| Karpathy 4원칙 | 작업 방식·계획 | 코드 최소화 판단 | 🟡 부분 충돌 | Ponytail 우선 (Goal-Driven Execution 테스트 기준) |
| Anti-Pattern Catalog | 에이전트 프로세스 품질 | 코드 최소화 판단 | 🟢 없음 | 병렬 적용 |

---

## 3. 적용 우선순위

복수 규칙이 동시에 적용될 때의 판단 순서:

```
1순위: ① HTML 학습안내서 STANDARD.md (확정·고정)
2순위: Ponytail 결정 사다리 (이 코드가 필요한가?)
3순위: code-development-rules.md (코드 품질·검증)
  3-1순위: Karpathy 4원칙 (작업 방식, Ponytail과 충돌 시 Ponytail 우선)
4순위: Atomic Commits (커밋 시점)
5순위: Anti-Pattern Catalog (복잡한 작업에서 프로세스 체크)
```

---

## 4. 불채택 사유

| 항목 | 불채택 이유 |
|------|------------|
| Lean Rule Files (ETH Zurich arXiv 2602.11988) | 논문 내용이 "규칙 파일이 성능 향상에 도움이 안 됨"으로 불일치. 별도로 Karpathy 4원칙을 채택 |
| Plan-First (freecodecamp) | 웹 기사로 원문 접근 불가. 별도로 Karpathy Goal-Driven Execution을 채택 |
| Anti-Pattern Cataloguing (thepromptshelf.dev) | 웹 기사로 원문 접근 불가. 별도로 travisdrake/context-engineering을 채택 |
| Spec-Driven Development (전면 적용) | 과도한 사전 설계로 Ponytail 최소화 원칙과 충돌 가능 |
| Context Engineering (전체 도구 체계) | 단일 개발자 환경에 과도함 |
| Multi-agent AGENTS.md 동기화 | 단일 에이전트 환경에 불필요 |

---

## 5. 재검토 주기

- 새로운 에이전트 환경 도입 시
- 반복적인 AI 실수 패턴이 발생할 때마다
- GitHub 공개 저장소에서 원본 확인이 가능한 새 방법론 발견 시

---

> **참고 파일:**
> - Ponytail 전체 규칙: [`../ponytail/AGENTS.md`](../ponytail/AGENTS.md)
> - 코드 개발 규칙: [`code-development-rules.md`](code-development-rules.md)
> - Karpathy 4원칙: [`../karpathy/CLAUDE.md`](../karpathy/CLAUDE.md)
> - Anti-Pattern Catalog: [`../context-engineering/anti-patterns.md`](../context-engineering/anti-patterns.md)
