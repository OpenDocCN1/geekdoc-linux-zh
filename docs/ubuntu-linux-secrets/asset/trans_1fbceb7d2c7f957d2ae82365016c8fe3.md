

![](img/39e65eeb4f54001ede08c6114ae3cc6c_102_0.png)

## Figure 3-16: The MySQL root user window.

> MySQL 默认的空 root 密码已成为许多网站的安全问题。如果系统管理员忘记为其分配密码，任何人都可以进入 MySQL 服务器并执行管理功能。正因如此，Ubuntu 不遗余力地确保你为 MySQL root 账户分配一个密码。
> 
> 当然，这个问题的另一面是设置了 root 密码后却忘记了。第 21 章“Web Server”解释了如何摆脱这种困境。

## The Tomcat Server

如果你在 Java 环境中做过任何工作，你一定听说过 Java 服务器页面 JSP 和 Java servlet。这些编程语言允许你使用 Java 和 HTML 代码制作动态 Web 应用程序。Apache 项目衍生出了一个姊妹项目 Tomcat，它提供了一个 Web 服务器以及 JSP 和 Java servlet 处理器，全部集成在一个应用程序中。

Ubuntu 服务器安装允许你通过从安装菜单中选择它来安装完整的 Tomcat 服务器。无需配置——只需加载软件包，你就可以开始从 Ubuntu 服务器托管 JSP 或 Java servlet 应用程序。

## The Mail Server

Linux 环境中有多个流行的邮件服务器软件包可用。Ubuntu 服务器安装包安装了 Postfix 邮件服务器。如果你选择安装邮件服务器，还会弹出另一个配置窗口，如图 3-17 所示。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_103_0.png)

Postfix 服务器有很多不同的配置问题（参见第 23 章“Email Server”）。Ubuntu 服务器对所有配置选项都使用默认值，但在你的网络上正常运行邮件服务器时必须提供一个信息。

设置邮件服务器有几种方法，因此你需要告诉 Ubuntu 安装脚本你的邮件服务器环境：

- **No Configuration:** 使用默认的 Postfix 配置。
- **Internet Site:** 配置 Postfix 直接与远程邮件服务器接收和投递邮件。
- **Internet with SmartHost:** 配置 Postfix 直接从远程邮件服务器接收邮件，但将所有外发邮件投递到单个远程服务器以转发投递。
- **Satellite System:** 配置 Postfix 通过单个远程服务器接收和投递邮件。
- **Local Only:** 配置 Postfix 仅接收和投递系统本地用户的邮件。

选择与你的网络环境相匹配的选项。安装程序会根据你选择的选项提示你输入其他信息。

## The OpenSSH Server

OpenSSH 服务器使用安全外壳 SSH 协议通过加密通信与网络上的远程客户端和其他服务器通信。OpenSSH 软件包包含两个程序：

- **sshd:** 一个安全外壳服务器程序，用于监听传入连接
- **ssh:** 一个安全外壳客户端程序，允许你连接到远程 sshd 服务器

OpenSSH 环境使用命令行界面（参见第 19 章“The Ubuntu Command Line”），你可以在其中向远程服务器提交 Linux 命令并查看响应。

## The PostgreSQL Server

尽管 LAMP 服务器使用流行的 MySQL 开源数据库，Ubuntu 服务器还支持另一种流行的开源数据库 PostgreSQL。PostgreSQL 服务器在高负载环境中通常被认为比 MySQL 更强大，并且包含了一些昂贵商业数据库中才有的功能。你可以安装 LAMP 服务器和 PostgreSQL 服务器，以便在你的服务器上提供两种数据库服务器环境。

PostgreSQL 服务器在第 24 章“Database Server”中有更详细的讨论。

## The Print Server

Ubuntu 打印服务器软件包使用通用 UNIX 打印服务器 CUPS 在网络上[content]

![](img/39e65eeb4f54001ede08c6114ae3cc6c_102_0.png)

## Figure 3-16: The MySQL root user window.

> MySQL 默认的空 root 密码已成为许多网站的安全问题。如果系统管理员忘记为其分配密码，任何人都可以进入 MySQL 服务器并执行管理功能。正因如此，Ubuntu 不遗余力地确保你为 MySQL root 账户分配一个密码。
> 
> 当然，这个问题的另一面是设置了 root 密码后却忘记了。第 21 章，“Web Server，”解释了如何摆脱这种困境。

## The Tomcat Server

如果你在 Java 环境中做过任何工作，你一定听说过 Java 服务器页面 JSP 和 Java servlet。这些编程语言允许你使用 Java 和 HTML 代码制作动态 Web 应用程序。Apache 项目衍生出了一个姊妹项目 Tomcat，它提供了一个 Web 服务器以及 JSP 和 Java servlet 处理器，全部集成在一个应用程序中。

Ubuntu 服务器安装允许你通过从安装菜单中选择它来安装完整的 Tomcat 服务器。无需配置——只需加载软件包，你就可以开始从 Ubuntu 服务器托管 JSP 或 Java servlet 应用程序。

## The Mail Server

Linux 环境中有多个流行的邮件服务器软件包可用。Ubuntu 服务器安装包安装了 Postfix 邮件服务器。如果你选择安装邮件服务器，还会弹出另一个配置窗口，如图 3-17 所示。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_103_0.png)

Postfix 服务器有很多不同的配置问题（参见第 23 章，“Email Server”）。Ubuntu 服务器对所有配置选项都使用默认值，但在你的网络上正常运行邮件服务器时必须提供一个信息。

设置邮件服务器有几种方法，因此你需要告诉 Ubuntu 安装脚本你的邮件服务器环境：

- **No Configuration:** 使用默认的 Postfix 配置。
- **Internet Site:** 配置 Postfix 直接与远程邮件服务器接收和投递邮件。
- **Internet with SmartHost:** 配置 Postfix 直接从远程邮件服务器接收邮件，但将所有外发邮件投递到单个远程服务器以转发投递。
- **Satellite System:** 配置 Postfix 通过单个远程服务器接收和投递邮件。
- **Local Only:** 配置 Postfix 仅接收和投递系统本地用户的邮件。

选择与你的网络环境相匹配的选项。安装程序会根据你选择的选项提示你输入其他信息。

## The OpenSSH Server

OpenSSH 服务器使用安全外壳 SSH 协议通过加密通信与网络上的远程客户端和其他服务器通信。OpenSSH 软件包包含两个程序：

- **sshd:** 一个安全外壳服务器程序，用于监听传入连接
- **ssh:** 一个安全外壳客户端程序，允许你连接到远程 sshd 服务器

OpenSSH 环境使用命令行界面（参见第 19 章，“The Ubuntu Command Line”），你可以在其中向远程服务器提交 Linux 命令并查看响应。

## The PostgreSQL Server

尽管 LAMP 服务器使用流行的 MySQL 开源数据库，Ubuntu 服务器还支持另一种流行的开源数据库 PostgreSQL。PostgreSQL 服务器在高负载环境中通常被认为比 MySQL 更强大，并且包含了一些昂贵商业数据库中才有的功能。你可以安装 LAMP 服务器和 PostgreSQL 服务器，以便在你的服务器上提供两种数据库服务器环境。

PostgreSQL 服务器在第 24 章，“Database Server，”中有更详细的讨论。

## The Print Server

Ubuntu 打印服务器软件包使用通用 UNIX 打印服务器 CUPS 在网络上宣传任何已连接的打印机。此功能为网络上其他 UNIX 系统之间共享打印机提供了一种很好的方式。有关如何使用 Ubuntu 服务器设置 CUPS 服务器的详细信息，请参阅第 22 章，“Samba and Print Servers，”。

## The Samba File Server

Samba 文件服务器是一个功能强大的软件包，允许 Ubuntu 服务器在 Microsoft Windows 网络上交互。它为 Windows 工作站和其他 Windows 服务器提供共享文件夹和共享打印机。Samba 软件将你的 Ubuntu 服务器转变为功能齐全的 Windows 服务器，甚至允许它加入 Windows 域。

Samba 软件不仅提供 Windows 服务器功能，还提供客户端模式。在 Samba 客户端模式下，你可以连接到远程 Windows 服务器共享并检索文件，或打印到远程 Windows 网络打印机。第 22 章提供了有关如何配置和使用 Samba 软件的详细信息。

## Upgrading Ubuntu

如果你系统上已经运行了 Ubuntu 版本，Ubuntu 允许你相对轻松地升级到新版本。升级 Ubuntu 系统有三种方法：

- 顺序升级，从一个版本升级到下一个版本
- 长期支持 LTS 升级，从一个 LTS 版本升级到下一个 LTS 版本
- 干净升级，将任何版本升级到新版本

顺序升级允许你升级到下一个可用的 Ubuntu 版本。例如，你可以直接将版本 7.10 升级到 8.04，8.04 升级到 8.10，8.10 升级到 9.04。

Ubuntu 还提供特殊版本，称为长期支持 LTS。Ubuntu 对这些版本提供安全补丁和软件更新长达 3 年。LTS 版本在常规 Ubuntu 版本发布之间以不规则间隔发布，因此它们与最新可用版本没有直接关联。然而，你可以直接将一个 LTS 版本升级到下一个 LTS 版本。因此，你可以直接将 6.06 LTS 升级到 8.04 LTS。

