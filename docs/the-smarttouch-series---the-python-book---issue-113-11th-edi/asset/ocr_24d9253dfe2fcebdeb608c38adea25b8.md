A simple Python program for Polynomial Fitting

```
```python
from matplotlib.pyplot import *
import numpy as np

from matplotlib.pyplot import plot
from matplotlib.pyplot import show
aa1, aa2 = np.loadtxt('coeffs.txt', usecols=(0,1), unpack=True)

def p(x):
    return aa1*x + aa2

plot(aa1, aa2, 'o')
plot(aa1, aa2)
ylabel('Coefficients')
xlabel('m, c')
xlim(-2, 2)
xlim(-3, 0.03)
show()
```
```

Matplotlib
generated output

![](bbox=[0.52, 0.14, 0.76, 0.31])

A Python script
that uses SciPy to
process an image

```
```python
from scipy import ndimage
from PIL import Image
from scipy import Image
import matplotlib.pyplot as plt
import matplotlib.image as mpimg
from PIL import Image

image = plt.imread(mpimg.imread('1A.png'), cmap=plt.cm.gray)

plt.subplot(221)
plt.imshow(image, cmap='gray')
plt.title('Original image')

plt.subplot(222)
filtered = ndimage.median_filter(image, size=(9,9))
plt.imshow(filtered, cmap='gray')
plt.title('Median filter applied')

plt.subplot(223)
blur_image = ndimage.gaussian_filter(image, 10)
plt.imshow(blur_image)
plt.title('Gaussian blur applied')
```
```

```
```python
import numpy as np

help(ndimage.correlate1d, ndimage.ndimage.convolve, ndimage.convolve1d, ndimage.correlate, ndimage.correlate1d)

# numpy.core.ndimage
# ... [help text omitted for brevity] ... #
# correlate1d(input, weight, axis=0, output=None, mode='reflect', cval=0.0, origin=0)
#    ... [help text omitted for brevity] ... #
```
```

Finding help
is easy

# # Scientific computing
## with NumPy

Powerful calculations with
NumPy, SciPy and Matplotlib

# ## Resources

+   *   **NumPy**:
    www.numpy.org
*   **SciPy**:
    www.scipy.org
*   **Matplotlib**:
    www.matplotlib.org

NumPy is the primary Python package for performing scientific computing. It has a powerful N-dimensional array object, tools for integrating C/C++ and Fortran code, linear algebra, Fourier transform, and random number capabilities, among other things. NumPy also supports broadcasting, which is a clever way for universal functions to deal in a meaningful way with inputs that do not have exactly the same form.

Apart from its capabilities, the other advantage of NumPy is that it can be integrated into Python programs. In other words, you may get your data from a database, the output of another program, an external file or an HTML page and then process it using NumPy.

This article will show you how to install NumPy, make calculations, plot data, read and write external files, and it will introduce you to some Matplotlib and SciPy packages that work well with NumPy.

NumPy also works with Pygame, a Python package for creating games, though explaining its use is beyond the scope of this article. It is considered good practice to try the various NumPy commands inside the Python shell before putting them into Python programs. The examples in this article are using either Python shell or iPython.

# 01
## Installing NumPy

Most Linux distributions have a ready-to-install package you can use. After installation, you can find out the NumPy version you are using by executing the following:

```
```python
$ python
Python 2.7.3 (default, Mar 13 2014, 11:03:55)
[GCC 4.4.7] on linux2
Type "help", "copyright", "credits" or
"license" for more information.
>>> numpy.version.version
```
```