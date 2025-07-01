---
title: 2D Fluid Simulation on the GPU
subtitle: Practical course at KIT
summary: A 2D grid based fluid simulation built with Vulkan compute shaders to utilize GPU hardware.
date: 2023-08-02
cardimage: fluid_card.png
featureimage: fluid.png
caption: Wind tunnel scene simulating turbulent flow around a circle.
authors:
  - Dominik: author.png
links:
  - github: 
      url: https://github.com/dom-wuest/FluidSim2D
      label: Source code
  - pdf: 
      url: https://github.com/dom-wuest/FluidSim2D/raw/main/docs/TechnicalReport.pdf?download=
      label: Technical report
---
## About this project
This project is focused on implementing and optimizing a fluid simulation using Vulkan compute shaders. A grid-based approach has been taken as this maps to GPU memory efficiently and allows for optimizations later on.
The simulation domain is limited to 2D as this simplifies visualization. In this project, compute and present queues are created, and the simulation steps are synchronized to be executed in the correct order. A simulation step is split into advection, pressure projection and visualization. These steps are implemented in different compute shaders which require synchronization as well. A naive implementation of these shaders was used for reference when optimizing performance. For this, a detailed performance analysis was performed using Nvidia Nsight Graphics. Besides optimizing shader dispatches in general by supporting multiple frames in flight, the pressure projection shader was optimized specifically with memory throughput in mind. The performance analysis showed that this shader dominated the duration of a simulation step. The shader itself is memory-bound as it propagates pressure values through the grid iteratively. Here we see a lot of potential for optimization and implemented different techniques such as ghost zoning, kernel decomposition and loop unrolling to increase performance. For technical details and the results of our performance analysis, refer to the [technical report](https://github.com/dom-wuest/FluidSim2D/blob/main/docs/TechnicalReport.pdf).

## Key features and optimizations

Feature | Status
--------|-------
fluid advection | ✔️
resolve fluid incompressibility | ✔️
scenes with different boundary conditions | ✔️
mouse interaction | ✔️
cli | ✔️
pressure visualization | ✔️
windows support | ✔️
linux support | ✔️

The performance of a naive implementation is far from optimal. To compute more simulation steps per second, the performance was analyzed using Nvidia Nsight Graphics, and the most significant bottlenecks were identified. 
Overall the simulation is memory-bound as most shader dispatches require data from neighbouring grid cells as well. Multiple optimization techniques have been used to increase GPU utilization and throughput.

Optimization | Status | Details
-------------|--------|----------
reduce required memory bandwidth | ✔️ | optimized pressure projection step as it dominates the simulation time
support multiple frames in flight | ✔️ | don't wait for simulation step to finish, start next step asap
decouple simulation resolution | ✔️ | support different resolutions for simulation grid and output buffer

![Pressurbox scene](./images/pressurebox.png)

## Technical report
An important goal of this project is to learn the skills necessary to write high-performance GPU code. To achieve this the simulation is implemented using the Vulkan. The naive implementation was analyzed thoroughly using [Nvidia Nsigh Graphics](https://developer.nvidia.com/nsight-graphics). Slow shaders and bottlenecks within the shaders were identified and the main performance limiters were optimized to improve overall performance:

![Analysis using Nsight Graphics](./images/nsight-optimized.png)

For details about the implementation and optimization of the simulation take a look at the [technical report](https://github.com/dom-wuest/FluidSim2D/blob/main/docs/TechnicalReport.pdf). It contains information about the underlying physics of fluids and a description of the simulation steps that were implemented. In the technical report, there is a section about performance analysis and optimization on the GPU. For this project dependent texture reads (DTRs) were removed, the workgroup size was optimized and ghost zoning was implemented to make use of shared memory (left). The improvements were analyzed and compared to the naive implementation (right).

![ghost zoning and performance gain](./images/optimization.png)

## Acknowledgments
Special thanks to Mike and Reiner for supervising the project, providing important feedback and motivating the implementation of ghost zoning for a significant performance gain.