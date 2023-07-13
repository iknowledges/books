# Appendix B: Fundamentals of Probability

## B.5 The Normal and Related Distributions

### The Normal Distribution

Mathematically, the pdf of X can be written as
$$
f(x)=\frac{1}{\sigma\sqrt{2\pi}}\exp[-(x-\mu)^2/2\sigma^2],-\infty<x<\infty,
$$
where $\mu=E(X)$ and $\sigma^2=Var(X)$. We say that X has a **normal distribution** with expected value $\mu$ and variance $\sigma^2$, written as $X\sim Normal(\mu,\sigma^2)$.

If X is a positive random variable, such as income, and Y=log(X) has a normal distribution, then we say that X has a *lognormal distribution*.

### The Standard Normal Distribution

If a random variable Z has a Normal(0,1) distribution, then we say it has a **standard normal distribution**. The pdf of a standard normal random variable is denoted $\phi(z)$, with $\mu=0$ and $\sigma^2=1$, it is given by
$$
\phi(z)=\frac{1}{\sqrt{2\pi}}\exp(-z^2/2),-\infty<z<\infty.
$$

The standard normal cumulative distribution function is denoted $\Phi(z)$ and is obtained as the area under $\phi(z)$, to the left of z,
$$
\Phi(z)=P(Z\leq z).
$$

The most important formulas are
$$
\begin{aligned}
&P(Z>z)=1-\Phi(z)\\
&P(Z<-z)=P(Z>z)\\
&P(a\leq Z\leq b)=\Phi(b)-\Phi(a)
\end{aligned}
$$

Another useful expression is that, for any c>0,
$$
\begin{aligned}
P(|Z|>c)&=P(Z>c)+P(Z<-c)\\
&=2\cdot P(Z>c)=2[1-\Phi(c)]
\end{aligned}
$$

**Property Normal.1**: If $X\sim Normal(\mu,\sigma^2)$, then $(X-\mu)/\sigma\sim Normal(0,1)$.

**Property Normal.2**: If $X\sim Normal(\mu,\sigma^2)$, then $aX+b\sim Normal(a\mu+b,a^2\sigma^2)$.

**Property Normal.3**: If X and Y are jointly normally distributed, then they are independent if, and only if, Cov(X,Y)=0.

**Property Normal.4**: Any linear combination of independent, identically distributed normal random variables has a normal distribution.

### The Chi-Square Distribution

Let $Z_i, i=1, 2,…,n$, be independent random variables, each distributed as standard normal. Define a new random variable as the sum of the squares of the $Z_i$:
$$
X=\sum_{i=1}^nZ_i^2.
$$
Then, X has what is known as a **chi-square distribution** with n **degrees of freedom** (or df for short). We write this as $X\sim \chi^2$.

It can be shown that if $X\sim \chi_n^2$, then the expected value of X is n, and the variance of X is 2n.

### The t Distribution

Let Z have a standard normal distribution and let X have a chi-square distribution with n degrees of freedom. Further, assume that Z and X are independent. Then, the random variable
$$
T=\frac{Z}{\sqrt{X/n}}
$$
has a **t distribution** with n degrees of freedom. We will denote this by $T\sim t_n$.

The expected value of a t distributed random variable is zero (strictly speaking, the expected value exists only for n>1), and the variance is n/(n-2) for n>2. (The variance does not exist for $n\leq 2$ because the distribution is so spread out.)

As the degrees of freedom gets large, the t distribution approaches the standard normal distribution.

### The F distribution

To define an F random variable, let $X_1\sim\chi_{k_1}^2$ and $X_2\sim\chi_{k_2}^2$ and assume that $X_1$ and $X_2$ are independent. Then, the random variable
$$
F=\frac{X_1/k_1}{X_2/k_2}
$$
has an **F distribution** with $(k_1,k_2)$ degrees of freedom. We denote this as $F\sim F_{k_1,k_2}$.

The order of the degrees of freedom in $F_{k_1,k_2}$ is critical. The integer k1 is called the *numerator degrees of freedom* because it is associated with the chi-square variable in the numerator. Likewise, the integer k2 is called the  *denominator degrees of freedom* because it is associated with the chi-square variable in the denominator.