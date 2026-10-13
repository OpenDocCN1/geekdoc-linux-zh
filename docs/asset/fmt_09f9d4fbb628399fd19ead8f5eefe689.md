
# 第 23 章：安装和升级软件包

查询功能用于获取有关已安装软件的大量信息。软件包维护实现了包的安装、删除和升级。软件包验证使系统管理员能够将通过 `rpm` 安装的文件当前状态与从原始包获取的信息进行比较。软件包构建模式用于从源代码构建或重新构建 RPM。最后，管理模式和杂项模式影响的是 RPM 本身，而不是软件包。它们被用于修复可能的数据库损坏，并确定 RPM 的通用配置。

## 通用选项

在命令行中，主要的 RPM 命令是 `rpm`。除了后续章节讨论的特定模式的命令行选项外，`rpm` 接受接受表 23-1 中列出的通用命令行选项。

表 23-1 通用 RPM 命令行选项

| 选项 | 描述 |
| --- | --- |
| - v | 显示 RPM 操作状态的基本信息。 |
| - vv | 显示调试信息。对软件打包人员和 RPM 开发人员最有用。 |
| --quiet | 仅显示错误信息。 |
| --help | 显示用法摘要。 |

| 选项 | 描述 |
|---|---|
| --version | 显示 RPM 版本号。 |
| --justdb | 仅更新数据库，不更新文件系统。 |

在排查失败的软件包安装或删除时，`-vv` 选项可能非常有用，但要准备好从大量且通常看起来晦涩的输出中进行筛选，以找到你需要的信息。`justdb` 会导致 RPM 执行一种干运行（dry-run）操作。任何操作（如安装或删除 RPM）的结果只会影响 RPM 的数据库；不会在文件系统中添加或删除文件。例如，以下命令使用 `justdb` 从 RPM 数据库中删除 `whois` 包，而不会实际删除文件：

```
# rpm -e whois
# rpm -q whois
package whois is not installed
# ls -l /usr/bin/whois
-rwxr-xr-x 1 root root 7996 Feb 16 08:47 /usr/bin/whois
```

第二个命令使用 `-q`（query）选项来查看 `whois` RPM 是否已安装。如输出所示，它不在数据库中。但 `ls` 命令显示 `whois` 实际上仍然已安装。只有 RPM 数据库发生了变化，文件系统没有。

> RPM 命令支持的选项比表 23-1 中列出的更多。为了简化讨论，本章仅讨论最常用且实用的选项。

`--justdb` 的一个常见用途是在使用非 RPM 源（如 tar 包）升级软件包后，从数据库中移除该包条目。在这种情况下，RPM 条目是无效的，需要在不删除已安装文件的情况下将其移除。

## 查询模式

RPM 的查询模式是其最强大、实用的功能之一。RPM 查询的通用形式为：

```
rpm -q [queryoptions]
```

`-q`（或如果你更喜欢用 `--query`）指定查询操作，而 `queryoptions` 是要查询的内容、查询类型、运行方式或输出格式。

然而，最常用的查询使用以下通用语法：

```
rpm -q [queryoptions] package [...]
```

`query` 指定要查询的 RPM。使用用空格分隔的包名列表查询多个 RPM。查询模式的威力是以复杂的 `queryoptions` 列表为代价的。`queryoptions` 分为两类：一组控制要查询的软件包，另一个定义要显示的信息。表 23-2 列出了查询模式中许多但并非所有的选项。`Type` 列使用 `S` 表示软件包，`I` 表示信息。除非另有说明，所有选项都需要包名作为参数。

### 表 23-2 查询选项

| 选项 | 类型 | 描述 |
| ------|---|---|
| -a | S | 查询所有。 |
| --requires | S | 查询所需的项。 |
| --whatprovides | S | 查询提供的项。 |
| -f | S | 查询指定文件。 |
| -g | S | 查询组。 |
| -p | S | 查询包。 |
| -i | I | 显示关于 RPM 的信息。 |
| -R | I | 查询依赖。 |
| --provides | I | 查询所有提供的。 |
| --changelog | I | 显示 RPM 的日志。 |
| --querytags | I | 打印已知标签。 |
| -qformat | I | 创建自定义格式。 |

正如表 23-2 所示，RPM 的查询模式非常扩展且灵活，允许获取任何类型的信息。通过 `--qf` 选项，你可以创建自定义输出。后续章节将演示如何使用这些选项。然而，某些选项需要额外的说明。使用 `-f` 时，必须是完整路径。

### 查询依赖

`--provides`、`-R`、`--requires` 和 `--whatprovides` 允许你识别软件包之间的依赖关系。能力参数表示依赖本身，通常是另一个 RPM 名称或特定文件名。要确定 RPM 依赖于哪些能力，使用 `--requires capability` 列出所有需要能力的包。例如，以下命令显示了所有需要 RPM 能力的包：

```bash
$ rpm q --requires rpm
gawk
fileutils
textutils
mktemp
popt
glibc >= 2.92
dbl = 85
/bin/sn
```

示例输出被截断了。如输出所示，RPM 包需要 `gawk` 能力以及大于等于 `2.92` 的 `glibc` 能力。在这种情况下，`gawk` 能力另一个 RPM，而 `glibc` 能力识别了最小版本。要识别软件包提供了哪些能力，使用 `--provides` 选项：

```
$ rpm -q --provides rpm
librpm.so.0
librpmbuild.so.0
librpm.so.0
rpm = 4.0.2-8
```

前三行显示 RPM 提供了能力（在这种情况下是文件名）`librpm.so.0`、`librpmbuild.so.0` 和 `librpm.so.0`。最后一行显示了 rpm 包本身的版本号，并表明 RPM 是它自身的一种能力。

命令输出显示了 6 个需要 RPM 能力的包，其中两个你可能不会怀疑它们需要该能力的包：rhn_register 和 update。

因此，在删除 RPM 软件包之前，你必须先删除依赖于该包的 6 个包。

查询 RPM 依赖信息的选项为系统管理员提供了宝贵信息，涵盖了构成已安装的 Red Hat Linux 系统的许多 RPM 软件包之间的关系。

#### 此 RPM 包含什么内容？

自然地，查找一个 RPM 的内容（无论是否已安装）通常是有用的，甚至是必要的。表 23-2 中列出的许多选项使得这成为可能。这些可能性范围从简单地显示包名和版本号，到关于 RPM 安装中每个文件的详细信息不等。你可以使用 -a 选项列出所有已安装的 RPM。不过，大多数查询处于这两个极端情况之间，查询有限的包子集或有限选择的包特性或文件。

最简单的查询 -q 只显示 RPM 的名称和版本号，如下命令所示。

```
$ rpm -q whos
whois 1.0.6 1
```

如果你想要更多更多描述性的信息，请添加 -i：

```
$ rpm -qi whos
Name : whos               Relocations: (not relocateable)
Version : 1.0.6             Vendor: Red Hat, Inc.
Release : 1                Build Date: Fri 16 Feb 2001
Install date: Thu 24 May 2001  Build Host: porky.devel.redhat.com
Group : Applications/Internet  Source RPM: whos-1.0.6-1.src.rpm
Size : 38187               License: LGPL
Packager : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary : Internet whos/nicclient.
Description:
A whos client that accepts both traditional and finger-style queries.
```
