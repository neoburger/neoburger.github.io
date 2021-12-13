# NeoBurger Public Strategies

## The Introduction

TODO

## The Problem

Given:

- $\mathcal{C}$: a set of candidates
- $v_c \in \mathbb{R_{\ge 0}}$: the votes of each candidate $c \in \mathcal{C}$
- $k_c \in \mathbb{R_{\ge 0}}$: the reward coefficient of each candidate $c \in \mathcal{C}$
- $n \in \mathbb{R_{\ge 0}}$: the total amount of *NEO* we hold

Solve the amount of *NEO* $n_c \in \mathbb{R_{\ge 0}}$ we vote to each candidate $c \in \mathcal{C}$ satisfing $\sum_{c \in \mathcal{C}}{n_c} = n$ and maximizing the following *GAS* reward expression:

$$
f = \sum_{c \in \mathcal{C}}{\frac{n_c k_c}{v_c + n_c}} \in \mathbb{R_{\ge 0}}
$$

## The Metric

- time complexity
- space complexity

## The Solution

1. calculate $n_*$:
 
    $$
    n_* = \sum_{c \in \mathcal{C}}{v_c}
    $$

2. calculate $u$:
 
    $$
    u = \frac{n + n_*}{\sum_{c \in \mathcal{C}}{\sqrt{k_c v_c}}}
    $$

3. for $\forall c \in \mathcal{C}$:
 
    $$
    n_c = u \sqrt{k_c v_c} - v_c
    $$

## The Analysis

### Correctness

TODO

## The Experiment

TODO

## The Conclusion

TODO

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
