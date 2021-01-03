---
title: "Spherical Light Integration over Spherical Caps via Spherical Harmonics"

# Authors
# If you created a profile for a user (e.g. the default `admin` user), write the username (folder name) here 
# and it will be replaced with their full name and linked to their profile.
authors:
- admin
- Li-Yi Wei

# Author notes (optional)
#author_notes:
#- "Equal contribution"
#- "Equal contribution"

date: "2020-12-04T00:00:00Z"
doi: "https://doi.org/10.1145/3410700.3425427"

# Schedule page publish date (NOT publication's date).
publishDate: "2020-12-04T00:00:00Z"

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ["1"]

# Publication name and optional abbreviated publication name.
publication: In *SIGGRAPH Asia 2020 Technical Communications*
publication_short: In *SA' 20*

abstract: Spherical area light sources are widely used in synthetic rendering. However, traditional Monte Carlo methods can require an excessive number of samples for sufficient accuracy. We propose a Spherical Harmonics (SH) based method to provide a trade-off between performance and accuracy. Our key idea is an analytical integration of SH over spherical caps. The SH integration is first decomposed into a weighted sum of Zonal Harmonics (ZH) integration, which could be evaluated using recurrence formulae. The resulting integration could then be used for rendering spherical area lights efficiently, saving 50% light samples at best while maintaining competitive accuracy. Our method can easily fit into an existing SH based rendering framework to support near-field sphere lighting.

# Summary. An optional shortened abstract.
summary: We present triple sphere, a method to integrate spherical lights over spherical caps via spherical harmonics for rendering applications.

tags: []

# Display this page in the Featured widget?
featured: true

# Custom links (uncomment lines below)
# links:
# - name: Custom Link
#   url: http://example.org

url_pdf: ''
url_code: ''
url_dataset: ''
url_poster: ''
url_project: ''
url_slides: ''
url_source: ''
url_video: ''

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com/photos/pLCdAaMFLTE)'
  focal_point: ""
  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects:
- example

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides: example
---

{{% callout note %}}
Click the *Cite* button above to demo the feature to enable visitors to import publication metadata into their reference management software.
{{% /callout %}}

{{% callout note %}}
Create your slides in Markdown - click the *Slides* button to check out the example.
{{% /callout %}}

Supplementary notes can be added here, including [code, math, and images](https://wowchemy.com/docs/writing-markdown-latex/).
