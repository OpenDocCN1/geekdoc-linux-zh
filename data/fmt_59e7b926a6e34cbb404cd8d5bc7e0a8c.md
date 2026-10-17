
## 测试服务器

下一步是测试服务器。你新 Apache 服务器的配置位于 `/usr/local/apache/conf` 目录。切换到该目录并编辑找到的 `httpd.conf` 文件。在文件中找到包含 `Port` 关键字的行，对于使用 Apache 1.3.20 的用户来说，那应该是第 314 行。将默认值改为 `8080`。

如果一切顺利，你将看到类似下面的内容：

```
apachectl: http started
```

接下来，我们将查看进程列表以检查 `httpd` 是否正在监听：

```
ps aux httpd | grep http
```

你将得到类似列表 D 的输出。

### 列表 D: `ps aux | grep http` 输出

| 2205 | S | 0:00 | `httpd-perl -f /etc/httpd/conf/httpd-perl.conf -DPERLP` |
| 2212 | S | 0:00 | `httpd-perl -f /etc/httpd/conf/httpd-perl.conf -DPERLP` |
| 2213 | S | 0:00 | `httpd-perl -f /etc/httpd/conf/httpd-perl.conf -DPERLP` |
| 2214 | S | 0:00 | `httpd-perl -f /etc/httpd/conf/httpd-perl.conf -DPERLP` |
| 2215 | S | 0:00 | `httpd-perl -f /etc/httpd/conf/httpd-perl.conf -DPERLP` |
| 2268 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 2276 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 2277 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 2278 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 2279 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 13812 | S | 0:00 | `httpd -DERLPROXED -DAVE_PHP4 -DAVE_SSL -DAVE_PRO` |
| 8068 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8069 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8070 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8071 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8072 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8073 | S | 0:00 | `/usr/local/apache/bin/httpd` |
| 8084 | pts/2 | S | 0:00 | `grep httpd` |

是的，它在这里。你可以看到，我们旧的 Apache 也在运行，但你可以看出输出中从 `PID` 为 `8068` 开始的进程属于我们新的 Apache 服务器。

下一步是将你的 Web 浏览器指向 `localhost:8080` 或 `www.yourdomain.com:8080`，取决于你是否与新服务器相关联。如果你看到了 Apache 页面，恭喜你！Apache 在你的系统上成功运行了！由于我们有点多疑，想额外确认一下，我们将执行：

```
telnet localhost 8080
```

你将看到：

```
Trying 127.0.0.1.

Connected to localhost.local.

Escape character is '^'
```

此时，输入以下内容并按 [Enter] 键：

```
HEAD /HTTP/1.0
```

你应该会看到与下面非常相似的内容：

```
Date: Fri, 22 Jun 2001 01:26:57 GMT

Server: Apache/1.3.20 (Unix)

PHP/4.0.6
```

其余部分我们可以忽略。如果你不对运行在 `80` 端口的 Web 服务器进行此测试，你可能会看到旧版本的 Apache 以及可能的旧版本的 PHP。嗯，这里。正如你所看到的，它报告运行着 Apache 1.3.20 和 PHP 4.0.6，这些都是我们刚刚安装的。

还有一个最后的测试，以确保 PHP 正常工作。进入你的 `/usr/local/apache/httpd` 目录，使用你喜欢的编辑器创建一个名为 `test.php` 的新文件，内容如下：

```php
<?php phpinfo(); ?>
```

现在将你的浏览器指向 `localhost:8080/test.php` 或你新 Apache 安装的类似 URL。你是否看到了一个关于 PHP 的信息页面，例如系统信息、正确的 PHP 版本以及配置指令的详情？如果是，PHP 工作正常。恭喜你！

## 结论

我们今天完成的工作只是让大家回归本质。我们都被喜喜软件的 RPM 和 DEB 软件包宠坏了；

```bash
--modules=mod_linuxprivs
```

指定 `ProFTPD` 是作为独立服务还是 `inetd` 服务运行。在我们的示例中，`ProFTPD` 作为一个独立服务器运行。如果你想从 `inetd` 运行 `ProFTPD`，请将其更改为 `inetd`，并将以下内容放入你的 `/etc/inetd.conf` 文件中：

```bash
mod_ratio:mod_readme
```

```
ftp stream tcp now rout

/usr/sbin/tcpd -inetproftpd
```

```bash
make

make install
```

第一条命令将设置 `make` 环境。你将告诉它使用 `/` 目录作为安装的顶层目录，它会将二进制文件存放在 `/usr/bin`，将手册存放在 `/usr/man` 等。你还告诉它处理 `/etc` 目录下的 `proftpd` 文件，并在 `/var/run/proftpd.daily` 提供位置状态文件（`PID`，或进程标识）。最后，你告诉它包含三个模块：

- `mod_linuxprivs` 为 `ProFTPD` 提供 Linux 权限支持。
- `mod_ratio` 提供上传/下载比例支持。
- `mod_readme` 提供显示状态信息的支持。

接下来，你制作二进制文件，然后使用 `make` 将所有内容安装到其正确位置。

## `/etc/proftpd.conf` 配置文件的详解

接下来，你想定义一些服务器默认值。这些值必须在 `<VirtualHost>` 或 `<Global>` 指令中定义，你应该将它们直接放在信息之后：

`ProFTPD` 的主配置位于 `/etc/proftpd.conf` 文件中。用你喜欢的文本编辑器打开 `proftpd` 文件，让我们来看几个可以创建一个启用多个安全选项的有效 FTP 服务器的指令：

```
# 基本默认设置
Port 21
TimeoutLogin 120
TimeoutIdle 600
TimeoutTransfer 900
TimeoutStalled 3600
MaxInstances 30
```

你首先想为服务器定义默认值。以下内容将定义 `ProFTPD` 需要的一些服务器信息。这些应该是你的 `proftpd.conf` 文件中的第一个条目。像配置文件一样，你使用行首的哈号 (`#`) 在文件中放置注释。

`Port` 关键字定义了服务器应该监听的默认端口（这对于 `inetd` 启动的服务器没有影响）。默认 FTP 端口是 `21`，因此将其设置为该值。

```
# 服务器信息
ServerName? MyServer
ServerType standalone
ServerAdmin mailto:myemail@mydomain.com
```

`TimeoutLogin` 关键字定义了服务器在连接建立后等待用户登录的超时时间。将值设置为 `120` 意味着你给用户两分钟登录，然后开始断开他们。

```
DefaultServer on
```

`ServerName` 关键字定义了服务器的默认名称。`HttpServer` 关键字

`Timeout` 关键字定义了在未接收数据或其他数据模式的情况下，`ProFTPD` 等待断开客户端的秒数。值 `0` 将禁用此，但如果 `TCP` 连接损坏，这通常是一个坏主意，服务器将永远不会终止断开的会话。

![](img/18a4efcf5db19984d10d986ab04de74b_112_0.png)

如果你需要切换到不同的 `UID`/`GID` 设置。在上面的示例中，我将 `UID` 和 `GID` 都设为了用户 `ftp`，这是一个非特权用户。你也可以使用用户 `nobody`（Apache 默认使用它）。

`TimeoutTransfer` 关键字用于定义客户端在登录 FTP 服务器后，在不启动文件上传或下载或不检索目录列表的情况下，可以空闲的最大秒数。

## 定义权限和日志选项

`TimeoutIdle` 关键字定义了在服务器和客户端之间的活动数据连接期间，未发送数据的最大等待秒数（换句话说，连接已挂起）。默认值为 `0`（无限期）。

现在你可以开始为服务器定义权限了。首先，你想允许所有用户登录服务器，所以我们必须使用 `<Limit>` 指令。因为这在 `<Global>` 或 `<VirtualHost>` 指令之外，此设置适用于所有定义的服务器：

最后，`MaxInstances` 关键字定义了独立服务器在任何给定时间产生的最大子进程数（对空闲启动的服务器没有影响）。由于每个子进程都是活动连接，它也控制了可以同时登录的用户数。超过配置最大值的连接将写入系统日志并被拒绝。默认是无限的，但这通常定义了配置。

### 服务器和服务

```
# 基本默认设置
Port 21
TimeoutLogin 120
TimeoutIdle 600
TimeoutTransfer 900
TimeoutStalled 3600
MaxInstances 30

# 服务器信息
ServerName? MyServer
ServerType standalone
ServerAdmin mailto:myemail@mydomain.com
```

`DefaultServer on`

`ServerName` 关键字定义了服务器的默认名称。`HttpServer` 关键字

`Timeout` 关键字定义了在未接收数据或其他数据模式的情况下，`ProFTPD` 等待断开客户端的秒数。值 `0` 将禁用此，但如果 `TCP` 连接损坏，这通常是一个坏主意，服务器将永远不会终止断开的会话。

并使用写入格式将 `READ` 命令组写入文件 `/var/log/access.log`（还记得之前定义的 `LogFormat` 关键字吗？）。第二个 `ProFTPD` 实例将所有 `AUTH` 命令记录到文件 `/var/log/proftpd/auth_name` 格式。最后一个实例是一个捕获型日志（paranoid log），它将使用默认格式写入 `/var/log/proftpd/paranoid.log` 文件。

对于安全意识型系统，你应该关闭它，否则匿名用户将永远无法登录。

`AnonRequirePassword` 如果设置为 `on`，将强制客户端输入有效密码。在匿名环境中，预计客户端将输入电子邮件地址作为密码，因此你应该设置 `AnonRequirePassword off`。如果你正在定义一个需要强制使用有效密码的访客账户，你将设置

你 FTP 站的后续部分。所有有效用户都将使用其常规用户名/密码登录到主目录，但为了允许匿名 FTP 客户端，你需要在 `<Anonymous>` 和 `</Anonymous>` 标签中定义一个区域，如下：

最后，让我们为真实用户添加一些额外的安全性。由于默认情况下你将连接到 FTP 站点并放置在 `/anonymous` 目录，让 `ProFTPD` 对该主目录进行 `chroot`。这可以防止用户移动到主目录之外。在任何其他没有 `chroot` 主目录的 FTP 目录，例如 `/etc` 或 `/usr/bin`。当你告诉 `ProFTPD` `chroot` 主目录时，你将被放置在 `/home/username`，且 `/home/username` 被视为绝对目录。如果用户尝试切换到 `/etc` 或 `/username`，`ProFTPD` 将尝试切换到 `/home/username/etc`。此外，这不应该是 FTP 安全性的完整基础（这成本很高），用户 组

```xml
<Anonymous>
    User ftp
    Group ftp
    UserAlias anonymous
    RequireValidShell off
    AnonRequirePassword off
    MaxClients 10
</Anonymous>
```

此部分告诉 `ProFTPD` 允许在主目录进行匿名连接。（你可以完全使用 `/home ftp`，不像 `wu-ftpd` 那样需要匿名密码）。在这里你再次定义 `User` 和 `Group` 关键字，告诉 `ProFTPD` 允许使用 FTP 用户的 `UID`/`GID` 建立匿名 FTP 连接。`UserAlias` 关键字告诉 `ProFTPD` 将匿名用户名映射到 FTP 用户。如果你没有名为 `anonymous` 的匿名 Linux 用户，为了允许该操作，你需要将其映射到一个现有的登录用户，使用 `ftp` 或 `nobody`。`UserAlias` 的格式为

```
DefaultRoot /home/bob

DefaultRoot /home/jim jim
```

这 意味着当 `bob` 登录时，他的根目录是 `/home/bob`，用户 `jim` 也是如此。

## 结论

虽然加固 FTP 站点并不是最简单的，但 `ProFTPD` 通过提供允许你收紧系统潜在漏洞防御措施的指令，使其变得更简单、更直观。除了安全性之外，`ProFTPD` 还是大多数 Linux 发行版自带的 `wu-ftpd` 的传统替代品。它不仅安全得多，而且更加通用且可配置。关键字

```
<login-user> <userid>
```
