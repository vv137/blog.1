---
title: "Euler-Maclaurin Summation Formula"
layout: post
tags: ["Mathematics", "Analysis"]
use_math: true
hidden: false
---


급수와 적분은 근본적으로 이산적인 대상과 연속적인 대상을 다루기에
다르다. 하지만 적분판정법만 보더라도 급수와 적분은 꽤나 밀접한 관계가
있다는 것을 느낄(?) 수 있다. Euler-Maclaurin 합 공식은 이러한 두
대상을 이어주는 역할을 한다. 본문에서는 Euler-Maclaurin 공식을
유도[^1]하고 이를 바탕으로 자연수 $p$-제곱의 합을 구하는 방법인
Faulhaber의 공식[^2]을 증명한다.

---

## Introduction

Euler-Maclaurin summation formula gives an estimation of the sum
$\sum ^N _{i=n} f(i)$ in terms of the integral $\int ^N _n f(x) \; dx$
and correction terms. It was discovered independently by Euler and
Maclaurin. Leonhard Euler discovered this formula in 1735[^5] to compute
slowly converging infinite series[^6] and Colin Maclaurin discovered it
in 1742[^7] to use to calculate integrals.

## High school students' recursive approach to the Faulhaber's formula

Here, we only will consider the case $p=4$. The cases $p=1$, $p=2$,
$p=3$ are considered familiar to everyone, so we will skip.

Using the binomial theorem, we find
$$(k+1)^5 = k^5 + 5k^4 + 10k^3 + 10k^2 + 5k + 1 .$$ We subtract $k^5$
from both hand sides to get following equation:
$$(k+1)^5 - k^5 = 5k^4 + 10k^3 + 10k^2 + 5k + 1 .$$

Put positive numbers from $1$ to $n$ in $k$ and sum each results:
$$\begin{aligned}
    \nonumber
    (n+1)^5 - n^5 &= 5n^4 + 10n^3 + 10n^2 + 5n + 1 \\
    \nonumber
    n^5 - (n-1)^5 &= 5(n-1)^4 + 10(n-1)^3 + 10(n-1)^2 + 5(n-1) + 1 \\
    \nonumber
    & \vdots \\
    \nonumber
    3^5 - 2^5 &= 5 \cdot 2^4 + 10 \cdot 2^3 + 10 \cdot 2^2 + 5 \cdot 2^1 + 1 \\
    \nonumber
    2^5 - 1^5 &= 5 \cdot 1^4 + 10 \cdot 1^3 + 10 \cdot 1^2 + 5 \cdot 1^1 + 1 \\
    (n+1)^5 - 1 &= 5 \sum ^n _{k=1} k^4 + 10 \sum ^n _{k=1} k^3 + 10 \sum ^n _{k=1} k^2 + 5 \sum ^n _{k=1} k + n .\end{aligned}$$
We already know the formulae of $\sum_k k^3$, $\sum_k k^2$, $\sum_k k$.
Substitute every sum($\sum$) to the closed formulae:
$$\sum ^n _{k=1} k^4 = \frac{(n+1)^5}{5} - \frac{1}{5} - 2 S_3(n) - 2 S_2(n) - S_1(n) - \frac{1}{5} .$$
Here we denote $S_p(n) := \sum ^n _{k=1} k^p$. $$\begin{aligned}
    \nonumber
    S_4(n) &= \frac{n^5}{5} + n^4 + 2n^3 + 2n^2 + n + \frac{1}{5} - \frac{1}{5} - 2 S_3(n) - 2 S_2(n) - S_1(n) - \frac{1}{5} \\
    \nonumber
    &= \frac{n^5}{5} + (1 - 1/2) n^4 + (2 - 1 - 2/3) n^3 + (2 - 1/2 - 1 - 1/2) n^2 \\
    \nonumber
    &+ (1 - 1/3 - 1/2 - 1/5)n \\
    &= \frac{1}{5} n^5 + \frac{1}{2} n^4 + \frac{1}{3} n^3 - \frac{1}{30} n\end{aligned}$$

## Bernoulli Numbers

The Bernoulli numbers $B_n$ are rational numbers that can be defined as
coefficients in the following power series expansion:
$$\label{eq:generating}
    \frac{x}{e^x-1} = \sum ^\infty _{n=0} B_n \frac{x^n}{n!}$$ These
numbers are important in many fields of mathematics.

It is not easy to find the coefficients in the right hand side of
equation [\[eq:generating\]](##eq:generating){reference-type="ref"
reference="eq:generating"} by differentiation. However, it is easy to
write Taylor series for the reciprocal of the left hand side of equation
[\[eq:generating\]](##eq:generating){reference-type="ref"
reference="eq:generating"}:
$$\frac{e^x-1}{x} = \frac{1}{x} \sum ^\infty _{k=1} \frac{x^k}{k!} = \sum ^\infty _{k=0} \frac{x^k}{(k+1)!} = 1 + \frac{x}{2} + \frac{x^2}{6} + \frac{x^3}{24} + \cdots$$
Thus, the Bernoulli numbers can be calculated in recurssive manner by
equatin to zero the coefficients at positive powers of $x$ in the
identity $$\begin{aligned}
    \nonumber
    1 &= \frac{x}{e^x-1} \frac{e^x-1}{x} = \left( 1 + \frac{x}{2} + \frac{x^2}{6} + \frac{x^3}{24} + \cdots \right) \left( B_0 + B_1 x + \frac{B_2}{2} x^2 + \cdots \right) \\
    &= B_0 + \left( \frac{B_0}{2!0!} + \frac{B_1}{1!1!} \right) x + \left( \frac{B_0}{3!0!} + \frac{B_0}{2!1!} + \frac{B_0}{1!2!} \right) x^2 + \cdots .\end{aligned}$$
From here, $B_0 = 1$, $B_1 = -1/2$, $B_2 = 1/6$, $B_3 = 0$,
$B_4 = -1/30$, etc. Note that $B_1$ is the only non-zero Bernoulli
number with an odd subscript.

## Operators

If $f(x)$ is a good function (대충 아무 생각 없이 미분과 적분을 적절하게
할 수 있다는 뜻.), then the correspondence
$$f(x) \longrightarrow f'(x) := \frac{d}{dx} f(x)$$ can be regarded as
the operator of differentiation $$\hat{D} := \frac{d}{dx}$$ that acts on
the function and transforms it into derivative. Also, given $\hat{D}$,
we can naturally define the powers of the operator of differentiation
$$\hat{D}^2 f(x) = \hat{D} ( \hat{D} f(x) ) = \frac{d^2}{dx^2} f(x)$$ or
in general, $$\hat{D}^n = \frac{d^n}{dx^n} .$$ Also, for good function
$g(x)$, we can define a function of the operator of differentiation as
following:
$$g(x) = \sum ^\infty _{n=0} a_n x^n \implies g(\hat{D}) = \sum ^\infty _{n=0} a_n \hat{D}^n .$$

Let's consider the exponential function of $\hat{D}$:
$$\hat{T} := e^{\hat{D}} = \sum ^\infty _{n=0} \frac{\hat{D}^n}{n!} .$$
When we apply $\hat{T}$ to a good function $f(x)$,
$$\hat{T} f(x) = \sum ^\infty _{n=0} \frac{1}{n!} \left( \hat{D}^n f(x) \right) = \sum ^\infty _{n=0} \frac{1}{n!} \frac{d^n f}{dx^n} .$$
The last expression is just a Taylor series for $f(x+1)$. Thus,
$$\hat{T} f(x) = f(x+1),$$ and $\hat{T}$ can be regarded as the shift
operator. For a positive integer $n$, shifting by $n$ can be considered
as sthe result of operator $\hat{T}$: $$f(x+n) = \hat{T}^n f(x) .$$

## Summation of series in terms of operator $\hat{D}$

We can now formally write[^8] $$\begin{aligned}
    \nonumber
    \sum ^\infty _{n=0} f(x+n) &= f(x) + f(x+1) + f(x+2) + \cdots \\
    \nonumber
    &= f(x) + \hat{T} f(x) + \hat{T}^2 f(x) + \cdots \\
    &= \left( 1 + \hat{T} + \hat{T}^2 + \cdots \right) f(x) = \frac{1}{1-\hat{T}} f(x) = \frac{1}{1-e^{\hat{D}}} f(x) .\end{aligned}$$
Treating $\hat{D}$ as an ordinary variable, and using Bernoulli numbers,
we obtain the expression: $$\begin{aligned}
    \nonumber
    \frac{1}{1-e^{\hat{D}}} &= -\frac{1}{\hat{D}} \frac{\hat{D}}{e^{\hat{D}}-1} = -\frac{1}{\hat{D}} \left( 1 - \frac{1}{2} \hat{D} + \sum ^\infty _{n=2} \frac{B_n}{n!} \hat{D}^n \right) \\
    &= -\frac{1}{\hat{D}} + \frac{1}{2} - \sum ^\infty _{n=2} \frac{B_n}{n!} \hat{D}^{n-1} .\end{aligned}$$
It is natural to assume that $\hat{D}$ satisfies the relation
$$\hat{D} \left( \frac{1}{\hat{D}} f(x) \right) = \frac{\hat{D}}{\hat{D}} f(x) = f(x) .$$
Therefore, $\frac{1}{\hat{D}}$ has to be an inverse operator to
differentiation, that is integration.
$$\frac{1}{\hat{D}} f(x) = \int f(x) \; dx + C .$$ We need to fix an
integration constant. As we see later, we obtain consistent results, if
$$-\frac{1}{\hat{D}} f(x) = \int ^x _\infty f(x) \; dx$$ Collecting the
results together, we get $$\label{eq:form_1}
    \sum ^\infty _{n=0} f(x+n) = \int ^\infty _x f(x) \; dx + \frac{1}{2} f(x) - \sum ^\infty _{n=2} \frac{B_n}{n!} \frac{d^{n-1}}{dx^{n-1}} f(x) .$$

## The Euler-Maclaurin summation formula

Equation [\[eq:form_1\]](##eq:form_1){reference-type="ref"
reference="eq:form_1"} is the Euler-Maclaurin summation formula. It can
be rewritten for the case of a finite sum as following:
$$\begin{aligned}
    \nonumber
    \sum ^N _{k=n} f(k) &= \sum ^\infty _{k=n} f(k) - \sum ^\infty _{k=N+1} f(k) \\
    \nonumber
    &= \sum ^\infty _{k=n} f(k) - \sum ^\infty _{k=N} f(k) + f(N) \\
    \nonumber
    &= \int ^\infty _x f(x) \; dx - \int ^\infty _N f(x) \; dx + \frac{1}{2} f(n) - \frac{1}{2} f(N) + f(N) \\
    \nonumber
    &- \sum ^\infty _{n=2} \frac{B_n}{n!} \left[ \frac{d^{n-1}}{dx^{n-1}} f(x) \right] _{x=n} + \sum ^\infty _{n=2} \frac{B_n}{n!} \left[ \frac{d^{n-1}}{dx^{n-1}} f(x) \right] _{x=N} \\
    \nonumber
    &= \int ^N _n f(x) \; dx + \frac{1}{2} \left( f(N) + f(n) \right) \\
    &+ \sum ^\infty _{n=2} \frac{B_n}{n!} \left( f^{(n-1)} (N) - f^{(n-1)} (n) \right) .\end{aligned}$$

## Faulhaber's formula

Faulhaber's formula, named after the early 17th century mathematician
Johann Faulhaber, expresses the sum of the p-th powers of the first n
positive integers: $$\sum ^n _{k=1} k^p = 1^p + 2^p + \cdots + n^p .$$
Now, we will derive Faulhaber's formula from the Euler-Maclaurin
summation formula. In this case, $f(x) = x^p$. $$\begin{aligned}
    \nonumber
    \sum ^n _{k=1} k^p &= \sum ^n _{k=0} k^p \\
    \nonumber
    & = 1^p + 2^p + \cdots + n^p \\
    \nonumber
    &= \int ^n _0 x^p \; dx + \frac{n^p}{2} + \sum ^p _{i=2} \frac{B_i}{i!} \frac{p!}{(p-i+1)!} n^{p-i+1} \\
    &= \frac{n^{p+1}}{p+1} + \frac{n^p}{2} + \sum ^p _{i=2} \frac{B_i}{i!} \frac{p!}{(p-i+1)!} n^{p-i+1}\end{aligned}$$
We get following formulae:
$$\sum ^n _{k=1} k = \frac{n^2}{2} + \frac{n}{2} = \frac{n(n+1)}{2} ,$$
$$\sum ^n _{k=1} k^2 = \frac{n^3}{3} + \frac{n^2}{2} + \frac{1}{6} \frac{2!}{2!1!} n = \frac{n(n+1)(2n+1)}{6},$$
$$\sum ^n _{k=1} k^3 = \frac{n^4}{4} + \frac{n^3}{2} + \frac{1}{6} \frac{3!}{2!2!} n^{3-2+1} + 0 = \frac{n^4 + 2n^3 + n^2}{4} = \left( \frac{n(n+1)}{2} \right) ^2 .$$
They are familiar formulae for high school students.

## The sum of the $4$-th power of the first $n$ positive integers: The Euler-Maclaurin formula approach

$$\begin{aligned}
    \nonumber
    \sum ^n _{k=1} k^4 &= \frac{n^5}{5} + \frac{n^4}{2} + \frac{1}{6} \frac{4!}{2!3!} n^{4-2+1} - \frac{1}{30} \frac{4!}{4!1!} n^{4-4+1} \\
    &= \frac{n^5}{5} + \frac{n^4}{2} + \frac{n^3}{3} - \frac{n}{30}\end{aligned}$$
We get the same result as before.

## Appendix: Some Bernoulli numbers

For odd $n$, $B_n = 0$ except $B_1 = -\frac{1}{2}$.

    $n$    $0$        $1$              $2$              $4$              $6$               $8$              $10$               $12$               $14$
  ------- ----- ---------------- --------------- ----------------- ---------------- ----------------- ---------------- --------------------- ---------------
   $B_n$   $1$   $-\frac{1}{2}$   $\frac{1}{6}$   $-\frac{1}{30}$   $\frac{1}{42}$   $-\frac{1}{30}$   $\frac{5}{66}$   $-\frac{691}{2730}$   $\frac{7}{6}$

## Appendix: The remainder term

The remainder term arises because the integral is usually not exactly
equal to the sum. The formula may be derived by applying repeated
integration by parts. The size of the remainder term can be estimated as
$$| R_p | \leq \frac{2 \zeta (p)}{(2 \pi)^2} \int ^N _n | f^{(p)}(x) | \; dx ,$$
where $\zeta$ denotes the Riemann zeta function. This remainder term is
valid when $p > 1$.

[^1]: 정확하진 않지만 이쯤에서 넘어가자.

[^2]: Johann Faulhaber (1631). Academia Algebrae - Darinnen die
    miraculosische Inventiones zu den höchsten Cossen weiters continuirt
    und profitiert werden.

[^3]: MIMIC

[^4]: Sungkyunkwan University, Department of Physics, Suwon

[^5]: L. Euler, \"Inventio summae cuiusque seriei ex dato termino
    generali (Finding the sum of any series from a given general
    term),\" Commentarii academiae scientiarum Petropolitanae
    (Commentary of the St. Petersburg Scientist Academy), vol. 8, pp.
    9--22, Oct. 1735.

[^6]: The series is now called as the Riemann zeta function, $\zeta(s)$.
    He was solving Basel problem and justified the result with the
    approximated value which calculated with the Euler-Maclaurin
    formula.

[^7]: C. Maclaurin, A Treatise on Fluxions, Edinburgh: T. W. and T.
    Ruddimans, 1742.

[^8]: Of course, we can try a finite sum instead of the infinite sum.
