---
title: "07. Hough Transform and SIFT Features"
date: 2021-02-25T12:38:59-05:00
draft: true
---

## Last class - interest points
- Corners
- Blobs (we didn't discuss)

## Today's class
- Blob detection - difference of Gaussians

## Line detection
- Distinct from edge detection
- We want to take a shape and divide it into the sum of rectangles

### Idea 1: lead with Sobel
- Sobel extracts horizontal / vertical edges
- ...but what if the image is rotated?
- Canny: let's detect all edges
- Introduces new issue: not all edges are lines

### Idea 2: count pixels that support each line hypothesis
- Use thresholding to decide which lines have the most support
- ...but what if the edges are rotated?

## Hough transform
- Early type of "voting scheme" for detecting lines
- Each pixel "casts a vote" for lines

General outline:
- Discretize *parameter space* into bins (parameters being slope and intercept)
- For each feature point in the image, put a vote in every bin in the parameter space that could have generated this point.
    - The "spoke" of lines that intersect this point.
- Find bins that have the most votes.

You *do* need to apply Sobel (or Canny) first, because we only want edges to vote

Then, we define a "buffer matrix" that describes every possible line.

E.g., \\(m\\) on the y-axis, \\(b\\) on the x-axis.

But there are problems with the \\((m,b)\\) parameter space.
- Unbounded parameter domains
- Vertical lines require infinte \\(m\\)

What if we use an alternative formula: polar equation of a line
$$
    xcos(\theta) + ysin(\theta) = \rho
$$
Now, our parameters are \\((\theta, \rho)\\). \\(Rng(\theta) = [0, \pi), Rng(\rho) = [0, \text{some sensible upper bound determined by image size})\\)

## Hough transform
As described, this is very slow, but optimizations exist.
Susceptible to some noise, can often detect spurious lines.

Each point \\((x, y)\\) in the image space will add a sinusoid in the hough transform parameter space.

### Incorporating image gradients
- When we detect an edge point, we also know its gradient direction
- But this means that the line is actually uniquely determined.

So we can optimize our transform by setting Theta according to the gradient. Voting is much easier now!!!

### Generalizing to other shapes
- We can vote in "circle space" to detect for circles, as long as we can think of a way to convert to a reasonable parameter space.

### For the quiz
- Make sure you learn how to read the Hough space of an image

## What about images without corners?
- Many organic images lack sharp corners.
- Corner detection is difficult on these.

## Blob filter
- "Laplacian of Gaussian" - circularly symmetric operator for blob detection in 2D

Uses Laplacian operator, \\(\nabla^2 f  = \frac{\partial^2 f}{\partial x^2} + \frac{\partial^2 f}{\partial y^2} \\)

## Symmetry
- Remember, filters tend to find things that "look like the filter"

## Accounting for scale
Scale-space detection
- Scale the image: simply convolve the image at several different revolutions, using the same kernel
- Scale the blob: convolve the image using different scaled kernels

## Efficient implementation
- Approximating the Laplacian using difference of gaussians