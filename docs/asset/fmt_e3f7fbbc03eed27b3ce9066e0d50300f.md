
有时，你可能会看到诸如“`Internal Server Error`”的错误消息。最可能的原因是 Perl 脚本没有为名为 `apache` 的用户提供可执行权限。重申一下，这通常通过为该 Perl 脚本赋予 `755` 权限来解决。

## 场景与解决方案

| 场景 | 解决方案 |
|---|---|
| 你需要配置一个网站 | 安装 Apache，在 `/var/www/html` 目录中配置适当的文件。 |
| 你需要配置多个网站 | 使用 Apache，将 `httpd.conf` 文件末尾的 `<VirtualHost>` 容器作为模板，为所需的任意多个网站使用。 |
| 你需要配置一个安全网站 | 在 `/etc/httpd/conf.d` 目录的 `ssl.conf` 文件中配置虚拟主机。 |
| 你需要为 `www.example.org` 网站提供专用 SSL 证书 | 从 `/etc/pki/tls/certs` 目录运行 `genkey www.example.org` 命令。 |
| 重启后 Apache 服务未运行 | 使用 `chkconfig --list httpd` 命令确保 `httpd` 服务在适当的运行级别启动。如果没问题，请检查 `/var/log/httpd` 目录中 `error_log` 的内容。 |
| Apache 中的 CGI 脚本未运行 | 在 Apache 配置文件中，确保 `ExecCGI` 选项处于活动状态；`AddHandler` 指令指定 `cgi-script .pl`，`ScriptAlias` 指向适当的目录；脚本对所有用户可执行并且与 `/var/www/cgi-bin` 目录中的 SELinux 上下文匹配。 |

## 认证总结

Apache 是目前使用最广泛的 Web 服务器。关键软件包可以从“Web Server”软件包组安装。`httpd-manual` 包包含一个可本地浏览的手册，可帮助完成其他 Apache 配置任务，即使在考试期间也是如此。关键配置文件包括 `/etc/httpd/conf` 目录中的 `httpd.conf` 和 `/etc/httpd/conf.d` 目录中的 `ssl.conf`。`httpd.conf` 和 `ssl.conf` 文件在 `<VirtualHost>` 容器中组织。借助这两个配置文件中的示例段落，你可以在一个系统上为多个网站创建虚拟常规主机和安全主机，即使只有一个 IP 地址可用。相关的日志文件存储在 `/var/log/httpd` 目录中。

你可以使用基于 `iptables` 命令的防火墙允许通过端口 `80` 和 `443` 访问 Apache，针对部分或全部系统。Apache 文件和目录与多个不同的 SELinux 上下文相关联。不同的 Apache 功能可能受多种不同的 SELinux 布尔设置监管。

`Listen` 和 `NameVirtualHost` 指令将流量定向到 Apache Web 服务器的端口 `80` 和 `443`，以及指定的虚拟主机。主机和用户基于的安全也可以在 Apache 配置文件中使用 `htpasswd` 等命令以及 `Allow` 和 `Deny` 等指令进行设置。

使用正确的 `security` 选项，用户和组管理的目录是可能的。事实上，有一个注释的段落可以启用用户主目录中的目录。组管理的目录稍微复杂一些，结合了第 8 章中讨论的基于 Apache 的用户目录和共享组目录的方面。也在安全方面，可以从 `/etc/pki/tls/certs` 目录使用 `genkey www.example.org` 之类的命令为特定主机（如 `www.example.org`）创建新证书。

在 Apache 网站上配置 CGI 内容比看起来更容易。事实上，Apache 文档中包含有关该过程的详细信息，包括一个 Perl 脚本，可用于确认生成的配置是否有效。

## 两分钟速览

这里列出了第 14 章认证目标中的一些关键点。

### Apache Web 服务器
- Red Hat Enterprise Linux 包含 Apache Web 服务器，目前它被使用的互联网网站数量超过所有其他 Web 服务器的总和的两倍。
- 您可以将 Apache 及相关软件包作为“Web Server”软件包组的一部分进行安装。
- Apache 配置文件包括 `/etc/httpd/conf` 目录中的 `httpd.conf` 和 `/etc/httpd/conf.d` 目录中的 `ssl.conf`。
- Apache 的日志信息位于 `/var/log/httpd` 目录中。

### 标准 Apache 安全配置
- Apache 可通过 `iptables` 规则以及各种 SELinux 布尔值和上下文进行保护。
- Apache 通过 `Listen` 和 `NameVirtualHost` 指令指定活动端口来支持安全性。
- Apache 支持基于 IP 地址或域名的主机安全。
- Apache 在 `htpasswd` 命令的帮助下支持基于密码的用户安全。

### 专用 Apache 目录
- Apache 使设置对用户主目录的访问变得容易，具体在它们的 `public_html/` 子目录中。
- 组管理的目录可以以与用户主目录类似的方式进行配置。

### 普通和安全虚拟主机
- [ ] 您可以在服务器上配置多个网站，即使只有一个 IP 地址。这可以通过使用虚拟主机实现。
- [ ] RHEL 配置支持在 `/etc/httpd/conf/httpd.conf` 文件末尾配置普通网站的虚拟主机。
- [ ] RHEL 配置支持在 `/etc/httpd/conf.d/ssl.conf` 文件末尾配置普通网站的安全虚拟主机。
- [ ] SSL 证书可以使用 `genkey` 命令创建，当在 `/etc/pki/tls/certs` 目录中运行时。

### 部署基本 CGI 应用程序
- [ ] CGI 内容的使用取决于 `ScriptAlias`、`ExecCGI` 和 `AddHandler cgi-script` 等配置选项。
- [ ] 标准 CGI 脚本需要 `755` 权限。如果需要，示例说明可在 `httpd-manual` 软件包提供的 Apache 手册中找到。

![](img/9139201cfcaf4292284a0eed074928e5_813_0.png)

![](img/9139201cfcaf4292284a0eed074928e5_814_0.png)

## 自测

以下问题将帮助衡量您对本章内容的理解程度。由于 Red Hat 考试中没有选择题，本书中也没有选择题。这些问题专门测试您对本章的理解。即使您有另一种执行任务的方法也可以。Red Hat 考试看重的是结果，而不是死记硬背琐碎知识。这些问题中的许多可能有不止一个答案。

### Apache Web 服务器
1. 指定配置和日志文件基本目录的 Apache 指令是什么？

2. 修改 `httpd.conf` 后，什么命令可以让 Apache 重新读取此文件，而不会断开当前连接的用户？

3. 指定与 Apache 关联的 TCP/IP 端口的指令是什么？

### 标准 Apache 安全配置
4. 什么命令创建 `/etc/httpd/passwords` 文件并为用户 `elizabeth` 配置密码？

5. 如果您在虚拟主机的段落中看到以下限制访问的指令，哪些计算机被允许访问？

6. 要允许访问普通网站和安全网站，需要在防火墙中打开哪些标准端口？

```
Order Allow,Deny

Allow from 192.168.0.0/24
```
