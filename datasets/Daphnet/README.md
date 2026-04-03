## 📊 Daphnet Freezing of Gait Dataset (FOG)

### 🧠 Overview

이 데이터셋은 파킨슨병 환자의 보행 데이터를 기반으로  
**Freezing of Gait (FOG, 보행 멈춤 현상)**을 탐지하기 위해 수집된 데이터입니다.

본 프로젝트에서는 해당 데이터를 활용하여  
**정상 보행 vs 이상 보행(FOG)** 을 분류하는 LSTM 모델을 구축합니다.

---

### 📁 Dataset Structure

각 `.txt` 파일은 하나의 실험 세션을 의미합니다.  
(예: `S01R01.txt`, `S02R01.txt` 등)

각 행(row)은 하나의 시간 스텝(time step) 데이터를 나타냅니다.

[time, ankle_x, ankle_y, ankle_z, thigh_x, thigh_y, thigh_z, trunk_x, trunk_y, trunk_z, label]

---

### 🧾 Columns Description

| Index | Description |
|------|------------|
| 0 | Timestamp (ms) |
| 1~3 | Ankle accelerometer (x, y, z) |
| 4~6 | Thigh accelerometer (x, y, z) |
| 7~9 | Trunk accelerometer (x, y, z) |
| 10 | Label |

---

### 🏷️ Label Definition

| Value | Meaning |
|------|--------|
| 0 | Not part of experiment (ignore) |
| 1 | Normal walking |
| 2 | Freezing of Gait (FOG) |

---

### ⚙️ Preprocessing

모델 학습을 위해 다음 전처리를 수행합니다.

#### 1. 불필요 데이터 제거
label == 0 제거

#### 2. Binary Classification 변환

0 → Normal

1 → Abnormal (FOG)

```
```python
df = df[df.iloc[:, -1] != 0]
df["label"] = df.iloc[:, -1].apply(lambda x: 1 if x == 2 else 0)
```

📊 Data Characteristics
	•	시계열 데이터 (Time-Series)
	•	IMU 센서 기반 데이터
	•	Class imbalance 존재 (정상 > 이상)

⸻

⚠️ Important Considerations

1. Class Imbalance
FOG 데이터가 상대적으로 적기 때문에
모델 학습 시 class weight 적용이 필요합니다.

2. Subject Dependency
환자별 보행 패턴이 다르므로
train/test를 사람 기준으로 분리해야 합니다.

⸻

🚀 Usage in This Project

본 프로젝트에서는:
	•	Daphnet → 이상 보행 데이터
	•	WISDM / 자체 수집 → 정상 보행 데이터

를 결합하여

👉 정상 vs 이상 보행 분류 모델을 구축합니다.

⸻

🧪 Model Pipeline
	1.	데이터 전처리
	2.	Sliding Window 적용
	3.	LSTM 모델 학습
	4.	이상 보행(FOG) 탐지
