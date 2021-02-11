---
title: "03. More on Light"
date: 2021-02-11T12:39:09-05:00
draft: true
---

## The big reveal
- Vicente has a green screen and was lying about his office???

## Recap
- Fast shutter speed and small aperture size: doesn't allow much light
- Slow shutter speed, large aperture size: allows a lot of light
- We learned about homogenous coordinates, intrinsic/extrinsic camera matrices


### Recap: extrinsic vs. intrinsic
- Intrinsic parameters: things you can't control about the camera
    - Happen "inside" the camera
    - E.g., optical center, focal length, etc.
- Extrinsic parameters: things you can control, outside the camera
    - Position, rotation, etc.

# Light: what determines the color of a pixel?
- Light emanates from some source, bounces off of surface elements and strikes sensors/our eyes

### BRDF (Bidirectional reflectance distribution function)
- Very complex model for modeling reflections

### Types of surfaces
- Diffuse: light strikes at a point, and is reflected "almost uniformly" in all directions
    - Perfect diffuse surface = "Lambertian" surface
- Glossy: light strikes a point, is reflected "mostly" in one direction
    - A kind of specular surface
- Mirror: light strikes a point, is reflected entirely in one direction
    - A kind of specular surface

### Reflection
- Body reflection:
    - Diffuse reflection (e.g., clay)
- Surface reflection:
    - Specular reflection (e.g., metal)

### Phong reflection model
- Approximation of BRDF
- BRDF of many surfaces can be approximated by Lambertian + Specular model
    - One component is perfectly defuse
    - The other is a perfect mirror

Three components in the Phong model:
- Ambient light (constant we add to each value)
    - Illuminates every point in the scene equally
- Diffuse
    - Computed by a constant times (light direction dot normal) times diffuse coefficient
- Specular

Interesting consequence: diffuse doesn't depend at all on viewing angle

### "A photon's life choices"
- Absorption
- Diffusion
- Reflection
- Transparency
- Refraction
- Fluorescence
- Subsurface scattering
- Phosphorescence
- Interreflection

## The eye as a camera
- Well, not exactly.
- But we can think of the pupil as an aperture
- Rods/cones on the retina are sensors

## Image processing / filtering
### Color images as tensors
Tensor of shape `(width, height, 3)`

### Basic image processing
Brightening: multiply by a constant

### Color spaces: RGB
- Some drawbacks:
    - High correlation
    - Not based on human perception

### HSV
More intuitive: hue, saturation, value

### L*a*b*
Based on human perception: a "perceptually uniform" color spacee