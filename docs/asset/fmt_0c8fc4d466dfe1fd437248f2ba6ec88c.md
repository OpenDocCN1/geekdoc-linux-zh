
使用这种方法，你可以轻松地开启或关闭一个位。`+` 运算符开启位，`-` 关闭位，`=` 关闭除命令指定位外的所有位。运算符后的参数是要要开启或关闭的位。

## 总结

在本章中，你学习了关于文件安全的基础知识以及如何在 Linux 系统上实现它。你学习了文件类型、文件权限以及如何更改它们。你学习了新文件的默认权限从何而来，以及如何更改它们。

在下一章中，你将通过探索来完成对文件权限的学习。

# 第 4 章

- 理解 SUID/SGID
- 理解 SUID/SGID（设置权限）
- 理解 SUID/SGID（以及文件）
- 理解等（etc.）

等等实现此操作的另一种方法是将程序设置为 SGID。SGID 位的作用完全相同，强制程序以特定组运行。通常，对于希望使用个人程序的的用户来说，这将是更好的响应。

在目录上，SUID 和 SGID 位具有不同的含义。最常用的用法是在用户共享文件的公共目录上，允许用户更新。将目录设置为 SGID，所有创建或修改的文件将属于目录的组。假设“其他”用户对该目录没有权限，则所有文件将仅允许该组的用户访问。

另一个重要的位是被称为“粘性位”（sticky bit）的位。你将看到如何设置 SUID 和 SGID 位。粘性位的设置方法与其他位相同。在可执行文件上，此位告诉操作系统将文本保存在交换设备上而不是保留在内存中。在目录上，它可以防止所有者以外的用户更改文件。其他人可以读取文件，但不能更改。你将在下文中查看该位的使用方法和位置。

# 理解 SUID/SGID 的危险

在系统中散布 SUID 程序会引发麻烦。正如前面提到的，某些程序必须是 SUID，普通用户才能使用。但必须对这些程序列表进行审查。

任何允许用户执行任意命令或跳出到命令行提示符的程序都不是 SUID 状态的候选者。但不应作为指南。如果找不到某个特定文件设置为 SUID 的合理理由，那么它就不应该是 SUID。此外，用户在其主目录下拥有一个 SUID root 程序也是没有理由的。

运行以下命令：

```
find -perm u+s -exec ls -l (*) \;
```

# 第 4 章：SUID/SGID 设置（文件/目录）

产生以下输出：

```
| -r-sr-xr-x 1 root root 2105164 Aug 30 07:25 /usr/local/bin/vmware |
| -rWS-x--x 1 root root 606031 Jul 22 20:07 /usr/local/bin/ssh |
| ---s--xr-x 1 root bin 1647592 Jul 25 13:34 /usr/local/bin/xlock |
| -rWsr-xr-x 1 root root 285151 Aug 21 17:23 /usr/local/sbin/mstr |
| -rWsr-xr-x 1 root root 17134 Jul 27 10:55 /usr/X11R6/bin/cardinfo |
| -rWS-x--x 1 root root 7150 Jul 27 20:25 /usr/X11R6/bin/Xwrapper |
| -r-sr-xr-x 1 root root 177280 Jul 28 00:32 /usr/bin/lp1q |
| -r-sr-xr-x 1 root root 235672 Jul 28 00:32 /usr/bin/lprm |
| -r-sr-xr-x 1 root root 171060 Jul 28 00:32 /usr/bin/iprm |
| -r-sr-xr-x 1 root root 105122 Jul 27 19:17 /usr/bin/login |
| -r-sr-xr-x 1 root root 7840 Jul 27 19:16 /usr/bin/rsh |
| -r-sr-xr-x 1 root bin 8703 Jul 27 19:16 /usr/bin/passwd |
| -rWS-x--x 2 root root 556924 Jul 28 03:05 /usr/bin/suidperl |
| -rWS-x--x 2 root root 556924 Jul 28 03:05 /usr/bin/perl15.00502 |
| -r-sr-xr-x 1 root root 387522 Jul 27 19:15 /usr/bin/chage |
| -r-sr-xr-x 1 root root 282424 Jul 27 29:15 /usr/bin/expiry |
| -r-sr-xr-x 1 root root 32268 Jul 27 19:16 /usr/bin/gpasswd |
| -r-sr-xr-x 1 root root 280320 Jul 27 20:15 /usr/bin/newgrp |
| -r-sr-xr-x 1 root root 13872 Jul 27 20:27 /usr/bin/chfn |
| -r-sr-xr-x 1 root root 13712 Jul 27 20:27 /usr/bin/chsh |
| -r-sr-sr-x 1 uucp uucp 125852 Jul 27 20:53 /usr/bin/cu |
| -r-sr-sr-x 1 uucp uucp 91568 Jul 27 20:53 /usr/bin/uucp |
| -r-sr-sr-x 1 uucp uucp 38492 Jul 27 20:53 /usr/bin/uanname |
| -r-sr-sr-x 1 uucp uucp 99656 Jul 27 20:53 /usr/bin/uastat |
| -r-sr-xr-x 1 uucp uucp 92720 Jul 27 20:53 /usr/bin/uux |
| ---s--xr-x 1 root root 23420 Jul 27 19:18 /usr/sbin/crontab |
| -rWsr-xr-x 1 root root 173290 Jul 28 00:32 /usr/sbin/lppic |
```
