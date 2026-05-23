# STONKS - TSLL 주가 예측 & 스윙매매 수익 극대화 프로젝트

## 프로젝트 한줄 요약
TSLL(테슬라 2배 레버리지 ETF)의 다음날 예상 고가/저가를 AI로 예측하여,
최저가 매수 → 최고가 매도 스윙전략으로 $100,000 시드로 연간 수익 극대화

## 실행 환경
- **Google Colab** (T4 GPU 무료 사용)
- Python 3.10+
- 별도 설치 불필요 — 각 노트북 첫 셀에서 pip install 자동 처리

## 노트북 실행 순서
| 순서 | 파일명 | 내용 |
|------|--------|------|
| 1 | `notebooks/01_data_collection_eda.ipynb` | 데이터 수집 + 탐색적 분석 |
| 2 | `notebooks/02_feature_engineering.ipynb` | 기술적 지표 생성 |
| 3 | `notebooks/03_models_arima_prophet.ipynb` | ARIMA / Prophet 학습 |
| 4 | `notebooks/04_models_xgboost_lstm.ipynb` | XGBoost / LSTM 학습 |
| 5 | `notebooks/05_model_tft.ipynb` | Temporal Fusion Transformer |
| 6 | `notebooks/06_backtest_comparison.ipynb` | 백테스트 + 수익률 비교 |
| 7 | `notebooks/07_final_prediction.ipynb` | 최종 모델로 2026~ 예측 |

## 핵심 전략
```
예측 고가/저가 → 매수/매도 주문 설정 → 스윙매매 시뮬레이션 → 연간 수익률 계산
```

## 폴더 구조
```
STONKS/
├── README.md
├── RULES.md
├── data/
│   ├── raw/          ← yfinance 원본 데이터 (.csv)
│   └── processed/    ← 기술지표 포함 전처리 데이터 (.csv)
├── models/           ← 학습된 모델 저장 (.pkl, .h5)
├── notebooks/        ← Jupyter 노트북 (Colab에서 실행)
├── results/          ← 백테스트 결과, 수익률 차트
└── history/          ← 세션 진행 기록
```
