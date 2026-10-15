
ftp://ftp.uu.net/graphics/jpeg/

将下载的文件解压到`/usr/local/src`。进入新创建的目录并输入：

```bash
./configure
```

默认情况下，它将到`/usr/local/lib`。这将配置程序在你的计算机上进行编译。运行完成后，输入：

```bash
make && make test
```

如果没有错误，输入：

```bash
make install
```

此时，编辑名为`/etc/ld.so.conf`的文件。如果该文件中没有看到`/usr/local/lib`，请将其添加到最后最后行。接下来，输入：

```bash
/sbin/ldconfig -v | more
```

你会在输出中看到多个以`libjpeg*`开头的文件。

# 安装 GIMP：Libtiff 283

解压此包并进入新目录。Zlib 使用不同的配置脚本进行安装，但命令行选项是类似的。输入以下命令设置编译环境：

```
./configure
```

使用`--prefix`选项设置不同的安装位置：

```
make test
```

这应该会在没有任何错误的情况下运行。如果你在运行`make test`时遇到错误，请检查`README`文件以获取额外说明。假设它在没有任何错误的情况下运行，输入以下命令：

```
make install && ldconfig
```

### A.3.3 PNG

读取和写入 PNG 文件需要 PNG 库。可以在这里获取：

```
ftp://ftp.uu.net/graphics/png/src/
```

在安装 PNG 之前，必须安装并运行`zlib`。PNG 的安装过程不是标准方法，因此仔细阅读`INSTALL`文件非常重要。开始时，当你位于`libpng`目录时，输入以下命令：

```
cp scripts/makefile.lnx Makefile
```

接下来，编辑`pngconf.h`以进行任何必要的配置更改。标准的 Linux 系统通常不需要任何更改。

注意，如果你正在运行 PowerPC 处理器，请取消注释`PNG_BIG_ENDIAN_SUPPORTED`所在的行。

![](img/f2e1dc39d482e76a84057f638c7a2d3f_306_0.png)

接下来，输入以下命令：

```
make test
```

这将运行一个很小的测试程序，读取示例 PNG 文件并将其保存到另一个文件中。如果这两个 PNG 文件完全相同，则 PNG 库已准备好进行编译。如果你在此处遇到问题，请返回并确保`zlib`已正确安装。如果你在`zlib`目录运行了`make test`且运行成功，则说明`zlib`安装正确。接下来，输入以下命令：

```
make install && ldconfig
```

PNG 现在已安装在你的系统上。

### A.3.4 Libtiff

Libtiff 的安装非常简单。可以在这里找到：

```
ftp://ftp.sgi.com/graphics/tiff
```

解压此文件并进入`tiff-<版本号>`目录。

相关文档在`html`目录中。如果你愿意，可以阅读`index.html`文件及其说明。如果你是标准 Linux 系统，输入以下命令：
`./configure && make`

如果没有错误，输入以下命令：
`make install && ldconfig`

之前描述的库是运行功能性 GIMP 所需的所有库。可以安装其他库，但它们有非常特定的用途，大多数用户并不需要它们。下一个库 GTK+ 是运行 GIMP 必需的。

# A.4 安装 GTK+

GTK+，或 GIMP 工具包（Toolkit），是一个极其灵活的库，用于为 X Window 系统创建图形用户界面。Linux 许多应用程序都使用这个库，你会发现在系统上安装它非常有用。由于它广受欢迎，GTK+ 可能已经安装在你的系统上了。如果它过时，可能会导致困难，除非你拥有最新版本的 GTK+，否则删除旧库并安装新版本。

### A.4.1 编译并安装 Glib 和 GTK+

如果你决定升级或安装 GTK+，则有必要下载。GTK+ 的主页为 http://www.gtk.org，文件位于：
`ftp://ftp.gtk.org/pub/gtk`

第一步是安装`glib`，它之前包含在 GTK+ 中，但现在已增长到需要独立分发的程度。它位于与 GTK+ 相同的目录下。首先解压`glib`归包并进入该目录。输入以下命令为你的系统配置归包：
`./configure --disable-debug`

完成后，输入以下命令：
`make`

该库最常见的错误与线程有关。如果发生与线程相关的错误，请使用`--enable-threads=no`选项重新配置`glib`。

如果`glib`在没有错误的情况下完成安装，请输入以下命令：
`make install && ldconfig`

`glib`将为你的系统完成配置。完成后，返回`/usr/local/src`目录并解压 GTK+ 归包。要配置此包，输入以下命令：
`./configure --disable-debug`

# 安装 GIMP：编译并安装 GIMP

输入`--disable-debug`会从二进制文件中移除调试信息，从而产生更小、运行更快的程序。如果你感兴趣通过通过故障排除帮助 GTK+ 的开发，可以开启调试。这只有在你修改 GTK+ 代码时才是有必要的。

如果你有一个数位板，你还会想要 XInput 支持。这通过在`configure`命令中添加`--with-xinput=free`实现。

如果编译在没有错误的情况下完成，输入以下命令：

```
make && make install && ldconfig
```

如果你在编译 GTK+ 时遇到关于`gettext`的错误，请在运行`configure`时添加命令`--disable-tls`。

# A.5 GIMP

在 GIMP 需要的所有库都运行并安装后，终于是安装 GIMP 的时候了。在安装完所有其他库后，GIMP 的安装应该非常简单。不过，请准备好去泡咖啡。GIMP 的编译时间将是 Linux 内核的三倍以上。双 Pentium II 处理器在这里非常好。

### A.5.1 哪个版本适合我？

取决于你使用的 GIMP。如果你想要前沿功能，使用开发版。如果你需要一个不会意外崩溃的版本，使用稳定版。GIMP 软件包可以在这里获取：
`ftp://ftp.gimp.org/pub/`

`imp`软件包可以在这里获取。如果你要安装稳定版 GIMP，还需要下载额外的。这将为你提供许多额外的渐变、笔刷等。

### A.5.2 编译并安装 GIMP

在下载完成后，解压 GIMP 归包并进入该目录。输入以下命令配置你的系统：

```
./configure --disable-debug
```

完成后，检查文件查看是否生成了任何错误。常见的错误是缺少`zlib`库。日志文件将显示：

# 安装 GIMP

如果在检查 JPEG、PNG 或 TIFF 库时遇到任何错误，请返回并确保这些库已正确安装。如果这些库无法工作，GIMP 可以正确编译但拒绝打开图像。当你确定一切已就绪时，输入以下命令：

```
make
```

这需要很长时间（去泡咖啡）。编译完成后，输入以下命令：

```
make install && ldconfig
```

这将安装 GIMP 的二进制文件。如果你下载了额外文件，将其解压到`/usr/local/src`并进入该目录。输入以下命令：

```
./configure && make install
```

你现在有一个可以运行的 GIMP！！是时候开始使用了。不建议以 root 用户身份工作，请以普通用户登录。启动 X Windows。新的窗口管理器会在菜单中带有 GIMP 条目。是时候加载它了。如果你没有 GIMP 条目，打开一个`xterm`并输入以下命令：

```
gimp
```
