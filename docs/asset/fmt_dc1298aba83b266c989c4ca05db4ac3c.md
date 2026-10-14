
```text
Build ALSA plugin: no
Build mikmod plugin: yes
Build Ogg Vorbis plugin: yes
Build OpenGL plugins: no
Pthread flag: -lpthread
Use one plugin dir: no
Allow one plugin dir: yes
```

由于现代 Linux 系统上的大多数音频应用程序在某种程度上使用 ALSA 音系统，这显然是不够的。识别缺失的内容需要检查 `configure` 脚本的输出。使用 `aptitude` 搜索 `asound` 发现了 `libasound2-dev`。安装之后，`configure` 脚本的输出显示：

```bash
$ ./configure
[ 大部分输出删除 ]
config.status: executing depfiles commands

Configuration:
Install path: /usr/local
Build OSS plugin: yes
Build esd plugin: yes
Build Solaris plugin: no
Build BSD Sun plugin: no
Build ALSA plugin: yes
Build mikmod plugin: yes
Build Ogg Vorbis plugin: yes
Build OpenGL plugins: no
Pthread flag: -lpthread
Use one plugin dir: no
Allow one plugin dir: yes
```

# 附章节

要解决这个问题，你必须将 `/usr/local/lib` 添加到系统查找共享库的目录列表中。你可以使用文本编辑器编辑 `/etc/ld.so.conf` 文件，并将目录 `/usr/local/lib` 添加到该文件的末尾。完成后后，你可以执行 `ldconfig` 命令（通过 `sudo`）将你的系统在该目录（及其包含的任何子目录）添加到系统查找共享库的位置列表中。之后你就可以没有任何问题地运行 `/usr/local/bin/xmms` 了。

构建使用非标准位置共享库的软件时，在安装过程中（即 `make` 过程）会显示类似下面的信息：

库已安装在：

`/usr/local/lib`

- 如果你确实链接了给定目录（`LIBDIR`）中的已安装库，你必须使用 `libtool` 并指定库的完整路径名，或者在链接时使用 `-L LIBDIR` 标志，并满足以下任一条件：

    - 在执行期间将 `LIBDIR` 添加到环境变量 `LD_LIBRARY_PATH` 中

    - 在链接期间将 `LIBDIR` 添加到环境变量 `LD_RUN_PATH` 中

    - 使用链接器标志 `-Wl,-rpath,$LIBDIR` 并让你的系统管理员将 `LIBDIR` 添加到 `/etc/ld.so.conf`

查看有关共享库的任何操作系统文档以获取更多信息，例如 `ld(1)` 和 `ld.so(8)` 手册页。

此类识别应用程序定位共享库可能的消息可能是一个潜在问题，但并不直观。

![](img/e3248f698da647444405a34229bd9df5_1279_0.png)

`/etc/ld.so.conf` 文件在你启动系统时会自动被扫描。一旦你向此文件添加了条目，你的系统将始终在那里查找——你不需要再次运行 `ldconfig` 命令。

# 构建附加软件

如前节所述，XMMS 提供了插件架构，使其能够方便地添加其他音频格式的库。如果你使用 SHN (SHN)，它是一种多年来流行的免费无损音频解码器。该解码器的源代码是免费获取的，但 Ubuntu 或 Ubuntu 系统上默认没有支持此音频格式的包。

由于 SHN 相关软件存在于 Ubuntu 仓库中，这为 XMMS 构建 SHN 插件变得非常容易，因为已安装的 SHN 相关软件版本与我们正在构建的内容之间不存在可能性的冲突。下一节将详细介绍如何将 Ubuntu 提供的软件与像 XMMS 这样不支持的包进行构建和集成。

由于不存在可能的冲突，为 XMMS 构建并安装 SHN 解码器的过程如下：

```bash
$ get
```

# 在 Ubuntu 和 Kubuntu 上进行开发

http://etree.org/shnutils/dist/xmms-shn/xmms-shn-2.4.1.tar.gz

[output deleted]

14:44:09 (251.02 KB/s) - `xmms-shn-2.4.1.tar.gz` saved [307397/307397]

```bash
$ tar xvzf xmms-shn-2.4.1.tar.gz
xmms-shn-2.4.1/
[output deleted]

$ cd xmms-shn-2.4.1

$ ./configure
checking build system... i686-pc-linux-gnu
[output deleted]
configure: ready to compile.
```

xmms-shn 现在已根据以下选项配置：

```text
version: 2.4.1
install dir: /usr/local/lib/xmms/Input
```

```bash
$ make install
[sudo] password for whv:
Making install in utils
[output deleted]
make[1]: Leaving directory '/home/wvh/src/xmms-shn-2.4.1'
```

从这个示例可以看出，插件的所有要求已通过 XMMS 本身满足，且只需少量工作即可完成配置、编译和安装。

当 Ubuntu 仓库提供的包还可以提供某些缺失的插件或其他软件时，情况会变得有趣。这将在下一节中讨论。

# 以不同的方式构建支持的软件

我依赖的另一个音频解码器是自由无损音频解码器 (FLAC)。FLAC 在 Ubuntu 仓库中是被支持的，因为它第 19 节讨论过的 GStreamer 等包。然而，Ubuntu 仓库提供的 FLAC 并不包含 XMMS 的插件，因为 XMMS 不再受支持。因此，我们需要以于通常的方式构建 FLAC 包并安装它，以避免与官方 FLAC 包提供的二进制文件、库和其他文件冲突。这应该是很容易，原因如下：

- FLAC 包安装在 `/usr` 目录层次结构下，而我们构建的 XMMS 版本位于 `/usr/local`。

- `/usr/local` 是大多数开源软件安装的默认路径。该目录在 Ubuntu 构建过程中会被覆盖，因此，如果我们想覆盖默认值，我们的自定义 FLAC 软件将自动使用 `/usr/local`。

- 使用包管理器检索它很容易。

*(注：此处原文文本似乎存在损坏或不完整，以上已根据上下文进行了可能的翻译)*

## 第四部分 额外章节

- **NetBeans:** NetBeans IDE 是一个用 Java 编写的完整 IDE，用于使用 Java、C++ 和 Ruby 等语言开发应用程序。由于它是用 Java 编写的，它可以运行在许多平台上，包括 Microsoft Windows、Linux、Mac OS X 和 Solaris，因此是 Eclipse 跨平台替代方案的良好选择。有关 NetBeans 的更多详细信息，请访问其主页：http://netbeans.org。

- **Pida:** Pida（Python 集成开发应用程序）是一个基于 GTK 的 IDE，用于使用 Python 脚本语言编写操作模式图形化应用程序。pida IDE 非常流行，并支持在其统一框架内轻松集成熟悉的开发工具。有关关于 pida 的更多信息，请访问其主页：http://pida-berlios.de。

- **Sbcl:** sbcl IDE（Steel Common Lisp）是一个为用 Lisp 语言编写的应用程序提供的图形环境。sbcl IDE 最初基于卡内基·梅隆大学 CMU Lisp 提供的 Common Lisp 环境，但目前由其他人进行维护和增强。sbcl IDE 具有原生的 Lisp 代码解析器和复杂的调试器。有关关于 sbcl 的更多信息，请访问其主页：http://sbcl.forge.net。

- **Free-java-sdk:** Free-java SDK 是通过结合和集成顶级的开源工具创建的 IDE，旨在为 Systems 提供的标准 Java 开发工具包（JDK）提供替代方案。free-java-sdk 程序包是由 Debian 发行版开发者提供的各种开源项目汇集的，因此被 Ubuntu Linux 继承。
