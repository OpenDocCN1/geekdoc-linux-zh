
## 列表 473 - 列出已加载的驱动程序

一旦我们收集了模块列表并识别出我们想要获取更多信息的模块（例如上面示例中的 `libata`），就可以使用 `modinfo` 来查找该特定模块的更多信息。我们需要注意的是，这需要完整路径才能运行。

```
joe@debian-privesc:-$ /sbin/modinfo libata
filename: /lib/modules/4.19.0-21-amd64/kernel/drivers/ata/libata.ko
version: 3.00
license: GPL
description: Library module for ATA devices
author: Jeff Garzik
srcversion: 00E4F0B13BA2AAF8137BF
depends: scsi_mod
retpoline: Y
intree: Y
name: libata
ver: 4.19.0-21-amd64 SMP mod_unload modversions
sig_id: PKCS#7
signer: Debian Secure Boot CA
sig_key: 4B6E:F5:AB:CA:C6:98:25:17:8E:05:24:86:7C:CB:C0:53:1F:8C
```

### 列表 474 - 显示关于模块的额外信息

一旦获取了驱动程序和版本的列表，我们就能更好地找到相关的漏洞。

在本模块的后后部分，我们将探索各种权限提升的方法。然而，在本节中，我们应该涵盖几个特定的枚举项，这些项可能会揭示权限提升的“捷径”。

除了之前描述的 `rwx` 文件权限外，还有两种额外的特殊权限适用于可执行文件：`setuid` 和 `setgid`。它们用字母 `"s"` 表示。

如果设置了这两种权限，权限位中会出现大写或小写的 `"s"`。这允许当前用户以所有者权限（`setuid`）或所有者组权限（`setgid`）执行该文件。

当运行可执行文件时，它通常会继承运行它的用户的权限。但是，如果设置了 `SUID` 权限，二进制文件将以文件所有者的权限运行。这意味着如果一个二进制文件设置了 `SUID` 位且由 `root` 所有，任何本地用户都能够以提升后的权限执行它。

当用户或系统自动脚本启动 `SUID` 时，它会继承启动脚本的 `UID/GID` 作为有效 `UID/GID` (`euid`, `egid`)，这是操作系统用于验证并授予特定操作权限的实际用户。

任何能够成功绕过 `setuid root` 程序的用户都可以有效地渗透进 `root` 用户，并获得系统上的所有权限。渗透测试人员在获得系统访问权限后，经常搜索此类文件，作为提升权限的手段。

我们可以使用 `find` 来搜索标记为 `SUID` 的二进制文件。在这种情况下，我们从根目录 (`/`) 开始搜索，寻找设置了 `SUID` 位（`-perm -u=s`）的文件（`-type f`），并丢弃所有错误信息（`2>/dev/null`）。

```
joe-debian-privesc:-$ find / -perm -u=s -type f 2>/dev/null
/usr/bin/chsh
/usr/bin/fusermount
/usr/bin/chfn
/usr/bin/suid
/usr/bin/sudo
/usr/bin/pkexec
/usr/bin/ntfs-3g
/usr/bin/gpasswd
/usr/bin/newgrp
/usr/bin/bwrap
/usr/bin/vi
/usr/bin/umount
/usr/bin/mount
/usr/lib/polkit-agent-1/polkit-agent-helper-1
/usr/lib/xorg/wrap
/usr/lib/ject/decrypt-get-device
/usr/lib/openssh/ssh-keysign
/usr/lib/spice-gtk/spice-client-glib-usb-acl-helper
/usr/lib/dbus-1.0/dbus-daemon-launch-helper
/usr/sbin/ppdd
```

### 列表 475 - 搜索 SUID 文件

在这种情况下，命令找到了 `SUID` 二进制文件。对 `SUID` 二进制文件的探索将取决于多个因素。例如，如果 `/bin/cp`（复制命令）是 `SUID`，我们就可以以 `root` 身份复制并覆盖如 `/etc/passwd` 等敏感文件。

可以在 `g0tm1lk` 编写的汇编 `548` 中找到全面的权限提升技术列表，以及其他 `549` 个更及时的 `550` 资源。

在手动枚举 Linux 权限提升技术涵盖主要概念后，我们将在接下来的章节中学习如何批量自动化这一过程。

## 17.1.3 自动化枚举

正如上一节所学到的，Linux 系统包含大量可用于进一步攻击的信息。然而，收集这些详细信息可能非常耗时。坦率地说，我们可以使用各种脚本来自动化此过程。

为了获取目标系统的初始基线，我们可以在类 Linux 的 UNIX 变体中使用 `unix-privesc-check`。这个 Bash 脚本预装在我们本地 Kali 机器的 `/usr/bin/unix-privesc-check` 中，它执行许多检查以找到任何可以被用于本地权限提升的系统错误配置。我们可以通过不带任何参数运行该脚本来查看该工具的详情。

### OffSec

`SHLV=1`

`XDG_SESSION_ID=35`

`LC_TYPE=UTF-8`

`SSH_RUNTIME_DIR=/run/user/1000`

`SSH_CLIENT=152.168.118.2 59800 22`

`PATH=/usr/local/bin:/usr/bin:/usr/local/games:/usr/games`

`DBUS_SESSION_BUS_ADDRESS=unix:path=/run/user/1000/bus`

`MAIL=/var/mail/joe`

`SSH_TTY=/dev/pts/1`

`OLDPw=/home/joe/.cache`

`-_=/usr/bin/env`

## 使用 Kali Linux 进行渗透测试

有趣的是，`SCRIPT_CREDENTIALS` 变量包含一个类似于密码的值。为了确认我们处理的是一个持久变量，我们需要检查 `.bashrc` 配置文件。

```
joe@debian-privesc:~$ cat .bashrc
# ~/.bashrc: executed by bash(1) for non-login shells.
# see /usr/share/doc/bash/examples/startup-files (in the package bash-doc)
# for examples

# If not running interactively, don't do anything
case $ - in
  *) *;
  *) return)
esac

# don't duplicate lines or lines with space in the history.
# See bash(1) for more options
export SCRIPT_CREDENTIALS="lab"
HISTCONTROL=ignorebb
...
```

### 列表 479 - 检查环境变量

从上述内容，我们可以确认该持有变量在用户 shell 启动时被导出（`exported`）了。

> 在环境变量中存储明文密码不被认为是一种安全的最佳实践。为了与交互式脚本进行安全身份验证，建议采用公钥认证并使用密码口令保护私钥。

### 列表 480 - 检查 .bashrc

让我们首先尝试通过输入新发现的密码来提升权限。

```
joe@debian-privesc:~$ su - root
Password:
root@debian-privesc:~# whoami
root
```

### 列表 481 - 使用泄露的凭据成为 'root' 用户

`PWK - Copyright ©2023 OffSec Services Limited. All rights reserved.`

`547 Made in Morocco`

## 使用 Kali Linux 进行渗透测试

我们已经成功获得了 `root` 权限，现在让我们尝试另一种基于环境变量凭据发现的权限提升路径。

与其直接针对 `root` 账户，不如尝试获取在之前章节节中发现的 `eve` 用户的访问。

利用我们对脚本凭据的了解，我们可以基于已知密码构建一个自定义字典，尝试对 `eve` 账户进行暴力破解。

我们可以使用 `crunch` 命令行工具来生成自定义词汇列表。我们将最小和最大长度设置为 `6` 个字符，使用 `-t` 参数指定模式，然后将前几个字符硬编码为 `Lab`，后面接三个数字。

```
kali@kali:~$ crunch 6 6 -t Lab%%%%
```

### 列表 482 - 为暴力破解攻击生成单词列表

然后我们可以验证生成的单词列表的内容：

```
kali@kali:~$ cat wordlist
Lab000
Lab001
Lab002
Lab003
Lab004
Lab005
Lab006
Lab007
Lab008
Lab009
```
