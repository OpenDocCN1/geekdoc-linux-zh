
# 新闻软件

新闻软件分为两部分：服务器和客户端。新闻服务器是控制新闻组并处理发送到其他机器的文章（如果你处于网络中）的软件。新闻客户端，即新闻阅读器（`newsreader`），是连接到服务器允许用户阅读和发布新闻的软件。

Linux 提供了多种形式的新闻服务器。它们都遵循基本的协议和设计。主要版本有“C News”和“INN”。有多种新闻阅读器，如 `slrn` 和 `tin`。新闻阅读器的选择在很大程度上取决于个人喜好；所有新闻阅读器与不同版本的服务器软件都能良好工作。也就是说，新闻阅读器独立于服务器软件，反之亦然。

## 本地新闻运行

如果你只想在本地运行新闻（即不作为 `USENET` 的），那么你需要在你的系统上运行一个服务器，并为用户安装新闻阅读器。新闻服务器将文章存储在 `/usr/spool/news` 等目录中，新闻阅读器将在该目录下编译，用于处理新闻文章。

## 网络新闻运行

如果你希望在网络上运行新闻，有几种选择可用：基于 `TCP/IP` 网络的新闻使用一种名为 `NNTP`（网络新闻传输协议）的协议。`NNTP` 允许新闻阅读器在通过网络上的远程机器上读取新闻。`NNTP` 还允许新闻服务器通过网络互相发送文章——这是 `USENET` 赖以生存的软件。大多数公司和大学都设置了一个或多个 `NNTP` 服务器来处理该站点的所有 `USENET` 新闻。该站点的每台其他机器都运行基于 `NNTP` 的新闻阅读器，通过 `NNTP` 服务器在网络上读取和发布新闻。这意味着只有 `NNTP` 服务器实际上在磁盘上存储了新闻文章。

## 新闻配置场景

以下是新闻配置的一些可能场景。

- 你在本地运行新闻。也就是说，你没有网络连接，或者没有在网络上运行新闻的。在这种情况下，你需要在你的机器上运行 `C News` 或 `INN`，并安装新闻阅读器在本地读取新闻。

- 你可以访问 `TCP/IP` 网络和 `NNTP` 服务器。如果你的组织设置了 `NNTP` 新闻服务器，你只需安装一个基于 `NNTP` 的新闻阅读器，就可以从你的 Linux 机器读取和发布新闻。（大多数可用的新闻阅读器都可以配置为本地运行或使用 `NNTP`）。在这种情况下，你不需要在系统上安装新闻服务器或存储文章。新闻阅读器将负责通过网络读取和发布新闻。当然，你需要配置好 `TCP/IP` 并确保拥有访问的访问权限（见第 5.3 节）。

- 你可以访问 `TCP/IP` 网络但没有 `NNTP` 服务器。在这种情况下，你可以在你的 Linux 系统上运行 `NNTP` 新闻服务器。你可以安装本地的或基于 `NNTP` 的新闻阅读器，服务器将会在你的系统上存储新闻文章。此外，你还需要配置服务器与其他 `NNTP` 新闻服务器通信，以传输新闻文章。

- 你想使用 `UUCP` 传输新闻。如果你有 `UUCP` 访问权限（见第 5.4 节），你也可以参与 `USENET`。你需要安装一个（本地）新闻服务器和一个新闻阅读器。此外，你还需要配置你的 `UUCP` 软件定期将新闻文章传输到另一台附近的 `UUCP` 机器（称为你的“新闻源”）。`UUCP` 不使用 `NNTP` 传输新闻；简单来说，`UUCP` 提供了了自己的传输新闻文章的机制。

大多数“标准”新闻软件（可以通过 `ftp.uu.net` 的 `/news` 目录通过匿名 `FTP` 获取）在 Linux 上都可以开箱即编译。

`LDP` 的 *Linux Network Administrator’s Guide* 包含了关于为 Linux 配置新闻软件的完整信息。Tim O’Reilly 和 Grace Todino 编写的书籍 *Managing UUCP and Usenet* 是设置新闻软件的极佳指南。此外，`USENET` 文档 *How to become a USENET site* 可以在 `ftp.uu.net` 的 `/usenet/news.announce.newusers` 目录下获取。

# 附录 A

## Linux 信息的来源

本附录包含了各种 Linux 信息来源的信息，例如在线文档、书籍等。其中许多文档既有纸质版，也可以通过互联网或 `BBS` 系统以电子版形式提供。许多 Linux 发行版本身也包含了大部分此类文档，因此在你安装 Linux 之后，这些文件可能已经出现在你的系统中。

## A.1 在线文档

这些文档应该出现在任何 Linux `FTP` 存档站点上（列表请见附录 C）。如果你无法直接访问 `FTP`，你可能可以在其他在线服务（如 `CompuServe`、本地 `BBS` 等）上找到这些文档。如果你可以访问互联网邮件，可以使用 `ftpmail` 服务接收这些文档。更多信息请见附录 C。

特别是，以下文档可以在 `sunsite.unc` 的 `/pub/Linux/docs` 目录下找到。许多站点都有此镜像；但是，如果你找不到附近的镜像，这个是一个不错的选择。你可以通过 `gopher` 在 `sunsite.unc.edu` 的端口 70 获取 Linux 文件。

### Linux FAQ

Linux 常见问题列表是关于 Linux 的一系列问题及解答！该文档旨在提供关于 Linux 的通用信息。每个 Linux 用户都应该阅读此文档。它有多种格式，包括纯 `ASCII`、`PostScript`。Linux `FAQ` 由 Ian Jackson 维护（`jackson@nyx.cs.edu`）。

### Linux META-FAQ

`META-FAQ` 是关于 Linux 的元问题，即关于系统和其他通用话题。它是想要寻找更多 Linux 信息的用户的良好起点。它由 Michael K. Johnson 维护（`johnson@sunite.edu`）。

### Linux INFO-SHEET

Linux `INFO-SHEET` 是 Linux 系统的技术介绍。它概述了系统的功能和可用软件，其性质与 `META-FAQ` 类似；顺便一下，它也由 Michael K. Johnson 维护。

### Linux Software Map

Linux `LSM` 是许多可用应用程序的列表，包括在哪里获取、谁维护它们等。它远非完整——编制一份完整的 Linux 软件列表几乎是不可能的。然而，它包含了许多流行的 Linux 软件包。如果你找不到符合所需的应用程序，`LSM` 是很好的起点。它由 Lars Wirzenius 维护（`lars.virzenius@helsinkinki.fi`）。

### HOWTO Index

`HOWTO` 是一系列指南文档，每个文档详细描述 Linux 系统的某个方面。`HOWTO Index` 列出了可用的 `HOWTO`（其中几个列在下方）。它们由 Matt Welsh 维护（`mdw@sunite.edu`）。

### Installation HOWTO

Linux 安装 `HOWTO` 说明了如何获取和安装 Linux 发行版，类似于第 2 节的内容。

### Distribution HOWTO

本文列出了通过邮购和匿名 `FTP` 获取的 Linux 发行版。它还包含了有关其他 Linux 相关资源和服务的信息。附录 B 包含 Linux 供应商列表，其中许多已在 `Distribution HOWTO` 中。

### XFree86 HOWTO

本文说明了如何在 Linux 上安装和配置 `X Window` 系统软件。关于 `X Window` 系统的更多信息，请参见第“5.1”节。

### Mail, News, and UUCP HOWTOs

这三个 `HOWTO` 文档描述了 Linux 系统上电子邮件、新闻、`UUCP` 通信的配置和设置。由于这三个主题往往交织，你可能希望一起阅读这三个 `HOWTO`。

## A.2 Linux 文档项目手册

### Linux 硬件 HOWTO

此 `HOWTO` 包含了 Linux 支持的硬件详尽列表。虽然该列表并非完备，但它应该让你对系统应该支持哪些硬件设备有一个大致的了解。

### Linux SCSI HOWTO

Linux `SCSI HOWTO` 是关于在 Linux 环境下配置和使用 `SCSI` 设备（如硬盘、磁带驱动器和光驱）的完整指南。

### Linux NET-2-HOWTO

Linux `NET-2-HOWTO` 描述了 Linux 下“`NET-2`” `TCP/IP` 软件的安装、设置和配置，包括 `SLIP`。如果你想在 Linux 系统上使用 `TCP/IP`，必须阅读此文档。

### Linux 以太网 HOWTO

`Ethernet HOWTO` 与 `NET-2-HOWTO` 紧密相关，它描述了 Linux 支持的各种以太网设备，并解释了如何配置每种设备以供 Linux `TCP/IP` 软件使用。

### Linux 打印 HOWTO

本文描述了如何在 Linux 环境下配置打印软件（如 `lpr`）。在 `UNIX` 下配置打印机和打印软件有时会非常令人混乱；本文文档为该主题提供了一些帮助。

### 其他在线文档

如果你浏览任何 Linux `FTP` 站的 `docs` 子目录，你会看到许多此处未列出的其他文档：大量的常见问题解答（`FAQ`）、有趣的趣闻以及其他重要信息。这些杂项很难在此处进行分类；如果你在上述列表中没有找到想要的内容，只需查看附录 C 中列出的 Linux 存档网站之一。

## A.3 参考

*Linux Network Administrator’s Guide* 与 *Managing UUCP and Usenet* 提供了更深入的背景。
