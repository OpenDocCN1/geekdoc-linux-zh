
## 配置 sendmail

如果你发现需要与系统管理员展开对话，只需提到“sendmail.cf 文件”、“地址重写规则”或“邮件循环发回自身”，你会立刻被理解，被视为同道中人，并成为大量同情的接受者。

sendmail.cf 文件（或 sendmail 配置文件）因其晦涩的语法、几乎难以解读的规则集以及让管理员抓狂的能力而闻名（且不祥）。实际上，这种名声有些是实至名归的，但随着 m4 预处理器宏的出现（在本节末尾讨论），配置 sendmail 在过去几年变得容易了许多。更好的是，sendmail RPM 中包含的默认 /etc/sendmail.cf 文件很可能无需修改即可工作，尽管仍应进行少量调整。

文件 /etc/sendmail.cf 包含用于指导 sendmail 守护进程行为的配置信息和可选值。整个文件长度超过 1,000 行，至少其中一半并未在此讨论（如果你发现需要操作这些行，那你将值得被同情）。一些潜在有用的行将在以下章节中呈现，并在相关选项块后插入注释。

sendmail.cf 文件的通用格式是单字符命令后跟一个参数（通常用单字符表示，但并非绝对）。例如，选项由大写字母 O（代表 option）引导。如果需要值，该值放在最后。命令必须从行的第一列开始，因为行首空白表示上一行的延续。此外，单行只能存在一个命令。有效命令在表 19-3 中描述。以 # 开头的行被视为注释，不进行处理。

**表 19-3：/etc/sendmail.cf 中可用的命令**

| 命令 | 描述 |
| :--- | :--- |
| C | 定义“类宏”，一个可以包含多个值的变量。 |
| D | 定义宏，只能包含一个值。 |
| E | 设置环境变量。 |
| F | 定义“文件类宏”，值从文件或管道获取。 |
| H | 选择头部行的格式。 |
| K | 声明键数据库文件。 |
| L | 允许基于系统负载平均值的处理限制。 |
| M | 定义 MDA 及其参数。 |
| O | 为选项分配值。 |
| P | 定义消息优先级级别。 |
| R | 组装重写规则。 |
| S | 开始一组重写规则。 |
| T | 将用户分类为“受信任的”。 |
| V | 定义配置文件的主要版本。 |

由于设置一个可用的 `sendmail.cf` 文件是让你的电子邮件服务正常运行的关键，以下章节致力于逐行解析此文件。如果你正在设置第一个电子邮件服务器，应彻底阅读这些章节，以便理解 `sendmail` 的工作原理以及你需要更改哪些内容以适合你的电子邮件配置。首先讨论选项行，接着讨论 `m4` 预处理器、forward 文件和别名文件。

> **注意：** `sendmail.cf` 文件中以井号 (#) 开头的任何行都是注释，不会被解释。通常，你可以取消这些行的注释并修改它们以激活特定功能，如以下章节所述。

### sendmail 组件文件

`sendmail.cf` 文件的第一部分包含用于创建 `sendmail.cf` 文件的组件文件列表。它还包含关于配置文件格式和版本的信息。以下是 `sendmail.cf` 文件开头的示例：

```text
#
# Copyright (c) 1998-2001 Sendmail, Inc. and its suppliers.
#           All rights reserved.
# Copyright (c) 1983, 1995 Eric P. Allman.  All rights reserved.
# Copyright (c) 1988, 1993
#  The Regents of the University of California.  All rights reserved.
#
# By using this file, you agree to the terms and conditions set
# forth in the LICENSE file which can be found at the top level of
# the sendmail distribution.
#
#
############################################################
#
#          SENDMAIL CONFIGURATION FILE
#
############################################################

#####  $Id: cfhead.m4,v 8.76.4.16 2001/03/06 22:56:36 ca Exp $  #####
#####  $Id: cf.m4,v 8.32 1999/02/07 07:26:14 gshapiro Exp $  #####
#####  linux setup for Red Hat Linux  #####
#####  $Id: linux.m4,v 8.11.16.2 2000/09/17 17:04:22 gshapiro Exp $
#####
#####  $Id: local_procmail.m4,v 8.21 1999/11/18 05:06:23 ca Exp $  #####
#####  $Id: no_default_msa.m4,v 8.1.10.1 2000/09/17 17:04:22 gs Exp $
#####
#####  $Id: smrsh.m4,v 8.14 1999/11/18 05:06:23 ca Exp $  #####
#####  $Id: mailertable.m4,v 8.18 1999/07/22 17:55:35 gshapiro Exp $
#####
#####  $Id: virtuuserstable.m4,v 8.16 1999/07/22 17:55:36 gshapiro Exp $
#####
#####  $Id: redirect.m4,v 8.15 1999/08/06 01:47:36 gshapiro Exp $  #####
#####  $Id: always_add_domain.m4,v8.9 1999/02/07 07:26:08 gshapiroExp $
#####
#####  $Id: use_cw_file.m4,v 8.9 1999/02/07 07:26:13 gshapiro Exp $
#####
#####  $Id: use_ct_file.m4,v 8.9 1999/02/07 07:26:13 gshapiro Exp $
#####
#####  $Id: local_procmail.m4,v 8.21 1999/11/18 05:06:23 ca Exp $  #####
#####  $Id: access_db.m4,v 8.15 1999/07/22 17:55:34 gshapiro Exp $
#####
#####  $Id: blacklist_recipients.m4,v 8.13 1999/04/02 02:25:13 gs Exp $
#####
#####  $Id: accept_unresolvable_domains.m4,v 8.10 1999/02/0707:26:07
#####              gshapiro Exp $
#####  $Id: proto.m4,v 8.446.2.5.2.41 2001/05/23 21:32:16 ca Exp $
#####
```

前面的注释块很有用，因为它指示了用于创建此 sendmail.cf 文件的组件 m4 宏文件（来自 /usr/lib/sendmail-cf 目录的子目录中）。/etc/sendmail.mc 文件是实际用于构建 sendmail.cf 的配置文件（使用命令 `m4 /etc/sendmail.mc > /etc/sendmail.cf`）。以下是来自 sendmail.cf 文件的代码，指示配置文件相关的版本和供应商。

```text
# level 9 config file format
V9/Berkeley
```

上面的行将此配置文件标识为对应 sendmail V9 的开源 Berkeley 发行版。接下来的行涉及某些安全功能：

```text
# override file safeties - setting this option compromises sys security
# addressing the actual file configuration problem is preferred
# need to set this before any file actions are encountered in cf file
#0 DontBlameSendmail=safe
```

根据前三个注释行判断，此版本的 sendmail 默认有些多疑。通过不设置 `DontBlameSendmail=safe`，sendmail 不会接受组写或世界写权限的 `.forward` 文件、包含文件、收件箱、配置文件、类文件或哈希映射文件，或者位于组写或世界写权限目录中的文件。如果需要覆盖这些默认设置，可以移除 `DontBlameSendmail` 行前的注释符号 (#)。接下来的行与 LDAP 映射有关。

```text
# default LDAP map specification
# need to set this now before any LDAP maps are defined
#0 LDAPDefaultSpec=-h localhost
```

使用 `LDAPDefaultSpec` 选项，你可以添加包含特定 LDAP 设置的默认 LDAP 映射。这些设置适用于所有 LDAP 映射，除非单个映射覆盖这些值。在定义任何 LDAP 映射之前设置此选项。

### sendmail 本地信息条目

*sendmail.cf* 文件中的下一个条目出现在本地信息标题下。它们使你能够输入特定于本地主机的配置信息。以下是该部分看到的行：

```text
##############
# local info  #
##############

Cwlocalhost
# file containing names of hosts for which we receive email
Fw/etc/mail/local-host-names
```

前面的行具有类似的功能。`Cwlocalhost` 行定义了类宏 `w`，其中包含分配给该机器所有可能主机名的列表。这包括任何 DNS 别名、`/etc/hosts` 中的所有引用，甚至可能还包括具有该机器账户的个人使用的错误名称（以避免那些邮件被退回）。由于在某些主机上这可能变得相当庞大，`Fw/etc/mail/local-host-names` 行定义了文件类宏 `w`，允许将这些主机名存储在单独的文件中，在此情况下为 `/etc/mail/local-host-names`。接下来的行用于设置你的 TCP/IP 域名：

```text
# my official domain name
# define only if sendmail cannot automatically determine your domain
```

