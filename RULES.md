# STONKS 프로젝트 룰북

## 진행 규칙
1. 뭘 하던지간에 설명을 무조건 해줘야 함
2. 계속 만들어주면서 부족해보이는 부분 있으면 개선사항 알려주거나 해결방안 추천해준다
3. Claude Projects/STONKS 폴더를 만들어 그 내부에서 모든 작업 처리한다
4. 폴더 내의 /STONKS/history 폴더를 만들어 핵심 포인트, 진행 상황 세션별로 저장한다. 토큰이 90%에 도달하면 저장한다. (불가능하다면 큰 변화나 발전 이후 저장)
5. 세션에서 파일 수정/추가가 발생한 경우, 세션 종료 전에 변경사항을 GitHub에 PR로 올린다.
   - PR 제목: `[세션번호] 핵심 작업 한 줄 요약` (예: `[Session 003] 버그 수정 및 Drive 마운트 추가`)
   - PR 본문: 변경된 파일 목록, 주요 변경 내용, 다음 세션 TODO 포함
   - Colab에서 GitHub 연동 사용 (`파일 → GitHub에 사본 저장`)하면 매번 수동 업로드 불필요

## 프로젝트 개요
- **목표**: TSLL 주가 예측 모델 구축 및 스윙매매 수익 극대화
- **종목**: TSLL (Direxion Daily TSLA Bull 2X Shares - 테슬라 2배 레버리지 ETF)
- **학습 데이터**: 2025~2026 일별 가격 데이터
- **예측 대상**: 2026~ 일별 예상 최저가 / 최고가
- **시드머니**: $100,000 USD
- **전략**: 스윙매매 - 예측 최저가 근처 매수, 예측 최고가 근처 매도
- **평가 기준**: 1년 수익률 기준 최고 성능 모델 선정

## 프로젝트 폴더 구조
```
STONKS/
├── RULES.md              ← 이 파일
├── README.md             ← 프로젝트 설명
├── data/
│   ├── raw/              ← yfinance 등에서 가져온 원본 데이터
│   └── processed/        ← 전처리된 데이터
├── models/               ← 각 모델 코드
├── notebooks/            ← Jupyter 노트북
├── results/              ← 백테스트 결과, 수익률 비교
└── history/              ← 세션별 진행 상황 기록
```

## 후보 모델 (비교 후 최고 성능 선정)
- LSTM (Long Short-Term Memory)
- Prophet (Meta/Facebook)
- ARIMA / SARIMA
- XGBoost
- Transformer (Temporal Fusion Transformer)
- 앙상블

## GitHub API 인코딩 규칙 (필수)
> GitHub API로 한글 텍스트 전송 시 반드시 아래 방식을 사용한다.

PowerShell에서 한글이 깨지는 원인: `ConvertTo-Json`이 한글을 `\uXXXX`로 이스케이프 처리함.

**올바른 방법 — UTF-8 바이트 직접 전송:**
```powershell
# JSON 생성 후 UTF-8 바이트로 변환해서 전송
$bodyJson = @{ title = "한글제목"; body = "한글내용" } | ConvertTo-Json -Depth 10 -Compress
$bodyBytes = [System.Text.Encoding]::UTF8.GetBytes($bodyJson)

Invoke-RestMethod -Uri $url -Method Post `
    -Body $bodyBytes `
    -Headers @{ Authorization = "token $TOKEN" } `
    -ContentType "application/json; charset=utf-8"
```

**절대 사용 금지:**
```powershell
# 이 방식은 한글 깨짐 발생
Invoke-RestMethod -Uri $url -Body ($obj | ConvertTo-Json) ...
```

## 업데이트 이력
- 2026-05-23: 프로젝트 초기 설정
- 2026-05-23: GitHub PR 업로드 규칙 추가
- 2026-05-23: GitHub API 한글 인코딩 규칙 추가 (UTF-8 바이트 직접 전송)
