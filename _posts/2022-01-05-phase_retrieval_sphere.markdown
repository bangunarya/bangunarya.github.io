---
layout: post
title:  "Phase Retrieval from the Intensity of Spherical Measurements"
date:   2019-09-22 08:42:13 +0100 (3)
categories: jekyll update
---

<div style="text-align: justify"> 
It has been discussed in the previous blog that electromagnetic fields acquired on the spherical coordinates can be expanded by using spherical harmonics or, if we also measure the polarization, Wigner D-functions.  Hence, sampling acquisitions can be represented by a linear system of equations as follows  

$$
\begin{equation}
\underbrace{\begin{pmatrix}
  f(\theta_1,\phi_1, \chi_1) \\
  f(\theta_2,\phi_2, \chi_2) \\
  \vdots\\
  f(\theta_m,\phi_m, \chi_m)
\end{pmatrix}}_{\mathbf{y} \in \mathbb{C}^m}=
\underbrace{\begin{pmatrix}
  \mathrm{D}_0^{0,0}(\theta_1,\phi_1,\chi_1) \quad  \dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_1,\phi_1,\chi_1)\\
  \mathrm{D}_0^{0,0}(\theta_2,\phi_2,\chi_2) \quad  \dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_2,\phi_2,\chi_2)\\
  \vdots\\
  \mathrm{D}_0^{0,0}(\theta_m,\phi_m,\chi_m) \quad  \dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_m,\phi_m,\chi_m)\\
\end{pmatrix}}_{\mathbf{A} \in \mathbb{C}^{m \times N}}  
\underbrace{\begin{pmatrix}
  f_0^{0,0} \\
  f_1^{-1,-1} \\
  \vdots\\
  f_{B-1}^{B-1,B-1}
\end{pmatrix}}_{\mathbf{x} \in \mathbb{C}^N},
\end{equation} 
$$ 

where \(f(\theta_i,\phi_i,\chi_i)\) for \( i \in \{1,2,3,\dots,m\}\) or simply denoted as \(i \in [m]\) represents \(m-\)sampling points of our signals measured with angle distributions on the elevation \(\theta \in [0, \pi] \) as well as azimuth and polarization \(\phi,\chi \in [0,2\pi)\), respectively. 
<br>
<br>
Suppose we acquire signals from non-ideal and non-linear measurements on the spherical coordinates. Such conditions appear, for instance, when only the intensity measurements are available during acquisition processes, i.e., in the phaseless spherical near-field antenna measurements [1]. In this case, the measurement model would become 

$$
\begin{equation}
b_i = |y_i|^2 = |\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 \in \mathbb{R},
\end{equation}
$$

where the vector \(\mathbf{a}_i = [\mathrm{D}_0^{0,0}(\theta_i,\phi_i,\chi_i) \quad \mathrm{D}_1^{-1,-1}(\theta_i,\phi_i,\chi_i) \dots  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_i,\phi_i,\chi_i)]^T \in \mathbb{C}^N \) consists of Wigner D-functions for arbitrary sampling points \(i \in [m]\ \). The goal in spherical near-field measurements is that, by acquiring electromagnetic fields on the near-field region so that acquisition can be done in small-range measurement systems, we want to estimate the spherical mode coefficients \(\mathbf{x} \in \mathbb{C}^N\) and construct the far-field radiation pattern by transforming the estimated spherical mode coefficients. While the standard estimation of spherical mode coefficients in spherical near-field antenna measurements is a linear inverse problem, the phaseless problem is a non-linear inverse problem since we only have intensity measurements to estimate the coefficients. Additionally, this problem is related to phase retrieval problems.
<br>
<br>
As a consequence of losing the phase information in phase retrieval problems, we always encounter ambiguities when reconstructing the coefficients \(\mathbf{x} \in \mathbb{C}^N\). For instance, when multiplied to another phase \(\mathbf{\hat{x}} = \mathbf{x} e^{i\alpha}\), identical intensity measurements are attained. This trivial ambiguity is called the global phase factor. Mathematically, we can express it as

$$
|\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 = |\langle\mathbf{a}_i,\mathbf{\hat x}\rangle|^2\quad \forall i \in [m]
$$

In contrast to the construction of matrix \(\mathbf{A} \in \mathbb{C}^{m \times N}\) from a random distribution, e.g., Gaussian, where we usually only have a global phase ambiguity, the structured measurement matrices from spherical harmonics and Wigner D-functions suffer from other ambiguities due to the conjugate-symmetries of those functions. When considering equiangular sampling points, apparently we also face other ambiguities which are summarized in the following:
<ol>
<li> Global phase ambiguity</li>
<li> Conjugate symmetries</li>
<li> Ambiguities related to specific sampling points</li>
</ol> 
A complete discussion of ambiguities that emerge during matrices construction from structured basis functions like spherical harmonics is discussed in our work [2].

<br>
<br>
Vibrant research activities to find out the condition for a recovery guarantee have been discussed. From the algebraic geometry point of view, it has been shown in the complex field that the number of measurements or total sampling points \( m \geq 4N - 2 \) suffice in guaranteeing a unique reconstruction up to some ambiguities [3]. However, uniqueness does not tell us anything about the existence of a feasible algorithm or stability in the presence of noise. In recent years, many algorithms have been developed to address phase retrieval problems. From the convex optimization point of view, the problem can be approached by relaxing the rank minimization to trace minimization [4], which is explained below

$$
b_i =|\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 = \text{trace}\left(\mathbf{a}_i\mathbf{a}_i^H \mathbf{x}\mathbf{x}^H \right) = \text{trace}\left(\mathbf{a}_i\mathbf{a}_i^H \mathbf{X} \right) \quad \text{for} \quad i \in [m],
$$
where  \(\mathbf{X} = \mathbf{x}\mathbf{x}^H  \in \mathbb{C}^{N \times N}\) is a rank-1 matrix  and \(\mathbf{x}^H\) denotes a conjugate transpose or a Hermitian transpose. We have an optimization problem as follows

$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{find}}
& &  \mathbf{X}
& \text{subject to}
& & {b_i} = \text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)
&&&\text{and} \quad \text{rank}\left(\mathbf{X}\right) = 1
\end{aligned}
\end{equation*}
$$

This problem is in general NP-hard. Nevertheless, we can approach this by using convex relaxation and thus trace minimization as follows
$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{minimize}}
& &  \text{trace}\left(\mathbf{X}\right)
& \text{subject to}
& & {b_i} = \text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)
&&& \text{and} \quad \mathbf{X} \succcurlyeq 0.
\end{aligned}
\end{equation*}
$$
The trace is a notation to sum all elements in the main diagonal of a square matrix. Imposing trace minimization as the objective function and adding positive semidefinite constraint \(\mathbf{X} \succcurlyeq 0\) relax the solution onto a convex set. Hence, we can guarantee that we will get a global optimum on the solution up to some ambiguities.  Since the original solution lies in the space of rank-1 matrices, the question is now: in which condition will the relaxation problem have a rank-1 solution? As discussed in [4], the condition holds when we can show the following
<ol>
  <li> The construction of a matrix or a collection of vector \(\mathbf{a}_i\) for \(i \in [m]\) satisfies a condition related to the restricted isometry property (RIP). </li>
  <li> A dual certificate exists for trace minimization. </li>
</ol>

For the first condition, we can adopt a proof technique from the compressed sensing literature. The difficulty lies in the second condition, where we want to construct a dual certificate for the trace minimization problems which depends highly on the structure of the measurement matrix or the collection of vector \(\mathbf{a}_i \) for \( i \in [m] \). In [4], the authors probabilistically show that it is possible to construct a dual certificate if we have \(\mathbf{a}_i\) for \( i \in [m] \) from the Gaussian distribution.  Another proof technique is also discussed in [5], where the author coined \(\textit{the golfing scheme} \).
<br>
<br>
Coming back from our original problem, when \(\mathbf{a}_i\) for \( i \in [m] \) is a collection of spherical harmonics or Wigner D-functions, the construction of a dual certificate is not easy. We will discuss why the proof strategy is not trivial in a future article.

Another approach to deal with the convex relaxation problem of phase retrieval is changing the objective function \( \text{trace}\left(\mathbf{X}\right)\) to nuclear norm minimization \(\left\lVert \mathbf{X} \right\rVert_1 \). Here, we use the notation of Schatten \(p-\)norm for \(p=1\). The idea stems from the fact that since the rank of a matrix can be measured by the number of non-zero singular values, i.e., if the rank matrix equals to one, then we only have one non-zero singular value and we can change the rank minimization on the objective function to minimizing the sum of the absolute value of those singular values, written as 
$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{minimize}}
& &  \left\lVert \mathbf{X} \right\rVert_1
& \text{subject to}
& &  {b_i} = \text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)\\
\end{aligned}
\end{equation*}
$$
This approach has been discussed, for instance, in [6]. Here, a different proof strategy has been discussed, where the authors call the approach as \(\textit{the bowling scheme}\). We will discuss the proof strategy as well as the challenge of adopting this approach to structured matrices from spherical harmonics and Wigner D-functions in a future article.

</div>

<br> 
<br> 

References: 

[1] [Phaseless spherical near-feld antenna measurements:Concept, algorithm and simulation](https://ieeexplore.ieee.org/abstract/document/5171897)\\
[2] [Signal recovery from phaseless measurements of spherical harmonics expansion](https://ieeexplore.ieee.org/abstract/document/8902696)\\
[3] [On signal reconstruction without phase](https://www.sciencedirect.com/science/article/pii/S1063520305000667) \\
[4] [PhaseLift: Exact and Stable Signal Recovery from Magnitude Measurements via Convex Programming](https://onlinelibrary.wiley.com/doi/abs/10.1002/cpa.21432)\\
[5] [Recovering Low-Rank Matrices From Few Coefficients in Any Basis](https://ieeexplore.ieee.org/abstract/document/5714248/)\\
[6] [Convex recovery of a structured signal from independent random linear measurements](https://arxiv.org/abs/1405.1102)\\