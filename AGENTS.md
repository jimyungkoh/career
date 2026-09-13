# Agent Guide

이력서·경력기술서 관리 디렉터리.

## Always On

파일을 수정할 때 내용을 공유하거나 서로 참조하는 관련 파일이 있으면 항상 함께 갱신해 문서 간 모순이 생기지 않게 한다. 아래 규칙들은 이 원칙의 구체 사례다.

### Source of Truth (SoT)

아래 두 Markdown 파일이 이 디렉터리의 유일한 원천(SoT)이다. 내용 추가·수정·삭제는 항상 이 파일들에서만 수행한다.

| SoT | 산출물 | 문서 |
| --- | --- | --- |
| `resume-sot.md` | `resume.html` | 이력서 |
| `work-experience-sot.md` | `work-experience.html` | 경력기술서 |

### 갱신 규칙

1. **SoT만 편집한다.** `-sot.md` 파일을 수정하면, 같은 작업 안에서 대응되는 `.html` 산출물도 반드시 함께 갱신한다. md만 수정한 채 작업을 끝내지 않는다.
2. **HTML을 직접 편집하지 않는다.** `.html`은 SoT에서 파생된 산출물이다. 내용 변경이 필요하면 SoT md를 먼저 수정한 뒤 html을 재생성한다. 단, SoT 내용과 무관한 스타일·레이아웃 개선은 html에서 수행할 수 있다.
3. **HTML 형식을 유지한다.** HTML 생성·재생성·수정 전에 반드시 [HTML 문서 규격](docs/html-spec.md)을 읽고 적용한다. 각 html은 독립형 단일 파일(인라인 `<style>`, 외부 의존은 Pretendard 폰트 CDN만)로 유지하고, 기존 디자인 토큰(CSS 변수, `.sheet` 레이아웃, `.masthead` 등 섹션 구조)을 보존한 채 SoT의 내용만 반영한다.
4. **문서 간 정합성을 유지한다.** 두 SoT는 같은 경력을 다른 깊이로 서술하므로, 회사·직책·기간·성과 수치(예: 40초→10초, 건당 비용 90% 절감, AI 상담 무전환 종결 62%, 로드 3초→0.7초, 이미지 용량 77.5% 절감)가 양쪽에서 일치해야 한다. 한쪽만 수정하면 다른 쪽도 함께 점검한다.

## Just In Time

아래 문서는 해당 조건일 때만 읽고 적용한다. 일괄 로드하지 않는다.

```text
docs/
├── html-spec.md — HTML 문서 규격; HTML 생성·재생성·수정 시 반드시 읽고 적용
├── commit-convention.md — 커밋 컨벤션; commit 요청 시
└── pending-convention.md — pending 문서 규칙; `pending/`에 문서 저장·수정 시
```
