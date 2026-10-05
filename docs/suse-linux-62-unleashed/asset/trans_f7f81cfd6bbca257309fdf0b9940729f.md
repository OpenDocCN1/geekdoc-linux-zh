

# SuSE Linux 编程工具
第25 章

# 注意

根据 LessTif 开发者的说法，IBM 的 ViaVoice 在其 Linux 版本使用了 LessTif。

# 构建、安装和测试 LessTif

虽然 LessTif 包含在 SuSE Linux 中，但你可以通过 http://www.lesttif.org 找到最新的 Linux 版 LessTif 发行版（可能在 ftp.hung.com 或镜像站点）。按照说明下载当前版本 0.89 的源代码或二进制归包，该版本压缩格式下略大于 3MB，解压后占用超过 15MB空间。使用 `tar` 命令解压 LessTif 归包，后跟包名，如下所示：

```
# tar xvzf lestif-0.88.0.tar.gz
```

接下来，进入 LessTif 目录并使用 `configure` 命令为你的系统配置软件构建，如下：

```bash
# ./configure
```

然后你可以使用 `make` 命令构建软件，如下：

```bash
# make
```

大约 15 分钟后（在 64MB、300MHz 的 Pentium 计算机上），构建将完成。

# 提示

在安装 LessTif 之前，先切换到测试目录，然后配置并 `make` LessTif 测试套件，如下：

```bash
# ./configure
# make
```

这将创建近 200 个程序并提供大量的示例源码：

如需安装 LessTif 库和文档，再次使用 `make` 命令后接 `install`，如下（以 root 用户身份）：

```bash
# make install
```

![](img/cbac72550c7126a22162e94d91a0c360_810_0.png)

# 图形、多媒体和效率工具
第四部分

LessTif 的包含文件和库将安装 /usr/local 目录下。你可以通过编译并运行示例 Motif 文件（列表 25.5）来测试 LessTif 的安装，如下：

```bash
# gcc -o lestifskel skel.c -L/usr/local/lib -IXm -L/usr/X11R/lib -ISM -LICE -Ixt -IX11
```

注意在 /usr/local/lib 路径使用了 `-l` 链接器选项。这告诉链接器在 /usr/local/lib 目录下查找任何所需的库。此外，注意你可以多次使用此选项。程序构建并链接后，尝试运行生成的客户端，如下：

```
./lestifskel
```

你可能会得到关于找不到 Motif 共享库的错误：

```
./lestifskel: error in loading shared libraries:
libXm.so.1: cannot open shared object file: No such file or directory
```

这是因为程序找不到 LessTif 库。解决方案是定义并存储环境变量 LD_LIBRARY_PATH，并将其指向已安装的 LessTif 库，如下：

```
# LD_LIBRARY_PATH=/usr/local/lib;export LD_LIBRARY_PATH
```

然后你就可以运行编译后的程序。当前的发行版不需要你使用 `make` 或 `xkmmf`，并且带有共享库和静态库。如果你是一个真正的 Motif 黑客，并且对图形界面构建和组件编程的内部感兴趣，你应该阅读 LessTif 如何构建的细节。你可以在 http://www.igpm.rwth-aachen.de/-albrecht/hungry.html 免费获得 Harold Albrecht 的书籍《Inside LessTif》。

# Perl 编程

Perl（实用提取与报告语言）由 Larry Wall 在 20 世纪 80 年代开发，他已经负责过许多相当重要的 UNIX 工具。Larry 声称 Perl 实际上代表“Pathologically Eclectic Lister”（病态折衷主义列表器）。随着 90 年代初万维网的诞生，Perl 成为 CGI 编程的首选语言。随着开源运动的兴起，Perl 获得的关注几乎与 Linux 不相上下。

Larry 表示，Perl 都是让简单的事情变得简单，让困难的事情变得可能。许多语言让你在内存分配和变量类型上花费过多的时间，而 Perl 包含了 C、BASIC 以及其他编程语言的特征。

在 Perl 中，“有多种方法实现”（there is more than one way to do it）是 Perl 的非正式格言，它出现的频率高到被通用缩写为 TIMOWDI。如果你熟悉其他编程语言，就可以编写功能 Perl 代码。

在写作期间，Perl 的当前生产版本是 5.005_03（包含在本书 CD 中）。5.07 版本作为开发者版本可用（通常被认为是实验性的）。你可以通过在 shell 提示符输入 `perl -v` 来确定安装的 Perl 版本。

Perl 是一种解释语言。它已移植到许多操作系统，用于 Web 开发、文本处理和系统管理等各种用途。

#  Perl 程序

以下示例是一个基本的 Perl 脚本：

```perl
#!/usr/bin/perl
print "Hello, world!\n";
```

以下示例了如何在 Perl 中使用变量：

```perl
$name = "Alice";
$age = 30;
print "My name is $name and I am $age years old.\n";
```

以下示例演示了如何在 Perl 中使用循环：

```perl
for ($i = 0; $i < 5; $i++) {
    print "Iteration $i\n";
}
```

以下示例了如何在 Perl 中使用条件语句：

```perl
if ($age >= 18) {
    print "You are an adult.\n";
} else {
    print "You are a minor.\n";
}
```

Perl 是一种强大且多功能的语言，可以用于广泛的任务。通过不断练习，你可以学会使用 Perl 做一些惊不起的事情。

