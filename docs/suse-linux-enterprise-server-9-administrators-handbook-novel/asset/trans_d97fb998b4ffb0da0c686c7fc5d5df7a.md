
## 注记
经常，SUID 位被系统应用程序或脚本使用，以便进程可以作为 root 访问系统资源。另一方面，SGID 位并不经常被系统程序使用，但主要被系统管理员用来设置共享目录。

## 警告
您应密切监控设置了 SUID 和/或 SGID 位的程序和脚本。黑客利用某些漏洞后留下 root SUID 程序作为后门的情况相当常见。关键在于使用 Tripwire（参见第 12 章，“入侵检测”）、Bastille 和 seccheck（参见第 13 章，“系统安全”）等应用程序并跟踪您的系统！

要设置这三种特殊权限位中的任何一种，chmod 需要第四位数字。此值指定为最显著的（最左边的）数字，其可能的值列于表 6.8 中。例如，chmod 1777 testDir 表示所有者、组和其他用户对 testDir 具有完全的读、写和执行权限，并且世界权限的粘滞位也被设置。ls 输出看起来像这样：

```
Athena:/home/admin # chmod 1777 testDir
Athena:/home/admin # ls -l testDir
drwxrwxrwt  2 root admin 48 2005-01-19 17:35 testDir
```

## 表 6.8
### 特殊权限模式代码

| 八进制数字 | 二进制值 | 描述 |
|---:|---:|---|
| 0 | 000 | SUID、SGID 和粘滞位均未设置 |
| 1 | 001 | 粘滞位已设置 |
| 2 | 010 | SGID 位已设置 |
| 3 | 011 | SGID 和粘滞位已设置 |
| 4 | 100 | SUID 位已设置 |
| 5 | 101 | SUID 和粘滞位已设置 |
| 6 | 110 | SUID 和 SGID 位已设置 |
| 7 | 111 | SUID、SGID 和粘滞位均已设置 |

使用文本值的相应 chmod 命令是 chmod a+rwx,o+t testDir。ls 显示的特殊模式符号反映了对应的执行位是否也被设置。例如，如果粘滞位已设置但世界的可执行位未设置，则显示符号 T 而不是 t。表 6.9 总结了根据执行位设置显示的特殊模式符号。

## 表 6.9
### 特殊权限文本表示

|  | 执行位未设置 | 执行位已设置 |
|---|---|---|
| SUID | `---S------` | `---s------` |
| SGID | `------S---` | `------s---` |
| Sticky | `---------T` | `---------t` |

> **注记**
> 
> 当您使用 chmod 中的文本值设置这些特殊权限模式时，请使用小写字符，例如 s 和 t，而不是大写字符。大小写区分由 ls 用于显示不同的权限组合。

## SUID/SGID 的安全影响
值得讨论 Linux/Unix 世界中 SUID 和 SGID 程序和脚本的需求，即使它们可能被黑客留下的特洛伊木马。 首先，考虑 /etc/passwd 文件。只有文件所有者（root）对其具有写访问权限（rw-r--r--）。然而，作为普通用户，您可以使用 passwd 和 chsh 命令以非常有限的方式修改此文件的内容。

对 /usr/bin/passwd 程序的权限位检查显示，文件所有者的 SUID 和执行位均已设置（rwsr-xr-x）。这表明 passwd 实用程序是一个 root SUID 程序。它之所以是 SUID 程序，是因为权限位中的 s 标志，而它之所以是 root SUID 程序，是因为 root 拥有该文件。因此，当任何人运行 passwd 程序时，用户暂时获得 root 用户的权限——但仅限于程序执行期间，并且仅限于该程序内部。没有这种机制，许多系统管理任务会因安全影响而变得不必要地复杂。例如，您如何有效地保护 /etc/shadow 文件，同时允许用户更新自己的密码？

另一方面，SUID API 调用可用于降低用户的权限而不是提高权限。例如，对于基于 IP 的服务要绑定到特权端口之一，它需要以 root 身份运行。然而，在端口绑定后，应用程序不再需要 root 权限；它可以使用 SUID 调用将进程的 UID 更改为非特权用户。或者一个程序可能以 root 身份运行，但出于安全原因，它可以生成以较低特权级别运行的进程。一个例子是 Apache Web 服务器；其 `suexec` 实用程序（参见 http://httpd.apache.org/docs-2.0/suexec.html）以用户 `wwwrun` 和组 `www`（SLES 9 上的默认设置）而不是作为主 Apache 进程的所有者执行 CGI 和 SSI 程序，主 Apache 进程通常以 root 运行。

## 注记
对于应用程序成为 SUID 程序，它必须进行 SUID 或类似的 API 调用（SUID 调用有多种变体），并且文件权限位必须相应设置。仅仅在程序上设置 SUID 位并不会自动使其成为 SUID 程序。

组所有权有相同的机制。例如，如果您检查 `/usr/bin/uucp` 的权限，您会看到用户和组的 s 标志（`r-sr-sr-x`）。因此，当您运行 uucp（Unix-to-Unix CoPy）时，您暂时获得拥有用户（uucp）和拥有组（uucp）的权利。

SUID 脚本通常比 SUID 程序更危险。这在很大程度上是由于运行脚本首先会调用一个 shell。如果脚本是 SUID root，则调用的 shell 将以 root 权限运行。在 shell 被调用但脚本运行之前，可以中断内核并替换 shell 即将执行的文件。被替换的文件可能是任何可执行的 shell 脚本，包括另一个 shell（在这种情况下将是 root shell）。由于这些安全影响，Linux 系统早已禁用了 SUID/SGID shell 脚本的支持。如果您确实需要一个执行 SUID/SGID 的脚本，请使用启用了 taint 模式的 Perl 开发它。

## 提示
当 Perl 脚本文件设置了其 SUID 和/或 SGID 位时，Perl 解释器会自动进入偏执模式并执行一系列特殊安全检查以检测可能受污染的数据，例如验证 PATH 变量中指定的目录是否不可被他人写入。您可以通过在脚本开头使用 `-T` 命令行标志显式启用此 taint 模式，即 `#!/usr/bin/perl -T`。该标志强烈建议用于服务器程序以及代表他人运行的任何程序，例如 CGI 脚本。当 taint 模式打开时，它将保持打开状态，直到脚本结束。

您可以使用 Tripwire、Bastille 和 seccheck 等应用程序自动搜索和报告可疑的 SUID/SGID 程序和脚本。

但如果您是一位刚到客户现场进行安全审计的顾问，以下命令可能很有用：

- 获取所有 SUID 或 SGID 文件（程序和脚本）的列表，请使用以下命令：

```
# find / -type f -perm +ug=s -exec ls -l {} \;
```

- 要查找所有 root SUID 文件，请使用此命令：

```
# find / -type f -owner root -perm +u=s -exec ls -l {} \;
```

- 仅通过查看文件中的前两个字节来检查 SUID 或 SGID 脚本，以查看它们是否为 #!（所谓的魔数），表明它是一个脚本文件：

```
# find / -type f -perm +ug=s -print0 2> /dev/null | \
perl -n0e 'chomp; open(FILE, $_); read(FILE,$magic,2); \
print "$_\n" if $magic eq "#!"; close(FILE);'
```

## 提示
将系统上的 SUID 和 SGID 程序数量保持在最低限度。这里的主要关注点应放在 root SUID 程序上。非 root SUID 和 SGID 程序风险较小，但仍可能成为安全漏洞的来源。

## 提示
如果您不确定程序或脚本是否应设置其 SUID/SGID 位，或您已确定一个或多个 SUID 文件或目录是不必要的，请使用 chmod u-s,g-s name 禁用它们。请确保记录您所做的修改，以便在需要时可以稍后恢复更改。

## SGID 和文件共享
使用 SLES，只要用户是拥有文件或目录组所有权的组的成员，他或她就可以根据组权限设置访问它；这并不重要该用户的首要组是否不同。例如，/usr/share/projectDestiny 目录的组所有者是 destiny，并且组已被授予读、写和执行权限。用户 carol 是 users、audio、video 和 destiny 组的成员，她的首要组是 users。只要 carol 是 destiny 组的成员，她将完全访问 projectDestiny 目录。其他用户也是如此。然而，这有一个管理上的不足和一个安全缺陷。
