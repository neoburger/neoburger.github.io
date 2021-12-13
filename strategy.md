# NeoBurger Public Strategies

## The Introduction

TODO

## The Problem

Given:

- $\mathcal{P}$: a set of candidates
- $\mathcal{Q}$: a set of agents
- $v_p \in \mathbb{R_{\ge 0}}$: the votes of each candidate $p \in \mathcal{P}$
- $k_p \in \mathbb{R_{\ge 0}}$: the reward coefficient of each candidate $p \in \mathcal{P}$
- $n \in \mathbb{R_{\ge 0}}$: the total amount of *NEO* we hold

Solve:

- $n_q \in \mathbb{R_{\ge 0}}$: the amount of *NEO* distributed to each agent $q \in \mathcal{Q}$
- $p_q \in \mathcal{P}$: the voting target of each agent $q \in \mathcal{Q}$

which maximize the following *GAS* reward expression:

$$
\sum_{q \in Q}{\frac{n_q k_{p_q}}{v_{p_q} + n_q}}
$$


## The Metric

TODO

## The Solution

TODO

## The Analysis

TODO

## The Experiment

TODO

## The Conclusion

TODO

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
