---
title: "01. Introduction: What is Computer Vision?"
date: 2021-02-04T12:37:42-05:00
draft: true
---

## A "ridiculously brief" history of computer vision
- Most computers didn't have graphical interfaces until relatively recently
- 2010s: deep learning / convolutional approaches flourish

## Some high-reliability domains
- Digit / letter recognition (check reading, license plate recognition)
- Facial recognition
- Biometrics
- Getting there: object recognition
    - e.g., iNaturalist species recognition
- Special FX
    - e.g., using video to capture actors' facial expressions, then rendering
- Sportsvision first-down line
- Medical imaging
- Smart cars
- Gaming (Kinect)
- Industrial robotics

## What's so hard?
Seeing is:
- Cognitively intensive ("a great feat of natural intelligence")
- Nontrivial
    - Optical illusions, negative space (gestalt principle), ambiguities

Computer vision is not "just pattern recognition." Seeing requires world knowledge, an understanding of context

## What is an image?
To us, they're easily understood. But to computers, images are two-dimensional arrays of intensities

Claim: intensity arrays and the visual experience of an image contain the same information; they are merely different representations

Processing one of these representations is almost an automatic process for most of us...

For example: how do we know what an image is like in three dimensions—from a two-dimensional projection?
- There are multiple candidate objects for a single 2-d projection. How do we decide which is real?
    - Using world knowledge and context.

#### Other challenges
- Variable illumination
- Background clutter
- Intra-class variation
    - Some weird chairs look very different, but they're still chairs

## What is the state of the art?
- Given enough data, many systems are surprisingly robust to the previously outlined challenges
- But still not at the same level as humans, despite the hype
- Still many open challenges, such as few-shot learning, transfer learning, and unsupervised learning

## Non-technical technical discussion: Cameras
Claim: cameras "exist in nature" and are discovered rather than invented

### Accidental cameras
Pinhole cameras can be made accidentally, like using windows and a shutter

## Let's design a camera
Idea 1: just put a piece of film in front of an object. Do we get a reasonable image?
- No... every point in the image projects to every point in the film, leading to a blurred mess

Idea 2: add a barrier with a hole to block off most of the rays
- Reduces blurring
- Opening is known as the _aperture_

Historical note: the word "camera" comes from Latin, _camera obscura_. _Camera_ means room. The _camera obscura_ is a dark room with a small aperture, known to ancient Greek and Chinese scholars

Can "save" the image on a camera by projecting onto a piece of paper and tracing over by hand.
Later, by burning into a coating of photosensitive Syrian asphalt on a pewter plate. But it takes several hours.

Next, the "Daguerrotype," an improved version that used better optics in the lens and a more sensitive "film" material.

Eastman Kodak Company, in 1885, uses nitrate film

### Back to the pinhole camera
- The image in a pinhole camera gets projected upside down
- Two new concepts:
    - \\(f\\), focal length = distance between aperture and image plane
    - \\(c\\), pinhole center radius (aperture size)

### Projective geometry
Cameras turn three-dimensional scenes into two-dimensional projections

What is not preserved?
- Area
- Length
- Angles (parallel lines converge at a "vanishing point")

What is preserved? (in a standard, perfect pinhole camera)
- Straight lines are straight

For our purposes, a pinhole camera model is a good approximation of an actual camera.

## Digital cameras
A digital camera replaces film with a sensor array. Each cell in the array is a light-sensitive diode that converts photons to electrons.

Early digital cameras were much lower resolution than film cameras, because they couldn't fit very many sensors in the sensor array