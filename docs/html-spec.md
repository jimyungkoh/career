# HTML 문서 규격

`output/resume.html`과 `output/work-experience.html`을 생성·재생성하거나 스타일·레이아웃을 수정할 때 반드시 적용한다. 공통 템플릿 파일이나 빌드 도구 대신 이 규격으로 두 독립형 HTML의 디자인을 유지한다.

## 원천과 수정 범위

- 경로는 저장소 루트 기준이다. 각 `output/<name>.html`의 내용 원천은 `content/<name>.md`다. 현재 문서 목록과 대응 관계는 [README.md](../README.md)의 `문서` 표를 따른다. 이 문서는 디자인 규격이며 경력 내용의 원천이 아니다.
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
| `--space-section` | `32px` | 최상위 섹션 사이 |
| `--space-group` | `16px` | 섹션 안의 프로젝트·경험, 상위 제목과 하위 그룹 사이 |
| `--space-content` | `8px` | 제목과 본문·목록, 문단과 목록 사이 |
| `--space-item` | `4px` | 같은 목록 안의 항목 사이 |

### 간격 계층

- 화면·모바일·인쇄에서 `32 > 16 > 8 > 4px`의 같은 계층을 사용한다. 상위 섹션 하나만 줄이거나 인쇄에서 하위 간격을 따로 키우지 않는다.
- 이력서의 `section`과 경력기술서의 `section.block`은 각 문서의 최상위 섹션이다. 이력서의 `.project`·`.other-item`은 그 아래 그룹이다.
- 상위 `h2`에서 첫 하위 그룹까지는 `16px`, 프로젝트 제목에서 본문·목록까지는 `8px`다. 첫 `.other-item`의 위 마진과 `.chips`의 위 마진은 없애 `h2` 아래 마진만 적용한다.
- 목록의 마지막 `li`와 마지막 `.cert-row`에는 아래 마진을 두지 않는다. 하위 요소의 끝 여백이 다음 상위 섹션의 간격에 관여하지 않게 한다.
- CSS 숫자뿐 아니라 인접 요소의 실제 경계 사이 거리를 확인한다. 마진 상쇄로 첫 항목의 간격이 달라지는 경우도 점검한다.

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
- `ul.dia`: 기본 목록 표식 제거, 위 마진 `var(--space-content)`. `li`는 상대 위치, 왼쪽 패딩 `22px`, 아래 마진 `var(--space-item)`이며 마지막 항목은 `0`.
- `ul.dia li::before`: 빈 내용, 절대 위치, 왼쪽 `4px`, 크기 `6px × 6px`, 배경 `var(--ink)`, `transform: rotate(45deg) translateY(-50%)`. 세로 위치는 문서별 표를 따른다.
- `ul.dia strong`: 색 `var(--ink)`, 굵기 `700`.
- 링크 `a`: `color: inherit` 한 규칙만 지정한다. 링크 색은 각자가 놓인 문맥 색을 그대로 상속하고(예: 헤더 `.contact`의 `--muted`), 밑줄은 브라우저 기본값을 유지한다. 요소별로 링크 색을 따로 지정하지 않는다.

## 문서별 차이

같은 클래스 이름이어도 아래 차이는 유지한다.

| 항목 | 이력서 | 경력기술서 |
| --- | --- | --- |
| `<title>` | `고지명 · Product Engineer` | `경력기술서 · 고지명` |
| 본문 행간 | `1.72` | `1.75` |
| `.masthead` 아래 마진 | `28px` | `26px` |
| `h1` 크기 / 행간 / 위 마진 | `34px` / `1.2` / `0` | `32px` / `1.25` / `6px` |
| `.intro` 아래 마진 | `8px` | `8px` |
| 섹션 위 마진 | `section`: `32px` | `section.block`: `32px` |
| `h2` 아래 마진 | `16px` | `16px` (`.proj-head` 안에서는 `0`) |
| `.proj-head` 아래 마진 | `0` (뒤따르는 목록의 위 마진 `8px`) | `8px` |
| `.note` 위 마진 | `8px` | `8px` |
| `ul.dia` 위 마진 | `8px` | `8px` |
| 다이아몬드 표식 `top` | `0.78em` | `0.8em` |

### 이력서 구조

- `.sheet` 안에 `.masthead` → `.intro` → `section` 순서로 배치한다.
- 헤더의 이름 `h1`, `.role`, `.contact` 구조를 유지한다.
- 경력은 `.company`, `.role-line`, `.project`, `.proj-head h3`, `.date`, `ul.dia`로 표현한다. `.project` 위 마진은 `var(--space-group)`이며 프로젝트 제목은 `16px`, 굵기 `700`이다.
- 기타 경험은 `.other-item`과 `.org`, 자격 사항은 `.cert-row`와 `.what`, `.sub`를 유지한다. `.other-item` 사이 간격은 `16px`, `.org` 위 마진은 `4px`, `.cert-row` 사이 간격은 `8px`다.
- 기술 목록은 `.chips` 안의 `span`으로 표현한다. flex 줄바꿈, 간격 `8px`를 사용하고 위 마진은 두지 않는다.
- 칩 토큰: `--chip-bg: #f4f5f7`, `--chip-border: #d7dae0`, `--chip-text: #454b54`.
- 칩: 테두리 `1px solid var(--chip-border)`, 배경 `var(--chip-bg)`, 반경 `7px`, 패딩 `5px 14px`, 크기 `13px`, 굵기 `500`, 색 `var(--chip-text)`.

### 경력기술서 구조

- `.sheet` 안에 `.masthead` → `hr.head-rule` → `.intro` → `.note` → `section.block` 순서로 배치한다.
- 헤더의 `.kicker`, `h1`, `.company`, `.role-line` 구조를 유지한다.
- 프로젝트는 `.proj-head` 안의 `h2`와 `.date`로 표현한다. 이 `h2`의 아래 마진은 `0`, 자간은 `0.5px`이다.
- 2쪽 구성은 프로젝트마다 배경·담당 범위를 합친 소개 `p` 하나와 기능별 구현·성과를 연결한 `ul.dia` 항목 2~4개로 작성한다. 별도 `CORE CAPABILITIES`, 반복 소제목, 기술 요약 목록은 두지 않는다. 핵심 기술·판단·성과 수치와 측정 조건은 해당 본문에 남긴다.
- 상세 소제목 `h4`: 크기 `15px`, 굵기 `700`, 색 `var(--ink)`, 마진 `var(--space-group) 0 var(--space-content)` (`16px 0 8px`).
- `.block p`의 아래 마진은 `var(--space-content)` (`8px`). 본문 `p strong`은 색 `var(--ink)`, 굵기 `700`이다.
- `.tech-points`: 크기 `13.5px`, 색 `var(--muted)`, 위 마진 `16px`. 내부 `strong`도 같은 색에 굵기 `700`을 사용한다.
- `hr.head-rule`, `hr.project-sep`: 기본 테두리를 없애고 위쪽에 `1px solid var(--rule)`을 적용한다. 마진은 각각 `0 0 26px`, `var(--space-section) 0 0` (`32px 0 0`)이다.

## 모바일·인쇄

- `@media print`: `body` 배경을 흰색, 패딩을 `0`으로 한다. `.sheet`는 그림자 제거, `max-width: none`, 패딩 `0`으로 한다.
- `@media (max-width: 720px)`: `body` 패딩 `0`, `.sheet` 패딩 `40px 24px`를 유지한다.
- 기존 미디어 쿼리 순서와 동작을 보존한다. 인쇄와 좁은 화면에서 모두 적용될 수 있으므로 변경 시 실제 결과를 확인한다.
- 인쇄 전용 값은 `@media print` 안에서만 덮어쓰고 화면 표시를 바꾸지 않는다. 화면에서 확인한 줄바꿈·행간·여백은 그대로 둔다.

### 인쇄 적용 값

간격은 위 공통 토큰을 상속하며 인쇄 전용으로 재정의하지 않는다.

| 항목 | 이력서 | 경력기술서 |
| --- | --- | --- |
| `@page` 여백 | `20mm 16mm` | `11mm 15mm` |
| `body` 행간 | `1.72` | `1.76` |
| 섹션 위 여백 | `section` `32px` | `section.block` `32px` |
| 목록 항목 아래 여백 | `ul.dia li` `4px`, 마지막은 `0` | `ul.dia li` `4px`, 마지막은 `0` |
| 프로젝트 머리 아래 여백 | `.proj-head` `0` | `.proj-head` `8px` |

- 강제 페이지 나눔(`break-before: page`)을 쓰지 않는다. 두 문서 모두 흐름대로 배치하고, 페이지를 채우려고 간격 계층을 깨거나 종이 여백을 늘리지 않는다.
- 인쇄 시 `ul.dia`는 `list-style: disc; padding-left: 22px`, 내부 `li`는 `position: static; padding-left: 0`으로 바꾸고 `li::before`는 `content: none`으로 숨긴다. 화면의 다이아몬드는 유지하되 PDF에서는 기본 목록 표식을 사용해 본문이 제목 뒤로 밀려 추출되는 현상을 막는다. 텍스트 추출 순서는 PDF 재생성 후 별도로 검증한다.
- 인쇄 결과물과 페이지 밀도 기준은 [PDF 문서 규격](pdf-spec.md)을 따른다.

## 완료 전 확인

- [ ] SoT 내용이 HTML에 빠짐없이 반영되었고, 임의로 추가한 경력·수치가 없다.
- [ ] 독립형 HTML, 인라인 CSS, 허용된 폰트 CDN만 사용하는 형식을 유지했다.
- [ ] 공통 토큰·레이아웃과 문서별 차이를 유지했다.
- [ ] 화면·모바일·인쇄에서 실제 섹션 간격이 하위 그룹·본문·목록 항목 간격보다 크다.
- [ ] 내용만 수정한 경우 불필요한 CSS·구조 변경이 없다.
- [ ] 내용을 바꿔 인쇄 값이 어긋나면 [PDF 문서 규격](pdf-spec.md)에 따라 PDF를 재생성하고 밀도 기준을 확인했다.
- [ ] 스타일·구조를 변경했다면 데스크톱·모바일·인쇄 미리보기에서 잘림·가로 넘침·제목과 날짜 겹침을 확인했다. 확인하지 못한 항목은 완료 보고에 명시한다.

실제 간격 확인: 각 HTML을 열고 브라우저 콘솔에서 실행한다. 데스크톱·모바일 너비와 DevTools의 print 미디어 에뮬레이션에서 반복한다. PDF의 페이지 경계·밀도는 별도로 확인한다.

```javascript
await document.fonts.ready;
if (!document.querySelector('.sheet > section')) throw new Error('문서 없음');
for (const [selector, expected] of [
  ['.sheet > section', 32], ['.project', 16],
  ['.other-item + .other-item', 16], ['h2 + .other-item', 16],
  ['ul.dia', 8], ['.block > .proj-head + p', 8],
  ['.cert-row + .cert-row', 8], ['ul.dia > li + li', 4]
]) {
  for (const el of document.querySelectorAll(selector)) {
    const gap = el.getBoundingClientRect().top
      - el.previousElementSibling.getBoundingClientRect().bottom;
    if (Math.abs(gap - expected) > 1) {
      throw new Error(`${selector}: ${gap}px, expected ${expected}px`);
    }
  }
}
console.log('간격 계층 확인 완료');
```
