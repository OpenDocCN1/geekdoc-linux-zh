# 4.3 Separable Filters 157

Despite the ready availability of the pixel values $I()$, the Harris detector is normally evaluated as the first-order Taylor expansion of the above expression:

$$E(u, v) = \sum_{x,y} [I(x+u, y+v) - I(x, y)]^2$

$$= \sum_{x,y} [(I(x,y) + I_x(x,y) + I_y(x,y)) - I(x,y)]^2$

where $I_x$ and $I_y$ are the partial derivatives of $I$ with respect to $x$ and $y$.

$$= \sum_{x,y} [I_x^2(x,y) + 2uvI_x(x,y)I_y(x,y) + v^2I_y^2(x,y)]^2$

$$= [u \ v] \left( \begin{matrix} I_x^2(x,y) & I_x(x,y)I_y(x,y) \ I_x(x,y)I_y(x,y) & I_y^2(x,y) \end{matrix} \right) [u \ v]$

The matrix $M = \begin{bmatrix} I_x^2(x,y) & I_x(x,y)I_y(x,y) \ I_x(x,y)I_y(x,y) & I_y^2(x,y) \end{bmatrix}$ measures the patch's center pixel’s “corner response” $R$, as

$$R = \det(M) - k(trace(M))$

where

$$trace \left( \begin{matrix} a & b \ c & d \end{matrix} \right) = ad-bc$

and

and $k$ is parameter, typically set to $k=0.04$.

$R$ is subjected to a threshold; where any value over a threshold is considered a corner.

Figure 4.8 shows the corners (shown in white) for the Lena image for different threshold values for a patch size of $5 \times 5$. These images are generated using the following steps:

+   1. Apply $7 \times 7$ separated Gaussian filter

+   2. Compute $I_x$ and $I_y$ using Sobel filter

+   3. Apply $5 \times 5$ Harris corner detector, which performs:

+   a. Compute products of derivatives at each pixel $(I_x^2, I_xI_y, I_y^2)$

+   b. Compute the response at each pixel