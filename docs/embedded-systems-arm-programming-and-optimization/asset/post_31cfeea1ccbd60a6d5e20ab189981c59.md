
# Memory optimization and video processing

+ CHAPTER OUTLINE
4.1 Stencil Loops 148
4.2 Example Stencil: The Mean Filter 149
4.3 Separable Filters 150
4.3.1 Gaussian Blur 151
4.3.2 The Sobel Filter 153
4.3.3 The Harris Corner Detector 156
4.3.4 Lucas-Kanade Optical Flow 158
4.4 Memory Access Behavior of 2D Filters 160
4.4.1 2D Data Representation 161
4.4.2 Filtering Along the Row 162
4.4.3 Filtering Along the Column 163
4.5 Loop Tuning 164
4.6 Tiling and the Stencil Halo Region 167
4.7 Example 2D Filter Implementation 167
4.8 Capturing and Rendering Video Frames 172
4.8.1 YUV and Chroma Subsampling 172
4.8.2 Exporting Tiles to the Frame Buffer 174
4.9 VideoLinux Driver and API 176
4.10 Applying the 2D Tiled Filter 181
4.11 Applying the Separated 2D Tiled Filter 182
4.12 Top-Level Loop 182
4.13 Performance Results 183
4.14 Chapter Wrap-up 184
Exercises 184

The optimization objective in the previous chapter was to reduce the average number of cycles per instruction (CPI) by replacing higher latency instructions with lower latency instructions, specifically by replacing floating-point operations with fixed-point operations. Chapter 3 also covered the

Stencils, on the other hand, compute each output element as a function of input array elements whose locations are defined relative to the coordinate of the output element. The input and output arrays are often two-dimensional (2D) or three-dimensional (3D), so for example the kernel

## 4.2 Example Stencil: The Mean Filter

may compute output element (x,y) as a function of the input elements above, below, to the left, and to the right, that is, (x,y-1), (x,y+1), (x-1,y), (x+1, y), any pattern is possible.

Stencil loops are common in scientific and image processing code. They are often embedded deeply in nested loops, as when a stencil loop is applied iteratively (multiple times) to each frame of a video stream. As such, the stencil loop is generally the most expensive component of any application that requires it, so stencil loops are often a target for optimization.

Luckily, stencil loops have two properties that allow for optimization. The first is their data-level parallelism. In cases where the input and output array are separate, each output element may be computed independently of the other output elements. This makes these stencil loops “embarrassingly parallel,” meaning that concurrent processors and/or functional units can compute output elements with little synchronization overhead. In other cases, the input and output arrays reside in the same memory pool, which creates dependencies between output elements. In this case, the stencil is still parallelizable but the code must constrain the order in which output are computed.

The second property is their data reuse. Input elements referenced by one output overlap with elements referenced by other outputs. This way, stencils may reuse input data through the processor’s cache. However, stencil patterns are often complex in the sense that they span multiple dimensions, and can lead to conflict misses in the cache. This is especially problematic when there is a long delay between the first and second time the loop references a particular input element, which is especially challenging for larger input spaces and/or stencil stencils.

## 4.2 EXAMPLE STENCIL: THE MEAN FILTER

A mean filter is an example of a simple stencil. A mean filter calculates the average value among a set of inputs arranged on a 2D grid.

Figure 4.1 depicts the relationship between the input and output arrays for a 3 × 3 mean filter in which the input array is shown on the left and the output array is on the right. The elements of the first rows and four columns of each array are labeled with letters through P.

In the 3 × 3 mean filter, each location of the output array is computed as the arithmetic mean of the 3 × 3 neighborhood of input elements centered on the corresponding location in the input array. For example, output K will reference input elements F, G, H, J, K, L, N, O, and P.

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_153_0.png)

FIGURE 4.1 $3 \times 3$ mean filter.

Locations close to the boundary of the output array would reference locations outside the bounds of the input array. For example, output element A references only input elements A, B, E, and F.

Stencil loops often exhibit a high level of data reuse, where the same input element can be used multiple times when computing output elements. As such, stencil loops have a high arithmetic intensity but their performance depends on the ability of the memory system to take advantage of the locality of data access, since otherwise the stencil may access off-chip memory through cache misses more than necessary.

## 4.3 SEPARABLE FILTERS

Stencil loops are often used to implement Finite Impulse Response (FIR) filters, which are comprised of a set of coefficients. The filtering operation computes each output element by multiplying each coefficient against a set of input elements and sums. In the 2D case, if the coefficients are stored in an $(n \times n)$ matrix $G$ and the input image is stored in $I$, then the output value $O_{r,c}$ is computed

```
$O_{r,c} = \sum_{i=1}^{n} \sum_{j=1}^{n} G_{i,j} I_{|r-i|,|c-j|} - 1$
```

This requires $n^2$ multiplications and $n$ adds per output ($2n^2$ operations), but there is a simple way to reduce this workload. Any 2D FIR filter whose coefficient matrix can be calculated as the product of a column vector and row vector is **separable**, meaning that it is equivalent to performing a 1D row filter on $I$ to compute intermediate matrix $I2$, followed by a column filter on $I2$ to compute output O. In other words, any 2D FIR filter whose coefficient matrix $G=CR$ can be performed as a series of 1D filters using $C$ and $R$.

```
$O_{r,c} = \sum_{i=1}^{n} \sum_{j=1}^{n} G_{i,j} I_{|r-i|,|c-j|} - 1$
```

Figure 4.2 shows these two passes. The dashed rectangle shows which input elements are used. The shaded coloration shows which output have already been computed.

### 4.3.1 Gaussian blur

Gaussian blur is a weighted mean filter in which the coefficients are normalized samples from a probability density function (PDF).

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_154_0.png)

FIGURE 4.2 Row pass (top) and column pass (bottom) of a $3 \times 3$ filter.

![](img/e6ebc663bbb86c6e7bf9ef22ad136e6f_155_0.png)

FIGURE 4.3 2D Gaussian blur using 7×7 coefficient array applied to "Lena" image. Note the black line that borders the bottom and right edges, which is produced from the filter being multiplied against implicit zeros that exist beyond the boundaries of the image.

As shown in 4.3, applying the Gaussian blur makes images appear out of focus, producing an effect that softens the edges. The amount of blurring depends on the number of coefficients.

Image formats usually store pixel values as integers, whereas the Gaussian PDF is defined over real numbers. Because of this, the image data is typically converted into floating- or fixed-point format when applying the Gaussian blur.

In other words, the Gaussian blur is a *low pass filter* that attenuates high-frequency signals from the image, where the high-frequency signals sharpen the sharply defined edges. The Gaussian blur is a common operation in image editing and many computer vision algorithms.

A 2D Gaussian blur is separable because the 2D Gaussian PDF is equivalent to the product of 1D Gaussian PDFs.

The Gaussian blur is implemented using the following algorithm.

**Row pass:**

```
for i=1 to rows
for j=1 to columns
sum = 0;
for k=1 to n
image_j = j+k-floor(n/2);
if (image_j > 0) && (image_j <= columns)
```
