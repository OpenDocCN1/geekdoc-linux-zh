
这些宏定义了你要使用哪种类型的邮件移动实用工具和协议。`procmail` 设置允许 `sendmail` 将电子邮件传递给 `procmail` MTA。另一方面，`smtp` 设置告知 `sendmail` 假设它使用 SMTP 在邮件服务器之间传递邮件数据。有些人喜欢同时包含 `MAILER(local)`，但无论是否添加，此设置默认都会假定。添加它只是一种形式。有关可用的完整邮件发送器集，请参见 `www.sendmail.org/m4/mailers.html`。

以下是最后一组特征：

```
FEATURE('access_db')
FEATURE('blacklist_recipients')
dnl We strongly recommend to comment this one out if you want to protect
dnl yourself from spam. However, the laptop and users on computers that do
dnl not have 24x7 DNS do need this.
FEATURE('accept_unresolvable_domains')
dnl FEATURE('relay_based_on_MX')
```

## 12.6 附加功能与垃圾邮件警告

这些功能在表 12.6 中进行了说明，同时也包含了之前文件中已有的功能。请注意最后两项前面的警告。这两项功能都会让你面临垃圾邮件（spam）或大量机器生成邮件的问题。更糟糕的是，如果你允许 `relay_based_on_MX` 功能，某人可以通过将其 MX 记录指向你的邮件服务器，利用你的服务器将邮件反弹给其他用户来发送垃圾邮件。当人们认为你的站点上有人向他们发送垃圾邮件时，除了这种场景外，很少有事情会像你收到如此多的愤怒邮件那样糟糕。

有关如何防止这种情况发生的更多信息，请参阅“即时解决方案”章节中的“保护你自己免受垃圾邮件”。

## 12.7 引言：m4

在处理 `sendmail` + IDA 时，你会经常听到 `m4` 程序。该工具是一个宏预处理器，它将你在 MC 文件中看到的格式转换为你在 CF 文件中看到的格式（将在下一节中介绍）。`m4` 不仅用于 `sendmail`，它还是 `GNU Autoconf` 工具的核心，该工具用于创建如今许多源代码包提供的“configure”脚本。

你使用 `m4` 的格式如下：

```
m4 options macrofile > cffile
```

有关如何使用 `m4` 生成 `sendmail` 服务器配置文件的详细信息，请参阅“即时解决方案”章节中的“在命令行构建 `sendmail.cf`”。

## 12.8 CF 文件

如今，`m4` 工具通常用于避免直接编辑 `sendmail` 服务器配置文件 `sendmail.cf`。尽管如此，你仍然应该能够浏览 `sendmail.cf` 文件并进行较小的更改，这对于处理简单问题时避免折腾宏可以节省你一些时间。下面的讨论将带你了解默认 Red Hat `sendmail.cf` 文件的相关部分，并逐一解释每个部分。

文件以一大段版权信息和其他背景细节开头。所有这些行都以井号（#）开头，这意味着所有内容都被注释掉了。你最可能想要更改的部分如下所示：

```
###################
#  local info  #
###################
```

这是应用于邮件服务器本身及其宿主机的信息。注意这个第一项的格式：

```
Cwlocalhost
```

`sendmail.cf` 中的命令按单字母类别分组，通常后面还有一个单字母来指定你要执行的具体操作。在这种情况下，类别是 `C`，代表 class（类）。表 12.7 给出了 `sendmail.cf` 类别的完整列表。`w` 是具体的 `C` 类别命令，它指定你即将列出该主机已知的名称。在这种情况下，仅包含 "localhost"：

> **注意：** 既然你已经学会了如何读取宏文件，这些类别现在应该看起来很熟悉了。

接下来在 `sendmail.cf` 中是以下内容：

```
# file containing names of hosts for which we receive email Fw/etc/sendmail.cw
```

`F` 类别是一个信号，表示你想从文件中导入信息。与该类别一起使用的命令 `w` 基本上与 `C` 中的含义相同——你想导入此主机充当代理的机器名称。我使用“基本上”这个词是因为在配置 MX 记录中列出的邮件服务器时，文件 `/etc/sendmail.cw` 通常包含你网络上机器的列表。

**表 12.7** `/etc/sendmail.cf` 中的命令类别。

| 类别 | 用途 |
| :------- | :------ |
| `C` | 创建组 |
| `D` | 创建新宏 |
| `F` | 从文件或 FIFO 导入组的值 |
| `H` | 定义邮件头信息 |
| `K` | 创建键控数据库 |
| `M` | 定义邮件发送器或邮件发送器的接口 |
| `O` | 设置全局选项 |
| `P` | 创建消息优先级 |
| `R` | 在规则集中创建规则 |
| `S` | 开始构建规则集 |
| `V` | 在配置文件中设置版本信息供您自己参考 |

此外，请注意 `/etc/sendmail.cf` 文件有很好的注释。在用于从 `CW` 文件导入数据的代码之后，是以下内容：

```
# my official domain name
# ... define this only if sendmail cannot
# automatically determine your domain
#Dj$w.Foo.COM
CP.
```

这里需要解释两件事。第一是被注释掉的代码。多年前，你必须填写 `Dj` 项——`D` 代表定义宏，`j` 代表此邮件主机所在的官方域名。第二是另一个 `C` 类项。`P` 命令不是预定义的。通过它，该行创建一个名为 `P` 的新类，内容仅为一个单点。

> **提示：** 宏中的大写命令通常是用户定义的，而不是内部的。

在此之后，出现以下内容：

```
# "Smart" relay host (may be null)
DS
```

`D` 宏定义类别中的 `S` 命令不存在。同样，你正在这里创建一个新宏。`DS` 宏仅在你拥有不属于主网络且否则不知道如何向外部发送邮件的机器时使用。例如，这些机器可能位于防火墙后面。智能中继主机知道网络流量必须经过哪里才能到达外部世界。

接下来是一组三个类定义：

```
# operators that cannot be in local usernames (i.e., network indicators)
CO @ % !

# a class with just a dot (for identifying canonical names)
C.

# a class with just a left bracket (for identifying domain literals)
C[
```

这三个类——`CO`、`C.` 和 `C[`——之前都不存在，所以它们都是全新的宏。第一个定义了假设不是登录名一部分的字符。第二个项在内容上完全等同于类 `CP`，因为它只包含一个单点。（参见第 11 章关于 CNAME 条目的讨论以刷新你对规范名称的记忆。）最后一个类仅包含一个左括号。域字面量（domain literal）是邮件头的一部分，其中包含括号内的 IP 地址。该 IP 地址不是通过 DNS 查找的。相反，它应该被原样使用。

在此之后是一组文件定义。这些都是必须在 `sendmail` 设置过程中的某个时间点创建（或至少填写）的文件。前三个以 `K` 类别开头，因此是键控数据库：

```
# Mailer table (overriding domains)
Kmailertable hash -o /etc/mailertable
```

```
# Virtual user table (maps incoming users)
Kvirtuser hash -o /etc/mail/virtusertable
```

```
# Access list database (for spam stomping)
Kaccess hash -o /etc/mail/access
```

第四个条目如下所示，它是不同的。`F` 是一个类类别，从列出的文件中加载其内容。`R` 是一个用户定义的类。注意内容以 `-o` 开头。这是 `hash -o` 命令的一部分。

```
# Hosts that will permit relaying ($=R)
FR-o /etc/mail/relay-domains
```

接下来是你关于仅是用户名、没有 @domain.extension 附加的电子邮件地址的策略。`R` 宏被定义（`D`）以携带这种情况下的指令。留空假设所有仅以地址为本地域名内的用户名属于本地域名。这是一个合理的假设。

```
# who I send unqualified names to (null means deliver locally)
DR
```
