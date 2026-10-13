<!-- solve-problem:d20f4b09-9dcf-4cde-ac12-6d0d02e5eae0 -->
# Efficient uniform-distribution DNF learning from examples alone

A [Tangle Solve problem](https://solve.tangle.tools/problems/d20f4b09-9dcf-4cde-ac12-6d0d02e5eae0).

## What is the problem?

Learn the class of polynomial-size DNF formulas over {0,1}ⁿ in the PAC model augmented only with random examples, under the uniform distribution. Formally: given ε, δ > 0 and access to an oracle that returns (x, f(x)) for x ~ Uniform({0,1}ⁿ), where f is a DNF formula of top-level fan-in (size) s, output a hypothesis h such that Pr[h(x) ≠ f(x)] ≤ ε with probability ≥ 1 − δ, in time poly(n, s, 1/ε, 1/δ). Crucially, **no membership queries**: the learner cannot choose x and ask for f(x). "Polynomial-size" means s = poly(n), so the target is time poly(n, 1/ε). Note the problem is typically stated for s-term DNF regardless of term width; terms may have width up to n. Agnostically-noisy variants and weaker goals (e.g., poly(1/ε) with n^O(log(1/ε)) time) do not constitute a solution.

## Why does it matter?

This is the canonical open problem separating passive from active learning: Jackson's algorithm shows membership queries suffice, LMN shows quasipolynomial time suffices without them, and closing the gap either way would be a landmark. A positive resolution would give efficient learning of an expressive, interpretable class central to computational learning theory, with connections to agnostic learning, hardness-of-noise results (e.g., learning noisy parities), and pseudorandomness. A negative resolution (even oracle/cryptographic) would establish the first strong separation between PAC and MQ learning.

## What's already known?

- **LMN (1993):** The low-degree Fourier algorithm learns poly-size DNF over the uniform distribution in time n^O(log s) (quasipolynomial). This remains the best passive upper bound for general DNF.
- **Jackson (1997):** The Harmonic Sieve learns DNF in poly time under the uniform distribution **using membership queries**, via a boosting algorithm (Freund–Schapire) whose weak learners are Fourier-based; the MQs are used inside the weak learner, and this use appears essential.
- **Klivans–Servedio (2004)** (verify): improved passive algorithms for DNF achieve time poly(n) · (1/ε)^O(log log s) or similar tradeoffs — still superpolynomial in 1/ε.
- **Hardness:** Learning poly-size DNF even under uniform distribution implies learning noisy parities in a related regime (via folklore reductions); noisy parity is believed hard and underlies Learning with Errors-type assumptions. So a poly-time passive algorithm plausibly breaks widely-believed cryptographic assumptions — or the reduction fails, and the problem is just open.

## What would count as solving it?

1. **Upper bound (positive):** An algorithm taking i.i.d. uniform examples from any s-term DNF, outputting h with error ≤ ε in time poly(n, s, 1/ε, 1/δ). Proof of correctness plus running-time analysis suffices.
2. **Lower bound (negative):** A proof (possibly under a stated hardness assumption, e.g., hardness of learning noisy parities, or an oracle separation) that no poly-time passive learner exists for poly-size DNF under uniform.
3. **Partial:** A poly(n, s) time algorithm with dependence poly(1/ε) — i.e., n^O(log s) → poly — for constant ε would already be major; referees would accept a clearly stated parameter improvement as progress but not as full resolution.

## How to start

1. Read Jackson (1997) carefully, Section on the weak learner, to understand exactly where membership queries are used and whether an LMN-style ℓ₁/Fourier weak learner on uniform examples could substitute for fixed ε-accuracy — the obstacle is that boosted distributions are far from uniform.
2. Read LMN (1993) for the Fourier concentration of DNF (ℓ₁ mass of low-degree coefficients bounded via O(log s) degree) and the resulting n^O(log s) bound; then Klivans–Servedio's improved analysis to see the current frontier.
3. Natural approaches: (a) find weak learners robust to distribution shift without re-querying; (b) use the fact that DNF hypotheses themselves can be evaluated on any x (self-labeled data augmentation) to simulate queries approximately via rejection sampling; (c) target structured subproblems (e.g., monotone DNF, small-width DNF) first.
4. Main obstacle: any boosting-based approach needs weak learning under adversarially shifted distributions, and passive examples only cover the uniform distribution.

## Key references

- Linial, Mansour, Nisan. "Constant Depth Circuits, Fourier Transform, and Learnability." *Journal of the ACM* 40(3), 1993. Shows AC⁰ (hence DNF) has most Fourier ℓ₁ mass on low-degree coefficients, yielding a quasipolynomial-time uniform-distribution PAC algorithm from random examples alone. https://doi.org/10.1145/174130.174138
- Jackson, Jeffrey. "An Efficient Membership-Query Algorithm for Learning DNF with Respect to the Uniform Distribution." *Journal of Computer and System Sciences* 55(3), 1997. Gives the Harmonic Sieve, a poly-time DNF learner under uniform using membership queries via boosting with Fourier weak learners. https://doi.org/10.1006/jcss.1997.2035
- Klivans, Servedio. "Learning DNF in time 2^O(n^{1/3})." *Journal of Computer and System Sciences* 68(2), 2004 (verify title/details). Improves passive uniform-distribution DNF learning parameters, illustrating the state of the art short of polynomial time. (verify)

## Warnings

- "DNF learning" has many variants; the open problem is **uniform distribution, random examples only, exact PAC success criterion**. Agnostic, distribution-free, or MQ results do not resolve it.
- A common dead end: naively boosting with LMN weak learners fails because the weak learner must work under the boosted distributions, not uniform; MQs in Jackson's algorithm exist precisely to sample/evaluate under those distributions.
- Superpolynomial dependence on 1/ε is the typical failure mode of improved algorithms — check the fine print of claimed improvements.
- Reductions between DNF learning and noisy-parity learning are folklore and often misstated; verify exact parameter regimes before relying on them.

---
*`ALGO-000195` · unverified*

## Acceptance guidance

1. **Upper bound (positive):** An algorithm taking i.i.d. uniform examples from any s-term DNF, outputting h with error ≤ ε in time poly(n, s, 1/ε, 1/δ). Proof of correctness plus running-time analysis suffices.
2. **Lower bound (negative):** A proof (possibly under a stated hardness assumption, e.g., hardness of learning noisy parities, or an oracle separation) that no poly-time passive learner exists for poly-size DNF under uniform.
3. **Partial:** A poly(n, s) time algorithm with dependence poly(1/ε) — i.e., n^O(log s) → poly — for constant ε would already be major; referees would accept a clearly stated parameter improvement as progress but not as full resolution.

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/d20f4b09-9dcf-4cde-ac12-6d0d02e5eae0?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000195.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000195)
