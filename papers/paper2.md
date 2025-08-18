# A learning based pedestrian flow prediction approach with diffusion behavior

- 📅 연도: 2025
- ✍️ 저자: Weiming Mai et al.
- 🏫 학회/저널: Transportation Research Part C

---

## 🔑 핵심 기여 (Key Contributions)
1. 보행 흐름 예측 문제를 그래프 기반 학습 문제로 정의
  - 센서 네트워크를 directed graph로 모델링하여, 보행 흐름 예측을 체계적으로 수행
2. Diffusion behavior 기반 학습 모델 제안
  - 보행자의 이동이 단순한 시계열 변화가 아니라 공간-시간적으로 확산되는 특성임을 반영.
3. 실제 데이터에서 성능 입증
  - 기존 방법보다 높은 정확도와 일반화 성능을 보여, 실무 적용 가능성을 검증.

* 기존 연구들은 보행자 흐름 예측 문제에서 단순 시계열 모델 또는 **graph convolution (GCN류)**을 주로 사용
* “Diffusion process”라는 개념은 본인이 처음 제시한 것이 아님.
* 하지만 보행자 흐름 예측(pedestrian flow prediction)이라는 도메인에 diffusion behavior를 적용

---

## 🧩 연구 방법 (Methodology)
- 사용한 데이터셋: 실제 건물 내부 센서 데이터를 수집
- 알고리즘/모델:
  1. 그래프 기반 모델링 (Graph Construction) : 각 센서를 **노드(node), **유향 엣지(edge)**는 보행자가 실제 이동 가능한 경로(상류 → 하류), 
  2. Diffusion Behavior 반영 (Core Idea) : 기존 GCN류 모델은 공간적 상관성만 고려하지만, 저자는 보행 흐름을 “확산(diffusion)” 현상으로 정의
  3. 학습 모델 설계 (Learning-based Prediction Model)
     3.1 Diffusion Graph Convolution Layer
     - 보행 흐름이 네트워크에서 방향성과 전이 확률을 따라 전파됨을 반영.
     - 기존 GCN은 정적 adjacency matrix를 쓰지만, 여기서는 확산 행렬(diffusion matrix)을 활용.
     3.2 emporal Learning Layer
     - 시계열적 의존성을 반영하기 위해 RNN/LSTM/GRU류 모듈과 결합.
     - 즉, 시공간(spatio-temporal) 특성을 동시에 모델링.
     3.3 Output Layer
     - 다운스트림 노드의 미래 흐름을 $M$ step 동안 예측.
- 실험 설정: OOD 시나리오(out-of-distribution) 실험도 포함

---

## 📊 결과 (Results)
- 평가 지표: RMSE, MAE, MAPE 등 오차 기반 지표.
- 비교 기준 (Baseline) 대비: 전통적 시계열 모델 (ARIMA, LSTM 등), 기존 GCN류 모델 (ST-GCN, DCRNN 등)과 비교
- 결과 : 저자들의 diffusion 기반 학습 모델이 기존 시계열·GCN류 모델보다 예측 정확도와 일반화 성능이 우수. 특히 **새로운 상황(OOD)**에서 성능 저하가 덜함 → 실사용 가능성 높음.

---

## 📝 한줄 요약
👉 건물이나 대형 인프라 내부에서 보행자 흐름(pedestrian flow)을 미래 시점까지 예측
👉 (1) 센서 네트워크를 그래프로 모델링, (2) 보행 흐름을 확산 과정으로 정의, (3) diffusion graph convolution + temporal learning을 결합한 모델을 학습

---

[⬅️ 목록으로 돌아가기](../README.md)
