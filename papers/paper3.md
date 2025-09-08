Optimizing last-mile delivery through crowdshipping on public transportation networks

📅 연도: 2025

✍️ 저자: Mikele Gajda, Olivier Gallay, Renata Mansini, Filippo Ranza 

1-s2.0-S0968090X25002542-main

🏫 학회/저널: Transportation Research Part C, Vol.179, 105250 

1-s2.0-S0968090X25002542-main

🔑 핵심 기여 (Key Contributions)

PTCP(公共교통 기반 크라우드십핑 문제) 정식화

대중교통망·통근자·보관함(APL)·백업서비스를 통합한 라스트마일 최적화 문제로 정의. 

1-s2.0-S0968090X25002542-main

MILP + 유효부등식(valid inequalities) 제안

컴팩트 MILP를 제시하고, 해공간을 타이트하게 하는 부등식으로 연산 효율 개선. 

1-s2.0-S0968090X25002542-main

ALNS 휴리스틱 설계 및 성능 입증

ISA 프레임 안의 ALNS(룰렛 선택·SA 수용·리히팅 포함)로 대규모 인스턴스에서 근접 최적해를 빠르게 탐색. 

1-s2.0-S0968090X25002542-main

 

1-s2.0-S0968090X25002542-main

민감도·비교 실험

CPLEX(유효부등식 포함) vs. ALNS 비교: 여러 소형 인스턴스에서 ALNS가 최적 또는 <1% 갭을 다수 달성. 

1-s2.0-S0968090X25002542-main

🧩 연구 방법 (Methodology)

문제 세팅:

배송사는 아침에 선택된 PT 역(APL)에 소포를 배치 → 통근자가 본인 동선 내에서 픽업·전달 → 못 끝난 건 백업서비스로 최종 배송. 목표는 총비용 최소화. 

1-s2.0-S0968090X25002542-main

모형/알고리즘:

MILP 정식화(+ 유효부등식): 해공간 축소로 B&B 탐색 가속. 

1-s2.0-S0968090X25002542-main

ALNS (Algorithm 1):

연산자 선택: 파괴/수리 연산자를 룰렛휠로 선택(가중치 적응).

수용 기준: 비용이 나빠도 온도 
𝑇
T에 따른 확률로 수용(SA), 리히팅 정책 포함.

용량 감소 트릭: 이전 해 재생성 방지 위해 파괴 단계에서 임시로 노드 용량 축소 후 복원. 

1-s2.0-S0968090X25002542-main

🧮 (참고) 핵심 제약 요약 – notation 유지
번호	원문 수식 (요지)	해석
(2)	
∑
𝑖
∈
𝑆
𝑠
𝑖
𝑝
=
1
−
𝑞
𝑝
∑
i∈S
	​

s
ip
	​

=1−q
p
	​

	각 소포는 출발 APL 1곳 선택(백업이면 제외).
(3)	
∑
𝑖
∈
𝐷
𝑝
𝑑
𝑖
𝑝
=
1
−
𝑞
𝑝
∑
i∈D
p
	​

	​

d
ip
	​

=1−q
p
	​

	각 소포는 후보 목적 APL 1곳 선택(백업이면 제외).
(4)	
∑
𝑗
𝑥
𝑝
𝑖
𝑗
𝑘
−
∑
𝑗
𝑥
𝑝
𝑗
𝑖
𝑘
=
𝑠
𝑖
𝑝
−
𝑑
𝑖
𝑝
∑
j
	​

x
pij
k
	​

−∑
j
	​

x
pji
k
	​

=s
ip
	​

−d
ip
	​

	통근자 경로상의 유량 보존(출발=순유출1, 도착=순유입1).
(7)	
∑
𝑝
𝑦
𝑘
𝑝
≤
1
∑
p
	​

y
kp
	​

≤1	통근자 1인은 최대 1개 소포.
(9)–(15)	
𝑎
,
𝑜
,
𝑙
a,o,l 연결	도착→점유, 출발→비점유, 초기 점유=출발 선택 등 시간 슬롯 연계.

전체 수식(2)(23)·유효부등식(24)(30)은 앞서 정리한 표를 그대로 쓰시면 됩니다(요청 시 파일용 마크다운 제공 가능).

📊 결과 (Results)

CPLEX(+유효부등식) vs. ALNS 비교(소형 14개 인스턴스):

7개에서 ALNS가 최적값 도달, 나머지 다수는 갭 < 1%. 계산시간은 ALNS가 훨씬 유리. 

1-s2.0-S0968090X25002542-main

ALNS 설정: 인스턴스 패밀리별 최적 구성은 대체로 600초 시간 제한에서 최적. 

1-s2.0-S0968090X25002542-main

📝 한줄 요약

👉 “통근자+대중교통+보관함+백업”을 하나의 최적화 프레임으로 묶고, **MILP(정확해)**와 **ALNS(대규모 근접해)**로 실용 가능성을 입증한 라스트마일 모델. 

1-s2.0-S0968090X25002542-main

🛠️ 구현 팁 (실무로 옮길 때)

소형 인스턴스: Pyomo/OR-Tools로 MILP 구성 후 CPLEX/HiGHS/SCIP로 풀이 → 최적해/상한 확보.

대규모 인스턴스: 논문 Algorithm 1 구조로 ALNS 구현(룰렛 가중치·SA·리히팅·용량감소 트릭 포함). 

1-s2.0-S0968090X25002542-main

🧭 Related & 참고문헌(발췌)

PT 기반 crowdshipping 실증·모형 연구들(덴마크 파일럿, 메트로 기반 등) 요약 인용. 

1-s2.0-S0968090X25002542-main

 

1-s2.0-S0968090X25002542-main

ALNS 서베이·도시물류 2계층 문제 등 휴리스틱 레퍼런스. 

1-s2.0-S0968090X25002542-main

 

1-s2.0-S0968090X25002542-main

❓개선·열린 질문

다중 환승/시간 불확실성을 확률모형(robust/stochastic)로 확장하면 성능·신뢰성 어떻게 변할까?

**보상 정책(현금 vs. 교통크레딧)**과 참여율/순응도가 비용·서비스율에 미치는 한계효과는?

APL **입지 재설계(공동최적화)**와 연동하면 전체 사회적 비용/배출 저감이 더 커질까?


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

