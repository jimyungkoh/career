# 커밋 컨벤션

## 형식

```text
type(scope): 한국어 제목

Why
- ...

What
- ...

How
- ...

검증
- ...
```

## 규칙

- Conventional Commits 기반. 허용 type: `merge`, `feat`, `fix`, `docs`, `style`, `refactor`, `perf`, `test`, `build`, `ci`, `chore`, `revert`.
- `scope`는 소문자.
- 제목은 한국어, 마침표 없음. 영문 대소문자 제한 없음.
- header 최대 200자, body 한 줄 최대 10,000자.

## 본문 작성 원칙

- **Why**: 배경과 해결할 문제. 제목 반복 금지.
- **What**: 파일 목록이 아닌 바뀐 동작과 영향 범위. 전후 변화.
- **How**: 선택한 구현 방식과 핵심 접근. 대안 대신 이 방식을 택한 이유.
- **검증**: 실행한 명령과 확인한 결과. 실패·미실행 검증은 사유와 함께 기록.

## Trailer

해당하는 것만 본문 아래에 추가:

```text
Constraint: 외부 제약
Rejected: 버린 대안 | 이유
Confidence: high|medium|low
Scope-risk: narrow|moderate|broad
Directive: 다음 수정자가 주의할 점
Tested: 실행한 검증
Not-tested: 확인하지 못한 범위
```

## 커밋 실행 규칙

- 명시적 요청 시에만 commit. push/PR로 확대 해석 금지.
- 내가 만든 변경만 stage (`git add -p` 또는 명시적 경로). 성격이 다른 변경은 논리 커밋으로 분리.
- secrets, `.env*`, token, key, 로컬 전용 설정과 작업용 임시 파일 커밋 금지.
- 정리 목적의 `git restore`/`reset --hard`/`clean`/`stash` 실행 금지.

## 검증과 완료 확인

- 커밋 전 `git status`, `git diff`, `git diff --staged`로 변경과 stage 범위를 확인한다.
- 저장소에 설정된 검증 명령과 훅이 있으면 사용한다. 특정 패키지 매니저나 훅 도구를 전제하지 않는다.
- 훅이 파일을 수정하면 변경 내용과 stage 범위를 다시 확인한다.
- 커밋 후 `git status`와 `git show --stat --oneline HEAD`로 결과와 남은 변경을 확인한다.
