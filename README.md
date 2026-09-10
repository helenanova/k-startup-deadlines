# k-startup-deadlines

한국 정부·공공기관 창업지원사업의 신청 마감일을 모은 오픈 데이터예요. K-Startup(창업진흥원) 같은 공식 공고를 직접 확인하고, 기계가 읽기 쉬운 JSON으로 정리해요.

An open dataset of application deadlines for Korean government startup support programs, verified against official announcements and published as machine-readable JSON. (English below.)

---

## 소개

창업지원사업 공고는 여러 사이트에 흩어져 있고, 마감일을 놓치면 그대로 끝이에요. 이 저장소는 진행 중인 프로그램의 신청 기간을 한 곳에 모아 두고, 캘린더 앱이나 봇, 스프레드시트에서 바로 가져다 쓸 수 있는 형태로 제공해요.

- 모든 항목은 공식 공고 원문 링크(`source_url`)를 달아요. 링크 없는 마감일은 올리지 않아요.
- 날짜와 시각은 ISO 8601 형식이고, 한국 표준시(`+09:00`) 기준이에요.
- 데이터는 [`data/programs.json`](data/programs.json) 한 파일이에요.

## 데이터 형식

각 프로그램은 이런 필드를 가져요:

| 필드 | 설명 |
| --- | --- |
| `id` | 고유 ID (예: `kstartup-178896`, K-Startup 공고 번호 기반) |
| `name_ko` / `name_en` | 프로그램 이름 (한국어 / 영어) |
| `agency_ko` / `agency_en` | 주관기관 |
| `ministry_ko` | 소관 부처 (없거나 불명확하면 `null`) |
| `category_ko` | 지원분야 (사업화, 글로벌, 시설·공간·보육 등) |
| `announcement_no` | 공고번호 (없으면 `null`) |
| `application_start` | 접수 시작 (ISO 8601, KST) |
| `application_deadline` | 접수 마감 (ISO 8601, KST) |
| `timezone` | 항상 `Asia/Seoul` |
| `eligibility_ko` | 신청 대상 요약 (요약일 뿐, 정확한 자격은 공고문 참조) |
| `support_ko` | 지원 내용 요약 |
| `source_name` / `source_url` | 공고 출처와 원문 링크 |
| `verified_at` | 이 저장소에서 마지막으로 원문을 확인한 날짜 |

스키마 정의는 [`data/schema.json`](data/schema.json)에서 볼 수 있어요.

## 사용 예시

```bash
# 아직 마감 전인 프로그램만 골라 마감 임박순으로 보기
jq '[.[] | select(.application_deadline > now | todate)] | sort_by(.application_deadline)' data/programs.json
```

## 수록 프로그램

지금은 K-Startup에 게시된 창업진흥원(KISED) 공고 위주예요. 모두의 창업 글로벌 재외국민 프로그램, 모두의 창업 프로젝트 2차, TECHFEST 2026 통합관, 대전 팁스타운 입주, 팁스(TIPS), 통합공고, 스타트업 코리아 특별비자를 담았어요. 최신 목록은 언제나 [`data/programs.json`](data/programs.json)이 정확해요.

## 기여하기

새 프로그램 추가, 마감일 정정, 출처 갱신 모두 환영해요. [CONTRIBUTING.md](CONTRIBUTING.md)를 먼저 읽어 주세요. 가장 중요한 규칙 하나: 마감일은 반드시 공식 공고에서 확인하고 원문 링크를 함께 적어 주세요.

## 주의

이 데이터는 편의를 위한 요약이에요. 신청 전에는 반드시 `source_url`의 공식 공고문을 확인해 주세요. 일정과 자격은 주관기관 사정으로 바뀔 수 있어요.

## 라이선스

[MIT](LICENSE)

---
---

## Introduction (English)

Korean startup support programs are scattered across many announcement sites, and missing a deadline is final. This repo collects application windows for ongoing programs in one place, in a format you can drop straight into a calendar app, bot, or spreadsheet.

- Every entry carries a link to the official announcement (`source_url`). No source link, no entry.
- Dates and times are ISO 8601, Korea Standard Time (`+09:00`).
- The data lives in a single file: [`data/programs.json`](data/programs.json).

## Data format

See the Korean field table above (field names are in English). The JSON Schema is in [`data/schema.json`](data/schema.json).

## Usage

```bash
# Programs still open, soonest deadline first
jq '[.[] | select(.application_deadline > now | todate)] | sort_by(.application_deadline)' data/programs.json
```

## Contributing

Additions, deadline corrections, and source refreshes are all welcome. Please read [CONTRIBUTING.md](CONTRIBUTING.md) (Korean) first. The one rule that matters most: verify every deadline against the official announcement and include its link.

## Disclaimer

This dataset is a convenience summary. Always confirm against the official announcement at `source_url` before applying. Schedules and eligibility can change at the agency's discretion.

## License

[MIT](LICENSE)
