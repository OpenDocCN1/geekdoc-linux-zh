
当 `TYPE` 为 `b`、`c` 或 `u` 时，必须指定 `MAJOR` 和 `MINOR`，当 `TYPE` 为 `p` 时，必须省略。如果 `MAJOR` 或 `MINOR` 以 `0x` 或 `0X` 开头，则被解释为十六进制；否则，如果以 `0` 开头，则解释为八进制；否则，为十进制。`TYPE` 可以：

+ `b`
创建一个块（缓冲）特殊文件
+ `c`, `u`
创建一个字符（非缓冲）特殊文件
+ `p`
创建一个 FIFO

注意：你的 shell 可能有自己的 `mknod` 版本，它通常会取代此处描述的版本。请参阅你的 shell 文档获取关于其支持的选项详情。

## 作者

由 David MacKenzie 编写。

# 报告缺陷

GNU coreutils 在线帮助：<> 向 <> 报告 `mknod` 翻译缺陷

## 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 版本 3 或更高版本 <->。这是一个免费软件：你可以自由地更改和重新发行它。在法律允许的范围内不提供任何保证。

# 另见

(2)

完整文档位于：<> 或通过本地直接可用：info ‘(coreutils) mknod invocation’

# mlabel

## 名称

`mlabel` - 创建 MSDOS 卷标

# 末尾警告

本手册页由 mtools 的 texinfo 文档自动生成，可能不完全准确或完整。请参阅此手册页末尾获取详情。

## 描述

`mlabel` 命令为磁盘添加卷标。其语法为：`mlabel [-vcsn] [-N serial] drive:[new_label]`

如果存在，`mlabel` 会显示当前卷标。如果未给出 `new_label`，且未设置 `c` 或 `s` 选项，则会提示用户输入新卷标。要删除现有卷标，请在提示处按回车键。

标签限制为 11 个单字节字符，例如 `Name1234567`。

确保标签有效的合理考虑包括：

+ `-c`
清除标签
+ `-s`
显示现有标签
+ `-n`
分配新标签
+ `-v`
详细输出
+ `-N`
设置序列号

`Mlabel` 仅在 Linux 上可用，因为它仅在 Linux 上有用。

## 另请

Mtools 的 texinfo 文档

# 查看 mtools 的 texinfo 文档

本手册页由 mtools 的 texinfo 文档自动生成。然而，此过程只是近似的，某些项目如交叉引用、脚注和索引在翻译过程中丢失了。事实上，这些项目在手册页格式中没有适当表示。此外，并不是所有信息都已转换为手册页版本。因此，我强烈建议你使用原始的 texinfo 文档。请参阅此手册页末尾查看 texinfo 文档的说明。

+ 要从 texinfo 文档生成打印副本，请运行以下命令：
```
./configure; make dvi; dvips mtools.dvi
```
+ 要生成 html 副本，运行：`./configure; make html`
可以在 ∞ 找到预制好的 html
+ 要生成 info 副本（可以使用 emacs 的 info 模式浏览），运行：`./configure; make info`

texinfo 文档在打印或作为 html 时看起来最美观。事实上，在 info 版本中，由于 info 的引用约定，某些示例难以阅读。

# mmd

## 名称

`mmd` - 创建 MSDOS 子目录

# 末尾警告

本手册页由 mtools 的 texinfo 文档自动生成，可能不完全准确或完整。请参阅此手册页末尾获取详情。

## 描述

`mmd` 命令用于在 MS-DOS 文件系统中创建目录。其语法为：

```
mmd [-d] msdosdirectory [ ]
```

`mmd` 在 MS-DOS 文件系统上创建一个目录。如果目录已存在，则发生错误。

## 另请

Mtools 的 texinfo 文档

# 查看 texinfo 文档

本手册页由 mtools 的 texinfo 文档自动生成。然而，此过程只是近似的，某些项目如交叉引用、脚注和索引在翻译过程中丢失了。事实上，这些项目在手册页格式中没有适当表示。此外，并不是所有信息都已转换为手册页版本。因此，我强烈建议你使用原始的 texinfo 文档。请参阅此手册页末尾查看 texinfo 文档的说明。

+ 要从 texinfo 文档生成打印副本，请运行以下命令：
```
./configure; make dvi; dvips mtools.dvi
```
+ 要生成 html 副本，运行：`./configure; make html`
可以在 ∞ 找到预制好的 html
+ 要生成 info 副本（可以使用 emacs 的 info 模式浏览），运行：`./configure; make info`

texinfo 文档在打印或作为 html 时看起来最美观。事实上，在 info 版本中，由于 info 的引用约定，某些示例难以阅读。

# mmount

## 名称

`mmount` - 挂载 MSDOS 磁盘

# 末尾警告

本手册页由 mtools 的 texinfo 文档自动生成，可能不完全准确或完整。请参阅此手册页末尾获取详情。

## 描述

`mmount` 命令用于挂载 MS-DOS 磁盘。它仅在 Linux 上可用，因为只有当内核允许配置磁盘几何结构时它才有用。其语法为：

```
mmount msdosdrive [mountargs]
```

`Mmount` 读取 MS-DOS 磁盘的引导扇区，配置驱动器几何结构，最后通过传递 `mountargs` 给 `mount` 进行挂载。如果没有指定挂载参数，则使用设备名称。如果磁盘被写保护，则将自动以只读模式挂载。

## 另参见

Mtools 的 texinfo 文档

## 查看 TEXINFO 文档

此帮助页（manpage）由 mtools 的 texinfo 文档自动生成。然而，此过程是粗略的，某些项目（如交叉引用、脚注和索引）在转译过程中丢失了。事实上，这些项目在帮助页格式中没有适当的表示方式。此外，并非所有信息都已翻译帮助页版本。因此，我强烈建议您使用原始的 texinfo 文档。请参见此帮助页末尾关于如何查看 texinfo 文档的说明。

+ 若要从 texinfo 文档生成可打印副本，请运行以下命令：
```
./configure; make dvi; dvips mtools.dvi
```
+ 若要生成 html 副本，请运行：`./configure; make html`
可以在 ∞ 处找到预制的 html 副本。
+ 若要生成 info 副本（可以使用 emacs 的 info 模式进行浏览），请运行：`./configure; make info`

texinfo 文档在打印或作为 html 显示时看起来最漂亮。事实上，在 info 版本中，由于 info 的引用约定，某些示例难以阅读。

## mmove

### 名称

`mmove` - 移动或重命名 MSDOS 文件或子目录

## 警告事项

此帮助页由 mtools 的 texinfo 文档自动生成，可能并不完全准确或完整。详见此帮助页末尾。

## 描述

`mmove` 命令用于移动或重命名现有的 MS-DOS 文件或子目录。

```
mmove [-v] [-D clash_option] sourcefile targetfile
mmove [-v] [-D clash_option] sourcefile [source...] targetdirectory
```

`mmove` 移动或重命名现有 MS-DOS 文件或子目录。与 MS-DOS 版本的 move 不同，`mmove` 能够移动子目录。文件或目录只能在一个文件系统内移动。数据无法从 MS-DOS 移动到 Unix 或反之亦然。如果省略了目标文件或目录的驱动器号，则假设与源文件相同的字母号。如果省略了所有参数中的驱动器号，默认假设驱动器 `a:`。

## 另参见

Mtools 的 texinfo 文档

## 查看 TEXINFO 文档

此帮助页由 mtools 的 texinfo 文档自动生成。然而，此过程是粗略的，某些项目（如交叉引用、脚注和索引）在转译过程中丢失了。事实上，这些项目在帮助页格式中没有适当的表示方式。此外，并非所有信息都已翻译帮助页版本。因此，我强烈建议您使用原始的 texinfo 文档。请参见此帮助页末尾关于如何查看 texinfo 文档的说明。

+ 若要从 texinfo 文档生成可打印副本，请运行以下命令：`./configure; make dvi; dvips mtools.dvi`
+ 若要生成 html 副本，请运行：`./configure; make html`
可以在 ∞ 处找到预制的 html 副本。
+ 若要生成 info 副本（可以使用 emacs 的 info 模式进行浏览），请运行：`./configure; make info`

texinfo 文档在打印或作为 html 显示时看起来最漂亮。事实上，在 info 版本中，由于 info 的引用约定，某些示例难以阅读。

## MODULE

### 名称

`module` - Modules 软件包的命令接口

## 语法概要

```
module [ switches ] [ sub-command ] [ sub-command-args ]
```

## 描述

`module` 是 Modules 软件包的用户界面。Modules 软件包通过 `modulefile`（模块文件）动态修改用户的环境。

每个 `modulefile` 包含配置应用程序 shell 所需的信息。一旦 Modules 软件包初始化，就可以使用解释 `modulefile` 的 `module` 命令基于模块来修改环境。通常，`modulefile` 指令 `module` 命令更改或设置 shell 环境变量，如 `PATH`、`MANPATH` 等。`modulefile` 可以由系统上的多个用户共享，用户也可以拥有自己的集合来补充或替换共享的 `modulefile`。

用户可以向当前环境添加或从当前环境中移除 `modulefile`。`module` 中包含的环境变化也可以通过 `module` 命令进行总结。如果没有给出任何参数，将显示 `module` 的用法和子命令的摘要。

`module` 命令执行的操作由子命令及其相关参数描述。

### 软件包初始化

当特定 shell 的初始化脚本被加载（source）到 shell 时，Modules 软件包和 `module` 命令会被初始化。该脚本创建 `module` 命令（作为别名或 shell 函数），创建 Modules 环境变量，并且如果启用了该功能，则会将环境快照保存为（如果 `BEGINENV=1`）`$MODULESBEGINENV` 指向的任何内容。

`module` 别名或函数执行 `modulecmd` 程序，由 shell 解析该命令的输出。`modulecmd` 的第一个参数指定 shell 的类型。

初始化脚本保留在 `$MODULEHOME/init/<shell>`，其中 `<shell>` 是被加载 shell 的名称。`modulecmd` 支持 `sh`, `csh`, `tsh`, `bash`, `ksh` 和 `zsh`。此外，支持 `python`、`perl` 和 `cmake` “shell”，它们会将环境变化以 `python`、`perl` 或 `cmake` 代码的形式写入标准输出（stdout）。

`perl` `module` 命令的设置如下：

```
uselib${'MODULEHOME'}."/init";perl;
```

而 `python` `module` 命令定义为：

```
import os,sys;
```

### Modulecmd 设置

`module` 别名或函数执行 `modulecmd` 程序，由 shell 解析该命令的输出。`modulecmd` 的第一个参数指定 shell 的类型。

初始化脚本保留在 `$MODULEHOME/init/<shell>`，其中 `<shell>` 是被加载 shell 的名称。`modulecmd` 支持 `sh`, `csh`, `tsh`, `bash`, `ksh` 和 `zsh`。此外，支持 `python`、`perl` 和 `cmake` “shell”，它们会将环境变化以 `python`、`perl` 或 `cmake` 代码的形式写入标准输出。

`perl` `module` 命令的设置如下：

```
uselib${'MODULEHOME'}."/init";perl;
```

而 `python` `module` 命令定义为：

```
import os,sys;
```

初始化脚本保留在 `$MODULEHOME/init/<shell>`，其中 `<shell>` 是被加载 shell 的名称。`sh`, `csh`, `tsh`, `bash`, `ksh` 和 `zsh` 被 `modulecmd` 支持。此外，支持 `python`、`perl` 和 `cmake` “shell”，它们会将环境变化以 `python`、`perl` 或 `cmake` 代码的形式写入标准输出。

`perl` `module` 命令的设置如下：

```
uselib${'MODULEHOME'}."/init";perl;
```

而 `python` `module` 命令定义为：

```
import os,sys;
```

### 命令开关

- `-userlvl <lvl>`, `-u <lvl>`: 将用户级别设置为指定的值。参数可以是以下之一：`novice`, `expert`, `advanced`。

`clear`
强制 Modules 包认为当前没有加载任何模块。

`purge`
卸载所有已加载的模块文件（modulefiles）。

`refresh`
