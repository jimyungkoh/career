# HTML 문서 규격

`output/resume.html`과 `output/work-experience.html`을 생성·재생성하거나 스타일·레이아웃을 수정할 때 반드시 적용한다. 공통 템플릿 파일이나 빌드 도구 대신 이 규격으로 두 독립형 HTML의 디자인을 유지한다.

## 원천과 수정 범위

- 경로는 저장소 루트 기준이다. 내용의 유일한 원천은 각각 `content/resume-sot.md`, `content/work-experience-sot.md`다. 이 문서는 디자인 규격이며 경력 내용의 원천이 아니다.
- 내용 변경은 SoT에서 먼저 수행하고 같은 작업에서 대응 HTML에 반영한다. 회사·직책·기간·성과 수치는 두 SoT 간에도 확인한다.
- 기존 HTML을 기준으로 필요한 부분만 갱신한다. 내용 갱신을 이유로 디자인을 새로 만들거나 문서별 차이를 임의로 통일하지 않는다.
- 디자인 변경을 명시적으로 요청받아 아래 규격을 바꾸면 이 문서도 함께 갱신한다.

## 파일 형식

- `<!DOCTYPE html>`, `<html lang="ko">`, UTF-8, viewport 메타 태그, 문서별 `<title>`을 유지한다.
- CSS는 각 HTML의 `<head>` 안에 있는 인라인 `<style>`에 포함한다.
- 외부 의존은 아래 Pretendard 스타일시트만 허용한다. 별도 CSS·JS 파일, UI 프레임워크, 아이콘 CDN, 빌드 도구는 추가하지 않는다.

  `https://cdn.jsdelivr.net/gh/orioncactus/pretendard@v1.3.9/dist/web/variable/pretendardvariable-dynamic-subset.min.css`

- CSS는 토큰·리셋·기본 레이아웃 → 헤더 → 섹션·본문 → 목록 → 문서별 요소 → 인쇄·모바일 규칙 순서로 정돈한다. 순서 변경 시 캐스케이드와 기존 출력이 달라지지 않게 한다.

## 공통 디자인

### 토큰

| CSS 변수 | 값 | 용도 |
| --- | --- | --- |
| `--ink` | `#1c2330` | 제목·강조·장식 |
| `--body` | `#3d4552` | 본문 |
| `--muted` | `#7a8089` | 보조 정보·날짜 |
| `--faint` | `#9aa0a8` | 주석·약한 장식 |
| `--rule` | `#e5e7ea` | 구분선 |

### 기본 레이아웃·타이포그래피

- 전체 요소: `margin: 0; padding: 0; box-sizing: border-box`.
- `html`: `-webkit-font-smoothing: antialiased; text-rendering: optimizeLegibility`.
- 본문 폰트: `'Pretendard Variable', Pretendard, -apple-system, BlinkMacSystemFont, 'Apple SD Gothic Neo', 'Noto Sans KR', sans-serif`.
- `body`: 배경 `#eceef1`, 글자색 `var(--body)`, 글자 크기 `14.5px`, 패딩 `48px 16px`. 행간은 문서별 표를 따른다.
- `.sheet`: 최대 너비 `840px`, `margin: 0 auto`, 흰색 배경, 패딩 `76px 84px`, 그림자 `0 2px 24px rgba(15, 23, 42, 0.08)`.
- `.masthead`: 왼쪽 테두리 `5px solid var(--ink)`, 왼쪽 패딩 `22px`.
- `.masthead h1`: 굵기 `800`, 색 `var(--ink)`, 자간 `0.5px`.
- `h2`: 크기 `19px`, 굵기 `800`, 색 `var(--ink)`, 자간 `2px`, 행간 `1.35`, 왼쪽 테두리 `5px solid var(--ink)`, 왼쪽 패딩 `14px`.
- `.proj-head`: flex, 양끝 정렬, baseline 정렬, 간격 `16px`.
- `.date`: 크기 `13px`, 색 `var(--muted)`, `white-space: nowrap`.
- `.intro strong`: 색 `var(--ink)`, 굵기 `700`.
- `.note`: 크기 `13.5px`, 이탤릭, 색 `var(--faint)`.
- `ul.dia`: 기본 목록 표식 제거. `li`는 상대 위치, 왼쪽 패딩 `22px`, 아래 마진 `7px`.
- `ul.dia li::before`: 빈 내용, 절대 위치, 왼쪽 `4px`, 크기 `6px × 6px`, 배경 `var(--ink)`, `transform: rotate(45deg) translateY(-50%)`. 세로 위치는 문서별 표를 따른다.
- `ul.dia strong`: 색 `var(--ink)`, 굵기 `700`.

## 문서별 차이

같은 클래스 이름이어도 아래 차이는 유지한다.

| 항목 | 이력서 | 경력기술서 |
| --- | --- | --- |
| `<title>` | `고지명 · Product Engineer` | `경력기술서 · 고지명` |
| 본문 행간 | `1.72` | `1.75` |
| `.masthead` 아래 마진 | `28px` | `26px` |
| `h1` 크기 / 행간 / 위 마진 | `34px` / `1.2` / `0` | `32px` / `1.25` / `6px` |
| `.intro` 아래 마진 | `14px` | `6px` |
| 섹션 위 마진 | `section`: `40px` | `section.block`: `38px` |
| `h2` 아래 마진 | `18px` | `16px` |
| `.proj-head` 아래 마진 | `0` | `16px` |
| `.note` 위 마진 | `8px` | `14px` |
| `ul.dia` 위 마진 | `8px` | `6px` |
| 다이아몬드 표식 `top` | `0.78em` | `0.8em` |

### 이력서 구조

- `.sheet` 안에 `.masthead` → `.intro` → `section` 순서로 배치한다.
- 헤더의 이름 `h1`, `.role`, `.contact` 구조를 유지한다.
- 경력은 `.company`, `.role-line`, `.project`, `.proj-head h3`, `.date`, `ul.dia`로 표현한다. `.project` 위 마진은 `24px`이며 프로젝트 제목은 `16px`, 굵기 `700`이다.
- 기타 경험은 `.other-item`과 `.org`, 자격 사항은 `.cert-row`와 `.what`, `.sub`를 유지한다.
- 기술 목록은 `.chips` 안의 `span`으로 표현한다. flex 줄바꿈, 간격 `8px`, 위 마진 `6px`를 사용한다.
- 칩 토큰: `--chip-bg: #f4f5f7`, `--chip-border: #d7dae0`, `--chip-text: #454b54`.
- 칩: 테두리 `1px solid var(--chip-border)`, 배경 `var(--chip-bg)`, 반경 `7px`, 패딩 `5px 14px`, 크기 `13px`, 굵기 `500`, 색 `var(--chip-text)`.

### 경력기술서 구조

- `.sheet` 안에 `.masthead` → `hr.head-rule` → `.intro` → `section.block` 순서로 배치한다.
- 헤더의 `.kicker`, `h1`, `.company`, `.role-line` 구조를 유지한다.
- 프로젝트는 `.proj-head` 안의 `h2`와 `.date`로 표현한다. 이 `h2`의 아래 마진은 `0`, 자간은 `0.5px`이다.
- 상세 소제목 `h4`: 크기 `15px`, 굵기 `700`, 색 `var(--ink)`, 마진 `22px 0 6px`.
- `.block p`의 아래 마진은 `4px`. 본문 `p strong`은 색 `var(--ink)`, 굵기 `700`이다.
- `.tech-points`: 크기 `13.5px`, 색 `var(--muted)`, 위 마진 `16px`. 내부 `strong`도 같은 색에 굵기 `700`을 사용한다.
- `hr.head-rule`, `hr.project-sep`: 기본 테두리를 없애고 위쪽에 `1px solid var(--rule)`을 적용한다. 마진은 각각 `0 0 26px`, `38px 0 0`이다.

## 모바일·인쇄

- `@media print`: `body` 배경을 흰색, 패딩을 `0`으로 한다. `.sheet`는 그림자 제거, `max-width: none`, 패딩 `0`으로 한다.
- `@media (max-width: 720px)`: `body` 패딩 `0`, `.sheet` 패딩 `40px 24px`를 유지한다.
- 기존 미디어 쿼리 순서와 동작을 보존한다. 인쇄와 좁은 화면에서 모두 적용될 수 있으므로 변경 시 실제 결과를 확인한다.

## 완료 전 확인

- [ ] SoT 내용이 HTML에 빠짐없이 반영되었고, 임의로 추가한 경력·수치가 없다.
- [ ] 독립형 HTML, 인라인 CSS, 허용된 폰트 CDN만 사용하는 형식을 유지했다.
- [ ] 공통 토큰·레이아웃과 문서별 차이를 유지했다.
- [ ] 내용만 수정한 경우 불필요한 CSS·구조 변경이 없다.
- [ ] 스타일·구조를 변경했다면 데스크톱·모바일·인쇄 미리보기에서 잘림·가로 넘침·제목과 날짜 겹침을 확인했다. 확인하지 못한 항목은 완료 보고에 명시한다.
