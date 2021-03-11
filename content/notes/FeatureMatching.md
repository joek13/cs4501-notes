---
title: "09. Feature Matching and Dense Stereo"
date: 2021-03-11T12:37:18-05:00
draft: true
---
## Recap
- Camera calibration (solving some complex linear algebra problem to determine what the camera matrix is)
    - We have a little bit of noise, so our giant system probably won't have a single solution


## Panorama Stitching (more later)

## Dense Stereo
Using two views of an object to extract information about it in three dimensions

### Motivation
Structure and depth are inherently ambiguous from single views
- Scale is ambiguous

### Extracting 3d information
- Shading; light is brightest when it strikes along the surface normal; dark when the two are orthogonal
- Focus/blurring; can use focus to distinguish foreground from background
- Texture; extracting shape from, say, the roughly equidistant seeds of a strawberry
- Motion

### Estimating scene shape
- "Shape from X": shading, texture, focus, motion, ...

Stereo:
- Shape from "motion" between two views
- Infer 3d shape of scene from two (multiple) images taken from slightly different viewpoints

Take inspiration from human stereopsis: we infer depth from the slight visual disparity between each eye

## Epipolar geometry

### Simplest case: parallel cameras
- Perform correspondence search pixel-by-pixel across images
    - Only really works if we have good texture and no repetition