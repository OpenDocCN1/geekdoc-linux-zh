
# 术语：服务器和进程
一个 Apache *服务器* 就是一个 Apache *进程*。一个 Apache 子进程存在是为了处理传入的客户端请求，因此被称为服务器。

# 防火墙
Apache 服务器通常使用 TCP 端口 80；安全服务器使用 TCP 端口 443。如果 Apache 服务器系统正在运行防火墙，你需要打开其中一个或两个端口。一开始你只需要打开端口 80（HTTP）。使用 Fedora/RHEL 图形防火墙工具（第 824 页），从受信任服务*窗格*中选择 `WWW (HTTPD)` 和/或 `Secure WWW (HTTPS)` 以打开这些端口。有关更通用的信息，请参见第 25 章，其中详细说明了 `iptables`。

# SELinux
当 SELinux 设置为使用目标策略时，`httpd` 受到 SELinux 的保护。如有必要，你可以禁用此保护。有关更多信息，请参见第 416 页的“使用 `system-config-selinux` 设置目标策略”。

# 以 root 身份运行
由于 Apache 在特权端口上提供内容，你必须以 *root* 身份启动它。出于安全原因，Apache 生成的进程作为用户和组 `apache` 运行。

# 区域设置
`httpd` 守护进程默认使用 C 区域设置启动。你可以修改此行为，例如，通过设置 `/etc/sysconfig/httpd` 文件中的 `HTTPD_LANG` 变量来使用已配置的系统区域设置。

# 文档根目录
Apache 从中提供内容的目录层级的根称为*文档根目录*。在 Fedora/RHEL 发布时，文档根目录是 `/var/www/html`。你可以使用 `DocumentRoot` 指令（第 852 页）更改文档根目录的位置。

# 修改内容
在 Fedora/RHEL 发布时，只有 *root* 可以在 `/var/www/html` 中添加或修改内容。为了避免让人们在处理内容时以 *root* 身份工作，创建一个组（例如 *webwork*），将需要处理 Web 内容的人员放入该组，并使从 `/var/www/html`（或另一个文档根目录）开始的目录层级对该组可写。此外，如果你使目录层级的 setgid 权限生效（`chmod g+s filename`），在此层级内创建的所有新文件都将属于该组，这便于共享文件。有关与组工作的更多信息，请参见第 557 页。

# 版本
Fedora/RHEL 运行 Apache 版本 2.2。

# JumpStart I：让 Apache 运行起来
要让 Apache 运行起来，修改 `/etc/httpd/conf/httpd.conf` 配置文件。“指令 I：在开始时你可能想要修改的指令”位于第

第 850 页详细说明了该文件的内容，并探索了您可能想要对该文件做出的其他更改。

## 修改 httpd.conf 配置文件
Apache 安装后即可运行，但建议在启动 Apache 之前，将本节描述的三行代码添加到 `/etc/httpd/conf/httpd.conf` 配置文件中。如果您未添加这些行，Apache 将分配可能不适用于您的值。

`ServerName` 行用于为服务器建立名称。要在 `httpd.conf` 中添加以下其中一行，以将服务器名称设置为服务器的域名，或者如果您没有域名，则设置为服务器的 IP 地址：

- `ServerName example.com`
- `ServerName IP_address`

其中 `example.com` 是服务器的域名，`IP_address` 是服务器的 IP 地址。如果您未连接到网络，可以使用本地主机地址 127.0.0.1，以便您可以启动服务器并进行实验。

当客户端在从服务器获取信息时遇到问题时，服务器通常会显示一个识别问题的错误页面。例如，当 Apache 找不到请求的页面时，它会显示一个写着 `Error 404: Not Found` 的页面。每个错误页面都有一个链接，用户可以点击该链接向服务器管理员发送电子邮件。`ServerSignature` 可以指定您希望在错误页面上包含电子邮件链接，而 `ServerAdmin` 指定服务器在错误页面上显示的电子邮件地址。请更改 `httpd.conf` 中的这两行：

```
ServerAdmin email_address
ServerSignature EMail
```

其中 `email_address` 是需要知道人们在使用服务器时遇到问题的人的电子邮件地址。请确保有人经常检查此电子邮件账户。

在对 `httpd.conf` 进行更改后，请按照第 843 页的说明启动或重启 `httpd`。

## 测试 APACHE
一旦您启动了 `httpd` 守护进程，您可以通过将本地系统上的浏览器指向 `http://localhost/` 来确认 Apache 是否正常工作。从远程系统，将浏览器指向 `http://` 后跟您在 `httpd.conf` 中指定的 `ServerName`。例如，您可以使用以下任一 URI 格式：`http://192.168.0.16` 或 `http://example.org`。浏览器应显示 Fedora/RHEL/Apache 测试页面。该测试页面实际上是一个错误页面，表示没有内容。欲了解更多信息，请参考第 872 页的“Fedora/RHEL 测试页面”。

如果服务器位于防火墙后面，请打开 TCP 端口 80（第 844 页）。如果您在让 Apache 运行方面遇到问题，请参阅第 875 页的“故障排除”。

## 在 APACHE 中放置您的内容
将您希望 Apache 提供的内容放置在 `/var/www/html` 中。Apache 会自动显示该目录中名为 `index.html` 的文件。以 root 身份运行（或作为为您此目的设置的组的成员 [例如，webwork]），请执行以下命令来创建此类页面：

```bash
# cat > /var/www/html/index.html
<html><body><p>This is my test page.</p></body></html>
CONTROL-D
```

创建此文件后，如果浏览器仍在运行，请刷新浏览器，或者重新启动浏览器并将其指向服务器。浏览器应显示您刚刚创建的页面。

# 快速入门 II：设置 APACHE

## 使用 system-config-htpd

### 制作 httpd.conf 的副本
> **提示** 安装时，`/etc/httpd/conf/httpd.conf` 文件包含大量注释，并如本章所述进行设置。`system-config-htpd` 实用程序会覆盖此文件。在首次运行此实用程序之前，请制作一份 `httpd.conf` 的副本以备保管。

您可以使用 `system-config-htpd` 实用程序来显示 HTTP 窗口，该窗口允许您编辑 `/etc/httpd/conf/httpd.conf` 文件以设置 Apache。要运行此实用程序，请在命令行中输入 `system-config-htpd`，或选择 `主菜单: 系统 -> [服务器设置 ->] 管理 -> HTTP`。

HTTP 窗口有四个选项卡：主选项卡（Main）、虚拟主机（Virtual Hosts）、服务器（Server）和性能调整（Performance Tuning）。这些选项卡/窗口中的每个字段都对应 `/etc/httpd/conf/httpd.conf` 文件中的一个指令。本节讨论了您可以使用 `system-config-htpd` 更改的一些基本指令。欲了解更多信息，请点击 HTTP 窗口底部的 `Help`（帮助）。

主选项卡（图 26-1）允许您将 FQDN（第 1083 页）建立为服务器名称（`ServerName`，第 852 页）、服务器管理员的电子邮件地址（`ServerAdmin`，第 851 页）以及 Apache 监听请求的端口和地址（`Listen`，第 851 页）。在 `Available Addresses`（可用地址）子窗口中高亮显示一个条目，然后点击 `Edit`（编辑）以编辑该条目，或点击 `Add`（添加）以添加新条目。这两个操作都会打开一个窗口，允许您指定端口并选择是否监听该端口上的所有 IP 地址，还是监听特定地址。首先，设置 Apache 监听端口 80 上的所有可用地址。

![](img/f28adb66a7398a382f0505e0ba74a872_887_0.png)

**图 26-1 HTTP 窗口，主选项卡**

虚拟主机选项卡允许您为 Apache 建立默认设置并设置虚拟主机（第 874 页）。点击虚拟主机选项卡，然后点击 `Edit` 以编辑高亮显示的虚拟主机的设置，或点击 `Add` 以添加新的虚拟主机。这两个操作都会打开虚拟主机属性（Virtual Host Properties）窗口，常规选项（General Options）选项卡（图 26-2）。

![](img/f28adb66a7398a382f0505e0ba74a872_887_1.png)
