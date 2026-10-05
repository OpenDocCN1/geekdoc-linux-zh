

当前目录也被称为 . (点)。`ls` 命令允许列出目录的内容。如果你不提供参数，`ls` 将对当前目录进行操作。

```
$ pwd
/home/buxy
$ cd Desktop
$pwd
/home/buxy/Desktop
$ cd
$pwd
/home/buxy/Desktop
$ cd
$pwd
/home/buxy
$ ls
Desktop Downloads Pictures Templates
Documents Music Public Videos
```

你可以使用 `mkdir directory` 创建新目录，并使用 `rmdir directory` 删除现有的（空）目录。`mv` 命令允许移动和重命名文件及目录；使用 `rm file` 删除文件，使用 `cp source-file target` 复制文件。

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

Shell 通过运行在 `PATH` 环境变量列出的目录列表中找到的第一个同名的程序来执行每个命令。通常情况下，这些程序位于 `/bin`、`/sbin`、`/usr/bin` 或 `/usr/sbin`。例如，`ls` 命令位于 `/bin/ls`；而 `which` 命令则报告给定可执行文件的位置。有时命令直接由 Shell 处理，在这种情况下它被称为内置命令（`cd` 和 `pwd` 就属于其中）；`type` 命令允许你查询每个命令的类型。

```
$ echo PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/bin
$ ls
/bin/ls
```

```
$ type rm
rm is /bin/rm
$ type cd
cd is a shell builtin
```

`echo` 命令的用法是简单的在终端上显示字符串。在这种情况下，它被用于打印环境变量的内容，Shell 在执行命令行之前会自动将变量替换为它们的值。

# 环境变量

环境变量允许存储 Shell 或各种其他程序的全局设置。例如，每个进程都有自己的环境变量（它们是与上下文相关的）。Shell（如登录 Shell [login shells](https )）会声明变量，这些变量将传递给它们执行的其它程序（它们是可继承的）。

这些变量可以在 `/etc/profile` 中全系统定义，也可以在 `~/.profile` 中按用户定义。不特定于命令行解释器的变量被放在 `/etc/environment` 中，因为得益于可插身份模块 (PAM)，这些变量会被注入到所有用户会话中——即使在没有执行 Shell 的情况下也是。

# 3.3. 文件系统

# 3.3.1. 文件系统层次结构标准

与其他 Linux 发行版一样，Kali Linux 的组织符合文件系统层次结构标准 (FHS)，这使得其他 Linux 发行版的用户能够轻松地在 Kali 中找到。FHS 定义了每个目录的用途。顶层目录描述如下。

- /bin/：基础程序
- /boot/：Kali Linux 内核及其早期启动过程所需的其他文件
- /dev/：设备文件
- /etc/：配置文件
- /home/：用户文件
- /lib/：基础库
- /media/*：可移动设备（如 CD-ROM、USB 闪盘等）的挂载点
- /mnt/：临时挂载点
- /opt/：由第三方提供的额外应用程序
- /root/：管理员（root）的个人文件
- /run/：不跨重启持久的易性运行时数据（尚未包含在 FHS 中）
- /sbin/：系统程序
- /tmp/：临时文件（此目录在启动时通常会被清空）
- /usr/：应用程序（此目录根据根目录相同的逻辑进一步细分为 bin、sbin、lib）。此外，`/usr/share/` 包含与架构无关的数据。`/usr/local/` 目录旨在供管理员手动安装应用程序使用，而不会覆盖由软件包系统 (dpkg) 处理的文件。
- /var/：由守护进程处理的变量数据。这包括日志文件、队列、池和缓存。
- `/proc/` 和 `/sys` 是 Linux 内核特定的（不属于 FHS）。它们被内核用于将数据导出到用户空间。

### 3.3.2. 用户主目录

用户主目录的内容没有标准，但仍然有一些值得注意的惯例。了解用户主目录经常用波浪号 (~) 指代很有用，命令行解释器会自动将波浪号替换为正确的目录（该目录存储在 `HOME` 环境变量中，其通常值为 `/home/user/`）。

传统上，应用程序配置文件通常直接存储在你的主目录下，但文件名通常以点开头（mqtt 客户端将其配置存储在 `~/.mttrrc` 中）。注意，以点开头的文件名默认是隐藏的；`ls` 命令只有在使用 `-a` 选项时才会列出它们，图形化文件管理器需要显式配置才能显示隐藏文件。

有些程序使用在一个目录中组织的多个配置文件。有些应用程序（如 Firefox 浏览器）也使用其目录存储缓存。

## 3.4. 有用命令

#### 3.4.1. 显示和修改文本

`cat` 命令显示文件内容。它也可以用于合并文件。如果文件太大无法适应屏幕，可以使用分页器如 `less`。编辑器可以修改文件。`>` 输出重定向到文件。

```
$ echo "Kali!"
.txt
```

#### 3.4.2. 搜索文件

`find` 命令根据标准搜索文件。常用的标准是 `-name`。你也可以在文件名中使用通配符，如 `*`。

`grep` 命令搜索文件内容并提取匹配的正则表达式表达式。

#### 3.4.3. 进程管理

`ps` 命令列出当前运行的进程并通过显示 PID 来识别它们。一旦知道进程的 PID，`kill -signal` 命令允许你发送信号（如果你拥有该进程）。存在多种信号，最常见的是 TERM（终止请求）和 KILL（强制杀死）。

命令行解释器也可以在命令后带有 `&` 的情况下在后台运行程序。通过使用该符号，你可以立即恢复 Shell 的控制，尽管命令仍在运行（作为后台进程不可见）。`jobs` 命令列出后台运行的作业；运行 `fg %job-number` 将作业恢复到前台。当命令在前台运行时（无论是正常启动的，还是通过 `fg` 回到前台的），Ctrl+Z 组合会暂停进程并恢复命令行的控制。然后可以使用 `bg %job-number` 在后台重启该进程。

