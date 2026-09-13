# Pending 문서 규칙

`pending/`에 문서를 저장·수정할 때와 `pending/` 내용을 SoT에 반영할 때 적용한다. `pending/`은 이력서·경력기술서의 미반영 사항을 정리하는 로컬 작업 디렉터리이며, `.gitignore`로 git 추적에서 제외된다.

## 경로

```text
pending/${yyyy-MM}/${dd}/${aspect}.md
```

| 요소 | 값 |
| --- | --- |
| `${yyyy-MM}` | 문서를 작성한 연-월 (`2026-02`) |
| `${dd}` | 문서를 작성한 일, 2자리 (`09`, `13`) |
| `${aspect}` | 다루는 측면을 나타내는 영문 소문자 kebab-case 슬러그 (`military`, `education`, `side-project`) |

예: `pending/2026-02/13/military.md`

## 규칙

- 경로 날짜는 최초 작성 시점으로 고정한다. 이후 수정은 파일을 새로 만들지 않고 같은 경로의 파일을 갱신한다.
- 같은 날 같은 `aspect`는 하나의 파일로 유지한다.
- `pending/`은 SoT가 아니다. 사용자가 명시적으로 반영을 지시하거나 파일을 지목한 경우에만 `resume-sot.md` 또는 `work-experience-sot.md`에 반영한다.
- `pending/` 아래 파일은 커밋·stage하지 않는다.
