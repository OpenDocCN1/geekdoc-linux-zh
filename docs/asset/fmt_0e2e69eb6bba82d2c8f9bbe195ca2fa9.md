
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

```python
import numpy as np

help(ndimage.correlate1d, ndimage.ndimage.convolve, ndimage.convolve1d, ndimage.correlate, ndimage.correlate1d)

# numpy.core.ndimage
# ... [help text omitted for brevity] ... #
# correlate1d(input, weight, axis=0, output=None, mode='reflect', cval=0.0, origin=0)
#    ... [help text omitted for brevity] ... #
```

# 查找帮助很容易

## 使用 NumPy 进行科学计算

### 利用 NumPy、SciPy 和 Matplotlib 进行强大运算

## 资源

- **NumPy**: www.numpy.org
- **SciPy**: www.scipy.org
- **Matplotlib**: www.matplotlib.org

NumPy 是用于执行科学计算的主要 Python 包。它拥有强大的 N 维数组对象，以及用于集成 C/C++ 和 Fortran 代码的工具，还包括线性代数、傅里叶变换和随机数生成能力等。NumPy 还支持广播机制，这是一种巧妙的方法，使通用函数能够以有意义的方式处理形状不完全相同的输入。

除了其功能强大之外，NumPy 的另一个优势在于它可以集成到 Python 程序中。换句话说，你可以从数据库、其他程序的输出、外部文件或 HTML 页面获取数据，然后使用 NumPy 进行处理。

本文将向你展示如何安装 NumPy、执行计算、绘制图表、读写外部文件，并介绍一些与 NumPy 配合良好的 Matplotlib 和 SciPy 软件包。

NumPy 还可以与 Pygame（一个用于创建游戏的 Python 包）配合使用，尽管解释其用法超出了本文的范围。在将各种 NumPy 命令放入 Python 程序之前，先是在 Python shell 中尝试这些命令，被认为是一种良好的实践。本文中的示例使用的是 Python shell 或 iPython。

## 01 安装 NumPy

大多数 Linux 发行版都有现成的安装包可供使用。安装完成后，你可以通过执行以下命令来查看你正在使用的 NumPy 版本：

```
$ python
Python 2.7.3 (default, Mar 13 2014, 11:03:55)
[GCC 4.4.7] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>> numpy.version.version
```

```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'numpy' is not defined
>>> import numpy
>>> numpy.version.version
'1.6.2'
>>>
```

你不仅找到了 NumPy 的版本，还知道了 NumPy 已成功安装。

## 02 关于 NumPy

尽管名字很简单，但 NumPy 是一个强大的 Python 包，主要用于处理数组和矩阵。创建数组的方法有很多种，但最简单的是使用 `array()` 函数：

```
>>> oneD = array([1,2,3,4])
```

上述命令创建了一个一维数组。如果你想创建一个二维数组，可以如下使用 `array()` 函数：

```
>>> twoD = array([ [1,2,3],
          [3,3,3],
...      [-1,-0.5,-1],
...      [0,1,0] ] )
```

你还可以创建维度更多的数组。

## 03 使用 NumPy 进行简单计算

给定一个名为 `myArray` 的数组，你可以通过执行以下命令来查找其中的最小值和最大值：

```
>>> myArray.min()
>>> myArray.max()
```

如果你想查找所有数组元素的平均值，请运行下一个命令：

```
>>> myArray.mean()
```

同样，你可以通过运行以下命令来查找数组的中位数：

```
>>> median(myArray)
```

一组数据的中位数是一个将该数据集分成两个子集（左子集和右子集）且元素数量相同的元素。如果数据集的元素数量是奇数，则中位数是数据集的一部分。另一方面，如果数据集的元素数量是偶数，则中位数是排序后数据集中间两个元素的平均值。

![](img/e016e192a91ffc1a9e474690a590742f_80_0.png)

## 04 使用 NumPy 处理数组

NumPy 不仅采用了典型 Python 字符串和列表中的索引方法，还对其进行了扩展。如果你想从数组中选择特定元素，可以使用以下表示法：

```
>>> twoD[0,2]
```

你还可以使用以下表示法选择数组的一部分（切片）：

```
>>> twoD[:1,1:3]
```

最后，你可以使用 `tolist()` 函数将数组转换为 Python 列表。

## 05 读取文件

想象一下，你刚刚使用 AWK 从 Awk 文件日志中提取了信息，并希望使用 NumPy 处理该文本文件。以下 AWK 代码用于找出每小时的总请求数：

```
$ cat access.log | cut -d'|' -f2 | cut -d'|' -f1 | awk -F: '{print $2}' | sort -n | uniq -c | awk '{print $2, $1}' > timeN.txt
```

包含数据的文本文件（`timeN.txt`）的格式如下：

| 小时 | 请求数 |
| :--- | :------- |
| 00   | 191      |
| 01   | 225      |
| 02   | 121      |
| 03   | 104      |

读取 `timeN.txt` 文件并将其赋值给一个新的数组变量可以按如下方式进行：

```
aa = np.loadtxt("timeN.txt")
```

## 06 写入文件

将变量写入文件的过程与读取文件大致相似。如果你有一个名为 `aa` 的数组变量，你可以使用以下命令轻松地将内容保存到一个名为 `aaL.txt` 的文件中：

```
In [17]: np.savetxt("aaL.txt", aa)
```

你可以很容易地想到，之后可以使用 `loadtxt()` 函数读取 `aaL.txt` 的内容。

## 07 常见函数

NumPy 支持许多数值和统计函数。当你对数组应用函数时，该函数会自动应用于所有数组元素。

在处理矩阵时，你可以通过输入 `AA.I` 来找到矩阵 `AA` 的逆矩阵。你还可以通过输入 `np.linalg.eigvals(AA)` 找到其特征值，通过输入 `np.linalg.eig(GB)` 找到其特征向量。

## 08 处理矩阵

NumPy 二维数组的一个特殊子类型是矩阵。矩阵类似于数组，不同之处在于矩阵乘法取代了逐元素乘法。矩阵使用 `matrix`（或 `mat`）函数生成，如下所示：

```
In [2]: AA = np.mat('0 1; 1 1; 1 1 1')
```

你可以通过输入 `AA + BB` 来添加两个名为 `AA` 和 `BB` 的矩阵。同样，你可以通过输入 `AA * BB` 来乘以它们。

## 使用 Python
