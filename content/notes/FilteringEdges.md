---
title: "05. Filtering, Frequencies, and Edges"
date: 2021-02-18T12:40:58-05:00
draft: true
---

## Recap
- Convolution (most important)

## Today
- Sobel operator
- Filtering in frequency

## Sobel operator
- One sobel kernel detects vertical edges, another detects horizontal
- We take the absolute value of the output of each "dot product" because negative values don't make sense

## Sobel operators and calculus
- Sobel operators are equivalent to 2d partial derivatives of the image
- Vertical sobel operator - partial derivative with respect to X
    - A vertical edge is just a change in the image with respect to X
- Horizontal sobel operator - partial derivative with respect to Y
- We can compute magnitude and phase at each location
- Useful for detecting edges

"Where is the image changing in x and y?"

In image processing, convention is to describe your input image as \\(f[x,y]\\) (square brackets for discrete inputs)

### Dealing with discreteness
Digital images are not continuous, so we can't really take a derivative. But we can:

$$
    \Delta_x f[x,y] = f[x+1,y] - f[x,y]
$$

Also:
$$
    \Delta_x f[x,y] = f[x+1,y] - f[x-1,y]
$$

We can convert these definitions to convolutions.

i.e., second definition becomes:
$$
    k(x,y) = [-1, 0, 1]
$$

### Sobel operators
Vertical sobel operators smooth in Y and then differentiate in X.

The Sobel kernel is the column matrix \\([1,2,1] \times \\) the row matrix \\([1,0,-1]\\)

### Relationship to gradient
The vertical and horizontal sobel operators, taken together, represent the gradient of an iamge.

## Frequency
- A brief trip to the analog, continuous world

Some waves can be represented as the sum of other waves.
We can transmit signals by passing around "numbers in the time dimension."

Call some waveform \\(f(x)\\), such that \\(f(x) = g(x) + h(x)\\) where \\(g, h\\) are both sine waves

We *could* represent a signal in terms of its amplitude over time, but we can also represent it as intensity over different frequencies

### Any function can be approximated by polynomials
- Taylor series expansion: any function can be represented as a summation of polynomials
- ...if you let your final polynomial have a very high degree

But this is hard in practice. Periodic functions need to be approximated by many, many, many, many polynomials. The approximation won't last forever for a finite number of terms.

## Jean Baptiste Joseph Fourier
Crazy idea (1807): any function can be represented as the sum of sines and cosines.

Fourier transform takes a function in the time domain and transforms it to the frequency domain

- Fourier transform stores the magnitude and phase at each frequency
- Magnitude encodes how much signal there is at a particular frequency
- Phaes encodes spatial information indirectly.

## Issue: DFT is slow
Solution: FFT
- a much more efficient approximation of the DFT, so efficient that it is often implemented in hardware

## Convolution theorem
- "The fourier transform of the convolution of two functions is the product of their Fourier transforms."