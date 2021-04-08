---
title: "Convolutional Neural Networks"
date: 2021-04-08T13:19:54-04:00
draft: true
---

Important note: convolutional neural networks learn different kernels for each channel of an image, but the result of convolving each channels is then summed (like dot product)

so a 3x224x224 image will have 4x3x9x9 weights (4 output images, 3 input channels, 9x9 kernel for each) but an output of 4x224x224; not 12x224x224 or something else


