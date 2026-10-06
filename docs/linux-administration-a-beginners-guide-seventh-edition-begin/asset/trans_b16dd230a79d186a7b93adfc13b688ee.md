

## 114 Linux 系统管理：入门指南

要查看软件包带有哪些配置选项，只需简单运行：

```
[root@server hello-2.10]# ./configure --help
```

是的，在 "help" 单词前面有两个连字符（--）。

> 注意：一个常用的选项是 --prefix。该选项允许你设置软件包安装的基础目录。默认情况下，大多数软件包使用 /usr/local。软件包中的每个组件将安装到 /usr/local 中相应的目录中。

如果你对 configure 脚本提供的默认设置满意，请输入以下内容：

```
[root@server hello-2.10]# ./configure
checking for BSD-compatible install... /usr/bin/install -c
checking whether build environment is sane... yes
checking for a thread-safe mkdir -p... /usr/bin/mkdir -p
checking for gawk...
checking whether sets {MAKE} ... yes
checking whether supports nested variables... yes
checking for gcc... gcc
...OUTPUT TRUNCATED...
config.status: creating po/POTFILES
config.status: creating po/Makefile
```

根据你设置的所有选项，运行 configure 脚本将创建一个类型名为 Makefile 的特殊文件。Make 是编译阶段的基础。通常，如果 configure 失败，你就无法获得 Makefile。请确保 configure 确实无错误地完成。

## 编译软件包

这个阶段不符合我们约会模型中的任何阶段！但你可能会将其比作盲目热爱的时期，一切都进展得飞快，很多事情都无法解释。

你所做的就是运行 make，如下所示：

```
[root@server hello-2.10]# make
```

make 会读取 configure 脚本创建的所有文件。这些文件告诉 make 应该编译哪些文件以及按什么顺序编译它们——这至关重要，因为可能有成百个源文件。取决于你的系统速度、可用内存以及它处理其他事务的忙碌程度，编译过程可能需要一段时间才能完成，所以不要感到惊讶。

## 第 4 章：软件管理

## 115

当 make 工作时，它会显示它正在运行的每条命令以及与其相关的所有参数。这些输出是编译器的常规调用以及传递给编译器的所有参数——这些是非常枯燥的内容，甚至程序员也倾向于自动化它们！

如果编译顺利通过，你将看不到任何错误信息。大多数编译器错误信息都是清晰且明显的，所以不要担心漏掉某个错误。如果你看到错误，不要恐慌。大多数错误信息并不反映程序本身的问题，而是通常是系统以某种方式出现。通常，这些信息由于文件权限不当或找不到文件/库导致的。

通常情况下，慢下来阅读错误信息。即使它看起来有点奇怪，它也可能用通白的英语解释哪里有问题，让你能够修复它。如果错误仍然令人困惑，查看软件包的文档，看是否有可以联系的邮件列表或电子邮件地址。大多数开发者非常乐意提供帮助，但你需要保持友好并直奔主题。（换句话说，不要在邮件的开头就开始大抱怨软件有多糟糕）。

## 安装软件包

你几乎完成了所有的工作。你找到了你的伴侣，研究了他们，编译了他们——现在是时候让他们和你住在一起了——再次！
与编译不同，安装阶段通常非常顺利。在大多数情况下，一旦编译成功完成，你只需要运行以下命令：

```
[root@hello-2.10] # make install
```

这将软件包安装到你之前在使用 configure 脚本时指定的默认前缀（或 --prefix）参数所的位置。
它将启动安装脚本（通常嵌入在 Makefile 中）。因为 make 在执行时会显示每条命令，所以你会看到大量的文本。不要担心——这是完全正常的。除非你看到错误信息，否则软件包将安全地安装。

如果你看到错误信息，最可能是因为权限问题。查看它之前尝试安装的最后一个文件，并检查在类位置放置文件所需的所有权限。你可能在这一步需要使用 chmod、chown 和 chgrp 命令。

> 注意：如果安装的软件旨在全系统使用，那么 make install 阶段几乎总是需要超级用户（root 用户）执行的。因此，大多数指令都会要求你在执行此操作之前成为 root 用户。

另一方面，如果一个普通用户为个人使用编译并安装软件软件包到该用户具有完全权限的目录中（例如，通过指定 --prefix=/home/<USERNAME>/local/），则不需要变成 root 即可运行 make install 阶段。

![](img/9f6657924397c33f088db5321b751a83_141_0.png)

## 测试软件

一个常见的错误是经历了配置和编译过程，但在安装时，他们没有测试软件以确保它按预期运行。如果软件要供非 root 用户使用，则测试软件也需要作为普通用户进行。

例如，我们将运行 `hello` 命令来验证它是否按预期运行。假设你更改了路径，请使用二进制文件的完整路径来执行：

```
[root@server hello-2.10]# /usr/local/bin/hello
```

Hello, world!

## 清理

软件包安装完成后，你可以对安装过程中创建临时文件进行清理。由于你拥有提取源代码的原始 tar 包，你可以运行以下命令来执行：

```
[root@server src]# rm -f /usr/local/hello-2.10.tar.gz
```

