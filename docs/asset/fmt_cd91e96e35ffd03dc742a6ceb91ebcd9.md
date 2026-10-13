
- 向上更改目录一级，这样当您发出 `pwd` 命令时，可以看到当前位置是 `/usr/local/gnu`。

- 解压和 gunzip `libPropList-0.10.1.tar.gz` 文件，这会创建一个同名的目录。

- 进入新目录并阅读那里的 `INSTALL` 文件，就像您处理 `WindowMaker` 文件时所做的那样。说明非常简单。

- 按顺序单独执行以下每个命令，安装应该就不会有复杂的问题。请注意，大多数 `make install` 命令通常是最后一步，并且通常应作为 root 用户执行。

```text
./configure
make
make install
```

确保单独发出每个命令。如果收到任何错误消息，请记录下来，并检查是否正确执行了指示。通常简单的拼写错误会导致最糟糕的错误。很容易将句号与逗号混淆，特别是如果您的视频分辨率设置较高的情况下。

如果您过去成功编译过该程序，并且上述程序显得“司空见惯”，您可以按顺序执行所有命令，或者将其作为一个单一命令执行：

```
./configure ; make ; make install
```

一旦成功安装了 `libPropList` 二进制文件，您会注意到源代码目录仍然在 `/usr/local/gnu` 中。不要急于立即删除此目录。您可能仍然希望参考其内容，或者如果您怀疑二进制文件已损坏（一种不太可能但可能发生的情况），您可以重新编译该程序。

在验证所有必需的文件都已安装后，您应该准备好编译和安装 `Window Maker`。您可以在一条命令中移动到旧的目录位置——也就是说，向上移动一级目录结构，然后再回到新的目录中。如果您仍在 `libPropList-0.10.1/` 目录中，您可以通过输入以下内容更改到 `WindowMaker-0.63.0/` 目录：

```
cd ../WindowMaker-0.63.0/
```

输入 `pwd` 以验证您是否在正确的目录中。再次通读 `INSTALL` 文件，以确保您理解需要哪些文件以及需要做什么。幸运的是，`Window Maker` 的作者们意识到许多初学者首先通过编译如他们这样的 GUI 来学习 Linux，因此他们非常小心地编写了说明，且没有以居高临下的方式对待新手。

### 运行 Configure 程序

与 `libPropList` 安装一样，您首先需要输入以下内容开始 `configure` 程序：

```
./configure
```

然而，与 `libPropList` 不同，`configure` 程序允许您指定额外的选项。要启用声音以及与其他窗口管理器的兼容性，只需输入以下内容：

```
./configure --enable-sound --enable-gnome --enable-kde
```

`configure` 脚本的目的是检查二进制文件所需的程序与机器上已安装的程序。如果它发现 Linux 安装缺少某个二进制文件或库，`configure` 脚本将停止并打印一条错误消息，解释无法在给定步骤继续的原因。大多数 `configure` 脚本现在是标准化的，因为运行较新的程序需要一组特定的库和程序。不久之前，许多变量必须手动检查，并且在命令行中正确放置适当的选项，以便每个程序都知道在哪里找到依赖的文件。`configure` 脚本使许多这种手工操作过时了。

其功能是创建 `makefile`。该文件是根据系统上加载的可用选项动态生成的。您可以接受基于脚本所确定已安装组件的 `makefile`，或者稍后手动编辑 `makefile`。您可以编辑 `makefile`，使其执行您需要它执行的操作。例如，如果您需要包含额外的库，或者路径错误（即，它指向位于您的路径中比您想要使用的目录更早的目录中的二进制文件），您可能需要编辑该文件。一些程序员不建议摆弄生成的 `makefile`，理由是他们自己的程序可能会因此失败。新手程序员经常摆弄代码，导致无法干净地编译代码。然后他们责怪作者而不是自己。

以下是 `./configure` 命令生成输出的一个小示例。您可以看到如何查询每个单独的包以及响应是什么，即是否找到了正确版本的程序。在此实例中，`configure` 程序运行成功。

```
### pwd
/usr/local/gnu/WindowMaker-0.63.0/
```

## 安装额外的程序

第 11 章

343

```
# ./configure --enable-sound --enable-gnome --enable-kde
loading cache ./config.cache
checking for a BSD compatible install... (cached) /usr/bin/install -c
checking whether build environment is sane... yes
checking whether make sets ${MAKE}... (cached) yes
checking for working aclocal... found
checking for working autoconf... found
checking for working automake... found
checking for working autoheader... found
checking for working makeinfo... found
checking host system type... i586-pc-linux-gnu
checking for ranlib... (cached) ranlib
checking for gcc... (cached) gcc
checking whether the C compiler (gcc ) works... yes
checking whether the C compiler (gcc ) is a cross-compiler... no
checking whether we are using GNU C... (cached) yes
checking whether gcc accepts -g... (cached) yes
checking for ld used by GCC... (cached) /usr/bin/ld
checking if the linker (/usr/bin/ld) is GNU ld... (cached) yes
checking for BSD-compatible nm... (cached) /usr/bin/nm -B
checking whether ln -s works... (cached) yes
checking for object suffix... o
checking for executable suffix... no
checking for gcc option to produce PIC... -fPIC
checking if gcc PIC flag -fPIC works... yes
checking if gcc supports -c -o file.o... yes
checking if gcc supports -c -o file.lo... yes
checking if gcc supports -fno-rtti -fno-exceptions... yes
checking if gcc static flag works... -static
checking if the linker (/usr/bin/ld) is GNU ld... yes
checking whether the linker (/usr/bin/ld) supports shared libraries... yes
checking command to parse /usr/bin/nm -B output... ok
checking how to hardcode library paths into programs... immediate
checking for /usr/bin/ld option to reload object files... -r
checking dynamic linker characteristics... Linux ld.so
checking if libtool supports shared libraries... yes
checking whether to build shared libraries... yes
checking whether to build static libraries... yes
```

```
checking for bdir… .libs
creating libtool
Fixing libtool for -rpath problems.
checking host system type… i586-pc-linux-gnu
checking for POSIXized ISC… no
checking for gcc… (cached) gcc
checking whether the C compiler (gcc -g -O2 ) works… yes
```
