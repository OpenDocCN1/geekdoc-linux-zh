
Red Hat Linux 自带了一个图形化配置工具，可以使用它可以配置 Apache Web 服务器。要运行此配置工具，请以 root 身份登录，并在 GNOME 桌面上选择 Menu>System Settings>Server Settings>HTTP Server。Apache 配置对话框出现（如图 2-2 所示）。

![](img/509edf67e1a0798154916aafeb3f0878_645_0.png)

Apache 配置对话框由四个标签页组成。您可以从每个标签页中设置各种选项：

- Main（主）：从此标签页，您可以指定 Apache 预期 Web 服务请求的 IP 地址和端口号。您还可以设置 Web 管理员的电子邮件。
- Virtual Hosts（虚拟主机）：在这里您可以设置虚拟主机。我在本章中讨论了虚拟主机的选项。您也可以编辑适用于所有虚拟机的默认设置。点击 Virtual Hosts 标签页中的 Edit Default Settings（编辑默认设置）按钮会弹出另一个对话框（如图 2-3 所示），从中您可以设置许多不同的选项。

### 配置 Apache 服务器

图 2-3：

您可以从此配置窗口配置虚拟主机的属性。

![](img/509edf67e1a0798154916aafeb3f0878_646_0.png)

- Server（服务器）：此标签页包含服务器用户和组名称的设置，HTTP 服务器将以这些名称身份运行，以及存储进程 ID 文件的位置。
- Performance Tuning（性能调优）：在此标签页上，您可以设置允许的最大连接数、连接超时时间和每个连接的最大请求数。

最初，配置窗口显示来自配置文件 `/etc/httpd/conf/httpd.conf` 的默认值。在进行任何更改后，点击 OK 按钮。配置工具会提示您是否想要保存更改并退出。如果是，点击 Yes，您应该这样做。

![](img/509edf67e1a0798154916aafeb3f0878_646_1.png)

当您从此服务器配置 Apache HTTP 服务器并更改存储在 `/etc/httpd/conf/httpd.conf` 文件中的选项和属性时，只需编辑该配置文件（纯文本文件）即可轻松地进行更改。在接下来的章节中，我将向您介绍 Apache 配置文件中常用的配置指令。

# Apache配置文件

Apache 服务器的运行由位于 `/etc/httpd/conf` 目录下的 `httpd.conf` 文件控制。该文件控制服务器如何运行、提供哪些文档，以及谁可以访问这些文档。通常情况下，运行 Apache Web 服务器不需要在配置文件中更改任何内容。然而，了解配置文件的格式以及其中使用的各种关键字的含义是有用的。

在您学习 `/etc/httpd/conf` 中的配置文件时，请记住这些语法规则：

- 每个配置文件都是一个文本文件，您可以使用最喜欢的文本编辑器进行编辑，并使用 `more` 命令查看。
- 所有注释行都以 `#` 开头。
- 每行只能有一个指令。
- 额外的空格和空行会被忽略。
- 除了路径名和 URL 外，所有条目均不区分大小。

## httpd.conf 配置文件

`/etc/httpd/conf/httpd.conf` 文件是主配置文件 — 它包含了控制 Apache 服务器如何运行的指令。例如，`httpd.conf` 指定了服务器使用的端口号、服务器名称以及当服务器出现任何问题时发送邮件的电子邮件地址。此外，`httpd.conf` 还包含了关于页面位置的信息。在接下来的章节中，我将 Apache 指令分为三个单独的类别进行介绍：通用 HTTP 指令、资源配置指令和访问控制指令。最后，我将解释如何在 Apache 服务器中设置虚拟主机，以便单台服务器能够处理指向多个 IP 地址或主机名的请求。

## 通用 HTTP 指令

`httpd.conf` 文件中的一些有趣项目是：

- `ServerName` 指定您的站点主机名（格式为 `www.your.domain`）和服务器接受的端口号。`ServerName` 仅在将网页重定向到另一个网页时使用。这里有一个示例：

```
ServerName www.myhost.com:80
```

如果您没有注册域名，请使用您的 Red Hat 系统的 IP 地址。

- `ServerAdmin` 是 Web 服务器在发生错误时提供给客户端的电子邮件地址。默认值为 `root@localhost`。您应该将其设置为互联网上任何人都可以用来报告错误的有效电子邮件地址。

许多指令控制着 Apache 服务器的工作方式。以下列表总结了您可以在 `httpd.conf` 文件中使用的某些指令。您可以在默认设置中学习大多数大多数指令，但如果您正在维护 Web 服务器，了解它们是非常重要的。

- `IP-Address:Port` — 强制服务器监听特定的 IP 地址和端口号。默认情况下，服务器响应所有关联的 IP 地址。
- `User name [#]` — 指定 HTTP 守护进程使用的用户名或 ID。您可以保持此指令默认设置（`apache`）。如果您指定了用户 ID，请使用井号 (`#`) 前缀。
- `Group name [#]` — 指定以独立模式运行的 HTTP 的组名或 ID。默认组名是 `apache`。
- `ServerRoot pathname` — 指定 Web 服务器所在的目录。默认情况下，配置和日志文件位于此目录的子目录下。在 Red Hat Linux 中，`ServerRoot` 设置为 `/etc/httpd`。
- `ServerName www.company.com:80` — 设置服务器主机名为 `www.company.com`，端口为 80。`ServerName` 仅在将网页重定向到另一个网页时使用。
- `StartWorkers num` — 设置 Apache 服务器启动后立即启动的进程数。默认值为 8。
- `MaxSpareServers num` — 设置最大空闲进程数（未处理 HTTP 请求的空闲进程）。默认值为 20。
- `MinSpareWorkers num` — 设置最小空闲进程数（未处理 HTTP 请求的空闲进程）。当低于此阈值时，每秒创建一个新进程。默认值为 5。
- `Timeout numsec` — 设置客户端建立连接后等待等待查询的秒数。默认超时时间为 300（五分钟）。

`ErrorLog filename` — 设置 http 记录其遇到的错误的文件。如果文件名不以斜杠 (`/`) 开头，则名称相对于 `ServerRoot`。默认 `ErrorLog` 为 `/etc/httpd/error_log`，但 `/etc/httpd/logs` 是指向 `/var/log/httpd` 目录的符号链接。日志文件位于 `/var/log/httpd` 目录。典型的错误日志条目包括服务器重启和任何警告消息，如下：

```
[Jun 13 10:34:2003] [notice] Apache/2.0.45 (Red Hat Linux)
configured --- removing normal operations
[Jun 13 15:47:03 2003] [error] [client 192.168.0.2] File does not exist: /var/www/html/sample.html
```

### 622 配置 Apache Web 服务器

- `TransferLog 文件名` — 设置记录所有客户端访问 HTTP 请求（包括失败的访问）的文件。默认的 `TransferLog` 为 `/var/log/http/access_log`。以下示例显示了典型的访问是如何记录在该日志文件中的：

```
192.168.0.2 - - [Jul/2003:14:46:56 -0400] "GET / HTTP/1.1" 200 2898
"Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1"
192.168.0.2 - - [Jul/2003:14:46:56 -0400] "GET /icons/apache_pb.gif HTTP/1.1" 200 2366
"http://192.168.0.6/"Mozilla/4.0 (compatible; Windows NT 5.1"
```

- `Logformat 格式` — 指定 `TransferLog` 日志条目的格式。该格式也用于 `CustomLog` 指令以生成特定格式的日志。
- `CustomLog 格式` — 设置自定义日志文件的名称，该文件以 `formatname`（你使用 `LogFormat` 指令定义的）指定的格式记录所有客户端的 HTTP 记录（包括失败的访问）。
- `Pidfile 文件名` — 设置 HTTPD 存储其进程 ID（PID）的文件。默认的 `Pidfile` 为 `/var/run/httpd.pid`。你可以使用此信息杀死或重启 HTTP 守护进程。以下示例显示了如何重启 `httpd`：
