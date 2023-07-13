# Chapter 3: Multiple Regression Analysis: Estimation

## 3.1 Motivation for Multiple Regression

### The Model with Two Independent Variables
Generally, we can write a model with two independent variables as
$$
y=\beta_0+\beta_1 x_1+\beta_2 x_2+u.
$$
where 
- $\beta_0$ is the intercept.
- $\beta_1$ measures the change in y with respect to $x_1$, holding other factors fixed. 
- $beta_2$ measures the change in y with respect to $x_2$, holding other factors fixed.

In the model with two independent variables, the key assumption about how u is related to $x_1$ and $x_2$ is
$$
E(u|x_1,x_2)=0.
$$

The condition means that, for any values of $x_1$ and $x_2$ in the population, the average of the unobserved factors is equal to zero.

### The Model with k Independent Variables

The general **multiple linear regression model** (also called the *multiple regression model*) can be written in the population as
$$
y=\beta_0+\beta_1 x_1+\beta_2 x_2+\cdots+\beta_k x_k+u,
$$
where  
- $\beta_0$ is the intercept. 
- $\beta_1$ is the parameter associated with $x_1$. 
- $\beta_2$ is the parameter associated with $x_2$, and so on. 

The key assumption for the general multiple regression model is easy to state in terms of a conditional expectation:
$$
E(u|x_1,x_2,\cdots,x_k)=0.
$$

## 3.2 Mechanics and Interpretation  of Ordinary Least Squares

### Obtaining the OLS Estimates

In the general case with k independent variables, we seek estimates $\hat\beta_0,  \hat\beta_1, …, \hat\beta_k$ in the equation
$$
\hat y=\hat\beta_0+\hat\beta_1 x_1+\hat\beta_2 x_2+\cdots+\hat\beta_k x_k.\quad [3.11]
$$
The OLS estimates, k+1 of them, are chosen to minimize the sum of squared residuals:
$$
\sum_{i=1}^n(y_i-\hat\beta_0-\hat\beta_1 x_{i1}-\cdots-\hat\beta_k x_{ik})^2.
$$
As in simple regression analysis, equation (3.11) is called the **OLS regression line** or the **sample regression function (SRF)**. We will call $\beta_0$ the **OLS intercept estimate** and $\beta_1, … ,\beta_k$ the **OLS slope estimates**.

### Interpreting the OLS Regression Equation

The OLS regression line is
$$
\hat y=\hat\beta_0+\hat\beta_1 x_1+\hat\beta_2 x_2+\cdots+\hat\beta_k x_k.
$$
Written in terms of changes,
$$
\Delta\hat y=\hat\beta_0+\hat\beta_1\Delta x_1+\hat\beta_2\Delta x_2+\cdots+\hat\beta_k\Delta x_k.
$$

### OLS Fitted Values and Residuals

The **residual** for observation i is defined as,
$$
\hat u_i=y_i-\hat y_i,
$$
which $y_i$ is the actual value, $\hat y_i$ is the fitted or predicted value.

The OLS fitted values and residuals have some important properties:
1. The sample average of the residuals is zero and so  $\bar y=\bar\hat y$. 
2. The sample covariance between each independent variable and the OLS residuals is zero. Consequently, the sample covariance between the OLS fitted values and the OLS residuals is zero. 
3. The point $(\bar x_1, \bar x_2, …,\bar x_k, \bar y)$ is always on the OLS regression line: $\bar y=\hat\beta_0+\hat\beta_1\bar x_1+\hat\beta_2\bar x_2+\cdots+\hat\beta_k\bar x_k$.

### Goodness-of-Fit

As with simple regression, we can define the **total sum of squares (SST)**, the **explained sum of squares (SSE)**, and the **residual sum of squares** or **sum of squared residuals (SSR)** as
$$
\begin{aligned}
&SST=\sum_{i=1}^n(y_i-\bar y_i)^2 \\
&SSE=\sum_{i=1}^n(\hat y_i-\bar y_i)^2 \\
&SSR=\sum_{i=1}^n u_i^2.
\end{aligned}
$$

Using the same argument as in the simple regression case, we can show that
$$
SST=SSE+SSR.
$$

Just as in the simple regression case, the **R-squared** is defined to be
$$
R^2=\frac{SSE}{SST}=1-\frac{SSR}{SST},
$$
and it is interpreted as the proportion of the sample variation in $y_i$ that is explained by the OLS regression line. 

$R^2$ can also be shown to equal the squared correlation coefficient between the actual $y_i$ and the fitted values  $\hat y_i$:
$$
R^2=\frac{[\sum_{i=1}^n(y_i-\bar y_i)(\hat y_i-\bar y_i)]^2 }{[\sum_{i=1}^n(y_i-\bar y_i)^2][\sum_{i=1}^n(\hat y_i-\bar y_i)^2]}
$$

## 3.3 The Expected Value of the OLS Estimators

**Assumption MlR.1**: Linear in Parameters

The model in the population can be written as
$$
y=\beta_0+\beta_1 x_1+\beta_2 x_2+\cdots+\beta_k x_k+u,
$$
where $\beta_0,\beta_1,\beta_2,\cdots,\beta_k$ are the unknown parameters (constants) of interest and $u$ is an unobserved random error or disturbance term.

**Assumption MlR.2**: Random Sampling

We have a random sample of n observations, $\{(x_{i1}, x_{i2}, \cdots, x_{ik}, y_i): i=1, 2, \cdots, n\}$, following the population model in Assumption MLR.1.

**Assumption MlR.3**: No Perfect Collinearity

In the sample (and therefore in the population), none of the independent variables is constant, and there are no *exact linear* relationships among the independent variables.

**Assumption MlR.4**: Zero Conditional Mean

The error u has an expected value of zero given any values of the independent variables. In other words,
$$
E(u|x_1,x_2,\cdots,x_k)=0.
$$

**THEOREM 3.1**: UNBIASEDNESS OF OLS

Under Assumptions MLR.1 through MLR.4,
$$
E(\hat\beta_j)=\beta_j,\quad j=0,1,\cdots,k,
$$
for any values of the population parameter $\beta_j$. In other words, the OLS estimators are unbiased estimators of the population parameters.

## 3.4 The Variance of the OLS Estimators

**Assumption MlR.5**: Homoskedasticity
The error u has the same variance given any values of the explanatory variables. In other words, 
$$
Var(u|x1_, …, x_k)=\sigma^2.
$$

**THEOREM 3.2**: SAMPLING VARIANCES OF THE OLS SLOPE ESTIMATORS
Under Assumptions MLR.1 through MLR.5, conditional on the sample values of the independent variables,
$$
Var(\hat\beta_j)=\frac{\sigma^2}{SST_j(1-R_j^2)},
$$
for $j=1,2,\cdots,k$, where $SST_j=\sum_{i=1}^n(x_{ij}-\bar x_j)^2$ is the total sample variation in $x_j$, and  $R_j^2$ is the R-squared from regressing $x_j$ on all other independent variables (and including an intercept).

The **variance inflation factor** (VIF) for slope coefficient j is simply $VIF_j=1/(1-R_j^2)$.

### Estimating $\sigma^2$: Standard Errors of the OLS Estimators

**THEOREM 3.3**: UNBIASED ESTIMATION OF $\sigma^2$
Under the Gauss-Markov assumptions MLR.1 through MLR.5, $E(\hat\sigma^2)=\sigma^2$.

The positive square root of  $\hat\sigma^2$, denoted  $\hat\sigma$, is called the **standard error of the regression** (SER).

## 3.5 Efficiency of OLS: The Gauss-Markov Theorem

**THEOREM 3.4**: GAUSS-MARKOV THEOREM
Under Assumptions MLR.1 through MLR.5,  $\hat\beta_0,  \hat\beta_1, …,  \hat\beta_k$ are the best linear unbiased estimators (BLUEs) of $\beta_0, \beta_1, …, \beta_k$, respectively.