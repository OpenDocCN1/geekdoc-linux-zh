
```bash
# rpm -qcsf /bin/bash
normal    /etc/skel/.bash_logout
normal    /etc/skel/.bash_profile
normal    /etc/skel/.bashrc
```

## 列出最近安装的包

要列出最近安装的包，使用带有 `--last` 选项的后续命令。如果你最近安装或升级了许多包发生了某些情况，这非常有用。你可以将查询的输出管道到 `head` 命令，以只显示最后安装的十个，如下所示

```bash
# rpm qa --last | head
comps-8.0.2020910    Sat 05 Oct 2002 01:17:30 PM CDT
tinker-2.2.1-17      Sat 05 Oct 2002 01:16:58 PM CDT
tix-8.2.01-74        Sat 05 Oct 2002 01:16:52 PM CDT
tclx-8.3.74         Sat 05 Oct 2002 01:16:44 PM CDT
python-tools-2.2.1-17  Sat 05 Oct 2002 01:16:41 PM CDT
mx-2.0.3-6           Sat 05 Oct 2002 01:16:34 PM CDT
libxsit-python-1.0.19-1  Sat 05 Oct 2002 01:16:31 PM CDT
librpm-404-devel-4.0.4-8x.27  Sat 05 Oct 2002 01:16:27 PM CDT
itcl-3.2-74          Sat 05 Oct 2002 01:16:12 PM CDT
gnumeric-1.0.9-2      Sat 05 Oct 2002 01:15:46 PM CDT
```

## 创建自定义查询

`-qq` 或 `--queryformat` 选项允许你使用 `rpm` 命令创建自定义查询，尽管这种方式相当困难。你需要传递一个查询字符串，其语法源于 C 语言的 `printf` 函数，需要精确。

### 第 1 部分：RPM 基础

查询格式的基本语法为 `%[tag_name]`。百分比符号是唯一一个源自 C 语言 `printf` 函数的部分。你可以组合标签名称来为每个包显示多个项目。你还可以按照 C 语言的习惯添加格式化选项。

例如，要列出包名，可以使用如下命令：

```
$ rpm -qa --qf "%NAME"
redhat-menuslibcracklibgbdgnmppplibbac11libjbpeglinccpreshadow-utilslibermcapfreetypefileutilspsmscntmpointcountracklib-dictskrb5-libscyrus-slausmodermoxftkliblibbonalibobopthonptpytk2pxfb86configuredredhat-config-usreaders-config-keyboardprd4-python-vsf21bonuemashbind-untillibscyrus-sasi-plindosunixethootingerfrautfofasksb8configlesslibtool-libockdevmallcapMAKEDousemnconfetpentsysobipartedpppppssutilsrdsaterhnlibrpmmrshsetuptostatstatierartillopocclutistimeconfiguznerpcmcia-cnronxfree86
```

此命令使用了最简单的格式，仅包头中标签的值；在这种情况下是包名。由于我们没有使用其他格式，此命令将所有包名连在一起输出。为了解决输出中的这个问题，你可以在格式字符串的末尾放置 `\n`。这显著改进了输出结果。

例如，仅显示前几个条目：

```
# rpm -qa --qf "%NAME
"
redhat-menus
glib
cracklib
gdbm
gmp
libacl
libjpeg
linc
pcre
shadow-utils
libtermcap
freetype
info
fileutils
psmisc
tnp
mount
cracklib-dicts
krb5-libs
cyrus-sasl
usermode
Xft
```

此命令提供了一个自定义查询，其本质与 `rpm-qa` 命令相同。你可能倾向于使用更简单的 `rpm` 选项而不是使用此命令，但你可以将此示例作为创建自定义查询的指南。

![](img/9d29d6681c5f42792ea5da4b12142ca2_106_0.png)

`rpm` 命令的许多命令行选项都被定义为 opt 别名。这些 opt 别名在较长的查询格式字符串中定义了 `rpm` 命令行选项。有关 `popt` 的更多信息请参阅第 21 章。

你可以向查询字符串中添加项目，并使用 C 语言的约定来控制每个项目输出的 own。例如，以下命令打印所有包的名称和平台，显示前几个条目，每个条目的格式化为 20 个字符：

```
rpm -qa "-%20(NAME)-%20(PLATFORM)\n"
redhat-menus
noarch-redhat-linux-gnu
glibc
1386-redhat-linux-gnu
ccracklib
1386-redhat-linux-gnu
gdbm
1386-redhat-linux-gnu
gmp
1386-redhat-linux-gnu
libacl
1386-redhat-linux-gnu
libjpeg
1386-redhat-linux-gnu
linc
1386-redhat-linux-gnu
pcre
1386-redhat-linux-gnu
shadow-utils
1386-redhat-linux-gnu
libtermcap
1386-redhat-linux-gnu
freetype
1386-redhat-linux-gnu
info
1386-redhat-linux-gnu
fileutils
1386-redhat-linux-gnu
psmic
1386-redhat-linux-gnu
tp
1386-redhat-linux-gnu
mount
1386-redhat-linux-gnu
cracklib-dicts
1386-redhat-linux-gnu
krb5-libs
1386-redhat-linux-gnu
cyrus-sasl
1386-redhat-linux-gnu
usermode
1386-redhat-linux-gnu
Xft
1386-redhat-linux-gnu
```

## 使用查询格式标签

为了使用 `--queryformat` 选项构建查询，你需要知道可以使用哪些标签。要列出可用查询格式标签的名称，请使用 `--querytags` 选项，它会返回大量标签，此处为了空间考虑进行了截断：

```
# rpm --querytags
NAME
VERSION
RELEASE
SUMMARY
DESCRIPTION
BUILDTIME
```

这些标签中的每一个都有一个带有 `RPMTAG_` 前缀的版本，例如 `RPMTAG_NAME`。你可以带上或不带 `RPMTAG_` 前缀使用这些标签。例如：

```
$ rpm -q -f "%{RPMTAG_NAME}\n" sendmail
```

注意此命令如何使用 `-q` 选项查询单个包，而不是 `-qa` 查询所有包。你可以在任何 `rpm` 查询中使用查询格式。接下来的章节将根据标签中存储的信息的类型介绍可用的标签。

## 查询包信息

许多查询格式标签引用存储在头部的包信息数据，这些数据在第 3 章中介绍。表 5-3 列出了包信息标签。

表 5-3 包信息标签

| 标签 (Tag) | 包含内容 (Holds) |

| :--- | :--- |

| NAME | 包名 |

| VERSION | 版本号 |

| RELEASE | 发布版本号 |

| SUMMARY | 包的一行摘要 |

| DESCRIPTION | 关于包的描述性文本 |

| BUILDTIME | 包构建的时间 |

| BUILDHOST | 构建包的主机 |

| 标签 (Tag) | 包含内容 (Holds) |

| :--- | :--- |

| SIZE | 负载中所有普通文件的大小 |

| LICENSE | 包发布的许可协议 |

| GROUP | 包的描述性组或类别名称 |

| OS | 构建包的操作系统 |

| ARCH | 架构，例如 i386 |

| SOURCE | 的源码 |

| CHANGELOGTIME | 变更日志时间数组 |

| CHANGENAME | 变更日志名称数组 |

| CHANGELOGTEXT | 变更日志条目数组 |

| PREIN | 安装前脚本 |

| POSTIN | 安装后脚本 |
