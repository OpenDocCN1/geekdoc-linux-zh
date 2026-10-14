

# Linux 实用手册：日常使用的技巧与方法：

from the one the script was written on, and so you may have to change this line.

例如，一个脚本可能以以下行开头：

```
#!/usr/local/bin/perl
```

这一行表示脚本是用 perl 语言编写的；`#!` 之后的内容是 perl 程序的完整路径名，在本例中为 `/usr/local/bin/perl`。

如果你尝试执行此脚本而系统报告找不到文件错误，你必须将该第一行更改为与你系统上 perl 二进制文件位置相对应的路径。which 工具会输出此位置。

- 要查找 perl 在你的系统上安装的位置，输入：

```
$ which perl RET
```

如果该命令返回 `/usr/bin/perl` 或除 /usr/local/bin/perl 之外的其他路径名，你必须将脚本第一行中的位置更改为给出的路径名：

```
#!/usr/bin/perl
```

NOTE: 如果 which 命令的输出返回空，这意味着 perl 程序根本未安装在你的系统上；在这种情况下，你应该安装 perl 软件。

## A.4 管理用户

本节描述了系统管理员在管理系统的用户时必须执行的一些操作。

所有这些命令都必须由超级用户使用 root 账户运行——这些命令会编辑系统文件。

### A.4.1 创建用户账户
如何创建新用户账户。

### A.4.2 允许用户访问硬件外设
允许用户访问硬件。

### A.4.3 允许用户挂载驱动器
允许用户挂载驱动器。

## A.4.1 创建用户账户

要创建新用户账户，请使用 adduser。它以要为新账户使用的用户名作为参数。它会提示输入默认设置信息，包括用户的全名和初始密码。

- 要创建一个用户名为 bucky 的新用户，输入：

```
    # adduser bucky RET
```

***NOTE:*** 默认情况下，用户的主目录名称将与用户名相同。因此，例如，用户 bucky 的主目录为 `/home/bucky`。

## A.4.2 允许用户访问硬件外设

某些硬件外设，如 CD-ROM 驱动器和声卡，通常需要超级用户权限才能访问它们。这些设备也有自己的组，因此普通用户也可以通过加入其组来访问它们（参见章节 [Groups and How to Work in Them](#)）。

普通用户可能想要加入的组包括 `floppy`（软盘驱动器）、`audio`（声卡），以及 `dialout` 和 `dip`（调制解调器拨号权限）。

使用 addgroup 将用户添加到与硬件设备关联的组中。将要添加的用户名和要添加到的组名作为参数给出。

- 要将用户 doug 添加到 audio 组，输入：

```
    # addgroup doug audio RET
```

## A.4.3 允许用户挂载驱动器

`/etc/fstab` 文件指定了系统上使用的文件系统的详细信息，包括可能由软盘或 CD-ROM 驱动器挂载的文件系统。为了让用户能够在这些驱动器上挂载磁盘，请确保

`/etc/fstab` 中有软盘和 CD-ROM 驱动器的行，每行都包含 `user` 标志：

```
/dev/fd0      /floppy   auto   defaults,noauto,user   0   0
/dev/cdrom    /cdrom    auto   defaults,noauto,user   0   0
```

## A.5 显示系统信息

以下配方描述了显示你正在运行的系统信息的各种方法。

- A.5.1 系统运行了多久？
- A.5.2 我运行的是哪个版本的 Linux？
- A.5.3 我运行的是哪个版本的 Debian？

系统运行了多久？
我运行的是哪个版本的 Linux？
我运行的是哪个版本的 Debian？

### A.5.1 系统运行了多久？

要了解系统运行了多长时间，请使用 uptime 工具。当你将其作为命令运行时，它会输出当前时间、系统运行时间、已登录用户数，以及过去一分钟、五分钟和十五分钟的系统“负载平均值”。

- 要了解系统运行了多久，输入：

```
$ uptime RET
3:34pm  up 4:31,  4 users,  load average: 0.01, 0.05, 0.07
$
```

要获取系统最近重新启动的时间和日期列表，请将 `reboot` 作为参数传递给 last（参见章节 Listing the Last Times a User Logged In）。

- 要输出系统重新启动时间的列表，输入：

```
$ last reboot RET
```

