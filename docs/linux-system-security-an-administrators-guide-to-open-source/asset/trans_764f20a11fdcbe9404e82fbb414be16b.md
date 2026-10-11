

## 表 9.5 sudo 选项（续）

| 选项 | 描述 |
| :--- | :--- |
| -r *realm* | 指定 Kerberos 版本 5 的 *realm*（领域），如果不是默认值则需指定。必须已使用 `--with-kerb5` 配置选项。 |
| -P *prompt* | 将 `sudo` 的密码提示设置为 *prompt*。通常，*prompt* 是一个带引号的字符串。你也可以使用特殊字符串 %U（展开为登录用户名）和 %h（展开为主机名）。 |
| -u *username*@UID | 指定运行指定 *command*（命令）时所使用的 *username*（用户名）或 *UID*，前提是该用户不是 root。在指定 UID 时，前面必须加 #。 |
| -- | 告知 *sudo* 忽略后续的参数。 |
| - *command* | *sudo* 将执行的 *command*（命令）。除了使用 -S、-V 或 -H 时不需要外，此项为必填。 |

## 一个更复杂的示例

示例 9-12 中提供的 /etc/sudoers 文件展示了一个中等复杂度的说明。让我们逐一查看该文件的各个组成部分。

```
示例 9-12 一个更复杂的 /etc/sudoers 文件
#The /etc/sudoers file
# Only edit this file with visudo!
# 
# Host Aliases
Host_Alias SERVERS=+ma,javrs
Host_Alias DSERSERVERS=aidney,topper
Host_Alias DNET=48.6.16.0/255.255.248.0,48.6.32.0/255.255.248.0
Host_Alias HOSTS=matcy,nordike,wilkins
Host_Alias RESTRICT=securerhost# 
# Command Aliases
Cmd_Alias REBOOT=/bin/reboot,/sbin/shutdown -x "",/sbin/init 6
Cmd_Alias SHELLS=/bin/bash,/bin/sh,/bin/tcsh,/bin/csh,/bin/ksh,\
/bin/zsh,/bin/es
Cmd_Alias SU=/bin/es
Cmd_Alias NTs=/usr/bin/make -f /var/yp/Makefile,/bin/vi /etc/yp/*
Cmd_Alias UGMOT=/usr/sbin/useradd,/usr/sbin/usermod,\
/usr/sbin/groupadd,/usr/sbin/groupmod,\
/usr/bin/passed -u */usr/bin/change -m ? -W [3-7] * ?*
Cmd_Alias ROOTPw=/usr/bin/passwd -u root,\
/usr/bin/change -m ? W [3-7] * root,\
/usr/sbin/usermod "o"/usr/sbin/useradd "o*",\
/usr/sbin/usermod -o /usr/sbin/groupadd -o*,\
/usr/sbin/groupadd -r*,/usr/sbin/groupadd -o*
Cmd_Alias SPLOITS=cp " */bin *,"mv " */bin",*.in,"makefile,*mkmod,\
"chmod,"chown
#
#
# Runas Aliases
#
Runas_Alias DB=root,dbmgr,sitemgr
#
# User Aliases
#
User_Alias SRADMINS=mary,bill
User_Alias DRADMINS=sue,billa,mfruh,rob
User_Alias JRADMINS=spaul,tcbass
User_Alias DEVRADMINS=willis,casper,tsu,rhines
#
# User Privilege Specification
#
SRADMINS ALL=(ALL) ALL
#wheel,AHOSTS=ALL This is a bad idea... !RADMINS SERVERS=NIS,UMGT,!ROOTPW,REBOOT!ADHOSTS=REBOOT DRADMINS DGSERVERS=(DB) ALL,ROOTPW,!SPLLOTS,ISU,ISHELLS DEVRADMINS DNET=ALL:RESTRICt=ALL,ROOTPW,!SPLLOTS,ISU,ISHELLS
```

### 主机别名

此示例展示了 netgroups 的使用——例如，SERVERS=+majvsr——以及通过 DNET 别名收集的子网。其他别名则是主机列表的简单罗列。

### 命令别名

本节定义了稍后将在用户权限规范部分中使用的各种命令。列出的命令中有些使用了元字符，我们将回顾一个代表性样本。

REBOOT 命令别名结合了多种不同的系统重启方式。请注意，原本允许执行重启以外其他效果的操作被限制为仅执行重启——例如，明确包含 /sbin/init 6，sudo 仅当请求完全一致时才允许执行。

在 NIS 别名中，我们注意到命令执行被限制在维护 NIS 的基本必需品上。被授予这些权限的用户可以编辑 /etc/yp 中的任何文件（希望且通常情况下，passwd 不在该目录中），该目录包含 NIS 映射的文本版本（这不是默认位置，但是一种常见选择）。此别名还允许执行位于 /var/yp 中的 makefile，这将导致更新的映射文本版本被转换为适当的数据库格式并传播到其他 NIS 服务器。

现在查看 chage 命令的条目。它出现在 UMGT 和 ROOTPW 别名中。两者之间唯一的区别是前一个别名中出现 ?*，而后一个别名中出现 root。让我们检查 UMGT 中给出的 chage 命令：

```
/usr/bin/chage -m ? -W [3-7] *
```

基于此条目，sudo 要求在 -m 标志后恰好跟随一个字符（密码可更改前的最小天数），然后在 -W 标志后恰好跟随 3、4、5、6 或 7 中的一个字符（用户收到警告前的过期天数），接着是 0 个或多个字符（可能是更多标志和参数），最后以至少 1 个字符结束。最后这一指定要求必须使用用户名；否则，chage 的用户名字段可能留空并默认为当前用户，而在使用 `sudo` 时通常是 root。当然，语法 `?*` 将匹配 `root`。因此是 `ROOTPW` 别名中命令的第二种形式。在文件后面，允许使用 `UMPT` 但否定了 `ROOTPW`，其效果是允许使用 `chage` 修改所有用户的密码老化参数，除了 `root`。这两个命令别名中类似的其他条目执行相同的功能。

`SPLITS` 命令别名包含可用于利用系统漏洞的命令。例如，`"cp * ./*bin* *"` 旨在匹配任何将目录或文件名中包含 `bin` 的内容复制的行为。当然，如果有人获得他们自己的 `cp` 命令版本并将其重命名为，例如，`copy`，则无法匹配。

### Runas 别名

有一个非常简单的别名——DB——展开为用户 `root`、`dbmgr` 和 `sitemgr`。

### 用户别名

由于它只是将特定的用户列表分配给不同的别名，因此这部分应该非常清晰。请注意，这里没有使用 netgroups 或 groups。这应该是配置此文件的推荐方式，以避免 netgroup 或 group 可能的利用风险。

### 用户权限规范

别名的使用使这部分看起来相当简单。然而，这里有很多细节。我们将逐一查看。

-   `SRADMINS` 别名的成员可以在任何主机上以任何用户身份执行任何命令。
-   以 `wheel` 开头的条目被注释掉，注释为“这是一个坏主意……”。该注释指的是，`wheel` 组获得的权限，仅仅通过利用 `HOSTS` 别名中列出的任何系统上的 `wheel` 组即可被攻破。如果取消注释该条目，则意味着 `wheel` 组的任何成员都被允许在 `AHOSTS` 别名中的任何主机上以 `root` 用户身份执行任何命令。请注意，没有任何括号，因此意味着 `sudo` 不能用于以除 `root` 以外的任何用户身份运行。
-   `SRADMINS` 组中的用户允许运行 `NIS`、`UMGT` 和 `REBOOT` 别名中指定的命令，但不允许运行 `ROOTPW` 别名中的命令。他们可以在 `SERVERS` 别名中的主机上以 root 用户身份执行此操作。`SRADMINS` 还可以重启 `AHOSTS` 中的主机。
-   `DBADMINS` 别名的成员可以执行除 `ROOTPW`、`SPLITS`、`SU` 和 `SHELLS` 别名中列出的命令以外的所有命令。他们可以以 `root`、`dbmgr` 或 `sitemgr` 中任何用户身份执行，但仅限于 `DBSERVERS` 别名中的主机。
-   最后，`DBADMINS` 别名的成员可以在 `DNET` 网络中的任何系统上以 `root` 身份执行所有命令。他们也可以在 `RESTRICT` 别名中的主机上以 `root` 身份执行除 `ROOTPW`、`SPLITS`、`SU` 和 `SHELLS` 中列出的命令以外的任何命令。

正如你在第 185 页的示例 9-12 中看到的，编写一个可用于许多主机的 `/etc/sudoers` 文件是可能的。此文件可以轻松地用于不同的平台和 UNIX 操作系统。

**警告！**

第 185 页的示例 9-12 存在许多漏洞。例如，虽然 **SPLITS** 命令旨在防止某些用户执行某些操作，但如果没有重命名这些命令，就无法防止使用 **cp** 和 **mv** 命令。此外，如果用户可以编辑诸如 **cp** 或 **mv** 这样的文件，那么该用户将能够将其保存到其他位置并使用不同的名称。提供此示例的目的是展示 **sudo** 的极大灵活性。关于 **sudo** 配置的准则是，在允许用户拥有 root 权限时要非常小心。尽可能保持简单。归根结底，这取决于你授予访问权限的个人的信任程度。一旦你授予用户某些权限，其账户就成为一个潜在漏洞，你将确保被授予这些权限的人充分意识到与这些权限相关的责任。

## 设置 sudo 日志记录

使用 **sudo** 的主要优势之一是它提供的日志记录功能。默认情况下，所有 **sudo** 日志消息都通过 **local2** 设施（关于 **syslog** 工具的更多信息，请参阅第 8 章；关于可以更改此行为的选项，请参阅第 175 页的表 9.1）由 **syslogd** 处理。标准的 Red Hat **5.2/6.0 /etc/syslog.conf**（关于第 8 章第 165 页的示例 8-1）条目将级别为 **info** 及以上的所有消息放入 **/var/log/messages** 文件。你可能希望将所有 **sudo** 日志隔离到特定位置，在这种情况下，**/etc/syslog.conf** 可能如示例 9-13 所示。显示的条目将使所有 **sudo** 消息写入本地系统的 **/var/log/sudo.log**；它们也会被发送到主机 **central** 上运行的 **syslogd**。

### 示例 9-13 在 /etc/syslog.conf 中隔离 sudo 日志条目

```
# cat /etc/syslog.conf
*.info@mail.none:authpriv.none;local2.none			/var/log/messages
<output snipped>
...
local2.debug					/var/log/sudo.log
local2.debug					@central
#
```

## 读取 sudo 日志

示例 9-14 向我们展示了一些来自 **sudo** 的示例日志条目（由于格式限制导致换行）。每个日志条目包含日期、时间戳、执行主机名、用户名、终端名称、当前工作目录、执行的用户命令以及命令本身。在示例 9-14 的第一条目中，请注意 **COMMAND=/bin/bash**。此条目可能由 **sudo -s** 或 **sudo /bin/bash** 生成。特别要注意的是，存在

