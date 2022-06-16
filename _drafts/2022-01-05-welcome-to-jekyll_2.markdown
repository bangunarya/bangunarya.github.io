---
layout: post
title:  "Coherence Bound of Sensing Matrices from Spherical Harmonics and Wigner D-functions"
date:   2018-01-01 08:42:13 +0100 (2)
categories: jekyll update
---

In sparse recovery from underdetermined linear system of equation, basis pursuit or $$\ell_1$$-minimization is a convex optimization approach to guarantee that we can recover sparse solution, which can be written as

$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{x}}{\text{minimize}}
& &  \left\lVert \mathbf{x} \right\rVert_1 
& \text{subject to}
& & \mathbf{y} = \mathbf{A} \mathbf{x}
\end{aligned}
\end{equation*}
$$

A common technique to develop a mathematical proof for a recovery guarantee depends highly on the structure of the underdetermined matrix $$ \mathbf{A} \in \mathbb{C}^{m \times N} $$, where $$ m < N$$. Restricted Isometry Property (RIP) is commonly used as a fundamental building block to construct the argument. Intuitively, if a certain matrix fulfills RIP then the matrix only slightly affects the Euclidean norm of the vector $$ \mathbf{x}$$. However, it has been shown that constructing such deterministic matrix is difficult, as in the literature the construction of RIP matrix is always followed with a probabilistic approach, for instance the construction from Gaussian or sub-Gaussian distribution has been proven to fulfill RIP with high probability. 

In search of the RIP deterministic matrix is not only useful for a mathematical proof but also necessary for a practical point of view, since in general the construction of such matrix cannot be directly constructed from pure random distribtion. As an example, when considering spherical near-field antenna measurement we have to construct a matrix from certain functions, so called spherical harmonics $$Y_l^k (\theta,\phi)$$ or Wigner D-functions $$\mathrm{D}_l^{k,n}(\theta,\phi,\chi)$$ for degree $$l$$ and orders $$k,n$$. Aother metric yet easy to compute is called coherence, by which we characterize the property of the matrix by calculating normalized inner product of adjacent columns. Suppose we have matrix $$\mathbf A=[\mathbf{a}_1 \dots \mathbf{a}_N]\in\mbb C^{m\times N}$$, the coherence is given by

$$
\begin{equation*}
\begin{aligned}
& \underset{1 \leq iyj \leq N}{\text{max}}
& &  \frac{|\langle\mathbf{a}_i,\mathbf{a}_j\rangle}|}{\left\lVert \mathbf{a}_i \right\rVert_2  \left\lVert \mathbf{a}_j \right\rVert_2},
&end{aligned}
\end{equation*}
$$
$$
where the coherence is bounded by $$1$$ by using Cauchy-Schwarz and lower bounded by so-called Welch bound []. Deriving coherence bound for a structure matrix constructed from Wigner D-function and spherical harmonics is challenging since dependent variable on the functions with respect to angles and degree orders of the function. The matrix from Wigner D-functions can be constructed as follow

$$
\begin{equation}
 \mathbf{A} =
 \begin{pmatrix}
  \mathrm{D}_0^{0,0}(\theta_1,\phi_1,\chi_1) \quad \mathrm{D}_1^{-1,-1}(\theta_1,\phi_1,\chi_1) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_1,\phi_1,\chi_1)\\
  \mathrm{D}_0^{0,0}(\theta_2,\phi_2,\chi_2) \quad \mathrm{D}_1^{-1,-1}(\theta_2,\phi_2,\chi_2) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_2,\phi_2,\chi_2)\\
  \vdots\\
  \mathrm{D}_0^{0,0}(\theta_m,\phi_m,\chi_m) \quad \mathrm{D}_1^{-1,-1}(\theta_m,\phi_m,\chi_m) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_m,\phi_m,\chi_m)\\
\end{pmatrix}
\end{equation}
$$

The construction from spherical harmonics can be directly given by using relation 

$$
\begin{equation}\label{gener_SH}
\mathrm{D}_l^{k,n}(\theta,\phi,0) = (-1)^k \sqrt{\frac{1}{2\pi}}Y_{l}^{k}(\theta,\phi).
\end{equation}
$$

Since we are dealing with the inner product of adjacent columns consequently we have product of two Wigner D-functions. It turns out that the problem to find coherence bound on those matrices bears a strong resemblance from the angular momentum in quantum mechanics, where the product of Wigner D-functions can be represented by angular momentum coefficients, called Wigner 3j symbols given as follow

$$
\begin{equation}
\small
\begin{aligned}
 &\sum_{p=1}^m\overline{\mathrm{D}_{l_1}^{k_1,n_1}(\theta_p,\phi_p,\chi_p)}  \mathrm{D}_{l_2}^{k_2,n_2}(\theta_p,\phi_p,\chi_p)  \\
 &= C_{k_2,n_2}\sum_{\substack{\hat l=|l_2-l_1| }}^{l_1 + l_2} {\sqrt{\frac{(2l_1 + 1)(2l_2 +1)(2\hat{l} + 1)}{8 \pi^2}}} \\& \times \begin{pmatrix}
   l_1 & l_2 & \hat{l} \\
   -n_1 & n_2 & -\hat{n} 
  \end{pmatrix} \begin{pmatrix}
   l_1 & l_2 & \hat{l} \\
   -k_1 & k_2 & -\hat{k}
  \end{pmatrix}  \paran{\sum_{p=1}^m\mathrm{D}_{\hat{l}}^{\hat{k},\hat{n}}(\theta_p,\phi_p,\chi_p)},
\end{aligned}
\end{equation}
$$

Wigner 3j symbols are  denoted by {$ \begin{pmatrix}
   l_1 & l_2 & l_3 \\
   k_1 & k_2 & k_3
  \end{pmatrix} \in \R$}, and their exact formula is given in \cite[Section 7.10.2]{kennedy_hilbert_2013} or \cite{edmonds_angular_2016}. {In quantum mechanics, $l_i$'s and $k_i$'s are non-negative integers or half-odd numbers, however in this paper, we only focus on the case where they are all integers.} Despite their complex expressions, Wigner 3j symbols have a few useful properties. The so-called \textit{selection rules} state that Wigner 3j symbols $\begin{pmatrix}
   l_1 & l_2 & {l}_3 \\
   k_1 & k_3 & k_3
  \end{pmatrix}$
are non-zero only if:
\begin{itemize}
\item The absolute value of $k_i$ does not exceed $l_i$, i.e., $-l_i \leq k_i \leq l_i$ for $i=1,2,3$
\item The summation of all $k_i$ should be zero: $k_1 + k_2 +k_3 = 0$.
\item Triangle inequality holds for $l_i$'s: $\card{l_1 - l_2} \leq l_3 \leq l_1 + l_2$.
\item The sum of all $l_i$'s should be an integer.
% $l_1+l_2+l_3 \in \mathbb{N}$.
\item If $k_1 = k_2 = k_3 = 0$,  $l_1+l_2+l_3$ should be an even integer.
\end{itemize}
If one of the above conditions does not hold, the corresponding Wigner 3j symbol will be zero.

Beside deriving coherence bound for matrix from Wigner D-function and spherical harmonics by fixing parameter axes on the elevation $$\theta$$, sampling points that yield on the high coherence matrix is also discussed in our work

References

[1]//
[2]//
[3]//
[4]//
