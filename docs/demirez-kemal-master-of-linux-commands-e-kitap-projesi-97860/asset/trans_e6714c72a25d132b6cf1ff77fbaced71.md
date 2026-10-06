

# Cpio

一种简单的备份和恢复目录的方法，你可以使用 `cpio` 命令。该命令的基本用法如下：

- `ls | cpio -ov > backup.cpio`: 创建扩展名为 `.cpio` 的备份文件
- `cpio -idv < backup.cpio`: 恢复用 cpio 创建的备份文件
- `cpio --list < backup.cpio`: 列出备份文件的内容内容

例如，如果你想备份 `/etc` 目录，在 `/etc` 目录下第一次使用 `ls | cpio -ov > /tmp/backup.cpio` 命令，`/etc` 目录会被备份到 `/tmp` 下并命名为 `backup.cpio`。

```bash
root@kemal:/etc# ls | cpio -ov > /tmp/backup.cpio
adduser.conf
adjtime
aliases
alternatives
amap
anacrontab
apache2
apg.conf
apm
apparmor.d
apt
arpwatch.conf
at.deny
at-spi2
navahi
avavrdude.conf
```

现在让我们使用 `--list < backup.cpio` 命令列出备份文件的内容。

```bash
root@kemal:/tmp# -l backup.cpio
-rw-r--r-- 1 root root 956416 Kas 25 01:23 backup.cpio
root@kemal:/tmp# file backup.cpio
backup.cpio: cpio archive
root@kemal:/tmp# cpio --list < backup.cpio
adduser.conf
adjtime
aliases
alternatives
amap
anacrontab
apache2
apg.conf
apm
```

我们必须使用 `cpio -idv < /tmp/backup.cpio` 来恢复备份文件。

```bash
root@kemal:/etc# cpio -idv < /tmp/backup.cpio
cpio: adduser.conf oluşturulmadi: daha yeni ya
adduser.conf
```

# 第 13 章

## 运行级别-服务

## 运行级别 (Runlevels)

Linux 系统中有一个概念叫做运行级别（runlevels）。在解释这个概念之前，我们必须先理解 Linux 系统的启动和内核加载到内存的过程。

当 Linux 系统启动时，内核加载到内存并搜索硬件以安装驱动更新。然后挂载根文件系统（`/`）并启动 `init` 程序进行执行。在这个过程执行期间，运行级别会被调整。这种根据确定的进程来选择启动哪些服务的进度被称为运行级别。在 Linux 系统中，有这样的 7 种不同的工作状态。我们可以简单地将其总结为：

- 0：服务级别，没有任何服务运行，并开始关机过程。
- 1：单用户级别。网络服务不工作。系统可用于维护。
- 2：无网络支持的多用户操作级别。
- 3：网络辅助的多级工作级别。
- 4：未使用。但可以由用户特定定义。
- 5：图形用户界面的运行级别。今天绝大多数用于个人使用的 Linux 发行版，此级别都会默认开始工作。
- 6：重启级别。

要查看我们的系统运行在哪个级别上，我们可以使用 `runlevel` 命令。

```bash
root@kemal:~# runlevel
N 5
root@kemal:~# _
```

每个工作级别都有一个存放启动和服务终止服务脚本的文件夹。这些目录位于 `/etc` 目录下，格式为 `rcX.d`（X = 运行级别数字）。

```text
rc0.d
rc1.d
rc2.d
rc3.d
rc4.d
rc5.d
rc6.d
rc.local
rc5.d
```

此目录中以 K 开头的文件表示切换到此级别时将停止的服务。以 S 开头的文件表示切换到操作级别级别时将执行的服务。

```bash
root@kemal:/etc/rc5.d# ls
K1apache S01openven2
K1atftpd S01redsocks S01rsyslog
K1beef-wss S01whod S01thin
K1bluetooth S01samba-ad-dc S01luuid
K1darkstat S01mbd S02anacron
K1dns2tcp S1nmspd S02arpwatch
K1oldradis S1ssh S02atd
K1lexim4 S1lsh S02cron
K1lined S02avahi-daemon S02dbus
K1miredo K2mysql S02gdom
K1nmbd K2postgresql S02irqbalance
K1ntp README
K1openbsd-inetd S01binfmt-support S02redis-server
root@kemal:/etc/rc5.d#
```

# 158 | Linux 命令精通

事实上，这里显示的文件是指向 `/etc/init.d` 目录中文件的符号链接。

```bash
root@kemal:/etc/rc5.d# file K0apache2
K0apache2: symbolic link to ..init.d/apache
root@kemal:/etc/rc5.d# _
```

如果你在 `/etc` 目录下使用 `rc*,*` 命令，你将列出所有操作级别上 `rc*,*` 服务的状态。

```bash
root@kemal:/etc# ls rc.*
rc.local:
rc0.d:
K0apache2 K0lirbalance
K0watch K0miredo
K0latd K0mbd
K0atftpd K0openbsd-inet
K0beef K0vas-manager
K0uetoot K0vasscanner
K0darkstat K0vpn
K0dns2 K0redis-server
K0ldradis K0whod
K0lexim4 K0redsocks
K0lined K0ls
K1miredo K0green-security-assistant
K1nmbd K0samba-ad-dc
K1ntp K0liined
K1openbsd-inetd K0bd
rc1.d:
K1apache2 K0green-security-assistant
K1atftpd K0rw
K1at K0liod
K1atd K0miredo
K1beef-wss K0nmbd
K1bluetooth K0openbsd-inet
K1darkstat K0sn
K1dns2tcp K0vas-manager
K1oldradis K0
```

## Sysv-rc-conf

现在让我们聊聊可以使用的查看工作级别配置的命令。但请在使用此命令时确保终端是全屏。在某些情况下，Linux 终端不会反映全屏。我们将使用 `sysv-rc-conf` 命令。该命令的输出将如下。

| Sysv RunLevel | stop service | start service | help | quit | 1 | 2 | 3 | 4 | 5 | 6 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| anacron | [ ] | [X] | [X] | [ ] | [ ] | | | [X] | [X] | | | |
| apache2 | [ ] | [X] | [X] | [ ] | [ ] | | | [X] | [X] | [ ] | | |
| arpatch | [ ] | [X] | [X] | [ ] | [ ] | | [X] | [X] | [ ] | | | |
| atd | [ ] | [X] | [X] | [ ] | [ ] | | [X] | [X] | [ ] | | |
| atftpd | [ ] | [X] | [X] | [ ] | [ ] | | [X] | [X] | [ ] | | | |
| avahi-daemon | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| beef-xss | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| binfat-suppo | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| bluetooth | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| console-s | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| crond | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| cryptat | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | |
| cryptiss | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| darkat | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| dbus | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| desktop-7 | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| dracut | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| exim4 | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| gdm1 | [ ] | [X] | [X] | [ ] | [ ] | | | | | | | | |
| gnomap | [ ] | [ ] | [X] | [X] | [ ] | | | | | | | | |

使用方向键移动。'n': 下页，'p': 上页，空格：切换开启/关闭

如你所见，我们可以在这里对服务进行安排。要返回终端退出程序，只需按 Q 键。如果你不想对此配置进行安排只想查看列表，可以使用 `sysv-rc-conf --list` 命令。

```bash
root@kimal:~# sysv-rc-conf --list
anacron  2:on  3:on  4:on  5:on
apache2   0:off 1:off 2:off 3:on  4:on  5:off 6:off
arpatch  0:off 1:off 2:on  3:on  4:on  5:off 6:off
atd      0:off 1:off 2:on  3:on  4:on  5:off 6:off
atftpd    0:off 1:off 2:off 3:off 4:off 5:off 6:off
avahi-daemon 0:off 1:off 2:off 3:off 4:off 5:off 6:off
beef-xss  0:off 1:off 2:off 3:off 4:off 5:off 6:off
binfat-suppo 2:off 3:on  4:on
bluetooth 0:off 1:off 2:off 3:off 4:off 5:off 6:off
console-s 0:off 1:off 2:off 3:off 4:off 5:off 6:off
crond 0:off 1:off 2:off 3:off 4:off 5:off 6:off
cryptat 0:off 1:off 2:off 3:off 4:off 5:off 6:off
cryptiss 0:off 1:off 2:off 3:off 4:off 5:off 6:off
darkat 0:off 1:off 2:off 3:off 4:off 5:off 6:off
dbus 0:off 1:off 2:off 3:off 4:off 5:off 6:off
desktop-7 0:off 1:off 2:off 3:off 4:off 5:off 6:off
dracut 0:off 1:off 2:off 3:off 4:off 5:off 6:off
exim4 0:off 1:off 2:off 3:off 4:off 5:off 6:off
gdm1 0:off 1:off 2:off 3:off 4:off 5:off 6:off
gnomap 2:off 3:off 4:off
```

