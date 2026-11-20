# AI_TRADE_REPORT

[![자동 보고서 생성](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions/workflows/auto-update.yml/badge.svg?branch=main)](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions/workflows/auto-update.yml)

**수출·글로벌 무역·ESG 관련 12개 주제를 한 화면에서 확인하는 웹 보고서 프로젝트임.**

Python으로 보고서 HTML을 생성하고, GitHub Actions로 생성·검증·저장을 자동화함. 생성 결과는 저장소 루트의 `index.html`에 반영함.

> **현재 운영 범위**
>
> 보고서 자동 생성·검증·저장은 구현되어 있음. 현재 실행 경로의 데이터 모듈은 코드에 고정된 내용과 수치를 반환하며, 환율 추이 차트에는 난수로 생성한 예시 값이 포함되어 있음. 최신 뉴스·통계·실제 환율을 매일 수집하는 기능은 추가 구현이 필요함. 화면의 날짜나 “검증됨” 표시는 개별 자료의 최신성·정확성을 입증하지 않음.

## 바로가기

- [저장소](https://github.com/DrSujinSeo/AI_TRADE_REPORT)
- [자동 업데이트 실행 및 결과](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions/workflows/auto-update.yml)
- [전체 실행 기록](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions)
- [보고서 HTML](index.html)
- [자동 실행 설정](.github/workflows/auto-update.yml)

## 보고서 구성

| 번호 | 주제 | 화면에서 다루는 내용 |
|---|---|---|
| 1 | 산업동향 | 산업별 수출 및 공급망 관련 내용 |
| 2 | 원자재동향 | 에너지·광물·농산물 관련 내용 |
| 3 | 데일리 환율 시세 | 환율 관련 설명 및 예시 추이 차트 |
| 4 | 시장트렌드 | 주요 산업 및 시장 변화 |
| 5 | 국가동향 | 주요 수출시장 관련 내용 |
| 6 | 법적규제 | 무역·산업 관련 규제 내용 |
| 7 | 소비자동향 | 소비 및 구매행태 관련 내용 |
| 8 | 해외인증 | 해외시장 진출 관련 인증 내용 |
| 9 | 해외전시회 | 주요 전시회 관련 내용 |
| 10 | ESG | 환경·사회·지배구조 관련 내용 |
| 11 | CBAM | 탄소국경조정제도 관련 내용 |
| 12 | 지속가능경영보고서 | 지속가능성 공시 및 보고 관련 내용 |

위 표는 보고서의 주제 구성을 설명함. 개별 수치·규제·일정은 원문과 기준일을 확인한 후 활용해야 함.

## 자동 실행 방식

| 항목 | 현재 설정 |
|---|---|
| 주 실행 파일 | `.github/workflows/auto-update.yml` |
| 정기 실행 | 매일 오전 8시 한국시간, UTC 기준 전날 23시 |
| 수동 실행 | Actions 화면의 `Run workflow` 사용 |
| 코드 변경 시 실행 | `main` 브랜치의 `.github/workflows/**` 또는 `scripts/**` 변경 |
| 실행 환경 | Ubuntu 24.04 / Python 3.11 |
| 동시 실행 | 동일 저장소·브랜치의 보고서 생성을 직렬 처리함 |
| 실행 제한 | 작업별 최대 15분 |
| 생성 결과 | 루트 `index.html` |
| 저장 방식 | HTML 변경이 있을 때만 커밋·푸시함 |
| 실행 산출물 | 보고서 HTML을 아티팩트로 보관함, 보관기간 30일 |

GitHub의 예약 실행은 서비스 상황에 따라 지연될 수 있음. README 변경만으로는 보고서 생성 작업을 자동 실행하지 않음.

기존 `daily-update.yml`과 `daily-auto-update.yml`은 수동 실행 진입점으로 유지함. 두 파일 모두 주 실행 파일을 호출하며, 별도의 정기 실행 일정은 두지 않음.

## 작동 여부 확인

### 직접 실행하는 방법

1. [자동 업데이트 화면](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions/workflows/auto-update.yml)을 엶.
2. `Run workflow`를 클릭함.
3. 브랜치를 `main`으로 선택하고 실행 버튼을 클릭함.
4. 새로 생긴 실행 항목을 열고 완료 결과를 확인함.

| 표시 | 의미 | 확인할 사항 |
|---|---|---|
| `Queued` | 실행 대기 중임 | 대기 후 결과 확인 |
| `In progress` | 실행 중임 | 완료 후 결과 확인 |
| `Success` | 실행이 정상 완료됨 | 생성·검증·저장 단계 확인 |
| `Failure` | 실행 중 오류가 발생함 | 빨간색으로 표시된 단계의 로그 확인 |
| `Cancelled` | 실행이 취소됨 | 취소 사유와 이후 실행 결과 확인 |

### 정상 완료 기준

다음 단계가 모두 성공했는지 확인함.

| 실행 단계 | 확인 내용 |
|---|---|
| `Generate HTML Report` | Python으로 HTML 생성 완료 |
| `Validate report` | 고유한 섹션 ID 12개 및 HTML 종료 태그 확인 |
| `Commit and push report` | 변경된 HTML 저장 완료 또는 변경 없음으로 정상 종료 |
| `Upload report artifact` | 실행 결과 HTML 보관 완료 |

검증 단계는 문서 구조를 확인함. 데이터의 사실 여부, 원문과의 일치 여부, 출처 링크의 정상 작동 여부까지 검사하는 단계는 아님.

## 사이트 반영 확인

1. 실행 결과가 `Success`인지 확인함.
2. 저장소의 [index.html 변경 이력](https://github.com/DrSujinSeo/AI_TRADE_REPORT/commits/main/index.html)을 확인함. 내용이 같으면 새 커밋이 생기지 않을 수 있음.
3. [전체 Actions 기록](https://github.com/DrSujinSeo/AI_TRADE_REPORT/actions)에서 최신 `pages build and deployment` 결과를 별도로 확인함.
4. 사이트에서 새로고침한 뒤 보고서 내용과 메뉴 전환이 정상인지 확인함.

GitHub Pages의 주소와 배포 방식은 저장소 `Settings → Pages`에서 확인함. 보고서 생성 작업의 성공과 Pages 배포 결과는 각각 확인해야 함.

## 로컬에서 보고서 생성

Python 3.11을 기준으로 아래 명령을 저장소 루트에서 실행함.

```bash
git clone https://github.com/DrSujinSeo/AI_TRADE_REPORT.git
cd AI_TRADE_REPORT

python -m venv .venv
```

가상환경 활성화 명령은 운영체제에 따라 선택함.

**Windows PowerShell**

```powershell
.\.venv\Scripts\Activate.ps1
```

**macOS / Linux**

```bash
source .venv/bin/activate
```

의존성 설치 후 HTML을 생성함.

```bash
python -m pip install -r scripts/requirements.txt
python scripts/generate_html.py
```

생성한 `index.html`을 브라우저에서 열어 확인함. 차트는 외부 Chart.js CDN을 사용하므로 차트 표시에는 인터넷 연결이 필요함.

## 주요 파일

| 경로 | 역할 |
|---|---|
| `index.html` | 현재 게시 대상 보고서 |
| `scripts/generate_html.py` | 주 실행 절차에서 사용하는 HTML 생성기 |
| `scripts/fetch_data_crawling.py` | 위 생성기가 가져오는 데이터 모듈, 현재 고정 데이터·예시 값 반환 |
| `scripts/requirements.txt` | Python 의존성 목록 |
| `.github/workflows/auto-update.yml` | 정기·수동·코드 변경 실행을 담당하는 주 워크플로 |
| `.github/workflows/daily-update.yml` | 주 워크플로를 호출하는 기존 수동 실행 진입점 |
| `.github/workflows/daily-auto-update.yml` | 주 워크플로를 호출하는 기존 수동 실행 진입점 |

다른 이름의 생성기·수집기, `scripts/index.html`, 백업 HTML 및 기존 검증 문서는 과거 작업 파일로 남아 있음. 현재 실행 경로는 위 표의 주 워크플로와 두 Python 모듈을 기준으로 확인함. 기존 문서의 “100% 검증” 또는 “실시간 수집” 표현은 현재 기능을 보장하지 않음.

## 오류가 발생했을 때

| 증상 | 점검 방법 |
|---|---|
| Python 설치 단계 실패 | 주 워크플로의 Python 버전과 실행 환경을 확인함 |
| `403` 또는 `Permission denied` | 실행 로그의 토큰 권한, `contents: write`, 브랜치 보호 규칙을 확인함 |
| HTML 생성 단계 실패 | Python 오류 메시지와 의존성 설치 결과를 확인함 |
| 보고서 검증 실패 | 생성 결과의 12개 섹션 및 HTML 완성 여부를 확인함 |
| 푸시 충돌 | 동시 수정 여부와 푸시·리베이스 로그를 확인함 |
| 생성 성공 후 사이트 미반영 | 최신 Pages 배포 결과와 브라우저 캐시를 확인함 |
| 화면 날짜만 최신으로 보임 | 현재 날짜 표시와 실제 데이터 기준일을 구분하여 확인함 |

문의·수정 요청 시 **실패한 실행의 URL과 실패 단계명**을 함께 기록하면 원인 확인에 도움이 됨. 비밀번호·토큰·API 키는 로그나 이슈에 기재하지 않음.

## 향후 개선 과제

- 공식 기관의 API·RSS·원문을 활용한 실제 자료 수집 구현
- 각 자료의 제목·기관명·발행일·수집일·원문 URL 기록
- 고정 수치와 난수 환율 차트를 실제 관측 데이터로 교체
- 수집 실패 시 마지막 성공 데이터와 해당 기준일 표시
- 수치·단위·기준기간 및 출처 링크 검증 추가
- 웹 화면에서 예시 데이터와 실제 수집 데이터를 구분하여 표시
- 사용하지 않는 과거 생성기·백업·캐시 파일 정리
