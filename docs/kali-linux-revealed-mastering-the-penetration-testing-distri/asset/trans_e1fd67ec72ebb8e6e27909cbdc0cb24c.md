

当前目录通常简称为（`.` 一个点）。`ls` 命令用于列出目录的内容。如果不提供参数，`ls` 将作用于当前目录。

```
$ pwd
/home/buxy
$ cd Desktop
$ pwd
/home/buxy/Desktop
$ cd .
$ pwd
/home/buxy/Desktop
$ cd ..
$ pwd
/home/buxy
$ ls
Desktop  Downloads  Pictures  Templates
Documents  Music  Public  Videos
```

你可以使用 `mkdir directory` 创建新目录，并使用 `rmdir directory` 删除现有的（空）目录。`mv` 命令允许移动和重命名文件和目录；删除文件使用 `rm file`，复制文件使用 `cp source-file target-file`。

```
$ mkdir test
$ ls
Desktop  Downloads  Pictures  Templates  Videos
Documents  Music  Public  test
$ mv test new
$ ls
Desktop  Downloads  new  Public  Videos
Documents  Music  Pictures  Templates
$ rmdir new
$ ls
Desktop  Downloads  Pictures  Templates  Videos
Documents  Music  Public
```

shell 通过运行在 PATH 环境变量列出的目录中找到的第一个同名程序来执行每个命令。大多数情况下，这些程序位于 `/bin`、`/sbin`、`/usr/bin` 或 `/usr/sbin` 中。例如，`ls` 命令位于 `/bin/ls`；`which` 命令报告给定可执行文件的位置。有时命令直接由 shell 处理，这种情况称为 shell 内置命令（`cd` 和 `pwd` 属于此类）；`type` 命令允许你查询每个命令的类型。

```
$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
$ which ls
/bin/ls
```

```
$ type rm
rm is /bin/rm
$ type cd
cd is a shell builtln
```

请注意 `echo` 命令的用法，它只是将字符串显示在终端上。在这种情况下，它用于打印环境变量的内容，因为 shell 在执行命令行之前会自动用变量的值替换变量。

![](img/46e3313ea1bb2892f314630a4f0677b8_80_0.png)

## 3.3. 文件系统

### 3.3.1. 文件系统层次标准

与其他 Linux 发行版一样，Kali Linux 的组织方式与文件系统层次标准（FHS）保持一致，这使得其他 Linux 发行版的用户可以轻松地在 Kali 中找到路径。FHS 定义了每个目录的用途。顶级目录描述如下。

- `/bin/`: 基本程序
- `/boot/`: Kali Linux 内核及其早期引导过程所需的文件
- `/dev/`: 设备文件
- `/etc/`: 配置文件
- `/home/`: 用户的个人文件
- `/lib/`: 基本库
- `/media/*/`: 可移动设备（CD-ROM、U 盘等）的挂载点
- `/mnt/`: 临时挂载点
- `/opt/`: 由第三方提供的额外应用程序
- `/root/`: 管理员（root）的个人文件
- `/run/`: 易失性运行时数据，不会在重启后保留（尚未包含在 FHS 中）
- `/sbin/`: 系统程序
- `/srv/`: 托管在此系统上的服务器使用的数据
- `/tmp/`: 临时文件（此目录通常在启动时清空）
- `/usr/`: 应用程序（此目录根据与根目录相同的逻辑进一步细分为 bin、sbin、lib）。此外，`/usr/share/` 包含与架构无关的数据。`/usr/local/` 目录旨在供管理员手动安装应用程序而不覆盖由包管理系统（dpkg）处理的文件。
- `/var/`: 由守护进程处理的变量数据。这包括日志文件、队列、池和缓存。
- `/proc/` 和 `/sys/` 是 Linux 内核特有的（不属于 FHS）。它们用于内核向用户空间导出数据。

### 3.3.2. 用户主目录

用户主目录的内容没有标准化，但仍有几个值得注意的约定。一个是用户的主目录通常用波浪号（`~`）引用。这是有用的，因为命令解释器会自动将波浪号替换为正确的目录（该目录存储在 HOME 环境变量中，其常用值为 /home/user/）。

传统上，应用程序配置文件通常直接存储在主目录下，但文件名通常以点开头（例如，mutt 邮件客户端将其配置存储在 `~/.muttrc` 中）。请注意，以点开头的文件名默认是隐藏的；`ls` 命令只有在 `-a` 选项使用时才列出它们，并且图形化文件管理器需要明确配置以显示隐藏文件。

一些程序还使用组织在一个目录中的多个配置文件（例如，`~/.ssh/`）。一些应用程序（如 Firefox 网络浏览器）还使用其目录来存储下载数据的缓存。这意味着这些目录可能会消耗大量磁盘空间。

这些直接存储在主目录中的配置文件，通常统称为 dotfiles，长期以来已经泛滥，导致这些目录充斥着它们而变得杂乱无章。幸运的是，在 FreeDesktop.org 伞标下的集体努力促成了 XDG 基础目录规范，这是一种旨在清理这些文件和目录的约定。该规范指出，配置文件应存储在 `~/.config` 下，缓存文件在 `~/.cache` 下，应用程序数据文件在 `~/.local`（或其子目录）下。这种约定正在逐渐获得推广。

图形化桌面通常有快捷方式显示 `~/Desktop/` 目录的内容（或非英语配置系统中相应的翻译）。

最后，电子邮件系统有时会将收到的邮件存储到 `~/Mail/` 目录中。

## 3.4. 实用命令

### 3.4.1. 显示和修改文本文件

`cat file` 命令（旨在将文件连接到标准输出设备）读取文件并在终端上显示其内容。如果文件太大而无法适合屏幕，你可以使用分页器如 `less`（或 `more`）逐页显示它。

`editor` 命令启动文本编辑器（如 `Vi` 或 `Nano`）并允许创建、修改和读取文本文件。最简单的文件有时可以直接从命令解释器通过重定向创建：`command > file` 创建一个名为 `file` 的文件，其中包含给定命令的输出。`command >> file` 相似，但它是将命令的输出追加到文件而不是覆盖它。

```
$ echo "Kali rules!" > kali-rules.txt
$ cat kali-rules.txt
Kali rules!
$ echo "Kali is the best!" >> kali-rules.txt
$ cat kali-rules.txt
Kali rules!
Kali is the best!
```

### 3.4.2. 在文件和内部搜索

`find directory criteria` 命令根据几个标准搜索 `directory` 层级下的文件。最常用的标准是 `-name filename`，它允许按名称搜索文件。你还可以在文件名搜索中使用常见的通配符，如 `*`。

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

`grep expression files` 命令搜索文件内容并提取匹配正则表达式的行。添加 `-r` 选项启用对目录中包含的所有文件的递归搜索。这允许你仅知道文件部分内容时寻找文件。

### 3.4.3. 管理进程

`ps aux` 命令列出当前正在运行的进程，并通过显示其 PID 帮助识别它们。一旦知道进程的 *PID*，`kill -signal pid` 命令允许你向它发送信号（如果你拥有该进程）。存在多种信号；最常用的是 *TERM*（请求优雅终止）和 *KILL*（强制终止）。

命令解释器还可以在命令后跟 “&” 时在后台运行程序。通过使用与符号，你可以立即重新控制 shell，尽管命令仍在运行（作为隐藏的背景进程）。`jobs` 命令列出在后台运行的进程；运行 `fg job-number`（用于 *foreground*）将作业恢复到前台。当命令在前台运行时（无论是正常启动还是使用 `fg` 恢复到前台），*Ctrl+Z* 键组合会暂停进程并恢复对命令行的控制。然后可以使用 `bg job-number`（用于 *background*）在后台重启该进程。

### 3.4.4. 管理权限

Linux 是一个多用户系统，因此需要提供权限系统来控制对文件和目录的授权操作集，这包括所有系统资源和设备（在 Unix 系统上，任何设备都由文件或目录表示）。这一原则为所有类 Unix 系统所共有。

每个文件或目录都有针对三类用户的特定权限：

- 其 *所有者*（用 *u* 表示，如同 user）
- 其 *所有者组*（用 *g* 表示，如同 group），代表组的所有成员
- *其他*（用 *o* 表示，如同 *other*）

可以组合三种类型的权限：

- *读取*（用 *r* 表示，如同 *read*）；
- *写入*（或 *修改*，用 *w* 表示，如同 *write*）；
- *执行*（用 *x* 表示，如同 *EXecute*）。

对于文件而言，这些权限很容易理解：读取访问允许读取内容（包括复制），写入访问允许更改它，执行访问允许运行它（只有它是程序时才会起作用）。

