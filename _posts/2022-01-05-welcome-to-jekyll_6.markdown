---
layout: post
title:  "Ptychography Live Processing using SSB method"
date:   2021-07-19 08:42:13 +0100
categories: jekyll update
---
<div style="text-align: justify"> 
The Single Side Band (SSB) method [1] is a ptychography algorithm derived from the assumption that electrostatic potential of a specimen or object under observation can be approximated by the weak phase model, which means we have a very thin specimen, i.e., below \(5\) nm. Therefore, the phase object can be represented as a linear approximation. Suppose the electrostatic potential of the specimen under test given by \(V(\mathbf r)\), where the phase grating can be written as a unit amplitude object \(X = e^{iV(\mathbf r)}\). By assuming we have a very thin specimen, the phase grating can be approximated by first-order Taylor approximation, where Taylor series of the exponential function is expressed as

$$
e^{x} = 1 + x + \frac{x^2}{2!} + \frac{x^3}{3!}  + \dots
$$

Taking the first-order Taylor approximation, we can approximate the phase grating or phase object as \( 1 + iV( \mathbf r)\). Hence, the intensity of the diffraction patterns recorded in the detector in terms of scanning points can be reformulated as

$$
\begin{equation}
\begin{aligned}
I\left(\mathbf{q}, \mathbf{R}\right) &= |\mathcal{F}_{\mathbf{q}}\left( p\left( \mathbf{r} - \mathbf{R}\right) \left( 1 + iV(\mathbf r)\right) \right)|^2\\
&= |\left( p\left( \mathbf{q}\right)e^{-i2\pi \mathbf{q}\mathbf{R}} \circledast_{\mathbf{q}} \left( \delta(\mathbf q) + iV(\mathbf q)\right) \right)|^2.
\end{aligned}
\end{equation}
$$

Using the distributive property of convolution, expanding the square function, i.e., \(|a|^2 = a \overline{a}\), as well as applying Fourier transform on the scanning coordinate \( \mathbf{R} \) to get spatial frequency \( \mathbf{Q} \), we will have 

$$
I\left(\mathbf{q}, \mathbf{Q}\right) = |p\left(\mathbf{q} \right)|^2 \delta(\mathbf{Q}) - i p\left(\mathbf{q}\right) \overline{p\left(\mathbf{q} +  \mathbf{Q}\right)} V(-\mathbf{Q}) +  i \overline{p\left(\mathbf{q}\right)} {p\left(\mathbf{q} +  \mathbf{Q}\right)} V(\mathbf{Q})
$$

It can be seen that we can factorize the intensity by the centre band as well as the sideband with respect to the autocorrelation of the probe function.

The challenge when implementing this model is that, due to the volume of data to be processed in the experimental STEM data, we are required to have a large memory allocation and high-performance computation when reconstructing the specimen or object transfer function. Additionally, it is difficult to apply real-time reconstruction during the acquisition process. 


Taking advantage of the Hermite polynomials to compress the intensity of the diffraction pattern as well as the sparse structure of the autocorrelation of the probe's illumination on Fourier space, we can achieve an efficient computation directly on the L1-L3 cache, which is the strategy to reach the goal in live processing. We discuss our approach and implementation of live processing with the SSB method in [2,3].
</div>

<br> 
<br> 

References:

[1] [Experimental tests on double-resolution coherent imaging via STEM](https://www.sciencedirect.com/science/article/abs/pii/0304399193901057)\\
[2] [Live Processing of Momentum-Resolved STEM Data for First Moment Imaging and Ptychography](https://www.cambridge.org/core/journals/microscopy-and-microanalysis/article/live-processing-of-momentumresolved-stem-data-for-first-moment-imaging-and-ptychography/5FDD47E708AC82B22ADDB0A074108213)\\
[3] [Github and video reconstruction](https://github.com/LiberTEM/libertem.github.io)
 


