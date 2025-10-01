# 📘 Monte Carlo (MC) 질문 정리 노트  

## ❓ MC Prediction과 Control은 뭐가 달라?
- **Prediction**: 주어진 정책 π가 얼마나 좋은지 평가하는 것. (V나 Q 추정)  
- **Control**: 최적 정책을 찾는 것. Q를 추정하고, 그걸로 정책을 개선(π ← greedy(Q))  
- -> Prediction = 평가, Control = 평가 + 개선  


## ❓ 왜 Control에서는 V가 아니라 Q를 구해?
- 최적 정책을 찾으려면 `argmax_a Q(s,a)`로 행동을 직접 고를 수 있어야 하기 때문.  
- V만 있으면 어떤 행동이 더 좋은지 직접 비교가 안 됨.  


## ❓ V와 Q의 관계는?
\[
v_\pi(s) = \sum_a \pi(a|s) \, q_\pi(s,a)
\]

- **Q(s,a)**: 상태 s에서 행동 a를 했을 때 기대 보상  
- **V(s)**: 정책 π에 따라 행동을 골랐을 때 평균 기대 보상  
- V는 Q의 확률적 평균값.  



## ❓ On-policy는 뭔데?
- 행동도 학습도 같은 정책 π를 따르는 방식.  
- 탐험 보장을 위해 **ε-soft 정책**을 사용 (모든 행동에 확률 조금씩 부여).  
- 해석:  
  - “이 상태에서는 A 행동을 90% 확률로, B 행동을 10% 확률로 하는 것이 최적이다.”  



## ❓ Off-policy는 왜 등장했어?
- On-policy는 탐험과 최적 정책을 동시에 만족시키려다 한계가 있음.  
- Off-policy의 발상: **탐험은 b, 학습은 π로 분리**  
  - b (behavior policy): 데이터를 모으는 정책 (탐험 위주, ε-greedy)  
  - π (target policy): 학습하고 싶은 정책 (greedy)  



## ❓ Importance Sampling에서 C와 W는 뭐야?
- **C(s,a)**: 지금까지 모은 가중치 합 (count 역할)  
- **W**: 이번 에피소드에서의 중요도 가중치 (π/b 확률 비율 누적)  
- 업데이트 식:
  \[
  Q \leftarrow Q + \frac{W}{C} (G - Q)
  \]
  - `(G - Q)`는 새 데이터(G)와 기존 평균(Q)의 차이 → 평균 업데이트 방식.  



## ❓ π랑 b는 둘 다 확률 분포야?
- **π**: 학습하고 싶은 목표 정책 (보통 greedy).  
- **b**: 데이터를 수집하는 행동 정책 (ε-greedy 같은 확률 분포).  
- 에피소드는 b로 만들고, 학습할 땐 π 기준으로 보정(W에 반영).  



## ❓ 결국 강화학습은 뭘 구하려는 거야?
- 한 문장: **상태마다 어떤 행동을 해야 장기적으로 가장 큰 보상을 받을까?**  
- 즉, 최적 정책 π*.  
- Reward, Return, V, Q, Policy… 전부 이걸 표현하는 다른 도구일 뿐.  



## ❓ Off-policy의 차별점은?
- On-policy: 행동=학습 (ε-soft)  
- Off-policy: 행동은 b(탐험), 학습은 π(목표 정책, 보통 greedy)  
- 연결: importance sampling (MC), max Q 타깃(Q-learning)  
