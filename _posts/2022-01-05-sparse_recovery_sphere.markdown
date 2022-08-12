---
layout: post
title:  "Sparse Recovery on the Sphere and the Rotation Group"
date:   2017-05-30 08:42:13 +0100 (1)
categories: jekyll update
---
<div style="text-align: justify">
The spherical coordinate with radius \(r = 1\), also called the unit two-dimensional sphere \(\mathbb{S}^2\) embedded in the three-dimensional Euclidean space \(\mathbb{R}^3\), can be defined as follows

$$
\mathbb{S}^2 = \{\mathbf{u} \in \mathbb{R}^3 \quad | \quad \left\| \mathbf{u}  \right\|_2 = 1\},
$$
where the vector \(\mathbf{u} = [u_x, u_y, u_z]^T\) is the three-dimensional Cartesian coordinate and  \(\left\|.\right\|_2\) is the \(\ell_2-\)norm or the Euclidean norm. Parameterization of three-dimensional Euclidean spaces to the unit sphere can also be presented in the coordinate transformation 

$$
u_x = \sin \theta \cos \phi\\
u_y = \sin \theta \sin \phi\\
u_z = \cos \theta.
$$

Signal acquisition on the unit sphere is necessary for many practical measurement systems, such as spherical near-field measurements, spherical microphone arrays, and so on.
<br> 
<br> 
 Suppose we record signals on the spherical coordinate system expressed as a function \(f(\theta,\phi) \in \mathbb{C}\), where we have \(\theta \in [0, \pi]\) as the elevation angle and \(\phi \in [0, 2\pi)\) as the azimuth angle. Furthermore, let us first assume that this function \(f: \mathbb{S}^2 \rightarrow \mathbb{C}\) is a square-integrable function (the beautiful mathematical property of this function is not discussed here, but this concept is intuitively important to define the finite energy density of signals). Therefore, we can expand this signal by using orthonormal basis functions on the sphere, namely spherical harmonics \(Y_l^k (\theta,\phi)\), given as

$$
f(\theta,\phi) = \sum_{l = 0}^{\infty} \sum_{k = -l}^l f_l^k Y_l^k (\theta,\phi),
$$

where spherical harmonics of degree \(l\) and order \(k\) can be written in terms of the associated Legendre polynomials \(P_l^k \left(\cos \theta \right)\) and trigonometric function \(e^{ik\phi}\) as 

$$
Y_l^k (\theta,\phi) = \sqrt{\frac{2l + 1}{4\pi}\frac{(l-k)!}{(l +k)!}} P_l^k \left(\cos \theta \right) e^{ik\phi}
$$

Most of the time, we have bandlimited signals, where instead of having the infinite expansion of spherical harmonics, we only consider an expansion up to the \(B\)th degree of spherical harmonics. This condition is not contrived because it exists in the experimental system, i.e., spherical near-field antenna measurements. Additionally, we also acquire not only one sample but also \(m\) samples. Thereby, the expansion can be rewritten as a linear system of equations.
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

In most cases, we are interested in estimating the \(s\)-sparse coefficient \({f_l^k}\), i.e., \(s\) non-zero, with fewer measurements \(\mathbf{y} \in \mathbb{C}^m\), i.e., \(m \leq N\). Hence, this inverse problem is a sparse recovery problem which is related to compressed sensing. As it turns out, depending on the sampling distribution to acquire signals \(\mathbf{y} \in \mathbb{C}^m\) and to construct the spherical harmonic sensing matrix \(\mathbf A \in \mathbb{C}^{m \times N}\), we have different conditions to guarantee unique reconstruction by using the basis pursuit algorithm or the \(\ell_1-\) minimization [1,2]. The idea stems from the fact that matrix \(\mathbf A\) should fulfill the so-called restricted isometry property, as discussed in the literature on compressed sensing [3].

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

In spherical near-field measurements, we are interested in acquiring not only the electromagnetic fields on the sphere but also their polarization. The setting becomes different while considering the polarization since we now have the rotation variables \(\chi \in [0,2\pi)\). Consequently, we have different basis functions on the spherical rotation, also called the rotation group, namely Wigner D-functions, given as

$$
\begin{equation}
\mathrm{D}_l^{k,0}(\theta,\phi,\chi)= N_l e^{-i k\phi} \mathrm{d}_l^{k,n}(\cos \theta)  e^{-i n\chi}, 
 \label{def:WigD}
\end{equation}
$$

where \(N_l=\sqrt{\frac{2l+1}{8\pi^2}}\) is the normalization factor such that the Wigner D-functions have a unit norm.
The function \(\mathrm{d}_l^{k,n}(\cos \theta) \) is the Wigner d-function of degree \(l\) and orders \(k,n\). It should be noted that, in this case, we have another order \(n\) to represent the rotation or the polarization of angle \(\chi \in [0, 2\pi)\). The relation between spherical harmonics and Wigner D-functions is expressed as follows

$$
\begin{equation}\label{gener_SH}
\mathrm{D}_l^{k,n}(\theta,\phi,0) = (-1)^k \sqrt{\frac{1}{2\pi}}Y_{l}^{k}(\theta,\phi).
\end{equation}
$$

Hence, in this case, our matrix \(\mathbf{A}\) becomes

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

Therefore, the recovery guarantee of the inverse problem on the sphere and the rotation group boils down to checking the RIP of structured random matrices constructed from the random sampled spherical harmonics or Wigner D-functions. The investigation related to this matrix and sparse recovery condition has also been discussed in our paper [4], where we follow the same philosophy and use the RIP for a bounded orthonormal system [1,2,3].
</div>

<br> 
<br> 

References:

[1] [Sparse recovery for spherical harmonic expansions](/https://arxiv.org/pdf/1102.4097/)\\
[2] [Weighted Eigenfunction Estimates with Applications to Compressed Sensing](/https://arxiv.org/pdf/1111.2383.pdf/)\\
[3] [A mathematical introduction to compressive sensing](https://link.springer.com/book/10.1007/978-0-8176-4948-7)\\
[4] [Sparse recovery in Wigner-D basis expansion](/https://arxiv.org/pdf/1609.01104.pdf/)