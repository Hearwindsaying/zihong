---
title: 3D Digital Modeling FA22
summary: "Projects for CS22/122: 3D Digital Modeling."
tags:
- Rendering
- Digital Arts
- Final Project
date: "2020-07-15T00:00:00Z"

# Optional external URL for project (replaces project detail page).
external_link: ""

image:
  #caption: Rendering of Living-Room (Benedikt Bitterli's Resources) by Colvillea
  placement: 2
  focal_point: Smart

# links:
# - icon: github
#   icon_pack: fab
#   name: Code
#   url: https://github.com/Hearwindsaying/Colvillea-archive

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

Here are some of selected shots from [Prof. Lorie Loeb's modeling class](https://www.cs22.space/)[^1] I took in Fall 22.
Interestingly, I also took [Prof. Wojciech Jarosz's rendering algorithms](https://cs87-dartmouth.github.io/Fall2022/darts-overview.html) in FA22 and they are somewhat complementary to each other.
Rendering Algorithms tells us how to render photorealistic images given the scene and Digital Modeling tells us how to author the scene for a renderer and use the renderer from an artistic perspective. 

# Classroom

{{< figure src="https://cdna.artstation.com/p/assets/images/images/022/431/184/large/u-like-erkinbekov-school-room7.jpg?1575407742" caption="Motivation image from artstation. Credits: https://www.artstation.com/artwork/L20Kbl" numbered="true" id="sneaky">}}

{{< figure src="1-try-to-match-reference-img.jpg" caption="Attempts at reproducing the motivation classroom, with some customization." numbered="true" id="sneaky">}}

{{< figure src="featured.jpg" caption="Best shot I love. CS87/287 Rendering Algorithms is so hard! " numbered="true" id="sneaky">}}

{{< figure src="3-bring-pbrt-alive-and-correct.jpg" caption="Bring pbrt into live! " numbered="true" id="sneaky">}}

{{< figure src="4-looking-back.jpg" caption="Looking back at the classroom. " numbered="true" id="sneaky">}}

{{< figure src="5-scratch-some-volumetrics.jpg" caption="Scratch with some volumetrics rendering. " numbered="true" id="sneaky">}}

[^1]: I have two shots, room and abstract rendering featured on the course website (Winter 23 version)!

# Abstract

{{< figure src="portal.jpg" caption="Portal in Big Hero 6. Image credits: http://alexey.stomakhin.com/research/portal.html " numbered="true" id="sneaky">}}

My abstract design is inspired by a [talk at SIGGRAPH 2015 -- Big Hero 6: Into the Portal](https://media.disneyanimation.com/uploads/production/publication_asset/140/asset/BH6_Into_the_Portal.pdf). 
They author this portal using a variation of Mandelbrot fractals with volumetric path tracing.
I went in another direction instead by applying deformers to geometry.

{{< figure src="wip_abstract.png" caption="My portal design WIP. Rendered with Arnold for Maya 2022" numbered="true" id="sneaky">}}

{{< figure src="zihong_abstract.jpg" caption="Final rendering for my abstract." numbered="true" id="sneaky">}}

# Credits
Modeling, UV layout and rendering are done by myself.
Textures are external resources:

Mathematicians:
 - https://www.thefamouspeople.com/profiles/archimedes-422.php
 - https://en.wikipedia.org/wiki/Carl_Friedrich_Gauss#/media/File:Carl_Friedrich_Gauss_1840_by_Jensen.jpg
 - https://en.wikipedia.org/wiki/Leonhard_Euler#/media/File:Leonhard_Euler_-_edit1.jpg
 - https://www.usna.edu/Users/math/meh/riemann.html
 - http://scihi.org/wp-content/uploads/2014/04/Henri_Poincare2.jpg
 - http://scihi.org/henri-poincare/
 - https://en.wikipedia.org/wiki/Joseph-Louis_Lagrange#/media/File:Лагранж.jpg
 - https://www.sapaviva.com/euclid-of-alexandria/
 - https://en.wikipedia.org/wiki/David_Hilbert
 - https://en.wikipedia.org/wiki/Gottfried_Wilhelm_Leibniz#/media/File:Christoph_Bernhard_Francke_-_Bildnis_des_Philosophen_Leibniz_(ca._1695).jpg
 - https://upload.wikimedia.org/wikipedia/commons/e/ef/Alexander_Grothendieck.jpg
 - https://upload.wikimedia.org/wikipedia/commons/f/f3/Pierre_de_Fermat.jpg
 - https://upload.wikimedia.org/wikipedia/commons/5/53/Evariste_galois.jpg
 - https://www.daviddarling.info/images/Riemann.jpg
 - https://www.mapsofindia.com/world-map/world-political-map-2020.jpg?v:1.0

Others:
 - Chalkboard: https://www.freepik.com/free-photo/old-black-background-grunge-texture-dark-wallpaper-blackboard-chalkboard-concrete_20038789.htm#query=chalkboard%20texture&position=3&from_view=keyword
 - Wall hangings are from my portfolio: https://hearwindsaying.github.io/portfolioWeb/index.html
 - Grid texture and pbrt book cover textures are from pbrt-v2 (miscquads.pbrt）: https://www.pbrt.org/scenes-v2
 - MDLHandbook picture is from NVIDIA MDL Handbook:
 - http://mdlhandbook.com/
 - Several book pages are from pbrt-v3: https://pbr-book.org/
 - HDRI are from: https://polyhaven.com/a/garden_nook
 - Quiz pages are from CS87/287 Rendering Algorithms Quiz
 - Source images for wine bottle: https://www.youtube.com/watch?v=4R0e6O5afE4

