# career

고지명의 이력서·경력기술서를 관리하는 저장소.

## 구조

```text
career/
├── AGENTS.md   # 에이전트 작업 규칙
├── README.md   # 문서 안내
├── content/    # 원천(SoT) — 내용 편집 대상
├── output/     # 산출물 — 열람·제출 대상
├── docs/       # 관리 규칙·디자인 규격
└── pending/    # 미반영 메모 (Git 제외)
```

`content/`와 `output/`은 모두 Git으로 추적하고, 변경 이력은 Git으로 관리한다.

## 문서

| 문서 | 원천 (SoT) | 산출물 |
| --- | --- | --- |
| 이력서 | [resume.md](content/resume.md) | [resume.html](output/resume.html) |
| 경력기술서 | [work-experience.md](content/work-experience.md) | [work-experience.html](output/work-experience.html) |

현재 문서 목록과 SoT–산출물 대응은 이 표를 기준으로 한다.

## 갱신

내용 수정은 `content/`의 SoT md에서만 수행하고, 같은 작업에서 `output/`의 대응 HTML에도 반영한다. HTML은 파생 산출물이므로 내용을 직접 수정하지 않는다. 스타일·레이아웃을 포함한 HTML 갱신은 [HTML 문서 규격](docs/html-spec.md)을 따른다.

## 규칙

- 에이전트 작업 규칙: [AGENTS.md](AGENTS.md)
- HTML 문서 규격: [docs/html-spec.md](docs/html-spec.md)
- 커밋 컨벤션: [docs/commit-convention.md](docs/commit-convention.md)
- Pending 문서 규칙: [docs/pending-convention.md](docs/pending-convention.md)
