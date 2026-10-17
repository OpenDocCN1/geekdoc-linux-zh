
`UserDir` `public_html`

# 快速上手：从用户目录提供 HTTP 内容

首先启用/配置 `UserDir` 选项。现在，假设用户 `yang` 想要通过 Web 服务器从其家目录提供某些 Web 内容，按照以下步骤操作即可实现该目标：

1. 以用户 `yang` 的身份登录系统时，创建 `public_html` 文件夹：

```
yang@server:~$ mkdir ~/public_html
```

2. 为父目录设置正确的权限：

```
yang@server:~$ chmod 711 ~
```

3. 为 `public_html` 文件夹设置正确的权限：

```
yang@server:~$ chmod 755 ~/public_html
```

4. 在 `public_html` 目录下创建一个名为 **index.html** 的示例页面：

```
yang@server~$ echo "<h1>Yang的首页</h1>" > ~/public_html/index.html
```

此后，你可以通过浏览器访问 `http://localhost/~yang/`。

注意，在启用了 SELinux 子系统的旧版 Red 系发行版中，你可能需要进行更多操作才能让 `UserDir` 指令工作。这是因为用户家目录下文件的默认安全上下文是 `user_home_t`。为了让该功能正常工作，你必须将 `~/public_html/` 下所有文件的上下文更改为 `httpd_content_t`，以便 Apache 读取这些文件。执行命令如下：

```
[yang@fedora-server ~] $ chcon -Rt httpd_content_t ~/public_html/
```

## ErrorLog (错误日志)

定义 Web 服务器错误日志的位置。

语法：`ErrorLog file_path| syslog[: facility]`

示例：`ErrorLog/var/log/httpd/error_log`

## LogLevel (日志级别)

此选项设置发送到错误日志的消息详细程度。允许的日志级别有 `emerg`、`alert`、`crit`、`error`、`warn`、`notice`、`info` 和 `debug`。默认日志级别为 `warn`。

语法：`LogLevel level`

## Alias (别名)

`Alias` 指令允许将文档（Web 内容）存储在文件系统中 `DocumentRoot` 指令指定的任何其他位置。它还允许为可能很长的路径名创建缩写（别名）。

语法：`Alias URL_path actual_file_or_directory_path`

## ScriptAlias (脚本别名)

`ScriptAlias` 选项指定一个目标目录或文件包含要处理的 CGI 脚本。

语法：`ScriptAlias URL_path actual_file_or_directory_path`

## VirtualHost (虚拟主机)

Apache 最常用的功能之一是它支持多个虚拟主机。这使得单个 Web 服务器可以托管不同的站点。它通过使用两个标签来实现：起始 `<VirtualHost>` 标签和结束 `</VirtualHost>` 标签。

`<VirtualHost>` 标签指定了配置生效的主机和端口。在块内部，你可以定义特定于该虚拟机的指令。

```apache
<VirtualHost *:80
    ServerName example.com
    DocumentRoot /var/www/html
    ErrorLog logs/error_log
</VirtualHost>
```

如果你需要查看比这更多的日志信息，只需将数字 10 更改为你需要查看的行数。如果你想在错误或日志生成时实时查看它们，可以持续地使用 `tail` 命令的 `-f` 选项。这提供了一个非常有用的调试工具，因为你可以尝试对服务器进行操作（例如请求网页或重启 Apache），并在另一个虚拟终端中查看实验结果。这里显示了带有 `-f` 关的 `tail` 命令：

```
master@fedora-server html1]$ sudo tail -f /var/log/httpd/error_log
```

此命令将持续跟踪日志，直到你终止程序。在运行 `systemd-journal` 服务的 Fedora/CentOS/RHEL 系统上，你也可以使用 `journalctl` 工具通过运行以下命令查看来自 `httpd.service` 单元最新消息：

```
master@fedora-server -]$ journalctl -u httpd.service
```

> 提示 如果启用了 SELinux，在类 Red Hat 发行版上排查 Web 服务器故障时请注意它没帮助的干扰。你可能会发现 httpd 运行不符合预期，甚至令人担忧的是，没有相应的日志帮助你排查故障！在这种情况下，你可能需要临时禁用 SELinux。

在运行 `systemd-journal` 服务的类 Debian 发行版上，你可以使用 `journalctl` 工具查看来自 `apache2.service` 单元的最新消息，如下：

```
master@ubuntu-server -]$ journalctl -u apache2.service
```

## 总结

本章介绍了如何从零开始 Apache（又名 `httpd`）搭建你自己的 Web 服务器。单本章的内容就足够让你运行一个顶级页面和基础配置了。至少，这里涵盖的内容将帮助你把 Web 服务器接入到互联网，或者实习生——取决于你更倾向于哪一个！

强烈建议你花时间翻阅相关的官方 Apache 手册/文档（`http://httpd.apache.org/docs/`）。它编写得很好、简洁且足够灵活，可以让你设置几乎任何想象到的任何配置。

# 第 20 章：简单邮件传输协议 (SMTP)

简单邮件传输协议 (`SMTP`) 是互联网上传输邮件的事实标准。任何想要能够发送和接收邮件的邮件服务器都必须能够支持 `SMTP`。作为一种基于标准的协议（参见 `RFC 5321`），`SMTP` 广为人知、与平台无关，并且在各种操作系统和设备上得到了良好支持。

在本章中，我们将讨论 `SMTP` 作为协议的机制以及它与其他邮件相关协议的关系，例如邮局协议 (`POP`) 和互联网消息访问协议 (`IMAP`)。然后，我们将介绍 `Postfix` `SMTP` 服务器，它是目前市场上较简单且更安全的服务器之一。

## 理解 SMTP

`SMTP` 定义了邮件从一个主机发送到另一个主机的方法。仅此而已。它没有定义邮件应该如何存储。它没有定义邮件如何递送给接收者。

`SMTP` 的优势在于它的简单性，这在部分归功于 20 世纪 80 年代网络的动态特性（大约是该协议发明的时期）。在那时，人们用各种泡泡糖糖和胶水将网络连接在一起。`SMTP` 是第一个独立于传输机制的邮件标准。这意味着使用 `TCP/IP` 网络的人可以使用相同的格式向使用两个罐子和一根线的人发送消息——至少在理论上是这样。

`SMTP` 也独立于操作系统，因此每个系统可以使用自己的风格来存储邮件，而不必担心消息发送者如何存储她的邮件。你可以将其比作电话系统的工作方式：每个电话服务供应商都有自己独立的计费系统。然而，它们都约定了一种标准方式来连接它们的网络，以便通话可以透明地从一个网络到另一个网络。

在自由开源软件 (`FOSS`) 世界中，几个软件包（如 `Exim`、`Postfix`、`Sendmail` 和 `opensmtpd`）提供了它们自己的 `SMTP` 实现。

## 基础 SMTP 细节

你是否曾遇到过一个“朋友”代表某个政府机构向你发送一封邮件，通知你欠了去年的税，外加额外的罚金？我们将向你展示是如何做到的，而且更有趣的是，你可以如何自己做到这一点。（当然，我们并不提倡这种行为。）

此处的目的是为了展示 `SMTP` 如何将消息从一个主机发送到另一个主机。毕竟，学习如何伪造邮件并没有学习如何排查与邮件相关的问题重要。因此，在这个示例中，你充当发送主机，而你连接的任何一个都是接收主机。

`SMTP` 要求主机能够向另一个主机发送纯 ASCII 文本。通常，这是通过连接邮件服务器上的 `SMTP` 端口（25 端口）完成的你可以使用 `Telnet` 程序执行此操作。这里有一个示例：

```
master@server ~$ telnet mailserver 25
```

在这里，主机 `mailserver` 是接收者的邮件服务器。`mailserver` 后的 25 告诉 `Telnet` 你想与服务器的 25 端口（标准 `SMTP` 端口）通信，而不是标准的 `Telnet` 端口 23。

邮件服务器将返回如下问候消息：

`220 mail SMTP Postfix`

你现在正在与 `SMTP` 服务器直接通信。

虽然有很多 `SMTP` 命令，但有四个值得注意：

- `HELO`
- `MAIL FROM:`
- `RCPT TO`
- `DATA`

`HELO` 命令用于客户端向服务器介绍自己。该参数是发起连接的主机名。当然，大多数邮件服务器都会接受这个信息。这里有一个示例：

```
HELO example.org
```
