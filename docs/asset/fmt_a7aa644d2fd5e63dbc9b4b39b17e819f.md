
# 第12章 — 成为 Web 托管服务

## 虚拟主机配置示例

- `ScriptAlias /cgi-bin/ /var/www/cgi-bin/` — 设置 CGI 脚本的默认位置。我们在示例中覆盖了此项，允许我们的每个托管客户添加自己的 CGI 脚本。（使用 `ScriptAlias` 而非仅用 `Alias` 是告诉服务器目录中的文件将作为脚本运行而不是显示。）

- `Indexes VersionSort NameWidth=` — 设置目录索引的显示方式。`FancyIndexing` 显示目录内容，并带有每种类型的链接允许你按名称、最后修改、大小和描述进行排序。`VersionSort` 使软件包包按逻辑顺序排序。`NameWidth` 设置显示的文件名长度（默认为 `*` 或不限制）。

- `AddType MIME_extension` — 当你添加不同类型的内容（音频、视频等）时，你可以通过 MIME 类型和文件扩展名来识别内容的类型。例如，`AddType application/x-tar` 告诉你的服务器告知客户端以 `.tgz` 结尾的文件其 MIME 类型为 `application/x-tar`。通过这些信息，Web 浏览器可以决定对内容进行正确的操作（例如显示、启动外部查看器或下载）。你可以检查 `/etc/mime` 来查看你的内容是否已经定义。如果没有，你可以使用 `AddType` 来添加或更改 MIME 文件扩展名以正确识别内容。

- `README.html` — 设置 Apache 在显示目录时查找的 readme 文件名（`README.html`）。

![](img/93c80330322e65d5105a6014afe2d85d_249_0.png)

许多选项可以添加到虚拟主机容器内部。在设置每个虚拟主机时，你拥有非常大的灵活性。尽管它们在同一台机器上，虚拟主机在数据数据、显示文件和记录方面的行为可能有所不同。

除了描述的指令外，还有许多机会来优化和增强你的 Web 服务器。这里是一些你可能想要查看的功能示例：

- `Timeout` — 有一些你可能想要查看的功能示例：
- `Modules` — 有一些你可能想要查看的功能示例：
- `Languages` — 有一些你可能想要查看的功能示例：

## 步骤 6：设置磁盘配额

为了限制每个用户消耗磁盘空间量，你使用名为磁盘配额（disk quotas）的功能。在开始之前，你必须已经创建了一个单独的分区。如果你不在乎用户消耗多少空间，可以跳过此步。

### 日志配置

- `ErrorLog logs` — 将错误写入到 `/var/log/httpd/error_log` 文件。我们为每个虚拟 Web 服务器覆盖了此项并创建了独立的错误日志文件。

- `CustomLog access log combined` — 将活动写入到 `/var/log/httpd/access_log` 文件。同样，我们为每个虚拟 Web 服务器覆盖了此项并创建了独立的访问日志文件。

- `ServerSignature On` — 当 `ServerSignature` 设置为 `On`（默认值）时，当服务器生成页面（例如发生错误情况时），服务器信息将写入页面中。信息包括 Apache 服务器的版本、主机地址和端口号。

### 实施磁盘配额

5. 创建一个用于配额检查的启动脚本。作为 root 用户，创建一个名为 `/etc/init.d/quota` 的新文件。以下是该脚本可能内容的示例：

```bash
#!/bin/bash
# init file for quota
#
# description: Checks disk quotas
#
# processname: quota
# chkconfig: 90 90
# source function library
# /etc/rc.init.d/functions

case "$1" in
start)
echo -n "Checking quotas: "
daemon /sbin/quotacheck -avug
echo
echo -n "Starting quotas: "
daemon /sbin/quotan -avug
echo
    ;
stop)
echo -n "Shutting down quotas: "
daemon /sbin/quotaoff -a
echo
    ;
restart)
$0 stop
$0 start
    ;
*)
echo -n "Usage: quota (start|stop|restart)"
exit 1
esac
```

6. 使配额脚本具有可执行权限，将其设置为启动机时开启，并立即开启：

- `# chmod 755 /etc/init.d/quota`
- `# chkconfig quota on`
- `# service quota start`

7. 要检查使用配额的分区（例如 `/home`）中每个用户占用了多少磁盘空间，请输入以下：

- `# quota -a`

**设备 `/dev/hda1` 上的用户配额报告**

块宽限时间: 7天；Inode 宽限时间: 7天

| User | soft | hard | grace | soft | hard | grace |
|---|---|---|---|---|---|---|
| root | 364908 | 0 | 0 | 5239 | 0 | 0 |
| chock | * | 558716 | 302007 | 512000 | 38 | 0 |

现在，你的计算机上的 `/home` 目录应该已经启用了磁盘配额。

## 第7 步：创建防火墙

使用第 7 章中的描述来配置你的防火墙。端口 `80` 是允许访问 Web 服务器内容的关键端口。当 Web 浏览器仅提供 Web 内容 URL 时，这就是默认尝试访问的位置。

除了 `80` 端口外，你可能考虑开放端口 `20` 和 `21` (`FTP`)、`53` (`DNS`)、`22` (使用 `ssh` 进行远程登录)、`25` (邮件检索) 以及端口 `110` (使用 `post3` 进行邮件检索)。

到此时，你应该已经拥有了一个可以运行的 Web 服务器。接下来，你可以参考“监控你的服务器”部分有关维护服务器和保持其安全的信息。然后，参考“添加 Web 服务器内容”部分，了解你的 Web 托管客户如何将内容放置到你的 Web 服务器上。

## 监控你的服务器

保护和监控服务器的技巧大部分与第 11 章中为 Mini ISP 项目描述的相似。专门对于 Web 托管，你希望能够：

- 监控网站的任何滥用模式。
- 生成统计数据以查看每个虚拟网站收到的活动量。

### 查看日志文件

我们的第一个建议是查看基础日志文件。如果你喜欢进行图形化操作，Red Hat Linux 有一个检查系统日志文件的 GUI 工具，称为“系统日志”（System Logs）窗口。你可以从桌面打开系统日志窗口，点击 系统工具 -> 系统日志（或输入 `redhat-logvi`）。图 12-2 显示了该窗口的示例。

系统日志中你感兴趣的是启动日志（Boot Log，查看服务是否正常启动）、邮件日志（Mail Log，查看邮件活动）和安全日志（Security Log，查看谁试图登录你的系统）。你应该偶尔检查这些文件，以确保服务器没有异常业务。

访问日志（Access Log）和 Apache 错误日志（Apache Error Log）对于单域名 Web 机最有用。你可能记得你为 Web 服务器上的每个虚拟主机创建了单独的访问和错误日志。你可以用传统方法检查：在文本编辑器中打开它们。

如果你安装了 `logwatch` 软件包，有一种更简单的方法来扫描潜在危险的日志消息。每天一次（默认是凌晨 4:00），`logwatch` 会扫描你的日志文件并向 root 用户发送电子邮件。邮件内容详细说明了任何潜在的危险情况（登录失败尝试、端口扫描等）。

![](img/93c80330322e65d5105a6014afe2d85d_253_0.png)

图 12-2：要监控发送到你喜欢的任何帐户的邮件，请将 `/etc/log.d/conf/logwatch.conf` 文件中的以下行从 `root` 更改为你想使用的电子邮件地址：

`MailTo = root`

### 查看网站活动

有很多可用工具可以监控网站活动并为你的客户制作彩色图表。一种用于绘制数据传输量和服务器访问次数等内容的工具被称为 `Webalizer`。你可以通过以下步骤在 Red Hat Linux 中使用 `Webalizer`：

1. 在终端窗口中作为 root 用户，输入以下：

`# webalizer`

2. 打开 Mozilla 或浏览器并输入：

```
http://localhost/usage/index.html
```

3. 编辑 `/etc/webalizer.conf` 文件以查看输出。

## 添加 Web 服务器内容
