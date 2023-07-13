# Chapter 4. Multiple Regression Analysis: Inference

## 4.1 Sampling Distributions of the OLS Estimators

**Assumption MLR.6**: Normality
The population error u is independent of the explanatory variables $x_1, x_2, …, x_k$ and is  normally distributed with zero mean and variance $\sigma^2$: $u\sim Normal(0,\sigma^2)$.

For cross-sectional regression applications, Assumptions MLR.1 through MLR.6 are called the **classical linear model (CLM) assumptions**.

**THEOREM 4.1**: NORMAL SAMPLING DISTRIBUTIONS
Under the CLM assumptions MLR.1 through MLR.6, conditional on the sample values of the independent variables,
$$
\hat\beta_j\sim Normal[\beta_j,Var(\hat\beta_j)],
$$
where $Var(\hat\beta_j)$ was given in Chapter 3 [equation (3.51)]. Therefore,
$$
(\hat\beta_j-\beta_j)/sd(\hat\beta_j)\sim Normal(0,1).
$$

### 4.2 Testing Hypotheses about a Single Population Parameter: The t Test

**THEOREM 4.2**: t DISTRIBUTION FOR THE STANDARDIZED ESTIMATORS
Under the CLM assumptions MLR.1 through MLR.6,
$$
(\hat\beta_j-\beta_j)/se(\hat\beta_j)\sim t_{n-k-1}=t_{df},
$$
where $k+1$ is the number of unknown parameters in the population model $y=\beta_0+\beta1 x_1+\cdots+\beta_k x_k+u$(k slope parameters and the intercept $\beta_0$) and $n-k-1$ is the degrees of freedom(df).

### Testing Other Hypotheses about $\beta_j$

The general t statistic is usefully written as
$$
t=\frac{estimate-hypothesized value}{standard error}.
$$

### Testing against One-Sided Alternatives

In most applications, our primary interest lies in testing the **null hypothesis**
$$
H_0:\beta_j=0,
$$
where j corresponds to any of the k independent variables.
The statistic we use to test $H_0$ is called “the” **t statistic** or “the” **t ratio** of $\hat\beta_j$ and is defined as
$$
t_{\hat\beta_j}=\hat\beta_j/se(\hat\beta_j).
$$

### Two-Sided Alternatives

In applications, it is common to test the null hypothesis $H_0:\beta_j=0$ against a **two-sided alternative**; that is,
$$
H_1:\beta_j\neq 0.
$$

When the alternative is two-sided, the rejection rule for $H_0:\beta_j=0$ is
$$
|t_{\hat\beta_j}|>c,
$$
where $|\cdot|$ denotes absolute value and c is an appropriately chosen critical value.

If $H_0$ is rejected in favor of $H_1:\beta_j\neq 0$ at the 5% level, we usually say that “$x_j$ is **statistically significant**, or statistically different from zero, at the 5% level.” If $H_0$ is not rejected, we say that “$x_j$ is **statistically insignificant** at the 5% level.”

### Testing Other Hypotheses about $\beta_j$

Generally, if the null is stated as
$$
H_0:\beta_j=a_j,
$$
where $a_j$ is our hypothesized value of $\beta_j$, then the appropriate t statistic is
$$
t=(\hat\beta_j-a_j)/se(\hat\beta_j).
$$

### Computing p-Values for t Tests

The p-value is the probability of observing a t statistic as extreme as we did if the null hypothesis is true. This means that small p-values are evidence against the null; large p-values provide little evidence against $H_0$.

If $\alpha$ denotes the significance level of the test (in decimal form), then $H_0$ is rejected if p-value<$\alpha$; otherwise, $H_0$ is not rejected at the 100$\alpha$% level.

Some regression packages only compute p-values for two-sided alternatives. but it is simple to obtain the one-sided p-value: just divide the two-sided p-value by 2.

### 4.3 Confidence Intervals

Using the fact that $(\hat\beta_j^2-\beta_j)/se(\hat\beta_j)$ has a t distribution with n-k-1 degrees of freedom, simple manipulation leads to a confidence interval (CI) for the unknown $\beta_j$: a 95% confidence interval, given by
$$
\hat\beta_j\pm c\cdot se(\hat\beta_j),
$$
where the constant c is the 97.5th percentile in a $t _{n-k-1}$  distribution.

Once a confidence interval is constructed, it is easy to carry out two-tailed hypotheses tests. If the null hypothesis is $H_0: \beta_j=a_j$, then $H_0$ is rejected against $H_1: \beta_j\neq a_j$ at the 5% significance level if, and only if, $a_j$ is not in the 95% confidence interval.

### 4.4 Testing Hypotheses about a Single Linear  Combination of the Parameters

The hypothesis of interest is 
$$
H_0:\beta_1=\beta_2.
$$
The alternative of interest is
$$
H_1:\beta_1<\beta_2.
$$

To construct a t statistic for testing , we rewrite the null and alternative as $H_0: \beta_1-\beta_2=0$ and $H_1: \beta_1-\beta_2<0$, respectively. 
$$
t=\frac{\hat\beta_1-\hat\beta_2}{se(\hat\beta_1-\hat\beta_2)}.
$$

To find $se(\hat\beta_1-\hat\beta_2)$, we first obtain the variance of the difference.
$$
Var(\hat\beta_1-\hat\beta_2)=Var(\hat\beta_1)+Var(\hat\beta_2)-2Cov(\hat\beta_1,\hat\beta_2).\quad [4.22]
$$

The standard deviation of  $\hat\beta_1-\hat\beta_2$ is just the square root of (4.22), and, since $[se(\hat\beta_1)]^2$ is an unbiased estimator of $Var(\hat\beta_1)$, and similarly for $[se(\hat\beta_2)]^2$, we have
$$
se(\hat\beta_1-\hat\beta_2)=\{[se(\hat\beta_1)]^2+[se(\hat\beta_2)]^2-2s_{12}\}^{1/2}
$$
where $s_{12}$ denotes an estimate of $Cov(\hat\beta_1,\hat\beta_2)$.

## 4.5 Testing Multiple Linear Restrictions: The F Test

### Testing Exclusion Restrictions

Write the unrestricted model with k independent variables as
$$
y=\beta_0+\beta_1 x_1+\cdots+\beta_k x_k+u,\quad [4.34]
$$
the number of parameters in the unrestricted model is k+1.

Suppose that we have q exclusion restrictions to test (The order of the variables is arbitrary), the null hypothesis is stated as
$$
H_0:\beta_{k-q+1}=0,\cdots,\beta_k=0,
$$
which puts q exclusion restrictions on the model (4.34). 

When we impose the restrictions under $H_0$, we are left with the restricted model:
$$
y=\beta_0+\beta_1 x_1+\cdots+\beta_{k-q}x_{k-q}+u.
$$

The F statistic (or F ratio) is defined by
$$
F=\frac{(SSR_r-SSR_{ur})/q}{SSR_{ur}/(n-k-1)},
$$
where $SSR_r$ is the sum of squared residuals from the restricted model and $SSR_{ur}$ is the sum of squared residuals from the unrestricted model.

**numerator degrees of freedom**:
$$
q=df_r-df_{ur},
$$
which show that q is the difference in degrees of freedom between the restricted and unrestricted models.

**denominator degrees of freedom**:
$$
n-k-1=df_{ur}
$$

It is pretty clear from the definition of F that we will reject $H_0$ in favor of $H_1$ when F is sufficiently “large.”

Once c has been obtained, we reject $H_0$ in favor of $H_1$ at the chosen significance level if
$$
F>c.
$$

If $H_0$ is rejected, then we say that $x_{k-q+1}, …, x_k$ are **jointly statistically significant** (or just jointly significant) at the appropriate significance level.

### The R-Squared Form of the F Statistic

Using the fact that $SSR_r=SST(1-R_r^2)$ and $SSR_{ur}=SST(1-R_{ur}^2)$, we can obtain
$$
F=\frac{(R_{ur}^2-R_r^2)/q}{(1-R_{ur}^2)/(n-k-1)}=\frac{(R_{ur}^2-R_r^2)/q}{(1-R_{ur}^2)/df_{ur}}
$$
This is called the **R-squared form of the F statistic**.

### Computing p-Values for F Tests

In the F testing context, the p-value is defined as
$$
p-value=P(\tau>F),
$$
where we let $\tau$ denote an F random variable with (q,n-k-1) degrees of freedom, and F is the actual value of the test statistic.