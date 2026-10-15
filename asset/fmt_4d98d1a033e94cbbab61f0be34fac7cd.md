
之前的脚本示例需要 `sh` 程序（一种 Linux shell）来运行脚本。你还必须确保脚本文件（如 `listrpmpkgs`）可用。因此，如果你将文件存储在 `/home/user/bin`，运行脚本时使用以下命令：

```
$ sh /home/user/bin/listrpmpkgs
```

这并不方便。此外，你总是必须记住你把 `listrpmpkgs` 文件存储在了哪里。为了让这个命令更好，你可以将脚本转换为命令。

## 将脚本转换为命令

要将脚本转换为命令，需要执行三个简单操作：

1. 在文件开头添加特殊注释（shebang），以便 Linux 识别该文件为命令。
2. 修改文件权限，使其可执行。
3. 将文件复制到你的命令路径目录中。

### 脚本使用 `#` 来向人类读者解释用途。按照惯例，Linux 使用文件第一行的 `#` 注释表示这是一个 shell 脚本。在大多数情况下，应该是 `/bin/sh`。再次编辑你的 `listrpmpkgs`，添加该注释：

```
#!/bin/sh
rpm -qa | grep rpm
```

确保 `#` 注释位于第一行。接下来，修改脚本权限将其标记为可执行。使用 `chmod` 命令。在修改权限之前运行 `ls -l` 命令查看：

```
$ ls -l listrpmpkgs
-rw-r--r-- 1 eric eric Jan 12:00
```

第一组字符 `-rw-r--r--` 表示所有者、组和世界（所有人）的权限。`rw` 表示读写，`r` 表示所有人只读。要为所有者给该文件添加执行权限，使用以下命令：

```
$ chmod u+x listrpmpkgs
```

在这个命令中，`u` 代表文件的所有者（历史原因代表其他人）。`+x` 添加了执行权限。运行此命令后，你可以看到修改后的权限：

```
$ ls -l listrpmpkgs
-rwxr-xr-x 1 eric eric Jan 12:00 listrpmpkgs
```

使用 `man chmod` 命令查看关于此命令的更多信息（img/9d29d6681c5f42792ea5da4b12142ca2_314_0.png）。你现在可以在本地运行该命令了。例如：

```
$ ./listrpmpkgs
librpm404-devel-4.0.4-8x.27
librpm404-4.0.4-8x.27
rpm404-python-4.0.4-8x.27
rpm-4.1-1.06
rpm-devel-4.1-1.06
gnorpm-0.9-1
rpm-python-4.1-1.06
redhat-rpm-config-8.0-1
rpm-build-4.1-1.06
rpmbuild-1.0-0
```

下一步是将文件复制到系统命令路径中的目录。要查看路径中有哪些目录，运行以下命令：

```
$ echo $PATH
/usr/local/bin:/usr/bin:/bin:/usr/X11/bin:/home/eric/bin:/usr/java/jdk1.4.0_01/bin
```

选择这些目录中的一个。`/usr/local/bin` 目录是本地创建命令的常用地方。如果这只是你个人使用的命令，家目录下的目录会更好。在示例中，`/home/eric/bin` 就是一个目录。

### 部分 RPM

如果你使用 C shell (`csh`) 或 Tc shell (`tcsh`)，你需要运行 `rehash` 命令，告诉 shell 重新查看路径中的可用命令。

输入以下命令：

```
$ listrmpmpkgs
librpm404-devel-4.0.4-8x.27
librpm404-4.0.4-8x.27
rpm404-python-4.0.4-8x.27
rpm-4.1-1.06
rpm-devel-4.1-1.06
gnorpm-0.9-1
rpm-python-4.1-1.06
redhat-rpm-config-8.0-1
rpm-build-4.1-1.06
rpmrebuild-1.0-0
```

你现在已经用自己的命令扩展了 Linux 命令集。

Windows 用户可能习惯程序文件名以 `.exe` 结尾，脚本以 `.bat` 或 `.cmd` 结尾。当你运行这些程序或脚本时，不需要包含 `.exe`、`.bat` 或 `.cmd` 扩展名。但在 Linux 和 Unix 中，全名很重要，所以如果你将脚本命名为 `rpminfo.bat`，每次运行脚本都必须输入 `rpminfo.bat`。这就是为什么大多数 Linux 程序和脚本没有扩展名。

如果你想与其他人共享脚本，也应该给他们执行权限。你可以通过以下命令实现：

```
$ chmod a+x listrmmpkgs
```

在这种情况下，`a` 代表所有用户。

## 向你的脚本传递命令行选项

到为止使用的 `listrmmpkgs` 脚本并不好用。它只执行一个命令，仅此而已。在不编写新脚本的情况下，我们无法对其进行自定义。

让脚本更灵活的一种方法是允许它使用命令行选项。就像 `rpm` 命令接受无数种选项一样，你也可以让你的脚本接受选项。

Shell 为传递给 shell 的命令行选项定义了特殊变量。

### 表 15-2 命令行选项的 Shell 变量

| 变量 | 存储内容 |
| --- | --- |
| `$0` | 从命令行输入的脚本本身的名称 |
| `$1` | 第一个选项 |
| `$2` | 第二个选项 |
| `$3` | 第三个选项 |
| `$4` | 第四个选项 |
| `$5` | 第五个选项 |
| `$6` | 第六个选项 |
| `$7` | 第七个选项 |
| `$8` | 第八个选项 |
| `$9` | 第九个选项 |
| `$*` | 所有命令行选项 |
| `$$#` | 命令行选项的数量 |

![](img/9d29d6681c5f42792ea5da4b12142ca2_316_0.png)

> 注意：如果你使用 C shell 运行脚本，请用 `$$argv` 代替 `$$`。

你可以使用这些变量允许用户传递要搜索的文本，而不是总是搜索 rpm。通过此添加，你的新脚本重命名为 `rpmgrep`，如列表 15-1 所示：

### 列表 15-1: rpmgrep

```
#!/bin/sh

rpm -qa | grep $*
```

该脚本现在期望一个包含要搜索文本的命令行选项。将此脚本标记为可执行；然后你可以如下所示运行它：

```
$ ./rpmgrep python
python-devel-2.2.17-17
gnome-python2-gtkhtml2-1.99.11-8
gnome-python2-canvas-1.99.11-8
gnome-python2-1.99.11-8
rpm404-python-4.0-8x.27
orbit-python-1.99.0-4
gnome-python2-bonobo-1.99.11-8
gnome-python2-gconf-1.99.11-8
libxslt-python-1.0.19-1
libxml2-python-2.4.23-1
python-2.2.17-1
rpm-python-4.1-1.06
mod_python-3.0.0-10
python-tools-2.2.17-1
```

如果你想让此命令可用，请按照上一节所述，将其复制到命令行路径中的目录中。

## 检查 RPM 文件

当你处理大量的 RPM 文件时，你会发现对于每个获取的新包，你都会反复运行相同的命令。例如，你可能想查看一个包需要哪些功能。你可以每次输入 `rpm` 命令，或者编写一个带有必要命令行选项的短 shell 脚本。列表 15-2 显示了这个脚本。

### 列表 15-2: rpmdepend

```
#!/bin/sh

rpm -qp --requires *
```

该脚本期望一个 RPM 软件包文件的名称。按如下方式运行命令：

```
$ rpmdepend vim-common-6.1-14.i386.rpm
rmlib(PayloadFilesHavePrefix) <= 4.0-1
rmlib(CompressedFileNames) <= 3.0-4-1
/bin/sh
/usr/bin/awk *
```

## 第 15 章：使用脚本自动化 RPM

`libc.so.6`

`libc.so.6(GLIBC_2.0)`

`libc.so.6(GLIBC_2.0)`

我执行的另一个常见任务是列出 RPM 中的所有文件以及包的描述性信息。这非常有帮助，因为许多 Linux 包的名称没有描述性，例如 `dia` 和 `anaconda`。

### 列表 15-3: rpminfo

```
#!/bin/sh
rpm -qip $* | less
```

该脚本列出一组可能很行，因此脚本将输出管道到 `less` 命令。例如：
