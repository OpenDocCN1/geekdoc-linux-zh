
然而，观察到跨模块的界面使用的字体类型没有一致性。此外，根据项目要求，团队应该仅使用 Font Experts Ltd. 提供的字体。

为了确保团队在软件界面设计中使用字体时保持一致性，Sulekha 决定配置一个中央字体服务器，该服务器所有参与该项目的团队都可以访问。

## 练习答案

为了在团队之间保持相似字体使用的一致性，Sulekha 需要执行以下任务：

- 1. 配置字体服务器
- 2. 在每个 X 客户端编辑 `/etc/X11/XF86Config` 文件
- 3. 停止 `xfs` 服务
- 4. 在每个 X 客户端验证新添加字体

### 1. 配置字体服务器

要配置中央字体服务器，请执行以下步骤：

a. 在服务器上使用以下命令通过任何文本编辑器打开文件 `/etc/X11/fs/config`：

```
# vi /etc/X11/fs/config .
```

b. 确保计算机已配置为监听 tcp 端口。在 `/etc/X11/fs/config` 文件中找到 `no-listen = tcp`。在 `no-listen = tcp` 行之前插入 `#` 字符，并将行包含在代码中。

c. 在 `/etc/X11/fs/config` 文件的 `no-listen = tcp` 行下方添加行 `port = 7100`，并保存文件。

d. 执行以下命令，如果不存在，则创建目录 `/usr/share/fonts/local`：

```
# mkdir /usr/share/fonts/local .
```

e. 从 NFS 服务器的 `/home/fonts(NFS Share)` 目录执行以下命令，将 Blue Moon Computers 使用的字体复制到字体服务器的 `/usr/share/fonts/local` 目录：

```bash
# scp 192.168.0.53:/home/fonts/* /usr/share/fonts/local
```

从 NFS 共享目录复制字体的 sc 命令语法为：

```bash
# scp <NFS 服务器的IP 地址>:<字体目录路径 /usr/share/fonts/local
```

f. 执行以下命令进入 `/usr/share/fonts/local` 目录：

```bash
# cd /usr/share/fonts/local
```

g. 执行以下命令更新系统的字体信息：

```bash
# mkfontdir > fonts.scale
# mkfontdir
```

h. 执行以下命令将目录 `/usr/share/fonts/local/` 作为根目录添加到 Xfs 字体路径中：

```bash
# chfontpath -a /usr/share/fonts/local/
```

i. 执行以下命令重启 X 字体服务器，以便新的数据库软件可以使用新字体：

```bash
# service xfs reload
```

j. 执行以下命令验证新字体目录路径是否成功已到计算机：

```bash
# chfontpath - list
```

### 2. 在每个 X 客户端编辑 `/etc/X11/xF86Config` 文件

执行以下步骤编辑 `/etc/X11/xF86Config` 文件：

a. 要指定字体服务器的 IP 地址，请编辑文件 `/etc/X11/xF86Config`。使用以下命令通过 `vi` 编辑器打开文件：

```bash
# vi /etc/X11/xF86Config
```

b. 在 `/etc/X11/XF86Config` 文件中找到行 `FontPath "unix:/7100"`。将识别出的行替换为以下行：

```bash
FontPath "tcp/192.168.0.1:7100"
```

在前一行中，`tcp` 是用于访问 X 字体服务的协议。`192.168.0.1` 是字体服务器的 IP 地址，`7100` 是端口号。

c. 保存文件更改并退出编辑器。

### 3. 停止 `xfs` 服务

停止 X 客户端上的 `xfs` 服务，以免运行在它们上的 X 客户端应用程序尝试从本地计算机获取字体，而是重定向到 X 字体服务器获取字体。要停止正在运行的 `xfs` 服务，执行以下命令：

```bash
# service xfs stop
```

要在启动时停止 `xfs` 服务，执行以下命令：

```bash
# chkconfig --level 5 xfs off
```

停止 `xfs` 服务后，重启计算机以使用字体服务器服务。

### 4. 在每个 X 客户端验证新添加的字体

执行以下步骤在 X 客户端验证新添加的字体：

- a. 从终端运行以下命令打开 `xfontsel` 窗口：

```bash
# xfontsel
```

- b. 选择 `fmly` 菜单以查看并验证字体是否已添加到字体服务器。

## 使用 Shell 和编辑器工作

### 描述 Shell 的类型

UNIX 和 Linux 提供了多种 Shell。UNIX 中最流行的 Shell 有：

- Bourne shell (波恩壳)
- C shell (C 壳)
- Korn shell (K 壳)

### Bourne Shell

Bourne shell 是在 AT&T 开发的原始命令处理器，以其开发者 Stephen R. Bourne 命名。该 shell 随 UNIX 正式发行。Bourne shell 是最快的命令处理器，也是被广泛使用的 shell。Bourne shell 的可执行文件名为 `sh`，安装为 `/bin/sh`。

### C Shell

C shell 是由 William Joy 等人在加州大学伯克利利分校开发的另一个命令处理器。它的名字源于其编程语言，该语言的语法类似于 C 语言。它与 Bourne shell 不兼容。C shell 的开发目的是提供一种类似于 C 语言的编程接口。然而，它并不适合编写 shell 脚本。C shell 之流行是因为它是首批引入命令历史功能的 shell 之一。C shell 的可执行文件名为 `csh`。

### Korn Shell

Korn shell 由 David Korn 开发，是 AT&T 的产物。它结合了 C shell 和 Bourne shell 的优秀特性。Korn shell 的可执行文件名为 `ksh`。

Bourne、C 和 Korn shell 在 Linux 中也可用。Linux 中提供的其他 shell 是通过增强 UNIX 中使用的 shell 的功能而开发的。Linux 中最流行的 shell 有：

- Bash
- Tcsh
- ASH

### Bash

Bash 是“Bourne Again Shell”的缩写。它是 Bourne shell 的增强版，也是大多数 Linux 计算机的默认 shell。Bash 能够存储你使用过的命令历史。Bash 是自由软件基金会提供的 GNU 项目产品。GNU 项目由一组创建和分发软件的程序员组成。Bash 还可以存储以前会话的命令。

### Tcsh

Tcsh 代表 Tom’s C shell，也称为 TC shell。它是 C shell 的增强版。Linux 上 shell 可用的符号链接是 `csh`。你可以在 shell 提示符处输入 `tcsh` 来执行 Tcsh shell。C shell 和 Tcsh 与 Bourne shell 不兼容。

### ASH

A Shell (`ash`) 由伯克利大学的 Kenneth Alquist 开发。这是一个轻量级的 Bourne shell，通常适用于内存有限的计算机。Linux 和 UNIX 可用的其他 shell 有 bash, login, esh, fsh, zsh, ksh, ish, psh, rc, sash。下表比较了某些 shell 提供的功能：

### 表 5-1 Shell 比较

| 特性 | Bourne | Korn | C | Tcsh |
| :--- | :--- | :--- | :--- | :--- |
| 后台处理 | 是 | 是 | 是 | 是 |
| 命令历史 | 否 | 是 | 是 | 是 |
| I/O 重定向 | 是 | 是 | 是 | 是 |
| Shell 脚本 | 是 | 是 | 是 | 是 |
| 命令别名 | 否 | 是 | 是 | 是 |
| 文件名补全 | 否 | 是 | 否 | 是 |
| 命令补全 | 否 | 否 | 否 | 是 |
| 命令编辑 | 否 | 是 | 否 | 是 |
| 作业控制 | 否 | 是 | 是 | 是 |

## 使用 Shell 和编辑器

所有上述 shell 提供一些常用功能，如变量、通配符和 I/O 重定向。

你可以通过查看文件 `/etc/shells` 查看安装的 shell。

## 处理 Shell 变量
