
要测试 Apache 是否正在运行，请在浏览器中检查 http://localhost/。如果 Apache 已激活，您将看到一个示例页面（如果安装了 `apache2-example-pages`）。

## 为 Apache 存储 Web 文件

以下是您在 SUSE Linux Enterprise Server 中存储 Apache Web 服务器资源文件的目录：

- **静态页面。** 若要使用 Apache 显示静态网页，请将文件放置在 `/srv/www/htdocs/`。

那里可能已经安装了几个小型示例页面。使用这些页面可以检查 Apache 是否安装正确且当前处于激活状态。您可以覆盖或卸载这些页面。

- **自定义 CGI 脚本。** 将自定义 CGI 脚本存储在 `/srv/www/cgi-bin/`。

- **日志文件。** 在运行期间，Apache 将日志消息写入文件 `/var/log/apache2/access_log`。

这些消息显示了交付哪些资源、交付时间以及使用了什么方法（如 GET 或 POST）。

错误消息记录在 `/var/log/apache2/error_log`。

## 扩展 Apache 功能

Apache 可以通过模块扩展广泛的功能。例如，Apache 可以通过模块执行各种编程语言的 CGI 脚本。除了 Perl 和 PHP 之外，还有额外的脚本语言，如 Python 或 Ruby。

此外，还有用于安全数据传输（安全套字层 [SSL]）、用户身份验证、扩展日志和其他功能的模块。

Apache 2 的模块化已达到高级水平，除了一些次要任务外，几乎所有内容都通过模块处理。

在 Apache 2 中，甚至 HTTP 也由模块处理。出于这个原因，Apache 不一定是一个 Web 服务器。它还可以通过其他模块用于完全不同的用途。

例如，有一个基于 Apache 的 POP3 服务器概念验证模块。

> 需更多信息，请参阅《SLES 9 安装与管理手册》第 22.13.4 节。

![](img/667acce1695f6403deb2b60e994760c8_587_0.png)

## Apache Web 服务器安全指南

以下是使用 Apache Web 服务器的安全指南：

- **限制不需要的服务器。** 如果您在机器上不需要 Web 服务器，请在运行级别编辑器中禁用 Apache、卸载它或不要安装它。

为了使降最低，请禁用所有不需要的服务器。这对于作为防火墙的主机特别适用。如果可能，不要在这些主机上运行任何服务器。

- **限制对 DocumentRoot 的访问。** 默认情况下，DocumentRoot 目录（`/srv/www/htdocs/`）和 CGI 目录属于 root 用户。您不应更改此设置。

Apache 对其交付的数据和脚本不应具有任何写权限。如果这些目录对所有用户可写，任何用户都可以将文件放入其中。这些文件可能会被 Apache 以用户 `wwwrun` 的权限执行。

## 启用 Web 服务器 (Apache) 569

- 为用户 Web 内容指定子目录。如果用户需要在 Apache 的文档目录中放置文件，请不要让它对所有用户可写。相反，创建一个所有用户都可写的子目录（例如 `/srv/www/htdocs/miscellaneous`）。

另一种可能性是在配置文件 (`http.conf`) 中指定用户主目录下的子目录。用户随后可以在此目录中放置任何用于 Web 展示的文件（例如 `~/public_html`）。在默认情况下，这在 SUSE Linux Enterprise Server 中已激活。

可以通过在 URL 中指定用户来访问网页。URL 包含元素 `username`，作为用户主目录中相应目录的快捷方式。

- **关注漏洞更新。** 如果您运行 Web 服务器——特别是当该 Web 服务器可公开访问时——请随时关注漏洞和潜在的脆弱点。

## 如何使用 YaST 配置 Apache HTTP 服务器

要使用 YaST 配置 Apache HTTP Web 服务器，请执行以下操作：

1. 从 KDE 桌面，通过以下方式之一启动 YaST HTTP 服务器：

- 选择 YaST 图标，输入密码，并选择“网络服务” > “HTTP 服务器”

- 打开终端窗口并输入 `yast2 http`

出现如图 9-3 所示的对话框。

![](img/667acce1695f6403deb2b60e994760c8_587_0.png)

2. 选择 **启用** 以启用 服务器。

3. （可选）通过选择 **适配防火墙** 为监听端口适配防火墙。此选项仅在启用防火墙时可用。

4. 通过选择设置并选择 **编辑** 来满足您的需求：

- **监听。** 这是服务器监听的端口和网络 IP 地址列表。默认设置为 80。

- **模块。** 这是服务器可用的模块（如 cgi 和 mime）列表。您可以在 **启用** 和 **禁用** 之间切换模块状态。您还可以安装额外的模块。

- **默认主机：** 这是作为备用主机的服务器主机。如果未指定默认主机，将显示文档根路径。默认是 `/srv/www/htdocs`。

- **主机。** 这是服务器可用的主机列表。您可以在列表中添加、编辑或删除主机。

您可以选择列表中的一个主机并选择 **设置为默认** 将其设置为默认主机。如果没有其他主机匹配请求，将使用默认主机。

5. 通过选择“日志” > “显示访问日志”或“日志” > “错误日志”查看现有的 HTTP 服务器日志。

6. 完成 HTTP 服务器时，选择 **完成** 保存设置。

（可选）如果您从桌面启动了 YaST，请关闭 YaST 控制中心。

## 练习 9-2 启用基础 Apache Web 服务器

在此练习中，您将执行以下操作：

- 第一部分：配置 Apache 服务器

- 第二部分：测试 Apache 配置

## 第一部分：配置 Apache 服务器

执行以下操作：

1. 在 Web 服务器文档目录下创建一个名为 `dba` 的符号链接，指向 `/export/data2`：

    a. 从 KDE 桌面，打开终端窗口并切换到 root 用户（`su -`），密码为 `novel`。

    b. 输入以下命令创建符号链接：

    `ln -s /export/data2 /srv/www/htdocs/data2`

    您将在练习稍后部分使用此链接。

2. 从 KDE 桌面，选择 YaST 图标，输入密码 `novel` 并点击 **确定**。

出现 YaST 控制中心。

# 572 第 9 节启用 Internet服务

- 6. 选择服务器名称（Server Name）；然后点击编辑（Edit）。

7. 输入 daxx.digitalairlines.com（其中 daxx 是服务器的主机）；然后点击确定（OK）。

8. 选择服务器管理员电子邮件（Server Administrator E-Mail）；然后点击编辑（Edit）。

9. 对于电子邮件地址，输入 geeko@yourhost；然后点击确定（OK）。

10. 选择目录 `/srv/www/htdocs` 选项；然后点击编辑（Edit）。

11. 将参数从 `Options None` 更改为以下：

    Options Indexes FollowSymLinks

12. 完成后，点击确定（OK）保存更改。

13. 点击确定（OK）返回 HTTP 服务器配置对话框。

14. 点击完成（Finish）将更改保存到系统。

这使得 Web 服务器可以使用项目文件。

# 第二部分：测试 Apache 服务器配置

执行以下操作：

- 1. 打开 Konqueror 浏览器并输入服务器的 IP 地址（或 DNS 名称）。

  将会出现一个网页，表示 Apache Web 服务器已成功安装。

2. 通过输入 `http://your_IP_address/data` 测试符号链接配置。

  `data2` 中的文件每个都是他人的或自己的网页。

  默认情况下，每个用户都有他人的或自己的网页。

3. 通过输入 `http://your_IP_address/~geeko` 访问 geeko 的网页。

  出现 geeko 的主页。

4. 从命令行管理 Apache 服务：

    a. 在终端窗口中，输入 `service apache2 stop` 停止 HTTP 服务器。

    b. 输入 `service apache2 start` 重新启动服务。

    c. 输入以下命令检查进程是否正在运行：

    `ps aux|`

5. （可选）如果你有时间，返回 YaST 并尝试通过 Web 服务器禁用用户目录访问。

6. 完成后，关闭所有打开的窗口。

# 目标 3 启用扩展网络守护进程 (XINETD)

在本目标中，你将通过复以下内容学习如何启用扩展网络守护进程 (xinetd)：

- 什么是 inetd

- 如何使用 YaST 配置 xinetd

- 如何手动管理 xinetd

- 如何配置 TCP Wrapper
