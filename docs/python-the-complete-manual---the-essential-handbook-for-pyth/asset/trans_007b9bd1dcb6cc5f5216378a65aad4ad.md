

## 用 Python 替换你的 shell

## 使用 Python 工作

```
%page %paste %pastebin %pdf %pdoc %pfile
%info %pinfo2 %popd %pprint %precision %profile %prun
%search %psource %pushd %pwd %pycat %pylab %quickref
%recall %rehash %reload_ext %rper %rerun %reset
%reset_selective %reselect %save %xsc %xsb %thb %timeout
%unalias %unload_ext %who %who_is %whos %xdel %mode
```

Autmagic 已关闭，魔法函数需要 `%paste`。要查看任何魔法函数的的帮助，请调用 `%magic?`。运行时代码编辑：你可以使用 `%run` 运行任何 Python 脚本。你也可以使用 control-run 配合 pdb 调试器 -d 运行 Python 脚本，或使用 pdb 性能分析 -p。你还可以使用 `%edit` 命令编辑 Python 脚本，该命令会在 `EDITOR` 环境变量定义的编辑器中打开指定的 Python 脚本。

**支持 Shell 命令：** 要运行 shell 命令，请在命令前加 `!`

示例：
[5]: !ps

| PID TTY | TIME | CMD |
| --- | --- | --- |
| 4508 tty000 | 00:00.07 | -bash |
| 84275 tty001 | 00:00.03 | -bash |
| 17958 tty002 | 00:00.18 | -bash |

[8]: !clang prog.c -o prog
prog.c:21:2: warning: type specifier missing, defaults to 'int' [-Wimplicit-int]

已生成。

Qt 控制台：IPython 自带基于 Qt 的控制台。它提供了只有 GUI 才能的功能，如内联函数、使用语法高亮的多行编辑以及图形功能。通过以下命令启动 Qt：

```
$ ipython qtconsole
```

## 结论

如你所示，很容易为你的 shell 环境需求定制 Python。os、subprocess 和 shift 等 Python 模块可供你使用，利用 Python 完成你所需的一切工作。IPython 将这种体验变成了一个更完整的包。为了执行标准 Python shell 能执行的操作并带有更方便的功能，Python 的魔法函数确实提升了你的 shell 体验。下次当你打开 Bash 会话时，再考虑一下，既然铂金触手可及，何满足于黄金？

如果你遇到关于缺少模块的错误，请确保已安装相关依赖包 -PyQt、pygments、pyx 和 ZeroMQ。

![](img/c72194f2c3aec198936695a665a5167c_56_0.png)

## 使用 NumPy 进行科学计算

### 你将需要...

- NumPy
www.numpy.org

- SciPy
www.scipy.org

- Matplotlib
www.matplotlib.org

## 使用 NumPy 进行科学计算

使用 NumPy、SciPy 和 Matplotlib 进行强大的计算

NumPy 是执行科学计算的主要 Python 软件包。它拥有强大的多维数组对象、用于集成 C/C++ 和 Fortran 代码的工具、线性代数、傅里叶变换以及随机数功能等。NumPy 还支持广播机制（broadcasting），这是通用函数以有意义的方式处理形式不完全相同的输入的一种巧妙方法。

除了功能外，NumPy 的另一个优势是它可以集成到 Python 程序中。换句话说，你可以从数据库、另一个程序的输出、外部文件或 HTML 页面获取数据，然后使用 NumPy 进行处理。

本文将向你展示如何安装 NumPy、进行计算、绘制数据、读写外部文件，并向你介绍一些与 NumPy 配合良好的 Matplotlib 和 SciPy 包。

NumPy 还可以与 Pygame（一个用于创建游戏的 Python 包）一起工作，尽管遗憾解释其用法超出了本文的范围。

在将命令放入 Python 程序之前，在 Python shell 中尝试各种 NumPy 命令被认为是良好的做法。本文示例使用了 Python shell 或 IPython。

## 使用 NumPy 进行科学计算 与 Python 工作

一个简单的多项式拟合 Python 程序！

```
import numpy as np
x = np.array([0, 1, 2, 3, 4])
y = np.array([1, 2, 4, 8, 16])
pp = np.polyfit(x, y, 2)
pf = np.poly1d(pp)
print(pf)
```
![](img/c72194f2c3aec198936695a665a5167c_58_0.png)

Matplotlib 生成输出 使用 SciPy 处理图像的 Python 脚本

```
import numpy as np
from scipy import ndimage
import matplotlib.pyplot as plt
image = plt.imread('image.png')
image_filtered = ndimage.gaussian_filter(image, sigma=3)
plt.imshow(image_filtered)
```
![](img/c72194f2c3aec198936695a665a5167c_1.png)

查找帮助很容易

## 安装 NumPy

大多数 Linux 发行版都提供了可以安装的包。安装后，你可以通过以下命令查看 NumPy 版本：

- * $ python
Python 2.7 (default, Mar 13 20:55) on GCC 4.7
输入 "help", "license" 获取更多信息：
* >> numpy.version
Traceback (most recent call last):
File "<stdin>", line 1, in <module>
NameError: name 'numpy' not defined
* >> import numpy
* >> numpy.version
>> '1.6'

你不仅找到了 NumPy 版本，还知道 NumPy 已正确安装。

## 使用 NumPy 进行简单计算

关于 NumPy，尽管名字简单，NumPy 是一个主要用于数组和矩阵的强大包。创建数组的许多方法是使用 array 函数。给定一个名为 myArray 的数组，你可以执行以下命令找到其中的最小值和最大值：

- * >> myArray = np.array([1,2,3,4])
- * >> myArray.min()
- * >> myArray.max()

如果你创建一个二维数组，可以使用 array 函数：

- * >> twoD = np.array([[1,2,3,4],[5,6,7,8]])

如果你想找到所有数组元素的平均值，可以运行下一个命令：

- * >> myArray.mean()
array([1,2,3,4])

同样，你可以找到元素的位数，位数是将数据集分成具有相同数量元素的子集（左侧和右侧）。如果数据集元素个数为奇数，位数就是数据的中间部分。另一方面，如果元素个数为偶数，位数就是排序数据集两个中间元素的平均值。

## NumPy 数组

NumPy 数组采用了 Python 用于字符串和列表的索引方法，但对其进行了扩展。如果你想从数组中选择一个元素，使用以下符号：

- * >> arr[0,1]

你也可以使用以下符号选择数组的切片（切片）：

- * >> arr[1:1:3]

最后，你可以使用 tolist() 函数将数组转换为 Python 列表。

img/c72194f2c3aec198936695a665a5167c_59_1.png)

## 读取文件

假设你刚刚使用 NumPy 从 Apache 日志收集了信息，现在你想使用 NumPy 处理文件。以下 AWK 代码找出每个时间点的请求总数：

```
$ cat access.log | cut -d ' ' -f2 | cut -d ' ' -f1 | awk '{print $2}' | sort | uniq -c | awk '{print $2, $1}' > time.txt
```

数据文件 (time.txt) 的格式如下：

```
00 191
01 225
02 121
03 104
```

读取 time.txt 文件并将其赋值给新变量可以这样操作：

```
aa = np.loadtxt("time.txt")
```

## 写入文件

将变量写入文件与读取文件非常相似。如果你有一个名为 aa 的数组变量，可以使用以下命令轻松将内容保存到文件 aa.txt：

- * In [17]: np.savetxt("aa.txt", aa)

随后你可以使用 loadtxt() 函数轻松读取 aa.txt 的内容。

## 常用函数

NumPy 执行了许多数值和统计函数。当你将函数应用到数组时，该函数将自动应用到所有数组元素：

在处理矩阵时，可以通过输入 "A.inv()" 找到 A 的逆。你还可以使用 "np.linalg.eigvals(A)" 找到特征值，使用 "np.linalg.eig()" 找到特征向量。

## 矩阵操作

二维 NumPy 数组的一个特殊子集是矩阵。矩阵类似于数组，矩阵乘法取代了逐逐元素的乘法。使用 matrix（或 mat）函数生成矩阵如下：

- * In [2]: aa = np.mat("0 1 1
1 1; 1 1")

