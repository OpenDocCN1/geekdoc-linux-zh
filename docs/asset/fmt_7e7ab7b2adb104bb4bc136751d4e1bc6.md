
支持多架构的包安装器可以用于在你的桌面机上安装 RPi `armhf` 库。`dpkg` 的版本必须大于 16。

此时，你已经有了一个交叉编译器，你目前应该能够交叉编译使用标准 C/C++ 库的应用程序。

```
molloid@desktop:~$ apt update
molloid@desktop:~$ apt install libicu-dev
```

Reading lists...

Building dependency tree...

Reading dependency information...

Setting up libicu-dev (0.41-6)

Processing triggers for libc-bin (2.19-18)

现在，可以在 x86 机器上模拟 `armhf` 指令（这会有性能开销），并且测试程序可以在桌面机上执行：

```
molloid@desktop: ~/testpi
Testing the RPi pre-built toolchain
```

# 使用第三方库进行交叉编译 (多架构 Multiarch)

此部分对于交叉编译 C/C++ 应用程序并不是必需的；然而，未来你可能需要添加第三方库来处理图像和数值处理等任务。从传统来说，这是一个非常困难的话题，但归于 Debian 和 Ubuntu 最近的发布，这个问题变得更容易管理了。

此时，你已经有了一个交叉编译器，你目前应该能够交叉编译使用标准 C/C++ 库的应用程序。然而，如果你想构建一个使用包含编译代码第三方库的 C/C++ 应用程序呢？如果你在 x86 机器上安装该库，它将包含原生 x86 代码。如果你想使用该第三方库并部署到你的 RPi，你需要使用包含 ARM 机器指令的库。

传统上，开发者使用诸如 `xapt` 之类的工具，它可以动态将 Debian 包转换为跨平台版本（例如 `xapt -a armhf - libopencv-dev`）。然而，Debian (8+) 的最新版本现在对多架构（multiarch）包安装有强力支持。

支持多架构的包安装器可以用于在你的桌面机上安装 RPi `armhf` 库。`dpkg` 的版本必须大于 16。

此时，你已经有了一个交叉编译器。

```
molloid@desktop:~$ sudo dpkg --add-architecture armhf
```

按照以下方式安装交叉编译工具：

```
mollyd@desktop:$ sudo apt install cross-build-essential-armhf
Setting up libyaml-perl (0.41-6)
Processing triggers for libc-bin (2.19-18)
mollyd@desktop:$ cd /usr/bin
mollyd@desktop~$ ls -l "g*"
lrwxrxrxr 1 root root 27 Jan 16 2015 arm-linux-gnueabih-g++
-> arm-linux-gnueabih-g+-4.9
lrwxrxrxr 1 root root 7 Feb 27 07:13 g++ -> g++-4.9
lrwxrxrxr 1 root root 7 Feb 27 07:13 x86_64-linux-gnue-gnu-g++ -> g++-4.9
```

你可以看到 `/usr/bin` 目录现在包含一个用于原生编译 x86 代码的 `g++` 条目，以及一个用于编译 `armhf` 代码的 `arm-linux-gnueabih-g++` 条目。

可以在任何位置（`/usr/bin` 在默认 `PATH` 中）通过以下命令测试编译器并检查其版本：

```
mollyd@desktop:$$ arm-linux-gnueabih-g++ -v
gcc version 4.9.2 (4.9.2-10)
```

你可以使用 `apt-cache` 代码来测试此工具链，你应该获得相同的结果。你可以在桌面机上安装两个工具链。由于 `/usr/bin` 条目出现在 `PATH` 环境变量中，交叉工具链将具有优先级。

> 注意：使用 `apt-cache` 搜索替代编译器版本。带有 Raspberry 发行行的 Pi 支持硬浮点 `hf`，因此在可用时使用带有 `hf` 后缀的工具：

```
mollyd@desktop:$$ apt-cache search gnueabih | grep g++
g++4.9-arm-linux-gnueabih GNU C++ compiler
g++-arm-linux-gnueabih - GNU C++ cross-compiler for architecture armhf
```
