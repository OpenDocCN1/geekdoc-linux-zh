
## 写权限中的漏洞

从文件中移除写权限非常容易。例如，如果你想让 `license.txt` 文件变成“只读”，可以使用以下命令来移除该文件的写权限：

```
$ chmod a-w license.txt
```

但是，文件的所有者仍然可以进行修改。这在 gedit 等图形界面文本编辑器中不会生效。即使在 nano 文本编辑器中也不会生效。然而，如果在 vi 文本编辑器中进行了修改，该文件的所有者可以使用感叹号（!）（即 bang 字符）来覆盖缺少写权限的限制。换句话说，在 vi 编辑器中，文件的所有者可以运行以下命令来覆盖缺少写权限的限制：

```
:w!
```

## 基本的用户和组概念

Linux 和 Unix 一样，通过用户和组进行配置。每个使用 Linux 的人都被设置了一个用户名，即使只是“guest”（访客）也是如此。甚至还有一个名为“nobody”的标准用户。请查看 `/etc/passwd`。该文件的一个版本如图 4-1 所示。

![](img/9139201cfcaf4292284a0eed074928e5_202_0.png)

```
games:x:12:100:games:/usr/games:/sbin/nologin
gopher:x:13:30:gopher:/var/gopher:/sbin/nologin
ftp:x:14:50:FTP User:/var/ftp:/sbin/nologin
nobody:x:99:99:Nobody:/:/sbin/nologin
dbus:x:81:81:System Message Bus:/:/sbin/nologin
rpc:x:32:32:rpcbind Daemon:/var/cache/rpcbind:/sbin/nologin
avahi-autoipd:x:170:175:Avahi IPv4LL Stack:/var/lib/avahi-autoipd:/sbin/nologin
nscd:x:28:28:NSCD Daemon:/sbin/nologin
... [passwd listing continues]
```

如图所示，`/etc/passwd` 文件中列出了各种各样的用户名。甚至许多 Linux 服务，如邮件、新闻、ftp 和 apache，都有自己的用户名。无论如何，`/etc/passwd` 文件遵循特定的格式，将在第 8 章中详细介绍。目前，请注意该文件中显示的唯一普通用户是 exam prep 和 michael，他们的用户 ID（UID）和组 ID（GID）分别是 500 和 501，并且他们的主目录与他们的用户名相匹配。下一个用户将获得 UID 和 GID 502，依此类推。

这种 UID 和 GID 的匹配是基于 Red Hat 用户私有组方案。现在运行 `ls -l /home` 命令。输出应该类似于以下内容。

```
drwx------. 4 exam prep exam prep 4096 Dec 15 16:12 exam prep
drwx------. 4 michael michael 4096 Dec 16 14:00 michael
```

请注意权限。基于本章前面描述的 rwx/ugo 概念，只有指定的用户所有者才能访问其主目录中的文件。

## umask（文件模式创建掩码）

umask 在 Red Hat Enterprise Linux 中的工作方式可能令人惊讶，特别是如果你来自不同的类 Unix 环境。你无法配置 umask 以允许自动创建的新文件自动获得执行权限。这有助于增强安全性：如果拥有执行权限的文件较少，攻击者（cracker）可用于运行程序以突破你系统的文件也就更少。

> 在 Linux 世界里，黑客（hacker）是一个好人，只是想创建更好的软件。而破解者（cracker）是想出于恶意目的入侵你系统的人。在计算机安全领域，这些术语分别可以翻译为“白帽子黑客”和“黑帽子黑客”。

每次你创建新文件时，默认权限都基于 umask 的值。在过去，umask 的值会抵消文件数字权限的值。例如，如果 umask 的值是 000，那么该用户创建的任何文件的默认权限曾经是 777 – 000 = 777，这意味着所有用户都具有读、写和执行权限。但现在它们是 666，因为普通的文件不再能获得执行权限。另一方面，目录需要执行权限，以便其中包含的任何文件都能被读取。

当你输入 umask 命令时，命令会返回一个由四个数字组成的输出，例如 0245。截至本文撰写时，umask 输出中的第一个数字始终是 0，并且不使用。将来，这个第一个数字可能会用于允许自动包含 SUID 或 SGID 位的新文件。

此外，无论 umask 的值如何，在 Red Hat Enterprise Linux 中，新文件都不能再自动以执行权限创建。换句话说，umask 值为 0454 与 0545 在新文件上产生的权限是相同的。你需要使用诸如 chmod 之类的命令来设置特定文件的执行权限。

## 默认 umask

考虑到这一点，默认的 umask 是由 `/etc/bashrc` 文件驱动的，特别是以下代码段，它根据 UID 的值来驱动 umask 的值：

```
if [ $UID -gt 199 ] && [ "`id -gn`" = "`id -un`" ]; then
  umask 002
else
  umask 022
fi
```

换句话说，UID 为 200 及以上的用户账户的 umask 为 002。

相比之下，UID 低于 200 的用户的 umask 为 022。在 RHEL 6 中，诸如 adm、postfix 和 apache 之类的服务用户具有较低的 UID；这主要影响为此类服务创建的日志文件的权限。当然，root 管理用户具有最低的 UID 0。默认情况下，为此类用户创建的文件具有 644 权限；为此类用户创建的目录具有 755 权限。

相比之下，普通用户的 UID 为 500 及以上。此类用户创建的文件通常具有 664 权限。此类用户创建的目录通常具有 775 权限。

## 更改权限和所有权的命令

帮助你管理文件权限和所有权的关键命令是 chmod、chown 和 chgrp。在接下来的小节中，你将学习如何使用这些命令来更改权限以及拥有特定文件甚至一系列文件的用户和组。

如果你在对目录使用上述任何命令时指定了 -R 开关，它会递归地应用更改。这些更改将应用于该目录中的所有文件，包括所有子目录。递归意味着这些更改也会应用于每个子目录中的文件，依此类推。

## chmod 命令

chmod 命令使用与所有者、组和其他人关联的权限的数字值。在 Linux 中，权限被分配以下数字值：r = 4，w = 2，x = 1。例如，如果你疯狂到想要赋予所有用户对磁盘的读、写和执行权限，你可以运行 `chmod 777 /sbin/fdisk` 命令。chown 和 chgrp 命令调整与引用文件关联的用户和组所有者。

chmod 命令很灵活。你并不总是必须使用数字。例如，以下命令为 Ch3Lab1 文件的用户所有者设置执行权限：

```
# chmod u+x Ch3Lab1
```

注意 u 和 x 如何遵循关联的 RHCSA 目标中指定的 ugo/rwx 格式。解释一下，此命令为文件的用户所有者（用 u 表示）添加（用加号表示）执行权限（用 x 表示）。

这些符号可以组合使用。例如，以下命令禁用本地文件 special 的组所有者和所有其他用户的写权限：

```
# chmod go-w special
```

虽然你可以使用 chmod 命令中的三种用户类型，但这并不是必须的。如第 3 章的实验中所述，以下命令使引用的文件对所有用户可执行：

```
# chmod +x Ch3Lab2
```

对于 SUID、SGID 和粘滞位，有一些特殊的选项可供选择。如果你选择使用数字位，这些特殊位也被分配了数字值，其中 SUID=4，SGID=2，粘滞位=1。例如，以下命令配置 SUID 位。它为名为 testfile 的文件设置了用户所有者的 rwx 权限、组所有者的 rx 权限以及其他用户的 r 权限：

```
# chmod 4754 testfile
```

如果你更喜欢使用 ugo/rwx 格式，以下命令为本地 testscript 文件激活 SGID 位：

```
# chmod g+s testscript
```

以及以下命令为 /test 目录开启粘滞位：

```
# chmod o+t /test
虽然本节描述的 chmod 命令假设更改是由 root 管理用户进行的，但这并不总是必须的。文件的用户所有者被允许更改与该文件关联的权限。

## chown 命令

chown 命令可用于修改拥有文件的用户。例如，查看我为本章创建的第一张图片的所有权，基于 `ls -l` 命令：

```
-rw-r--r--. 1 michael exam prep 855502 Oct 25 14:07 F04-01.tif
```

此文件的用户所有者是 michael；此文件的组所有者是 exam prep。

显示的 chown 命令将用户所有者更改为用户 elizabeth：

```
# chown elizabeth F04-01.tif
```

你可以使用 chown 做更多事情；例如，以下命令将引用的文件用户和组所有者更改为用户 donna 和组 supervisors，假设该用户和组已经存在。

```
# chown donna.supervisors F04-01.tif
```

## chgrp 命令

你可以使用 chgrp 命令更改文件的组所有者。例如，以下命令将引用的 F04-01.tif 目录的组所有者更改为名为 project 的组（假设它存在）：

```
# chgrp project F04-01.tif
```

