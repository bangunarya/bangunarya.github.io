---
layout: post
title:  "Ptychography Method"
date:   2020-05-10 08:42:13 +0100
categories: jekyll update
---
<div style="text-align: justify"> 
One of the most fundamental challenges in electron microscopy imaging is phase reconstruction given only the intensity data during measurement processes. This problem occurs because the current detector hardware used in the implementation is unable to record phase information of the exit wave that passes through the specimen under test. Since the phase information is necessary to improve image resolution, to understand the interaction of electrons and atoms within a material, and in particular to recover the electrostatic potential of the specimen, the phase retrieval algorithm is crucial for the application in electron imaging. 

Ptychography is a method to address the phase retrieval problem by processing multiple intensity diffraction patterns stemming from overlapping illuminations of the object. In the literature, the aberration-free illumination given by the electron wave incident is also called the probe, where the structure is modelled by a Bessel function of the first order \(J_1\).  The two-dimensional probe \(\mathbf{P} \in \mathbb{C}^{N \times N} \), which depends on the aperture sizes \(q_{\text{max}}\), is given by

$$
\begin{equation*}
\begin{aligned}
   \small
p_{y,x} &= \pi q_{\text{max}}^2 \left(\frac{2J_1\left(2 \pi q_{\text{max}} |\mathbf{r}| \right)}{2\pi q_{\text{max}}|\mathbf{r}|} \right),
\end{aligned}
\end{equation*}
$$
where  \(\quad y,x \in [N] \) represents discrete grid of the illumination} and \(|\mathbf{r}| = \sqrt{ x^2 + y^2}\). 
The intensity of this function, sometimes also called Airy disk, is shown in the following

<center><img src="/assets/img/probes.png"  aligned="center" width="450" height="350" ></center>

Suppose we have a specimen under test given by variable \(\mathbf{X} \in \mathbb{C}^{N \times N}\). This variable represents the object transfer function given an electron wave as the input wave. The intensity of diffraction patterns acquired by the detector in an electron microscope is given by 

$$
\begin{equation*}
\mathbf{I}_s = |\mathcal{F}(\mathbf{P}_s \circ \mathbf{X})|^2,
\end{equation*}
$$

where the index \(s \in [S] \) represents the total scanning points by shifting the main beam of Airy function according to the position defined by the microscopist, \(\circ\) is the element-wise or Hadamard product, and \( \mathcal{F}: \mathbb{C}^{N \times N} \rightarrow \mathbb{C}^{N \times N}\) is the two-dimensional Fourier transform. In general, during the measurement process, the adjacent beams usually overlap each other such as with the settings presented in the following figure 
  
<center><img src="/assets/img/ptycho_model.png"  aligned="center" width="390" height="350" ></center>

Since we can model the forward process by the acquisition of intensity diffraction pattern, the fundamental question in ptychography is to solve the non-linear inverse problem by reconstructing the specimen under test \(\mathbf{X} \in \mathbb{C}^{N \times N}\) given multiple intensity measurements. Several algorithms have been developed in recent years to address this problem, for instance, by adopting the alternating projection method as discussed in ePIE [1], reformulating the forward model as in the SSB method [2], as well as by expanding the squared function and regrouping probe and specimen transfer function in terms of Wigner function as in WDD method [3].

The problem with most algorithms above, i.e., ePIE and SSB, is that  they are derived with the condition of thin specimens, e.g., below \( 5 \) nm, and the strong dynamical scattering is neglected. Several attempts to employ different approaches such as incorporating the multislice model, i.e., modelling thick specimens using a collection of many thin specimens [4,6], as well as directly using the scattering matrix derived from Schrödinger equation, e.g., sometimes called the Blochwave model, has been discussed [5,6]. While the first approach can be seen as a heuristic approach, the latter has a computational problem due to calculation of the eigenvalue decomposition on a huge matrix. In the next article, we will specifically discuss the ptychography model for a thick specimen.
</div>

<br> 
<br> 

References: 

[1] [An improved ptychographical phase retrieval algorithm for diffractive imaging](https://www.sciencedirect.com/science/article/abs/pii/S0304399109001284)\\
[2] [Experimental tests on double-resolution coherent imaging via STEM](https://www.sciencedirect.com/science/article/abs/pii/0304399193901057)\\
[3] [The theory of super-resolution electron microscopy via Wigner-distribution deconvolution](https://royalsocietypublishing.org/doi/abs/10.1098/rsta.1992.0050)\\
[4] [Ptychographic transmission microscopy in three dimensions using a multi-slice approach](https://opg.optica.org/josaa/abstract.cfm?uri=josaa-29-8-1606)\\
[5] [Diffraction contrast of electron microscope images of crystal lattice defects - II. The development of a dynamical theory](https://royalsocietypublishing.org/doi/10.1098/rspa.1961.0157)\\
[6] [Advanced computing in electron microscopy](https://link.springer.com/book/10.1007/978-1-4757-4406-4)