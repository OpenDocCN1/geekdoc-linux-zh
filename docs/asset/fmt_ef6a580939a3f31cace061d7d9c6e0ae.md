
不遍历任何符号链接（默认值）

- `--help`

显示此帮助信息并退出

- `--version`

输出版本信息并退出

如果缺失所有者，则保持不变。如果缺失组，则保持不变，但如果由符号 OWNER后的冒号暗示，则将其更改为登录组。OWNER 和 GROUP 可以是数字的也可以是符号的。

## 示例

`chown root /u`

将 `/u` 的所有者改为“root”。

`chown root:staff /u`

同样，但将其组更改为“staff”。

`chown -hR root /u`

将 `/u` 及其子文件的所有者改为“root”。

### 作者

由 David Mackenzie 和 Jim Meyering 编写。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 chown 翻译错误

# 版权

Copyright © 2015 Free Software Foundation, Inc. License GPLv3+: GNU GPL 版本3 或更高版本 <http://gnu.org/licenses/gpl.html>。这是免费软件：你可以自由地更改和分发它。在法律允许的范围内不提供任何保证。

# 另请

`chown(2)`

完整文档位于：<http://www.gnu.org/software/coreutils/chown> 或通过本地可用：info ‘(coreutils) chown invocation'

## 名称

`chronyc` - 用于 `chronyd` 的命令行界面

# 语法摘要

```
chronyc [OPTIONS]
```

### 描述

`chrony` 是一对用于维护计算机时钟准确性的程序。

`chronyc` 是一个命令行界面程序，可用于监控 `chronyd` 的性能并在运行时更改各种运行参数。

# 使用方法

`chronyc` 支持的所有命令的详细说明可以通过发行版随附的文档（`chrony.txt` 和 `chrony.texi`）获取。

### 选项

下方包含了 `chronyc` 支持的选项摘要。

- `-h hostname`

指定主机名（默认 `127.0.0.1`）

- `-p port-number`

指定端口号

- `-n`

显示原始 IP 地址（不尝试查找主机名）

- `-4`

仅将主机名解析为 IPv4 地址

- `-6`

仅将主机名解析为 IPv6 地址

- `-m`

允许在命令行上指定多个命令。每个参数将被整体解释为一条完整的命令。

- `-f conf-file`

此选项可指定配置文件的替代位置（默认 `/etc/chrony.conf`）。`-a` 选项需要配置文件。

- `-a`

使用此选项后，`chronyc` 将在启动时尝试自动身份验证。它将读取配置文件，从密钥文件中读取命令键并运行 `authhash` 和 `password` 命令。

- `command`

指定命令。如果没有给出命令，`chronyc` 将以交互方式读取命令。

# 错误

如需报告错误，请访问 http://chrony.tuxfamily.org

# 另请

`chronyd(8)`

http://chrony.tuxfamily.org/

### 作者

Richard Curnow <rc@rc0.org.uk>

此手册页由 Jan Schaumann <jsuma@netmeister.org> 作为“缺失手册页项目”的一部分编写。请参 http://www.netmeister.org/misc/m2p/index.html 详情。

完整的 `chronyd` 文档以 texinfo 格式提供。

## 名称

`chroot` - 更改根

# 语法摘要

```
chroot [OPTIONS]
```

### 描述

`chroot` 更改命令及其子进程的根目录。

根目录更改指定的目录。如果没有指定，则使用当前根目录。

目录必须是一个目录，且进程对其拥有读取和执行权限。新目录必须是当前根目录的子目录，或者进程拥有 root 权限。

`chroot` 命令更改命令及其子进程的根目录。

## 名称

`chroot` - 更改根

# 语法摘要

```
chroot [OPTIONS] [DIRECTORY]
```

### 描述

`chroot` 更改命令及其子进程的根目录。

根目录更改指定的目录。如果没有指定，则使用当前根目录。

目录必须是一个目录，且进程对其拥有读取和执行权限。新目录必须是当前根目录的子目录，或者进程拥有 root 权限。

### 作者

由 Free Software Foundation 编写。

本手册页文档了 GNU 版本的 `chroot`。`chroot` 更改命令及其子进程的根目录。

# 报告错误

GNU coreutils 在线帮助：<http://www.gnu.org/software/coreutils/> 向 <http://translationproject.org/team/> 报告 `chroot` 翻译错误

# 版权

Copyright ... omitted ...

### 选项

- `--help`

显示此帮助信息并退出

- `--version`

输出版本信息并退出

# 另请

`chroot(2)`

# 用法

默认行为是运行一个新命令：

```
chrt priority command [arguments]
```

你也可以获取现有任务的实时属性：

```
chrt -p pid
```

或者设置这些属性：

```
chrt -r -p priority pid
```

# 权限

用户必须拥有 `CAP_SYS_NICE` 权限才能更改进程的调度属性。任何用户都可以获取调度信息。

# 注意事项

只有 `SCHED_FIFO`、`SCHED_OTHER` 和 `SCHED_RR` 属于 POSIX 1003.1b 进程调度标准。其他调度属性在某些系统上可能会被忽略。

Linux 默认调度策略是 `SCHED_OTHER`。

### 参见

`taskset(1)`, `nice(1)`, `renice(1)`

Linux 调度方案的描述请参见 `sched_setscheduler(2)`。

### 作者

由 Robert M. Love 编写。

# 版版权

Copyright © 2004 Robert M. Love. 本软件为免费软件；请参源代码复制条件。不提供任何保证；即使对于商品性或特定用途的适用性也是如此。

# 可用性

`chrt` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

`chsh` - 更改你的登录 shell

### 概要

```
chsh [-s shell] [-l] [-u] [-v] [username]
```

### 描述

`chsh` 用于更改你的登录 shell。如果命令行上没有提供 shell，`chsh` 会提示输入一个。

如果与 `libuser` 链接，`chsh` 支持非本地条目（kerberos、LDAP 等），否则请使用 `ypchsh, lchsh` 或任何其他用于非本地条目的实现。

### 选项

- `-s`, `--shell shell`

指定你的登录 shell。

- `-l`, `--list-shells`

打印 `/etc/shells` 中列出的 shell 列表并退出。

- `-u`, `--help`

显示帮助文本并退出。

- `-v`, `--version`

显示版本信息并退出。

# 有效 shell

`chsh` 会接受系统上任何可执行文件的完整路径。然而，如果 shell 未在 `/etc/shells` 文件列表中，它将发出警告。另一方面，它也可以配置为仅接受该文件中列出的 shell，除非你是 root 用户。

# 退出状态

操作成功返回 0，如果操作失败或命令语法无效则返回 1。

### 参见

`login(1)`, `passwd(5)`, `shells(5)`

### 作者

Salvatore Valente <svalente@mit.edu>

# 可用性

`chsh` 命令是 `util-linux` 软件包的一部分，可以通过 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

## 名称

`chvt` - 切换前虚拟终端

### 概要

`chvt N`

### 描述

命令 `chvt N` 将 `/dev/ttyN` 设置为前台终端。（如果相应的屏幕不存在，则会创建它。要移除未使用的 VT，请使用 `deallocvt(1)`。组合键 (Ctrl)-左Alt-FN（N 范围为 1-12）通常具有类似的效果。）

`cifscreds` - 在内核密钥环中管理 NTLM 凭据

### 概要
