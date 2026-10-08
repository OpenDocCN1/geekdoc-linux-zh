
`nokeepail ssl-un-shutdown \\`

`downgrade-1.0 force-response-1.0`

```
```

`CustomLog logs /ssl_request_log \`

`"%t %h %{SSL_PROTOCOL} %x{SSL_CIPHER} \"%r\" %b"`

```
```

`</VirtualHost>`

```
```

这里最重要的元素是 `Listen` 选项以及在 `<VirtualHost _default_:443> </VirtualHost>` 标签内定义的选项。默认情况下，安全站点作为默认站点托管（这很不错，因为它允许你与其他不安全的站点一起运行）。我们将在本章后面的部分介绍虚拟主机。

你还应该注意以下选项：

```
SSLCertificateFile /etc/pki/tls/certs/localhost.crt

SSLCertificateKeyFile /etc/pki/tls/private/localhost.key
```

它们定义了证书文件和密钥的选项及位置，这些在托管安全网站时会被使用。虽然默认设置可以使用，但如果你更改了 IP 地址或域名，将需要生成新的证书和密钥。安装 `crypto-utils` 包可以提供完成此操作所需的 `openssl` 和 `genkey` 命令。然而，由于此主题是考试的一部分，我在这里不会列出完整步骤。

你的安全网站需要采取的额外步骤是在防火墙上开启额外的端口。

步骤 1. 使用 `iptables` 命令创建防火墙规则：

```
# iptables -I INPUT 5 -p tcp -m tcp --dport 443 -j ACCEPT
```

步骤 2. 保存规则：

```
# service iptables save
```

步骤 3. 重启防火墙使更改生效：

```
# service iptables restart
```

# CGI

现在你已经知道了如何配置和保护 Web 服务器，让我们来看一些部署。

步骤 1. 创建一个目录用于：

```
# mkdir /var/www/webapp-01
```

步骤 2. 将文件复制到新创建的目录：

```
# cp /home/user01/app.py /var/www/webapp-01
```

步骤 3. 在你的 `/etc/httpd/conf.conf` 文件中添加以下部分：

```
ScriptAlias /webapp-01 "/var/www/webapp-01/"

<Directory "/var/www/webapp-01/">

  Options ExecCGI FollowLinks

  Order allow,deny

  Allow from all

</Directory>
```

步骤 4. 检查配置错误：

```
# service httpd configtest

Syntax OK
```

步骤 5. 为目录设置正确的权限：

```
# chmod 755 -R /var/www/webapp-01
```

步骤 6. 重启 Web 服务：

```
# service httpd restart
```

现在，如果你访问 `http://172.168.1.1/webapp-01/app.py`，你应该在浏览器中看到 CGI 应用程序的运行！如果你以前用过 Apache，你就知道默认已经设置了一个 CGI 应用程序目录。安装 Apache 时，会创建 `/var/www/cgi-bin` 目录。你会在主配置中看到以下部分：

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin/
# /var/www/cgi-bin 应该根据你配置的 ScriptAlias 目录项进行更改

<Directory "/var/www/cgi-bin">
  AllowOverride None
  Options None
  Order allow,deny
  Allow from all
</Directory>
```

# 虚拟主机

Apache 的一大优点是，你可以在单个主机上运行多个网站。这是通过虚拟主机配置实现的，你可以在主 Apache 配置文件中定义不同的站点。我们已经讨论了主配置文件中的全局选项和服务器选项。第三部分涉及虚拟主机选项：

| 选项 | 描述 |
| :--- | :--- |
| NameVirtualHost | 指定虚拟主机的主机名或 IP 地址 |
| ServerAdmin | 指明管理员的电子邮件地址 |
| DocumentRoot | 定义虚拟主机文件的目录 |
| ServerName | 定义虚拟主机的 URL |

## 第 14 章：Web 服务 34

`ErrorLog` 指定错误日志的位置

`CustomLog` 指定自定义日志的位置

这些选项许多与配置文件中主服务器部分提供的选项相似。如果虚拟主机部分中没有定义某个选项，它将默认使用主服务器部分中设置的值。

设置虚拟主机非常简单，只需执行以下操作：

- 步骤 1. 复制主服务器部分的默认站点作为示例：

```
<VirtualHost *:80>
ServerAdmin webmaster@example.com
DocumentRoot /var/www/site1
ServerName site.com
ErrorLog logs/site1_error_log
CustomLog logs/site1_access_log
</VirtualHost>
```

- 步骤 2. 在运行配置之前不要忘记验证语法：

```
# httpd -S
VirtualHost configuration:
wildcard NameVirtualHosts and _default_servers:
*:80 www.site1.com
(/etc/httpd/conf/httpd.conf:985)
Syntax OK
```

- 步骤 3. 如果你有有多个虚拟主机站点，可以使用以下命令进行检查：

```
# httpd -D DUMP_VHOSTS
VirtualHost configuration:
wildcard NameVirtualHosts and _default_servers:
*:80 www.site1.com
(/etc/httpd/conf/httpd.conf:985)
Syntax OK
```

# Squid Web 代理

代理服务器通常位于客户端和用户尝试访问的目标地之间的设备设备。它可以为代理背后的客户端提供安全性、匿名性，甚至是保护。Squid 有助于这一过程，它是 Red Hat 的一个代理服务器。它位于用户正尝试连接的客户端和服务器之间。很多时候，当你想要控制对 Internet 的访问时（例如 Web 过滤），就会使用这些设备。作为代理，它还可以缓存用户从 Web 请求的数据并使其本地可用，从而减少网关和防火墙等外部设备的负载。在这里，我们将介绍如何设置 Web 代理、定义访问控制列表并对其进行故障排除。

## 安装 Squid

就像你处理 Web 服务器一样，你需要首先开始安装 Squid 所需的包。安装 Squid 代理服务器只需要一个包。

- 步骤 1. 使用以下命令安装包：

```
# yum -y squid
```

- 步骤 2. 安装后，进行验证：

```
# rpm -qa | grep squid
squid-3.1.4-1.el16.x86_64
```

接下来，开启 Squid 开机启动。使用 `chkconfig` 命令来实现此。

- 步骤 3. 启用 Squid 开机启动：

```
# chkconfig squid on
```

- 步骤 4. 验证服务将在开机启动：

```
# chkconfig squid -list
squid       0:off 1:off 2:on 3:on 4:on 5:on
6:off
```

现在你已经包已安装并在开机启动，可以将注意力转向配置了。

## 配置代理

在设置代理服务器时，你需要了解以下项目：

- `/etc/sysconfig/squid` 配置文件的启动选项
- `/etc/squid/squid.conf` 该服务的主配置文件
- `/var/pool/squid` 代理服务器上的缓存位置
- `/var/log/squid` 代理服务器的日志文件

正如大多数服务一样，议程中的首要任务是主配置文件。我想先警告一下，此配置文件包含大量的文档和许多示例，它包含 4000 多行，所以如果你计划阅读并处理整个配置文件，请务必留出时间！作为 Apache 用户，配置 Web 服务器可能是一个艰巨且有时漫的过程，直到你正确设置好它。然而，本实验只需要代理服务器的基本功能，因此使其运行起来不应该太困难。让我们来看一些主要的配置选项：

- `http_port` 指定监听的端口
- `visible_hostname` 标识 Squid 服务器的名称
- `hierarchy_stoplist` 提供一个单词列表，告诉 Squid 服务器处理请求
- `access_log` 跟踪下载的 页面
- `acl` 定义访问控制列表
- `http_access` 定义哪些系统或网络具有访问权限

你可以使用默认端口运行 Squid，这将使测试变得更容易。但是，你可以将 `visible_hostname` 选项设置为你的服务器名称：

```
# nano /etc/squid/squid.conf
visible_hostname = RHEL01
```

# 考试提示

> 注意，许多代理喜欢使用 8080 端口。对于为什么 Squid 使用 3128 作为默认端口，我不知道，但请准备好如果考试要求 Squid 监听其他端口，你知道如何更改默认端口。如果你在生产环境中运行 Squid，也应该更改默认端口，因为出于安全考虑，让任何内容保持默认选项都不是好主意。

你还应该定义 Squid 服务器应该处理的 URL 语法。

## 防火墙和 SELinux 配置

正如你看到的，防火墙和 SELinux 的要求其实简单。

- 步骤 1. 使用防火墙创建：

```
# httpd -S
VirtualHost configuration:
wildcard NameVirtualHosts and _default_servers:
*:80 www.site1.com
(/etc/httpd/conf/httpd.conf:985)
Syntax OK
```

- 步骤 2. 在运行配置之前验证语法：

```
# httpd -S
VirtualHost configuration:
wildcard NameVirtualHosts and _default_servers:
*:80 www.site1.com
(/etc/httpd/conf/httpd.conf:985)
Syntax OK
```

- 步骤 3. 如果你有有多个虚拟主机站点，可以使用以下命令进行检查：

```
# httpd -D DUMP_VHOSTS
VirtualHost configuration:
wildcard NameVirtualHosts and _default_servers:
*:80 www.site1.com
(/etc/httpd/conf/httpd.conf:985)
Syntax OK
```

## Red Hat® 考试实践指南：RHCSA™ 和 RHCE® 指南与实验手册

## Web 安全

Squid 通过使用访问控制列表（ACL）使用基于主机的安全机制。这些 ACL 在主配置文件 `/etc/squid/squid.conf` 中配置。在配置文件中，你可以为网络定义 ACL 并允许所有其他网络访问。

## 总结

Web 服务非常重要，因为它们在互联网上起着至关重要的作用。高效学习设置和管理 Apache Web 服务器内部机制需要大量时间。对于考试，确保你熟悉配置和虚拟主机的知识。代理也有助于缓解如果没有它们 Web 服务器将承受的压力。这两项服务结合 DNS 一成了网站的 Web 基础设施。

## 复习题

- 1. Apache Web 服务器运行在什么端口？HTTPS 又是呢？
- 2. 除了 `httpd` 之外，安全网站还需要额外的包吗？如果是，它们是什么？
- Red Hat® 考试实战指南：RHCSA™ 和 RHCE® 认证指南与实验手册
- 3. 你可以使用什么命令创建受保护的页面？
- 4. 如果在运行第 3 题的命令后使用 `-c` 选项再次调用，会发生什么？
- 5. 你可以使用什么命令验证 Apache 配置文件的语法？
- 6. 什么是虚拟主机？
- 7. 虚拟主机如何被使用？
- 8. 如何更改目录的安全上下文以配合 Apache 工作？
- 9. Web 代理为你的网络提供什么好处？
- 10. Squid 运行的默认端口是什么？

## 复习题答案

- 1. Apache 使用 80 端口用于 HTTP，使用 443 端口用于 HTTPS。
- 2. 是的。为了让 Apache 安全网站，需要安装 `mod_ssl` 包。
- 3. 可以使用 `htpasswd` 命令对网页进行密码保护。
- 4. 存储用户名及其加密密码的文件将被删除并替换为新文件。
- 5. `service httpd config`
- 6. 虚拟主机是通过单个 IP 地址托管多个网站的方法。
- 7. 如果你是托管公司或想从单个 IP 地址运行多个网站/应用程序，可以使用虚拟主机来实现此目标。
- 8. 使用 `chown` 命令，你可以更改文件的上下文以配合 Apache 工作。
- 9. Web 代理可以提供多种好处，包括安全性、用于加快加载时间的网页缓存以及负载均衡。
- 10. 默认情况下，Squid 运行在 3128 端口。

# 实验 14

## 任务 1 – Web 服务器设置

- 步骤 1。按照以下指南设置 Apache Web 服务器：

Web 服务器应仅通过 80 端口访问。

默认网站应位于 `/var/www/first_site` 目录下。

该网站应仅从本地网络 `172.168.1.0/24` 访问。

**步骤 2.** 在 `first_site` 目录中创建一个 `index.html` 文件。使用以下文本作为文件内容：

```html
<body>
<h2>This is my first web site!</h2>
</body>
</html>
```

当本地网络上的任何客户端都能访问 `first_site` 网站时，任务完成。

## 任务 2 – 安全网站

**步骤 1.** 按照以下指南设置另一个网站：

该网站应仅通过 443 端口 `HTTPS` 访问。

安全网站应位于 `/var/www/secure_site` 目录下。

该网站应仅从本地网络 `172.168.1.0/24` 访问。

**步骤 2.** 在 `first_site` 目录中创建一个 `index.html` 文件。使用以下文本作为文件内容：

```html
<body>
<h2>This is the secure version of my site!</h2>
</body>
</html>
```

当本地网络上的任何客户端都能访问 `secure_site` 网站时，任务完成。

## 任务 3 – Web 代理

**步骤 1.** 按照以下指南使用 Squid 设置 Web 代理：

- 代理应能够处理 `172.168.1.0/24` 子网的所有 Web 流量。
- 配置 Client02 使用代理其 Web 流量。
- 代理应监听 3128 端口。

当 Client02 能够通过代理访问互联网时，任务完成。

本章涵盖了以下主题：

- 网络文件系统——本部分涵盖了文件系统以及客户端如何使用它们。
- NFS 安全——本部分涵盖了 NFS。
- NFS 故障排除——本部分研究了 NFS。
- 连接客户端——本部分研究了如何连接到 NFS 服务器。

涵盖了以下 RHCE 目标：

- 安装提供服务所需的包
- 配置 SELinux 以支持该服务
- 配置服务在系统启动时启动
- 配置服务进行基本操作
- 为服务配置基于主机的和基于用户的安全性
- 为特定客户端提供网络共享
- 提供适用于组的共享

# NFS

你有许多不同的方法可以与网络上的用户共享文件。本章是第一个处理通过网络共享文件的章节。具体而言，我们将在下一章中查看 Samba，在第 17 章查看 FTP。NFS 提供了一种方法，让网络上的其他系统可以在集中位置存储文件。这确保了备份更加简单，并且安全性在单点保持完整（而不是分散在多个服务器上）。作为系统管理员，将数据保留在中心位置将会让你的工作变得轻松得多。

# 网络文件系统

网络文件系统 `NFS` 协议在 Linux 系统上运行良好，因为它允许对文件的集中管理以及一些其他很棒的功能。要让 NFS 正常工作，你首先需要设置 NFS 服务器，然后设置客户端访问服务器。像任何其他服务一样，在执行任何操作之前，你需要安装几个包。服务器和客户端的实际服务是相同的，区别在于运行的配置文件。NFS 有四种不同的版本；版本 4 是是最新的。虽然你可以禁用服务器监听的版本，但客户端实际上在连接到服务器时决定它将使用哪个版本（除非，服务器提供的版本正是客户端请求的版本）。随着学习的深入，这个描述将变得更有意义。

当 RHEL5 引入时，它带有 NFS 的两个版本，默认使用的是版本 3。在 RHEL6 中，版本 3 和 4 都可用，默认是 4。由于许多改进，如果你仍在使用 RHEL5，建议使用版本4。

# 安装 NFS 服务器

按照以下步骤安装 NFS 服务器。

- 步骤 1. 在设置 NFS 服务器之前，安装所需的包：

```
# yum install -y nfs-utils nfs-acl-tools
```

- 步骤 2. 验证包安装情况：
