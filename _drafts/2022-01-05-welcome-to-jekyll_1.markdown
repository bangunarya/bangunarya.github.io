---
layout: post
title:  "Sparse Recovery on the Sphere and the Rotation Group"
date:   2017-01-01 08:42:13 +0100 (1)
categories: jekyll update
---
The spherical coordinate with radius $$r = 1$$, sometimes also called unit two-dimesional sphere $$\mathbb{S}^2$$, embedded in the three-dimensional Euclidean space $$\mathbb{R}^3$$ can be defined as follow

$$
\mathbb{S}^2 = \{\mathbf{u} \in \mathbb{R}^3 \quad | \quad \left\| \mathbf{u}  \right\|_2 = 1\}
$$

Here, $$\left\| \right\|_2$$ is $$\ell_2-norm$$ or Euclidean norm. Parameterization of three-dimensional Euclidean space to the unit two-dimensional sphere can also be defined in the  coordinate transformation, where we have

$$
u_x = \sin \theta \cos \phi\\
u_y = \sin \theta \sin \phi\\
u_z = \cos \theta
$$

In many practical measurement system, we acquired signals on the unit sphere, for instance spherical near-field measurements, spherical microphone arrays. Suppose we record signals on the spherical coordinate given as a function $$f(\theta,\phi) \in \mathbb{C}$$. Furthermore, assume that this function $$f: \mathbb{S}^2 \rightarrow \mathbb{C}$$ is a square-integrable function. Therefore, we can expand this signal by othonormal basis functions on the sphere so called spherical harmonics $$Y_l^k (\theta,\phi)$$, given as

$$
f(\theta,\phi) = \sum_{l = 0}^{\infty} \sum_{k = -l}^l f_l^k Y_l^k (\theta,\phi),
$$

where spherical harmonics of degree $$l$$ and order $$k$$ can be written in terms of associated Legendre polynomials $$P_l^k \left(\cos \theta \right)$$ and trigonometric function $$e^{ik\phi}$$ as 

$$
Y_l^k (\theta,\phi) = \sqrt{\frac{2l + 1}{4\pi}\frac{(l-k)!}{(l +k)!}} P_l^k \left(\cos \theta \right) e^{ik\phi}
$$

Most of the time we have a bandlimited signal, where instead of having infinite expansion of spherical harmonics, we only consider expansion up to $$B$$ degree spherical harmonics. This condition is not contrived which exist in the experimental system, i.e., spherical near-field antenna measurements. Additionally, we also acquired not only one sample but $$m$$ samples instead. Thereby, the construction of expansion can be rewritten as a linear system of equations

$$
\begin{equation}
\underbrace{\begin{pmatrix}
  f(\theta_1,\phi_1) \\
  f(\theta_2,\phi_2) \\
  \vdots\\
  f(\theta_m,\phi_m)
\end{pmatrix}}_{\mathbf{y} \in \mathbb{C}^m}=
\underbrace{\begin{pmatrix}
  Y_0^0(\theta_1,\phi_1) \quad Y_1^{-1}(\theta_1,\phi_1)&\dots& Y_{B-1}^{B-1}(\theta_1,\phi_1) \\
  Y_0^0(\theta_2,\phi_2) \quad Y_1^{-1}(\theta_2,\phi_2)&\dots& Y_{B-1}^{B-1}(\theta_2,\phi_2) \\
  \vdots\\
  Y_0^0(\theta_m,\phi_m) \quad Y_1^{-1}(\theta_m,\phi_m)&\dots& Y_{B-1}^{B-1}(\theta_m,\phi_m) \\
\end{pmatrix}}_{\mathbf{A} \in \mathbb{C}^{m \times N}}  
\underbrace{\begin{pmatrix}
  f_0^0 \\
  f_1^{-1} \\
  \vdots\\
  f_{B-1}^{B-1}
\end{pmatrix}}_{\mathbf{x} \in \mathbb{C}^N}
\end{equation} 
$$ 

In most cases, we are interested to estimate the $$s$$-sparse coefficient $${f_l^k}$$, i.e., $$s$$ non zero, with fewer measurements, i.e., $$m \leq N$$. Hence, this inverse problem is sparse recovery problem which is also related to compressed sensing. It turns out that depending on the sampling distribution to acquired signals $$\mathbf{y} \in \mathbb{R}^m$$ and to construct a spherical harmonic sensing matrix $$\mathbf A \in \mathbb{C}^{m \times N}$$ we have different conditions to guarantee reconstruction by using basis pursuit algorithm or $$\ell_1-$$ minimization [1,2]. The idea stems from the fact that the matrix $$\mathbf A$$ should fulfill so called restricted isometry property in compressed sensing.

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

In spherical near-field measurement, we are interested not only to acquired electromagnetic fields on the sphere but also polarization. Hence, the setting is quite different since we have rotation variables $$\chi \in [0,\2\pi)$$. Considering this setting, we have different basis functions on the rotation group, called Wigner D-functions, given as

$$
\begin{equation}
\mathrm{D}_l^{k,n}(\theta,\phi,\chi)= N_l e^{-i k\phi} \mathrm{d}_l^{k,n}(\cos \theta)  e^{-i n\chi}, 
 \label{def:WigD}
\end{equation}
$$

where $$N_l=\sqrt{\frac{2l+1}{8\pi^2}}$$ is the normalization factor to guarantee that Wigner D-functions are unit norm.
The function $$\mathrm{d}_l^{k,n}(\cos \theta) $$ is the Wigner d-function of degree $$l$$ and orders $$k,n$$. It should be noted that in this case we have another order $$n$$ to represent the rotation or polarization of angle $$\chi \in [0, 2\pi)$$. The relation between spherical harmonics and Wigner D-functions is given by

$$
\begin{equation}\label{gener_SH}
\mathrm{D}_l^{k,n}(\theta,\phi,0) = (-1)^k \sqrt{\frac{1}{2\pi}}Y_{l}^{k}(\theta,\phi).
\end{equation}
$$

Hence, our matrix $$\mathbf{A}$$ in this case becomes

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

The investigation related to this matrix and sparse recovery condition has been also discussed in our paper [3]





References:\\
[1][Sparse recovery for spherical harmonic expansions by Holger Rauhut and Ward](/https://arxiv.org/pdf/1102.4097/)\\
[2][Weighted Eigenfunction Estimates with Applications to Compressed Sensing by Nicolas Burq, Semyon Dyatlov, Rachel Ward, and Maciej Zworski](/https://arxiv.org/pdf/1111.2383.pdf/)\\
[3][Sparse recovery in Wigner-D basis expansion by Arya Bangun, Arash Behboodi, and Rudolf Mathar](/https://arxiv.org/pdf/1609.01104.pdf/)