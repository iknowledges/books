# Chapter 5. Multiple Regression Analysis: OLS Asymptotics

## 5.1 Consistency

**THEOREM 5.1** CONSISTENCY OF OLS:
Under Assumptions MLR.1 through MLR.4, the OLS estimator $\hat\beta_j$ is consistent for $\beta_j$, for all $j=0,1,...,k$.

**Assumption MLR.4'** Zero Mean and Zero Correlation:
$E(u)=0$ and $Cov(x_j,u)=0$, for $j=1,2,...,k$.

## 5.2 Asymptotic Normality and Large Sample Inference

**THEOREM 5.2** ASYMPTOTIC NORMALITY OF OLS:
Under the Gauss-Markov Assumptions MLR.1 through MLR.5,
(i)$\sqrt{n}(\hat\beta_j-\beta_j)\sim Normal(0,\sigma^2/a_j^2)$, where $\sigma^2/a_j^2>0$ is the **asymptotic variance** of $\sqrt n(\hat\beta_j-\beta_j)$; for the slope coefficients, $a_j^2=plim(n^{-1}\sum_{i=1}^n\hat{r}_{ij}^2)$, where the $\hat{r}_{ij}$ are the residuals from regressing $x_j$ on the other independent variables. We say that $\hat\beta_j$ is asymptotically normally distributed (see Appendix C);
(ii)$\sigma^2$ is a consistent estimator of $\sigma^2=Var(u)$;
(iii) For each j,
$$
(\hat\beta_j-\beta_j)/sd(\hat\beta_j)\sim Normal(0,1)
$$
and
$$
(\hat\beta_j-\beta_j)/se(\hat\beta_j)\sim Normal(0,1)
$$
where $se(\hat\beta_j)$ is the usual OLS standard error.

## 5.3 Asymptotic Efficiency of OLS

In the k regressor case, the class of consistent estimators is obtained by generalizing the OLS first order conditions:
$$
\sum_{i=1}^ng_j(x_i)(y_i-\tilde\beta_0-\tilde\beta_1x_{i1}-\cdots-\tilde\beta_kx_{ik})=0,j=0,1,\cdots,k,\quad[5.19]
$$
where $g_j(x_i)$ denotes any function of all explanatory variables for observation i.

**THEOREM 5.3** ASYMPTOTIC EFFICIENCY OF OLS:

Under the Gauss-Markov assumptions, let $\hat\beta_j$ denote estimators that solve equations of the form (5.19) and let $\hat\beta_​j$ denote the OLS estimators. Then for $j=0,1,2,...,k$, the OLS estimators have the smallest asymptotic variances: $Avar \sqrt n(\hat\beta_j-\beta_j)\leq Avar \sqrt n(\tilde\beta_j-\beta_j)$
