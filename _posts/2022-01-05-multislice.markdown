---
layout: post
title:  "Multislice Method for Thick Specimens"
date:   2022-05-10 08:42:13 +0100
categories: jekyll update
---
<div style="text-align: justify">
The ptychography method in electron microscopy models interaction between the illuminated probe and the specimen under investigation mathematically as having a multiplicative property. In this case, for each overlapping scanning point during the acquisition processes, we can formulate the exit wave that passes through the specimen as the result of a multiplication between the entrance wave and the specimen transfer function. Suppose the specimen transfer function denoted as \(\mathbf{X} \in \mathbb{C}^{N \times N}\) and the illuminated probe as \(\mathbf{P}_s \in \mathbb{C}^{N \times N}\) with scanning point index \(s\) and total scanning points \(s \in [S]\). Hence, the intensity of diffraction patterns observed at scanning point \(s \) is given by

$$
\mathbf{I}_s = |\mathcal{F}(\mathbf{P}_s \circ \mathbf{X})|^2 \in \mathbb{R}^{N \times N},
$$

where the symbol \(\circ\) denotes the element-wise multiplication or Hadamard product. As discussed earlier in the previous article, this model is oversimplified and neglects scattering processes that occurred between the electron and the atom inside the specimen. Several approaches to address the limitation of this model exist in the literature, namely using the Blochwave and the multislice model [1,2,3]. In this article, we focus on the latter, where according to the definition, the multislice method models the thick specimen as a collection of several thin slices of the specimen under observation, as presented in the figure below.

<center><img src="/assets/img/forw_multislice.png"  aligned="center" width="250" height="350" ></center>

The only caveat is that a propagator is required to model the propagation wave between slices, which is usually called a Fresnel propagator. Let us focus on the interaction between the probe \(\mathbf{P}_s \in \mathbb{C}^{N \times N}\) at scanning point \(s \in [S]\) and the first slice \(\mathbf{X}^1 \in \mathbb{C}^{N \times N}\), which is given by the element-wise product and in turn produces an exit wave of slice \(1\)

$$
\begin{equation*}
\mathbf{E}_s^1 = \mathbf{P}_s \circ \mathbf{X}^1.
\end{equation*}
$$

The first exit wave at scanning point \(s\), e.g., \( \mathbf{E}_s^1\), can be used as the illumination for the second slice after applying Fresnel propagation

$$
\mathcal{V}_z\left(\mathbf{E}\right) := \mathcal{F}^{-1}\left(\mathcal{F} \left( \mathbf{E}\right) \circ \mathbf{H}_m \right),
$$
where \(\mathcal{F}\) is the Fourier operator and \(\mathbf{H}_m \in \mathbb{C}^{N \times N}\) is the Fresnel propagator matrix at \(m-\)th slice with entries

$$
\begin{equation}
h_{y,x} := e^{-\pi i\Delta_m \lambda \left( \left( q_y^2 + q_x^2 \right) + 2\left( q_x \frac{\sin \theta_x}{\lambda} + q_y \frac{\sin \theta_y}{\lambda} \right)\right)}, \quad y,x\in [N].
\label{eq:fresnel_element}
\end{equation}
$$

The parameters \(q_y,q_x\) denote the discrete grid in the reciprocal or diffraction space and hence represent spatial frequencies, \(\Delta_m\) is the distance of the wave propagation, and \(\theta_x, \theta_y\) are the two-dimensional tilt angles. Here, we assume that the illumination is set to be perpendicular to the object surface along a major crystallographic axis, i.e. tilt angles are zero.

As the beam reaches the second slice, it is described as \(\mathcal{V}_z\left(\mathbf E_s^1\right)\) and the next exit wave is given by

$$
\begin{equation*}
\mathbf E_s^2 = \mathcal{V}_z\left(\mathbf{E}_s^1\right) \circ \mathbf{X}^2.
\end{equation*}
$$

Suppose we have \(m\) slices in total, the general representation of the \(m-\)th observed exit wave is written as
$$
\mathbf{E}_s^m = \mathcal{V}_z\left( \mathbf{E}_s^{m-1}\right) \circ \mathbf{X}^m \quad \text{for} \quad  m \in [M], m \neq 1,
$$

Finally, the intensity of the Fraunhofer diffraction pattern that is recorded by a detector in the far-field is given by
$$
\begin{equation}\label{eq: intensity measurements}
\mathbf{I}_s = \left|{\mathcal{F}\left(\mathbf{E}_s^M \right)}\right|^2 \, \forall \, s \in [S].
\end{equation}
$$

The previous approach is called the forward model, which models the propagation of the probe's illumination through a thick specimen. The goal of this approach is that, by using the ptychography model, one should address the non-linear inverse problem to estimate each slice and construct a three-dimensional specimen transfer function. The method has been proposed by incorporating the ptychography approach, i.e., alternating projection method in terms of ePIE, to address the inverse processes [4].  
<br> 
<br> 
One of the disadvantages of the current forward model is that it is difficult to separate the illuminated probe and the specimen transfer function as a single entity, since the Fresnel propagation entangles the process between probe and object. In our recent preprint [5], we propose a reformulation of the classical multislice method. Therefore, we can model the specimen under test as a single matrix and disentangle the probe's illumination. Furthermore, we also proposed two optimization-based algorithms to estimate the specimen under test.
 
</div>

<br> 
<br> 

References:

[1] [The scattering of electrons by atoms and crystals. I. A new theoretical approach](https://scripts.iucr.org/cgi-bin/paper?a02113)\\
[2] [Diffraction contrast of electron microscope images of crystal lattice defects - II. The development of a dynamical theory](https://royalsocietypublishing.org/doi/10.1098/rspa.1961.0157)\\
[3] [Advanced computing in electron microscopy](https://link.springer.com/book/10.1007/978-1-4757-4406-4)\\
[4] [Ptychographic transmission microscopy in three dimensions using a multi-slice approach](https://opg.optica.org/josaa/abstract.cfm?uri=josaa-29-8-1606)\\
[5] [Inverse Multislice Ptychography by Layer-wise Optimisation and Sparse Matrix Decomposition](https://arxiv.org/pdf/2205.03902.pdf)
 