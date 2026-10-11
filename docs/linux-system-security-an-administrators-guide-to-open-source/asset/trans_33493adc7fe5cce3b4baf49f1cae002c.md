

## 表 13.7 tiger 命令行选项

| 选项 | 用途 |
|---|---|
| -v | 打印 tiger 版本信息。 |
| -B | 在命令行中指定 tiger 基础目录。 |
| -1 | 指定 tiger 日志目录。 |
| -w | 指定 tiger 工作目录。 |
| -b | 指定 tiger 二进制文件目录。 |
| -c | 指定 tigerrc 文件。 |
| -e | 生成详细报告（在每个消息 ID 出现的地方插入完整说明）。 |
| -E | 生成与默认报告类似的报告，但生成一份包含输出中引用的每个消息 ID 完整文本的独立报告。 |
| -S | 服务器检查。意味着检查服务器及其上配置的无盘客户端。在非 SunOS 4 系统上可能效果不佳。 |
| -O | 指定操作系统。 |
| -A | 指定架构。 |
| -R | 指定操作系统版本。 |
| -t | 指定 tiger 测试模式。 |

# 运行时操作概述

tiger 已预先配置以支持多种操作系统。这些信息的大部分存储在 systems 目录中（通常只有开发人员才需要对其进行修改）。当运行 tiger（或独立的 tiger 脚本）时，scripts/config 可执行文件会尝试定位最合适的配置文件，但如果找不到完全匹配的文件，它将使用更通用的配置信息。所使用的配置会在输出开头报告。config 脚本还会解析命令行选项。输出示例如示例 13-3 所示。

**示例 13-3** *tiger* 显示运行时使用的配置文件。

```
# scripts/check_perms
Configuring ...  
Will try to check using config for 'i686' running Linux 2.0.36 ...  
--CONFIG-- [con005c] Using configuration files for Linux 2.0.36.  
Using configuration files for generic Linux 2.  
Not all checks may be performed.
```

如果找不到您的特定操作系统或操作系统版本，您可以尝试添加支持。参见第 375 页的 *修改 tiger*。

此时，配置工作应当已完成，准备从命令行运行 *tiger*。我们也可以单独运行这些脚本，如示例 13-4 所示。（现在去找找 Joe，看看他在忙什么！）我们将在下一节中更详细地描述这些脚本。

## 示例 13-4 独立运行 check_rhosts

```
# scripts/check_rhosts
Configuring...
Will try to check using config for 'i686' running Linux 2.0.36...
--CONFIG-- [con005c] Using configuration files for Linux 2.0.36. Using
configuration files for generic Linux 2.
Not all checks may be performed.
# Performing check of /etc/hosts.equival and .rhosts files...
# Checking accounts from /etc/passwd...
--WARN-- [rcmd013w] User joe's .rhosts file contains an attempted comment
line
--FAIL-- [rcmd002f] User joe's .rhosts file has a '+' for host field.
#
```

# tiger 脚本

*tiger* 旨在检查系统的基本配置；这包括文件和目录权限检查、所有权检查、交叉引用检查等。执行这些检查的脚本可以通过主 *tiger* 脚本运行（如果在 *tiger.rc* 文件中配置），或者在您想要运行特定检查时单独运行。一些脚本具有辅助实用程序，这些实用程序无法单独运行。本节将检查执行这些检查的脚本。

*check_accounts*。此脚本检查用户账户中的问题。它会报告那些可能通过使用包含命令的 .forward 文件、.rhosts 文件或 *cron* 作业来使用的被禁用的账户。它还会检查密码文件中的问题，包括无密码账户、UID 为 0 的非 root 账户以及配置错误（例如密码文件中尝试添加注释）。此外，*check_accounts* 还会查找非零长度的 .hushlogin 文件（有时入侵者使用它来隐藏信息），以及主目录上可能导致他人添加或删除文件的权限问题。这些项目的存在可能表明配置错误，允许被禁用的账户继续使用，或暴露出被入侵的迹象。*check_accounts* 的运行时间取决于您系统中的账户数量。示例 13-5 展示了 *check_accounts* 的运行示例。

*check_aliases*。*check_aliases* 脚本检查 sendmail 程序使用的别名，并报告潜在漏洞和配置错误。

## 示例 13-5 运行 check_accounts 脚本。

```
# scripts/check_accounts
Configuring....
Will try to check using config for 'i686' running Linux 2.0.36....
--CONFIG-- [con005c] Using configuration files for Linux 2.0.36. Using
configuration files for generic Linux 2.
Not all checks may be performed.

# Performing check of user accounts....
# Checking accounts from /etc/passwd.
-WARN-- [acc000w] Login ID adm is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID bin is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID daemon is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc000w] Login ID ftp is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID games is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc000w] Login ID gopher is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID lp is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc000w] Login ID mail is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID news is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID nobody is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc000w] Login ID operator is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc001w] Login ID uucp is disabled, but still has a valid shell
(/bin/sh).
-WARN-- [acc006w] Login ID lp's home directory (/var/spool/lpd) has group
'daemon' write access.
-WARN-- [acc006w] Login ID mail's home directory (/var/spool/mail) has group
'mail' write access.
```

该脚本将报告已知问题，例如 uucode 别名的存在，对由非 root 用户拥有或可写的包含文件的引用，或对不存在的文件的引用，以及不存在或由非 root 用户拥有或可写的程序别名的存在。如果包含的别名或程序文件由非 root 用户拥有或可写，则可能允许非 root 用户以 root 权限执行命令。

**check_anonftp.** 此脚本验证匿名 FTP 设置是否正确。将检查 FTP 用户密码文件中主目录字段的错误，这些错误可能导致机器被入侵；并检查 FTP 目录层次结构中文件的属主和权限问题。如果 FTP 未正确配置，可能会获得对系统的未经授权访问。

**check_cron.** check_cron 脚本检查实际 cron 命令及其路径中包含的目录组件的属主和权限。如果用户的 cron 作业由非执行该作业的用户或非系统账户拥有，或者如果其中任何组件可由他人写入，则该命令将被报告为该账户的潜在漏洞。cron 作业的属主无法控制文件的完整性，执行 cron 作业可能导致系统被入侵。

check_embedded。check_embedded 脚本搜索由 root 和/或其他用户引用的文件或二进制文件中包含的嵌入式路径名，并报告潜在弱点。如果嵌入式名称又指向另一个嵌入式文件名或二进制文件，则递归执行嵌入式名称检查，直到检查完所有名称或达到最大递归深度（一个可配置选项）为止。这里的弱点是指文件或二进制文件由非系统账户拥有或可写。

此脚本有许多配置选项（参见第 352 页的表 13.6）。您可以选择仅检查 SUID 二进制文件、所有二进制文件或所有常规文件。您可以选择为 root 或所有用户执行此检查，或者您可以配置允许拥有正在检查的文件的用户和组（限制越多，安全性越高），并指定递归深度级别。

当单独运行时，check_embedded 会引用 tiger systems 目录中的 embedlist，并检查其中列出的文件中的嵌入式名称。当与其他 tiger 脚本一起运行时，除了 embedlist 之外，还会生成并检查由 root 或其他用户引用的文件或二进制文件列表（根据配置选项）。

此脚本运行可能需要几分钟。如果您的系统内存很少，它在尝试执行递归检查时可能会挂起；您可能需要限制其搜索的深度。示例 13-6 展示了 check_embedded 的输出。

![](img/7933c44717ab0711177ea7153f959fc5_404_0.png)

check_exports。check_exports 脚本检查文件系统（如果存在）从您的系统导出的方式，并报告可能存在的配置错误和漏洞。导出文件系统时可以使用许多选项，如果不加小心地使用，您的文件可能会被未经授权的人查看或修改。

如果将匿名 ID 设置为 0，check_exports 脚本将发出警告，这可能会导致未经授权访问。它会报告由于将文件系统以 root 权限导出到其他机器或授予所有主机读或写访问权限而造成的任何漏洞。它还会标记对 / 或 /usr 文件系统的不安全导出。

