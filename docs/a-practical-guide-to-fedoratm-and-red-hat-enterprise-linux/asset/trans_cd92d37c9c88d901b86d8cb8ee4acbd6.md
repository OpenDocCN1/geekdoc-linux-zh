

最后一条命令将一个空命令的输出重定向到文件，其结果与前面的命令相同。你可以使用其中任何一条命令将现有文件截断为零长度，同时不改变其权限。你还可以使用 /dev/null 来消除你不想要的输出：

```
$ grep portable * 2> /dev/null
```

此命令显示工作目录中所有文件里包含字符串 portable 的所有行。输出到标准错误（第 333 页）的内容（如权限或目录错误）会被丢弃，而输出到标准输出的内容则显示在屏幕上。另请参阅第 158 页。

### /dev/pts

一个通往 Linux 内核的钩子。此伪文件系统是伪终端支持的一部分。伪终端被远程登录程序（如 ssh 和 telnet）以及 xterm 和其他图形终端模拟器所使用。下面的一系列命令表明 Sam 登录在 /dev/pts/1 上。在使用 `tty` 验证他所登录的伪终端，并使用 `ls` 显示该伪终端存在后，Sam 将 `echo` 命令的输出重定向到 /dev/pts/1，此时输出出现在他的屏幕上：

```
$ tty
/dev/pts/1
$ ls /dev/pts
0 1 2 ptmx
$ echo Hi there > /dev/pts/1
Hi there
```

### /dev/random 和 /dev/urandom

内核随机数发生器的接口。你可以使用 `dd` 与这两个文件中的任意一个来创建一个填充有伪随机字节的文件。然而，如果熵不足，urandom 可能会生成潜在质量较低的结果（尽管对于大多数用途而言，这种差异无关紧要）。以下是一个示例：

```
$ dd if=/dev/urandom of=randfile bs=1 count=100
100+0 records in
100+0 records out
100 bytes (100 B) copied, 0.00084387 seconds, 1.13 kB/s
```

前面的命令从 /dev/urandom 读取数据并写入名为 randfile 的文件。块大小为 1，计数为 100；因此 randfile 的长度为 100 字节。如果需要随机性更强的字节，你可以从 /dev/random 读取。有关更多信息，请参阅 urandom 和 random 手册页。

# 使用 random 可能会导致系统挂起

如果熵不足，从 /dev/random 读取可能会导致系统长时间挂起。此问题在虚拟系统中很常见。你可以通过移动鼠标、在键盘上打字或复制文件来创建熵并解除系统挂起。或者，你可以从 /dev/urandom 读取。

### 擦除文件

你可以使用类似的技术在删除文件之前擦除其数据，使得从已删除文件中恢复数据几乎不可能。出于安全原因，你可能希望擦除文件。

在下面的示例中，`ls` 显示名为 secret 的文件的大小。使用块大小 1 和与 secret 中字节数对应的计数，`dd` 擦除了该文件。`conv=notrunc` 参数确保 `dd` 覆盖文件中的数据，而不是磁盘上的其他（错误）位置。

```
$ ls -l secret
-rw-r--r--, 1 sam pubs 5733 01-27 13:12 secret
$ dd if=/dev/urandom of=secret bs=1 count=5733 conv=notrunc
5733+0 records in
5733+0 records out
5733 bytes (5.7 kB) copied, 0.0358146 seconds, 160 kB/s
$ rm secret
```

为了增加安全性，在运行 `dd` 后运行 `sync` 以刷新磁盘缓冲区，并在删除文件前多次重复这两条命令。或者，你可以使用 `shred`（第 223 页）来擦除文件。有关擦除文件的更多信息，请访问 wipe.sourceforge.net。

- **/dev/shm** 实现共享内存，它为进程提供了一种高效的信息共享方式。
- **/dev/zero** 从此文件读取的输入包含无限个零（数字零，而不是 ASCII 零）。你可以用以下之类的命令用零填充一个文件（例如交换文件；第 513 页）或用零覆盖一个文件：

```
$ dd if=/dev/zero of=zeros bs=1024 count=10
10+0 records in
10+0 records out
10240 bytes (10 kB) copied, 0.000160263 seconds, 63.9 MB/s

$ od -c zeros
0000000  \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0 \0
*
0024000
```

`od` 实用程序显示新文件的内容。

如果你尝试使用 /dev/null 来填充一个文件的零，你会填充你正在工作的那个分区：

```
$ cp /dev/zero bigzero
cp: error writing 'bigzero': No space left on device
cp: failed to extend 'bigzero': No space left on device
$ rm bigzero
```

- **/etc** 存放本机系统配置文件。
- **/etc/aliases** 邮件传递系统用来存储用户的 `aliases`。编辑此文件以适应本地需求。有关更多信息，请参阅第 746 页的 /etc/aliases。
- **/etc/alternatives** 存放符号链接，以便你可以使用与包含该实用程序的文件名不同的名称来调用实用程序。例如，当你输入命令 `cancel` 时，shell 使用以下链接调用 `cancel.cups`：

```
$ ls -l /usr/bin/cancel
lrwxrwxrwx. 1 root root 30 06-04 19:31 /usr/bin/cancel -> /etc/alternatives/print-cancel
$ ls -l /etc/alternatives/print-cancel
lrwxrwxrwx. 1 root root 20 06-04 19:31 /etc/alternatives/print-cancel -> /usr/bin/cancel.cups
```

alternatives 目录还允许一个实用程序出现在多个目录中，并且可以通过提供执行类似任务（例如，`mailq` 可以根据使用的是哪个服务器来调用 `sendmail` 或 `postfix` 命令）的熟悉命令来降低管理员的学习曲线。

此外，此目录允许你使用多个名称调用同一个实用程序。虽然 alternatives 目录并不允许开发人员做他们原本无法做的事情，但它提供了一种有序的方式来维护更新这些链接。使用 `whereis`（第 2.55 页）查找指向某个实用程序的所有链接。

### /etc/at.allow、/etc/cron.allow 和 /etc/cron.deny

默认情况下，用户可以使用 `at` 和 `crontab` 实用程序。`at.allow` 和 `cron.allow` 文件分别列出了允许使用 `at` 和 `crontab` 的用户。`at.deny` 和 `cron.deny` 文件指定了不允许使用相应实用程序的用户。根据 Fedora/RHEL 的配置，空的 `at.deny` 文件和缺失的 `at.allow` 文件允许任何人使用 `at`；缺失的 `cron.allow` 和空的 `cron.deny` 文件允许任何人使用 `crontab`。要防止除具有 root 权限的用户之外的任何人使用 `at`，请删除 `at.deny` 文件。要防止除具有 root 权限的用户之外的任何人使用 `crontab`，请创建一个仅包含条目 `root` 的 `cron.allow` 文件。有关 `crontab` 的更多信息，请参阅第 607 页的“调度任务”。

- **/etc/default** 一个目录，包含为 NFS 和 `useradd` 等系统服务和实用程序设置默认值的文件。查看此目录中的文件以获取更多信息。
- **/etc/fstab** 文件系统（挂载）表——包含系统管理员指定的可挂载设备列表。有关更多信息，请参阅第 524 页。
- **/etc/group** 组允许用户在不赋予所有系统用户访问权限的情况下共享文件或程序。当多个用户正在处理非公共文件时，此方案非常有用。`/etc/group` 文件将一个或多个用户名与每个组（GID [组 ID 号]）关联起来。名为 `wheel` 的组成员是管理员，可以使用 `sudo` 获取 root 权限；请参阅第 429 页的“管理员和 wheel 组”，了解更细粒度的文件访问控制方式。

`/etc/group` 文件中的每个条目都有四个由冒号分隔的字段，用于描述一个组：
`group-name:password:group-ID:login-name-list`

`group-name` 是组的名称。`password` 是一个可选的经过散列（第 12.52 页）的密码。此字段通常包含一个 `x`，表示不使用组密码。`group-ID` 是一个数字，1-499 保留给系统账户。`login-name-list` 是属于该组的用户的逗号分隔列表。如果条目太长无法在一行中显示，请以反斜杠（`\`）结束该行，这会引用随后的 RETURN 键，并在下一行继续该条目。以下是组文件中的一个示例条目。该组名为 `pubs`，没有密码，组 ID 为 1103：

```
pubs:x:1103:max,sam,zach,mark
```

你可以使用 `groups` 实用程序来显示用户所属的组：

```
$ groups sam
sam : sam pubs
```

每个用户都有一个主组，这是该用户在 `/etc/passwd` 文件中被分配的组。默认情况下，Fedora/RHEL 拥有用户私有组：每个用户的主组与用户同名。此外，根据用户在 `/etc/group` 文件中出现的 `login-name-lists`，用户可以属于其他组。实际上，你同时属于你的主组和你在 `/etc/group` 中被分配的任何组。当你尝试访问你不拥有的文件时，Linux 会检查你是否是有权访问该文件的组的成员。如果是，你将受到该文件的组访问权限的约束。如果你不是有权访问该文件的组的成员，并且你不拥有该文件，你将受到该文件的公共访问权限的约束。

当你创建一个文件时，Linux 将其分配给你的主组。有关使用 `system-config-users` 处理组的信息，请参阅第 600 页。

### /etc/hostname

存放系统名称。使用 `hostnamectl`（第 219 页）更改系统的域名。有关域名的更多信息，请参阅第 300 页。

### /etc/hosts

存储其他系统的名称、IP 地址，以及可选的别名。通常，此文件包含本地系统的主机名和 IP 地址。它还包含一个针对 `localhost` 的特殊条目。此条目支持环回服务，允许本地系统与自身通信（例如，用于 RPC 服务）。环回服务的 IP 地址始终为 127.0.0.1 (IPv4) 或 ::1 (IPv6)，而 127.0.1.1 命名本地系统。有关更多信息，请参阅第 300 页。以下是一个简单的 /etc/hosts 文件：

```
$ cat /etc/hosts
127.0.0.1     localhost localhost.localdomain localhost4 localhost4.localdomain4
::1     localhost localhost.localdomain localhost6 localhost6.localdomain6
127.0.1.1     tiny
192.168.0.9   jam
192.168.0.10  plum
192.168.0.12  dog
...
```

如果你不使用 NIS 或 DNS 来查找主机名（称为主机名解析），则必须在 `/etc/hosts` 中包含本地系统应能通过主机名联系到的所有系统。（系统始终可以通过使用系统的 IP 地址来联系另一个系统。）`/etc/nsswitch.conf` 文件（第 495 页）中的 `hosts` 条目控制检查主机名解析服务的顺序。

