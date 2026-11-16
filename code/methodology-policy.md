# AI 코딩 방법론 채택 정책

**상태:** ② 추가 규칙 (점진적 개선)  
**최종 업데이트:** 2026-11-16  
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

### 채택된 방법론 (2종)

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

## 2. Ponytail과 충돌 분석 요약

| 방법론 | 적용 도메인 | Ponytail 도메인 | 충돌 여부 | 처리 방식 |
|--------|------------|----------------|----------|----------|
| Atomic Commits | Git 워크플로 | 코드 작성 판단 | 🟢 없음 | 병렬 적용 |
| Code + Proof | 검증 절차 | 테스트 필요성 판단 | 🟢 없음 | Ponytail 확장 |

---

## 3. 적용 우선순위

복수 규칙이 동시에 적용될 때의 판단 순서:

```
1순위: ① HTML 학습안내서 STANDARD.md (확정·고정)
2순위: Ponytail 결정 사다리 (이 코드가 필요한가?)
3순위: code-development-rules.md (코드 품질·검증)
4순위: Atomic Commits (커밋 시점)
```

---

## 4. 불채택 사유

| 항목 | 불채택 이유 |
|------|------------|
| Lean Rule Files (ETH Zurich arXiv 2602.11988) | 논문 내용이 "규칙 파일이 성능 향상에 도움이 안 됨"으로 Lean Rule Files 방법론 자체와 불일치. 원본 출처와 내용이 맞지 않아 제외 |
| Plan-First (freecodecamp) | 웹 기사로 원문 접근 불가. 복사 가능한 GitHub 원본 없음 |
| Anti-Pattern Cataloguing (thepromptshelf.dev) | 웹 기사로 원문 접근 불가. 복사 가능한 GitHub 원본 없음 |
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
