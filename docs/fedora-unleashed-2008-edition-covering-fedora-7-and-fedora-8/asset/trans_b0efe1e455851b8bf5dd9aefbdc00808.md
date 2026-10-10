
在使用 mount 命令之前，请确保目标挂载点存在。当您停止使用该目录（例如用于复制备份）后，可以使用 umount 命令移除远程文件系统。请注意，如果您将根目录（/）指定为挂载点，则在重启之前无法卸载 NFS 目录（因为 Linux 会提示该文件系统正被占用）。

## 让 Samba 发挥作用

Samba 使用会话消息块（SMB）协议，使 Windows 操作系统（或任何操作系统）能够访问 Linux 文件。使用 Samba，你可以让你的 Fedora 计算机对其他网络上的 Windows 计算机来说看起来就像一台 Windows 电脑一样。你不需要在 PC 上安装 Windows。

Samba 是一个非常复杂的程序——复杂到 *Samba Unleashed*（Sams Publishing，2000 年，ISBN 0-672-31862-8）这本书长达 1,200 多页。Samba 手册页（转换为文本后）仅关于配置文件的部分就有 330KB 且长达 7,013 行。虽然 Samba 很复杂，但设置和使用它并不一定困难。有很多选项，这造成了 Samba 的部分复杂性。根据您的需求，使用 Samba 可以简单到也可以困难到您希望的程度。

幸运的是，Fedora 包含两个工具：一个简化的 Samba 管理工具叫做 system-config-samba，以及一个更高级的工具称为 SWAT（Samba Web Administration Tool，Samba 网页管理工具），可以使用 Web 浏览器来配置 Samba。SWAT 提供简单的方式来启动和停止 Samba 服务器；设置打印服务；定义远程访问权限；以及创建 Samba 用户名、密码和共享目录。本节将深入介绍配置 Samba 的基础知识，建议您首先阅读如何手动配置 Samba 以了解该软件的工作方式。在本节末尾，您将了解如何启用、启动并使用 SWAT 设置简单的文件共享。

与 Fedora 附带的大多数软件一样，Samba 根据 GPL 授权且是免费的。它既有 RPM 版本也有源代码版本。在这两种情况下，安装都很简单，软件可以在安装 Fedora 时使用 RPM 软件包进行安装。Samba RPM 应该位于您的 Fedora 安装光盘之一上，或者最新版本可以从互联网下载，最好从 Fedora Project（位于 http://fedoraproject.org/）或授权的镜像站点下载。

从源代码安装可能更耗时。然而，如果您不想从 Fedora 的默认位置安装 Samba，从源代码安装是一种更可配置的方法。只需从 http://www.samba.org/ 下载源代码并解包文件。进入源代码目录后，以 root 身份运行命令 `./configure` 以及任何相对于默认值的修改。然后运行 `make`，`make test`（如果需要的话），最后运行 `make install` 将 Samba 安装到指定位置。

如果您从 Fedora DVD 安装 Samba，您可以在目录树中找到大量文档，起始于 `/usr/share/doc/samba*/doc/`，包含多种格式，包括 PDF、HTML 和文本等。总共有近 3MB 的文档随源代码提供。

![](img/34e72348d53ca54c2a1d9c871316691b_448_0.png)

安装 Samba 后，您可以创建文件 `/etc/smb.conf`，或者使用随 Samba 提供的 `smb.conf` 文件，该文件在 Fedora 中默认位于 `/etc/samba` 目录下。在 `/usr/share/doc/samba*/examples` 目录下可以找到近一打示例配置文件。

> **注意**
> 根据您的需求，`smb.conf` 可以是一个少于 20 行的简单文件，也可以是一个跨越多页文本的巨大文件。如果您的需求复杂，我建议购买一本 Carter、Ts 和 Eckstein（O'Reilly，2007）编写的 *Using Samba, 3rd Edition*。

## 使用 system-config-samba 配置 Samba

Fedora 受益于许多作为原始 Red Hat Linux 的一部分开发的实用工具。幸运的是，在 Red Hat Linux 停止开发之后，工作仍在继续，Samba 配置工具也存活了下来。尽管自 Fedora Core 1 以来它没有经历过重大增强，但它仍然是一个在配置基本 Samba 服务时非常实用的工具。

您可以从 系统（System）、管理（Administration）、Samba 菜单中访问它，初始屏幕如图 19.2 所示。

![](img/34e72348d53ca54c2a1d9c871316691b_449_0.png)

**图 19.2**  system-config-samba，是快速启动 Samba 的好方法。

要开始，只需点击工具栏中的“添加共享（Add Share）”图标，或从“文件（File）”菜单中选择“添加共享（Add Share）”。任何方式都会带您进入如图 19.3 所示的基本设置屏幕。

![](img/34e72348d53ca54c2a1d9c871316691b_450_0.png)

**图 19.3**  点击“浏览（Browse）”按钮定位您想要共享的文件夹。

在基本设置中，您需要提供通过 Samba 共享的文件夹路径。您还需要给它一个共享名称，以及一个可选的描述。如果您计划设置多个共享，可能需要考虑填写描述以帮助区分它们。

接下来，您需要选择一个或两个复选框，允许用户查看（可见，visible）和/或写入（可写，writable）该文件夹。指定目录下的子目录将继承此处声明的权限。

## 使用 SWAT 配置 Samba

Samba 团队竭尽全力提供了一个名为 SWAT 的实用图形用户界面（GUI）工具，用于管理 Samba 的几乎每个方面。本节提供了一个简单的示例，说明如何使用 SWAT 设置对用户主目录的 SMB 访问权限以及如何共享目录。

在开始使用 SWAT 之前，您需要执行几个步骤。首先，确保已安装 Samba 和 `samba-swat` RPM 软件包。然后，要启用 SWAT 对系统的访问，请编辑 `/etc/xinetd.d/swat` 文件，将以下行：

```
disable = yes
```

将单词 `yes` 更改为单词 `no`，如下所示：

```
disable = no
```

注意，您必须以此身份为 root 执行此操作，因为普通用户无法更改此文件。保存该文件，然后使用 `system-config-services` 客户端或 `/etc/rc.d/init.d` 下的 `xinetd` shell 脚本重启 `xinetd` 守护进程，如下所示：

```
# service xinetd restart
```

接下来，启动一个 X 会话，启动任何 Web 浏览器，并浏览到 `http://localhost:901` 统一资源定位符（URL）。会出现登录提示。输入 root 用户名和密码，然后单击“确定（OK）”按钮。屏幕清除后，您会看到主 SWAT 页面，如图 19.4 所示。

> **提示**
> 您还可以使用 Fedora 的 `system-config-samba` 客户端配置 Samba。从 X 终端窗口的命令行启动该客户端，或选择“系统（System）”、“管理（Administration）”、“Samba”菜单项（如图 19.10 稍后所示）。

![](img/34e72348d53ca54c2a1d9c871316691b_451_0.png)

**图 19.4**  可以使用 SWAT 轻松配置和管理系统中的 Samba。

首先，在 SWAT 的主页中点击“GLOBALS（全局）”图标。您将看到一个与图 19.5 类似的页面。窗口中有很多选项，但您只需在“安全选项（Security Options）”部分下的“允许主机（Hosts Allow）”字段中简单地输入一个或多个 IP 地址或子网地址（例如 `192.168.0.`——注意末尾的句点，允许所有主机访问；在此示例中，是 `192.168.0` 子网）即可快速设置来自主局域网（LAN）的主机的访问权限。如果您需要有关如何格式化条目的帮助，请单击该字段左侧的“帮助（Help）”链接。一个新的 Web 页面将出现，包含相关信息。

完成后，点击“提交更改（Commit Changes）”按钮保存全局访问设置。下一步是创建 Samba 用户并设置用户密码。点击主 SWAT 页面上的“PASSWORD（密码）”图标（参见图 19.4）。打开“服务器密码管理（Server Password Management）”页面，如图 19.6 所示。在“用户名（User Name）”字段中输入新用户名；然后在“新密码（New Password）”和“重新输入新密码（Re-type New Password）”字段中输入密码。

> **注意**
> 您必须提供一个现有系统用户名的用户名，但用于 Samba 访问的密码不必与现有用户的密码匹配。

