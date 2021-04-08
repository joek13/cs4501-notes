---
title: "11. Softmax Classifier"
date: 2021-03-30T12:53:47-04:00
draft: false
---

## Non-parametric models
- Don't need to fit training parameters
    - e.g., k-NN
    - Drawback: needs to keep ALL of its training data around to work properly

## Parametric models
- Somehow "summarize" the training data into a model

## Softmax Classifier
### Inference vs. Training
- Set for learning on, vs. set for evaluating correctness

### Supervised learning - classification
- Arrange training data into columns of (input, label)
- In the CIFAR-10 dataset, the images are 32x32x3 (res: 32x32, 3 channels)
- For this toy example, we're gonna pretend the inputs can be represented as vectors on \\(\mathbb{R}^4
\\)
    - Inputs
- Our labels {dog, cat, bear} are represented as {1, 2, 3}
    - Or "targets" or "ground truth"

### Convert to one-hot
- We convert our labels to one-hot vectors, i.e. 1 -> [1, 0, 0], 2 -> [0, 1, 0], 3 -> [0, 0, 1].

### Linear softmax
- Get activation values: each input entry is multiplied by some corresponding weight; their weighted sum can be biased 
- (Activation values can technically take on any values; normalization is necessary)
- Then the activation is normalized across the sum so they all sum to one
- Uses this activation function to achieve normalized confidence scores:

$$
    f_a = \frac{e^{g_a}}{e^{g_a} + e^{g_b} + e^{g_c}}
$$

### How to find W, b?
- Find values that minimize some cost or loss function