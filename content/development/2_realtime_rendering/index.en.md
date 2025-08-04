---
title: Realtime Rendering
subtitle: "Practical course at KIT"
summary: In this practical course, numerous realtime rendering techniques were implemented using an OpenGL framework. These include Level of Detail (LOD) techniques, Precomputed Lighting, Path Guiding, Denoising and ReSTIR.
date: 2025-04-26
cardimage: realtime_rendering_card.png
featureimage: realtime_rendering_card.png
caption: Village-Scene rendered with ReSTIR.
authors:
  - Dominik: author.png
---


## Assignment 1: Level of Detail (LOD)
In the first assignment I implemented a Level of Detail (LOD) technique for terrain rendering. It uses a heightmap to generate a terrain mesh and applies a tessellation shader to adaptively refine the mesh based on the projected screen space area of each quad. The technique allows for efficient rendering of large terrains while maintaining visual quality. It is an implementation of the Concurrent Binary Tree (CBT) algorithm, which dynamically adjusts the level of detail based on the camera's position and view direction. As described in the paper [Concurrent Binary Trees (with application to longest edge bisection)](https://onrendering.com/data/papers/cbt/ConcurrentBinaryTrees.pdf) by Jonathan Dupuy (Unity Technologies), the data structure maps well to modern GPU architectures, allowing for efficient traversal and rendering of the terrain mesh.
{{< figSingle src="images/1_cbt_terrain.png" caption="CBT implementation for adaptive terrain tesselation. The Mesh is finely tesselated near the camera. Progressively coarser tessellation is applied further away from the camera and outside the view frustum without introducing discontinuities. In this debug view, the different levels of the tree are visualized." >}}



## Assignment 2: Precomputed Lighting
Based on the presentation [Large-scale Global Illumination at Activision](https://research.activision.com/publications/2021/09/large-scale-global-illumination-in-call-of-duty) I implemented a precomputed lighting technique using spherical harmonics (SH). It utilizes a precomputed warped irradiance volume to store the lighting information for each surface point. A spatial grid is is used to store the SH coefficients which can be interpolated and used to evaluate the indirect illumination at runtime. The technique allows for efficient rendering of complex lighting scenarios with minimal runtime overhead. The vertical resolution is improved by remapping to the extend of the local geometry instead of using the height of the entire scene. While this complicates the trilinear interpolation, it allows for a more accurate representation of the lighting in the scene. During offline computation of the SH coefficients, the lighting samples are validated to include only irradiance of ouside areas, reducing darkening and light leaking artifacts.
{{< figSingle src="images/2_precomputed.png" caption="Precomputed lighting with spherical harmonics. The scene is illuminated by the environment map and a directional light source. Both contribute to the overall lighting. Realistic ambient occlusion and subtle color bleeding can be observed under the trees." >}}

## Assignment 3: Path Guiding and Denoising
The third assignment focused on path guiding and denoising techniques. I implemented a path guiding algorithm stores a von Mises-Fisher distribution in a screen-sized buffer. The algorithm is based on the paper [Real-Time Path-Guiding Based on Parametric Mixture Models](https://arxiv.org/abs/2112.09728) by Mikhail Derevyannykh. Beyond the scope of this assignment, I added temporal reporjection of the per-pixel distributions and utilized spatial sample reuse to improve the learning speed of the algorithm.

Even with guiding, the single-sample estimates can be noisy, especially in complex scenes with many light sources. To mitigate this, I implemented a denoiser based on the paper [Edge-Avoiding À-Trous Wavelet Transform for Fast Global Illumination Filtering](https://jo.dreggn.org/home/2010_atrous.pdf) by Dammertz et al. It uses a wavelet transform to filter the noise while preserving edges and details in the image. The à-trous filter implementation yields high performance on the GPU. A combination of three edge stopping functions based on the noisy pixel color, surface normal and world space position is used to preserve high-frequency details such as sharp shadows or object edges.
{{< figSingle src="images/3_pg_denoising.png" caption="*Left*: Path traced image. *Middle*: After denoising. *Right*: Path Guiding result after few seconds of learning the distributions." >}}

## Project: ReSTIR
As a final project for the course, we had the opportunity to implement an algorithm of our choice. I teamed up with Felix Mühlenberend to work on the Reservoir-based SpatioTemporal Importance Resampling (ReSTIR) algorithm. Our implementation focused on improving the efficiency of light sampling in complex scenes with many light sources. First, we extracted the emissive geometry at scene loading and added light sampling to the framework. Next we implemented [Resampled Importance Sampling (RIS)](https://diglib.eg.org/items/7b8d7c38-ee96-4415-acdd-3dd164fa8fad) as described by Talbot et al. in their paper. Finally, we extended this to full ReSTIR by implementing the spatio-temporal resampling steps as described in the [ReSTIR paper](https://research.nvidia.com/sites/default/files/pubs/2020-07_Spatiotemporal-reservoir-resampling/ReSTIR.pdf) by Bitterli et al. As recommended by the authors, we added an alias table for efficient sample generation based on the surface area. This lead to a significant performance increase over our naive sample generation. We evaluated our implementations on different scenes and presented the results to our fellow students. 
{{< figSingle src="images/4_restir_result.png" caption="RIS and ReSTIR compared to uniform light sampling on a many-light Sponza Scene." >}}

## Conclusion
The course provided a great opportunity to implement and experiment with various realtime rendering techniques. The assignments and project allowed me to deepen my understanding of the underlying algorithms and their practical applications in modern game engines. The use of OpenGL and GLSL for implementation provided a solid foundation for learning about graphics programming and real-time rendering techniques. Overall, the course was a valuable experience that enhanced my skills in computer graphics and realtime rendering.

Special thanks to the supervisors, Addis Dittebrandt, Mikhail Derevyannykh and Dmitrii Klepikov for their guidance and support throughout the course. Also, thanks to Felix for the great collaboration on the ReSTIR project. The course was a great learning experience and I look forward to applying the knowledge gained in future projects.

## Where is the code?
While I would love to share the code for this course, it is not publicly available. The course was conducted at the Karlsruhe Institute of Technology (KIT) and the framework is part of the course materials. Also, since a lot of work went into creating the framework and assignments, I do not want to spoil the experience for future students by uploading my solutions. If you are interested in the course, I recommend checking out the [KIT Computer Graphics Group](https://cg.ivd.kit.edu/index.php) website for more information on their courses and projects.