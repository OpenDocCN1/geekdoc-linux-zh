
```bash
nessus
```

出现 Nessus Setup 窗口。

- 8. 输入 `nessusd` 用户和密码，然后点击 Log In。Nessus 显示用于建立安全连接的证书并询问你是否接受。点击 Yes。客户端连接服务器后，Log in 按钮变为 Log out，左侧会出现 Connected（已连接）标签。

- 9. 点击 Target（目标）选择标签。输入 IP 地址范围以扫描网络中的所有主机。例如，扫描私有网络 192.168.0.0 中的第一个主机：

`192.168.0.0/24`

- 10. 点击 Start（开始）按钮。Nessus 开始扫描。扫描期间，Nessus 显示扫描进度的页面。扫描完成后，你可以进行数据分析并查看结果。

### SAINT

安全审计集成工具（SAINT）是一种扫描漏洞的工具。它基于常见漏洞披露（CVE）。

### 跟踪安全新闻与更新

为了跟上最新的安全警报，你可能需要每天访问以下一个或多个：

- CERT Coordination Center：http://www.cert.org

- Computer Incident Advisory Capability (CIAC)：http://www.ciac.org/

- National Infrastructure Protection Center：http://www.nipc.gov

如果你可以使用新闻，可以定期浏览：

- comp.security.announce

- comp.security.unix

如果你更喜欢通过电子邮件接收定期安全更新，还可以注册订阅邮件列表：

- redhat-watch-list：按照 www.redhat.com/mailing-lists/ 订阅此邮件列表。

- linux-security：按照 www.redhat.com/mailing-lists/ 订阅此邮件列表。

- FOCUS-LINUX：填写 http://online.securityfocus.com/cgi-bin/sfonline/subscribe.pl 订阅关注 Linux 安全问题的邮件列表。

- Cert Advisory 邮件列表：按照 http://www.cert.org/contact_cert/certmailist.html 订阅此邮件列表。

最后，你应该检查 Red Hat 网站 www.redhat.com/apps/support/errata/index.html，获取可能修复 Red Hat Linux 已知安全问题的更新。

## 总结

作为系统管理员，你的首要任务是 Red Hat Linux 系统和本地网络的安全。你可能还需要担心如何防止来自互联网的未经授权访问。本章介绍了系统和网络安全主题，并向展示了如何使用 Red Hat Linux 的某些安全功能。

## 第22 章：系统与网络安全 707

通过阅读本章，你将学习以下内容：

- 整个组织范围的安全框架是有帮助的。在这种框架中，你首先根据业务需求和风险分析建立安全策略。然后，你根据安全策略、业务需求和可用技术开发一套整体安全解决方案。最后，你实施管理实践以持续监控、检测并响应任何安全问题。

- 风险分析意味着识别威胁和漏洞。然后，你可以评估每个漏洞发生的概率和影响，并决定缓解那些最可能被利用的漏洞，以及哪些利用将造成最大的危害。

- 为了加固 Red Hat Linux 系统，你必须保护密码和网络服务（如 FTP、NFS 和 HTTP）。你可以使用 `chkconfig` 命令禁用不必要的服务。对于由 `xinetd` 启动的服务，你也可以编辑 `/etc/xinetd.d` 目录下的配置文件来关闭或服务。

- 使用安全外壳（SSH）进行安全的远程登录。本章将展示如何使用 SSH。

- 对于连接到互联网的系统（包括本地网络），你可以在内部网络和互联网之间建立防火墙来满足安全需求。任何公共访问的服务器（如 Web 和 FTP 服务器）都应该放置边界网络或非军事化区（DMZ）之外。

- 防火墙有很多种类——包过滤器、双宿主机和应用程序网关（代理服务器）。本章提供了防火墙概述，以及使用 Red Hat Linux 自带的 `iptables` 软件实现的包过滤防火墙。

- 你可以通过安装和设置配套光盘中的 Tripwire 软件来监控系统文件和目录的完整性。

- 你应该定期检查 Red Hat Linux 系统 `/var/log` 目录下的日志文件，寻找任何入侵威胁的迹象。

- 你还应该对系统和网络进行定期的安全审计。你可以使用 `nmap` 和 Nessus 等自动化工具测试你的网络安全。

- 本章提供了一些资源，你可以通过这些资源学习更多关于加固 Red Hat Linux 的知识。你可以利用这些在线资源跟进最新的安全新闻。

# 第五部分

# 编程 Red Hat Linux

第23 章：Linux 软件开发

第24 章：Shell 和 Perl 脚本编写

第25 章：Tcl/Tk 脚本编写

第26 章：Java 编程

# Linux 软件开发

![](img/b418dfc0d37b54b9876d5e801170c507_744_0.png)

### 本章要点

理解 makefile

编写示例 makefile

理解 GNU 通用公共许可证

理解 GNU 库通用公共许可证

理解可执行与链接格式 (ELF)

# 第五部分：编程 Red Hat Linux

许多 Linux 用户恰好是软件开发者。如果你想把开发软件作为爱好，或者想为 Linux 添加功能，你会发现 Linux 包含了创建 UNIX 和 X 应用程序所需的一切。你可以使用 GNU 和 C++ 编译器来编写常规程序（你将它们编译并链接成可执行文件）。

作为替代方案，你可以使用 Tcl/Tk 脚本语言来编写解释型图形应用程序。

本章讨论了在 Linux PC 上进行软件开发。重点不在于任何编程语言。相反，本章描述了如何使用各种软件开发工具，如编译器、性能分析器和版本控制系统。

本章还描述了自由软件基金会的 GNU 通用公共许可证对你可能需要开发的任何 Linux 软件项目的影响。你需要了解这一点，因为你在 Linux 中中使用 GNU 工具和 GNU 库来开发软件。

此外，我还讨论了动态链接和可执行与链接格式 (ELF)，它使得动态链接变得更容易。这些主题对 Linux 程序员来说，因为动态链接减少了可执行文件的大小，并可能允许程序员以二进制形式发布软件，即使他们使用了 GNU 库。

# Linux 中的软件开发工具

如所预期，作为 UNIX 的类品，Linux 包含了这些传统的软件开发工具：

- 文本编辑器，如 `vi` 或 `emacs`，用于编辑源代码（在第11章中描述）

- 用于编译和链接 C 语言编写的程序的编译器——C 是编写 UNIX 应用程序的首选语言（尽管现在许多程序员正在转向 C++）。Linux 包含了 GNU 和 C++ 编译器。最初，GNU C编译器被称为 `GCC`。`GCC` 的缩写代表 GNU Compiler Collection（GNU 集合，参见 http://gcc.gnu.org/ 中的描述）。

- 用于自动化软件构建过程的 GNU `make` 工具——将对象模块组合成可执行文件或库的过程。

- 用于调试程序的调试器。Linux 包含了 GNU 调试器 `gdb`。

- 版本控制系统，用于跟踪源文件的各种版本。Linux 带有 `RCS`（修订控制系统）和 `CVS`（并发版本系统）。现在，许多开源项目使用 `CVS` 作为版本控制系统。

如果你在从本书配套光盘安装 Red Hat Linux 时，按照第 2 章概述的步骤选择了“开发工具”软件包组，这些工具将自动安装。接下来的几节将简要描述如何使用这些工具编写应用程序。

# 使用 Info 获取帮助

你可能已经注意到大多数工具都来自自由软件基金会的 info。第23 章：Linux 软件开发 713

在 info 中，在线帮助文本以节点的形式组织；每个节点代表特定主题的信息。第一行显示该节点的页眉。

图 23-1：在 Shell 提示符下输入 `info` 后的终端窗口。

![](img/b418dfc0d37b54b9876d5e801170c507_746_0.png)

## 第五部分：红帽 Linux 编程

Texinfo 文档记录系统
