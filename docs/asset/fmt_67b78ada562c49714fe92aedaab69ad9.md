
代码累加了每个寄存器必需的 8 位部分和。不幸的是，`vaddpd`指令没有在寄存器中累加所有 4 个值。相反，它累加了前 2 个值并将结果留在寄存器的上半部分。有必要使用`vextractf128`指令将这些和移动到寄存器的下半部分以准备相加。当对 1000000 对值进行测试时，AVX 版本花费了 3.9 秒，相当于 20.5 GFLOPS。该代码包含了许多并行执行的指令，这有助于 CPU 执行更多操作。

## 练习

- 编写一个 SSE 函数来计算双精度数组的平均值和标准差。
- 编写一个函数对两个双精度序列进行最小二乘拟合。

# 附录 A

## 安装 ebbe

安装 ebbe 基本上有两种选择：要么安装预编译的二进制包或从源码安装。安装二进制包需要不同的 Linux 发行版，这可能会令人沮丧。另一方面，从源码安装很容易保持更新。

### 安装二进制包

你可以在这里 找到二进制包：https://sourceforge.net/projects/ebbe/Linux。那里会有一些针对几个 Linux 版本的文件。我的电脑运行的是 Ubuntu。要安装，请下载文件并执行它。安装程序看起来不错，每一步都选择默认值即可。OS X 的二进制安装也在这里：https://sourceforge.net/projects/ebbe/os。OS X 的二进制安装是一个 gzip 压缩包。你应该使用：

```
tar xvf ebbe-2.3.4.tgz
```
解压文件。这将创建一个名为 "ebe" 的目录。要安装 ebbe，你需要运行脚本：

```
cd ebbe
bash install
```
这将把 ebbe 安装在 `/usr/local/bin`，但你也可以指定安装目录：

```
bash install
```

### 在 Linux 上从源码安装

在 Linux 上从源码安装并不困难。基本思想是安装编译 ebbe 所需的程序和库，下载源代码并编译。示例是针对 Qt 4，但 ebbe 也兼容 Qt 5。

#### 安装 Ubuntu 需要的包

需要的包（由 Ubuntu 14.04 定义）是 `astyle`、`g++`、`gfortran`、`git`、`qt4-dev-tools` 和 `yasm`。可以在 Ubuntu 下安装：

```
sudo apt-get install astyle g++ gfortran qt4-dev-tools yasm
```
也可以每个包使用单独的命令来安装。许多包依赖于其他包，它们也会与列表包一起下载并安装。在另一个 Linux 版本上，包名可能会不同，内容也可能不同。可能需要安装随 `g++` 安装的 `gdb`。你可以使用 GUI 工具安装这些包，Ubuntu 软件中心不会让任务变得更容易。直接输入 `apt-get` 命令简单得多。

#### 安装 Fedora 需要的包

对于 Fedora，安装包的工具是 `yum`，且需要的包名称不同。使用：

```bash
sudo yum install astyle
sudo yum install gcc-c++
sudo yum install gcc-gfortran
sudo yum install git
sudo yum install qt-devel
sudo yum install qtwebkit-devel
```
我们需要的工具名称在 `/usr/bin` 中都附加了 "qt4"，这样你可以在同一台电脑上拥有 Qt 4 和 Qt 5。最简单的替代方案是将这些工具安装目录放入 `PATH` 变量中。这可以在命令行完成，也可以在主目录下的 `.bash_profile` 文件中完成：

```bash
export PATH=/usr/lib64/qt4/bin:$PATH
```

#### 下载源代码

使用 `git` 程序从 sourceforge 拷贝源代码：

```bash
git clone git://git.code.sf.net/p/ebbe/code ebbe
```
这将创建一个名为 `ebbe` 的目录，包含所有源代码。Git 是一个源码管理系统，使得将来可以从 ebbe 目录使用 `git pull` 更新源代码。它只会下载更改部分。

#### 编译并安装 ebbe

`ebbe` 目录下有一个名为 "`rebuild`" 的 shell 脚本，它执行构建 ebbe 所需的所有命令。你可以通过以下方式调用它：

```bash
cd ebbe
bash rebuild
```
这将编译几十个 C++ 文件。构建 ebbe 后，你需要通过以下操作安装它：

```bash
sudo cp ebbe *.qm /usr/local/bin
```
`*.qm` 文件用于允许为 ebbe 的 GUI 选择不同的语言。你可以选择中文、法语和其他语言。如果你更改了语言，需要退出并重启 ebbe 才能生效。

## 在 OS X 上从源码安装

在 OS X 上构建 ebbe 需要获取 `g++`、`gdb`、`estyle`、`gfortran`、`git`、`yasm` 和 Qt。Xcode 包提供了 `g++` 和 `gdb`。MacPorts 包提供了其余。

### 从 Apple App Store 安装 Xcode

安装 Xcode 是安装 MacPorts 的第一步，详见：https://www.macports.org/install.php。他们建议使用 Apple 开发者网站或 Apple App Store。我建议使用屏幕顶部应用程序菜单下的 App Store 选择进入 App Store 并搜索 Xcode。它是 Apple 的免费下载软件。

接下来，你应该使用 `xcode-select -install` 安装 Xcode 命令行工具。

你很可能会收到一条消息，提示该软件包不存在。你可以忽略该消息。显然，Xcode 现在已经包含了命令行工具。你可以通过在命令行中输入 "`g++`" 和 "`gdb -v`" 来验证这一点。这些就是你需要的工具。

### 安装 MacPorts

如需查看 MacPorts 安装指南，你需要为你的操作系统下载相应的软件包文件。对于我那台运行 Mavericks 的电脑，软件包文件是 `MacPorts-2.3.0-10.9-Mavericks.pkg`。下载完成后，点击该软件包即可安装 MacPorts。

MacPorts 是一个命令行工具，可以让你访问数千个免费程序。要搜索 vim 的版本，请输入：

```
sudo port search gimp |
```
你应该能看到 `gimp` 被列出来，后面跟着第一项可选功能说明。你可以使用以下命令安装 `gimp`：

```
sudo port install gimp
```
这仅作为一个示例，运行 obe 并不需要 `gimp`。

## 安装 ebe 所需的工具

安装 MacPorts 后，你就可以使用 MacPorts 安装构建和运行 ebe 所需的工具

```
sudo port install astyle
sudo port install g95 # 替代 gfortran
sudo port install git
sudo port install qt4-mac
sudo port install yasm
```
如果你不想使用 FORTRAN，则没有必要安装 `g95`；但如果你想使用 FORTRAN，简单的方法是通过以下命令将 `g95` 链接为 `gfortran`：

```
sudo ln -s /opt/local/bin/g95 /opt/local/bin/gfortran
```
安装这些工具后，下载、构建和安装的步骤与 Linux 类似。

### 下载源码

`git` 命令是相同的：
`git clone git://git.code.sf.net/p/qtebe/code ebe`

## 构建并安装 ebe

构建和安装的步骤相同，唯一的区别是建议安装在 `/opt/local/bin` 中。

```
cd ebe
bash rebuild
sudo cp ebe *.qm /opt/local/bin
```
