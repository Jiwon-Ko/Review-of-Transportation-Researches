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


| 번호        | 원문 수식 (notation 유지)                                                                      | 의미 (해석)                                                                               |
| --------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| (2)       | $\sum_{i \in S} s_{ip} = 1 - q_p \quad \forall p \in P$                                  | 각 parcel $p$는 정확히 하나의 출발 APL에서 시작 (단, 백업 배송 시 제외).                                    |
| (3)       | $\sum_{i \in D_p} d_{ip} = 1 - q_p \quad \forall p \in P$                                | 각 parcel $p$는 고객 후보 목적지 집합 중 하나에서 종료 (백업 시 제외).                                       |
| (4)       | $\sum_{j:(i,j)\in A_k} x_{pij}^k - \sum_{j:(j,i)\in A_k} x_{pji}^k = s_{ip} - d_{ip}$    | crowdshipper $k$의 경로상 flow balance: 출발역에서는 outflow=1, 목적역에서는 inflow=1, 중간역에서는 in=out. |
| (5)       | $e_i \ge s_{ip} \quad \forall i \in S, p \in P$                                          | 어떤 parcel이라도 source $i$에서 시작하면 해당 역은 활성화.                                             |
| (6)       | $x_{pij}^k \le y_{kp} \quad \forall (i,j)\in A_k, p, k$                                  | arc $(i,j)$로 parcel $p$를 이동시키려면 crowdshipper $k$가 해당 parcel에 할당되어야 함.                 |
| (7)       | $\sum_{p \in P} y_{kp} \le 1 \quad \forall k \in K$                                      | crowdshipper는 최대 한 개 parcel만 처리 가능.                                                   |
| (8)       | $\sum_{j:(i,j)\in A_k} x_{pij}^k \le l_{ipt}$                                            | 시간 $t$에 parcel이 역 $i$를 떠날 경우에만 arc를 사용할 수 있음.                                         |
| (9)       | $a_{ipt} = 1 \quad \text{if parcel } p \text{ arrives at station } i \text{ at time } t$ | parcel은 같은 시간대에 동일 역에 한 번만 도착 가능.                                                     |
| (10)      | $a_{ipt}=1 \Rightarrow o_{ip(t+1)}=1$                                                    | parcel이 시간 $t$에 도착하면 다음 슬롯 $t+1$에서 해당 역에 위치.                                          |
| (11)      | $o_{ip(t+1)}=1 \;\text{if } o_{ipt}=1, l_{ipt}=0$                                        | parcel이 시간 $t$에 역 $i$에 있었고 떠나지 않았다면 $t+1$에도 같은 역에 남음.                                 |
| (12)      | $l_{ipt}=1 \Rightarrow o_{ip(t+1)}=0$                                                    | parcel이 시간 $t$에 역 $i$를 떠나면 $t+1$에는 그 역에 존재하지 않음.                                      |
| (13)      | $\sum_{i \in N} o_{ipt} \le 1 - q_p \quad \forall p, t$                                  | parcel은 매 시간 슬롯마다 최대 1개 역에만 존재 (백업 시 네트워크 상 위치 X).                                    |
| (14)      | $\sum_{p \in P} (o_{ipt} + a_{ipt}) \le C_i \quad \forall i, t$                          | 각 역의 수용량 $C_i$ 제한.                                                                    |
| (15)      | $o_{ip1} = s_{ip} \quad \forall i \in S, p \in P$                                        | 초기 시점(시간 슬롯 1)에서 parcel은 출발역에 위치.                                                     |
| (16)–(22) | $s_{ip}, d_{ip}, q_p, e_i, a_{ipt}, l_{ipt}, o_{ipt}, x_{pij}^k, y_{kp} \in \{0,1\}$     | 주요 의사결정 변수들의 이진 조건.                                                                   |
| (23)      | 모든 변수 $\ge 0$                                                                            | 비음수 제약.                                                                               |

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

## 📝 개선점?
- 보행자 방향을 왼쪽, 오른쪽으로만 설정했다면 중간에 빠져나가는건 구현을 못한걸까?
- 드론처럼 중간에 빠져나가는걸로 네트워크를 구현을 하게 된다면?

[⬅️ 목록으로 돌아가기](../README.md)
