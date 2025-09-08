# Optimizing last-mile delivery through crowdshipping on public transportation networks

- 📅 연도: 2025  
- ✍️ 저자: Mikele Gajda, Olivier Gallay, Renata Mansini, Filippo Ranza  
- 🏫 학회/저널: *Transportation Research Part C*, Vol.179, 105250

---

## 🔑 핵심 기여 (Key Contributions)
1. **PTCP (Public Transportation-based Crowdshipping Problem) 정식화**  
   - 대중교통망·통근자·보관함(APL)·백업서비스를 통합한 라스트마일 최적화 문제 정의.
2. **MILP + Valid Inequalities 제안**  
   - MILP 수식으로 문제를 모델링하고, 유효 부등식으로 해공간을 타이트하게 하여 연산 성능 향상.
3. **ALNS 휴리스틱 설계**  
   - ISA 프레임워크 안에서 ALNS(룰렛 선택·SA 수용·리히팅 포함) 구현 → 대규모 인스턴스에서 근사 최적해 탐색.
4. **실험으로 성능 입증**  
   - 소규모 인스턴스: MILP로 최적해 확인  
   - 대규모 인스턴스: ALNS로 빠른 계산 + 최적에 근접한 결과

---

## 🧩 연구 방법 (Methodology)

### 문제 세팅
- 배송사는 아침에 선택된 PT 역(APL)에 소포를 배치.  
- 통근자는 본인 동선 내에서 소포를 픽업·전달.  
- 배송이 끝나지 못하면 **백업 서비스**가 투입.  
- **목표**: 총 비용 최소화.

### 모델/알고리즘
1. **MILP 정식화**
   - 변수: \(s_{ip}, d_{ip}, q_p, e_i, y_{kp}, x_{pij}^k, a_{ipt}, l_{ipt}, o_{ipt}\)
   - 비용: 보상(ρ), 소스활성(ν), 적재(σ), 백업(γ)
   - 제약: 출발/도착 선택, 유량 보존, 스테이션 활성화, 시간 슬롯 기반 도착/출발/위치, 용량 제약
   - (24)–(30) valid inequalities 추가 → 연산 성능 개선
2. **ALNS (Algorithm 1)**
   - Destroy operators (D1: 소포 제거, D2: 경로 절단)
   - Repair operators (R1: greedy, R2: random)
   - 연산자 선택: 룰렛휠 + 적응 가중치 업데이트
   - 수용 기준: Simulated Annealing (나쁜 해도 확률적으로 수용), 리히팅 포함
   - 종료 조건: 시간 제한 or 개선 없음

---

## 🧮 핵심 제약 요약 (notation 유지)

| 번호 | 원문 수식 | 의미 |
|---|---|---|
| (2) | \(\sum_{i \in S} s_{ip} = 1 - q_p \) | 각 소포는 정확히 하나의 출발 APL에서 시작 (백업이면 제외). |
| (3) | \(\sum_{i \in D_p} d_{ip} = 1 - q_p \) | 각 소포는 후보 목적지 중 하나에서 종료 (백업이면 제외). |
| (4) | \(\sum_{j} x_{pij}^k - \sum_{j} x_{pji}^k = s_{ip} - d_{ip}\) | crowdshipper 경로상의 flow balance. |
| (5) | \(e_i \ge s_{ip}\) | 소스역이 사용되면 활성화. |
| (6) | \(x_{pij}^k \le y_{kp}\) | arc 사용 시 crowdshipper 할당 필요. |
| (7) | \(\sum_{p} y_{kp} \le 1\) | crowdshipper는 최대 1개 소포만 운반. |
| (8)–(15) | \(a,o,l\) 연계 | 도착→점유, 출발→비점유, 초기 점유=출발 선택 등 시간 슬롯 제약. |
| (16)–(23) | 변수 도메인 | 이진/비음수 조건. |
| (24)–(30) | Valid inequalities | 출발/도착/백업/할당 간 논리적 관계 강화. |

---

## 📊 결과 (Results)
- **CPLEX(+valid inequalities) vs. ALNS** 비교  
  - 소규모 14개 인스턴스 중 7개에서 ALNS가 최적해 달성  
  - 나머지 대부분에서도 갭 < 1%  
- 실행시간: ALNS가 훨씬 빠름  
- 최적 ALNS 파라미터 설정: 냉각률 0.75–0.9, 시간제한 600초에서 성능 최적화

---

## 📝 Discussion
- **의의**: 기존 연구의 공백(출발/도착/백업/환승 고려)을 채운 통합 모델 제안  
- **MILP**: 정확해 기준 제공 (benchmark)  
- **ALNS**: 대규모 실용 가능성 입증  
- **향후 연구**:  
  - 확률적/강건 모델 확장 (수요/시간 불확실성)  
  - 보상 정책 설계 다양화 (현금, 교통 크레딧 등)  
  - APL 입지 재설계와의 공동최적화  

---

## 📝 한줄 요약
👉 “통근자+대중교통+보관함+백업”을 하나의 프레임으로 묶고, MILP(정확해)와 ALNS(근사해)로 **라스트마일 배송 최적화**를 구현.



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

