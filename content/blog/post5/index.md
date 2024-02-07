---
title: Real Time Neural Path Guiding
subtitle: "Bachelor thesis"
summary: A novel neural network based path guiding technique for realtime path tracing. A small neural network is trainied in online fashion to approximate incident radiance in world space. This information is used for guiding scatter rays in future frames.
date: 2023-03-30
cardimage: bachelorthesis_card.png
featureimage: bachelorthesis.png
caption: Title page and a section about activation functions for the neural network from my bachelors thesis.
authors:
  - Dominik: author.png
links:
  - github: https://github.com/dom-wuest/NeuralPathGuiding
  - link: https://github.com/dom-wuest/Portfolio#readme
---
**Abstract**

With modern GPUs supporting hardware-accelerated ray tracing, we do have the ability to generate path-traced images in realtime. Due to the time constraint, the amount of rays per pixel and frame is limited to a few. This leads to high variance in the Monte Carlo estimate for the Radiative Transfer Equation. In this work we discuss state of the art techniques for reducing variance of direct and indirect illumination with the main focus on rendering dynamic scenes in realtime.

We propose a novel path guiding technique to reduce variance by learning an estimate of the 5D incident radiance field within the scene. A multilayer perceptron is used to partition the spatial domain and a parameterized model is fitted to approximate the directional domain of this radiance field. During rendering this estimated radiance field can be used to guide the paths towards directions of high incident radiance. As a parameterized model we examine the use of von Mises-Fisher distributions and derive a loss function to train the multilayer perceptron in online fashion. We evaluate different strategies to collect training data and test our approach on static and dynamic scenes.

**Concept**

In 2021 Muller et al. proposed a realtime radiance caching technique which uses a small multilayer perceptron to cache radiance. To see their paper click [here](https://research.nvidia.com/publication/2021-06_real-time-neural-radiance-caching-path-tracing). Their neural network implementation is fast enough to be trained and queried every single frame. In my thesis I use the same neural network approach, however instead of caching the radiance at a point in the scene, the multilayer perceptron learns the distribution of incident radiance at this point. This information can be used to guide future rays in more promissing directions and thus reduce noice in the final render. Over the course of roughly 60 frames, the multilayer perceptron is able to learn an approximation of the radiance distibution in a simple scenes and thus reduce the noise produced by the path tracer.

{{< figSingle src="images/learning_cornell.png" caption="A neural network learns the direction to the light source over time. This information can be used to reduce noise of a path tracer." >}}

**Limitations and Future Work**

In the current state the implementation suffers from numerical instability which causes flickering and in some cases introduces NaNs in the calculations. This is most likely due to the noisy samples used for training. As shown in my thesis, changes to the loss function reduced these issues. However, there is room for improvement, so further research is needed.

The use of a single-lobe von-Mises-Fisher distribution is not sufficient for representing more complex lighting. The use of multiple lobes or other distributions could improve the quality of the approximation sicnificantly. As shown below, in spots that are illuminated from to opposing light sources, the vMF approximates the incident radiance poorly. This results in a noisy output in those areas.

{{< figSingle src="images/vMF_limits.png" caption="Single-lobe vMF poorly approximates illumination from opposing light sources." >}}

**Acknowledgement**

The codebase for my thesis was kindly provided by Egor Feklisov and Dmitrii Klepikov from Moscow State University. Their work got me setup for my research quickly and allowed many interesting experiments.

Special thanks to Mikhail Dereviannykh and Dr. Johannes Schudeiske, who gave me this amazing opportunity and supported me with valuable advice during my research!

Check out their research at (https://www.mishok43.com/home) and (https://jo.dreggn.org/home/)!