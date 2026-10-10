

例如 `newsyslog` 或 `logrotate`。这些工具应通过 `cron` 守护进程频繁调用。有关更多详细信息，请查看 `newsyslog` 或 `logrotate` 的手册页（man pages）。

## /var 目录的剩余空间

根据环境不同，存储在 `/var` 目录中的日志和 spool 文件可能会变得非常大。使用 `df` 命令定期检查 `/var` 中的剩余空间是一个好习惯。

`/var` 目录必须作为独立的分区挂载。请参见第 8 章中的“磁盘分区”部分以获取更多信息。

## 补丁管理

保持软件补丁和更新处于最新状态至关重要。诸如 Bugtraq 之类的邮件列表经常会列出软件漏洞，软件供应商通常会迅速修复这些问题。根据你所使用的发行版和包管理工具，这些补丁可能位于不同的位置。下表列出了最流行的 Unix 和 Linux 发行版，以及获取软件补丁的资源：

| 发行版 | 补丁 |
| :--- | :--- |
| AIX | <http://techsupport.services.ibm.com/rs6000/fixes> |
| BSDI | <http://www.bsdI.com/services/support/patches/> |
| Caldera OpenLinux | <ftp://ftp.calderasystems.com/pub/updates/OpenLinux/> |
| Debian Linux | <http://www.debian.org/security/> |
| FreeBSD | <ftp://ftp.freebsd.org/pub/FreeBSD/releases/> |
| IRIX | <http://www.sgi.com/support/security/> |
| HP Unix | <http://us-support.external.hp.com/> |
| Mandrake Linux | <http://www.linux-mandrake.com/en/security/> |
| NetBSD | <http://www.netbsd.org/Security/> |
| OpenBSD | <ftp://ftp.openbsd.org/pub/OpenBSD/patches/> |
| Red Hat Linux | <http://www.redhat.com/support/errata/> |
| Slackware Linux | <ftp://ftp.slackware.com/pub/slackware/> |
| Solaris | <ftp://sunsolve1.sun.com/pub/patches/> |
| SuSE Linux | <http://www.suse.com/us/support/security/index.html> |

通常，发行版供应商花费更多时间将其资源更新为包含安全补丁的状态。如果你的 Unix 或 Linux 发行版供应商没有列出针对已公布漏洞的补丁，请尝试前往软件供应商的网站查找补丁。如果你必须等待你的发行版供应商提供更新，请考虑暂时禁用或卸载易受攻击的软件。

此外，请查看本书参考文献中心的“在线资源”部分，了解可以订阅的邮件列表，以便及时接收最新软件漏洞公告的更新。

## 本章小结

必须启用并强制执行日志记录，以捕获系统活动的详细信息。此外，必须正确设置日志文件的文件权限，以防止恶意用户对其进行篡改。保持软件更新和补丁最新也非常重要，以保护系统免受本地和远程用户利用软件漏洞的影响。因此，每个系统管理员都应尝试实施本章中提出的建议，以确保防范各种类型的恶意活动和入侵尝试。

# 第三部分

# 专题

- **第 10 章** Nessus 攻击脚本语言 (NASL)
- **第 11 章** 无线黑客技术
- **第 12 章** 使用 Sharp Zaurus PDA 进行黑客攻击

# 第 10 章

# Nessus 攻击脚本语言 (NASL)

本章内容：

- 从命令行运行 NASL 脚本
- 使用 NASL 编写 Nessus 插件
- 小结

Nessus 是一款免费且开源的安全扫描器，可从 http://www.nessus.org/ 获取。本章提供了一个分步示例，演示如何使用 NASL（Nessus 攻击脚本语言）为 Nessus 编写漏洞检查插件。由于 NASL 专门用于编写 Nessus 插件，它使得这些插件的开发变得简单明了。Nessus 公开可用的插件列表可在 http://cgi.nessus.org/plugins/ 找到。

> 使用 NASL 编写的插件文件名以扩展名 ".nasl" 结尾。由于 NASL 是一种解释型语言，这些文件也被称为 NASL “脚本”。

## 从命令行运行 NASL 脚本

请查看你的 Nessus 安装目录中的 plugins 目录，以找到随每个 Nessus 发行版捆绑的所有 NASL 脚本。可以使用 nasl 解释器从命令行运行 NASL 脚本：

```
nasl -t target_ipaddress script.nasl
```

## 使用 NASL 编写 Nessus 插件

在本节中，我们将查看一个示例，介绍如何使用 NASL 编写漏洞检查插件。但首先，我们必须找出一个要检查的漏洞示例。一旦识别出漏洞，我们就可以通过编写合适的插件来使用 Nessus 检测它，如下几段所述。

### 漏洞示例

Web 应用程序经常使用文本文件来存储应用程序设置信息。为了说明我们的示例，假设一个 Web 应用程序将用户名和密码信息存储在 Web 服务器 Web 根目录中的文件（如 /src/passwd.inc）中。如果运行该应用程序的 Web 服务器被配置为提供 .inc 文件，这种情况将被视为一个漏洞。外部用户可以通过向 Web 服务器请求 /src/passwd.inc 来利用此类漏洞，从而获取用户密码。

### 插件

本节描述如何使用 Nessus 检测 Web 服务器上是否存在文件 /src/passwd.inc。首先，我们必须编写一个 NASL 脚本来执行此操作。该脚本将作为一个 Nessus “插件”。这样一个脚本看起来如下所示：

```
if(description)
{
        script_id(99999);

        script_version("$Revision: 1.0 $");

        script_name(english: "Checks for /src/passwd.inc");

        desc["english"] = "/src/passwd.inc is usually installed
by XYZ application and contains user password information
in clear text.

Solution: Configure your web-browser to not serve .inc
files.

Risk factor : High";

        script_description(english:desc["english"]);

        script_summary(english:"Checks for the existence of
/src/passwd.inc");

        script_category(ACT_GATHER_INFO);

        script_copyright(english:"This script is Copyright
(C)2003 Nitesh Dhanjani");

        script_family(english:"CGI abuses");

        script_require_ports("Services/www", 80);

        exit(0);
}

include("http_func.inc");

port = 80;

if(get_port_state(port))
{
    hget = http_get(item:"src/passwd.inc", port:port);
    mysoc = http_open_socket(port);
    if(!mysoc)exit(0);
    send(socket:mysoc, data:hget);
    myrec = http_recv(socket:mysoc);
    http_close_socket(mysoc);
    if (!("404" >< myrec))
    {
        security_hole(port);
    }
}
```

当 Nessus 运行脚本以提取插件的摘要信息时，`description` 变量的值被设置为 1。因此，当 `description` 的值为真（即非零）时，我们定义各种插件描述变量的值。

`script_id` 函数为插件设置唯一的 ID。每个插件的值必须是唯一的。在这种情况下，我们可以将其设置为 9999 这样的大数，以确保值 distinct（不同/独特）。`script_version` 函数显示有关插件的版本信息。更新此数字以反映插件的最新版本是个好主意。`script_description` 函数设置插件的描述，当用户查询插件时，该描述由 Nessus 客户端显示。同样，`script_summary` 函数用于设置插件的摘要描述。

`script_category` 函数设置 Nessus 所需的插件类别。在我们的情况下，我们将其设置为 `ACT_GATHER_INFO`，因为该插件收集远程服务的信息；也就是说，它检查 Web 服务器上是否存在文件 `/src/passwd.inc`。`script_copyright` 函数用于设置作者版权信息。

Nessus 将插件分为不同的“家族”，以帮助对执行的漏洞检查进行排序。我们将其设置为“CGI abuses”以指示基于 CGI 的 Web 应用的滥用。访问 [http://cgi.nessus.org/plugins/dump.php3?view=web&family](http://cgi.nessus.org/plugins/dump.php3?view=web&family) 查看按家族分类的公开可用插件列表。

可以通过在 GUI 客户端的扫描选项选项卡中选择适当的复选框来配置 Nessus，以优化测试。当

