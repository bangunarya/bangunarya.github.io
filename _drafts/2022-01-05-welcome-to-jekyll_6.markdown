---
layout: post
title:  "Ptychography Live Processing using SSB method"
date:   2018-01-01 08:42:13 +0100
categories: jekyll update
---

Single Side Band (SSB) method is a ptychography algorithm derived from the assumption that the electrostatic potential of the specimen or object under observation can be approximated by weak phase model, which means we have a very thin specimen, i.e., below \(5\) nm, and hence the phase object can be represented as a linear approximation. Suppose the electrostatic potential of the specimen under test given by \(V(\mathbf r)\) where the phase grating can be written as unit amplitude object \(X = e^{iV(\mathbf r)}\). By assuming we have a very thin specimen the phase grating can be approximated by first order Taylor approximation, where the Taylor series of exponential function is written as

$$
e^{x)} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!}  + \dots
$$

Taking first order Taylor approximation we can approximate phase grating or phase object as \( 1 + iV( \mathbf r)\). Hence, the intensity of diffraction patterns recorded in the detector in terms of scanning points can be reformulated as

$$
\begin{equation}
\begin{aligned}
I\left(\mathbf{q}, \mathbf{R}\right) &= |\mathcal{F}_{\mathbf{q}}\left( p\left( \mathbf{r} - \mathbf{R}\right) \left( 1 + iV(\mathbf r)\right) \right)|^2\\
&= \left( p\left( \mathbf{q}\right)e^{i2\pi \mathbf{q}\mathbf{R}} \circledast_{\mathbf{q}} \mathcal{F}_{\mathbf{q}}\left( 1 + iV(\mathbf r)\right) \right) \left(\overline{\left( p\left( \mathbf{q}\right)e^{i2\pi \mathbf{q}\mathbf{R}} \circledast_{\mathbf{q}} \mathcal{F}_{\mathbf{q}}\left( 1 + iV(\mathbf r)\right) \right)} \right)
\end{aligned}
\end{equation}
$$

It can be seen that we can factorize the intensity by center band as well as the side band..

The challenge when implementing this model is that due to the volume of data to be processed in the experimental STEM data, we are required to have large memory allocation and high performance computation when reconstructing the specimen or object transfer function. Additionally, it is difficult to apply real time reconstructing during acquisition process. Taking advantageous of the Fourier transformation and Hermite polynomials to compress the intensity of diffraction pattern as well as the sparse structure of the intersection of probe's illumination on the Fourier space, we can improve computation time as well as to achieve an efficient computation directly on the L1-L3 cache, in which the strategy to reach the goal in live processing. We discuss our approach and implementation of live processing with SSB method in [].


References:




