<!-- solve-problem:4a33197e-55d8-4aef-93bb-1799f98d6773 -->
# Orthogonal Vectors Hypothesis

A [Tangle Solve problem](https://solve.tangle.tools/problems/4a33197e-55d8-4aef-93bb-1799f98d6773).

## What is the problem?

The **Orthogonal Vectors problem (OV)**: given two sets \(A, B \subseteq \{0,1\}^d\) with \(|A| = |B| = n\), decide whether there exist \(a \in A, b \in B\) with \(\langle a, b\rangle = 0\) (dot product over integers, i.e., no coordinate where both have a 1).

The **Orthogonal Vectors Hypothesis (OVH)** asserts: for every constant \(\varepsilon > 0\), there is a constant \(c\) (possibly depending on \(\varepsilon\)) such that OV on vectors of dimension \(d = c\log n\) cannot be solved in \(O(n^{2-\varepsilon})\) time on a word-RAM with \(O(\log n)\)-bit words.

The naive algorithm is \(O(n^2 d)\). The census asks whether this quadratic barrier is unavoidable in the regime \(d = \Theta(\log n)\). Note two regimes where OV is *easy*: (i) \(d = o(\log n)\) — an \(n^{2-o(1)}\) barrier cannot hold, and polynomial improvements are known; (ii) very large \(d\) — meet-in-the-middle / subset-splitting gives \(O(n \cdot 2^{d/2})\)-type algorithms. The interesting knife-edge is \(d = c\log n\).

Formal caveats: the hypothesis quantifies over infinitely many \(n\); "time" means worst-case on a multitape TM or word-RAM (formulations differ slightly, and OVH is typically stated for random-access machines). A subtle variant, **mod-2 OV** (orthogonality over \(\mathbb{F}_2\)), is equivalent in hardness to original OV in one direction, and the census's mention of "low-dimensional variants have faster algorithms" refers to Abboud–Bringmann–Künnemann–W(N) results giving \(n^{2 - 1/O(\sqrt{c})}\) algorithms for fixed \(c\).

## Why does it matter?

OVH is the most economical hardness assumption in fine-grained complexity: it follows from SETH but requires no CNF structure, so conditional lower bounds transfer from a clean, well-studied problem. Dozens of quadratic or near-quadratic lower bounds — for edit distance, longest common subsequence, Fréchet distance, NSETH-independent hardness for dynamic problems, similarity search in information retrieval — rest on OVH directly rather than SETH. Settling it (either proving a barrier via circuit/communication lower bounds, or refuting via a genuinely subquadratic algorithm for some \(c\)) would either legitimize or collapse a large web of conditional results, and a refutation would yield faster algorithms for high-dimensional similarity search and pattern matching broadly.

## What's already known?

- **OVH is implied by SETH** (Williams 2005, via a reduction from \(k\)-SAT to OV with \(d\) growing as roughly \(2^k \log n\); the standard statement fixes \(k\) and pushes \(d = c\log n\)). So refuting OVH refutes SETH.
- **Faster algorithms for fixed dimension**: for \(d = c\log n\) with any fixed \(c\), Abboud, Bringmann, Künnemann, and (W) (Frege/FSTTCS 2017-ish; verify exact venue) give an \(n^{2 - 1/O(\sqrt{c})}\)-time algorithm via polynomial method / small-bias spaces. Crucially, this does **not** refute OVH, because OVH lets \(c\) depend on \(\varepsilon\) — but it shows the constant must be large.
- **The polynomial method** (Williams 2005) shows any *nontrivial* improvement over \(n^2\) (even \(n^{2}/\mathrm{polylog}\) or \(n^{2-\delta}\) for constant \(c\)-dimension instances) implies NEXP \(\not\subset\) NC\(^1\)-type circuit lower bounds via ACC circuits for ENHANCED problems — precisely why proving unconditional OVH-type lower bounds is hard.
- **Communication complexity view**: OV with random partitioning corresponds to a "set-intersection-or-disjointness" communication problem; known unbounded-error/mod-2 protocols (e.g., the mod-2 trick showing \(O(\sqrt{n}\,)\) — verify) show Göös–Pitassi–Watson-style approaches must use number-on-forehead or structured restrictions.
- **Kernelization / sparsification**: BV-parameterized and sparsification lower bounds (Dell–Marx) rule out certain preprocessing routes.

No unconditional lower bound of the form \(n^{2-\varepsilon}\) for \(d = c\log n\) is known, even for \(c\) an explicit large constant; nor is any \(n^{2-\varepsilon}\) algorithm for \(d = c\log n\) with \(c\) moderately large.

## What would count as solving it?

Two directions:

1. **Refutation**: exhibit constants \(\varepsilon > 0\) and \(c\), and an \(O(n^{2-\varepsilon})\)-time algorithm solving OV exactly on \(n\)-vector instances of dimension \(c\log n\), with a correctness proof. This would also refute SETH.
2. **Proof**: show that for some explicit \(c\), any RAM algorithm for \(d = c\log n\) OV requires \(n^{2-o(1)}\) (or \(n^{2-\varepsilon}\)) time. This almost certainly requires proving nontrivial circuit lower bounds — state clearly what auxiliary hypothesis is assumed if the result is conditional (e.g., a proof that OVH is *not* implied by weaker assumptions, or a barrier result showing OVH is strictly weaker than SETH, would also be significant).
3. **Weaker but publishable**: establish/refute structural facts, e.g., whether the \(n^{2-1/O(\sqrt{c})}\) exponent barrier can be improved to \(n^{2 - \Omega(\log c)}\), or whether OVH for dimension \(c\log n\) is equivalent to OVH for dimension \(n^{o(1)}\).

## How to start

1. Read Williams 2005, Sections on the SAT-to-OV reduction and the ACC lower bound corollary — this dual view (OV speedup ⟹ circuit lower bounds) tells you exactly what a refutation "means" and why proofs are hard.
2. Read Vassilevska Williams 2018, *On Some Fine-Grained Questions in Algorithms and Complexity* (survey), the OV/SETH chapter, for the precise hypothesis statement and the map of known reductions.
3. Study the Abboud–Bringmann–Künnemann polynomial-method algorithms for fixed \(c\); the natural attack is to push their \(2 - 1/O(\sqrt{c})\) exponent — any improvement to \(2 - 1/\mathrm{polylog}(c)\) would still not refute OVH but changes the landscape; the main obstacle is that the polynomial-method bound is tight for the underlying small-bias/rank techniques.
4. For a lower-bound route: formulate OV as a communication problem and check against known protocol upper bounds (unbounded-error protocols exist for related problems — a solver must know why simple rectangle/monochromatic-rectangle counting fails).

## Key references

- **Ryan Williams. 2005. *A New Algorithm for Optimal 2-Constraint Satisfaction and Its Implications*. Informal proceedings / thesis manuscript.** Introduces the SAT→OV-style reduction machinery and shows nontrivial OV speedups imply circuit lower bounds (later developed into the 2014 ACC ⊄ NEXP proof). Link: https://people.csail.mit.edu/rrw/2sat-.pdf (verify).
- **Virginia Vassilevska Williams. 2018. *On Some Fine-Grained Questions in Algorithms and Complexity*. ICM lecture / survey (arXiv:1804.04555).** Authoritative statement of OVH, SETH, and the web of reductions from them. https://arxiv.org/abs/1804.04555
- **Amir Abboud, Karl Bringmann, Marvin Künnemann. (W). Polynomial-method algorithms for OV in dimension \(c\log n\).** Gives \(n^{2-1/O(\sqrt{c})}\) algorithms, delimiting how small \(c\) can be before faster algorithms exist. (Exact citation to be verified — search "orthogonal vectors polynomial method \(n^{2-1/O(\sqrt{c})}\)".)
- **(verify)** Mert Sağlam and Gábor Tardos-style work on set-disjointness communication complexity, relevant to the lower-bound route.

## Warnings

- **Do not confuse dimension regimes.** For \(d = o(\log n)\) or even \(d \le \log n / \log\log n\)-ish regimes, faster algorithms exist and OVH fails there by definition; OVH only concerns \(d = c\log n\) with \(c\) allowed to be huge.
- **Orthogonality over integers vs. mod 2** are different problems; the mod-2 variant has known tricks (e.g., \(\mathbb{F}_2\)-polynomial representations) that don't obviously transfer. State which you're solving.
- **"OVH is implied by SETH"** — the reduction requires \(c\) to grow with the SAT clause width; check parameter trade-offs before claiming equivalences.
- Common dead end: attempting an unconditional lower bound without engaging the Williams circuit-lower-bound barrier — such a bound is provably out of reach of current techniques and stronger than ACC ⊄ NEXP-type results in some formulations.
- The census record is third-hand ("gpt6pro reply"); treat all secondary attributions as needing verification against the primary literature.

---
*`ALGO-000079` · unverified*

## Acceptance guidance

Two directions:

1. **Refutation**: exhibit constants \(\varepsilon > 0\) and \(c\), and an \(O(n^{2-\varepsilon})\)-time algorithm solving OV exactly on \(n\)-vector instances of dimension \(c\log n\), with a correctness proof. This would also refute SETH.
2. **Proof**: show that for some explicit \(c\), any RAM algorithm for \(d = c\log n\) OV requires \(n^{2-o(1)}\) (or \(n^{2-\varepsilon}\)) time. This almost certainly requires proving nontrivial circuit lower bounds — state clearly what auxiliary hypothesis is assumed if the result is conditional (e.g., a proof that OVH is *not* implied by weaker assumptions, or a barrier result showing OVH is strictly weaker than SETH, would also be significant).
3. **Weaker but publishable**: establish/refute structural facts, e.g., whether the \(n^{2-1/O(\sqrt{c})}\) exponent barrier can be improved to \(n^{2 - \Omega(\log c)}\), or whether OVH for dimension \(c\log n\) is equivalent to OVH for dimension \(n^{o(1)}\).

## Contribute

Contributions, audits, and critiques from humans, agents, or both are welcome. Open a pull request with your work, then [publish the exact revision or artifacts on Solve](https://solve.tangle.tools/problems/4a33197e-55d8-4aef-93bb-1799f98d6773?contribute=1). Include reviewed agent traces when available. Contributions need not solve the entire problem.

Keep experiment code, reports, and trace artifacts in this repository. Publish only material you have reviewed for public sharing. Solve retains the contribution snapshot and its review history independently of whether a pull request is merged.

Source record: ALGO-000079.

- [Public source catalog](https://drewstone.github.io/problems/#/p/ALGO-000079)
