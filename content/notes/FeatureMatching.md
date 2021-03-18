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
- Use similar triangles to solve for disparities
- Use disparities to estimate depth

### Less simple case: when cameras aren't aligned
**Stereo image rectification**
- Reproject onto a common plane parallel to the line between optical centeers
    - Two homographies (3x3 transform), one for each input image reprojection
    - Note: matrices can only represent linear transformations
- Pixel motion is horizontal after this translation

### Robust feature-based alignment
- Extract features
- Compute *putative matches*
- Loop:
    - Hypothesize a transformation T for some small subset of matches
    - Verify the transformation (search for other matches consistent with T)

Sound familiar? This is exactly RANSAC

Mosaics have a natural interpretation in 3D
- The images are reprojected onto a common plane
- The mosaic is formed on this plane
- "Synthetic wide-angle camera"

### Image reprojection
- How to relate two images from the same center?
- Cast a ray through each pixel in first image
- Draw the pixel that ray intersects the second image
We can represent this as a 2d image warp instead of a 3d projection

### Image reprojection as a homography
- A projective transform is a mapping between any two picture planes with same center of projection
- Called a homography