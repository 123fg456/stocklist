# 국내 주식 수급 분석 — 검증 우선 프로토타입

이 버전은 **비공식 pykrx의 실시간 정상 동작을 보장하지 않습니다**. 데이터 조회 실패 시 추천 종목을 만들지 않습니다.

## 실행

```bash
pip install -r requirements.txt
python analyze.py --limit 100
```

- `--limit 100`은 첫 100개 종목만 시도하므로 **전체 시장 TOP 10이 아닙니다**.
- 전체 시도: `python analyze.py --limit 0` (상당한 시간이 걸리고 차단될 수 있음).
- 결과: `report.json`, 표시: `index.html` (동일 디렉터리에서 웹서버로 열기).
- 120거래일 미만 또는 마지막 거래일 불일치 종목은 제외됩니다.
- 우선주 제외는 이름 패턴 기반이며 완전하지 않습니다. 스팩·ETF 등 분류도 추가 보강 필요합니다.
- 수급 점수는 시험용이며 펀더멘털/기술/텐배거 점수는 **구현하지 않았습니다**.
- 공식 확정 여부는 원본 거래일과 항목 확인만으로 증명되지 않습니다. 확정 데이터 확인은 별도 필요합니다.

## GitHub 모바일 배포

GitHub 저장소 루트에 이 폴더 안의 파일과 `.github/workflows/daily.yml`을 **경로 그대로** 올립니다. GitHub Pages의 `Deploy from a branch` / `main` / `/ (root)`를 선택합니다. Actions 탭에서 `Daily flow analysis`를 수동 실행해 보고 `report.json`의 상태와 실패 원인을 확인합니다. GitHub Actions 무료 사용량·권한·예약 실행 지연은 계정 설정에 따라 다릅니다.

**주의:** GitHub 웹 업로드는 숨김 폴더 경로를 유지하기 어려울 수 있습니다. 이 경우 웹 UI에서 `.github/workflows/daily.yml` 파일을 직접 생성하거나 PC의 git을 사용해야 합니다.

## 보안·법적 유의

증권계좌 인증이나 API 키가 없습니다. KRX 웹페이지의 비공식 접근 방식은 변경되거나 서비스 정책상 제한될 수 있습니다. 요청을 대량으로 보내기 전에 이용약관과 허용 범위를 확인하세요.
