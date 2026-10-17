
```bash
make check
```

安装软件包：

```bash
make install
```

### 8.49.2. Libffi 的内容

已安装库：`libffi`

# 简述

- `libffi` 此库被其他程序用于加载和卸载内核模块

## 8.50. Python 3.11

Python 是一种高级、解释型编程语言。其设计哲学通过显著的缩进强调了代码的可读性。

预计编译时间：2.0 SBU

所需的磁盘空间：372 MB

### 8.50.1. 安装 Python

Python 是 `python-3.11` 包的一部分。使用 `python-3.11.tar.bz2` 文件作为源压缩包。

为编译 Python 准备工作：

```
./configure --prefix=/usr
    --enable-shared
    --enable-optimizations
```

编译软件包：

```
make
```

要测试结果，请执行：

```
make check
```

安装软件包：

```
make install
```

### 8.50.2. Python 3 的内容

已安装库：`libpython3.11.so`

已安装目录：`/usr/include/python3.11`, `/usr/lib/python3`

`python3` 是 Python 的解释器，Python 是一种解释型、交互式面向对象的编程语言

## 51. Wheel-0.38.4

Wheel 是一个 Python 库，它是 Python wheel 打包标准的参考实现。

近似构建时间：少于 0.1 SBU

需要的磁盘空间：1.3 MB

## 85.1.1. Wheel 的安装

使用以下命令编译 Wheel：

```bash
PYTHONPATH=src pip3 wheel -w dist --no-build-isolation --no-deps $PWD
```

使用以下命令安装 Wheel：

```bash
pip3 install --no-index --find-links=dist wheel
```

`pip3` 配置选项和命令的含义：

```
PYTHONPATH=src
```

允许此包（尚未安装）为自己构建一个 wheel 存档，以避免“先有鸡还是有蛋”的问题。

`wheel`

```
-w dist
```

此命令为此包构建 wheel 存档。指示 `pip` 将创建的 wheel 放入 `dist` 目录中。

`install`

此命令安装包。

```
--no-build-isolation, --no-deps, and --no-index
```

这些选项防止从在线包仓库 (PyPI) 获取文件。如果按照正确的顺序安装包，`pip` 根本不需要获取任何文件；这些选项在用户发生错误时增加了一些安全性。

```
--find-links dist
```

指示 `pip` 在 `dist` 目录中搜索 wheel 存档。

## 85.2. Wheel 的内容

- 安装的程序：

安装的目录：

- `wheel`

`/usr/lib/python3.11/site-packages/wheel` 和 `/usr/lib/python3.11/site-packages/wheel-0.38.4.dist-info`

## 简要描述

`wheel` 是一个用于解包、打包或转换 wheel 存档的工具

## 8.52. Ninja-1.111

Ninja 是一个专注于速度的小构建系统。

近似构建时间：0.3 SBU

需要的磁盘空间：77 MB

> 提示：当 LFS 不使用 systemd 时，此部分并非必须。另一方面，Ninja 与 Mason 构成了一个强大的构建系统组合，这种组合可能会被越来越频繁地。BLFS 书中的几个包需要它。

## 8.52.1. Ninja 的安装

运行时，`ninja` 通常会利用尽可能多的并行进程。默认情况下，这是系统的内核数加 2。这可能会导致 CPU 过热，或使系统内存耗尽。当从命令行调用 `ninja` 时，传递 `-j` 参数将限制并行进程的数量。某些包嵌入了 `ninja` 的执行，且没有向其传递 `-j` 参数。

使用下方的*可选*程序可以通过环境变量 `NINJAJOBS` 限制并行进程的数量。**例如**，设置：

```bash
export NINJAJOBS=4
```

将 `ninja` 限制为四个并行进程。

如果需要，`ninja` 会通过运行流编辑器来识别环境变量 `NINJAJOBS`：

```bash
sed -i '' /int Guess/a \
int j = 0;\nchar* jobs = getenv("NINJAJOBS");\nif (jobs != NULL) j = atoi(jobs);\nif (j > 0) return j;\n	 src/ninja.cc
```

使用以下命令构建 Ninja：

```bash
python3 configure.py --bootstrap
```

构建选项的含义：

`--bootstrap`

此参数强制 Ninja 为当前系统重新构建自己。

要测试结果，请执行：

```bash
/.ninja ninja_test
./ninja_test --gtest_filter=SubprocessTest.SetWithLots
```

安装包：

```bash
install -vm755 ninja /usr/bin/
install -Vdm644 misc/bash-completion /usr/share/share/bash-completion/completions/ninja
install -Vdm644 misc/zsh-completion /usr/share/zsh/site-functions/_ninja
```

## 8.52.2. Ninja 的内容

- 安装的程序：`ninja`

## 简要描述

`ninja` 是 Ninja 构建系统

## 8.53. Meson-1.0.0

Meson 是一个开源构建系统，旨在既极快又尽可能对用户友好。

**近似构建时间：**少于 0.1 SBU

**需要的磁盘空间：**41 MB

> 提示：当 LFS 不使用 systemd 时，此部分并非必须。另一方面，Meson 与 Ninja 构成了一个强大的构建系统组合，这种组合可能会被越来越频繁地。BLFS 书中的几个包需要它。

## 8.53.1. Meson 的安装

使用以下命令编译 Meson：

```bash
pip3 wheel -w dist --no-build-isolation --no-deps $PWD
```

测试套件需要 LFS 范围之外的一些包。

安装包：

```bash
pip3 install --no-index --find-links dist meson
install -VM664 data/shell-completions/bash/meson /usr/share/bash-completion/completions/meson
install -VM664 data/shell-completions/zsh/_meson /usr/share/zsh/site-functions/_meson
```

安装参数的含义：

- `-w dist`

将创建的 wheels 放入 `dist` 目录。

`--find-links dist`

从 `dist` 目录查找包。

## 8.53.2. Meson 的内容

- 安装的程序：`meson`

- 安装的目录：`usr/lib/python3.11/site-packages/meson-1.0.0.dist-info`

## 简要描述

`meson` 是一个构建系统

## 8.54. Coreutils-9.1

Coreutils 包含了满足 POSIX 系统的基本工具。

**近似构建时间：**0.9 SBU

需要的磁盘空间：156 MB

## 8.54.1. Coreutils 的安装

使用以下命令编译 Coreutils：

```bash
./configure --prefix
```

配置选项的含义：

`--prefix`

此参数指定安装的根目录。

要测试结果，执行：

```bash
make test
```

构建包：

```bash
make
```

如果需要，运行以下命令安装包：

```bash
make install_test
```

安装包：

```bash
make install
```

## 85.2. Coreutils 的内容

安装的程序：
