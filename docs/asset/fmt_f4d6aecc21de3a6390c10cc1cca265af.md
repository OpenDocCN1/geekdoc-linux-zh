
**TABLE 1-7 Linux Information and News Sites**

## Documentation

sites. You can find other sites through resource pages that hold links to other Web sites—for example, the Linux Web site on the World Wide Web at `www.tldp.org/links.html`.

Linux documentation has also been developed over the Internet. Much of the documentation currently available for Linux can be downloaded from Internet FTP sites. A special Linux project called the Linux Documentation Project (LDP), headed by Matt Welsh, has developed a complete set of Linux manuals. The documentation is available at the LDP home site at `www.tldp.org`. Linux documents provided by the LDP are listed in Table 1-8, along with their Internet sites.

Most of the standard Linux software and documentation currently available is already included on your Red Hat DVD-ROM. HOW-TO documents are all accessible in HTML format, so you can view them easily with your Web browser. In the future, though, you may need to access Linux Internet sites directly for current information and software.

An extensive number of mirrors are maintained for the Linux Documentation Project. You can link to any of them through a variety of sources, such as the LDP home site, `www.tldp.org`, and `www.linuxjournal.org`. The documentation includes a user's guide, an introduction, and administration guides. These are available in text, PostScript, or Web page format. Table 1-8 lists these guides. You can also find briefer explanations, in what are referred to as HOW-TO documents.

| Sites | Web Sites |
|---|---|
| `www.tldp.org` | LDP 网站 |

| Guides | Document Format |
|---|---|
| Linux Installation and Getting Started Guide | DVI、PostScript、LaTeX、PDF 和 HTML |
| Linux User's Guide | DVI、PostScript、HTML、LaTeX 和 PDF |
| Linux System Administrator's Guide | PostScript、PDF、LaTeX 和 HTML |
| Linux Network Administrator's Guide | DVI、PostScript、PDF 和 HTML |
| Linux Programmer's Guide | DVI、PostScript、PDF、LaTeX 和 HTML |
| The Linux Kernel | HTML、LaTeX、DVI 和 PostScript |
| Linux Kernel Hacker's Guide | DVI、PostScript 和 HTML |
| Linux HOWTOs | HTML、PostScript、SGML 和 DVI |
| Linux FAQs | HTML、PostScript 和 DVI |
| Linux Man Pages | 手册页格式 |

**TABLE 1-8 Linux Documentation Project**

除了网站之外，还可以使用 Linux Usenet 新闻组。通过您的 Internet 连接，您可以访问 Linux 新闻组，阅读其他 Linux 用户的评论并发布自己的消息。存在多个 Linux 新闻组，每个都以 comp.os.linux 开头。对初学者特别有吸引力的是 comp.os.linux.help，您可以在这里发布问题。表 1-9 列出了一些您可以查看的 Usenet Linux 新闻组，尤其是用于发布问题的新闻组。

| 新闻组 | 标题 |
|---|---|
| comp.os.linux.announce | Linux 开发公告 |
| comp.os.linux.development.apps | 面向开发 Linux 应用程序的程序员 |
| comp.os.linux.development.system | 面向从事 Linux 操作系统开发的程序员 |
| comp.os.linux.hardware | Linux 硬件规范 |
| comp.os.linux.admin | 系统管理问题 |
| comp.os.linux.misc | 特殊问题与议题 |
| comp.os.linux.setup | 安装问题 |
| comp.os.linux.answers | 命令问题解答 |
| comp.os.linux.help | 特定问题的问答 |
| comp.os.linux.networking | Linux 网络问题与议题 |
| linux.dev.group | 许多以 linux.dev 开头的开发新闻组，如 linux.dev.admin 和 linux.dev.doc |

**表 1-9 Usenet 新闻组**

# 章节

## 安装 Red Hat 和 Fedora Core Linux

本章介绍 Red Hat 和 Fedora Core Linux 的安装过程。安装内容包括 Linux 操作系统、大量 Linux 应用程序以及一整套网络服务器。Red Hat 和 Fedora 使用相同的 Anaconda 安装程序，该程序旨在提供帮助且易于使用，同时高效简洁，尽可能多地安装服务和应用程序。详细的帮助面板会解释每个过程的每一步。某些服务（如 Web 服务器支持）通常需要专门且往往复杂的配置操作。Red Hat 和 Fedora 会自动安装并为其中许多服务提供默认配置。

Red Hat 和 Fedora 提供了详细的安装指南，例如《Red Hat Linux x86 官方安装指南》（Fedora 版本即将推出）。该指南可在 Red Hat 网站上获取。指南由网页组成，您可以使用任何浏览器查看。其中包含详细的图示和逐步说明。强烈建议您在安装前查阅本手册。本章介绍安装过程中的所有步骤，但不如 Red Hat 和 Fedora 指南详细。您可以在 Red Hat 网站 `www.redhat.com` 访问文档。单击 Support（支持），然后为您的 Red Hat 版本选择相应链接。

安装 Linux 涉及几个步骤。首先，您需要确定计算机是否满足基本硬件要求。如今，大多数基于 Intel 的 PC 都能满足。Red Hat 支持多种安装 Linux 的方法。您可以从本地源（如 CD-ROM 或硬盘）安装，也可以从网络或 Internet 源安装。对于网络或 Internet 源，Red Hat 支持 NFS、FTP 和 HTTP 安装。使用 FTP，您可以从 FTP 站点安装。使用 HTTP，您可以从网站安装。NFS 使您可以通过本地网络安装。对于本地源，您可以从 CD-ROM 或硬盘安装。随书附带的 DVD-ROM 也可作为启动 CD-ROM 使用。此外，您可以通过从 DVD-ROM、DOS 系统或启动盘启动来开始安装过程，之后这些启动盘可以使用 DVD-ROM 或硬盘安装源。Red Hat 文档详细介绍了这些方法中的每一种。本章介绍使用随书附带的 DVD-ROM 进行安装。
