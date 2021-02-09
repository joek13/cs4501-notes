---
title: "02. Projective Geometry & Light"
date: 2021-02-09T12:32:05-05:00
draft: false
---

### Review: cameras
Cameras are cool devices, and they've been around for longer than you might think.

### Shooting photos in manual
- Shutter time (time the shutter is open)
- Aperture (size of opening)
- ISO
- Focus / auto-focus

If you shoot in automatic, these variables are determined for you

### Shutter speed
- Long shutter speed lets more light in, but it causes blurring over time
- Long-exposure shots require a completely stable camera

### Aperture
- Aperture size impacts depth of field
- Large aperture = background blurred
- Small aperture = background fine

### ISO - light sensitivity
- Make as small as possible
- Overly high ISO results in lots of noise in the image

### Trade offs
- Small aperture: more focus, less light
- Small shutter time: capture fast moving item, less light
- Small ISO: less noisy, less light

### Difficult pictures
- Small object in foreground (large aperture required)
- Fast-moving object (low shutter time required)
- Dark object (high ISO required)

### Final thoughts - with a grain of salt
- Shooting in automatic, especially in low-light conditions, will often go the easy route of jacking up the ISO
- In low light, you might want to increase shutter time or enlarge your aperture
- No shame in shooting automatic in a clear day

## Projection: world coordinates \\(\to\\) image coordinates
You have an image, which is just a 2D matrix of intensity values. How can we reason about a three-dimensional world?

But we also care about the opposite process: projecting world coordinates into a 2-dimensional coordinate space.

Definition of camera coordinates:
$$
    \mathbf{p} = \langle U, V \rangle
$$
Definition of world coordinates:
$$
    \mathbf{P} = \langle X, Y, Z \rangle
$$

With focal length \\(f\\) (distance from camera to image plane):

$$
    U = -X * \frac{f}{Z}
$$
$$
    U = -Y * \frac{f}{Z}
$$

### Homogeneous coordinates
#### Conversion
Converting to homogeneous coordinates
$$
    (x, y) \mapsto \langle x, y, 1 \rangle
$$

$$
    (x, y, z) \mapsto \langle x, y, z, 1 \rangle
$$

Converting from homogeneous coordinates
$$
    \langle x, y, w \rangle \mapsto (x/w, y/w)
$$

Converting to homogeneous coordinates
$$
    \langle x,y,z,w \rangle \mapsto (x/w, y/w, z/w)
$$

### Desirable features of homogeneous coordinates
- Scale-invariant

### Projection matrix

$$
    x = K[R \space \space t]X
$$
- \\(x\\), image coordinates (u, v, 1)
- \\(K\\), intrinsic matrix (3x3)
- \\(R\\), rotation (3x3)
- \\(t\\), translation (3x1)
- \\(X\\), world coordinates (X,Y,Z, 1)

Intrinsic assumptions
- Unit aspect ratio (could change this by setting different focal lengths for x and y, \\(f_x, f_y\\))
- Optical center at origin
- No skew

Extrinsic assumptions
- No rotation
- Camera at (0,0,0)

### Remove assumption of optical center at (0,0)