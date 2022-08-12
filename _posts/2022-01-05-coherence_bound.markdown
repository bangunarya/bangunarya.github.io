---
layout: post
title:  "Coherence Bound of Sensing Matrices"
date:   2018-03-13 08:42:13 +0100 (2)
categories: jekyll update
---

<div style="text-align: justify"> Basis pursuit or \(\ell_1\)-minimization is a convex optimization method to recover a sparse solution from an underdetermined linear system of equations
$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{x}}{\text{minimize}}
& &  \left\lVert \mathbf{x} \right\rVert_1 
& \text{subject to}
& & \mathbf{y} = \mathbf{A} \mathbf{x}.
\end{aligned}
\end{equation*}
$$

A common technique to develop mathematical proofs that can guarantee unique reconstruction depends highly on the structure of the short-fat sensing matrix \( \mathbf{A} \in \mathbb{C}^{m \times N} \), where  \( m < N\). The Restricted Isometry Property (RIP) is commonly used as a metric and fundamental building block to state the argument. Intuitively, if a certain matrix fulfills the RIP, then the matrix only slightly affects the Euclidean norm of the vector \( \mathbf{x} \in \mathbb{C}^N \). However, it has been shown that constructing such deterministic matrix is difficult [1]. Hence, the construction of the RIP matrix is usually followed by a probabilistic statement, e.g., the matrix constructed from Gaussian or sub-Gaussian distribution has been proven to satisfy RIP with high probability [2].
<br> 
<br> 
Deterministic RIP matrix is not only sought after by the mathematics community but also necessary from a practical point of view. In general, sensing matrices in practical applications cannot be directly constructed from purely random distributions or arbirary values. As an example, when considering spherical near-field antenna measurements, we have to construct a matrix from certain functions, such as the so-called spherical harmonics \( Y_l^k (\theta,\phi) \) or Wigner D-functions \( \mathrm{D}_l^{k,n}(\theta,\phi,\chi) \) for degree \(l\) and orders \(k,n\). Another metric that is easy to compute and useful in practical applications is coherence, by which we characterize the matrix by calculating the normalized inner product of adjacent columns. 
<br>
<br>  
Suppose we have a sensing matrix \( \mathbf A=[\mathbf{a}_1 \dots \mathbf{a}_N]\in\mathbb C^{m\times N}\), the coherence is given by

$$
\begin{equation}
\begin{aligned}
& \underset{1 \leq i < j \leq N}{\text{max}}
& &  \frac{|\langle\mathbf{a}_i,\mathbf{a}_j\rangle|}{\left\lVert \mathbf{a}_i \right\rVert_2  \left\lVert \mathbf{a}_j \right\rVert_2},
\end{aligned}
\end{equation}
$$

where the coherence is upper-bounded by \( 1 \) as a direct consequence of the Cauchy-Schwarz inequality and lower-bounded by the so-called Welch bound [3]. Deriving the coherence bound for a structured matrix constructed from Wigner D-functions and spherical harmonics is challenging, since those functions depend on the degree, the order of the function, as well as the angles. The matrix from Wigner D-functions can be constructed as follows

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

The construction from spherical harmonics can be directly presented by using the relation 

$$
\begin{equation}\label{gener_SH}
\mathrm{D}_l^{-k,0}(\theta,\phi,0) = (-1)^k \sqrt{\frac{1}{2\pi}}Y_{l}^{k}(\theta,\phi).
\end{equation}
$$

Since we are dealing with the inner product of adjacent columns, we have a product of two Wigner D-functions which is inherently given from the structure of the matrix. As it turns out, the problem of finding the coherence bound on those matrices is very similar to calculating angular momentum in quantum mechanics, where the product of Wigner D-functions can be represented by the angular momentum coefficients, also called the Wigner 3j symbols, as follows

$$
\begin{equation}
\small
\begin{aligned}
 \sum_{p=1}^m\overline{\mathrm{D}_{l_1}^{k_1,n_1}(\theta_p,\phi_p,\chi_p)}  \mathrm{D}_{l_2}^{k_2,n_2}(\theta_p,\phi_p,\chi_p)  
 &= C_{k_2,n_2}\sum_{\substack{\hat l=|l_2-l_1| }}^{l_1 + l_2} {\sqrt{\frac{(2l_1 + 1)(2l_2 +1)(2\hat{l} + 1)}{8 \pi^2}}}  \\&\times \begin{pmatrix}
   l_1 & l_2 & \hat{l} \\
   -n_1 & n_2 & -\hat{n} 
  \end{pmatrix} \begin{pmatrix}
   l_1 & l_2 & \hat{l} \\
   -k_1 & k_2 & -\hat{k}
  \end{pmatrix}  \sum_{p=1}^m\mathrm{D}_{\hat{l}}^{\hat{k},\hat{n}}(\theta_p,\phi_p,\chi_p).
\end{aligned}
\end{equation}
$$

Wigner 3j symbols are denoted by \( \begin{pmatrix}
   l_1 & l_2 & l_3 \\
   k_1 & k_2 & k_3
  \end{pmatrix} \in \mathbb R \), and their exact formula is given in [4]. Despite their complex expressions, Wigner 3j symbols have a few useful properties. The so-called \(\textit{selection rules} \) state that Wigner 3j symbols \(\begin{pmatrix}
   l_1 & l_2 & {l}_3 \\
   k_1 & k_3 & k_3
  \end{pmatrix} \)
are non-zero only if:

<ol>
  <li> The absolute value of \(k_i\) does not exceed \(l_i\) i.e., \(-l_i \leq k_i \leq l_i \) for \(i=1,2,3\). </li>
  <li> The summation of all \(k_i\) should be zero: \(k_1 + k_2 +k_3 = 0\). </li>
  <li> Triangle inequality holds for \(l_i's: \lvert l_1-l_2 \rvert \leq l_3 \leq l_1 + l_2\). </li>
  <li> The sum of all \(l_i\)'s should be an integer. </li>
  <li> If \(k_1 = k_2 = k_3 = 0\),  \(l_1+l_2+l_3\) should be an even integer. </li>
</ol> 
 
If one of the above conditions does not hold, the corresponding Wigner 3j symbol will be zero.

The coherence bound can be subsequently derived from the property of the Wigner 3j symbols. We show that, considering equispaced angles on the elevation \(\theta \in [0, \pi]\), we can find a lower-bound given by the condition of the same orders in the adjacent columns of matrices, i.e., \( k_1 = k_2\) and \(n_1 = n_2\) as discussed in our works [5,6,7].   
</div>

<br> 
<br> 

References: 

[1] [The computational complexity of the restricted isometry property, the nullspace property, and related concepts in compressed sensing](https://ieeexplore.ieee.org/document/6658871)\\
[2] [A mathematical introduction to compressive sensing](https://link.springer.com/book/10.1007/978-0-8176-4948-7)\\
[3] [Lower bounds on the maximum cross correlation of signals](https://ieeexplore.ieee.org/abstract/document/1055219/)\\
[4] [Hilbert space methods in signal processing](https://www.cambridge.org/core/books/hilbert-space-methods-in-signal-processing/BA54ECB490D53FF8CB176CFDCE34A962)\\
[5] [Coherence Bounds for Sensing Matrices in Spherical Harmonics Expansion](https://ieeexplore.ieee.org/abstract/document/8461805)\\
[6] [Sensing matrix design and sparse recovery on the sphere and the rotation group](https://ieeexplore.ieee.org/abstract/document/8995561)\\
[7] [Tight bounds on the mutual coherence of sensing matrices for Wigner D-functions on regular grids](https://link.springer.com/article/10.1007/s43670-021-00006-2) 