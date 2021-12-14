# NeoBurger Public Strategy

> Neo was founded 2014 and has grown into a first-class smart contract platform. It is backed by a global developer community who continue to drive the blockchain forward. [more](https://neo.org/about)

> The N3 version of the Neo MainNet launched at 9:00:00 on August 2nd, 2021 (UTC). [more](https://neo.org/blog/details/4240)

> Neo is unique in that it was the first public blockchain platform to adopt a dual token mechanism (*NEO* and *GAS*). It separates the rights of governance from the rights of using the network. It also provides a means of acquiring the tokens needing to pay transaction fees. [more](https://neo.org/neogas#tokens)

> *NEO* token holders decide who is in charge of maintaining the Neo network through the election of a Neo Council. *GAS* token rewards are distributed to voters and council members alike. [more](https://neo.org/gov)

## The Introduction

> NeoBurger project seeks to compensate for the usability issues of indivisible NEO in applications such as DeFi, while also providing an avenue for maximized GAS rewards for holders. [more](https://neonewstoday.com/general/neoburger-an-automated-voting-dapp-and-neo-token-wrapper-launches-on-n3/)

> NeoBurger earns the majority of its *GAS* by voting in the Neo N3 governance mechanism. *NEO* pooled in the NeoBurger contract is automatically managed using different voting strategies. NEO is distributed between a limited number of “agents,” each of which can cast a vote. By using multiple agents as separate wallets, NeoBurger can get around the limitation of only being able to vote for one candidate at a time.

> Constant management of votes between the agents allows the NeoBurger platform to maximize the *GAS* received from the vote reward distribution. The majority of these rewards are passed on to *bNEO* holders, although some fees do also apply to certain actions. As more NEO is pooled in NeoBurger, the platform can employ further strategies, for example to use its increased vote weight to help elect new nodes to the council.

In this article, the NeoBurger strategy of a simplified governance mechnism of Neo network is introduced.

### Native Governance Reward Mechnism

Everyone can burn `1000` *GAS* and become a candidate.

Every *NEO* holder can vote to a candidate and the voting weight is its *NEO* balance. Votes can be changed or canceled by the *NEO* holder.

The Top 7 voted candidates are elected as consensus nodes and the Top 21 voted candidates are elected as council members.

There are 5 *GAS* generated in each block: `40%` of the *GAS* are splited equally among the 7 voter groups of consensus nodes and `40%` of the *GAS* are splited equally among the 14 voter groups of non-consensus-nodes council members. Inside each group, the *GAS* is distributed to the voters by their NEO balances.

In this article, reward coefficient is defined as the *GAS* distributed to each voter group.

NeoBurger can distribute its *NEO* to the controled agents who vote to different specific candidates.

We want to solve the optimal *NEO* distribution.

### Limitations of the Strategy

In this article:

- amount of *NEO* is a positive real number instead of a positive integer while *NEO* is an indivisible token;
- reward coefficients are constants while actually they can be changed by moving candidate's rank up or down; (actually moving candidates into or out from consensus nodes or council members is a dangerous operation for the entire network if the candidates are not prepared well)

## The Problem

Given:

- $\mathcal{C}$: a set of candidates
- $v_c \in \mathbb{R}_{\gt 0}$: the votes of each candidate $c \in \mathcal{C}$
- $k_c \in \mathbb{R}_{\gt 0}$: the reward coefficient of each candidate $c \in \mathcal{C}$
- $n \in \mathbb{R}_{\gt 0}$: the total amount of *NEO* we hold

Solve the amount of *NEO* $n_c \in \mathbb{R}_{\ge 0}$ we vote to each candidate $c \in \mathcal{C}$:

- satisfing $\sum_{c \in \mathcal{C}}{n_c} = n$

- maximizing the following *GAS* reward expression:

    $$
    f = \sum_{c \in \mathcal{C}}{\frac{n_c k_c}{v_c + n_c}} \in \mathbb{R}_{\gt 0}
    $$

## The Metric

- time complexity
- space complexity

## The Solution

Define the solution as a mapping $\Psi_{\mathcal{C}}$: $\mathcal{C} \rightarrow \mathbb{R}_{\ge 0}$

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

4. define $\mathcal{C}_+$:
 
    $$
    \mathcal{C}_+ = \{ c \vert c \in \mathcal{C}, n_c \ge 0 \}
    $$

5. return a mapping $\Psi_{\mathcal{C}}$:

   $$
   \Psi_{\mathcal{C}}(c) = \begin{cases} 0 & c \notin \mathcal{C}_+ \\ n_c & \mathcal{C}_+ = \mathcal{C} \\ \Psi_{\mathcal{C}_+}(c) & \text{else} \end{cases}
   $$

## The Analysis

Proof of Correctness and complexity will be explained in this section.

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

Sufficient conditions for a constrained local maximum can be stated in terms of a sequence of principal minors (determinants of upper-left-justified sub-matrices) of the [bordered Hessian matrix](https://en.wikipedia.org/wiki/Hessian_matrix#Bordered_Hessian) of second derivatives of the Lagrangian expression.

$$
\mathbf{H}(\Lambda) = 
\begin{bmatrix}
    \frac{\partial^2{\Lambda}}{\partial{\lambda}^2} & \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_1}}} & \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_2}}} & \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_3}}} & \dots & \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_{\lVert \mathcal{C} \rVert}}}} \\
    \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_1}}} & \frac{\partial^2{\Lambda}}{\partial{n_{c_1}}^2} & & & & \\
    \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_2}}} & & \frac{\partial^2{\Lambda}}{\partial{n_{c_2}}^2} & & & \\
    \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_3}}} & & & \frac{\partial^2{\Lambda}}{\partial{n_{c_3}}^2} & & \\
    \vdots & & & & \ddots & \\
    \frac{\partial^2{\Lambda}}{\partial{\lambda} \partial{n_{c_{\lVert \mathcal{C} \rVert}}}} & & & & & \frac{\partial^2{\Lambda}}{\partial{n_{c_{\lVert \mathcal{C} \rVert}}}^2} \\
\end{bmatrix}
$$

Then:

$$
\mathbf{H}(\Lambda) = 
\begin{bmatrix}
    0 & -1 & -1 & -1 & \dots & -1 \\
    -1 & -\frac{2 k_{c_1} v_{c_1}}{ {(v_{c_1} + n_{c_1})}^3 } & & & & \\
    -1 & & -\frac{2 k_{c_2} v_{c_2}}{ {(v_{c_2} + n_{c_2})}^3 } & & & \\
    -1 & & & -\frac{2 k_{c_3} v_{c_3}}{ {(v_{c_3} + n_{c_3})}^3 } & & \\
    \vdots & & & & \ddots & \\
    -1 & & & & & -\frac{2 k_{c_{\lVert \mathcal{C} \rVert}} v_{c_{\lVert \mathcal{C} \rVert}}}{ {(v_{c_{\lVert \mathcal{C} \rVert}} + n_{c_{\lVert \mathcal{C} \rVert}})}^3 } \\
\end{bmatrix}
$$

For $i \le \lVert \mathcal{C} \rVert \in \mathbb{N}_+$, the $i$-th upper-left-justified sub-matrices is:

$$
\mathbf{h}_i =
\begin{bmatrix}
    0 & -1 & -1 & -1 & \dots & -1 \\
    -1 & -\frac{2 k_{c_1} v_{c_1}}{ {(v_{c_1} + n_{c_1})}^3 } & & & & \\
    -1 & & -\frac{2 k_{c_2} v_{c_2}}{ {(v_{c_2} + n_{c_2})}^3 } & & & \\
    -1 & & & -\frac{2 k_{c_3} v_{c_3}}{ {(v_{c_3} + n_{c_3})}^3 } & & \\
    \vdots & & & & \ddots & \\
    -1 & & & & & -\frac{2 k_{c_i} v_{c_i}}{ {(v_{c_i} + n_{c_i})}^3 } \\
\end{bmatrix}
$$

Follow the [Leibniz formula for determinants](https://en.wikipedia.org/wiki/Leibniz_formula_for_determinants):

$$
\det \mathbf{h}_i = \sum_{1 \le t \le i}{(-1) {(-1)}^2 \prod_{1 \le s \le i, s \neq t}{-\frac{2 k_{c_s} v_{c_s}}{ {(v_{c_s} + n_{c_s})}^3 }}}
$$

Thus:

$$
\operatorname{sign}(\det \mathbf{h}_i) = \operatorname{sign}(\sum_{1 \le t \le i}{ {(-1)}^i }) = {(-1)}^i
$$

Thus it is a local maximum of function $f$.

Since the Hessian matrix shows $f$ is an [upper convex function](https://en.wikipedia.org/wiki/Concave_function) whose local maximum is also a global maximum, our solution is the global maximum.

The only issue left is that sometimes $\exists c \in \mathcal{C}$, $n_c \lt 0$.

define $\mathcal{C}_-$:
 
$$
\mathcal{C}_- = \{ c \vert c \in \mathcal{C}, n_c \lt 0 \}
$$

to satisfy $\forall c \in \mathcal{C}$: $n_c \ge 0$, we let:

$$
\forall c \in \mathcal{C}_- : n_c = 0
$$

Otherwise $f$ is never maximum because:

$$
\max{f} \vert_{\exists c \in \mathcal{C}_- : n_c \gt 0} \lt \max{f} \vert_{\forall c \in \mathcal{C}_- : n_c = 0}
$$

Then re-calculate the rest.

### Time Complexity

$$
O({\lVert \mathcal{C} \rVert}^2) 
$$

### Space Complexity

$$
O(\lVert \mathcal{C} \rVert) 
$$

## The Experiment

TODO

## The Conclusion

damn greedy :)

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
