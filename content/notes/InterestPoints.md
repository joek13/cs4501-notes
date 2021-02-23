---
title: "06. Interest Points: Corners and Blobs"
date: 2021-02-23T12:49:44-05:00
draft: true
---

### Recap
- Frequency domain
- Filtering in frequency
- Edge detection - "Canny"

Some goals:
- Detecting corners

Remember the Sobel operators? They can be thought of as "edge" detectors. Can we envision a similar procedure for corners?

### Edge detection
- Sobel + Thresholding
- Compute Sobel operators in \\(x\\) and \\(y\\) for each pixel in an image, then threshold based on magnitude

### Digression on Thresholding
Thresholding is "a very powerful algorithm" in computer vision

### Canny Edge Detector
- Produces cleaner, less noisy, more clearly delineated edges than the Sobel method
- Produces thin edges (1px wide)
- Tries to preserve edge connectivity
- Commonly implemented in image processing libraries.

Procedure:
1. Filter image with x, y derivatives of Gaussian
    - Apply Gaussian filter to image
    - Use Sobel (or alternative) to approximate x/y derivative of that image
    - Create two kernels whose values come from the x/y derivative of the Gaussian distribution function
    - Filter image with each kernel to find a "smoother" gradient
2. Find magnitude and orientation of gradient at each pixel
    - Magntiude: strength of change
    - Orientation: direction where gradient changes most strongly
3. Non-maximum suppression:
    - Thin multi-pixel wide "ridges" down to single pixel width
    - Makes our boundaries thinner, suppresses noise

### Non-maximum suppression
- Edges occur at the maximum value of the gradient
- Non-maximum suppression algorithm only keeps pixels that represent max gradient

### Hysterisis thresholding, connectivity analysis
More steps employed in Canny

#### Hysterisis thresholding
- Strengthens connected-but-weak edges, I think
    - Two thresholds, high and low
    - High threshold defines when we start new edges
    - Low threshold defines when we continue an edge
- Not super clear on this

## Corners, and Interest Points
- How to find corners
- What is a corner?

### What's so interesting?
- If we can find corners, maybe we can match images belonging to the same object?
- Or maybe we can triangulate the 3D coordinates of the image.

### Basic idea
- We should easily recognize a corner by looking through a small window
- Shifting the window in ANY direction should give a large change in intensity

This property is unique to conrners:
- Flat region: no change in any direction
- Edge: no change along the edge direction
- Corner: changes in any direction

### Harris corner detection
Compute the following matrix of squared gradients for every pixel.

$$
    M = \sum_{patch}{\begin{bmatrix}I_x^2 & I_xI_y \\\\ I_yI_x & I_y^2 \end{bmatrix}}
$$

Where \\(I_x, I_y\\) are gradients computed using Sobel or some other approximation.

E.g., : flat area has \\(I_x = I_y = 0\\). \\(M = 0\\)

Horizontal edge has \\(I_x = 0, I_y = b\\). 

Corner: \\(M = \begin{bmatrix}a & 0 \\\\ 0 & b\end{bmatrix}\\)

Compute \\(det(M)\\). If \\(det(M)\\) is greater than some threshold, then we say it's a corner.

#### Drawback
This works for corners that are aligned with the coordinate grid. But not for other corners.

To make it work for other corners, we use a modified formula:

\\(det(M) - 0.06 trace(M)^2 \\). We threshold it similarly.

This formula works because it essentially tests whether this matrix can be represented as a diagonal matrix under some rotation. (Under the correct rotation, our corners are aligned with the coordinate grid.)

(TODO: come back and study this)

