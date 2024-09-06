---
layout: post
title:  "Diffusion Processes"
date:   2023-11-10 23:08:13 +0100 (1)
categories: jekyll update
---
<div style="text-align: justify">
Diffusion models have gained momentum recently due to their remarkable performance in generating images, with similar advancements seen in video generation, as popularized by OpenAI. The core idea behind these models is that data distribution can be estimated using neural networks, enabling the generation of new images.
The training process involves learning the data distribution by injecting a well-known distribution, such as a Gaussian. As a result, inference can be performed by implementing a sampling process from the estimated distribution. This allows for the generation of new images starting from a completely random distribution.
The foundation of diffusion models can be traced back to the theory of stochastic differential equations (SDEs), where the transformation from one distribution, such as image data, to a Gaussian random distribution can be described using Brownian motion [1-2].
</div>
 The simple and well-explained blog can be read [here](https://lilianweng.github.io/posts/2021-07-11-diffusion-models/) and [here](https://iclr-blogposts.github.io/2024/blog/diffusion-theory-from-scratch/)
<center><img src="/assets/img/sde.png"  aligned="center" width="450" height="250" ></center>
The figure is taken from [1]. The extension for diffusion model is also in [3-4]. The following video is a 3D knee image from MRI, could you guess which one is the original knee image and which one is the generated one?
<center><img src="/assets/img/generative.gif"  aligned="center" width="350" height="350" ></center>


References:

[1] [Score-Based Generative Modeling Through Stochastic Differential Equations](https://arxiv.org/pdf/2011.13456)\\
[2] [Denoising Diffusion Probabilistic Models
](https://proceedings.neurips.cc/paper/2020/hash/4c5bcfec8584af0d967f1ab10179ca4b-Abstract.html)\\
[3] [Video Diffusion Model](https://proceedings.neurips.cc/paper_files/paper/2022/hash/39235c56aef13fb05a6adc95eb9d8d66-Abstract-Conference.html)\\
[4] [Align Your Latents High-Resolution Video Synthesis With Latent Diffusion Models](https://openaccess.thecvf.com/content/CVPR2023/papers/Blattmann_Align_Your_Latents_High-Resolution_Video_Synthesis_With_Latent_Diffusion_Models_CVPR_2023_paper.pdf)
 
