# 3.2 Affine Image Transformations 109

Assume the location of pixel, represented as a row and column value, is stored as a column vector $c$. A linear image transformation can be described as a $2 \times 2$ matrix $A$, and can be applied to this pixel by multiplication; $c' = A \cdot c$ is a column vector that represents the position of the pixel in the transformed image.

In an *affine transformation*, the matrix $A$ is a $3 \times 3$ matrix and there must be an additional element added to the pixel location vector.

For example, the three following affine matrices allow an image to be rotated clockwise by angle $\theta$ about the $X, Y$, and $Z$ dimensions:

```
$A_x = \begin{bmatrix} 1 & 0 & 0 \ 0 & \cos\theta & -sin\theta \ 0 & \sin\theta & \cos\theta \end{bmatrix}$
```

```
$A_y = \begin{bmatrix} \cos\theta & 0 & \sin\theta \ 0 & 1 & 0 \ -sin\theta & 0 & \cos\theta \end{bmatrix}$
```

```
$A_z = \begin{bmatrix} \cos\theta & \sin\theta & 0 \ -sin\theta & \cos\theta & 0 \ 0 & 0 & 1 \end{bmatrix}$
```

The effect of affine transformations can be combined by multiplying multiple transformation matrices. For example, the program can rotate an image about the $X, Y$, and $Z$ axes simultaneously by multiplying these three matrices together, is, $A_{XYZ} = A_x \cdot A_y \cdot A_z$.

An obvious way to transform an entire image is to iterate over all the pixels in the source image, calculate their new positions in the transformed image, and copy the pixel to its new location. However there is a problem with this approach. The transformed pixel locations will contain fractional values, making it unclear to copy the pixels to their new positions.

Instead, the program can iterate over all the pixels in the destination image and calculate the inverse transformation to determine each pixel's corresponding location in the source image, using the inverse transformations below. This will give integral pixel locations for our destination image and fractional pixel locations for our source image. The program can use interpolation to calculate the estimated value of fractional source image pixel locations.

```
$A'_x = \begin{bmatrix} 1 & 0 & 0 \ 0 & 1/\cos\theta & \tan\theta \ 0 & \tan\theta & -1/\cos\theta \end{bmatrix}$
```