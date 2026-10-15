

如果你从零开始实现一个邮件系统，并且没有需要处理的站点政治或偏见，选择一个 MTA 可能会很困难。sendmail 和 Exim 无疑是最复杂、也是最可配置、最强大的选项。Postfix 更简单、更快，并且在设计时将安全性作为首要目标。如果你所在的站点或系统管理员对某个特定的 MTA 有使用历史，除非你需要旧 MTA 中不可用的功能，否则不值得更换。

sendmail 的配置在下一节中介绍。Exim 的配置从第 807 页开始，Postfix 的配置从第 828 页开始。

## 20.8 SENDMAIL

sendmail 的源代码发行版可从 sendmail.org 获取，但如今很少需要从头构建它。如果你必须这样做，请参考顶层的 INSTALL 文件。如果你需要调整一些构建默认值，可以在 devtools/OS/your-OS-name 中找到 sendmail 的假设，并且可以通过编辑 devtools/Site/site.config.m4 来添加功能。sendmail 在编译期间不仅使用 m4 宏预处理器，也用于配置。一个 m4 配置文件通常命名为 hostname.mc，然后从一种略微用户友好的语法翻译成文件 hostname.cf 中的完全难以理解的低级语言，该文件随后被安装为 /etc/mail/sendmail.cf。

要查看系统上安装的 sendmail 版本以及它的编译方式，请尝试以下命令：

```
linux$ /usr/sbin/sendmail -d0.1 -bt < /dev/null
Version 8.13.8
Compiled with: DNSMAP HESIOD HES_GETMAILHOST LDAPMAP LOG MAP_REGEX MATCHGECOS MILTER MIME7TO8 MIME8TO7 NAMED_BIND NETINET NETINET6 NETUNIX NEWDB NIS PIPELINING SASL2V2 SCANF SOCKETMAP STARTTLS TCPWRAPPERS USERDB USE_LDAP_INIT
================ SYSTEM IDENTITY (after readcf) ================
(short domain name) $w = ross
(canonical domain name) $j = ross.atrust.com
(subdomain name) $m = atrust.com
(node name) $k = ross.atrust.com
==============================================================
```

该命令将 sendmail 置于地址测试模式（-bt）并进入调试模式（-d0.1），但不提供任何要测试的地址 < /dev/null。其副作用是 sendmail 会告诉我们它的版本以及编译时使用的编译器标志。一旦你知道版本号，你就可以查看 sendmail.org 网站，看看该版本是否与任何已知的<|message|>安全漏洞相关。

要找到系统上的 sendmail 文件，请查看已安装的 /etc/mail/sendmail.cf 文件的开头。那里的注释会提到配置构建所在的目录。该目录反过来应该能引导你找到 .mc 文件，即配置的原始来源。

大多数分发 **sendmail** 的厂商不仅提供二进制文件，还提供来自发行版树的 cf 目录，它们通常隐藏在操作系统文件中的某个位置。表 20.5 将帮助你找到它。

**表 20.5 — sendmail 配置目录位置**

| 系统 | 目录 |
|---|---|
| Ubuntu | `/usr/share/sendmail` |
| SUSE | `/usr/share/sendmail` |
| Red Hat | `/usr/share/sendmail-cf` |
| Solaris | `/etc/mail/cf` |
| HP-UX | `/usr/newconfig/etc/mail/cf` |
| AIX | `/usr/samples/tcpip/sendmail/cf` |

### The switch file

大多数系统都有一个“服务切换”配置文件 **/etc/nsswitch.conf**，它列举了可以满足各种标准查询（例如用户和主机查找）的方法。如果为某种查询列出了多个解析方法，服务切换文件还会确定咨询这些方法的顺序。

服务切换的存在通常对软件是透明的。然而，**sendmail** 喜欢对自己的查找进行精细控制，因此它目前忽略系统切换文件，而是使用自己的内部服务配置文件（`/etc/mail/service.switch`）。

切换文件中的两个字段会影响邮件系统：aliases 和 hosts。hosts 服务的可能取值为 dns、nis、nisplus 和 files。对于 aliases，可能的取值为 files、nis、nisplus 和 ldap。除 files 外，你使用的机制必须在编译 **sendmail** 时编译进去，服务才能使用。

### Starting sendmail

**sendmail** 不应由 **inetd** 或 **xinetd** 控制，因此必须在启动时显式启动。有关启动细节，请参阅第 3 章 *Booting and Shutting Down*。启动 **sendmail** 时使用的标志决定了其行为。你可以使用 `-b` 标志以多种模式运行 **sendmail**。`-bs` 代表“be”或“become”，并且始终与另一个决定 **sendmail** 将扮演角色的标志一起使用。表 20.6 列出了合法的值，并还包括 -A 标志，该标志在 MTA 和 MSA 行为之间进行选择。

如果你正在配置一台将从互联网接收传入邮件的服务器，请以守护进程模式（`-bd`）运行 **sendmail**。在此模式下，**sendmail** 监听网络端口 25 并等待工作。你通常还会指定 `-q` 标志——它设置了[^8]

[^8]: **sendmail** 监听的端口由 `DAEMON_OPTIONS` 决定；端口 25 是默认值。

