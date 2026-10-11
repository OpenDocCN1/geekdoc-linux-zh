
GNU/Linux 系统中包含的程序是自由软件；每个程序的发行条款在 `/user/share/doc/*/copyright` 中的各个文件中进行了描述。

在适用法律允许的范围内，Kali GNU/Linux **绝不提供任何保证**。

root@kali-rolling:-

处理你的输入并执行你的命令的程序称为 shell（或命令解释器）。Kali Linux 的默认 shell 是 `Bash`（它代表 Bourne Again SHELL，即“布恩再次加强版 shell”）。末尾的 `$` 或 `#` 字符表示 shell 正在等待你的输入。它还表示 `Bash` 是否将你识别为普通用户（带 `$` 的前者）或超级用户（带 `#` 的后者）。

## 3.2.2. 命令行基础：浏览目录树和管理文件

本节仅对涵盖的命令进行简要概述，所有命令都有许多此处未描述的选项，请参考其各自手册中提供的丰富文档。在渗透测试中，在成功利用漏洞后，你通常会获得该系统的 shell 访问。精通命令行对于你作为安全专业人员的成功至关重要。

一旦会话打开，`pwd` 命令（代表 print working directory）显示你在文件系统中的当前位置。使用 `cd` 目录命令（`cd` 代表 change directory）更改当前目录。当你没有指定目标目录时，你会被带回到主目录。当你执行 `cd -` 时，你会回到上一个工作目录（上一次 `cd` 调用之前的目录）。父目录始终是 `..`（两个点），而当前目录也被称为 `.`（点）。`ls` 命令允许列出目录的内容。如果你不提供参数，`ls` 将对当前目录操作。

```
$ pwd
/home/buxy
$ cd Desktop
$ pwd
/home/buxy/Desktop
$ cd
$ pwd
/home/buxy/Desktop
$ cd ..
$ pwd
/home/buxy
$ ls
Desktop Downloads Pictures Templates
Documents Music Public Videos
```

你可以使用 `mkdir directory` 创建目录，并使用 `rmdir directory` 删除现有（空）目录。`mv` 命令允许移动和重命名文件及目录；移动文件通过 `rm file` 实现，复制文件则通过 `cp source-file target` 完成。

```
$ mkdir test
$ ls
Desktop Downloads Pictures Templates Videos
Documents Music Public test
$ mv test new
$ ls
Desktop Downloads new Public Videos
Documents Music Pictures Templates
$ rmdir new
$ ls
Desktop Downloads Pictures Templates Videos
Documents Music Public
```

shell 通过运行在 `PATH` 环境变量列出的目录列表中找到的名称第一个程序来执行每个命令。通常情况下，这些程序位于 `/bin`、`/sbin`、`/usr/bin`、`/usr/sbin`。例如，`ls` 命令位于 `/bin/ls`；`which` 命令报告可执行文件的位置。有时命令由 shell 直接处理，在这种情况下，它被称为内置命令（`cd` 和 `pwd` 就在其中）；`type` 命令允许你查询每个命令的类型。

```
$ echo PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ ls
Desktop Downloads Pictures Templates Videos
Documents Music Public
```

```
$ echo PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ ls
/bin/ls
$ type rm
rm is an alias
$ type cd
cd is a builtin
```

shell 通过运行在 `PATH` 环境变量列出的目录列表中找到的名称第一个程序来执行每个命令。通常情况下，这些程序位于...

```
$ type rm
rm is an alias
$ type cd
cd is a builtin
```

`echo` 命令简单的显示一个字符串。

## 环境变量

环境变量允许进行全局设置，这些设置存储在 `/etc` 中。例如，shell 会话会传递到 `~/.profile`。这些设置是上下文相关的。

在 `/etc` 中环境变量允许进行全局设置，这些 shell 会话会传递到 shell 会话。在 shell 会话中，这些设置被定义在 `~/.profile`。

## 3.3. 文件系统

### 3.3.1. 目录层次结构

与其他 Linux 发行版一样，Kali Linux 符合文件层次结构（FHS），以便用户能够轻松找到目录。FHS 定义了每个目录的用途，如下：

- `/bin/`: 基础程序
- `/boot/`: 启动所需的文件
- `/dev/`: 设备文件
- `/etc/`: 配置文件
- `/home/`: 用户文件
- `/lib/`: 基础库
- `/media/*`: 可移动设备的挂载点（光盘、USB 等）
- `/mnt/`: 临时挂载点
- `/opt/`: 第三方提供的应用程序
- `/root/`: 管理员（root）文件
- `/run/`: 不跨重启的持久化运行时数据
- `/sbin/`: 系统程序
- `/srv/`: 本地托管的数据
- `/tmp/`: 临时文件（此目录在启动时通常会被清空）
- `/usr/`: 应用程序（此目录进一步细分为 bin、sbin、lib），此外 `/usr/share/` 包含架构无关的数据。`/usr/local/` 目录供管理员手动安装应用程序。
- `/var/`: 守护进程处理的可变数据。这包括日志文件、队列、池和缓存。`/proc/` 和 `/sys/` 是内核特有的（不属于 FHS）。它们被内核用于导出数据到用户空间。

### 3.3.2. 用户主目录

用户主目录的内容并没有标准，但仍有一些值得注意的惯例。一个用户主目录通常被称为波浪号（`~`），这是有用的，因为命令解释器会自动将波浪号替换为正确的目录（存储在 `HOME` 环境变量中，其通常值为 `/home/user/`）。

传统的，应用程序配置文件通常直接存储在你的主目录下，但文件名通常以点开头（例如，matt 客户端将其配置存储在 `~/.mtrc`）。注意，以点开头的文件默认是隐藏的；`ls` 命令只有在使用 `-a` 参数时才会列出它们；文件管理器需要显式配置以显示隐藏文件。

某些程序在一个目录中组织多个配置文件（例如 `~/.ssh/`）。某些应用程序（例如 Firefox 浏览器）还使用其目录存储下载数据的缓存。这意味着这些目录可能会消耗大量的磁盘空间。

图形桌面通常有快捷方式显示 `~/Desktop/` 目录的内容（或者对于非英语配置的系统，显示相应的翻译）。

最后，电子邮件系统有时会将传入的邮件存储在 `~/Mail/` 目录下。

## 3.4. 有用的命令

#### 3.4.1. 显示和修改文本

`cat` 文件命令（用于将文件连接到标准输出设备）会读取文件并在终端上显示其内容。如果文件太大无法在一个屏幕内显示，你可以使用分页器（如 `less` 或 `more`）按页显示。

编辑器启动一个文本编辑器（如 `Vi` 或 `Nano`），并允许创建、修改和读取文本文件。最简单的文件有时可以直接从命令解释器通过重定向创建：`command >file` 会创建一个包含给定命令输出的新文件。`command >>file` 与其类似，不同之处是将命令的输出追加到文件，而不是覆盖它。

```
$ echo "Kali rules!" > kali-rules.txt
$ cat kali-rules.txt
Kali rules!
$ echo "Kali is the best!" >> kali-rules.txt
$ cat kali-rules.txt
Kali rules!
Kali is the best!
```

#### 3.4.2. 搜索文件和文件内内容

`find` 目录准则命令根据若干准则在目录下的层次结构中搜索文件。最常用的准则是 `-filename`，它允许按文件名搜索。你也可以在文件名搜索中使用通配符如 `*`。

```
$ find /etc -name hosts
/etc/hosts
/etc/avahi/hosts
$ find /etc -name "hosts*"
/etc/hosts
/etc/hosts.allow
/etc/hosts.deny
/etc/avahi/hosts
```

`grep` 文件命令搜索文件内容并提取匹配正则表达式的行。`-r` 选项对目录中包含的所有文件启用递归搜索。这允许在你只知道文件部分内容时查找文件。
