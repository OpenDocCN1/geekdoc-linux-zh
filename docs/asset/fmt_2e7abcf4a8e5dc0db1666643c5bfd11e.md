
```
total 368468
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Desktop
drwxr-xr-x 10 kunaldeo staff 340 Jul 26 08:30 Documents
drwxr-xr-x 50 kunaldeo staff 1700 Aug 19 12:50 Downloads
drwxr-xr-x 127 kunaldeo staff 4318 Aug 19 01:43 Dropbox
drwx------@ 42 kunaldeo staff 1428 Aug 12 15:17 Library
drwx------@ 3 kunaldeo staff 102 Jul 3 23:32 Movies
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Music
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Pictures
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Public
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Terminal
drwxr-xr-x 5 kunaldeo staff 170 Aug 19 01:37 Terminal
```

![](img/c72194f2c3aec198936695a665a5167c_53_0.png)

上方具有 GUI 能力的 IPython 控制台截图（标准 `shell_INPUT/OUTPUT/ERROR_HANDLE`）

# 用 Python 替换你的 shell

## 使用 Python 工作

IPython 自带了一组预定义的“魔法”函数，它们可以使用命令行风格的语法。IPython 魔法命令习惯上以 `%` 前缀，但如果开启了 `%automagic`，你就可以在没有 `%` 的情况下调用魔法命令。要查看可用魔法函数的列表，请使用 `%magic`。它们包括与代码一起工作的函数（如 `%run`, `%edit`, `%macro`, `%reall` 等）、影响 shell 的函数（如 `%colors`, `%xmode`, `%autoindent` 等）以及其他函数（如 `%reset`, `%timeit`, `%paste` 等）。IPython 的大多数功能都是通过魔法函数驱动的。

### 补全

标签补全是探索任何对象的极佳方式。它还可以帮助避免拼写错误。

示例：

```python
import os
os.path [Tab]
```

### 对象资源器

你可以在任何对象后添加 `?` 来查看其详细信息。你也可以使用双问号（`??`）来查看相关对象的源代码。

```
%page %paste %pastebin %pdf %pdoc %pfile
%info %pinfo2 %popd %pprint %precision %profile %prun
%search %psource %pushd %pwd %pycat %pylab %quickref
%recall %rehash %reload_ext %rper %rerun %reset
%reset_selective %reselect %save %xsc %xsb %thb %timeout
%unalias %unload_ext %who %who_is %whos %xdel %mode
```

`Autmagic` 已关闭，魔法函数需要 `%paste`。要查看任何魔法函数的的帮助，请调用 `%magic?`。运行时代码编辑：你可以使用 `%run` 运行任何 Python 脚本。你也可以使用 `control-run` 配合 `pdb` 调试器 `-d` 运行 Python 脚本，或使用 `pdb` 性能分析 `-p`。你还可以使用 `%edit` 命令编辑 Python 脚本，该命令会在 `EDITOR` 环境变量定义的编辑器中打开指定的 Python 脚本。

**支持 Shell 命令：** 要运行 shell 命令，请在命令前加 `!`

示例：

[5]: `!ps`

| PID TTY | TIME | CMD |
| --- | --- | --- |
| 4508 tty000 | 00:00.07 | -bash |
| 84275 tty001 | 00:00.03 | -bash |
| 17958 tty002 | 00:00.18 | -bash |

[8]: `!clang prog.c -o prog`

`prog.c:21:2: warning: type specifier missing, defaults to 'int' [-Wimplicit-int]`

已生成。

Qt 控制台：IPython 自带基于 Qt 的控制台。它提供了只有 GUI 才能的功能，如内联函数、使用语法高亮的多行编辑以及图形功能。通过以下命令启动 Qt：

```
$ ipython qtconsole
```

## 结论

如你所示，很容易为你的 shell 环境需求定制 Python。`os`、`subprocess` 和 `shift` 等 Python 模块可供你使用，利用 Python 完成你所需的一切工作。IPython 将这种体验变成了一个更完整的包。为了执行标准 Python shell 能执行的操作并带有更方便的功能，Python 的魔法函数确实提升了你的 shell 体验。下次当你打开 Bash 会话时，再考虑一下，既然铂金触手可及，何满足于黄金？

如果你遇到关于缺少模块的错误，请确保已安装相关依赖包 -`PyQt`、`pygments`、`pyx` 和 `ZeroMQ`。

![](img/c72194f2c3aec198936695a665a5167c_56_0.png)

# 使用 NumPy 进行科学计算

## 你将需要...

- `NumPy`
  www.numpy.org
- `SciPy`
  www.scipy.org
- `Matplotlib`
  www.matplotlib.org

使用 NumPy、SciPy 和 Matplotlib 进行强大的计算

`NumPy` 是执行科学计算的主要 Python 软件包。它拥有强大的多维数组对象、用于集成 C/C++ 和 Fortran 代码的工具、线性代数、傅里叶变换以及随机数功能等。`NumPy` 还支持广播机制（`broadcasting`），这是通用函数以有意义的方式处理形式不完全相同的输入的一种巧妙方法。

除了功能外，`NumPy` 的另一个优势是它可以集成到 Python 程序中。换句话说，你可以从数据库、另一个程序的输出、外部文件或 HTML 页面获取数据，然后使用 `NumPy` 进行处理。

本文将向你展示如何安装 `NumPy`、进行计算、绘制数据、读写外部文件，并向你介绍一些与 `NumPy` 配合良好的 `Matplotlib` 和 `SciPy` 包。

`NumPy` 还可以与 `Pygame`（一个用于创建游戏的 Python 包）一起工作，尽管遗憾解释其用法超出了本文的范围。

在将命令放入 Python 程序之前，在 Python shell 中尝试各种 NumPy 命令被认为是良好的做法。本文示例使用了 Python shell 或 IPython。

## 使用 NumPy 进行科学计算 与 Python 工作

一个简单的多项式拟合 Python 程序！

```python
import numpy as np
x = np.array([0, 1, 2, 3, 4])
y = np.array([1, 2, 4, 8, 16])
pp = np.polyfit(x, y, 2)
pf = np.poly1d(pp)
print(pf)
```

![](img/c72194f2c3aec198936695a665a5167c_58_0.png)

Matplotlib 生成输出 使用 SciPy 处理图像的 Python 脚本

```python
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

- `$ python`

`Python 2.7 (default, Mar 13 20:55) on GCC 4.7`

输入 `"help"`, `"license"` 获取更多信息：

- `>> numpy.version`

`Traceback (most recent call last):`
