
过去，LPIC 考试提供两种版本，分别对应 Debian 和 Red Hat。现在你被要求两者都熟悉。概念是相同的，但命令不同。

## “我已经掌握了吗？”测验

“我已经掌握了吗？”测验可以帮助你评估是应该阅读整个章节，还是应该直接跳到“考试准备任务”部分进行复习。如果你不确定，请阅读整个章节。表 3-1 概述了本章的主要标题以及对应的“我已经掌握了吗？”问题。你可以在附录 A“‘我已经掌握了吗？’测验与复习题答案”中找到答案。

| 基础知识点章节 | 该章节涵盖的问题 |
| :--- | :--- |
| Linux 系统中的软件 | 1-2 |
| Debian 软件包管理 | 3-6 |
| RPM 和 YUM 软件包管理 | 7-9 |

表 3-1 “我已经掌握了吗？”基础知识点章节与问题映射

1. `libjpg.so.8.0.3` 可能是一个
   a. 静态库
   b. 共享库
   c. 二进制文件
   d. Shell 脚本

2. 动态链接器称为 ____，并在 ____ 中配置。
   a. `ld.so`, `/etc/ld.so.conf`
   b. `so.linux`, `/etc/ld.so.conf`
   c. `ld.so`, `/etc/so.linux.conf`
   d. `so.linux`, `/etc/so.linux.conf`

3. 你如何安装一个名为 `foo-1.2.3.deb` 的包？
   a. `yum install foo-1.2.3.deb`
   b. `rpm -i foo-1.2.3.deb`
   c. `dpkg --foo-1.2.3.deb`
   d. `apt-get install foo-1.2.3.deb`

4. 你如何查询 Debian 系统以查看是否安装了 `bulldozer` 包？
   a. `dpkg --info bulldozer`
   b. `apt-cache search bulldozer`
   c. `rpm -q bulldozer`
   d. `dpkg --list bulldozer`

5. 在更新远程 Debian 仓库文件列表后，你应该运行：
   a. `dpkg update`
   b. `apt-cache fetch`
   c. `apt-cache update`
   d. `apt-get update`

6. 如果你想安装本地 Debian 包并忽略任何依赖关系错误，你需要做什么？
   a. 无需操作，这是默认设置的。
   b. 添加 `--force-depends` (`dpkg -i pkg.deb --force-conflicts`)
   c. 添加 `--force-conflicts` (`dpkg -i pkg.deb --force-conflicts`)
   d. 添加 `--force-reinstreq` (`dpkg -i pkg.deb --force-reinstreq`)

7. RPM 包的完整名称不包含：
   a. 包名
   b. 版本
   c. 发行版
   d. 架构

8. 要检查 RPM 文件的签名，使用：
   a. `rpm -K`
   b. `rpm -q`
   c. `rpm -sig`
   d. `rpm - *`

9. 你如何检查已安装的包是否存在？
   a. `rpm -V`
   b. `rpm -q`
   c. `rpm -list`
   d. `rpm - *`

## 基础知识点

### Linux 系统中的软件

- 二进制文件
- 库
- 配置
- 数据

典型的软件由以下部分组成：
- 二进制文件
- 库
- 配置
- 数据

大部分需要的是：
- 二进制文件
- 库
- 配置
- 数据

`libcrypt.so.1`
`lrwxrwxrwx 1 root root 16 Sep 27 11:45 libcrypt.so.1 -> libcrypt-2.20.so`

从这个示例中看到，实际的库文件是 `libcrypt-2.20.so`，并且有两个符号链接：`libcrypt.so` 指向 `libcrypt.so.1`，而后者又是指向 `libcrypt-2.20.so` 的链接。这些文件中的每一个都代表一个版本号，取决于是谁或什么在请求，但它们都指向同一个文件。这允许同一系统上存在多个不兼容的共享库版本。应用程序只需要请求它们最初链接时使用的版本即可。

动态加载器会为你处理这种链接工作。它是通过在运行二进制文件时对其查询来实现的。

![](img/16cd7204aa58beaaf530d67f50f15fc5_112_0.png)

#### 确定所需的库

当你找到一个程序并想知道它依赖的库是否存在时，可以运行它并查看哪些部分报错（不安全的方法），或者使用 `ldd` 命令查询程序所需的库：

```
$ ldd /usr/bin/passwd

libc.so.6 => /lib64/libc.so.6 (0x00007fa7a3bae000)
libcrypt.so.1 => /lib64/libcrypt.so.1 (0x00007fa7a3773000)
lib64/ld-linux-x86-64.so (0x00007fa7a55be000)
```

输出告诉你，`password` 命令需要访问 `libc`（C 库，所有应用程序的基础功能集）、`libcrypt` 以及一个命名非常奇特的共享库，该库实际上是动态链接器本身。

#### 在其他地方查找库

某些库文件可能没有足够的头文件信息或内部信息，以至于链接器在库目录中构建链接时无法正确识别它们。

#### 关键知识点

`ldconfig` 程序读取 `/lib` 和 `/usr/lib` 目录下的所有库的头文件，以及 `/etc/ld.so.conf` 文件中注明的任何目录。根据这些头文件和库的文件名，`ldconfig` 为库创建正确的链接。

#### 注意事项

`ld.so.conf` 可能包含一行类似于 `ld.so.conf.d/*.conf` 的内容。在这种情况下，那里指定的文件也会被 `ldconfig` 读取和处理。这种系统允许软件包将库文件放置在它们库所在的位置，而无需编辑共享文件。

`ldconfig` 程序还会构建 `/etc/ld.so.cache` 文件，这是一个二进制文件，存储了系统上库的有序列表。该文件无法作为文本读取，但它被系统链接器 `ld.so` 用作快速引用。

#### 关键知识点

库必须能够被动态链接器访问，或者被添加到名为 `LD_LIBRARY_PATH` 的变量中，该变量包含用冒号（`:`）分隔的库路径。这为动态链接器提供了一个提示，让它去之前位置之外的地方查找。

要设置 `LD_LIBRARY_PATH` 变量，你可以在命令行中声明它：

```
export LD_LIBRARY_PATH=/some/path/name
```

或者，你可以编辑 `/etc/profile` 或 `~/bash_profile` 文件并执行相同的命令。第 11 章，“自定义环境”深入研究了这些文件。

尽管必须如此，`LD_LIBRARY_PATH` 被认为存在安全风险，因为它可能允许未经授权的程序访问系统库或暴露系统库路径。

## Debian 软件包管理

Debian 及其衍生系统（如 Ubuntu）拥有一强大的软件包管理系统，为管理员提供了查找、安装、查询和删除软件包的方法。

软件包管理的基本单元是扩展名为 `.deb` 的文件。这是一个 Debian 软件包：包含了应用程序的默认配置文件、文档、如何安装和删除它的说明，以及该软件包的任何依赖项。

`dpkg` 工具用于操作你系统上的软件包并处理 `.deb` 包。如果你系统中已经有了软件包，可以使用 `--info` 选项查看其内部内容。

高级软件包工具 `APT` 包含系列工具，帮助你在远程服务器上查找并下载软件包，然后使用 `dpkg` 安装它们。

像 `aptitude` 和 `synaptic` 这样的图形和文本界面构建在 APT 之上。它们提供了一个更友好的界面，而不是让你记住这些命令。

![](img/16cd7204aa58beaaf530d67f50f15fc5_114_0.png)

总结一下：本地软件包是 `.deb` 文件，并使用 `dpkg` 安装。APT 处理搜索远程仓库并下载软件包。`aptitude` 等工具提供了一个图形界面。

### 管理本地软件包

`dpkg` 工具操作你系统上的软件包并处理 `.deb` 包。

#### 示例 3-1 查看 deb 内部的内容

```
### dpkg --info acct.6.5.5-1_amd64.deb
package, version 2.0,
size 120424 bytes: archive=1899 bytes,
799 bytes, 4 lines confiles
746 bytes, 18 lines control
1776 bytes, 27 lines mdsums
507 bytes, 30 lines postinst /bin/sh
370 bytes, 26 lines postrm /bin/sh
163 bytes, 7 lines perm
Package: acct
Version: 6.5.5-1
Architecture: amd64
Maintainer: Mathieu Trudel <mathieu@gmail.com>
Installed-Size: 380
Depends: dpkg (>=1.1.4) | libc6 (>=2.3)
Section:
Priority: optional
Homepage: http://www.gnu.org/software/acct/
Description: The GNU Accounting utilities for process
```

软件包的信息包含在 `.deb` 文件中；`dpkg` 命令只是漂亮地显示它。顶部的 `control` 描述了 `dpkg` 使用的文件。文件本身为 104224 字节，内部是总计 1899 字节的控制文件存档：

- **confiles**: 安装后配置软件包的文件列表。与软件包中的其他文件处理方式不同；例如，当软件包删除时它们不会被移除。
- **control**: 包含软件包所有元数据的文件。
- **mdsums**: 文件列表和校验和，以便验证文件在任何时候都没有更改。
- **postinst**: 安装后运行的 shell 脚本。
- **postrm**: 软件包删除后运行的 shell 脚本。
- **prerm**: 在软件包删除之前运行的 shell 脚本。

在 `control` 信息之后，你会看到软件包的各种信息，如名称、版本、其目标硬件以及依赖项。

#### 使用 dpkg 安装软件包

![](img/16cd7204aa58beaaf530d67f50f15fc5_116_0.png)

安装软件包最常用的方法是从当前目录使用命令行以下命令之一：

```
dpkg --install gcc-4.7-base_4.7.2-5_amd64.deb
dpkg -i gcc-4.7-base_4.7.2-5_amd64.deb
```

这返回与以下类似的输出：

```
选择未选择的软件包 gcc-4.7-base:amd64。
读取数据库 ... 当前已安装 142987 个文件和目录。
正在解压 gcc-4.7-base:amd64 (来自 gcc-4.7-base_4.7.2-5_amd64.deb) ...
正在设置 gcc-4.7-base:amd64 (4.7.2-5) ...
```

有时你需要为软件包安装依赖项。要么先安装依赖项，要么在命令行中指定所有必要的软件包。后一种选项的命令如下：

```
dpkg -i gcc-4.7-base_4.7.2-5_amd64.deb libgcc1_4.7.2-5_amd64.deb
```

#### 软件包

当你需要用 `dpkg` 命令删除软件包时，可以使用两种方法之一：移除（remove）或清除（purge）。`-r` 或 `--remove` 选项移除软件包的文件，但将配置文件保留在磁盘上。另一种移除软件包的选项是 `-P` 或 `--purge` 选项，它会移除软件包的所有文件，包括任何配置文件。

要移除软件包但保留其配置文件，请使用以下之一：

```
dpkg --remove package_name
dpkg -r package_name
```

![](img/16cd7204aa58beaaf530d67f50f15fc5_117_0.png)

要清除软件包（包括其配置文件），请使用以下之一：

```
dpkg --purge package_name
dpkg -P package_name
```

当软件包安装时，任何配置文件都会记录在 `confiles` 文件中。这用于确定哪些文件在移除操作中保留，哪些文件在清除操作中也应该被清除。

#### 依赖问题

当你处理软件包时，所需软件包的安装经常会发现与它尝试安装的文件冲突的条目。有时在删除过程中，一个软件包拥有其他软件包所依赖的文件。

考虑到 Debian 稳健且不冗余的特性，使用软件包工具的 `--force` 选项可能会导致你的机器出现不愉快的情况。在删除具有依赖关系的软件包时要非常小心，并详细阅读 `dpkg` 手页中的 `force` 部分。对于考试，你需要知道强制移除数据库中标记为需要重新安装的损坏软件包，使用以下操作：

```bash
dpkg --force-reinstreq packagename
```

`--force-reinstreq` 用于被标记为需要重新安装的软件包，它允许 `dpkg` 移除该软件包。

![](img/16cd7204aa58beaaf530d67f50f15fc5_118_0.png)

此外，你可以在 `--install` 之后使用 `--force-depends` 选项将所有那些糟糕的错误信息转换为严重的警告，但该工具随后允许你执行即将执行的任何不当操作。这是一个示例：

```bash
dpkg --install --force-depends packagename
```

最后，你还可以使用 `--force-remove-essential` 选项。但请注意，覆盖依赖建议可能会导致系统处于损坏状态。

如果你确实必须这样做（通常是根据供应商或附近的 Debian 大师的指示），你可以强制安装软件包，无论与命令和选项产生冲突，如下：

```bash
dpkg --install new_pkg.deb --force-conflicts
```

如果你在强制跳过任何冲突后与该软件包或其他软件包出现问题，请记住你已被警告过。

#### 查询软件包

可以对当前安装的软件包查询大量的信息。特别地，你可以使用 `-l` 或 `--list` 选项列出软件包的存在、版本、名称和描述：

```bash
dpkg --list krb*
dpkg -l krb*
```

你可以使用单个包名（例如用于 Kerberos 相关包的 `krb5-user`），或者使用之前的文件名来查看后续输出所示的列表。

### dpkg --list krb*

Desired=Unknown/Install/Remove/Purge/Hold

| Status=Not/Inst/Conf-files/Unpacked/halfF-conf/Half-inst/trig-AWait| Trig-pend |

| // Err?=(none)/Reinst-required (Status,Err: uppercase=bad) || |

| Name | Version | Architecture | Description |

|---|---|---|---|

| un krb5-desc | <none> | | (no description available) |

| ii krb5-locales | 1.10.1+dfsg-5+d all | Internationalization support for MIT Kerberos | |

| un krb5-user | <none> | | (no description available) |

在一些头部之后，输出显示有三个以 krb5 开头的软件包。其中两个位于字符串 **are uninstalled**（未安装）的行，而 **krb5-locales** 被安装为版本 1.10.1。Debian 软件包系统向你显示之前在系统中安装过的软件包，这与其他系统不同。

你可以通过 **-s 或 --status** 选项检查特定软件包或多个软件包的状态：

```bash
dpkg --status krdc
```

返回的输出是 `--info` 选项的缩略版本。

你可以使用 **-L 或 --listfiles** 选项查看软件包安装的文件：

```bash
dpkg --listfiles coreutils
```

这产生的输出与后续输出所示类似（输出为了适应显示进行了截断）：

```
/.
/bin
/bin/cat
/bin/chgrp
/bin/chmod
/bin/chown
```

使用 `-S` 或 `--search` 选项允许你通过软件包数据库搜索磁盘上的安装文件，例如：

```bash
dpkg -S apt.conf
```

后续输出包含了从数据库条目中找到 apt .conf 文件的各种位置：
