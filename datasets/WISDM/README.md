WISDM Dataset (IMU 기반 보행 데이터) 사용 가이드

📌 개요

WISDM (Wireless Sensor Data Mining) Dataset은 스마트폰의 가속도 센서를 활용하여 수집된 인간 활동 데이터셋으로, 보행 분석 및 시계열 기반 인공지능 모델 학습에 활용된다.

본 프로젝트에서는 해당 데이터셋을 활용하여 보행 패턴을 분석하고, LSTM 기반 시계열 모델 학습을 수행한다.

⸻

📊 데이터 구성

1. Raw Dataset (사용 대상)

데이터 파일: WISDM_ar_v1.1_raw.txt

✔ 데이터 형식
```
[user],[activity],[timestamp],[x],[y],[z];
```