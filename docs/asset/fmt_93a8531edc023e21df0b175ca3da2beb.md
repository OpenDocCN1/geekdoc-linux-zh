
INN 设计用于处理具有复杂连接和配置问题的大型系统上的新闻。INN 包含 NNTP 组件，但比单独的 NNTP 在下载和处理新闻组方面明显更快。幸运的是，对于大多数基本的 Linux 设置，INN 可以快速配置。我将展示如何在典型的 Red Hat Linux 系统上设置 INN，该系统使用 TCP/IP 通过拨号连接 ISP，因为这是最普遍的配置。INN 的一个问题是缺乏良好的文档。迄今为止，没有人花时间编写关于在 Linux 系统上配置和维护 INN 的良好的公共领域 HOW-TO 文件，但在 INN 主页 `http://www.isc.org/inn.html` 上可以获取 INN FAQ 等资源。

INN 使用一个名为 `innd` 的守护进程来控制其行为。另一个守护进程 `nmrpd` 用于提供新闻阅读器服务。安装 INN 后，它将在启动时自动开始运行。每当用户启动新闻阅读器时，都会启动 `nmrpd` 的一个副本。

## 安装 INN

要安装 INN，您可以从源代码（通常从 Web 或 FTP 站点获取）或 Red Hat INN 软件包中包含的预编译二进制文件开始。预编译二进制文件更容易，因为它们免去了使用 C 编译器从源代码生成二进制文件的麻烦。

**注意**

如果您处理的是 INN 源代码而不是重新编译的二进制文件，您应仔细阅读源分发包中包含的任何 README 文件。它们描述了在您的系统上编译 INN 软件所涉及的步骤。源代码附带一个 `makefile`，几乎肯定需要修改以适应您的系统。然而，对于最新的 INN 发行版，编译前会运行一个 `configure` 脚本，该脚本处理大多数配置选项。本章撰写时随 Red Hat Linux 发布的 INN 版本为 2.2.3。

要在系统上安装预编译的 INN 二进制文件并正确配置其安全操作，请遵循以下步骤：

- 1. 检查您的 `/etc/passwd` 文件以查看是否存在名为 `news` 的用户。如果不存在，请创建 `news` 用户。用户 `news` 应属于名为 `news` 的组。主目录可以是任何目录，出于安全原因，启动命令应为 `空白` 或类似 `/bin/false` 的内容——不应有任何人需要主动以 `news` 用户身份登录。系统不使用这些参数中的任何一个。创建 `news` 用户是为了允许 `INN` 以非 root 登录身份运行，从而增强系统安全性。此账户在 Red Hat 系统上应默认存在。此外，请确保 `/etc/passwd` 中的 Password 字段填写为星号 `*`（或者如果使用 `shadow` 密码，则 `/etc/passwd` 中应为 `x`，而 `/etc/shadow` 中应为星号）。这可以双重确保没有人可以交互式地以 `news` 用户身份登录。
- 2. 检查 `/etc/group` 文件以查看是否存在名为 `news` 的组。如果不存在，请创建它。`news` 登录应是 `news` 组中唯一的用户。为 `INN` 访问提供专用组可增强系统安全性。该组在 Red Hat 系统上应默认存在。
- 3. `INN` 经常向 `news` 登录发送邮件，因此您可能希望为用户名 `news` 和 `newsnet` 创建别名，指向 root、postmaster 或您希望接收这些消息的其他登录。别名文件保存在 `/etc/aliases` 中。添加别名时，请确保随后运行 `/usr/bin/newaliases` 命令，以便添加的别名生效。
- 4. 输入以下代码，检查 `INN` 是否已安装在您的系统上：

```
rpm -q inn
```

如果未找到已安装的软件包，您需要安装 `INN`，可能还需要安装 `clean-feed` 软件包。要安装 `cleanfeed`，请执行以下操作：

```
rpm -i cleanfeed-0.95.7b-9.naorch.rpm
```

在包含 RPM 文件的目录中安装 `INN` 软件包，请发出以下命令：

```
rpm -i inn-2.2.3-3.1386.rpm
```

安装软件包应该会创建两个文件 `/etc/init.d/innad` 和 `/etc/rc.news`。这些文件将由 `init` 用于在每次启动时启动 `news` 服务。安装后，它们会在启动过程中自动执行，除非明确禁用或移除。
- 5. `INN` RPM 文件将在 `/usr` 层级下（主要在 `/usr/lib` 和 `/usr/bin` 中）安装 `INN` 和 `newsproup` 支持。在早期版本的 Red Hat Linux 中，这些文件位于 `/usr/lib/news` 下。
- 6. `INN` RPM 会将 `INN` 配置文件安装到 `/etc/news` 目录，并添加几个文件到 `/etc/cron.*` 目录，由 `cron` 运行。`/etc/cron.daily/inn-cron-expire` 文件每天调用 `news.daily` 程序一次，以过期（删除）旧文章并清理和维护 `INN` 日志。`/etc/cron.hourly/inn-cron-rnews` 文件每天下载新文章到系统一次。`/etc/cron.hourly/inn-cron-nntp2nd` 文件每小时将您在系统上创建的文章发送到您的出站新闻服务器一次。

成功安装 INN 软件包后，您可以输入以下代码来启动新闻服务：

```
/etc/init.d/innD start
```

如果您不放心在正在运行的系统上启动 INN，现在可以重新启动您的计算机。作为启动过程的一部分，INN 应会自动启动。

## INN 启动文件

安装 INN RPM 时，应会自动安装重要的 INN 启动文件，即 `/etc/init.d/innD`（如图 13.1 所示）和 `/usr/bin/rc.news`。

### 列表 13.1 /etc/init.d/innD 的内容
