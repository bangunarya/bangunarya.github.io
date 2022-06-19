---
layout: post
title:  "Optimizing Sensing Matrices for SNF"
date:   2022-06-10 08:42:13 +0100
categories: jekyll update
---

<div style="text-align: justify">
Coherence-based minimization is an optimization problem that aims to minimize the coherence of a sensing matrix. In compressed sensing, coherence is a metric to measure the structure of sensing matrices that can also guarantee sparse recovery algorithms to uniquely reconstruct sparse signals [1,2,3]. Despite providing a weaker reconstruction guarantee compared to restricted isometry property (RIP), the coherence metric is easier to compute [4]. Suppose we have a sensing matrix  \( \mathbf A=[\mathbf{a}_1 \dots \mathbf{a}_N]\in\mathbb C^{m\times N}\), the coherence is given by

$$
\begin{equation}
\begin{aligned}
& \underset{1 \leq i < j \leq N}{\text{max}}
& &  \frac{|\langle\mathbf{a}_i,\mathbf{a}_j\rangle|}{\left\lVert \mathbf{a}_i \right\rVert_2  \left\lVert \mathbf{a}_j \right\rVert_2}.
\end{aligned}
\end{equation}
$$

Thus, the coherence-based minimization can be written as finding sequence vectors of column matrices \([\mathbf{a}_1 \dots \mathbf{a}_N] \in\mathbb C^{m\times N} \) that minimize the maximum absolute value of inner products between adjacent columns as follows

$$
\begin{equation}
\begin{aligned}
& \underset{\mathbf{a}_1,\mathbf{a}_2 \dots, \mathbf{a}_N}{\text{min }}\,\,\underset{1 \leq i < j \leq N}{\text{max}}
& &  \frac{|\langle\mathbf{a}_i,\mathbf{a}_j\rangle|}{\left\lVert \mathbf{a}_i \right\rVert_2  \left\lVert \mathbf{a}_j \right\rVert_2}.
\end{aligned}
\end{equation}
$$
This optimization is, in general, non-convex and there is no guarantee that we can reach the global optimum. However, several heuristic approaches, have been discussed for instance in [5,6].  
<br> 
Considering a structured sensing matrix, we cannot arbitrarily assign random vectors as presented in the original coherence-based minimization problem. In this case, we have a sampling of functions to construct the sensing matrix. For instance, in spherical near-field measurement, we construct a sensing matrix which depends on certain functions, namely Wigner D-functions or spherical harmonics. In the following, we present the construction of a sensing matrix from sampled Wigner D-functions
$$
\begin{equation}
 \mathbf{A} =
 \begin{pmatrix}
  \mathrm{D}_0^{0,0}(\theta_1,\phi_1,\chi_1) \quad \mathrm{D}_1^{-1,-1}(\theta_1,\phi_1,\chi_1) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_1,\phi_1,\chi_1)\\
  \mathrm{D}_0^{0,0}(\theta_2,\phi_2,\chi_2) \quad \mathrm{D}_1^{-1,-1}(\theta_2,\phi_2,\chi_2) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_2,\phi_2,\chi_2)\\
  \vdots\qquad \qquad \dots \qquad \qquad \vdots\\
  \mathrm{D}_0^{0,0}(\theta_m,\phi_m,\chi_m) \quad \mathrm{D}_1^{-1,-1}(\theta_m,\phi_m,\chi_m) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_m,\phi_m,\chi_m)\\
\end{pmatrix}
\end{equation}
$$

The construction from spherical harmonics can be directly followed by using the relation between Wigner D-functions and spherical harmonics as follows

$$
\begin{equation}\label{gener_SH}
\mathrm{D}_l^{-k,0}(\theta,\phi,0) = (-1)^k \sqrt{\frac{1}{2\pi}}Y_{l}^{k}(\theta,\phi).
\end{equation}
$$

The coherence, hence, can be expressed as the inner product between sampled Wigner D-functions or spherical harmonics as presented below
$$
\begin{equation} \label{coherence_Wigner}
\begin{aligned}
\mu  &= \underset{ 1 \leq r < q \leq L}{\text{max}} |g_{q,r} \left(\boldsymbol \theta,\boldsymbol \phi,\boldsymbol \chi \right)|\\   
\end{aligned},
\end{equation}
$$

where \(g_{q,r} \left(\boldsymbol \theta,\boldsymbol \phi,\boldsymbol \chi \right)\) is expressed as

$$
\begin{equation}
\small
 \sum_{i = 1}^{m} \frac{\mathrm{D}_{l{(q)}}^{k{(q)},n{(q)}}(\theta_i,\phi_i,\chi_i)  \overline{\mathrm{D}_{l{(r)}}^{k{(r)},n{(r)}}(\theta_i,\phi_i,\chi_i)}}{\left\lVert \mathrm{D}_{l{(q)}}^{k{(q)},n{(q)}}(\boldsymbol\theta,\boldsymbol\phi,\boldsymbol\chi)\right\rVert_2 \left\lVert \mathrm{D}_{l{(r)}}^{k{(r)},n{(r)}}(\boldsymbol\theta,\boldsymbol\phi,\boldsymbol\chi) \right\rVert_2}
 \label{eq:product}
\end{equation}
$$

and the vector \(\mathrm{D}_{l}^{k,n}(\boldsymbol\theta,\boldsymbol\phi,\boldsymbol\chi)\) is, in turn, 
$$
\mathrm{D}_{l}^{k,n}(\boldsymbol\theta,\boldsymbol\phi,\boldsymbol\chi):=
\begin{pmatrix}
 \mathrm{D}_{l}^{k,n}(\theta_1,\phi_1,\chi_1),
 \dots,
  \mathrm{D}_{l}^{k,n}(\theta_m,\phi_m,\chi_m)
\end{pmatrix}^T.
$$
The problem of optimizing the coherence of a sensing matrix from Wigner D-functions can be seen as finding the distribution of sampling points on \(\theta \in [0, \pi] \) and \(\phi, \chi \in [0, 2\pi)\) that minimizes the coherence as follows:

$$
\begin{equation}
\begin{aligned}
& \underset{\boldsymbol \theta, \boldsymbol \phi, \boldsymbol \chi \in \mathbb{R}^m}{\text{min}}
& & \underset{ 1 \leq r < q \leq N}{\text{max}} \quad |{g_{q,r}(\boldsymbol \theta,\boldsymbol \phi,\boldsymbol \chi)}|\\
%& \text{subject to}
%& & \theta_i \in [0,\pi]\quad \text{and} \quad \phi_i,\chi_i \in [0,2\pi) \quad  \\ &&&\text{for} \quad i \in [K]
\end{aligned}\quad.
\label{eq:Opt_General}
\end{equation}
$$
This problem equals to solving the min-max optimization of a non-convex objective function. The non-convexity appears from the absolute value constraint as well as the structure of the Jacobi and the trigonometric polynomials. 
<br> 
<br> 
In our work, we proposed two approaches to address this optimization problem [7].  The first strategy involves changing the maximum constraint, which can be written as the maximum norm of a vector
$$
\left\lVert \mathbf{x}\right\rVert_{\infty} =  \underset{ 1 \leq i \leq N}{\text{max}} \quad |x_i|.
$$
Since this constraint is non-smooth and non-differentiable at specific points, we can approximate and smoothen the constraint by using the \(\ell_p-\)norm for a large enough \(p\). This approach stems from the fact that 
$$
\left\lVert \mathbf{x}\right\rVert_{\infty} =  \underset{ p \rightarrow \infty}{\text{lim}} \quad \left\lVert \mathbf{x}\right\rVert_{p}.
$$
Therefore, the coherence-based minimization can be rewritten as
$$
\begin{equation}
\begin{aligned}
&\underset{\boldsymbol \theta, \boldsymbol \phi, \boldsymbol \chi \in \mathbb{R}^m}{\text{min}}
& &\underset{p \rightarrow \infty}{\lim} \left(\underset{1 \leq r < q \leq N}{\sum} |g_{q,r}(\boldsymbol \theta,\boldsymbol \phi,\boldsymbol \chi)|^{p}\right)^{1/p},
\end{aligned} 
\end{equation}
$$
where, by applying the derivative of \(\ell_p-\)norm, we can implement gradient-based method to perform the coherence-based minimization. 

<br> 
<br> 
The second strategy employs the proximal method of \(\ell_\infty-\)norm. In this case, instead of approximating the infinity norm by using the \(\ell_p-\)norm for a large enough \(p\), we adopt the definition of proximal of \(\ell_\infty-\)norm. For \(\ell_{\infty}-\)norm, its proximal operator can be written as the projection onto its dual norm, which is the \(\ell_1-\)norm [7]. Suppose we have a vector \(\mathbf x \in \mathbb{R}^N \), then the proximal operator of \(\left\lVert \mathbf x\right\rVert _{\infty}\) is given by
$$
\text{prox}_{\left\lVert . \right\rVert_\infty}\left(\mathbf x\right) = \mathbf x - \text{Proj}_{\left\lVert . \right\rVert_1}\left( \mathbf x \right).
$$
The projection onto the \(\ell_1-\)norm is well-studied, for instance, in [9] and can be directly implemented. In our approach, we adopt the augmented Lagrangian method to perform the coherence-based minimization by using a proximal operator of \(\ell_\infty-\)norm.

</div>

<br> 
<br> 

References:
 
[1] [Sparse representations in unions of bases](https://ieeexplore.ieee.org/abstract/document/1255564)\\
[2] [Signal recovery from random measurements via orthogonal matching pursuit](https://ieeexplore.ieee.org/abstract/document/4385788/)\\
[3] [A mathematical introduction to compressive sensing](https://link.springer.com/book/10.1007/978-0-8176-4948-7)\\
[4] [The computational complexity of the restricted isometry property, the nullspace property, and related concepts in compressed sensing](https://ieeexplore.ieee.org/document/6658871)\\
[5] [Coherence Optimization and Best Complex Antipodal Spherical Codes](https://ieeexplore.ieee.org/document/7244248)\\
[6] [Optimized projections for compressed sensing](https://ieeexplore.ieee.org/abstract/document/4359525)\\
[7] [Optimizing Sensing Matrices for Spherical Near-Field Antenna Measurements](https://arxiv.org/abs/2206.02181)\\
[8] [Proximal Algorithms](https://dl.acm.org/doi/abs/10.1561/2400000003)\\
[9] [Efficient projections onto the l1-ball for learning in high dimensions](https://dl.acm.org/doi/abs/10.1145/1390156.1390191)
-