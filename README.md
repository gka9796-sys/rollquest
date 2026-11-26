# 롤퀘스트 (QuestHub) 랜딩페이지 · MVP 체험판

외부 CDN·폰트·이미지·스크립트를 쓰지 않는 정적 페이지 두 개입니다. 서버 없이, 빌드 없이 그대로 열립니다.

| 파일 | 역할 |
| --- | --- |
| `index.html` | 소개·가설 검증 랜딩페이지 (HTML + CSS 인라인, 스크립트 없음). **1분 설문(Google Forms)이 페이지 안에 임베드**되어 있습니다. |
| `app.html` | **MVP 체험판** — 미션 체크 보드 + 마감 카운트다운 + ‘하루 몇 판’ 계산기 (HTML + CSS + JS 한 파일, localStorage 사용) |
| `scanner.html` | **스크린샷 미션 인식 시제품** — 미션 화면 캡처를 올리면 브라우저 안에서 OCR 후 규칙으로 미션 목록을 만들고 `app.html`로 넘깁니다 |
| `assets/vendor/` | OCR 엔진(Tesseract.js)과 언어 데이터(tessdata_fast kor·eng). 외부 CDN 없이 이 폴더에서만 불러옵니다 |
| `assets/sample-mission.png` | 예시 이미지 (이 프로젝트에서 직접 만든 가짜 임무 화면) |
| `README.md` | 이 문서 |

제품명 표기는 **롤퀘스트 (QuestHub)** 로 통일했습니다. 라이브 설문(Google Forms)이 `롤퀘스트`로 되어 있어, 화면의 첫 표기는 `롤퀘스트 (QuestHub)`, 이후 문장은 `롤퀘스트`로 적습니다.

## 미리보기

`index.html` 을 브라우저로 열면 됩니다(더블클릭 또는 `file://` 경로). `app.html` 도 같은 방식으로 열리며, 두 파일이 같은 폴더에 있으면 서로 링크가 동작합니다.

`file://` 로 열 때 일부 브라우저는 localStorage를 막습니다. 그 경우 체크가 새로 고침 뒤에 남지 않고, 체험판 상단에 `저장 차단됨` 이 표시됩니다. 배포 후 `https://` 주소에서는 정상 저장됩니다.

## GitHub Pages 무료 배포 (아직 하지 않음 — 승인 후 진행)

1. GitHub에서 새 저장소를 만듭니다 — 예: `questhub-landing`, **Public**.
2. 이 폴더의 파일 세 개(`index.html`, `app.html`, `README.md`)를 저장소 **루트**에 올립니다. 두 HTML이 같은 폴더에 있어야 `index.html → app.html` 링크가 깨지지 않습니다.
   - 웹 업로드: 저장소 → **Add file → Upload files** → 세 파일 선택 → **Commit changes**.
   - 터미널을 쓴다면:
     ```bash
     cd documents/questhub-landing
     git init -b main
     git add index.html app.html README.md
     git commit -m "롤퀘스트(QuestHub) 랜딩페이지 + MVP 체험판"
     git remote add origin https://github.com/<계정>/questhub-landing.git
     git push -u origin main
     ```
3. 저장소 **Settings → Pages** 로 이동합니다.
   - **Source**: `Deploy from a branch`
   - **Branch**: `main` / `/ (root)` → **Save**
4. 1~2분 뒤 아래 주소가 열립니다 (계정 이름에 따라 다름).
   - `https://<계정>.github.io/questhub-landing/` → `index.html`
   - `https://<계정>.github.io/questhub-landing/app.html` → 체험판
5. 배포 후 이 네 가지를 직접 확인합니다.
   - 랜딩 상단의 **MVP 체험하기** 버튼이 `app.html` 로 이동하는가
   - 체험판에서 미션을 체크하고 새로 고침해도 체크가 남는가 (localStorage)
   - 페이스 계산기 숫자가 바뀌는가
   - `1분 설문` 버튼이 Google Forms로 열리는가

> 저장소 이름을 `questhub-landing` 이 아닌 `<계정>.github.io` 로 만들면 주소가 `https://<계정>.github.io/` 가 됩니다. 두 방식 모두 상대 경로라 파일은 그대로 씁니다.

## 배포 전에 정할 것

- **제품명**: `롤퀘스트 (QuestHub)` 로 통일 완료. 설문 폼 제목과 화면 표기가 일치합니다.
- **연락처**: 개인 이메일은 넣지 않았습니다(공개 페이지 스팸 노출 방지). 필요하면 푸터에 추가하세요.
- **og:image**: 아직 없습니다. 공유 미리보기를 쓰려면 1200×630 PNG를 같은 폴더에 두고 두 HTML의 `<head>` 에 `<meta property="og:image" content="og.png">` 를 추가합니다.
- **검색 노출**: `app.html` 에는 `<meta name="robots" content="noindex">` 를 넣어 두었습니다(체험판이 검색 결과로 먼저 노출되지 않게). 랜딩까지 막으려면 `index.html` `<head>` 에도 같은 줄을 넣으세요.

## 수정할 때 손대는 곳

### `index.html`

| 바꾸고 싶은 것 | 위치 |
| --- | --- |
| 색·글꼴 | `:root` 의 CSS 변수 |
| 설문 링크 | `docs.google.com/forms/...` 가 들어간 `<a>` 4곳 |
| 예시 화면 숫자 | `.mock` 안의 `27 / 48`, `2 / 4`, 진행 바 `width` |
| FAQ | `#faq` 섹션의 `<details>` 블록 |
| 체험판 진입 버튼 | 헤더 `.header-btns`, 히어로 `.cta-row`, `#demo` 섹션, 마지막 CTA, 푸터 |

### `app.html`

| 바꾸고 싶은 것 | 위치 (스크립트 안) |
| --- | --- |
| 패스 진척 마감·비활성화 시각 | `PROGRESS_END`, `PASS_OFF` (`kstDate(2027, 0, 6, 16, 59)` 형식, 월은 0부터) |
| 기본 미션 목록·BXP | `DEFAULT_MISSIONS` 배열 |
| 기본 리셋 시각 | `state.resetHour` (5 = 05:00 KST) |
| 판당 BXP 기본값 | `state.pace.bxpPerGame` (50) |
| 문구·안내 | HTML 본문, `#notes` 섹션 |

**새 액트가 열리면** `PROGRESS_END`·`PASS_OFF` 두 줄과 `#notes` 의 연도 표기, 기본 미션 목록을 새 공지 기준으로 고치면 됩니다. 날짜가 지난 뒤에 열면 마감 카드가 `종료` 로 표시되고 “새 액트가 열리면 날짜를 갱신해야 합니다” 안내가 뜹니다.

### 저장 키

브라우저 localStorage `questhub.mvp.v1` 한 곳에 미션 체크·직접 추가한 목표·리셋 시각·계산기 입력이 함께 저장됩니다. 값을 초기화하려면 브라우저 개발자 도구에서 이 키를 지우거나, 화면의 **목록 처음 상태로** 버튼을 누릅니다.

## 숫자의 근거

- 48단계 × 500 BXP, 반복 8단계 — 2026 시즌 3 월드 챔피언십 패스 (LoL 상점 패스 페이지)
- 진척 마감 2027-01-06 16:59 KST, 비활성화 2027-01-07 16:59 KST — Riot 고객지원 문서 정리
- 일일 100 BXP(1승 또는 2판), 주간 목표 4개(무작위 2×300 + 고정 2×500), 주간 리셋·3주 겹침
- **판당 BXP는 공식 고정값이 없습니다.** 분당 1.3점, 승리 +30%, 파티 +30% 로 추정한 50을 기본값으로 두고 화면에서 바꿀 수 있게 했습니다. 계산기의 가정은 화면 `#notes` 에 그대로 적어 두었습니다.

## 검증한 것 (2026-11-23)

- 두 HTML 모두 태그 균형 검사 통과(미닫힘·중복 id 없음), lxml 파싱 오류 없음, CSS 파싱 오류 없음(규칙 132개·155개).
- `app.html` 스크립트는 ES 파서(esprima) 구문 검사 통과.
- DOM 스텁 + 고정 시각(2026-11-23 18:59 KST)으로 실제 스크립트를 실행해 93개 항목 확인 — 초기 렌더, 마감 D-day·절대시각, 체크·진행률·localStorage 저장, 목표 추가/삭제, 필터, 계산기(하루 5판·총 190판), 리셋 시각 변경, 초기화, 재방문 시 값 복원, 패스 종료 후 표시, 손상된 저장값·범위 밖 입력 처리.
- 실제 브라우저 화면 렌더링은 이 작업 환경에서 페이지를 열 수 없어 눈으로 확인하지 못했습니다. 배포 전에 PC·휴대폰에서 한 번 열어 레이아웃을 봐 주세요.

## 지켜야 하는 고지

라이엇 3자 앱 정책은 제품에 아래 영문 고지 문구를 눈에 띄는 곳에 두도록 요구합니다. 두 HTML 푸터에 그대로 넣어 두었으니 지우지 마세요. (한국어 안내 문구도 함께 있습니다.)

## 2026-11-26 추가: 페이지 안 설문 · 스크린샷 미션 인식

### 1) 랜딩페이지 안 설문 (`index.html` `#survey`)

- 9문항 Google Form(`1SLItKFYc43VZT0eq9xVJQU_GusfxG504kgn5EMi1Mc8`)을 `?embedded=true` 주소로 **iframe 임베드**했습니다. 페이지를 떠나지 않고 응답·제출할 수 있고, 제출된 응답은 Google Forms에 그대로 저장됩니다.
- iframe을 못 불러오는 환경을 위해 **새 창에서 열기** 링크와 안내 문구를 함께 두었습니다(iframe 내부 문구 + 하단 링크).
- 헤더·히어로·마지막 CTA의 설문 버튼은 모두 `#survey` 앵커로 바뀌었습니다(외부 이동 없음).
- 응답을 시트 기록표로 옮기는 작업은 `documents/questhub/sync_survey_to_sheet.py`로 분리했습니다(아래 참고).

### 2) 스크린샷 미션 인식 (`scanner.html`)

- 이미지 업로드(클릭·드래그·Ctrl+V) → 미리보기 → **브라우저 안 OCR** → 규칙 파싱 → 미션 목록 → `app.html` 보드로 전달.
- OCR은 [Tesseract.js](https://github.com/naptha/tesseract.js)(Apache-2.0)와 [tessdata_fast](https://github.com/tesseract-ocr/tessdata_fast) kor·eng 모델을 **이 폴더에 직접 넣어** CDN 없이 동작합니다. 이미지는 서버로 전송되지 않습니다.
- 전처리 옵션: 어두운 배경 반전(기본 켜짐), 한국어+영어/영어만, 작은 이미지 확대.
- 파서가 잡는 것: 유형(일일/주간/이벤트), 진행도 `3 / 5`, `500 BXP`, 남은 시간(`2일 4시간`, `D-3`), 완료 표시. 확신도(높음/확인 필요/낮음)를 표시하고 이름·유형·BXP를 직접 고칠 수 있습니다.
- OCR을 못 쓰는 환경을 위해 **글자만 붙여넣어 파싱**하는 경로도 있습니다.
- 전달 방식: `localStorage` 키 `questhub.scanner.pending.v1`에 담아 두면, `app.html`이 열릴 때 한 번만 읽어 미션 목록에 추가하고 그 키를 지웁니다(같은 브라우저에서 열어야 함).

### 3) 검증 결과 (2026-11-26)

- `index.html`·`app.html`·`scanner.html` 모두 lxml 파싱 오류 0, 중복 id 0, 인라인 스크립트 esprima 구문 검사 통과.
- 실제 Chromium(원격 브라우저)에서 `raw.githack.com`으로 3개 페이지를 열어 렌더링·콘솔 오류·주요 기능을 확인했습니다. 스크린샷: `downloads/2026-11-26_rollquest_landing.png`, `downloads/2026-11-26_rollquest_app.png`, `downloads/2026-11-26_rollquest_scanner.png`.
- **한계**: 이 작업 환경에는 로컬 브라우저 바이너리가 없어 `127.0.0.1` 서버를 쓸 수 없었고, 검증은 GitHub에 푸시한 파일을 CDN 프록시로 연 것입니다. 휴대폰 화면과 Safari는 직접 확인하지 못했습니다.
