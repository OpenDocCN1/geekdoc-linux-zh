# 3.3 BILINEAR INTERPOLATION

```
$A'_i = \begin{bmatrix} 1/cos\theta & -tan\theta \ 0 & 1 & 0 \ tan\theta & 0 & 1/cos\theta \end{bmatrix}\nA'_j = \begin{bmatrix} cos\theta & -sin\theta & 0 \ \sin\theta & cos\theta & 0 \ 0 & 0 & 1 \end{bmatrix}$
```

When performing the inverse transformation, many of the pixels in the transformed image will correspond to fractional locations in the source image. Since our source image is discretely “sampled” at integral pixel positions, the program must use a technique for calculating the pixel colors of locations between pixels. There are various methods for doing this type of interpolation, but begin by using the simplest method, bilinear interpolation.

When an inverse transformation maps one of the destination image pixels to fractional source pixel, the program must estimate the color of this “virtual” value based on the sampled pixels around it. The basic idea of bilinear interpolation is that a fractional coordinate within a 2D space will be positioned somewhere inside of 2x2 pixel block. The interpolated pixel can be calculated using a weighted average of these four pixels, where the weights of each of the four pixels are calculated as a function of the fractional portion of the location in both dimensions.

Figure 3.1 depicts this situation, assuming the inverse transformation give us $(i,j)$ and $i_{int} = i$, $i_{rac} = i - int$ and $j_{int} = j$, $j_{rac} = j - j$.

The weights were calculated as:

```
$weight(i_{int}, j_{int}) = (1 - i_{rac}) \cdot (1 - j_{rac})$
weight(i_{int}+1, j_{int}) = (1 - i_{rac}) \cdot j_{rac}$
weight(i_{int}, j_{int}+1) = i_{rac} \cdot (1 - j_{rac})$nweight(i_{int}+1, j_{int}+1) = i_{rac} \cdot j_{rac}$
```

# 3.4 FLOATING-POINT IMAGE TRANSFORMATION

The image transformation and interpolation calculations must be performed using fractional values and floating point may seem like an obvious choice. One problem using floating point is that each transformed pixel will begin and end as a pixel location and color value, both of which are integers. This will require typecasting between integers and floats for the