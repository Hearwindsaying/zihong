---
title: Living-Room in Unity
#subtitle: Welcome 👋 We know that first impressions are important, so we've populated your new site with some initial content to help you get familiar with everything in no time.

# Summary for listings and search engines
summary: Bring the living-room scene to Unity.

# Link this post with a project
projects: [livingroom-in-unity]

# Date published
date: "2016-04-20T00:00:00Z"

# Date updated
lastmod: "2020-12-13T00:00:00Z"

# Is this an unpublished draft?
draft: false

# Show this page in the Featured widget?
featured: false

# Featured image
# Place an image named `featured.jpg/png` in this page's folder and customize its options here.
image:
  caption: 'The living-room rendered in Unity'
  focal_point: ""
  placement: 3
  preview_only: false

authors:
- Zihong Zhou

tags:
- Project

categories:
- Unity
- Rendering
---

## Notes
This is my final project for a virtual reality and game development course.
My contribution is bringing a Benedikt Bitterli's famous rendering scene living-room to Unity and showing how we could use various rasterization techniques to approximate the beauty image produced by offline renderer.

## Forewords
Ray tracing is an elegant algorithm used in computer graphics to synthesis realistic images.
It shoots tremendous rays to find intersection with geometries in the scene and shading with lights and tries its best to simulate the light transport process in nature.
The algorithm is not so fast however and it is not unusual to spend hours to days rendering a single image for the complex scenes produced by artists in the movie industry.

Rasterization on the other hand, represents a way to render in an efficient way, which is used ubiquitously in realtime rendering.
Thanks to the efforts of many graphics researchers and engineers for many years, realtime rendering could already produce some good-looking images nowadays.
Consequently, in this project I'd like to find out how good it could be in a game engine.

Note that these days realtime ray tracing becomes popular due to the introduction of NVIDIA's RTX architecture in Turing GPUs, which is able to do the ray intersection in a lightning fast way.
However, it requires a decent graphics card and my old GTX-960M is a bit out-of-date.
So I give up the idea and turn to Unity's HDRP Rendering Pipeline (The High Definition Render Pipeline) for the project.

## General
To generate an image as realistic as possible, we need to choose a GI (Global Illumination) system in Unity.
We will miss the nice indirect lighting, reflections for example if we skip this part.

Global Illumination Off             |  Global Illumination On
:-------------------------:|:-------------------------:
![](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@8.1/manual/Images/RayTracedGlobalIllumination1.png)  |  ![](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@8.1/manual/Images/RayTracedGlobalIllumination2.png)

Unity engine has several built-in solutions for achieving Global Illumination:
{{< figure src="gi_selection.png" caption="Two global illumination systems in Unity engine. Image courtesy of Unity documentation." numbered="false" >}}

{{% callout note %}}
*Update in 2021: Note that Enlighten is deprecated and we are suggested to use CPU or GPU-based Progressive Lightmapper instead.*
{{% /callout %}}

I attempted to use Enlighten in the first place and do not have a good experience since it is laborious to play with the parameters so as to reach my expectation.
I then turned to CPU and GPU based Progressive Lightmapper for the job.
Progressiveness indicates we could have a somewhat coarse preview immediately and it gradually gets refined as we wait.
This is usually preferred by lots of artists since it saves time for fast iterations.

## Sky and Fog Volume
To begin with, we should have a sky!

{{< figure src="preview-sky.png" caption="Our sunset skybox for the living room." numbered="false" >}}

I chose to use a sky from HDRI probe, which would also be the primary luminary for our scene.
We just need to import our HDRI panorama as a cubemap by setting the *Texture Shape* as *Cube* and using *Trilinear Filter*:

{{< figure src="sky.png" caption="Import our skybox with cubemap and trilinear filter." numbered="false" >}}

We could preview our loaded HDRI Sky in the scene as well by setting up the Volume:

{{< figure src="k1-volume.png" caption="Set up the HDRI Sky in Volume." numbered="false" >}}

Remember we need to specifiy the sky in the **Lighting/Environment HDR**.

{{< figure src="k0-hdri.png" caption="Specify our sky in Lighting." numbered="false" >}}

## Cleanup the Scene
The living-room scene is from [Benedikt Bitterli's Rendering Resources](https://benedikt-bitterli.me/resources/):

{{< figure src="s1_about_the_scene.png" caption="The living room I chosed." numbered="false" >}}

I first import all meshes (*.obj) into Maya and group the objects by materials according to the provided scene description file (.xml).
This could reduce our time for authoring and assigning materials in Unity later.

{{< figure src="s2-maya-group.png" caption="Group and name objects by materials in Maya." numbered="false" >}}

I also check the normals facing outwards and ensure the Y axis is up (the convention Unity uses):

{{< figure src="s3-fix-normals.png" caption="Visualize the normal to check the face orientation." numbered="false" >}}

## Import the Scene
After fixing all issues in the [last section](#cleanup-the-scene), it should work well to export the scene as FBX and import in Unity.

However, there is an issue to be considered -- what is our scale of the scene?
This is important since we have limited precision for representing decimal in computer science.
For example, the intersection point may slightly below the surface and when it shoots a shadow ray to the light to find out whether it's blocked or not, it will be occluded by itself -- a phenomena known as *shadow acne*.

{{< figure src="shadow-acne.png" caption="Shadow acne artifacts due to the error of loating point. Image courtesy of Scratchpixel 2.0." numbered="false" >}}

An idea is to offset the intersection pooint by epsilon, which should be related to the scale of the scene.
If our scene lives in a small world, 'a miss (ray epsilon in this context) is as good as a mile'!
Our scale or units thus should chosed in a *consistent* way throughout the scene to avoid these annoying artifacts.

One of the simplest solutions is to compare the imported scene with the default primitive in Unity.
A standard cube here has the length of 1 meter and I just scale our scene to make it match the scale -- a 5m\*10m*5m living room.

{{< figure src="s4-fix-units.png" caption="Scale our scene according to the standard cube in Unity to fix the unit." numbered="false" >}}

## Testing Global Illumination
After importing the models, it is time for playing around with the global illumination system now!
We could first ignore the minute props in the scene such as plants and the statue and check whether the global illumination works well for the 'global' environment, the look of the house.
So enable the paneling, ceiling, floor, wall and the fireplace glass only and tick **Contribute Global Illumination** under **Inspector/Mesh Renderer/Lighting**.

{{< figure src="s5-test-gi.png" caption="Parameters required to contribute global illumination." numbered="false" >}}

And we could enable the baked GI solution under **Lighting/Mixed Lighting** and **Lighting/Lightmapping Settings**.

{{< figure src="s7-bake-settings.png" caption="Settings for lightmap baking." numbered="false" >}}

Progressive GPU lightmapper is preferred when we have enough GPU memory (at least 4GB), which is generally the way much faster than the CPU one.
It requires us to have a GPU supporting OpenCL 2.2 as well.

Multiple importance sampling should always be enabled since it helps reduce variance by combining several sampling strategies.
Throwing more direct and indirect samples helps reduce noises even more, but it increases the baking time as well.
So we have to make a trade-off between the quality and time.
But that's not the whole story, since we could apply filtering even if we use fewer number of samples to get a decent result.
By selecting the **Auto** setting for the **Filtering**, unity will do all the magic for us!

Since we are using baked GI solution, so we must have a second UV for lightmapping.
This is done by Unity by enabling **Generate Lightmap UVs** during FBX import.

{{< figure src="s6-bake-lightmap.png" caption="Let Unity generate the lightmap UVs for us." numbered="false" >}}

## Material and Reflections
Since we have already grouped the meshes by materials, we could just assign each group of mesh with a unique material.
For the ceiling and the wall, we want a Lambertian BSDF as specified in the xml file.
I just use a simple **HDRP/Lit** shader with **Metallic = 0** and **Smoothness = 0**.

| Material | Base Color     |
| :------------ | :-----------: |
| ceiling  | R=G=B=0.578596 |
| wall     | R=G=B=0.4528   |

{{< figure src="s8-ceiling.png" caption="Setup for our ceiling material to match a Lambertian BSDF." numbered="false" >}}

For the floor and paneling, we need to emulate the substrate BSDF or rough-coating BSDF with the underlying BSDF being Lambertian and coated with a rough dielectric BSDF with GGX distribution.

{{< figure src="bsdf-roughcoating.png" caption="Illustration for light transport in a rough-coating BSDF. Image courtesy of Mitsuba 0.5 documentation." numbered="false" >}}

Thanks to the Laurent Belcour's excellent work on [layered material](https://belcour.github.io/blog/research/publication/2018/05/05/brdf-realtime-layered.html), we could easily simulate this kind of coating material in Unity using **StackLit** shader.

We shall use the Shader Graph to finish the task.
Here is what we have for the floor:

{{< figure src="s9-floor.png" caption="Shader Graph setup for the layered floor material." numbered="false" >}}

And the paneling material:

{{< figure src="s10-paneling.png" caption="Shader Graph setup for the paneling." numbered="false" >}}

The last material for our "global" environment is the fireplace, which is a perfectly smooth specular shader.
Besides setting the **Smoothness = 1** with **StackLit**, we need to deal with the reflection.
This is one of the nasty stuff in realtime rendering -- though reflection itself is a part of the global illumination, we still need to explicitly achieve the effect by using another technique -- Reflection Probes.
Here we create a reflection probe to capture the interior environment for the fireplace.
Clicking **Bake** option under the **Lighting**, we get the nice reflection for the fireplace!

{{< figure src="s11-probe.png" caption="Fix the reflection of our fireplace." numbered="false" >}}

But not for the interior, oops!

{{< figure src="s12-probe-global.jpg" caption="A weird look of our interior." numbered="false" >}}

It may not be so obvious, but the interior gets reflection from the exterior HDRI or Skybox instead of the interior -- the floor is not missing, but reflecting the bright sky!
This is due to the lack of another reflection probe for the scene.

So we could easily address this by adding another probe:

{{< figure src="s13-probe.png" caption="Use yet another reflection probe for interior reflections." numbered="false" >}}

and bake!

{{< figure src="s14-fixed-probe.png" caption="A corrected interior look." numbered="false" >}}

## Details and Props
It looks we are on the right track now, we could start to add more details for the scene!

After enabling all props meshes, we begin with the brushed steel.
It is like the fireplace glass, but we set the **Metallic = 1** to simulate the metal.
As for the painting back and the table wood, we could use the same material with the floor, with different base color textures.
The sofa, painting, pot, leaves and dirt are just the Lambertians so **HDRP/Lit** works well.

Note that we need to use **Translucent** material type for the leaves and alpha cutout the geometries according to the leaves map.

{{< figure src="s15-leaves.png" caption="Material setup for the leaves." numbered="false" >}}

Finally, we use a transparent surface type for the glass material.

{{< figure src="s16-glass.png" caption="Material setup for the glass." numbered="false" >}}

Here comes another nasty stuff in realtime rendering -- refraction.
Refraction is notoriously difficult to achieve in realtime rendering and is usually approximated by Screen Space Refraction:

{{< figure src="s18-glass.png" caption="Enable Screen Space Refraction in the volume setting." numbered="false" >}}

## Results and Discussions
After adding up all props and setting up the materials correctly, we could simply bake our GI and here is what I get:

{{< figure src="s19-final.png" caption="Final baked result for the living room in Unity!" numbered="false" >}}

It looks kind of cool -- perhaps not in a sense of realism but in a artistic style.

{{< figure src="../../project/example/featured.jpg" caption="Path traced reference image rendered by my **[Colvillea](https://hearwindsaying.github.io/project/example/)** renderer." numbered="false" >}}

By comparing with the ground truth image from the ray tracing [sGT Image], we find that the glass seems to be weird and we lack all the nice occlusion from the objects.
As for the user's experience, I think it requires artists to pay more attention to the stuff behind rendering.
For example, we have to consider the resolution or padding for the lightmap UVs, tuning the baking parameters, fixing light leaking due to the lack of reflection probes etc.

However, the image generated still looks good and the performance in realtime framerates (~80 FPS) is appealing; or we have to wait for hours to get a noise-free image using offline ray tracing!

Here is another result by leveraging the post-processing pipeline:

{{< figure src="s20-post-process.png" caption="Featured image for the living-room after post processing." numbered="false" >}}

## References
 - [Unity's Blog for HDRP](https://blogs.unity3d.com/2018/09/24/the-high-definition-render-pipeline-getting-started-guide-for-artists/)
 - [Unity's Documentation for HDRP](https://docs.unity3d.com/Packages/com.unity.render-pipelines.high-definition@7.1/manual/index.html)
 - [ArchViz with Unity's HDRP](https://www.youtube.com/watch?v=k05G2QNrvPE)
 - [Fontainebleau Demo -- A Unity's Official Demo for HDRP](https://github.com/Unity-Technologies/FontainebleauDemo)
 - [Laurent Belcour's Layered BSDF Paper](https://dl.acm.org/doi/10.1145/3197517.3201289)
