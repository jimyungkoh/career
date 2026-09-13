# PDF 문서 규격

`output/resume.pdf`와 `output/work-experience.pdf`를 생성·재생성할 때 적용한다. PDF는 제출·열람용 최종 산출물이며, 원천은 [HTML 문서 규격](html-spec.md)을 따르는 `output/<name>.html`이다.

## 원천과 수정 범위

- 경로는 저장소 루트 기준이다. `content/<name>.md`(SoT) → `output/<name>.html` → `output/<name>.pdf` 순서로 파생된다.
- PDF를 직접 편집하지 않는다. 내용·레이아웃 변경은 SoT와 HTML에서 수행한 뒤 PDF를 재생성한다.
- 페이지 밀도는 HTML의 인쇄 전용 CSS로 조정하고, 화면 표시는 바꾸지 않는다. 페이지를 채우려고 섹션 간격이나 종이 여백을 늘리지 않는다.

## 생성

Chrome headless로 각 HTML을 A4로 인쇄한다. 저장소 루트에서 실행한다.

```bash
for name in resume work-experience; do
  google-chrome --headless=new --disable-gpu --no-pdf-header-footer \
    --virtual-time-budget=10000 \
    --print-to-pdf="output/$name.pdf" "file://$PWD/output/$name.html"
done
```

- `--no-pdf-header-footer`로 URL·날짜 머리말을 넣지 않는다.
- 서체는 Pretendard CDN에서 받으므로 생성 시 네트워크가 필요하다.
- PDF 제목은 각 HTML의 `<title>`을 따른다.

## 인쇄 조건

인쇄 전용 값은 각 HTML의 `@media print` 안에만 둔다. 섹션·하위 그룹·본문·목록의 간격은 화면과 같은 `32 → 16 → 8 → 4px` 토큰을 상속한다.

| 항목 | 이력서 | 경력기술서 |
| --- | --- | --- |
| 용지 | A4 | A4 |
| `@page` 여백 | `20mm 16mm` | `11mm 15mm` |
| 본문 행간 | `1.78` | `1.62` |
| 섹션 위 여백 | `section` `32px` | `section.block` `32px` |
| 목록 항목 아래 여백 | `ul.dia li` `4px`, 마지막은 `0` | `ul.dia li` `4px`, 마지막은 `0` |
| 프로젝트 머리 아래 여백 | `.proj-head` `0` (뒤따르는 목록의 위 마진 `8px`) | `.proj-head` `8px` |
| 쪽수 | 2쪽 | 2쪽 |

- 강제 페이지 나눔(`break-before: page`)을 쓰지 않는다. 프로젝트와 섹션은 흐름대로 배치하고, `li`·`.proj-head`·`.cert-row`에 `break-inside: avoid`와 `break-after: avoid`를 두어 제목만 페이지 끝에 남거나 항목이 쪼개지는 것을 막는다.
- 색·서체·토큰은 HTML 문서 규격을 그대로 따르고, 인쇄에서 배경만 흰색으로 바꾼다.
- 내용이나 간격이 바뀌면 쪽수와 밀도를 다시 확인한다. 밀도 기준을 충족하지 못하면 페이지별 측정값을 완료 보고에 명시한다. 기준 자체를 임의로 완화하지 않는다.

## 밀도 기준

- 마지막 페이지를 제외한 페이지는 본문 하단 공백을 10% 이내로 유지한다.
- 마지막 페이지는 15% 이내로 둔다. 목록·제목 단위로 페이지를 나누기 때문에 남는 공백이 마지막 페이지에 모인다.
- 빈 페이지를 만들지 않는다.
- 강제 페이지 나눔으로 공백을 만드는 대신, 페이지 안에서 자연스럽게 나뉘도록 둔다.

## 완료 전 확인

- [ ] HTML 본문의 문구·수치·링크가 PDF에 빠짐없이 들어갔다.
- [ ] 쪽수와 페이지별 하단 공백이 밀도 기준 안에 있다.
- [ ] 잘린 글자, 가로 넘침, 페이지 경계에서 쪼개진 목록 항목이 없다.
- [ ] PDF 제목 메타데이터가 각 문서와 맞고 머리말·꼬리말이 없다.
- [ ] 저장소에 반영하기 전 PDF를 직접 열어 확인했다. 화면으로만 확인했다면 완료 보고에 명시한다.

밀도 확인:

```bash
python3 - <<'PY'
import fitz
MM = 72 / 25.4
for name, margin in [('resume', 20), ('work-experience', 11)]:
    doc = fitz.open(f'output/{name}.pdf')
    for i, page in enumerate(doc, 1):
        blocks = [b for b in page.get_text('blocks') if b[4].strip()]
        top, bottom = margin * MM, page.rect.height - margin * MM
        gap = 100 * (bottom - max(b[3] for b in blocks)) / (bottom - top)
        print(f'{name} p{i}: bottom_gap={gap:.1f}%')
PY
```
