---
layout: post
title:  "Ptychography Method"
date:   2018-01-01 08:42:13 +0100
categories: jekyll update
---

One of the most fundamental challenges in electron microscopy imaging is to reconstruct the phase given only intensity data during measurement processes. This problem appears due to the fact that the current detector hardware used in the implementation is unable to record phase information of the exit wave passes through the specimen under test. As the phase information is important to improve the image resolution, to understand the interaction of electrons and atoms within a material, and in particular to recover the electrostatic potential of the specimen, phase retrieval algorithm is crucial for the application in electron imaging. 

Ptychography is a method to address the issue in phase retrieval problem by processing multiple intensity of diffraction patterns stemming from the overlapping illuminations of the object. In the literature, this illlumination given by the electron wave incident is also called the probe, where the structure is modelled by a Bessel function of the first order, as follow

$$

$$

In literature, this function sometimes also called Airy function.

Suppose we have a specimen undertest given by variable \(\mathbf{X} \in \mathbb{C}^{N \times N}\). This variable represents the object transfer function given the electron wave as the input wave. Intensity of diffraction patterns acquired by the detector in electron microscope is given by 

$$
 ,
$$

where the index \(s \in [S] \) represents total of scanning points by shifting the main beam of Airy function according to the position defined by the microscopist, usually the adjacent beams overlap each other, during measurement processes..


Since we can model the forward process by the acquisition of intensity diffraction pattern, the fundamental question in ptychography is that we want to solve the non linear inverse problem by reconstructing the specimen under test \( ,\) given multiple intensity measurement. Several algorithms have been developed in recent years to address this problem, for instance by adopting alternating projection method as discussed in ePIE [], by reformulating the forward model by assuming weak phase model or thin specimen in SSB method, as well as by expanding the squared function and regrouping probe function and object transfer function in terms of Wigner function, the algorithm is coined as WDD [].

The problem using forward process to model the acquisition of intensity of diffraction pattern above is that this assumption is only valid for thin specimen, e.g., below \( 10 \) nm where strong dynamical scattering does not necessarily exist in the experimentla seting. Considering this problem, several attempts to use different model by incorporating multislice model, modeling thick specimens with collection of many thin specimen,  as well as directly using scattering matrix derived from Schrödinger  equation, e.g., sometimes is called Blochwave model, has been discussed []. While the first approach can be seen as the heuristic approach, the latter has computational problem due to calculating eigenvalue decomposition on huge matrix.
