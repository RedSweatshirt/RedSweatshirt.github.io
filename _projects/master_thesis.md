---
layout: page
title: Recovery of Herschel-Bulkley Fluid Parameters from Video via Differentiable Simulations
description: MIT M.Eng Thesis
img: assets/img/meng_thesis/bunny_init.png
importance: 1
category: school
---

<center>
    <div class="row justify-content-sm-center">
        <div class="col-sm mt-3 mt-md-0">
            {% include figure.liquid path="assets/img/meng_thesis/bunny_simulation.png" title="Ketchup Stanford Bunny Simulation" class="img-fluid rounded z-depth-1" %}
        </div>
    </div>
</center>
<div class="caption">
    Stanford Bunny simulation using recovered ketchup parameters over time from beginning (left) to middle (center) and end (right).
</div>


#### Abstract
Recreating the physical behavior of fluids from real-world footage remains a significant challenge, particularly for non-Newtonian fluids. This work introduces a novel method that combines neural radiance fields (NeRF), which map 3D scene coordinates to color and density using deep neural networks, with the material point method (MPM), a simulation technique that represents materials as moving points capable of large deformation. Our approach aims to accurately recover physical parameters and achieve high-fidelity 3D reconstructions from single-view videos of fluids, even those with complex rheological behaviors like shear thinning and thickening.

In this study, we apply our method to a Herschel-Bulkley fluid, namely ketchup, under two different real-world conditions: a 50mm column collapse and being squeezed from a bottle. By leveraging the differentiable nature of NeRF and the fluid simulation capabilities of MPM, our approach extracts parameters from real-world footage after initially training on approximate geometry derived from virtual models. The actual video footage is then used to estimate initial velocities and retrieve constitutive parameters, including modulus, yield stress, and viscosity. The iterative optimization process, which integrates continuous feedback between the NeRF-MPM simulation and the video data, enables us to extract constitutive parameters from real footage and perform predictive simulations that closely reflect the behavior observed in the training videos.

Key results include the retrieval of constitutive parameters, such as modulus, yield stress, and viscosity, as well as reconstructed videos that reflect the fluid behavior observed in the training video. The results demonstrate that our method can reconstruct the fluid's flow behavior from limited perspectives, accurately enough to visually reproduce the flow, showcasing its flexibility and robustness. This work not only validates the approach through a series of experiments but also highlights the potential for differentiable rendering and simulation techniques to advance our understanding and simulation of complex material dynamics, particularly in cases where direct measurements are challenging or impossible.

#### [Read Full Thesis on MIT DSpace](https://dspace.mit.edu/handle/1721.1/157204)