
```perl
if ($Config('missing_fields_redirect')) {

    print "Location: \$missing_fields_redirect\n\n";

}

} else {

    foreach $missing_field (@error_fields) {

        $missing_field_list .= '<li>$missing_field\n';

    }

}
```
`print <<"(END ERROR HTML)"`;

```
```

Content-type: text/html

<html>

<head>

<title>错误：空字段</title>

</head>

<center>

<table border=0 width=600 bgcolor=#9C9C9C>

<tr><th><font size+=2>错误：空字段</font></th></tr>

</table>

<table border=0 width=600 bgcolor=#CFCFCF>

<tr><<td>在您提交的表单中，以下字段为空：<p>

<ul>

$missing_field_list

</ul><br>

</</td>

```
在成功提交表单之前，必须填写这些字段。<p>

# 628 页 第 27 章 • 构建你自己的 Web 服务器

请使用浏览器的后退按钮返回表单
<hr size=1>
<center><font size=-1>
<a href="http://www.widewidmart.com/scripts/formmail.shtml">FormMail</a></a>/V1.6 &amp; 1995 - 1997 Matt Wright<br>
<a href="http://www.widewidmart.com/scripts/">Matt's Script Archive, Inc.</a> 的免费产品
</font></center>
<td></td></tr>
</table>
</center>
<body>
</html>

(END ERROR HTML)
}
exit;
```

需要注意的是，该程序设计用于向用户返回一个 HTML 页面，指示表单中的联系信息已处理，或者在发生错误时指示错误。这是所有 CGI 程序的重要组件：它们要么向浏览器返回有效数据（如 HTML 或图像文件的内容），要么将浏览器重定向到一个有效的 URL。

`formmail` 程序提供了许多其他功能，例如选择邮件主题的能力，并确保脚本不会被其他网站的用户滥用。详细信息请访问该程序的网站。

我们基础网站的最后重要部分是为 `/home/httpd/html/authors/` 目录创建访问限制，以便只有授权的用户才能访问该目录下的文件。这是一个两步过程。首先，我们需要创建一个包含必要用户的用户文件，就像我们在讨论保护目录的上一节中所做的那样。

我们为所有希望访问该目录的用户执行此操作。接下来，我们想要创建一个组（称之为 `authors`），以便管理目录访问的工作。我们通过在我们的 Web 服务器组文件中添加该组的条目来创建此组：

```
authors: <author1><author2><author3>
```

在此条目中，假设有三个用户获得了该目录的权限。

# 第二九章

# Linux 与 DOS/Windows

- 在 Linux 中运行 DOS 应用程序
- 使用 Wabi 运行 Windows
- 为什么不用 Wine？

反对将 Linux 作为文字处理等生产力任务日常操作系统的最大理由之一，是 Linux 缺乏应用程序。再加上无法运行 Windows 应用程序（至少 OS/2 可以做到，对吧？），Linux 就像一个异类，一个拥有伟大技术但营销极其糟糕的奇特案例。

关于这整个论点的问题点在于，Linux 实际上可以运行大多数 DOS 应用程序和许多 Windows 应用程序，而且具有更广泛的 Windows 兼容性前景。

Linux 对 DOS 的支持已经可用一段时间了，许多流行的 DOS 应用程序可以在 Linux 下几乎不费力地运行。

此外，目前正有若干努力致力于在 Linux 环境中提供完整的 Windows 兼容性。在商业上，Sun Microsystems 的 Wabi 环境已移植到 Linux 并以非常合理的价格提供。但本着 Linux 精神，一个 Linux 开发者团队承担了提供一种免费的、优于商业 Windows 兼容性的任务，这就是 Wine。

在本章中，我们将查看这三项尝试：DOS 仿真、Wabi 和 Wine。

## 在 Linux 中运行 DOS 应用程序

对 DOS 应用程序的支持是 Linux 中最强大的兼容性方案，并包含在大多数 Linux 发行版中。

大多数 Linux 发行版（包括 Red Hat 5.1）都带有一个 DOS 仿真应用程序 `DOSEmu`。在这种环境下，可以安装并运行 DOS（包括如 DOS 6.2 等较新版本），然后运行大多数 DOS 应用程序。当然，这也有局限性，包括影响某些图形和字体操作的限制，但整体运行良好。

此外，DOS 环境可以在 X Windows 的一个独立窗口中运行，从而便于在 Linux 程序旁边运行 DOS 应用程序。

`DOSEmu` 提供的功能包括：

- 多用户同时运行 DOS 的
- 将 Unix 目录挂载到特定驱动器的能力
- 从介质启动

为了简单起见，为了初步了解该软件的工作原理，我们将查看包含以下配置：

- 从软盘启动
- 从磁盘镜像启动

为了让 DOS 运行，必须有一个名为 `/etc/dosemu.conf` 的配置文件。这是一个非常复杂的文件，包含了：

- 从软盘启动
- 从磁盘镜像启动
- 从其他分区启动

为了了解配置典型 Dose 环境涉及的内容，以下是默认 `dosemu.conf` 文件的内容（为了简洁已删除了所有注释行）：

```bash
debug { off }

dosbanner on

timing on

terminal { charset latin on }

X { updatefreq 8 title 'DOS in a BOX' icon_name "xdos" }

mathco on

cpu 80386

xms 1024

ems 1024

host.com
```

## 邮件传输代理的概念

通常，当用户想到电子邮件系统时，他们想的是他们用于读取、撰写和发送消息的软件。这可能是 Netscape Communicator 的邮件模块、Eudora、Pegasus Mail 或 pine，但在所有情况下，这些程序仅仅是后端系统的接口，由后端系统真正执行路由和投递邮件的工作。

在这些情况下，用户的软件并没有实际处理发出的邮件的投递或收到的邮件的接收。这些程序被称为邮件用户代理（MUA）。有许多 MUA，它们的工作是为电子邮件世界提供用户界面。

这些 MUA 之后是邮件传输代理。MTA 负责投递、接收和路由邮件消息的工作。通常，它们都遵循某些标准协议（如简单邮件传输协议，或 SMTP），这些协议构成了互联网的电子邮件系统（以及几乎所有基于 Unix 的网络的电子邮件系统）。

MUA 和 MTA 之间的这种区别是非常重要的。为了给组织或任何其他计算机网络设置邮件服务器，必须与邮件传输代理一起工作。

## 作为顶级 MTA 的 Sendmail

毫无疑问，在 Unix 世界中，最顶级 MTA 是 Sendmail 程序。该程序定义了我们在互联网上熟悉的邮件系统，提供了我们都所周知的地址结构（username@some.domain）以及我们所预期的功能（如自动邮件转发）。

凭借其主导地位，Sendmail 已经成为可用最强大、最复杂的 Unix MTA。事实上，在大型组织中，Sendmail 系统的配置和管理可能非常复杂，以至于有一整本书都专门介绍设计 Sendmail 系统、配置它以及保持其运行的内容。

在本章中，我们将注意力集中在 Sendmail 的配置和使用上，因为它是 Red Hat Linux 自带的默认 MTA，而且在 Unix 网络中非常常见。

本章仅对 Sendmail 和如何配置它进行简要介绍。要更深入了解该主题，请访问网站 www.sendmail.org。

不过，首先，我们将对 Linux 可用的一些替代 MTA 进行简要调查。

## Smail

Sendmail 可能是主导性的 Unix 邮件传输代理，但在 Unix 世界中，smail 被广泛用 MTA。它的配置可能更简单（尽管并不总是如此），并且提供了类似的功能，包括对 SMTP 和 UUCP 的支持，使其非常适合在线邮件服务器配置。

Red Hat Linux 5 使用 Sendmail 作为其默认 MTA，并且不包含 smail 软件包。你可以从 ftp://ftp.uu.net/networking/mail/smail/ 下载最新版本的 smail。

## Qmail

Qmail 是 Sendmail 的替代方案，它没有获得像邮件那样的名气，但具有几个功能使其成为 MTA 领域的一个强有力的竞争者。

qmail 的作者将安全视为该软件包的明确首要任务。多年来，Sendmail 暴露了许多安全漏洞，这些漏洞随后都被修复了。qmail 的哲学是尽一切避免隐藏的漏洞，因为邮件是一项持续运行的服务，因此不断面临黑客攻击。

Qmail 还尝试让投递过程尽可能可靠，采用了一种收箱格式，如果系统在向收箱投递消息时发生崩溃，那么该格式将比损坏更安全。

更重要的是，qmail 整合了传统 MTA 中保留在单独应用程序中的功能：转发、别名、负载管理等。

qmail 的主页位于 http://www.qmail.org/top.html。

## 使用 M4 配置 Sendmail

正如前面提到的，对于经验丰富的 Unix 系统管理员来说，配置 Sendmail 可能是是一项艰巨的任务。要掌握该系统的复杂性可能需要多年时间。

Sendmail 的配置存储在 `/etc/sendmail.cf` 中，只需看随 Red Hat Linux 5 带的默认配置文件就能看出配置的复杂性。该文件非常长，因此在这里包含在单独的附录（附录 D）中。

如果你浏览这个文件，你会发现它由大量极其晦涩的规则组成，这些规则定义了 Sendmail 的行为。如果需要手动创建和编辑这种类型的配置文件，那么期望 Sendmail 专家之外的任何人来配置基础系统是不现实的。

幸运的是，Sendmail 提供了一个创建配置文件的设施：一个名为 `m4` 的程序。M4 允许你产生更简单的配置文件。M4 然后处理这些文件并将其转换为完整的 Sendmail 配置文件。所有最有知识的用户都应该以这种方式创建他们的 Sendmail 配置。

> 注意
> 你可以在位于 `/usr/lib/sendmail-cf/` 的配置文件随附的 README 文件中找到关于 m4 Sendmail 配置的讨论。有关使用 m4 配置 Sendmail 的示例，请参见 `/usr/lib/sendmail-cf/cf`。

在本节中，我们将首先安装使 m4 工作所需的必要配置，然后查看在线服务器的配置。

### 安装 Sendmail 配置

取决于你的发行版，Sendmail 配置文件可能在安装 Linux 时并未默认安装。在 Red Hat 5 的情况下，它们没有。要检查 `/usr/lib/sendmail-cf` 是否。

在 Red Hat 5 的情况下，安装文件很容易。将随书附带的光盘挂载到方便的位置（例如 `/mnt/cdrom`），然后使用 `rpm` 安装 `sendmail-cf`：

```
$ rpm -i /mnt/cdrom/RedHat/RPMS/sendmail-cf-8.8.7-12.i386.rpm
```

对于其他发行版，请查看你的文档了解如何安装文件。

### 创建在线邮件服务器

这样做是因为在线服务器更容易配置和理解。

> 注意
> 尽管 m4 系统简化了 Sendmail 配置，选项数量仍然是巨大的。我们只讨论本章出现的选项。

在线邮件服务器是全连接互联网的邮件服务器。当网络外部的人将邮件指向本地网络上的用户时，它可以直接投递；当网络上的用户发送消息时，它将立即发送。

在我们情况下，我们需要为用户的收箱配置 Sendmail，并立即尝试投递消息。如果互联网连接出现问题，消息将排队稍后投递。

我们的 m4 配置文件看起来像这样：

```
include(cf.m4)

OSTYPE(linux)

undefined(UUCP_RELAY)

undefined(BITNET_RELAY)

FEATURE(redirect)

FEATURE(always_add_domain)

MAILER(local)

MAILER(smtp)
```

让我们逐行分析：

- 第一行：`include.m4`。这些是构建 Sendmail 配置文件所需的通用配置文件。
- 第二行：`OSTYPE(linux)`。你的操作系统类型定义为 Linux，以便设置相应的默认值。
- 第三行：`undefined(UUCP_RELAY)`。通过不定义 UUCP 继器，我们表示没有主机接收 UUCP 定向邮件，且 UUCP 接收者必须直接连接。考虑到 UUCP 是在大多数网络尚未直接连接的时代设计的，大多数站点都会留空 `UUCP_RELAY`。
- 第四行：`undefined(BITNET_RELAY)`。由于我们没有连接到 Bitnet 网络，我们将其留空；使用 Bitnet 格式的地址将无法工作。
- 第五行：`FEATURE(redirect)`。如果设置，任何指向 `.REDIRECT` 的邮件将被拒绝，并带有用户新地址的消息。
- 第六行：`FEATURE(always_add_domain)`。此功能确保将域名添加到本地邮件地址。
- 第七行：`MAILER(local)`。启用本地邮件投递代理。
- 第八行：`MAILER(smtp)`。启用 SMTP 邮件传输代理用于发送邮件。

方式，当用户离开时，他们的新地址可以通过添加 `.REDIRECT` 来别命名为旧地址。

- 第 6 行：`FEATURE(always_add_domain)`。此功能确保 From 行始终包含本地域名，以便收件人可以回复回邮件。
- 第 7 行：`MAILER(local)`。本地邮件投送器支持允许 Sendmail 将邮件投递到 Unix 邮箱中。
- 第 8 行：`MAILER(smtp)`。SMTP 投送器支持允许 Sendmail 将消息发送到接收者的邮件服务器。这在服务器连接到互联网且可用 DNS 服务器的系统中有效。

为了从 m4 配置文件创建 Sendmail 配置文件，我们需要在 `/usr/lib/sendmail-cf/cf` 目录下创建 m4 文件。在这种情况下，让我们创建一个名为 `online.mc` 的文件。`.mc` 扩展名通常被用于 m4 配置文件。

接下来，切换目录到 `/usr/lib/sendmail-cf/cf` 并执行此命令：

```bash
$ m4 online.mc > online.cf
```

这将使用 m4 处理该文件并生成一个名为 `online.cf` 的 Sendmail 配置文件。

下一步是对现有的 `sendmail.cf` 文件进行备份，然后用我们刚刚创建的文件替换它。这需要 root 用户完成：

```bash
# cp /etc/sendmail.cf /etc/sendmail.cf
# cp online.cf /etc/sendmail.cf
```

最后也是一步是重启 Sendmail 守护进程：

```bash
# killall -HUP sendmail
```

`killall` 命令向所有运行命名程序的进程（在本例中 Sendmail）发送指定的信号。

当 Sendmail 守护进程在启动时运行时，它现在将加载你的新配置文件。如果你想手动加载 Sendmail，请使用命令：

```bash
# sendmail -bd
```

默认情况下，Sendmail 守护进程在大多数 Linux 发行版启动时加载，除非选择禁用它。如果你需要将 Sendmail 添加到启动循环，可以在 `rc.local` 文件中使用 `sendmail -bd` 命令。

> 提示：如果你计划运行大型 Sendmail 站点，O'Reilly & Associates 出版的《Sendmail》（第 2 版，1997年）是权威参考。该书由 Bryan Costales 和 Eric Allman 编写。不过，请做好长久阅读的准备。

## 我们接下来将去哪里？

通过本章，我们已经涵盖了与将 Linux 设置为内网服务器相关的所有主要主题。

在下一章中，我们将关注当今企业世界的一个重要课题：在 Linux 中运行 DOS 和 Windows 软件的能力。

令人惊讶的是，Linux 能够通过其 `dosemu` 软件支持 DOS 应用程序。此外，尽管仍处于早期阶段，但人们正在努力编写名为 Wine 的 Windows 仿真器，能够运行 16 位和 32 位 Windows 应用程序。虽然 Wine 尚未准备好作为企业环境中日常工作的工具，但它目前能够运行 Microsoft Word 和其他流行的 Windows 应用程序。我们将讨论这两个兼容包的功能和用途。

最后，我们将查看 Wabi，这是一个由 Sun Microsystems 为 Solaris 操作系统创建并由 Caldera 移植到 Linux 的 Windows 仿真环境。Wabi 提供了稳定、可靠的 Windows 3.1 仿真，并具有运行数十种流行的 Windows 3.1 应用程序。
