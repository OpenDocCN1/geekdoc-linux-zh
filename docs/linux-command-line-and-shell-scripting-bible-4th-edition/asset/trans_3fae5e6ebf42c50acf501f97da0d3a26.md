

## 在命令行上定义函数

您可以直接在命令行上定义函数。您可以以两种方式做到这一点。

第一种方法将函数定义在同一行中：

```bash
$ function divem { echo $[ $1 / $2 ]; }
$ divem 100 5 20
$
```

当您在命令行上定义函数时，必须记得在每个命令末尾包含分号，以便 shell 知道在哪里分隔命令：

```bash
$ function doubleit { read -p "Enter value: " value; echo $[ $value \* 2 ]; }
$ doubleit
Enter value: 20
40
$
```

另一种方法是使用多行来定义函数。当您这样做时，Bash shell 会使用二级提示符要求您输入更多命令。使用这种方法，您不需要在每个命令末尾放置分号；只需按 Enter 键即可。

```bash
$ function multern {
> echo $[ $1 \* $2 ]
> }
$ multern 2 5 10
$
```

当您在函数末尾使用花括号时，shell 就知道您已完成函数定义。

### 警告

在命令行上创建函数时要格外小心。如果您使用的函数与内置命令或其他命令同名，该函数将覆盖原始命令。

## 在 `.bashrc` 文件中定义函数

直接在命令行上定义 shell 函数的明显缺点在于，当您退出 shell 时，您的函数会消失。对于复杂的函数，这可能成为一个问题。一种简单得多的方法是将函数定义在一个每次启动新 shell 时都会被 shell 重新加载的位置。

最佳位置是 `.bashrc` 文件。每次启动时，无论是交互式启动还是从现有 shell 内部启动新 shell，Bash shell 都会在其主目录中查找此文件。

### 直接定义函数

您可以直接在主目录的 `.bashrc` 文件中定义函数。大多数 Linux 发行版已经在 `.bashrc` 文件中定义了一些内容，因此请小心不要删除这些项。只需将您的函数添加到现有文件的底部即可。以下是这样做的一个示例：

```bash
$ cat .bashrc
# .bashrc

# Source global definitions
if [ -r /etc/bashrc ]; then
    . /etc/bashrc
fi

function addem {
    echo $[ $1 + $2 ]
}
```

在下一次您启动新的 Bash shell 之前，该函数不会生效。那样做之后，您可以在系统的任何地方使用该函数。

### 加载函数文件

与 shell 脚本一样，您可以使用 `source` 命令（或其别名，点运算符）从现有库文件中将函数添加到您的 `.bashrc` 脚本中：

```bash
$ cat .bashrc
# .bashrc

# Source global definitions
if [ -r /etc/bashrc ]; then
    . /etc/bashrc
fi

. /home/rich/libraries/myfuncs
$
```

请确保您包含正确的路径名，以便 Bash shell 能够找到并引用库文件。下次您启动 shell 时，您的库中的所有函数都可在命令行界面中使用：

```bash
$ addem 10 5
15
$ multem 10 5
50
$ divem 10 5
2
$
```

更好的是，shell 还会将已定义的函数传递给子 shell 进程，以便您的函数自动可用于您从 shell 会话运行的任何 shell 脚本。您可以通过编写一个使用这些函数而不定义或加载它们的脚本来测试这一点：

```bash
$ cat test15
#!/bin/bash
# using a function defined in the .bashrc file

value1=10
value2=5
result1=$(addem $value1 $value2)
result2=$(multem $value1 $value2)
result3=$(divem $value1 $value2)
echo "The result of adding them is: $result1"
echo "The result of multiplying them is: $result2"
echo "The result of dividing them is: $result3"
$
```

```bash
$ ./test15
The result of adding them is: 15
The result of multiplying them is: 50
The result of dividing them is: 2
$
```

即使没有加载库文件，这些函数在 shell 脚本中也完美地工作。

# 通过实际示例进行操作

使用函数的内容远不止创建自己的函数。在开源世界中，代码共享至关重要，这也适用于 shell 脚本函数。有许多不同的 shell 脚本函数可供您下载并用于自己的应用程序中。

本节将引导您下载、安装和使用 GNU shtool shell 脚本函数库。shtool 库提供了一些简单的 shell 脚本函数，用于执行日常 shell 功能，例如处理临时文件和文件夹或格式化输出显示。

## 下载和安装

该过程的第一步是下载并将 GNU shtool 库安装到您的系统中，以便您能够在自己的 shell 脚本中使用库函数。为此，您需要使用 FTP 客户端程序或图形桌面上的浏览器。使用此 URL 下载 shtool 包：

```bash
ftp://ftp.gnu.org/gnu/shtool/shtool-2.0.8.tar.gz
```

这将文件 shtool-2.0.8.tar.gz 下载到您的下载文件夹。从那里，您可以使用 Linux 发行版中的 cp 命令行工具或图形文件管理器工具（如 Ubuntu 中的 Files）将文件复制到您的主目录。

将文件复制到主目录后，您可以使用 tar 命令解压它：

```bash
tar -zxvf shtool-2.0.8.tar.gz
```

这将解包文件到一个名为 `shtool-2.0.8` 的文件夹中。使用 `cd` 命令切换到新创建的文件夹：

```bash
cd shtool-2.0.8
```

现在您可以开始构建 shell 脚本库文件了。

# 构建库

shtool 发行版文件必须针对您的特定 Linux 环境进行配置。为此，它使用标准的 `configure` 和 `make` 命令，这些命令通常用于 C 编程环境。要构建库文件，您只需运行两个命令：

```bash
$ ./configure
$ make
```

`configure` 命令检查构建 shtool 库文件所需的软件。随着它找到所需的工具，它会使用正确的工具路径修改配置文件。

`make` 命令执行构建 shtool 库文件的步骤。生成的文件（`shtool`）是完整的库包文件。您还可以使用 `make` 命令测试库文件：

```bash
$ make test
Running test suite:
echo........ok
md4te.......ok
table.......ok
prop........ok
move........ok
install.....ok
mkdir.......ok
mklm........ok
mkshadow....ok
fixperm.....ok
rotate......ok
tarball.....ok
subst.......ok
platform....ok
arx.........ok
slo.........ok
scpp........ok
version.....ok
path.........ok
OK: passed: 19/19
$
```

测试模式测试 shtool 库中可用的所有函数。如果全部通过，则您可以准备将库安装到 Linux 系统上的通用位置，以便您的所有脚本都可以使用它。为此，您可以使用 make 命令的 install 选项。但是，您需要以 root 用户账户登录才能运行它：

```bash
# make install
Password:
./shtool mkdir -f -p -m 755 /usr/local
./shtool mkdir -f -p -m 755 /usr/local/bin
./shtool mkdir -f -p -m 755 /usr/local/share/man/man1
./shtool mkdir -f -p -m 755 /usr/local/share/aclocal
./shtool mkdir -f -p -m 755 /usr/local/share/shtool
...
./shtool install -c -m 644 sh.version
/usr/local/share/shtool/sh.version
./shtool install -c -m 644 sh.path
/usr/local/share/shtool/sh.path
#
```

现在您可以开始在自己的 shell 脚本中使用这些函数了！

## shtool 库函数

shtool 库提供了许多在处理 shell 脚本时可能有用的函数。表 17.1 显示了库中可用的函数。

**表 17.1 shtool 库函数**

| 函数 | 描述 |
| :--- | :--- |
| arx | 创建具有扩展功能的归档 |
| echo | 显示字符串值，带有结构扩展 |
| fixperm | 更改文件夹树内部的文件权限 |
| install | 安装脚本或文件 |
| mdate | 显示文件或目录的修改时间 |
| mkdir | 创建一个或多个目录 |

