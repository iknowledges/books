# Appendix C: Fundamentals of Mathematical Statistics

## C.2 Finite Sample Properties of Estimators

### Estimators and Estimates

Given a random sample $\{Y_1, Y_2, …, Y_n\}$drawn from a population distribution that depends on an unknown parameter $\theta$, an **estimator** of $\theta$ is a rule that assigns each possible outcome of the sample a value of $\theta$.

- *Example of an estimator*

Let $\{Y_1,…,Y_n\}$ be a random sample from a population with mean $\mu$. A natural estimator of $\mu$ is the average of the random sample:

$$
\bar Y=n^{-1}\sum_{i=1}^nY_i
$$

The sample average $\bar Y$ is now viewed as an estimator. 

For actual data outcomes $\{y_1, …, y_n\}$, the **estimate** is just the average in the sample: $\bar y=(y_1+y_2+\cdots+y_n)/n$

More generally, an estimator $W$ of a parameter $\theta$  can be expressed as an abstract mathematical formula:

$$
W=h(Y_1,Y_2,\cdots,Y_n)
$$

for some known function $h$ of the random variables $Y_1,Y_2,\cdots,Y_n$.

---

### Unbiasedness

**Unbiased estimator**: An estimator, $W$ of $\theta$, is an unbiased estimator if

$$
E(W)=\theta,
$$

for all possible values of $\theta$.

**Bias of an estimator**: If W is a biased estimator of u, its bias is defined as

$$
Bias(W)\equiv E(W)-\theta.
$$

Letting $\{Y_1, …, Y_n\}$ denote the random sample from the population with $E(Y)=\mu$  and $Var(Y)=\sigma^2$, define the estimator as

$$
S^2=\frac{1}{n-1}\sum_{i=1}^n(Y_i-\bar Y)^2
$$

which is usually called the **sample variance**.

---

### Efficiency

**Relative efficiency:** If $W_1$ and $W_2$ are two unbiased estimators of $\theta$, $W_1$ is efficient relative to $W_2$ when $Var(W_1) \leq Var(W_2)$ for all $\theta$, with strict inequality for at least one value of $\theta$.

One way to compare estimators that are not necessarily unbiased is to compute the **mean squared error (MSE)** of the estimators. If W is an estimator of $\theta$, then the MSE of W is defined as $MSE(W)=E[(W-\theta)^2]$.

It can be shown that $MSE(W)=Var(W)+[Bias(W)]^2$, so that MSE(W) depends on the variance and bias.

## C.3 Asymptotic or Large Sample Properties of Estimators

### Consistency

**Consistency**: Let $W_n$ be an estimator of $\theta$ based on a sample $Y_1, Y_2, …, Y_n$ of size n. Then, $W_n$ is a **consistent estimator** of $\theta$ if for every $\epsilon$,

$$
P(|W_n-\theta|>\epsilon)\to0 \quad as\quad n\to\infty.
$$

When $W_n$ is consistent, we also say that $\theta$ is the **probability limit** of $W_n$, written as $\plim(W_n)=\theta$.

It means that the distribution of $W_n$ becomes more and more concentrated about $\theta$, which roughly means that for larger sample sizes, $W_n$ is less and less likely to be very far from $\theta$. 

If $W_n$ is an unbiased estimator of $\theta$ and $Var(W_n)\to 0$ as $n\to\infty$, then $\plim(W_n)=\theta$.

**law of large numbers**: Let $Y_1, Y_2, …, Y_n$ be independent, identically distributed  random variables with mean $\mu$. Then,

$$
\plim(\bar Y_n)=\mu.
$$

**Property PLIM.1**: Let $\theta$ be a parameter and define a new parameter, $\gamma=g(\theta)$, for some continuous function $g(\theta)$. Suppose that $\plim(W_n)=\theta$. Define an estimator of $\gamma$ by $G_n=g(W_n)$. Then,

$$
\plim(G_n)=\gamma.
$$

This is often stated as

$$
\plim g(W_n)=g(\plim W_n)
$$

for a continuous function $g(\theta)$.

**Property PLIM.2**: If $\plim(T_n)=\alpha$ and $\plim(U_n)=\beta$, then

$$
\begin{aligned}
(i)&\plim(T_n+U_n)=\alpha+\beta\\
(ii)&\plim(T_nU_n)=\alpha\beta\\
(iii)&\plim(T_n/U_n)=\alpha/\beta,provided\quad\beta\neq 0
\end{aligned}
$$

### Asymptotic Normality

**Asymptotic Normality**: Let $\{Z_n: n=1, 2, …\}$ be a sequence of random variables, such that for all numbers z,

$$
P(Z_n\leq z)\to\Phi(z)\quad as\quad n\to\infty,
$$

where $\Phi(z)$ is the standard normal cumulative distribution function. Then, $Z_n$ is said to have an **asymptotic standard normal distribution**. 

**Central Limit Theorem**: Let $\{Y_1, Y_2, …, Y_n\}$ be a random sample with mean $\mu$ and variance $\sigma^2$. Then,

$$
Z_n=\frac{\bar Y_n-\mu}{\sigma/\sqrt n}
$$

has an asymptotic standard normal distribution.

CLT states that the average from a random sample for any population (with finite variance), when standardized, has an asymptotic standard normal distribution.

---

## C.4 General Approaches to Parameter Estimation

### Method of Moments

Generally, **method of moments** estimation proceeds as follows. The population parameter $\theta$ is shown to be related to some expected value in the distribution of Y, usually $E(Y)$ or $E(Y^2)$. We replace the population moment, $\theta$, with its sample counterpart, $E(Y)$ or $E(Y^2)$. This is where the name “method of moments” comes from.

### Maximum likelihood

Let $\{Y_1, Y_2, …, Y_n\}$ be a random sample from the population distribution $f(y;\theta)$. Now, define the **likelihood function** as 

$$
L(\theta;Y_1,\cdots,Y_n)=f(Y_1;\theta)f(Y_2;\theta)\cdots f(Y_n;\theta),
$$

which is a random variable because it depends on the outcome of the random sample $\{Y_1, Y_2, …, Y_n\}$. The **maximum likelihood estimator** of $\theta$, call it W, is the value of $\theta$ that maximizes the likelihood function.

The maximum likelihood principle says that, out of all the possible values for $\theta$, the value that makes the likelihood of the observed data largest should be chosen. 

The **log-likelihood function** is obtained by taking the natural log of the likelihood function:

$$
\log[L(\theta;Y_1,\cdots,Y_n)]=\sum_{i=1}^n\log[f(Y_i;\theta)],
$$

where we use the fact that the log of the product is the sum of the logs.

---

## C.5 Interval Estimation and Confidence Intervals

### The Nature of Interval Estimation

Suppose the population has a Normal($\mu$,1) distribution and let $\{Y_1, …, Y_n\}$ be a random sample from this population. The sample average, $\bar Y$, has a normal distribution with mean $\mu$ and variance 1/n: $\bar Y\sim Normal(\mu,1/n)$. From this, we can standardize $\bar Y$, and, because the standardized version of $\bar Y$ has a standard normal distribution, we have

$$
\begin{aligned}
&P(-1.96<\frac{\bar Y-\mu}{1/\sqrt n}<1.96)=0.95 \\
&P(\bar Y-1.96/\sqrt n<\mu<\bar Y+1.96/\sqrt n)=0.95
\end{aligned}
$$

We construct an interval estimate of $\mu$, which is obtained by plugging in the sample outcome of the average, $\bar y$. Thus,

$$
[\bar y-1.96/\sqrt n,\bar y+1.96/\sqrt n]
$$

is an example of an interval estimate of $\mu$. It is also called a 95% **confidence interval**.

The random interval $[\bar Y-1.96/\sqrt n,\bar Y+1.96/\sqrt n]$ contains m with probability 0.95. It is an example of an **interval estimator**.

A confidence interval is often interpreted as follows: “The probability that $\mu$ is in the interval is 0.95.”

Let the standard deviation $\sigma$ is known to be any value, the 95% confidence interval is

$$
[\bar y-1.96\sigma/\sqrt n,\bar y+1.96\sigma/\sqrt n]
$$

### Confidence Intervals for the Mean from a Normally Distributed Population

The t distribution arises from the fact that

$$
\frac{\bar Y-\mu}{S/\sqrt n}\sim t_{n-1}
$$

where $\bar Y$ is the sample average and $S$ is the sample standard deviation of the random sample $\{Y_1,…,Y_n\}$.

Let c denote the $97.5^{th}$ percentile in the $t_{n-1}$ distribution, the 95% confidence interval is calculated as

$$
[\bar y-c\cdot s/\sqrt n,\bar y+c\cdot s/\sqrt n],
$$

where $\bar y$ and $s$ are the values obtained from the sample.

In other words, c is the value such that 95% of the area in the $t_{n-1}$ is between -c and c: $P(-c<t_{n-1}<c)=0.95$.

More generally, let $c_\propto$ denote the $100(1-\alpha)$ percentile in the $t_{n-1}$ distribution. Then, a $100(1-\alpha)\%$ confidence interval is obtained as

$$
[\bar y-c_\propto s/\sqrt n,\bar y+c_\propto s/\sqrt n]
$$

Obtaining $c_\propto$ requires choosing $\alpha$ and knowing the degrees of freedom n-1.

Recall that $sd(\bar Y)=\sigma/\sqrt n$. Thus, $s/\sqrt n$ is the point estimate of $sd(\bar Y)$, The associated random variable, $S/\sqrt n$, is sometimes called the **standard error** of $\bar Y$. Because what shows up in formulas is the point estimate $s/\sqrt n$, we define the standard error of $\bar y$ as $se(\bar y)=s/\sqrt n$. Then, the confidence interval can be written in shorthand as

$$
[\bar y\pm c_\propto\cdot se(\bar y)].
$$

### Fundamentals of Hypothesis testing

We always denote the **null hypothesis** by $H_0$. In hypothesis testing, the null hypothesis plays a role similar to that of a defendant on trial in many judicial systems: just as a defendant is presumed to be innocent until proven guilty, the null hypothesis is presumed to be true until the data strongly suggest otherwise. 

In hypothesis testing, we can make two kinds of mistakes. First, we can reject the null hypothesis when it is in fact true. This is called a **Type I error**. The second kind of error is failing to reject $H_0$ when it is actually false. This is called a **Type II error**.

Hypothesis testing rules are constructed to make the probability of committing a Type I error fairly small. 

Generally, we define the **significance level** of a test as the probability of a Type I error; it is typically denoted by $\alpha$. Symbolically, we have
$$
\alpha=P(Reject\quad H_0|H_0)
$$
The right-hand side is read as: “The probability of rejecting $H_0$ given that $H_0$ is true.”

The **power of a test** is just one minus the probability of a Type II error. Mathematically,
$$
\pi(\theta)=P(Reject\quad H_0|\theta)=1-P(TypeII|\theta),
$$
where $\theta$ denotes the actual value of the parameter.

### Testing Hypotheses about the Mean in a Normal Population

A **test statistic**, denoted T, is some function of the random sample. When we compute the statistic for a particular outcome, we obtain an outcome of the test statistic, which we will denote t.

Given a test statistic, we can define a rejection rule that determines when $H_0$ is rejected in favor of $H_1$. All rejection rules are based on comparing the value of a test statistic, t, to a **critical value**, c. The values of t that result in rejection of the null hypothesis are collectively known as the **rejection region**.

Testing hypotheses about the mean $\mu$ from a Normal($\mu$, $\sigma^2$) population is straightforward. The null hypothesis is stated as
$$
H_0:\mu=\mu_0
$$
where $\mu_0$ is a value that we specify.

The rejection rule we choose depends on the nature of the alternative hypothesis.

**One-sided alternative**:
$$
\begin{aligned}
H_1:\mu>\mu_0\quad [C.32] \\
H_1:\mu<\mu_0\quad [C.33]
\end{aligned}
$$

**Two-sided alternative**:
$$
H_1:\mu\neq\mu_0
$$

Rather than working directly with $\bar y$, we use its standardized version, where $\sigma$ is replaced with the sample standard deviation, s:
$$
t=\sqrt n(\bar y-\mu_0)/s=(\bar y-\mu_0)/se(\bar y),
$$
where $se(\bar y)=s/\sqrt n$ is the standard error of $\bar y$.

We work with t because, under the null hypothesis, the random variable
$$
T=\sqrt n(\bar Y-\mu_0)/S
$$
has a $t_{n-1}$ distribution.

Now, suppose we have settled on a 5% significance level. Then, the critical value c is chosen so that $P(T>c|H_0)=0.05$; that is, the probability of a Type I error is 5%. Once we have found c, the rejection rule is
$$
t>c,
$$
where c is the 100(1-$\alpha$) percentile in a $t_{n-1}$ distribution; as a percent, the significance level is 100$\alpha$%.

The rejection rule is similar for the one-sided alternative (C.33). A test with a significance level of 100$\alpha$% rejects $H_0$ against (C.33) whenever
$$
t<-c
$$

For two-sided alternatives, a 100$\alpha$% level test is obtained from the rejection rule
$$
|t|>c,
$$
where $|t|$ is the absolute value of the t statistic. This gives a **two-tailed test**. We must now be careful in choosing the critical value: c is the 100(1-$\alpha$/2) percentile in the $t_{n-1}$ distribution.

We always say “fail to reject $H_0$” rather than “accept $H_0$.”

### Computing and Using p-Values

The **p-value** (sometimes called the *prob-value*) is the largest significance level at which we could carry out the test and still fail to reject the null hypothesis.

As an illustration, consider the problem of testing $H_0$: $\mu=0$ in a $Normal(\mu,\sigma^2)$ population. Our test statistic in this case is $T=\sqrt n\cdot\bar Y/S$, and we assume that n is large enough to treat T as having a standard normal distribution under $H_0$. Suppose that the observed value of T for our sample is t=1.52. We have
$$
p-value=P(T>1.52|H_0)=1-\Phi(1.52)=0.065
$$
where $\Phi(\cdot)$ denotes the standard normal cdf.

The p-value in this example has another useful interpretation: it is the probability that we observe a value of T as large as 1.52 when the null hypothesis is true.

Generally, small p-values are evidence against $H_0$, since they indicate that the outcome of the data occurs with small probability if $H_0$ is true. On the other hand, a large p-value is weak evidence against $H_0$.

Computing a p-value for a two-sided test is similar, but we must account for the two-sided nature of the rejection rule. For t testing about population means, the p-value is computed as
$$
P(|T_{n-1}|>|t|)=2P(T_{n-1}>|t|),
$$
where t is the value of the test statistic and $T_{n-1}$ is a t random variable.

#### Summary of How to Use p-Values: 

(i) Choose a test statistic T and decide on the nature of the alternative. This determines whether the rejection rule is t>c, t<-c, or |t|>c.
(ii) Use the observed value of the t statistic as the critical value and compute the corresponding significance level of the test. This is the p-value. If the rejection rule is of the form t>c, then p-value=P(T>t). If the rejection rule is t<-c, then p-value=P(T<t);  if the rejection rule is |t|>c, then p-value=P(|T|>|t|).
(iii) If a significance level $\alpha$ has been chosen, then we reject $H_0$ at the 100$\alpha$% level if $p-value<\alpha$. If $p-value\geq\alpha$, then we fail to reject $H_0$ at the 100$\alpha$% level. Therefore, it is a small p-value that leads to rejection.