# Compound Interest with Constant Cost

Compound interest means that interest is earned on prior interest in addition to the principal. Due to compounding, the total amount of debt grows exponentially, and its mathematical study led to the discovery of the number $e$. [more](https://en.wikipedia.org/wiki/Compound_interest)

The total accumulated value is given by the formula :

$$
p = p {(1 + \frac{r}{n})}^{n t}
$$

where:

- $p$ is the [principal sum](https://en.wikipedia.org/wiki/Principal_sum)
- $r$ is the [nominal interest rate](https://en.wikipedia.org/wiki/Nominal_interest_rate)
- $n$ is the compounding frequency
- $t$ is the overall length of time the interest is applied

Continuous compounding can be thought of as making the compounding period infinitesimally small, achieved by taking the limit as $n$ goes to infinity. See [definitions of the exponential function](https://en.wikipedia.org/wiki/Definitions_of_the_exponential_function) for the mathematical proof of this limit. The total accumulated value of continuous compounding can be expressed as:

$$
p e^{r t}
$$

## The Introduction

Essentially capitalizing the accumulated interest will lead:

$$
p_{*} = p + prt
$$

where:

- $p_{*}$ is the new principal sum
- $t$ is the time of capitalizing the accumulated interest

Continuous compounding enjoys the optimal accumulated value in this case.

However, if there is a constant cost when capitalizing the accumulated interest, the new principal sum  will be:

$$
p_{*} = p + prt - c
$$

It is now harmful to make the compounding period infinitesimally small.

It is better to keep $t > \frac{c}{p r}$ to ensure the growth of the accumulated value.

Then the question is: what is the best compounding period $t$ to maximize the accumulated value.

## The Problem

Given:

- $p \in \mathtt{R}_{+}$: principal sum
- $r \in \mathtt{R}_{+}$: nominal interest rate
- $c \in \mathtt{R}_{+}$: cost of capitalizing the accumulated interest

Solve:

- $t \in \mathtt{R}_{+}$: compounding period

## The Metric

Assume $i \in \mathbb{N}_{+}$ and ${t_f}_{i} = f({p_f}_{i}, r, c)$, the principal sum after $i$-th compounding period is:

$$
{p_f}_{i} = {p_f}_{i-1} + {p_f}_{i-1} r {t_f}_{i-1} - c
$$

The initial principal sum is:

$$
{p_f}_{0} = p
$$

The total time after $i$-th compounding period is:

$$
{T_f}_{i} = {T_f}_{i-1} + {t_f}_{i}
$$

and

$$
{T_f}_{0} = 0
$$

Then we define $f_1 > f_2$ if and only if:

$$
\exists i, j \in \mathbb{N}_{+}: {p_{f_1}}_{i} > {p_{f_2}}_{j} \land {T_{f_1}}_{i} < {T_{f_2}}_{j}
$$

## The Solution

$$
t = \frac{e^{W_\lambda + 1} + e \lambda}{p}
$$

where:

- $\lambda$ is $\frac{c - p}{e p}$
- $W_\lambda$ is the function value of [Lambert W function](https://en.wikipedia.org/wiki/Lambert_W_function) at $\lambda$

## The Analysis

TODO

## The Experiment

```python
from matplotlib.pyplot import plot
from matplotlib.pyplot import savefig
from scipy.special import lambertw
from math import e


def evaluate(f):
    X = 10
    P = 0.0001
    C = 1

    PT = [0]
    PF = [X]

    x = X

    while x < 1e10:
        t = f(x, P, C)
        x += x*P*t-C
        PT.append(PT[-1]+t)
        PF.append(x)

    plot(PT, PF)


def fsol(x, p, c):
    d = c/x
    m = 1-d
    r = e**(lambertw(-m/e)+1)
    return (r + d-1)/p


def fdp(x, p, c):
    N = 256
    T = c/N/p
    DP = [(x, 0)]
    while True:
        item = max(
            (DP[j][0] + DP[j][0]*p*T*(len(DP)-j)-c, j)
            for j in range(len(DP))
        )
        DP.append(item)
        if DP[-1][1] == len(DP) - 2 and DP[-2][1] == len(DP)-3:
            break

    ret = len(DP)-1
    nret = DP[ret][1]
    while nret > 0:
        ret = nret
        nret = DP[ret][1]

    return ret*T


evaluate(fsol)
evaluate(fdp)
savefig('result.png')
```

## The Conclusion

TODO

---

<script>MathJax = {tex: {inlineMath: [['$', '$'], ['\\(', '\\)']]}};</script>
<script id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/tex-chtml.js"></script>
