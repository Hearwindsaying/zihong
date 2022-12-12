---
# An instance of the Experience widget.
# Documentation: https://wowchemy.com/docs/page-builder/
widget: experience

# This file represents a page section.
headless: true

# Order that this section appears on the page.
weight: 65

title: Experience
subtitle:

# Date format for experience
#   Refer to https://wowchemy.com/docs/customization/#date-format
date_format: Jan 2006

# Experiences.
#   Add/remove as many `experience` items below as you like.
#   Required fields are `title`, `company`, and `date_start`.
#   Leave `date_end` empty if it's your current employer.
#   Begin multi-line descriptions with YAML's `|2-` multi-line prefix.
experience:
  - title: Rendering Engineer (Intern)
    company: Revobit
    company_logo: logo
    company_url: 'https://www.revobit.ai/'
    location: Guangzhou
    date_start: '2020-09-01'
    date_end: '2021-06-30'
    description: |3-
        * Worked on in-house real-time renderer designed for footwear manufacturing. Implemented Eric Heitz's Linearly Transform Cosine method for real-time shading polygonal area lights.

        * Reported and fixed several bugs of the offline renderer SDK.
        
        * Integrated a brand-new DirectX 12 renderer backend to the existing RHI (Render Harware Interface), being compatible to the current rendering pipeline and APIs. 

  - title: Rendering Engineer (Full-time)
    company: Revobit
    company_logo: logo
    company_url: 'https://www.revobit.ai/'
    location: Guangzhou
    date_start: '2021-07-01'
    date_end: '2022-08-20'
    description: |2-
        * Launched a new project on reference path tracer with high visual fidelity based on DirectX 12 backend and DXR (DirectX Ray Tracing) API.
        
        * Integrated NVIDIA's Realtime Denoiser and Intel's OpenImageDenoiser to the post-processing pipeline of the path tracer.
---
