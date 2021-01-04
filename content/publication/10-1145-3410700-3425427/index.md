---
# Documentation: https://wowchemy.com/docs/managing-content/

title: Spherical Light Integration over Spherical Caps via Spherical Harmonics
subtitle: ''
summary: ''
authors:
- Zihong Zhou
- Li-Yi Wei
tags:
- '"spherical harmonics"'
- '"area lighting"'
- '"ray tracing"'
categories: []
date: '2020-01-01'
lastmod: 2021-01-04T17:56:46+08:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ''
  focal_point: ''
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
publishDate: '2021-01-04T09:56:46.325885Z'
publication_types:
- '1'
abstract: 'Spherical area light sources are widely used in synthetic rendering. However,
  traditional Monte Carlo methods can require an excessive number of samples for sufficient
  accuracy. We propose a Spherical Harmonics (SH) based method to provide a trade-off
  between performance and accuracy. Our key idea is an analytical integration of SH
  over spherical caps. The SH integration is first decomposed into a weighted sum
  of Zonal Harmonics (ZH) integration, which could be evaluated using recurrence formulae.
  The resulting integration could then be used for rendering spherical area lights
  efficiently, saving 50% light samples at best while maintaining competitive accuracy.
  Our method can easily fit into an existing SH based rendering framework to support
  near-field sphere lighting. '
publication: '*SIGGRAPH Asia 2020 Technical Communications*'
url_pdf: https://doi.org/10.1145/3410700.3425427
doi: 10.1145/3410700.3425427
---
