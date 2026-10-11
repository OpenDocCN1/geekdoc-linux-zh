
在`/dev`目录中可能有几百个文件。其中大多数文件在日常活动中没什么用处。作为 Unix 或 Linux 系统的系统管理员，你主要将与代表磁盘驱动器的设备文件打交道。在处理与文件系统相关的命令时，知道硬盘驱动器的路径很重要。本指南第 10 节将更详细地介绍此主题。

> **注意**
>
> `/dev`中使用的*设备命名约定*因各发行版而异。

在`/dev`中还有一些有用的伪设备。伪设备不代表实际的硬件，仅存在于执行特定任务。下表描述了最常用的伪设备。

| 文件 | 用途 |
| :--- | :--- |
| `/dev/zero` | 产生连续 0 字节字符流的文件 |
| `/dev/random` | 随机数生成器 |
| `/dev/null` | 丢弃写入其任何数据的特殊文件 |

## Shell（外壳）

命令行解释器，也称为 shell（外壳），是一个接受用户输入（通常是某种命令）并执行所请求任务的程序。一旦任务完成，该程序将终止并将用户返回到 shell。

Shell 的提示符标识了正在使用的 shell 类型。有两种基本的 shell 提示符类型：
- 普通用户 shell（在某些系统中也可能是 % 或 >）
- 根用户 shell

以下是 `whoami` 命令的输出（第 94 页有讨论），它强调了命令行上普通用户 shell 提示符和根用户 shell 提示符之间的区别。

![](img/fa2f95b64a707c963dfa0445bd9281a7_15_0.png)

普通用户通常对系统的访问权限有限，而根用户拥有不受限制的可访问权限。第 5 节将更详细地介绍此主题。

> **警告**
>
> 在 Unix、Linux 和 BSD 系统上，根用户可以*做任何事情*。知道*你正在以* root 身份工作*很重要，以防止对系统造成意外损坏。

许多系统向 shell 提示符添加自定义信息。这些信息可以是当前用户登录名、系统主机名和当前目录等事物的有用指示符，如下一个示例所示。

![](img/fa2f95b64a707c963dfa0445bd9281a7_15_1.png)

下表描述了在之前示例中显示的自定义 shell 提示符中显示的信息。

| nick | @ | mylaptop | : | /var/log | $ |
| :---: | :---: | :---: | :---: | :---: | :---: |
| 用户名 | 间隔符 | 计算机名 | 间隔符 | 当前目录 | Shell 提示符 |

## Shell 的类型

Unix、Linux 和 BSD 系统有几种不同类型的 shell。每个 shell 都有自己的一套特性和使用语法。下表描述了当前可用的最流行的 shell。

| Shell | 提示符 | 名称 | 备注 |
|---|---|---|---|
| sh | $ | Bourne Shell | 某些 Unix 系统的默认 shell |
| bash | $ | Bourne | Bourne shell 的增强替代版本 |
| zsh | $ | ZSH | Z Shell | 大多数 Linux 和 Mac OS X 系统的默认 shell |
| csh | % | C Shell | 许多 BSD 系统的默认 shell |
| tcsh | > | T C Shell | C shell 的增强替代版本 |
| ksh | $ | Korn shell | AIX 系统的默认 shell |

`bash` shell 是当今最流行的 shell。它是所有 Linux 系统的默认 shell，也可以在大多数 Unix 和 BSD 系统上使用。像 `csh`、`tcsh` 和 `ksh` 等其他 shell 通常被默认用于非 Linux 系统。

## 访问 Shell

当你第一次启动系统时，你会看到一个类似于下面示例图片的登录提示符。

```text
Ubuntu Linux 9.04 
Login: nick 
Password: ****** 
$ 
```

输入你的用户名和密码后，系统将通过 `/etc/passwd` 文件验证你的登录凭据。如果登录信息正确，系统将启动你的 shell（这也是在 `/etc/passwd` 中指定的）。`$` shell 提示符表示你已登录并且“准备就绪”。

*欢迎来到命令行世界……让我们开始吧！*

### 第 2 节：命令行基础

**概述**

本节涵盖每个用户都应知道的最基本命令。这些基本命令涵盖了诸如获取帮助、导航目录和列出文件等主题。在开始之前，你需要了解关于命令行的三条重要规则：
- 1. Unix、Linux 和 BSD 系统对大小写（和空格）敏感。这意味着名为 MyFile 的文件与 myFile 并不相同，这与 DOS 或 Windows 系统上的情况不同。
- 2. 在命令行环境中工作时没有“回收站”或“垃圾箱”。在命令行上删除的文件会立即永久消失。
- 3. 你应该始终在测试系统上练习新命令，而不是在生产环境中使用的系统上。这可以最小化可能导致重要系统故障的事故几率。

了解这些之后，我们现在可以开始使用基本的 Unix、Linux 和 BSD 命令。

> 本书中列出的示例是在各种 Unix、Linux 和 BSD 系统上创建的。许多命令、选项和特性在其他平台上是相同的；然而，可能会存在一些细微差异。你应始终查阅你特定平台的手册以确保与提供的示例兼容。有关如何访问在线手册的更多信息，请参见第 20 页。

#### 本节涵盖的命令：

| 命令 | 用途 |
| :--- | :--- |
| `man` | 命令行程序的在线手册。 |
| `whatis` | 显示指定命令的描述。 |
| `ls` | 列出目录的内容。 |
| `pwd` | 显示当前/工作目录。 |
| `cd` | 更改（导航）目录。 |
| `tree` | 以树形层级格式显示目录的内容。 |
| `find` | 搜索文件和目录。 |
| `locate` | 在 locate 数据库中搜索文件和目录。 |
| `whereis` | 显示指定命令的二进制文件、手册页和源代码的位置。 |
| `file` | 显示指定文件的文件类型。 |
| `stat` | 显示有关文件系统、文件或目录的扩展信息。 |
| `date` | 显示或设置系统时钟。 |
| `cal` | 在命令行上显示日历。 |
| `history` | 显示最近执行过的命令。 |
| `clear` | 清除当前屏幕的内容。 |
| `logout` | 注销系统。 |
| `exit` | 退出当前 shell。 |

### 本部分使用的术语表：

- **参数 (Argument)**：由命令行程序使用的一个或多个可变输入项。
- **二进制文件 (Binary)**：编译后的程序或数据文件。
- **标志 (Flag)**：*选项 (Option)* 的同义词。
- **手册页 (Man Page)**：shell 命令的在线手册。
- **选项 (Option)**：一种修饰符，用于改变命令的默认操作。
- **参数 (Parameter)**：*参数 (Argument)* 的同义词。
- **递归地 (Recursively)**：在执行命令时包含所有子目录。
- **Shell 脚本 (Shell Script)**：在纯文本可执行文件中组合的一组命令。
- **源代码 (Source Code)**：程序的未编译代码。
- **开关 (Switch)**：*选项 (Option)* 的同义词。
- **工作目录 (Working Directory)**：你在目录树中的当前位置。

### man

**用途**：命令行程序的在线手册。

**用法语法**：`man [OPTIONS] [COMMAND/FILE]`

```
$ man ls
LS(1)                          User Commands                          LS(1)

NAME
   ls - list directory contents

SYNOPSIS
   ls [OPTION]... [FILE]...

DESCRIPTION
   List information about the FILEs (the current directory by
   default).  Sort entries alphabetically if none of -cftuvSUX nor
   --sort.

   -a, --all
          do not ignore entries starting with .
   ...

Viewing the manual page for the ls command
```
