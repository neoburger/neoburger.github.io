# NeoBurger Public Strategy

## The Introduction

TODO

## The Problem

Given:

- $\mathcal{C}$: a set of candidates
- $v_c \in \mathbb{R}_{\gt 0}$: the votes of each candidate $c \in \mathcal{C}$
- $k_c \in \mathbb{R}_{\gt 0}$: the reward coefficient of each candidate $c \in \mathcal{C}$
- $n \in \mathbb{R}_{\gt 0}$: the total amount of *NEO* we hold

Solve the amount of *NEO* $n_c \in \mathbb{R}_{\ge 0}$ we vote to each candidate $c \in \mathcal{C}$ satisfing $\sum_{c \in \mathcal{C}}{n_c} = n$ and maximizing the following *GAS* reward expression:

$$
f = \sum_{c \in \mathcal{C}}{\frac{n_c k_c}{v_c + n_c}} \in \mathbb{R}_{\gt 0}
$$

## The Metric

- time complexity
- space complexity

## The Solution

Define the solution as a function $\Psi$:$ $\mathcal{C} \times \mathbb{R}^{\lVert \mathcal{C} \rVert}_{\gt 0} \times \mathbb{R}^{\lVert \mathcal{C} \rVert}_{\gt 0} \times \mathbb{R}_{\gt 0} \rightarrow \mathcal{C} \rightarrow \mathbb{R}_{\ge 0}$

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

4. define $\mathcal{C}_-$:
 
    $$
    \mathcal{C}_- = \{ c \vert c \in \mathcal{C}, n_c \lt 0 \}
    $$

5. return a mapping $\psi$ where $V$ is $v_c$ for $\forall c \in \mathcal{C}$ and $K$ is $k_c$ for $\forall c \in \mathcal{C}$ :

   $$
   \psi(c) = \begin{cases} 0 & c \in \mathcal{C}_- \\ n_c & \lVert \mathcal{C}_0 \rVert = 0 \\ \Psi_{\mathcal{C} \setminus \mathcal{C}_-, V, K, n } & \text{else} \end{cases}
   $$

## The Analysis

### Correctness

Follow the [method of Lagrange multipliers](#https://en.wikipedia.org/wiki/Lagrange_multiplier):

In order to find the maximum of function $f$ subjected to the equality constraint $g = n - \sum_{c \in \mathcal{C}}{n_c} = 0$, form the Lagrangian function:

$$
\Lambda = f - \lambda g
$$

The necessary condition for the optimality can be inferred by solving the following equation

$$
\nabla{\Lambda} = 0
$$

Thus for $\forall c \in \mathcal{C}$:

$$
\frac{\partial{\Lambda}}{\partial{n_c}} = - \frac{k_c v_c}{ {(v_c + n_c)}^2 } - \lambda = 0
$$

Thus for $\forall c_i, c_j \in \mathcal{C}$:

$$
\frac{k_{c_i} v_{c_i}}{ {(v_{c_i} + n_{c_i})}^2 } = \frac{k_{c_j} v_{c_j}}{ {(v_{c_j} + n_{c_j})}^2 }
$$

Thus for $\forall c_i, c_j \in \mathcal{C}$:

$$
\frac{n_{c_i} + v_{c_i}}{\sqrt{k_{c_i} v_{c_i}}} = \frac{n_{c_j} + v_{c_j}}{\sqrt{k_{c_j} v_{c_j}}} 
$$

For $\forall c \in \mathcal{C}$: let $u = \frac{n_c + v_c}{\sqrt{k_c v_c}}$, then:

$$
\sum_{c \in \mathcal{C}}{u \sqrt{k_c v_c}} = \sum_{c \in \mathcal{C}}{n_c + v_c} = n + n_*
$$

Thus:

$$
u = \frac{n + n_*}{\sum_{c \in \mathcal{C}}{\sqrt{k_c v_c}}}
$$

Thus:

$$
n_c = u \sqrt{k_c v_c} - v_c
$$

## The Experiment

TODO

## The Conclusion

TODO

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
