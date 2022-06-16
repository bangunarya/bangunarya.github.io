---
layout: post
title:  "Phase Retrieval on the Sphere"
date:   2019-01-01 08:42:13 +0100 (3)
categories: jekyll update
---

<div style="text-align: justify"> Suppose we acquired signals on non-ideal and non-linear measurements on the spherical coordinate, such condition appear when only intensity measurements are able to be recorded. This setting exists in the phaseless spherical near-field antenna measurement, where due to imperfect condition of measurement setting we are only able to have intensity measurement [1]. It has been discussed in the previous blog that electromagnetic fields acquired on the spherical coordinate can be expanded by spherical harmonics. Additionally, by incorporating polarization acquisition the slightly modification but generalization on basis functions are possible by using Wigner D-functions. Hence, sampling acquisition can be represented by a linear system of equations as follows  

$$
\begin{equation}
\underbrace{\begin{pmatrix}
  f(\theta_1,\phi_1, \chi_1) \\
  f(\theta_2,\phi_2, \chi_2) \\
  \vdots\\
  f(\theta_m,\phi_m, \chi_m)
\end{pmatrix}}_{\mathbf{y} \in \mathbb{C}^m}=
\underbrace{ \begin{pmatrix}
  \mathrm{D}_0^{0,0}(\theta_1,\phi_1,\chi_1) \quad \mathrm{D}_1^{-1,-1}(\theta_1,\phi_1,\chi_1) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_1,\phi_1,\chi_1)\\
  \mathrm{D}_0^{0,0}(\theta_2,\phi_2,\chi_2) \quad \mathrm{D}_1^{-1,-1}(\theta_2,\phi_2,\chi_2) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_2,\phi_2,\chi_2)\\
  \vdots\\
  \mathrm{D}_0^{0,0}(\theta_m,\phi_m,\chi_m) \quad \mathrm{D}_1^{-1,-1}(\theta_m,\phi_m,\chi_m) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_m,\phi_m,\chi_m)\\
\end{pmatrix}}_{\mathbf{A} \in \mathbb{C}^{m \times N}}  
\underbrace{\begin{pmatrix}
  f_0^{0,0] \\
  f_1^{-1,-1} \\
  \vdots\\
  f_{B-1}^{B-1,B-1}
\end{pmatrix}}_{\mathbf{x} \in \mathbb{C}^N}
\end{equation} 
$$ 

It should be noted that \(f(\theta_i,\phi_i,\chi_i)\) for \( i \in \{1,2,3,\hdots,\}\) or simply denoted as \( \i \in [m]\)represent our signal acquired on the \(m \) sampling points \(\theta \in \[0, \pi\] \) and \(\phi,\chi \in \[0,2\)\). Due to non-ideal measurement settings we only have intensity measurements and do not have linear measurement, the model, therefore, is slightly changed as follow

$$
\begin{equation}
b_i = |y_i|^2 = |\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 \in \mathbff{R},
\end{equation}
$$

where the vector \( \mathbf{a}_i = \left[ \mathrm{D}_0^{0,0}(\theta_i,\phi_i,\chi_i) \quad \mathrm{D}_1^{-1,-1}(\theta_i,\phi_i,\chi_i) &\dots&  \mathrm{D}_{B-1}^{B-1,B-1}(\theta_i,\phi_i,\chi_i)\right]^T \in \mathbb{C}^N \) is nothing but Wigner D-functions for arbitrary sampling points $i$. The goal in spherical near-field measurements is that by acquiring electromagnetic fields on the near-field we want to estimate the spherical mode coefficients \(\mathbf{x} \in \mathbb{C}^N\), where later to transform this coefficient to estimate far-field radiation pattern. In general, this problem is non-linear inverse problem since we only have intensity measurement that represents the measurement setting to estimate the coefficients. Additionally, this problem has relation with phase retrieval problem. 

As the consequence of losing phase information, in phase retrieval problem we always have ambiguities when reconstructing the coefficients \(\mathbf{x} \in \mathbb{R}^N\). One condition of trivial ambiguity is the global phase factor, where by considering a multiplication to another phase \(\mathbf{ḩat x} = \mathbf{x} e^{i\alpha}\) we will have the same intensity measurements. Mathematically, we can write it as

$$
|\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 = |\langle\mathbf{a}_i,\mathbf{\hat x}\rangle|^2
$$

In contrast to the construction of matrix \(\mathbf{A} \in \mathbb{C}^{m \times N}\) from random distribution, e.g., Gaussian, where usually we only have global phase ambiguity, the structured measurement matrices from spherical harmonics and Wigner D-functions suffer from other ambiguities due to conjugate symmetry properties of those functions. It turns out that when considering equiangular sampling points, we also face another ambiguity. Summary of those ambiguities is given as follows
<ol>
  <li> Global phase ambiguity </li>
  <li> Conjugate symmetry properties </li>
  <li> Ambiguities related certain sampling points </li>
</ol> 
The complete discussion on those ambiguties from constructing matrices from structured basis function like spherical harmonics is discussed in our work [].

A vibrant research activities to find out a condition on the recovery guarantee has been discussed. From algebraic geometry point of view, it has been discussed that in complex field when we have the number of measurement or total sampling points  \( m \geq 4N - 2 \) suffice to guarantee for unique reconstruction. However, the uniqueness does not tell us anything about existence of feasible
algorithm or stability in presence of noise.  In recent years many algorithms have been developed to address phase retrieval problem. From convex optimization point of view this problem can be approached by using relaxation to trace minimization from rank minimization [], which is explained below

$$
b_i =|\langle\mathbf{a}_i,\mathbf{x}\rangle|^2 = \text{trace}\left(\mathbf{a}_i\mathbf{a}_i^T \mathbf{x}\mathbf{x}^T \right) = \text{trace}\left(\mathbf{a}_i\mathbf{a}_i^T \mathbf{X} \right) \quad \text{for} \quad i \in [m],
$$
where \(\mathbf{X} \in \mathbb{C}^{N \times N}\). Addressing the problem by using trace notation, here trace is notation to sum main diagonal of the matrix, we lift the solution onto rank-1 problem. Therefore, we have optimization problem as follow

$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{find}}
& &  \mathbf{X}
& \text{subject to}
& & \mathbf{b_i} = \\text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)\\
&&& \text{rank}\left(\mathbf{X}\right) = 1
\end{aligned}
\end{equation*}
$$

This problem is in general NP-hard. Nevertheless, we can approach this by using convex relaxation to trace minimization as follow
$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{minimize}}
& &  \text{trace}\left(\mathbf{X}\right)
& \text{subject to}
& & \mathbf{b_i} = \\text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)\\
&&& \mathbf{X} \succcurlyeq 0.
\end{aligned}
\end{equation*}
$$

Imposing trace minimization as objective function and positive semidefinite constraint \(\mathbf{X} \succcurlyeq 0\) relax the condition on the problem onto convex set. Hence we can guarantee that we will get global optimum on the solution. Of course the question is now in which condition the relaxation problem will have rank-1 solution since the original solution lies on the space of rank-1 matrices. As discussed in [], the condition holds when we can show  two conditons in the following
<ol>
  <li> The construction of matrix or collection of vector \(\mathbf{a}_i\) for \(i \in [m]\) satisfy a condition related to restricted isometry property (RIP) </li>
  <li> Dual certificate exist for the trace minimization </li>
</ol>

For the first condition usually we can address with the proof technique adopted from compressed sensing literature. The difficulty appears when we want to construct a dual certificate for trace minimization problem because usually the construction of dual certificate depend highly on the structure of measurement matrix or collection of vector \(\mathbf{a}_i\) for \( i \in [m] \). In [] the authors show  probabilistically it is possible to construct a dual certificate when constructing \(\mathbf{a}_i\) for \( i \in [m] \) from Gaussian distribution or in general the constrution of dual certificate for low rank matrix is also discussed in [], where the author coined the proof technique as \textit{golfing scheme}.

However, coming back from our original problem when \(\mathbf{a}_i\) for \( i \in [m] \) is nothing but the collection of spherical harmonics or wigner D-functions, the construction of dual certificate is not easy. We will discuss the proof strategy in the future article.

Another approach to deal with convex relaxation problem of phase retrieval is also possible when changing the objective function from \( \text{trace}\left(\mathbf{X}\right)\) to nuclear norm minimzation \(\left\lVert \mathbf{X} \right\rVert_1 \), here we use the notation of Schatten p-norm. The idea stems from the fact that since the rank of a matrix can be measured by the number of non-zero singular value, i.e., if rank matrix is equal to one then we have only one non-zero singular value,  we can change rank minimization on the objective function to the  minimizing the sum of absolute of singular value, written as 
$$
\begin{equation*}
\begin{aligned}
& \underset{\mathbf{X}}{\text{minimize}}
& &  \left\lVert \mathbf{X} \right\rVert_1
& \text{subject to}
& & \mathbf{b_i} = \\text{trace}\left( \mathbf{a}_i \mathbf{a}_i^T \mathbf{X} \right)\\
\end{aligned}
\end{equation*}
$$
This approach has been discussed, for instance in []. Here different proof strategy has been discussed, where the authors call the approach as \textit{the bowling scheme}. We will discuss the proof strategy as well as the challenge of adopting this pproach to stuctured matrices from spherical harmonics and Wigner D-function  in the future article.
</div>

References:

[1]
[2]
[3]
[4]