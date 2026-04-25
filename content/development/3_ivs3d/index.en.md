---
title: iVS3D
subtitle: "Preprocessing for Structure-From-Motion"
summary: iVS3D is a tool for preprocessing images for Structure-From-Motion (SfM) pipelines, including image selection, filtering, and metadata extraction.
date: 2025-12-22
cardimage: ivs3d_card.png
featureimage: ivs3d_card.png
caption: Main application window of iVS3D showing an image sequence with selected frames and GPS locations.
level: university
authors:
  - Dominik: author.png
links:
  - github: https://github.com/iVS3D/iVS3D
---

## Intelligent Video Sampler 3D
iVS3D (Intelligent Video Sampler 3D) is an open-source preprocessing framework for 3D reconstruction workflows. Instead of sending every frame of a video into a Structure-from-Motion pipeline, iVS3D helps produce a cleaner and more efficient dataset: selected images, synchronized metadata, and optional segmentation masks.

{{< vidSingle src="https://github.com/iVS3D/iVS3D/raw/refs/heads/video/iVS3D.mp4" poster="images/thumbnail.png" width="100%" >}}

Over the last few years, I have contributed to this project with a strong focus on engineering and extensibility. A major part of my work was improving and maintaining cross-platform development workflows based on Qt, OpenCV, and CMake, so the application can be built and used reliably across different operating systems (windows, linux) and hardware configurations (w/o CUDA).

Another key area was extending iVS3D through its plugin interface. The plugin architecture enables adding new image selection logic, mask generation, and data visualization capabilities, which makes experimentation and research iteration much faster. This approach is central to how iVS3D evolves from a frame sampler into a flexible preprocessing framework for different reconstruction scenarios.

I also worked on integrating neural network based capabilities using ONNX Runtime, including semantic segmentation (ConvNeXt, BiseNet), object detection (YOLO), and visual similarity (ResNet) analysis. These components help identifying useful frames, filtering distracting content, and generating masks that improve downstream reconstruction quality.

{{< figSingle src="images/semseg.png" caption="iVS3D Semantic Segmentation." >}}

One of the most useful aspects is the direct bridge to reconstruction: iVS3D can export prepared data and launch COLMAP/OpenMVS workflows locally or on a remote machine. Combined with ready-to-use releases (CPU and CUDA builds) and an extensible plugin interface, it has become a solid foundation for research and applied SfM projects.
