
输入密码后，您就可以在远程计算机上进行操作了。再次强调，您在键盘上输入的与远程计算机通信的所有内容都是加密的。使用 `exit` 或 `logout` 命令退出会话并返回到您计算机上的 shell。

> **警告**
>
> 最常见的远程访问命令 `telnet` 在此作为示例展示，因为它包含在大多数 Linux 发行版中；但你不应该使用它：`telnet` 在网络上传输用户名和密码时使用明文，给您的系统带来巨大的安全风险。此外，请注意，此服务必须在远程计算机上明确启用并允许（通过编辑 `/etc/xinetd.d` 目录下的名为 `telnet` 的文件，然后重启 `xinetd`；有关启动或重启系统服务的更多信息，请参阅第 15 章中的“手动启动和停止服务”部分）。

`telnet` 命令可以与远程主机名称或互联网协议（IP）地址一起使用，以登录到远程计算机。例如，要从名为 `laptop` 的主机登录到名为 `desktop` 的主机，您需要输入以下内容：

```bash
[andrew@laptop andrew]$ telnet desktop
```

按下回车键后，您将看到远程计算机提供的信息，随后系统会提示您输入远程系统上的用户名：

```text
Trying 192.168.2.70...
Connected to desktop.andboxuson.co.uk (192.168.2.73).
Escape character is '^]'.

Linux 2.6.10-1.741_FC3 (desktop.andboxuson.co.uk) (15:43 on Friday, 4 February 2005)

login: andrew
```

输入用户名（在本例中为 `andrew`）并按下回车键后，系统会提示您输入远程系统上的密码：

```text
Password:
Last login: Fri Feb 4 15:42:26 from 192.168.2.2
[andrew@desktop andrew]$ 
```

输入密码并按下回车键后（密码不会回显显示），您将获知上次登录的时间，然后就可以在远程计算机上进行操作了。使用 `exit` 或 `logout` 命令退出会话并返回到您计算机上的 shell。

虽然可以使用 `telnet` 通过有线和无线网络登录远程计算机，但不推荐这样做，尤其是通过互联网。当您输入用户名、按下回车键并输入密码时，您的用户名和密码会在网络上未加密传输。出于显而易见的原因，通过网络传输未加密的用户名和密码是个坏主意。然而，如果您拥有一个物理安全的内部网络，不连接互联网，并且实施了防火墙策略，不使用无线网络，那么使用 `telnet` 就没有问题。事实上，使用 `ssh` 的加密开销在某些情况下可能会降低网络传输速率。

> **注意**
>
> 可以通过加密的虚拟专用网络（VPN）安全地使用 `telnet`，但这超出了本章和本书的范围。此外，既然可以使用 SSH，何必麻烦呢？

## 更改用户信息

Linux 用户由 root 操作员分配一个名称，称为*用户名*。分配用户名的一种方法是使用名字的首字母和姓氏的小写形式；例如，Bernice Hudson 的用户名将是 `bhudson`。每个用户还必须拥有密码，该密码与用户名一起在图形化或基于文本的登录中使用。

> **注意**
>
> 旧版本的 Linux 操作系统将用户名长度限制为 8 个字符。当前版本的 Fedora 将用户名限制为 32 个字符。好的密码应至少包含 8 个字符，并包含大写和小写字母以及数字。可以使用 `mkpasswd` 命令（包含在 *expect* 软件包中）为用户生成随机密码。例如，要自动生成一个 10 个字符的密码，其中包含 3 个大写字母和 3 个数字，请使用 `mkpasswd -l 10 -d 3 -c 3`。好的密码不是生日、纪念日、宠物的名字、恋人的名字或您第一辆车的型号！

您不能更改用户名，但可以更改用户信息，如地址、电话等。使用 `chfn` 或 *change finger information* 命令进行这些更改。该命令会修改您在系统密码文件 `/etc/passwd` 条目中的内容，该文件由 `finger` 命令用来显示系统用户信息。例如，在命令行输入 `chfn` 并按下回车键：

```bash
$ chfn
Changing finger information for bhudson.
Password:
Name []: Bernice Hudson
Office []: Suite 56 N. Centennial Blvd.
Office Phone []: 919 555-1212
Home Phone []: 919 555-1213
Finger information changed.
```

系统会引导您通过一系列提示以输入新的或更新的信息。请注意，`chfn` 命令不允许在输入信息时使用逗号。您可以通过几种方式验证这些信息，例如查看 `/etc/passwd` 的内容：

```bash
$ grep bhudson /etc/passwd
bhudson:x:501:501:Bernice Hudson,Suite 56 N. Centennial Blvd.,\
919 555-1212,919 555-1213:/home/bhudson:/bin/bash
```

您还可以使用 `finger` 命令来验证更新的用户信息：

```bash
$ finger bhudson
Login: bhudson
Name: Bernice Hudson
Directory: /home/bhudson
Shell: /bin/bash
Office: Suite 56 N. Centennial Blvd.  Office Phone: 919 555-1212
Home Phone: 919 555-1213
Never logged in.
No mail.
No Plan.
```

## 阅读文档

虽然您在本书中学习了使用 Fedora 的基础知识，但您需要时间和实践来掌握并解决 Linux 操作系统和您的发行版中更复杂的方面。与任何操作系统一样，当您继续使用 Linux 时，预计会遇到一些问题或令人困惑的问题。解决这些问题的第一站是系统随附的文档；如果您在那里找不到所需的信息，请查看 Fedora 的网站。

> **注意**
>
> 检查 Fedora 网站以获取安全更新和错误修复是个好主意。请访问 http://fedoraproject.org/download/。或者，您可以随时快速执行 `yum update` 以确保您的系统拥有最新的软件。

Linux 和 UNIX 一样，是一个自文档化系统，可通过 `man` 命令访问手册页。Linux 提供了许多其他有用的命令来访问其文档。您可以使用 `apropos` 命令——例如，使用诸如 partition 这样的关键词——来查找与分区相关的命令，如下所示：

```bash
$ apropos partition
diskdumpfmt  (8) - format a dump device or a partition
fdisk   (8) - Partition table manipulator for Linux
GNU Parted [parted]  (8) - a partition manipulation program
mpartition (1) - partition an MSDOS hard disk
MPI_Cart_sub (3) - Partitions a communicator into subgroups which form
lower-dimensional Cartesian subgrids
```

### LVM 和分区命令

- `partprobe` (B) - 通知操作系统分区表已更改
- `pvcreate` (B) - 初始化磁盘或分区以供 LVM 使用
- `sfdisk` (B) - Linux 的分区表操作工具

若要查找命令及其文档，可以使用 `whereis` 命令。例如，如果你正在查找 `fdisk` 命令，可以这样做：

```bash
$ whereis fdisk
fdisk: /sbin/fdisk /usr/share/man/man8/fdisk.8.gz
```

## 使用手册页

若要了解有关命令或程序的更多信息，请使用 `man` 命令，后跟该命令的名称。Linux 和 X Window 命令的手册页位于 `/usr/share/man`、`/usr/local/share/man` 和 `/usr/X11R6/man` 目录中；因此，例如，若要阅读 `rm` 命令的手册页，请像这样使用 `man` 命令：

```bash
$ man rm
```

按 Enter 键后，`less` 命令（一种被称为分页器的 Linux 命令）将显示手册页。`less` 命令是一个文本浏览器，你可以使用它在文档中前后（甚至左右）滚动，以了解该命令的更多信息。输入字母 `h` 获取帮助，使用正斜杠输入搜索字符串，或按 `q` 键退出。

> **注意**
>
