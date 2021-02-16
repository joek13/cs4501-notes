---
title: "04. Image Filtering, Image Frequencies"
date: 2021-02-16T12:30:08-05:00
draft: true
---

## Recap
Previous class:
- The human eye as a camera
- Images as matrices
- Images as functions
- Image processing
- Image filtering

## Today's topics
- Image filtering: mean filter
- Image blurring
- Image gradients
- Image frequency

### Certified Vicente Moment
- Vicente noticed very few people were attending class, so he took attendance
- ...but there's no attendance grade in the syllabus, so he just did it to put a psychologically scary (but practically insignificant) zero in vagrants' gradebooks

### Color images as tensors
- Tensors of shape `(width, height, channels)` (where `channels` is usually 3)

## Image filtering
### Mean filter
Say we have a "peppered image"—an otherwise normal image with pixels randomly zeroed out.

How would we correct this computationally?

**Idea 1:** Take the mean of each neeighborhood of pixels

Issues:
- Zero pixels are negatively skewed, so their neighborhoods are extremely dark
    - Recall from stats: as a measure of central tendency, mean isn't robust to outliers
- Blurs the image

**Idea 2:** median filter
- Replace each pixel with the median value of its surrounding neighborhood

Issues:
- Introduces some distortion in noiseless parts of the image

### Image filtering: convolution operator
- Idea: for each neighborhood of pixels in the input image, compute a linear combination of these values and use them to compute an output image
General form:
$$
    g(x,y) = \sum_v{\sum_u{k(u,v) \times f(x - u, y - v)}}
$$

(**Convention note:** \\((u, v)\\) represents row-major order)

**Key**
- \\(k(u,v)\\): our kernel.
- \\(f(x, y)\\): our input image.
- \\(g(x,y)\\): our output image.

### Mean filter as a convolution
a.k.a., box filter
$$
k(u,v) = \frac{1}{9}
$$

(for a \\(3 \times 3\\) kernel)

### Gaussian blur
Kernel is calculated from the Gaussian (normal) distribution
- Note: even though any well-formed statistical distribution has to have a maximum cumulative probabiltiy of 1, this isn't a requirement of our kernel
- We can make kernels that don't sum to 1, and many Gaussian blurs don't do this

## Practical considerations
- What do we do at the edges?
    - Clip image
    - Mirror image off at boundaries
    - Wrap around

## Key properties of linear filters
- **Linearity**: \\( f_{1+2}(I) = f_{1}(I) + f_2(I) \\)
    - Applying filter 1 and then filter 2 two an image is same as applying a single filter whose kernel is the sum of 1 and 2's kernels
- **Shift invariance**: Filtering with a shifted filter is the same as filtering a shifted image

## Uses
- Enhance images
- Extract information
- Detect patterns
- DCNNs