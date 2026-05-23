# Session 001 - 프로젝트 초기화 및 전체 골조 완성

**날짜**: 2026-05-23  
**단계**: 프로젝트 설정 + 노트북 1~4, 6, 7번 생성

## 핵심 결정사항
- 종목: TSLL (Direxion Daily TSLA Bull 2X Shares ETF)
- 전략: 스윙매매 (예측 최저/최고가 기반)
- 시드: $100,000
- 평가: 1년 백테스트 수익률 기준 모델 선정
- 환경: Google Colab (T4 GPU 무료)
- 제출: 발표/시연 형식

## TSLL 특이사항 (중요!)
- 테슬라 2배 레버리지 ETF → 변동성 극히 높음
- 상장일: 2022년 8월 9일 → 데이터 3년치 밖에 없음
- 레버리지 ETF 특성상 "변동성 감소(Volatility Decay)" 존재
- TSLA 데이터를 피처로 활용 (상관계수 0.97+)

## 완성된 노트북 목록
| 번호 | 파일 | 내용 | 상태 |
|------|------|------|------|
| 01 | 01_data_collection_eda.ipynb | 데이터 수집 + EDA | 완성 |
| 02 | 02_feature_engineering.ipynb | 기술지표 + 피처 생성 | 완성 |
| 03 | 03_models_arima_prophet.ipynb | ARIMA + Prophet 베이스라인 | 완성 |
| 04 | 04_models_xgboost_lstm.ipynb | XGBoost + LSTM | 완성 |
| 05 | 05_model_tft.ipynb | TFT (미완성) | 다음 세션 |
| 06 | 06_backtest_comparison.ipynb | 백테스트 + 수익률 비교 | 완성 |
| 07 | 07_final_prediction.ipynb | 최종 예측 | 완성 |

## 다음 세션에서 할 것
1. 05_model_tft.ipynb (Temporal Fusion Transformer) 작성
2. Colab 실행 테스트
3. 개선사항: 포지션 사이징 로직 고도화
4. 개선사항: 05번 없어도 발표 가능 — 4개 모델로 충분

## 기술 스택
- yfinance: 데이터 수집
- pandas-ta: 기술지표 계산
- pmdarima: ARIMA 자동 파라미터 탐색
- prophet: Meta 시계열 예측
- xgboost: 그래디언트 부스팅
- tensorflow/keras: LSTM 딥러닝
- sklearn: 전처리 + 평가
