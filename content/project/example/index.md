---
title: Colvillea
summary: A Physically Based GPU Ray Tracer
tags:
- Ray Tracing
- GPU
- Physically Based Rendering
date: "2020-07-15T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  caption: Rendering of Living-Room (Benedikt Bitterli's Resources) by Colvillea
  placement: 2
  focal_point: Smart

links:
- icon: github
  icon_pack: fab
  name: Code
  url: https://github.com/Hearwindsaying/Colvillea-archive

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
#slides: example
---

<!--
# Colvillea
![Dining-room](https://github.com/Hearwindsaying/Colvillea/blob/master/examples/Gallery/dining-room_interactive.jpg)
-->

## Overview
**Colvillea** is a physically based global illumination renderer running on GPU. It relies on [NVIDIA's OptiX](https://developer.nvidia.com/optix) to achieve parallelism by leveraging GPU resources, resulting in high performance ray tracing rendering.

{{% callout note %}}
This project is archived and I am working on a new version of **Colvillea** that has much better performance thanks to OptiX 7 and wavefront path tracing.
{{% /callout %}}


## Motivation
Here are some motivations and objectives of building Colvillea:
 - Ease for implementation of ray tracer in GPU. Writing a GPU renderer from scratch could be of great difficulty and hard to get optimal performance. Debugging is also a pain in the neck. There might be a way out for all these problems thanks to OptiX.
 - Deliver RTX hardware acceleration for faster rendering. OptiX is one of the three ways for enabling RTCores so as to achieve higher ray tracing efficiency when possible.
 - Potential for implementation of some state-of-the-art rendering technologies. This is a personal project written during my learning of computer graphics. In the end, it should be both easy and convenient to extend to adding more features. It's also interesting to try out rendering algorithms in GPU to explore a better efficiency. 

## Features
### Light Transport
 - Direct Lighting
 - Unidirectional Path Tracing

### Reflection Models
 - Lambertian BRDF
 - Specular BRDF (Perfect Mirror)
 - Specular BSDF (Perfect Glass)
 - Ashikhmin-Shirley BRDF (Rough Plastic)
 - GGX Microfacet BRDF (Rough Conductor)
 - GGX Microfacet BSDF (Rough Dielectric)
 - Dielectric-Couductor Two Layered BSDF

### Sampler
 - Independent Sampler
 - Halton QMC Sampler (Fast Random Permutation)    
 - Sobol QMC Sampler

### Filter
 - Box filter
 - Gaussian filter

### Rendering Mode
 - Progressive Rendering

### Light Source Models
 - Point Light
 - Quad Light (Spherical Rectangular Sampling)
 - Image-Based Lighting (HDRI Probe)

### Camera 
 - Pinhole Camera
 - Depth of Field

### Geometry
 - Triangle Mesh (Wavefront OBJ)

### Miscellaneous
 - LDR/HDR Image I/O with Gamma Correction
 - Interactive rendering with editing scene

## Build
Building **Colvillea** requires OptiX 6.0 (6.5 is preferred) and CUDA 9.0 or above installed. For graphics driver on Windows platform, driver version 436.02 or later is required. All NVIDIA GPUs of Compute Capability 5.0 (Maxwell) or higher are supported but those with Turing architecture is required to access RTX hardware acceleration.

**Colvillea** currently builds on Windows only using [CMake](http://www.cmake.org/download/) and could be built using MSVC successfully. It's recommeded that create a separte directory in the same level folder as src folder. Note that you are required to use VS2015 or above targeted for 64-bit as CUDA_HOST_COMPILER in configuration step.
For better layout to support interactive rendering, please put imgui.ini file to the same directory as colvillea.vcxproj.

## Selected Images

{{< gallery album="gallery" >}}


## References
 - [NVIDIA OptiX](https://developer.nvidia.com/optix)

 - [PBRT](https://github.com/mmp/pbrt-v3)

 - [Mitsuba](https://github.com/mitsuba-renderer/mitsuba)
