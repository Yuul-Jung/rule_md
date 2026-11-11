# 📘 GitHub 교육용 HTML 제작 표준 v1.0

이 폴더는 **Yuul-Jung GitHub 교육자료의 공통 디자인·탐색·배포 규칙**을 제공합니다. `ai-agent-engineering`의 표지·책장 사진·좌측 통합 목차·장별 이동 방식을 공통 교육형 프로파일로 재사용합니다.

> **표준 규칙 원본:** [STANDARD.md](STANDARD.md)  
> **다른 저장소 적용 방법:** [INTEGRATION.md](INTEGRATION.md)  
> **범용 웹 공통 규칙:** [STANDARD.md 10절](STANDARD.md#10-범용-웹페이지-공통-규칙-기존-yjws-통합)  
> **실제 적용 사례:** [ai-agent-engineering](https://github.com/Yuul-Jung/ai-agent-engineering)

## 1. 파일 구성

| 파일 | 설명 |
|---|---|
| `STANDARD.md` | 시각 규격, 상단 사진, 좌측 탐색, 접근성, 버전 및 검증 규칙 |
| `INTEGRATION.md` | 다른 GitHub 저장소 README / AGENTS.md에서 참조하는 방법 |
| `course.json` | 저장소별 강좌 제목, 장 목록, 파일명, 버전 |
| `build.py` | Markdown 원고를 독립 실행형 HTML로 만드는 생성기 |
| `assets/hero-bookshelf.jpg` | 전체 저장소에서 공통 사용해야 하는 **동일한 상단 사진 원본** |
| `assets/site.css` / `site.js` | 색상, 배치, 장·절 이동, 모바일 메뉴, 코드 복사 |
| `content/ch01.md`, `ch02.md` | 예제 원고 |
| `example-output/` | 생성된 INDEX 및 두 장 예제(참고용) |

## 2. 새로운 교육 저장소에서 적용

가장 단순한 방법은 아래 문장을 해당 저장소의 `README.md`와 `AGENTS.md`에 추가하는 것입니다.

> 이 저장소의 GitHub Pages 교육용 HTML은 [Yuul-Jung 교육용 HTML 표준](https://github.com/Yuul-Jung/rule_md/tree/main/web/education-html)을 따릅니다. `STANDARD.md` 및 `INTEGRATION.md`를 확인하고, 상단 책장 이미지를 동일하게 유지하며 INDEX·장별 탐색·버전 규칙을 적용합니다.

**중요:** 링크만 적어두어도 자동으로 스타일이 적용되는 것은 아닙니다. 제작자가 규칙을 실제로 읽고 템플릿을 복사하거나 생성기를 실행해야 합니다. 오프라인/접근 불가 환경은 `INTEGRATION.md`의 로컬 사본 방식을 이용합니다.

## 3. 실행 예제 (Ubuntu)

```bash
# Python 가상환경 생성: 현재 폴더에 .venv 준비
python3 -m venv .venv

# 가상환경 활성화: 패키지를 프로젝트 안에 분리 설치
source .venv/bin/activate

# Markdown→HTML 변환 도구 설치
python -m pip install mistune

# course.json / content/*.md 편집 후 빌드
python build.py
```

결과는 `dist/index.html`, `dist/chXX_..._vNN.html`에 생성됩니다. 이미지·스타일·스크립트는 생성 HTML에 내장되어 있으므로 같은 폴더에 배치해 GitHub Pages에서 배포할 수 있습니다.

## 4. 기존 표준과의 관계

- 웹페이지 공통 기술·보안·접근성은 [STANDARD.md 10절](STANDARD.md#10-범용-웹페이지-공통-규칙-기존-yjws-통합)에 통합되어 있습니다.
- **교육용 배포 페이지에 한하여** 2열 좌측 목차, 컴팩트 책장 배너, 밝은 테마 기본 고정 등 교육형 외관을 `STANDARD.md`에 따라 적용합니다.
- RTL·C·Python 코드 자체는 [공통 코드 규칙](../../common/code-style-rules.md), FPGA/SoC 교재의 기술 사실은 [분야별 규칙](../../fpga-soc/MBV_SOC_rules.md)이 우선합니다.
- 다른 저장소의 원본이나 정상 기능은 새 표준 적용을 이유로 임의 삭제·재작성하지 않습니다.

## 5. 게시 검증

INDEX와 모든 장 링크, 좌측 탐색, 모바일 화면, 코드 복사, 보안·개인정보 노출을 확인합니다. 실제 브라우저에서 실행하지 않은 내용은 **미검증**으로 표시합니다.

참조 버전: **v1.0 · 2026-11-11**
