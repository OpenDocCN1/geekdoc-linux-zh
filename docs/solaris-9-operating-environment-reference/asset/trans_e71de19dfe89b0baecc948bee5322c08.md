

# 508

# install

```
::::::::::::::::::::::::::
bibliography.ib
::::::::::::::::::::::::::
yyyy (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy) (yyyyy)
>(yyyyy) (yyyyy)
::::::::::::::::::::::::::
bibliography.ic
::::::::::::::::::::::::::
bibliography:0,721
bibliography:721,720
bibliography:1441,720
bibliography:2161,720
castle%
```

# Files

/usr/lib/refer/mkey

用于映射书目数据库。

/usr/lib/refer/inv

用于反转书目数据库。

x.ia
条目文件文件。

x.ib
发布文件。

x.ic
标签文件。

x.ig
引用文件。

# Attributes

有关以下属性的描述，请参见 attributes(5)：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNdoc |

# See Also

addbib(1), lookbib(1), refer(1), roff(1), sortbib(1), attributes(5)

# install — 安装命令

# Synopsis

```
/usr/sbin/install -c dira [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -f dirb [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -n dir [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -d|-i [-m mode] [-u user] [-g group] [-o] [-s] dir...
/usr/sbin/install [-m mode] [-u user] [-g group] [-o] [-s] file
dirx...
```

# install

# Description

install 命令最常用于 Makefile 中（参见 make(1)），用于将文件安装到特定位置，或在文件系统中创建目录。每个文件都是通过复制到相应的目录来安装的。

install 不使用特殊权限将文件从一个地方复制到另一个地方。其影响如下：

- * 你必须拥有读取要安装文件的权限。
- 你必须拥有复制到目标目录的权限。
- * 如果你想使用 -option 选项，你必须拥有更改文件最终副本的模式的权限。
- * 如果你想通过 -u 或 -g 选项指定安装文件的所有者，你必须是超级用户（superuser）。如果你不是超级用户，则安装文件的所有者将是你，无论原始文件的所有者是谁。

install 会打印消息，准确你它正在替换或创建什么，以及它们将去何处。

如果你没有指定任何选项或目录 (dirx...)，install 将一组默认目录（/bin,/bin,/etc,/lib,/usr/lib）中搜索与 file 同名的文件。当它找到第一次出现的位置时，install 会发出一条消息，说明它正在用 file 覆盖该文件，并继续操作。如果未找到文件，程序将启动并退出。

如果你在 file 之后指定了一个或多个目录 (dirx...)，则会在默认目录之前搜索这些目录。

# Options

- -c dira 如果 file 不存在，则在 dira 指定目录中安装文件。如果找到了，则发出消息说明文件已存在，并退出而不覆盖它。

- -d 创建目录。缺失的父目录将按照 mkdir -p 的要求创建。如果目录已存在，则将所有者、组和模式设置为命令行上给出的值。

- -f 强制将文件安装到给定目录中，即使文件已存在。如果正在安装的文件不存在，将模式设置为 755并将所有者设置为 bin。如果文件已存在，则模式和所有者为现有文件的属性。

- -g group 将新文件的组 ID 设置为 group。仅对超级用户可用。默认设置为 bin。

- -i 忽略默认目录列表，仅在给定的目录 (dirx...) 中搜索。

- -m mode 将新文件的模式设置为 mode。默认设置为 0755。

- -n dirc 如果在任何搜索的目录中未找到文件，则将其放入 dirc 指定的目录。将新文件的模式设置为 755并将所有者设置为 bin。

# 510

# Intro,

- -O 如果找到了文件，则通过将找到的文件复制到其所在目录下的 OLFILE 中来保存该文件。此选项对于安装经常使用的文件（例如 /bin/sh 或 /lib/saf/ttym）非常有用，因为你无法删除现有文件。

- -S 抑制打印错误消息以外的消息。

- -u user 将新文件的所有者设置为 user。仅对超级用户可用。默认设置为 bin。

# Usage

有关大文件的描述，请参见 largefile(5)。

# Attributes

有关以下属性的描述如下：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNdoc |

# See Also

addbib(1), lookbib(1), refer(1), roffbib(1), sortbib(1), attributes(5)

# install — 安装命令

# Synopsis

```
/usr/sbin/install -c dira [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -f dirb [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -n dir [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -d|-i [-m mode] [-u user] [-g group] [-o] [-s] dir...
/usr/sbin/install [-m mode] [-u user] [-g group] [-o] [-s] file
dirx...
```

# install

# Description

install 命令最常用于 Makefile 中（参见 make(1)），用于将文件安装到特定位置，或在文件系统中创建目录。每个文件都是通过复制到相应的目录来安装的。

install 不使用特殊权限将文件从一个地方复制到另一个地方。其影响如下：

- * 你必须拥有读取要安装文件的权限。
- 你必须拥有复制到目标目录的权限。
- * 如果你想使用 -option 选项，你必须拥有更改文件最终副本的模式的权限。
- * 如果你想通过 -u 或 -g 选项指定安装文件的所有者，你必须是超级用户。如果你不是超级用户，则安装文件的所有者将是你，无论原始文件的所有者是谁。

install 会打印消息，准确你它正在替换或创建什么，以及它们将去何处。

如果你没有指定任何选项或目录 (dirx...)，install 将一组默认目录（/bin,/bin,/etc,/lib,/usr/lib）中搜索与 file 同名的文件。当它找到第一次出现的位置时，install 会发出一条消息，说明它正在用 file 覆盖该文件，并继续操作。如果未找到文件，程序将启动并退出。

如果你在 file 之后指定了一个或多个目录 (dirx...)，则会在默认目录之前搜索这些目录。

# Options

- -c dira 如果 file 不存在，则在 dira 指定目录中安装文件。如果找到了，则发出消息说明文件已存在，并退出而不覆盖它。

- -d 创建目录。缺失的父目录将按照 mkdir -p 的要求创建。如果目录已存在，则将所有者、组和模式设置为命令行上给出的值。

- -f 强制将文件安装到给定目录中，即使文件已存在。如果正在安装的文件不存在，将模式设置为 755并将所有者设置为 bin。如果文件已存在，则模式和所有者为现有文件的属性。

- -g group 将新文件的组 ID 设置为 group。仅对超级用户可用。默认设置为 bin。

- -i 忽略默认目录列表，仅在给定的目录 (dirx...) 中搜索。

- -m mode 将新文件的模式设置为 mode。默认设置为 0755。

- -n dirc 如果在任何搜索的目录中未找到文件，则将其放入 dirc 指定的目录。将新文件的模式设置为 755并将所有者设置为 bin。

# 510

# Intro,

- -O 如果找到了文件，则通过将找到的文件复制到其所在目录下的 OLFILE 中来保存该文件。此选项对于安装经常使用的文件（例如 /bin/sh 或 /lib/saf/ttym）非常有用，因为你无法删除现有文件。

- -S 抑制打印错误消息以外的消息。

- -u user 将新文件的所有者设置为 user。仅对超级用户可用。默认设置为 bin。

# Usage

有关大文件的描述，请参见 largefile(5)。

# Attributes

有关以下属性的描述如下：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNdoc |

# See Also

addbib(1), lookbib(1), refer(1), roffbib(1), sortbib(1), attributes(5)

# install — 安装命令

# Synopsis

```
/usr/sbin/install -c dira [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -f dirb [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -n dir [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -d|-i [-m mode] [-u user] [-g group] [-o] [-s] dir...
/usr/sbin/install [-m mode] [-u user] [-g group] [-o] [-s] file
dirx...
```

# install

# Description

install 命令最常用于 Makefile 中（参见 make(1)），用于将文件安装到特定位置，或在文件系统中创建目录。每个文件都是通过复制到相应的目录来安装的。

install 不使用特殊权限将文件从一个地方复制到另一个地方。其影响如下：

- * 你必须拥有读取要安装文件的权限。
- 你必须拥有复制到目标目录的权限。
- * 如果你想使用 -option 选项，你必须拥有更改文件最终副本的模式的权限。
- * 如果你想通过 -u 或 -g 选项指定安装文件的所有者，你必须是超级用户。如果你不是超级用户，则安装文件的所有者将是你，无论原始文件的所有者是谁。

install 会打印消息，准确你它正在替换或创建什么，以及它们将去何处。

如果你没有指定任何选项或目录 (dirx...)，install 将一组默认目录（/bin,/bin,/etc,/lib,/usr/lib）中搜索与 file 同名的文件。当它找到第一次出现的位置时，install 会发出一条消息，说明它正在用 file 覆盖该文件，并继续操作。如果未找到文件，程序将启动并退出。

如果你在 file 之后指定了一个或多个目录 (dirx...)，则会在默认目录之前搜索这些目录。

# Options

- -c dira 如果 file 不存在，则在 dira 指定目录中安装文件。如果找到了，则发出消息说明文件已存在，并退出而不覆盖它。

- -d 创建目录。缺失的父目录将按照 mkdir -p 的要求创建。如果目录已存在，则将所有者、组和模式设置为命令行上给出的值。

- -f 强制将文件安装到给定目录中，即使文件已存在。如果正在安装的文件不存在，将模式设置为 755并将所有者设置为 bin。如果文件已存在，则模式和所有者为现有文件的属性。

- -g group 将新文件的组 ID 设置为 group。仅对超级用户可用。默认设置为 bin。

- -i 忽略默认目录列表，仅在给定的目录 (dirx...) 中搜索。

- -m mode 将新文件的模式设置为 mode。默认设置为 0755。

- -n dirc 如果在任何搜索的目录中未找到文件，则将其放入 dirc 指定的目录。将新文件的模式设置为 755并将所有者设置为 bin。

# 510

# Intro,

- -O 如果找到了文件，则通过将找到的文件复制到其所在目录下的 OLFILE 中来保存该文件。此选项对于安装经常使用的文件（例如 /bin/sh 或 /lib/saf/ttym）非常有用，因为你无法删除现有文件。

- -S 抑制打印错误消息以外的消息。

- -u user 将新文件的所有者设置为 user。仅对超级用户可用。默认设置为 bin。

# Usage

有关大文件的描述，请参见 largefile(5)。

# Attributes

有关以下属性的描述如下：

| 属性类型 | 属性值 |
| --- | --- |
| 可用性 | SUNdoc |

# See Also

addbib(1), lookbib(1), refer(1), roffbib(1), sortbib(1), attributes(5)

# install — 安装命令

# Synopsis

```
/usr/sbin/install -c dira [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -f dirb [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -n dir [-m mode] [-u user] [-g group] [-o] [-s] file
/usr/sbin/install -d|-i [-m mode] [-u user] [-g group] [-o] [-s] dir...
/usr/sbin/install [-m mode] [-u user] [-g group] [-o] [-s] file
dirx...
```
