
`done`

`$`

````

`patch` 命令现在将`file1.c`修改为与`file2.c`相同。

`patch` 还有一个额外的技巧：撤销的能力。假设我们不喜欢这些更改并想要恢复原始的`file1.c`。没问题；只需再次使用`patch`并使用`-R`（反向补丁）选项。

````

```bash
$ patch -R file1.c diffs

Hmm... Looks like a normal diff to me...

Patching file1.c using Plan A...

Hunk #1 succeeded at 1.

Hunk #2 succeeded at 4.

Hunk #3 succeeded at 6.

done

$
```

`file.c`回到了原始状态。

`patch` 命令还有其他几个选项，但它通常非常擅长根据输入判断你想做什么，然后“做正确的事”。如果`patch`任何时候失败，它会创建一个`.rej`扩展的文件，其中包含无法补丁的部分。

当你处理软件补丁时，使用`diff -c`选项是一个好主意，它产生“上下文差异”。这提供了每个更改前后的若干行，以便`patch`在应用补丁之前验证上下文是否匹配。补丁也更容易阅读了。

> 如果你在程序中发现并修复了一个漏洞，给作者发送补丁比只发送文件描述更简单、更精确且更有礼貌。

## 其他分发工具

Linux 程序和源码通常分发在一个文件名包含版本号、扩展名为`.tar.gz`或`.tgz`的文件中。这些是 gzipped TAR（带档）文件，也称为“tarballs”。如果你使用普通的`tar`，必须分两个步骤处理这些文件。让我们为我们的应用程序创建一个 gzip 文件。

```bash
$ tar cvf myapp-1.0.tar main.c 2.c 3.c *.h
```

# 第 9 章

## 使用 RPM 包文件

每个软件包都存储在以`.rpm`扩展的文件中。软件包通常遵循具有以下结构的命名规范：

````
name-version-release.architecture.rpm
````

在这一结构中，`name`（名称）包含了软件包的通用名称，例如 MySQL 数据库的`mysql`，或者用于构建工具的`make`。`version`（版本）包含软件的版本号，例如 MySQL 的`3.23.54a`版本。`release`（发行）包含一个数字，指定文件中包含该版本的 RPM 的哪个发行版本。这非常重要，因为 RPM 包是由一组指令构建的（在本章稍后的“创建 RPM Spec 文件”中将介绍这些指令）。发行版本号允许你跟踪构建指令的更改。

`architecture`（架构）代表程序的架构，例如基于 Intel 系统的`i386`。对于编译后的程序，例如，为 SPARC 处理器创建的可执行文件很可能无法在 Intel 处理器上运行。架构可以是通用的，例如针对 SPARC 处理器的`sparc`，或者针对 AMD Athlon 芯片的`specx86_v9`。除非你对其进行覆盖，否则 RPM 系统将阻止你安装适用于不同架构的软件包。

对于不针对特定架构的软件包，架构也可以包含特殊值`arch`（例如文档文件、Java 程序或 Perl 模块），以及用于源码包的`src`。源码 RPM（Source RPM，简称 SRPM）包含了构建二进制 RPM 包所需的文件和构建指令。你发现的大多数下载 RPM 包都是为特定架构预构建的，这增加了数千个已预构建并准备好安装为 RPM 包的 Linux 软件包。这节省了你编译的麻烦。

此外，某些软件包依赖于特定版本，下载预构建的包比手动测试所有组件要容易得多。例如，802.11b 无线网络包是针对特定的内核补丁级别预构建的，如`kernel-wlan-ng-modules-rh18.0.2.7-athlon.rpm`，它包含了在 AMD Athlon 处理器上带有`2.4.218`内核的 Red Hat 9.0 的内核模块。

## 安装 RPM 包

要安装 RPM 包，请运行`rpm`命令。格式非常简单：

```bash
rpm -Uhv name-version-release.architecture.rpm
```

例如，

```bash
rpm -Uhv mysql-server-3.32.54a-11.i386.rpm
```

此命令安装（或升级）适用于 Intel x86 架构系统的`mysql-server`软件包。

`rpm`命令提供了与 RPM 系统的大多数用户交互。你可以使用如下命令查询是否安装了某个包：

```bash
rpm -qa mysql-server-mysql-server-3.32.54a-11
```

## 构建 RPM 包

要构建 RPM 包，请运行`rpmbuild`命令。该过程相对简单。我们需要：

- 收集你想要打包的软件。
- 创建描述如何构建软件包的`spec`文件。
- 使用`rpmbuild`命令构建软件包。

由于 RPM 的创建可能非常复杂，我们在本章中将坚持一个简单的示例，该示例应该足够以源码或二进制形式分发一个合理的应用程序。我们将感兴趣的读者留给更深奥的选项以及对通过补丁检索的软件包的支持。请查看 RPM 程序的手手册或 RPM HOWTO（通常在`/usr/doc`中）以获取更多信息。此外，请查看 Eric Foster-Johnson 编写的 Red Hat RPM Guide（Red Hat Press/Wiley）。

以下章节将针对我们简单的应用程序`myapp`遵循上述三个步骤。

## 收集软件

构建 RPM 包的第一步是收集你想要打包的软件。在大多数情况下，你将拥有应用程序源代码、一个构建文件（如`makefile`）以及可能还有一个在线帮助页。

收集这些软件最简单的方法是将这些文件打包成一个 tar 包（tarball）。用应用程序名称和版本号命名 tar 包，例如`myapp-1.0.tar.gz`。

我们可以修改之前的`makefile`以添加一个新目标，将文件构建为 tar 包。`makefile`如下：

```makefile
all: myapp

# 使用什么编译器

CC = gcc

# 头文件存放在哪里

INCLUDE = .

# 开发选项

CFLAGS = -g -Wall -ansi

# 发布选项

# CFLAGS = -O -Wall -ansi

# 本地库

MYLIB = mylib.a

myapp: main.o $(MYLIB)

	$(CC) -o myapp main.o $(MYLIB)

$(MYLIB): $(MYLIB) (2.0) $(MYLIB) (3.0)

main.o: main.c a.h

2.0: 2.c a.h

3.0: 3.c b.h

clean:

	-rm main.o 2.o 3.o $(MYLIB)
```

```makefile
dist: myapp-1.0.tar.gz

myapp-1.0.tar.gz: myapp

	-rm -rf myapp-1.0

	mkdir myapp-1.0

	cp *.h Makefile myapp-1.0

	tar zcvf $@ myapp-1.0
```

`makefile`中的`myapp-1.0.tar.gz`目标构建了我们简单应用程序源码的 tar 包。为了简单起见，我们添加了`dist`目标并调用相同的命令。运行以下命令来创建包：

```bash
$ make dist
```

然后我们需要将文件`myapp-1.0.tar.gz`复制到 RPM SOURCES 目录，通常是`/usr/src/redhat`。例如，

```bash
$ cp myapp-1.0.tar.gz /usr/src/redhat
```

这是 RPM 系统期望的源码 tar 包。这是 RPM 系统期望的软件包。例如，

```bash
$ ls SOURCES
```

RPM 系统期望源码以 tar 包的形式位于`SOURCES`中。`spec`文件以名称、版本号以及关于软件包的其他信息的定义开始。例如：

```spec
Vendor: Wrox Press

Distribution: Any

Name: myapp

Version: 1.0

Release: 1

Packager: neil@provider.com

License: Copyright 2003 by Wrox Press

Group: Applications/Media
```
