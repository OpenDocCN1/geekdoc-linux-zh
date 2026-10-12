
```
[root@netmon tmp]# chkconfig sendmail on
[root@netmon tmp]# chkconfig --list | grep mail
sendmail 0:off 1:off 2:off 3:on 4:off 5:on 6:off
[root@netmon tmp]# service sendmail start
Starting sendmail: [  OK  ]
Starting sm-client: [  OK  ]
[root@netmon tmp]#
```

## 系统关机

工作完成后，不应立即关机或断电。这可能会损坏文件以及文件系统目录结构。`Linux` 有多种优雅关闭和重启系统的方法，如下面的章节所述。

用于关闭系统的命令列表如下：

- `shutdown –h now`

- `halt`

- `poweroff`

- `init 0`

`init` 命令允许你更改当前的运行级别，而对于关机，该值为 0。下面是一个示例：

```
[root@netmon tmp]# init 0
```

`Fedora` 也有一个 `shutdown` 命令，可以起到相同的作用。它通常会提示你是否确定要执行该命令，可以使用 `-y` 开关来避免这种情况。`-h` 开关强制系统停机，第一个参数告诉系统在开始该过程前等待多久，在此例中为 0 分钟。你还可以指定在一天中的特定时间关机；详细信息请参阅 `man` 手册页。`shutdown` 命令的另一个优点是它警告用户关机即将发生：

```
[root@netmon tmp]# shutdown -hy 0
  Broadcast message from root (pts/0)
  -----
The system is going down for system halt NOW!
[root@netmon tmp]#
```

### 重启系统

使用以下命令重启系统：

- `shutdown -r`

- `reboot`

- `init 6`

你还可以通过进入运行级别 6 立即使用以下 `init` 命令重启系统：

```
[root@netmon tmp]# init 6
```

以下 `reboot` 命令具有相同的效果，但它还会向所有用户发送警告消息：

```
[root@netmon tmp]# reboot
```

广播消息“Broadcast message from root (pts/0)”显示如下：

```
The system is going down for reboot NOW!
[root@netmon tmp]#
```

通过使用 `-r` 开关并指定延迟时间（在此例中为 10 分钟），可以使用 `shutdown` 命令执行更优雅的重启：

```
[root@netmon root]# shutdown -ry 10
  Broadcast message from root (pts/0) :
  The system is going DOWN for reboot in 10 minutes!
  Broadcast message from root (pts/0) :
```

```
The system is going DOWN for reboot in 9 minutes!
…
Broadcast message from root (pts/0):
The system is going down for reboot NOW!
```

### 进入单用户模式

某些操作要求你强制系统注销所有用户、第三方应用程序和网络连接，以便只有系统管理员可以通过 `VGA` 控制台访问系统。另一个原因是恢复你的 `root` 密码。

### 切换到单用户模式

当系统正常运行时，可以使用 `init` 命令进入运行级别 1 来实现。最好从控制台执行此操作，因为如果你从远程终端会话执行，你将会被注销：

```
[root@netmon root]# init 1
…
[root@netmon tmp]# shutdown 1
Broadcast message from root (pts/0):
The system is going DOWN to maintenance mode in 1 minute!
Broadcast message from root (pts/0):
The system is going down to maintenance mode NOW!
```

### 在 Grub 欢迎屏幕进入单用户模式

你可以直接在系统通电后进入单用户模式：

1.  开启系统电源。

2.  当出现 `Linux` 标志屏幕（即允许你选择系统中安装的各种内核的屏幕）时，输入字母 `a` 代表“append”。你将看到如下提示，用于在 `grub.conf` 文件中找到的启动字符串中添加启动选项：`grub append> ro root=LABEL=/`

3.  在字符串末尾添加 1：

```
grub append> ro root=LABEL=/ 1
```

4.  按回车键。系统将继续启动，但会直接进入 `root #` 提示符，而不会先要求输入用户名和密码。

### 从单用户模式恢复到默认运行级别

`exit` 命令强制系统退出运行级别 1 并恢复到系统的默认运行级别。你也可以使用 `init` 命令（例如 `init 3` 和 `init 5`）来更改此默认行为：

## 恢复 root 密码

有时你可能会忘记 `root` 密码，或者前任系统管理员可能已经离职而没有将密码交给你。要恢复 `root` 密码，请执行以下步骤：

1.  前往 `VGA` 控制台并按下 `Ctrl-Alt-Del`。系统随后将有序地关闭。

2.  重新启动系统并进入单用户模式。

3.  在命令提示符处，更改你的密码。单用户模式假定控制台前的人是系统管理员 `root`，因此你无需指定 `root` 用户名。

4.  使用 `exit` 命令返回到你的默认运行级别（runlevel）。

```
bash-2.05b# exit
INIT: Entering runlevel: 3
...
Fedora Core release 6
Kernel 2.6.18-1.521 on an i686

netmom login:
```

## Grand Unified Bootloader (GRUB)

`Grand Unified Bootloader (GRUB)` 是一个多启动引导加载程序。在许多发行版中，它现在是默认的引导加载程序。`GRUB` 提供了对各种操作系统广泛的兼容性。用户可以从系统启动时显示的菜单界面中选择要运行的操作系统。使用箭头键移动到某个条目并按下 `ENTER`。输入 `e` 以编辑命令，这允许你更改内核参数或指定不同的内核。输入 `c` 命令会使你进入命令行界面。如果你的系统 `BIOS` 支持非常大的磁盘，`GRUB` 可以从其中任何位置启动。`Linux` 和 `Unix` 操作系统被称为多启动操作系统，并接受在启动时传递给它们的参数。

`GRUB` 配置存储在 `/etc/grub.conf` 文件中。你只需要创建你的条目，`GRUB` 将在你重启时自动读取它们。你可以设置几个选项，例如超时期间和使用哪个背景图像。你可以通过创建标题条目来指定要启动的系统，该条目以 `title` 术语开头。然后你必须指定操作系统内核或程序的位置，即哪个硬盘以及该硬盘上的哪个分区。此信息列在 `root` 选项后的括号中。编号从 0 开始，而不是 1，并且无论它们是 `IDE` 还是 `SCSI` 硬盘，硬盘都使用 `hd` 前缀表示。因此，`root(hd0,2)` 引用第一个硬盘 (`hda`) 以及该硬盘上的第三个分区 (`hda3`)。对于 `Linux` 系统，你还必须使用 `kernel` 选项来指示要运行的内核程序，使用完整路径名以及内核可能需要的任何选项。`RAM` 盘由 `initrd` 选项表示。

```
title Red Hat Linux (2.6.18-20)
root (hd0,2)
kernel /boot/vmlinuz-2.6.18-20 ro root=/dev/hda3
initrd /boot/initrd-2.6.18-20.img
```

对于 `Windows` 等另一个操作系统，你需要使用 `rootnoverify` 选项来指定 `Windows` 安装在哪里。此选项指示 `GRUB` 不要尝试挂载该分区。使用 `imageactive` 和 `chainloader +1` 选项以允许 `GRUB` 访问它。`chainloader` 选项告诉 `GRUB` 为该操作系统使用另一个引导程序。该数字指示引导程序所在的分区扇区——例如，`+1` 指示第一个扇区。

```
    title windows XP
    rootnoverify (hd0,0)
    imageactive
    chainloader +1
```
