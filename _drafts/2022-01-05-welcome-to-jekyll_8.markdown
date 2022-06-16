---
layout: post
title:  "Wigner Distribution"
date:   2018-01-01 08:42:13 +0100
categories: jekyll update
---

One of the most fundamental questions in ptychography is whether we can estimate both object transfer function and probe's illumination given only the intensity of diffraction patterns. In general this problem is difficult because we can have different phase function without altering the intensity of diffraction patterns. In contrast to SSB method that has been discussed earlier by assuming weak phase object, we can directly expand the formula that model the measurement process.

Suppose we have object transfer function in terms of the coordinate \( \mathbf{r} \in \mathbb{R}^2 \), where in this case the vector \( \mathbf{r} \) represents two-dimensional coordinate position of our object \( O\left(\mathbf{r}\right) \). In scanning transmission electron microscopy (STEM) setting, we raster the probe position according to its scanning coordinate, hence we can have the equation to model acquisition process as

$$
I\(\mathbf q, \mathbf R\) = |\mathcal{F} \left( p\left(\mathbf{r}- \mathbf{R}\right)) O\left(\mathbf{r}\right) \right) |^2,
$$

where in our notation \(\mathbf{q} \in \mathbb{C}^2\) and \(\mathbf{R} \in \mathbb{R}^2\) are the diffraction space or Fourier transform on the coordinate position of the object and the shift coordinate, respectively. By expanding the square function as the product with its complex conjugate we can write as follows

$$
\begin{equation}
\begin{aligned}
I\(\mathbf q, \mathbf R\) &= |\mathcal{F}_{\mathbf{r}} \left( p\left(\mathbf{r}- \mathbf{R}\right)  O\left(\mathbf{r}\right) \right)|^2 \\
&= |\left( p\left(\mathbf{q}\right) e^{-i2\pi \mathbf{q}\mathbf{R} } \right)  \circledast_{\mathbf{q}}  O\left(\mathbf{q}\right) \right)|^2 

\end{aligned}
\end{equation}
$$
