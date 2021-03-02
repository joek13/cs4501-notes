---
title: "08. Camera Calibration, Dense Stereo"
date: 2021-03-02T13:26:51-05:00
draft: true
---

# Camera Calibration
- Goal: find parameters of the camera transformation matrix
Recall:
$$
    x = K \begin{bmatrix} R & t \end{bmatrix}X
$$
So our goal is to find \\(K \begin{bmatrix} R & t \end{bmatrix}\\)

## Calibrating the camera
- Use a scene with known geometry
- Get a least-squares solution
- Use some room with markers; we know the real-world location of these markers and we know the image location of these markers
- Fit camera parameters to satisfy these knowns
- To solve this system, we need *at least* 6 known points
    - But in practice, many more than 6 are used

- We use SVD to solve this system of linear equations ***(how? linear algebra that i'll have to go learn on my own)***
(We can technically use any method of solving linear equations)

After performing calibration, we can do things like project augmented reality things
- Not robust to camera moving, rotating, etc.