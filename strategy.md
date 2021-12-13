# NeoBurger Public Strategies

## The Introduction

TODO

## The Problem

Given:

- $\mathcal{C}$: a set of candidates
- $v_c \in \mathbb{R}_{\ge 0}$: the votes of each candidate $c \in \mathcal{C}$
- $k_c \in \mathbb{R}_{\ge 0}$: the reward coefficient of each candidate $c \in \mathcal{C}$
- $n \in \mathbb{R}_{\ge 0}$: the total amount of *NEO* we hold

Solve the amount of *NEO* $n_c \in \mathbb{R}_{\ge 0}$ we vote to each candidate $c \in \mathcal{C}$ satisfing $\sum_{c \in \mathcal{C}}{n_c} = n$ and maximizing the following *GAS* reward expression:

$$
f = \sum_{c \in \mathcal{C}}{\frac{n_c k_c}{v_c + n_c}} \in \mathbb{R}_{\ge 0}
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

Follow the [method of Lagrange multipliers](#https://en.wikipedia.org/wiki/Lagrange_multiplier):

In order to find the maximum of function $f$ subjected to the equality constraint $g = \sum_{c \in \mathcal{C}}{n_c} - n = 0$, form the Lagrangian function:

$$
\Alpha = f - \lambda g
$$

The necessary condition for the optimality can be inferred by solving the following equation

$$
\nabla{\Alpha} = 0
$$

Thus for $\forall c \in \mathcal{C}$:

$$
\frac{\partial{\Alpha}}{\partial{n_c}} = - \frac{k_c v_c}{ {(v_c + n_c)}^2 } - \lambda = 0
$$

TODO

## The Experiment

TODO

## The Conclusion

TODO

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
