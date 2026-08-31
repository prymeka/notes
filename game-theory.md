# A curated path from game theory to SHAP explanations

For an ML engineer with physics training seeking to understand Shapley values—from their cooperative game theory origins to modern interpretability applications—this reading list provides **8 resources** organized in three stages. The progression builds intuition before formalism, then bridges theory to practice. **Six of eight resources are freely available online.**

## Stage 1: Cooperative game theory foundations

Your physics background means you'll appreciate how Shapley values emerge from symmetry principles and uniqueness proofs. Start here to build the conceptual vocabulary before tackling landmark papers.

### 1. Serrano's survey on cooperative games (entry point)

**Citation:** Roberto Serrano. "Cooperative Games: Core and Shapley Value." In *Encyclopedia of Complexity and Systems Science*, Springer, 2007. Also available as Brown University Economics Working Paper 2007-11.

This **20-page survey** is the ideal starting point—purpose-built for accessibility while maintaining rigor. Serrano covers the characteristic function representation, transferable utility games, the core, and the Shapley value with clear definitions and worked examples including parliamentary voting. The paper presents both Shapley's original 1953 axiomatization and Young's alternative 1985 characterization, giving you two complementary perspectives immediately.

**Why included:** Focused exclusively on cooperative games (exactly what Shapley values require), accessible length for rapid onboarding, covers all essential concepts.

**Accessibility:** ✅ FREE PDF at economics.brown.edu | **Difficulty:** Introductory-intermediate | **Time:** 2-3 hours

### 2. Osborne & Rubinstein textbook, Part IV (rigorous treatment)

**Citation:** Martin J. Osborne and Ariel Rubinstein. *A Course in Game Theory*. MIT Press, 1994. ISBN: 0-262-65040-1.

The standard graduate textbook for 30 years, with **~9,000+ citations** and an endorsement from Nobel laureate Robert Aumann noting its "recognition of cooperative theory's importance." Chapters 13-14 provide the full treatment of coalitional games: characteristic functions, the core, Shapley value proofs, the nucleolus, and bargaining solutions. The writing balances formalism with clarity, making it well-suited for physicists who appreciate precise notation but want motivated definitions.

**Why included:** Canonical reference that ML papers often cite; freely available; complete proofs you can verify.

**Accessibility:** ✅ FREE PDF (registration required) at books.osborne.economics.utoronto.ca | **Difficulty:** Graduate level | **Time:** 6-10 hours for Part IV

---

## Stage 2: Shapley value theory and axiomatics

With foundations established, these landmark papers reveal the mathematical elegance underlying the Shapley value—why it's *the unique* solution satisfying natural fairness properties.

### 3. Shapley's original 1953 paper (the landmark)

**Citation:** Lloyd S. Shapley. "A Value for n-Person Games." In *Contributions to the Theory of Games, Vol. II* (Annals of Mathematics Studies, No. 28), edited by H.W. Kuhn and A.W. Tucker, pp. 307-317. Princeton University Press, 1953. Also RAND Corporation Paper P-295.

The **11-page paper** that launched an entire field and contributed to Shapley's 2012 Nobel Prize. Shapley derives his value from three axioms with "simple intuitive interpretations": efficiency (total value distributed equals grand coalition worth), symmetry (equal contributors receive equal payoffs), additivity, and the null player property. He then proves *uniqueness*—the Shapley value is the only function satisfying these axioms. The famous formula emerges: a player's value equals their expected marginal contribution when players join in random order. Physicists will recognize this axiomatic style from thermodynamics or special relativity.

**Why included:** Essential primary source; elegant proof accessible to mathematically mature readers; the conceptual foundation for everything that follows.

**Accessibility:** ✅ FREE PDF at rand.org | **Difficulty:** Moderate | **Time:** 1-2 hours

### 4. Young's monotonicity characterization (alternative axiomatics)

**Citation:** H. Peyton Young. "Monotonic Solutions of Cooperative Games." *International Journal of Game Theory* 14, no. 2 (1985): 65-72. DOI: 10.1007/BF01769885

This **8-page paper** (~800 citations) provides the most important alternative characterization of Shapley values. Young replaces the somewhat technical additivity axiom with a single intuitive property—**strong monotonicity**: if a player's marginal contribution to every coalition increases, their payoff cannot decrease. This reveals the Shapley value's deep connection to measuring individual productivity: contribute more, receive more. Many practitioners find Young's axiomatics more philosophically compelling than Shapley's original.

**Why included:** Deepens understanding of *what the axioms mean*; the monotonicity interpretation connects directly to feature importance intuitions in ML.

**Accessibility:** ⚠️ Paywalled (Springer), typically available through institutional access | **Difficulty:** Moderate-advanced | **Time:** 1-2 hours

---

## Stage 3: Machine learning applications

These papers connect cooperative game theory to modern interpretability, showing how Shapley's 1953 insights became the foundation for explaining black-box models.

### 5. Rozemberczki et al. survey (the bridge)

**Citation:** Benedek Rozemberczki, Lauren Watson, Péter Bayer, Hao-Tsung Yang, Olivér Kiss, Sebastian Nilsson, and Rik Sarkar. "The Shapley Value in Machine Learning." *Proceedings of the 31st International Joint Conference on Artificial Intelligence (IJCAI)*, pp. 5572-5579, 2022. arXiv:2202.05594.

This survey (~290 citations) is the **critical bridge** between game theory and ML applications. It opens with cooperative game theory fundamentals and axiomatic properties, then systematically covers five application domains: feature selection, explainability (SHAP), multi-agent reinforcement learning, ensemble pruning, and data valuation. The paper includes a clear taxonomy classifying methods by Shapley value type, feature replacement approach, and approximation algorithm. Crucially, it discusses *limitations*—feature dependencies, approximation violations, computational complexity—that practitioners must understand.

**Why included:** Explicitly designed to connect game theory to ML; covers SHAP within broader context; identifies practical pitfalls; comes with an accompanying GitHub repository of resources.

**Accessibility:** ✅ FREE on arXiv | **Difficulty:** Intermediate | **Time:** 3-4 hours

### 6. Lundberg & Lee's SHAP paper (the unification)

**Citation:** Scott M. Lundberg and Su-In Lee. "A Unified Approach to Interpreting Model Predictions." *Advances in Neural Information Processing Systems 30 (NeurIPS)*, pp. 4766-4777, 2017. arXiv:1705.07874.

With **~28,000 citations**, this is one of the most influential ML interpretability papers ever written. Lundberg and Lee prove that Shapley values are the *unique* solution satisfying three desirable explanation properties: local accuracy, missingness, and consistency. This theoretical result unifies six previously separate methods—LIME, DeepLIFT, layer-wise relevance propagation, and others—showing they're all approximating Shapley values under different assumptions. The paper introduces **KernelSHAP**, a model-agnostic approximation combining LIME-style sampling with Shapley value guarantees.

**Why included:** The foundational paper for SHAP; proves why Shapley values are theoretically optimal for feature attribution; essential reading for any ML interpretability work.

**Accessibility:** ✅ FREE on arXiv and NeurIPS proceedings | **Difficulty:** Intermediate-advanced | **Time:** 3-4 hours

### 7. TreeSHAP paper (practical deployment)

**Citation:** Scott M. Lundberg, Gabriel G. Erion, Hugh Chen, Alex DeGrave, Jordan M. Prutkin, Bala Nair, Ronit Katz, Jonathan Himmelfarb, Nisha Bansal, and Su-In Lee. "From Local Explanations to Global Understanding with Explainable AI for Trees." *Nature Machine Intelligence* 2, no. 1 (2020): 56-67. arXiv:1905.04610.

This paper (~6,100 citations) solves the computational bottleneck that limited SHAP's practical adoption. The **TreeSHAP algorithm** computes *exact* Shapley values for tree ensembles in polynomial time O(TLD²), versus exponential time for the general case. For fraud detection using XGBoost, LightGBM, or random forests, this is the paper that makes SHAP computationally tractable. Beyond the algorithm, it introduces **SHAP interaction values** for capturing pairwise feature effects, plus visualization tools (summary plots, dependence plots) that convert local explanations into global model understanding.

**Why included:** Directly applicable to fraud prevention ML workflows; implemented in the shap Python library; demonstrates the full interpretability pipeline from theory to deployment.

**Accessibility:** ✅ FREE on arXiv (1905.04610) and PMC | **Difficulty:** Intermediate | **Time:** 3-4 hours

### 8. Myerson's textbook (comprehensive reference)

**Citation:** Roger B. Myerson. *Game Theory: Analysis of Conflict*. Harvard University Press, 1991. ISBN: 0-674-34116-3.

This comprehensive textbook by the 2007 Nobel laureate (whose PhD thesis was "A Theory of Cooperative Games") serves as your long-term reference. Chapters 8-10 cover bargaining and cooperation, coalitional games including Shapley value derivations, and cooperation under uncertainty. Myerson balances formal proofs with intuitive explanations and includes challenging problem sets. The book goes beyond Osborne-Rubinstein into mechanism design and information economics, providing depth if you continue exploring this field.

**Why included:** The most authoritative single-author game theory textbook; excellent for filling gaps or exploring tangential topics; Nobel laureate's perspective on cooperative games.

**Accessibility:** ⚠️ Purchase required (~$35 paperback) | **Difficulty:** Graduate level | **Time:** 15-20 hours for chapters 8-10

---

## Recommended reading order and time estimates

| Order | Resource | Stage | Time | Cumulative |
|-------|----------|-------|------|------------|
| 1 | Serrano survey | Foundations | 2-3 hrs | 3 hrs |
| 2 | Shapley 1953 | Theory | 1-2 hrs | 5 hrs |
| 3 | Young 1985 | Theory | 1-2 hrs | 7 hrs |
| 4 | Rozemberczki survey | Bridge | 3-4 hrs | 11 hrs |
| 5 | Lundberg & Lee 2017 | ML | 3-4 hrs | 15 hrs |
| 6 | TreeSHAP 2020 | ML | 3-4 hrs | 19 hrs |
| 7 | Osborne-Rubinstein Ch. 13-14 | Foundations | 6-10 hrs | as needed |
| 8 | Myerson Ch. 8-10 | Reference | 15-20 hrs | as needed |

The first six resources form the **core path** (~19 hours), taking you from no game theory knowledge to understanding and applying SHAP. Osborne-Rubinstein and Myerson serve as references for deeper exploration or when you want complete proofs.

## What makes this list work for your profile

The progression respects your physics background by presenting Shapley values through their axiomatic structure—the uniqueness proofs will feel familiar from thermodynamics or quantum mechanics. Young's 1985 monotonicity paper particularly resonates with physical intuition: the Shapley value essentially measures each player's "productivity," analogous to how partial derivatives measure each variable's contribution to a function.

For fraud prevention work, the TreeSHAP paper is especially relevant. Most production fraud models use gradient boosted trees, and TreeSHAP's polynomial-time algorithm makes real-time explanation feasible. The SHAP interaction values can reveal feature combinations driving fraud signals—patterns that univariate importance measures miss.

Six of eight resources are freely available, and the two requiring purchase (Young via institutional access, Myerson as optional reference) can be deferred until you've completed the free core path.