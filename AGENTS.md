# Agent Guide

이력서·경력기술서 관리 디렉터리.

## Always On

파일을 수정할 때 내용을 공유하거나 서로 참조하는 관련 파일이 있으면 항상 함께 갱신해 문서 간 모순이 생기지 않게 한다. 아래 규칙들은 이 원칙의 구체 사례다.

### Source of Truth (SoT)

`content/`의 Markdown 파일이 이 디렉터리의 유일한 원천(SoT)이며, `content/<name>.md`는 `output/<name>.html`과 `output/<name>.pdf`에 대응한다. 현재 문서 목록과 대응 관계는 [README.md](README.md)의 `문서` 표를 기준으로 한다.

경로는 저장소 루트 기준이다. 두 디렉터리는 모두 Git으로 추적하며, 관리 규칙은 `docs/`, 미반영 메모는 `pending/`에 둔다.

### 갱신 규칙

1. **SoT만 편집한다.** `content/<name>.md`를 수정하면, 같은 작업 안에서 `output/<name>.html`과 `output/<name>.pdf`도 반드시 함께 갱신한다. md만 수정한 채 작업을 끝내지 않는다.
2. **파생 산출물을 직접 편집하지 않는다.** `.html`과 `.pdf`는 SoT에서 파생된 산출물이다. 내용 변경이 필요하면 SoT md를 먼저 수정한 뒤 재생성한다. 단, SoT 내용과 무관한 스타일·레이아웃 개선은 html에서 수행할 수 있고, 이때도 PDF를 재생성한다.
3. **HTML 형식을 유지한다.** HTML 생성·재생성·수정 전에 반드시 [HTML 문서 규격](docs/html-spec.md)을 읽고 적용한다. 각 html은 독립형 단일 파일(인라인 `<style>`, 외부 의존은 Pretendard 폰트 CDN만)로 유지하고, 기존 디자인 토큰(CSS 변수, `.sheet` 레이아웃, `.masthead` 등 섹션 구조)을 보존한 채 SoT의 내용만 반영한다.
4. **PDF 밀도를 유지한다.** PDF 생성·재생성 전에 반드시 [PDF 문서 규격](docs/pdf-spec.md)을 읽고 적용한다. 페이지 하단 공백은 마지막 페이지 15% 이내, 나머지 페이지 10% 이내로 두고, 강제 페이지 나눔이나 섹션 간격 확대로 공백을 만들지 않는다. 인쇄 전용 값은 `@media print` 안에서만 바꾼다.
5. **문서 간 정합성을 유지한다.** 두 SoT는 같은 경력을 다른 깊이로 서술하므로, 회사·직책·기간·성과 수치(예: 40초→10초, 건당 비용 90% 이상 절감, DR 기동 약 5분과 월 고정비 약 2달러, 로드 3초→0.7초, 이미지 용량 77.5% 절감)가 양쪽에서 일치해야 한다. 한쪽만 수정하면 다른 쪽도 함께 점검한다.
6. **미반영 내용은 `pending/`에 정리한다.** 사용자가 명시적으로 반영을 지시하거나 대상 파일을 지목하지 않은 경우, 이력서·경력기술서 관련 새 내용은 SoT를 직접 수정하지 않고 `pending/`에 문서로 정리한다. 경로·형식은 `docs/pending-convention.md`를 따른다.

## Just In Time

아래 문서는 해당 조건일 때만 읽고 적용한다. 일괄 로드하지 않는다.

```text
docs/
├── html-spec.md — HTML 문서 규격; HTML 생성·재생성·수정 시 반드시 읽고 적용
├── pdf-spec.md — PDF 문서 규격; PDF 생성·재생성 시 반드시 읽고 적용
├── commit-convention.md — 커밋 컨벤션; commit 요청 시
└── pending-convention.md — pending 문서 규칙; `pending/`에 문서 저장·수정 시 또는 `pending/` 내용을 SoT에 반영할 때
```
