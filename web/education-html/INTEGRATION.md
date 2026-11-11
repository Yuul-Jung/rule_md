# 다른 GitHub 저장소에서 교육용 HTML 공통 규칙 참조하기

## 1. 중앙 표준의 위치

- 규칙 폴더: https://github.com/Yuul-Jung/rule_md/tree/main/web/education-html
- 표준 원문: https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/STANDARD.md
- 생성 도구: https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/build.py
- 실제 적용 예: https://github.com/Yuul-Jung/ai-agent-engineering

## 2. 기존 저장소 README.md에 삽입할 문구

```markdown
## 📘 교육용 HTML 공통 제작 규칙

이 저장소의 교육자료(웹페이지·강의 HTML)는 [Yuul-Jung 교육용 HTML 공통 표준](https://github.com/Yuul-Jung/rule_md/tree/main/web/education-html)을 적용합니다.

- [제작 규칙](https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/STANDARD.md)
- [다른 저장소 적용 안내](https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/INTEGRATION.md)
- [기준 디자인 사례](https://github.com/Yuul-Jung/ai-agent-engineering)

공통 책장 이미지, 컴팩트한 상단 배너, 좌측 전체 장/절 탐색, 모바일 메뉴, 파일 버전 및 검증 기준을 따릅니다.
```

## 3. AI 코딩 에이전트가 작업할 때: AGENTS.md 예시

저장소 루트에 `AGENTS.md`를 두고 다음 지침을 입력합니다.

```markdown
# GitHub 교육용 HTML 작성 규칙

이 저장소에서 새 HTML 교재를 만들거나 기존 교재를 수정할 때는 먼저 다음 문서를 확인한다.
- https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/STANDARD.md
- https://github.com/Yuul-Jung/rule_md/blob/main/web/education-html/INTEGRATION.md

적용 사항:
1. 책장 배너 이미지는 중앙 표준의 hero-bookshelf.jpg와 동일하게 유지한다.
2. 좌측 전체 장 목차와 현재 페이지 절 목차 및 모바일 메뉴를 구현한다.
3. 기존 학습 내용·코드·이미지는 보존하고, 차이가 있는 부분만 수정한다.
4. 수정 시 장별 파일명을 _v01 → _v02로 올리고 이전 생성본은 결과 폴더에서 정리한다.
5. 코드 문법, 내부 링크, 개인정보, 접근성과 브라우저 표시를 검증한다.
6. 확인하지 못한 실행 결과는 미검증으로 표기한다.
7. 원격 문서를 읽을 수 없으면 추정 적용하지 않고 로컬 규칙 사본을 요구한다.
```

README 링크는 **사람에게 기준을 안내**하는 기능이고, `AGENTS.md`는 **AI 코딩 에이전트에 작업 규칙을 안내**하는 역할입니다. 다만 모든 AI가 자동으로 원격 URL을 읽는 것은 아니므로, 필요 시 로컬 사본을 함께 제공해야 합니다.

## 4. 실제 템플릿을 복사해 사용하기

```bash
# 표준 저장소를 읽기 전용 참고용으로 내려받기
# 현재 폴더에 rule_md가 생성됩니다.
git clone https://github.com/Yuul-Jung/rule_md.git

# 교육 HTML 템플릿 복사(샘플 원고·디자인·생성기)
cp -a rule_md/web/education-html/. ./

# Python 가상환경 구성
python3 -m venv .venv
source .venv/bin/activate
python -m pip install mistune

# 강좌 설정과 content/*.md 편집 후 생성
python build.py
```

`cp -a`는 같은 이름의 파일을 덮어쓸 수 있습니다. **기존 프로젝트에서는 백업하거나 빈 템플릿 폴더에 복사**한 다음 필요한 파일만 병합하세요. `example-output/`은 예제이므로 운영 배포에는 `dist/`를 사용합니다.

## 5. 동일 버전 유지하기

`main` 브랜치 링크는 표준이 수정되면 내용이 바뀔 수 있습니다. 장기적으로 특정 규격을 유지하려면 검토한 커밋 SHA를 기록하고 해당 커밋 URL을 사용하세요.

예: `https://github.com/Yuul-Jung/rule_md/blob/<검증한-커밋-SHA>/web/education-html/STANDARD.md`

## 6. GitHub Pages 게시

1. `python build.py` 실행 후 `dist/`의 HTML 목록과 장별 파일명을 확인합니다.
2. 생성된 `index.html`과 모든 장별 HTML을 대상 저장소의 Pages 게시 폴더에 올립니다.
3. GitHub **Settings → Pages**에서 게시 브랜치/폴더를 지정합니다.
4. INDEX 링크·모바일 메뉴·코드 복사·대표 이미지 표시를 실제 브라우저로 확인합니다.

**버전 정책:** GitHub Pages 진입점은 `index.html`로 고정하고, 장별 산출물만 `_vNN.html` 형식으로 변경합니다. 생성기 출력 폴더의 구버전은 정리하되 원본 콘텐츠와 Git 이력은 보존합니다.
