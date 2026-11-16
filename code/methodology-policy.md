# AI 코딩 방법론 채택 정책

**상태:** ② 추가 규칙 (점진적 개선)  
**최종 업데이트:** 2026-11-16  
**목적:** Ponytail 외 채택된 GitHub 공개 방법론의 적용 범위·우선순위·충돌 처리 방식을 정의합니다.

---

## 1. 방법론 채택 현황

### 채택 기준

| 기준 | 설명 |
|------|------|
| Ponytail과 충돌 없음 | 결정 사다리 7단계와 직접 모순되지 않을 것 |
| 적용 도메인이 다름 | Ponytail이 다루지 않는 영역을 보완할 것 |
| 공개 출처 명확 | GitHub 공개 저장소 또는 근거 있는 연구 출처 |
| 실용적 단순성 | 규칙 자체가 복잡하지 않을 것 (규칙 파일 최소화 원칙 준수) |

---

### 채택된 방법론 (5종)

#### ① Lean Rule Files — 규칙 파일 최소화
> **출처:** ETH Zurich, arXiv 2602.11988 (2026.09); augmentcode.com; Anthropic Claude Code 공식 권장사항

**핵심 원칙:**
- AGENTS.md / CLAUDE.md는 **200줄 이하**로 유지한다.
- 규칙은 **구체적이고 프로젝트 특화**되어야 한다. "깔끔한 코드를 써라" 같은 일반 문구는 추가하지 않는다.
- 규칙 파일이 커질수록 에이전트가 중요 규칙을 무시할 확률이 높아진다. (ETH Zurich 실험 결과)
- 삭제 테스트: "이 규칙을 지우면 에이전트가 잘못된 행동을 하는가?" → No이면 삭제한다.

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail 자체도 27줄로 최소화된 규칙셋이다. 이 원칙은 rule_md 전체 운영에 적용한다.

---

#### ② Atomic Commits — 원자 단위 커밋
> **출처:** github.com/Baneeishaque/ai-agent-rules (`git-atomic-commit-construction-rules.md`); crystl.dev/library/agent-blocks/rules

**핵심 원칙:**
- 하나의 커밋은 하나의 논리적 목적만 가진다.
- 기능 변경 커밋과 코드 정리(들여쓰기·주석·리팩터링) 커밋을 분리한다.
- 커밋 메시지는 "무엇을"이 아니라 "왜"를 설명한다.
- AI 에이전트가 작성한 커밋은 `Co-Authored-By:` 또는 별도 태그로 표시한다.

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail은 코드 작성 판단에만 적용되며 git 워크플로에는 관여하지 않는다.

---

#### ③ Plan-First for Complex Changes — 복잡 변경 계획 우선
> **출처:** freecodecamp.org/news/how-to-manage-context-files; Anthropic Claude Code plan mode 권장사항; kdnuggets.com 10 Rules

**핵심 원칙:**
- **3개 이상 파일을 변경하는 작업**, 마이그레이션, 인증·보안 변경은 코드 작성 전에 계획을 먼저 작성한다.
- 계획에는 변경 대상 파일, 변경 이유, 예상 영향 범위를 명시한다.
- 한 줄 수정이나 단일 파일 버그 픽스에는 적용하지 않는다.

**Ponytail과의 관계:** 🟡 보완적 (우선순위 주의)  
Ponytail 결정 사다리를 먼저 적용해 "이 변경이 필요한가?"를 확인한 뒤, 필요하다고 판단되면 Plan-First를 적용한다.  
→ **순서: Ponytail 사다리 → Plan-First → 코드 작성**

---

#### ④ Anti-Pattern Cataloguing — 프로젝트 특화 금지 패턴
> **출처:** thepromptshelf.dev/blog/agents-md-best-practices-2026 (Pattern 4); affaan-m/everything-claude-code

**핵심 원칙:**
- 일반 베스트 프랙티스가 아니라 **이 프로젝트에서 AI가 반복적으로 저지르는 실수**를 명시적으로 목록화한다.
- 금지 패턴은 발생 사례가 확인된 뒤에만 추가한다. (예방적 추가 금지)
- `code/code-development-rules.md` 섹션 7의 `Anti-Pattern` 목록이 이 방법론을 구현한다.

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail은 "무엇을 쓰지 말 것인가"의 일반 원칙을 제공하고, Anti-Pattern Cataloguing은 프로젝트 특화 사례를 보완한다.

---

#### ⑤ Code + Proof — 코드와 검증 증거 동시 제시
> **출처:** Ponytail Testing 섹션과 연동; `code/code-development-rules.md` 섹션 5(자동 검증) 기반

**핵심 원칙:**
- 코드를 제시할 때는 실행 가능한 최소 검증(컴파일 로그·실행 결과·assert)을 함께 제시한다.
- "동작할 것 같습니다"라는 추측 표현은 사용하지 않는다.
- 검증하지 않은 항목은 반드시 `미검증`으로 명시한다.
- 비자명한 로직에만 적용한다. (한 줄짜리 명백한 코드는 검증 불필요 — Ponytail 테스트 규칙과 동일)

**Ponytail과의 관계:** 🟢 완전 호환  
Ponytail Testing 섹션("Non-trivial logic gets one small runnable check")을 실무적으로 확장한 것이다.

---

## 2. Ponytail과 충돌 분석 요약

| 방법론 | 적용 도메인 | Ponytail 도메인 | 충돌 여부 | 처리 방식 |
|--------|------------|----------------|----------|----------|
| Lean Rule Files | 규칙 파일 운영 | 코드 작성 판단 | 🟢 없음 | 병렬 적용 |
| Atomic Commits | Git 워크플로 | 코드 작성 판단 | 🟢 없음 | 병렬 적용 |
| Plan-First | 복잡 변경 계획 | 코드 작성 판단 | 🟡 순서 주의 | Ponytail 먼저 → Plan-First |
| Anti-Pattern | 프로젝트 금지 패턴 | 일반 최소화 원칙 | 🟢 없음 | Ponytail 보완 |
| Code + Proof | 검증 절차 | 테스트 필요성 판단 | 🟢 없음 | Ponytail 확장 |

---

## 3. 적용 우선순위

복수 규칙이 동시에 적용될 때의 판단 순서:

```
1순위: ① HTML 학습안내서 STANDARD.md (확정·고정)
2순위: Ponytail 결정 사다리 (이 코드가 필요한가?)
3순위: Plan-First (3파일 이상 변경 시 계획 먼저)
4순위: code-development-rules.md (코드 품질·Anti-Pattern·검증)
5순위: Atomic Commits (커밋 시점)
6순위: Lean Rule Files (규칙 파일 자체 운영 시)
```

---

## 4. 불채택 사유 (검토하고 채택하지 않은 항목)

| 항목 | 불채택 이유 |
|------|------------|
| Spec-Driven Development (전면 적용) | 과도한 사전 설계로 Ponytail 최소화 원칙과 충돌 가능. Plan-First(복잡 변경 한정)로 대체 채택 |
| Context Engineering (전체 도구 체계) | 도구 의존도가 높고 현재 단일 개발자 환경에 과도함. Lean Rule Files로 핵심만 채택 |
| Multi-agent AGENTS.md 동기화 | 현재 환경(단일 에이전트)에 불필요. 멀티 에이전트 환경 전환 시 재검토 |

---

## 5. 재검토 주기

- 새로운 에이전트 환경 도입 시
- 반복적인 AI 실수 패턴이 발생할 때마다 Anti-Pattern 목록 업데이트
- 연 1회 이상 Lean Rule Files 기준으로 전체 rule_md 파일 가지치기

---

> **참고 파일:**
> - Ponytail 전체 규칙: [`../ponytail/AGENTS.md`](../ponytail/AGENTS.md)
> - 코드 개발 규칙 (Anti-Pattern·Code+Proof 구현): [`code-development-rules.md`](code-development-rules.md)
> - VS Code 환경 (Atomic Commits 커밋 메시지 설정): [`../vscode/vscode-rules.md`](../vscode/vscode-rules.md)
