---
title: Learning Surrogate Models for Fluid Dynamics
subtitle: "Seminar paper at KIT"
summary: "Can the physical principles underlying expensive fluid dynamics simulations be approximated by neural networks? To answer this question, a literature review is conducted and various current research approaches are compared. Fundamental architectures such as CNNs, GNNs, and LSTMs are introduced, and their advantages and disadvantages are discussed based on the literature. The results show that neural networks are capable of approximating fluid simulations, often faster than traditional numerical methods."
date: 2021-03-15
cardimage: learning_cfd_card.png
featureimage: learning_cfd.png
caption: "3D fluid simulation using a CNN ([Link to image source](https://github.com/google/FluidNet))"
authors:
  - Dominik: author.png
links:
  - pdf: 
      href: /files/Proseminar_Learning_Surrogate_Models_For_Fluid_Simulation.pdf
      label: Seminar paper (de)
---

## Literature Review
In this seminar paper, I conducted a literature review on publications about surrogate models for fluid dynamics. First, I filtered by keywords such as "fluid dynamics", "surrogate model", and "neural network".
Then, I read the abstracts of the papers and selected those that were relevant to my topic. The selected papers were then analyzed in detail, focusing on the methods used, the results achieved, and the limitations of the approaches. It is important to keep the initial keywords as broad as possible to ensure that all relevant papers are included in the review. Therefore, I also included keywords like "finite element method" (FEM), "large eddy simulation" (LES), and "particle simulation", "convolutional neural networks" (CNNs) to cover a wide range of approaches. As shown below, the number of publications on this topic has increased significantly in recent years.

{{< figSVG src="images/chart_n_publications.svg" caption="Publications per year about FEM that include neural networks." >}}

## Overview and Comparison of Approaches
The literature review revealed that there are many different approaches to using neural networks for fluid dynamics. Some approaches use CNNs to approximate the Navier-Stokes equations, while others use Graph Neural Networks to model the interactions between particles in a fluid. Some approaches also use LSTMs to model the temporal evolution of fluid dynamics. Each approach has its own advantages and disadvantages, which I have summarized in the paper. 

{{< figGIF src="images/canyon.gif" caption="A CNN is used to approximate a particle-based fluid simulation. ([Link to image source](https://github.com/isl-org/DeepLagrangianFluids))" >}}

## Research Process
As this was my first scientific research project, I had to familiarize myself with the research process. I learned how to conduct a literature review, research and analyze existing work, how to write a paper and present my findings. As part of the seminar, we conducted peer review sessions where we reviewed each other's papers and provided feedback. This helped me to improve my writing skills and to learn how to give constructive feedback. I also learned how to present my findings in a clear and concise manner.

## Acknowledgements
I would like to thank my supervisor, Dr. Till Riedel, for his support and guidance throughout the research process. Also special thanks to my fellow students for their feedback during the peer review sessions. I learned a lot from this experience and I am grateful for the opportunity to conduct this research.