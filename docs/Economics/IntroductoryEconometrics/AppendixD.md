# Appendix D: Summary of Matrix Algebra

## D.2 Matrix Operations

### Trace

**Definition D.8 (Trace)**. For any $n\times n$ matrix A, the **trace of a matrix** A, denoted tr(A), is the sum of its diagonal elements. Mathematically,
$$
tr(A)=\sum_{i=1}^n a_{ii}.
$$

**Properties of Trace**
1. $tr(I_n)=n$
2. $tr(A^\prime)=tr(A)$
3. $tr(A+B)=tr(A)+tr(B)$
4. $tr(\alpha A)=\alpha tr(A)$
5. $tr(AB)=tr(BA)$, where A is $m\times n$ and B is $n\times m$.

### Inverse

**Definition D.9 (inverse)**. An $n\times n$ matrix A has an **inverse**, denoted $A^{-1}$, provided that $A^{-1}A=I_n$ and $AA_{-1}=I_n$. In this case, A is said to be *invertible* or *nonsingular*. Otherwise, it is said to be  *noninvertible* or *singular*.

**Properties of Inverse**
1. If an inverse exists, it is unique;
2. $(\alpha A)^{-1}=(1/\alpha)A^{-1}$, if $\alpha\neq 0$ and A is invertible;
3. $(AB)^{-1}=B^{-1}A^{-1}$, if A and B are both $n\times n$ and invertible;
4. $(A^\prime)^{-1}=(A^{-1})^\prime$

### D.3 Linear Independence and Rank of a Matrix

**Definition D.10 (Linear independence)**. Let $\{x_1, x_2,…, x_r\}$ be a set of $n\times 1$ vectors. These are **linearly independent vectors** if, and only if,
$$
\alpha_1 x_1+\alpha_2 x_2+\cdots+\alpha_r x_r=0
$$
implies that $\alpha_1=\alpha_2=\cdots =\alpha_r=0$.  If (D.2) holds for a set of scalars that are not all zero, then $\{x_1, x_2, …, x_r\}$ is *linearly dependent*.

**Definition D.11 (Rank)**
(i) Let A be an $n\times m$ matrix. The **rank of a matrix** A, denoted rank(A), is the maximum number of linearly independent columns of A. 
(ii) If A is $n\times m$ and rank(A)=m, then A has *full column rank*.

**Properties of Rank**
 1. $rank(A^\prime)=rank(A)$; 
 2. If A is $n\times k$, then $rank(A)\leq \min(n,k)$; 
 3. If A is $k\times k$ and $rank(A)=k$, then A is invertible.

### D.4 Quadratic Forms and Positive Definite Matrices

**Definition D.12 (Quadratic Form)**. Let A be an $n\times n$ symmetric matrix. The **quadratic form** associated with the matrix A is the real-valued function defined for  all $n\times 1$ vectors x:
$$
f(\mathbf{x})=\mathbf{x}^\prime A\mathbf{x}=\sum_{i=1}^n a_{ii}x_i^2+2\sum_{i=1}^n\sum_{j>1}a_{ij}x_i x_j.
$$

**Definition D.13 (positive definite and positive Semi-definite)**
(i) A symmetric matrix A is said to be **positive definite (p.d.)** if $\mathbf{x}^\prime A\mathbf{x}>0$ for all $n\times 1$ vectors x except $\mathbf x=0$. 
(ii) A symmetric matrix A is **positive semi-definite (p.s.d.)** if $\mathbf{x}^\prime A\mathbf{x}\geq 0$ for all $n\times 1$ vectors.

#### Properties of Positive Pefinite and Positive Semi-Definite Matrices. 
1. A positive definite matrix has diagonal elements that are strictly positive, while a p.s.d. matrix has nonnegative diagonal elements; 
2. If $A$ is p.d., then $A^{-1}$ exists and is p.d.; 
3. If X is  $n\times k$, then $X^\prime X$ and $XX^\prime$ are p.s.d.;
4. If X is $n\times k$ and $rank(X)=k$, then $X^\prime X$ is p.d. (and therefore nonsingular).

### D.5 Idempotent Matrices

**Definition D.14 (idempotent Matrix)**. Let A be an $n\times n$ symmetric matrix. Then A is said to be an idempotent matrix if, and only if, $AA=A$.

**Properties of Idempotent Matrices**. Let A be an $n\times n$ idempotent matrix. 
(1) $rank(A)= tr(A)$,
(2) A is positive semi-definite.

### D.6 Differentiation of Linear and Quadratic Forms

For a given $n\times 1$ vector a, consider the linear function defined by
$$
 f(\mathbf x)=\mathbf{a}^\prime\mathbf{x},
$$
for all $n\times 1$ vectors x. The derivative of f with respect to x is the $1\times n$ vector of partial derivatives, which is simply
$$
\frac{\partial f(\mathbf x)}{\partial\mathbf x}=\mathbf{a}^\prime.
$$

For an $n\times n$ symmetric matrix A, define the quadratic form
$$
g(\mathbf{x})=\mathbf{x}^\prime A\mathbf{x},
$$
Then,
$$
\frac{\partial g(\mathbf{x})}{\partial\mathbf x}=2\mathbf{x}^\prime A,
$$
which is a $1\times n$ vector.