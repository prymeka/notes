# Academic reading list for rigorous RL foundations

A Machine Learning Engineer seeking deep understanding of reinforcement learning should follow this progression from Bellman's foundational mathematics through modern deep RL algorithms. The **10 core papers** below provide complete coverage of MDPs, value functions, Q-learning, temporal difference methods, policy gradients, and the key innovations that enabled deep reinforcement learning. All papers except one are freely accessible.

## Part I: Theoretical foundations

### 1. Sutton & Barto — The canonical textbook (freely available)

**Citation:** Sutton, R.S. & Barto, A.G. (2018). *Reinforcement Learning: An Introduction*, 2nd Edition. MIT Press.

**Free PDF:** http://incompleteideas.net/book/RLbook2020.pdf

This textbook is essential reading before diving into papers. Chapters 1-6 establish the mathematical framework: **MDPs**, **Bellman equations**, **value functions V(s) and Q(s,a)**, **dynamic programming**, **Monte Carlo methods**, and **temporal difference learning**. Chapter 6 specifically clarifies the **on-policy vs off-policy** distinction through the famous cliff-walking example (SARSA vs Q-learning). Chapters 8-9 cover **model-based vs model-free** approaches. The second edition includes modern deep RL developments. Read this first—it will make every subsequent paper far more accessible.

---

### 2. Sutton (1988) — Temporal difference learning

**Citation:** Sutton, R.S. (1988). "Learning to Predict by the Methods of Temporal Differences." *Machine Learning*, 3(1), 9-44.

**Free PDF:** http://incompleteideas.net/papers/sutton-88-with-erratum.pdf

**Concepts covered:** TD(λ), eligibility traces, bootstrapping, convergence proofs

This paper introduced **temporal difference learning**—the core mechanism underlying nearly all RL algorithms. TD methods learn from incomplete sequences by "bootstrapping" (updating estimates based on other estimates), bridging Monte Carlo and dynamic programming approaches. The mathematical treatment proves convergence under specific conditions. Understanding TD is prerequisite to understanding Q-learning, SARSA, and all actor-critic methods.

---

### 3. Watkins & Dayan (1992) — Q-learning convergence

**Citation:** Watkins, C.J.C.H. & Dayan, P. (1992). "Q-learning." *Machine Learning*, 8(3-4), 279-292.

**Free PDF:** https://link.springer.com/content/pdf/10.1007/BF00992698.pdf

**Concepts covered:** Q-values, off-policy learning, model-free control, convergence proof

The foundational **Q-learning** paper provides a rigorous convergence proof showing that Q-values converge to optimal action-values with probability 1 under appropriate conditions. Q-learning is **model-free** (learns directly from transitions without building an environment model) and **off-policy** (learns about the optimal policy while following an exploratory policy). This paper establishes the theoretical basis for DQN and all subsequent value-based deep RL.

---

### 4. Sutton et al. (2000) — Policy gradient theorem

**Citation:** Sutton, R.S., McAllester, D., Singh, S. & Mansour, Y. (2000). "Policy Gradient Methods for Reinforcement Learning with Function Approximation." *Advances in Neural Information Processing Systems 12 (NeurIPS 1999)*, 1057-1063.

**Free PDF:** https://papers.nips.cc/paper/1999/file/464d828b85b0bed98e80ade0a5c43b0f-Paper.pdf

**Concepts covered:** Policy gradient theorem, actor-critic foundations, compatible function approximation

This paper proves the **policy gradient theorem**: ∇J(π) = E[∇log π(a|s) · Q(s,a)]. The crucial insight is that the gradient does not depend on the derivative of the state distribution—a non-obvious result enabling practical policy optimization. This theorem underlies REINFORCE, A3C, TRPO, and PPO. The paper also establishes when function approximation for critics is "compatible" with unbiased gradient estimates.

---

## Part II: Deep reinforcement learning landmarks

### 5. Mnih et al. (2015) — Deep Q-Networks

**Citation:** Mnih, V., Kavukcuoglu, K., Silver, D., et al. (2015). "Human-level Control through Deep Reinforcement Learning." *Nature*, 518(7540), 529-533.

**ArXiv version:** https://arxiv.org/abs/1312.5602 (2013 preprint)

**Concepts covered:** DQN, experience replay, target networks, end-to-end learning from pixels

The paper that launched deep RL. **DQN** combines Q-learning with deep neural networks, introducing two critical innovations: **experience replay** (storing transitions and sampling randomly to break correlations) and **target networks** (separate network for stable TD targets, updated periodically). These techniques solved the notorious instability of combining neural networks with TD learning. DQN achieved human-level performance on 49 Atari games learning directly from pixels—demonstrating that deep learning could scale RL to high-dimensional state spaces.

---

### 6. van Hasselt et al. (2016) — Double DQN

**Citation:** van Hasselt, H., Guez, A. & Silver, D. (2016). "Deep Reinforcement Learning with Double Q-learning." *Proceedings of AAAI-16*, 2094-2100.

**ArXiv:** https://arxiv.org/abs/1509.06461

**Concepts covered:** Maximization bias, overestimation in Q-learning, decoupled action selection/evaluation

This paper identifies and solves a fundamental problem: standard Q-learning systematically **overestimates Q-values** due to using the max operator for both action selection and evaluation. Double DQN uses the online network to select actions but the target network to evaluate them. This minimal modification significantly improves performance and became standard practice. Understanding why overestimation occurs requires understanding the statistical properties of the Bellman operator.

---

### 7. Mnih et al. (2016) — A3C and asynchronous methods

**Citation:** Mnih, V., Badia, A.P., Mirza, M., et al. (2016). "Asynchronous Methods for Deep Reinforcement Learning." *Proceedings of ICML 2016*, PMLR 48:1928-1937.

**ArXiv:** https://arxiv.org/abs/1602.01783

**Concepts covered:** Actor-critic architecture, advantage functions, parallel training, on-policy deep RL

**A3C** (Asynchronous Advantage Actor-Critic) demonstrated that parallelism can replace experience replay for stabilizing deep RL training. Multiple actors interact with separate environment copies, sending asynchronous gradient updates to shared parameters. This paper established actor-critic as a viable deep RL paradigm and introduced the **advantage function** A(s,a) = Q(s,a) - V(s) for variance reduction. A3C is **on-policy** and **model-free**, contrasting with the off-policy DQN family.

---

### 8. Schulman et al. (2017) — Proximal Policy Optimization

**Citation:** Schulman, J., Wolski, F., Dhariwal, P., Radford, A. & Klimov, O. (2017). "Proximal Policy Optimization Algorithms." arXiv:1707.06347.

**ArXiv:** https://arxiv.org/abs/1707.06347

**Concepts covered:** Clipped surrogate objective, trust regions, policy optimization, on-policy learning

**PPO** has become the default algorithm for many applications due to its simplicity and robustness. It constrains policy updates using a clipped objective function—a simpler alternative to TRPO's KL-divergence constraint. The algorithm allows multiple epochs of minibatch updates per data collection phase, improving sample efficiency. PPO is **on-policy** and **model-free**. This paper is essential reading for anyone working with RLHF (Reinforcement Learning from Human Feedback), as PPO is the standard algorithm for training language models from human preferences.

---

### 9. Haarnoja et al. (2018) — Soft Actor-Critic

**Citation:** Haarnoja, T., Zhou, A., Abbeel, P. & Levine, S. (2018). "Soft Actor-Critic: Off-Policy Maximum Entropy Deep Reinforcement Learning with a Stochastic Actor." *Proceedings of ICML 2018*, PMLR 80:1861-1870.

**ArXiv:** https://arxiv.org/abs/1801.01290

**Concepts covered:** Maximum entropy RL, off-policy actor-critic, stochastic policies, continuous control

**SAC** represents the current state-of-the-art for continuous control tasks. It maximizes a combined objective of reward and policy entropy, encouraging exploration while maintaining off-policy learning efficiency. Key innovations include twin Q-networks (mitigating overestimation) and automatic temperature tuning. SAC is **off-policy** (using experience replay) and **model-free**, combining the sample efficiency of off-policy methods with the stability of entropy regularization. Essential for robotics applications.

---

### 10. Hessel et al. (2018) — Rainbow

**Citation:** Hessel, M., Modayil, J., van Hasselt, H., et al. (2018). "Rainbow: Combining Improvements in Deep Reinforcement Learning." *Proceedings of AAAI-18*.

**ArXiv:** https://arxiv.org/abs/1710.02298

**Concepts covered:** Integration of DQN improvements, ablation studies, distributional RL, multi-step learning

**Rainbow** systematically combines six DQN extensions: Double DQN, Prioritized Experience Replay, Dueling Networks, Multi-step Learning, Distributional RL (C51), and Noisy Networks. The paper's ablation study reveals which components provide the largest improvements and whether they are complementary or redundant. This is the definitive synthesis paper for value-based deep RL, demonstrating what a fully-optimized **off-policy, model-free** algorithm can achieve.

---

## Supplementary reading for deeper understanding

| Paper | Year | Why Include |
|-------|------|-------------|
| Bellman, *Dynamic Programming* (Dover reprint) | 1957 | Origin of Bellman equations; Chapter 3 essential |
| Kaelbling et al., "RL: A Survey" (*JAIR*) | 1996 | Historical context, classical framing |
| Schulman et al., "Trust Region Policy Optimization" (*ICML*) | 2015 | Theoretical foundation for PPO |
| Lillicrap et al., "DDPG" (*ICLR*) | 2016 | Bridges DQN to continuous actions |

---

## Recommended reading order

**Week 1-2:** Sutton & Barto Chapters 1-6, then Sutton (1988) TD paper

**Week 3:** Watkins & Dayan (1992), then Sutton & Barto Chapters 8-9

**Week 4:** Sutton et al. (2000) policy gradients, then A3C paper

**Week 5:** DQN → Double DQN → Rainbow progression

**Week 6:** PPO and SAC papers

This ordering builds mathematical intuition before introducing neural network complications, then traces both the value-based (DQN family) and policy-based (PPO/SAC) branches of modern deep RL.