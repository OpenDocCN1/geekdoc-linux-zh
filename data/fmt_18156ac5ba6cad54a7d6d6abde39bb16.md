
6. 重启 Apache 服务器，你就可以通过 `http://www.yourdomain.com/appname` URL 访问 FastCGI 应用/脚本，其中 `www.yourdomain.com` 应替换为你自己的 Web 服务器主机名，`appname` 应替换为你放在 `/www/mysite/fast-bin` 目录中的 FastCGI 应用。要测试你的 FastCGI 设置，只需将以下测试脚本（见列表 5-2）放在你的 fast 目录中然后访问它。

列表 5-2：`testfcgi.pl`

```perl
#!/usr/bin/perl -w
## CVS ID: $$Id:
use strict;
use CGI::Fast qw(:standard);
# 在此处执行任何启动/初始化步骤。

my $counter = 0;
```

## 第5章：Web 服务器性能

117

```perl
#
### FastCGI 请求循环
while (new CGI::Fast) {
    print header;
    print "This is a FastCGI test script" . br;
    print "The request is served by script PID: $$ . br;
    print "Your request number is : $counter++;"; br;
}
exit 0;
```

当你在运行列表 5-2 中的脚本时，使用诸如 `http://www.yourserver.com/fast-bin/testfcgi.pl` 的 URL 请求，你会发现 PID 不会改变，而计数器（`counter`）会随着你不断刷新请求而发生变化。如果你在运行此 FastCGI 的 Web 服务器上执行 `auxww | grep testcgi`，你会看到只有一个脚本实例在运行，并且它正在处理所有的客户端请求。如果负载过高，Apache 会启动另一个脚本实例。

FastCGI 是扩展你的 Web 应用程序扩展性的极佳解决方案。它允许你将在远程应用程序服务器上运行 FastCGI 应用程序/脚本。这意味着你可以将 Web 服务器与应用程序分离，从而获得更好的管理和性能潜力。此外，与 `mod_perl` 不同，为了性能，你并不局限于基于 Perl 的脚本；通过 FastCGI，你可以使用多种编程语言（如 C、C++ 和 Perl）编写你的应用程序。

非常有趣，Java 已开始在高性能 Web 应用程序开发中占据领先地位。在几年前，Java 还被认为运行缓慢且编写 Web 应用程序过于形式化。随着 Java 的成熟，它已演变成一个非常强大的 Web 开发平台。通过 Java，你拥有 Java Servlets、Java Server Pages 以及许多可用于提高扩展性和健壮性的 Java 技术。Java 赋予你创建分布式 Web 应用程序的能力。

### 使用 Java servlets

出于某些未知原因，Linux 平台上的 Java 并没有一个良好的开端。它正在逐渐好转，Java 运行时环境和开发工具也更加稳定。尽管如此，即使是复杂的多线程 Java servlets，当相同的代码在其他操作系统（如 Solaris 或 Windows 2000）下运行良好时，在 Linux 下仍然无法工作。

配合后端数据库 `lets` 使用非常 `lets`。你可以实现一个作为数据库连接池的 Java servlet，保持到后端数据库服务器的连接集。当另一个 servlet 需要数据库连接时，它可以从连接池服务器获取，并在完成使用后返回。这提供了比

# 第二部分：网络与服务性能

118

`mod_fastcgi`

比之前讨论的 `mod_perl` 或 `mod_fastcgi` 方法更有效的数据库池化管理。如果你在思考为什么我一直提到数据库连接性，那么你可能还没有开发过主要的 Web 软件。几乎每个主要的软件开发都需要后端连接，我经常根据平台允许如何（以及方便地）管理此类资源来考虑一个平台的好坏。Java servlets 在一个或多个定义了这一点。现在你知道了加速静态和 Web 内容的许多方法，请考虑加速你对他人内容的访问。这通常通过设置一个具有缓存能力的代理服务器来实现。在接下来的章节中介绍了 Squid，它正是如此。

## 使用 Squid 代理缓存服务器

Squid 是一个开源的符合 HTTP 1.1 标准的代理缓存服务器，可以增强用户的 浏览体验。你可以从 `www.squid-cache.org` 下载最新的稳定 Squid 源码分发。理想情况下，你希望使用两个网络接口运行代理缓存服务器。

- 一个接口连接到互联网网关或路由器
- 一个接口连接到内部网络。

> 禁用代理缓存系统上的 IP 转发可以确保没有人能绕过代理服务器直接访问互联网。

以下是如何为你的系统安装和配置它。

## 编译并安装 SQUID 代理缓存服务器

1. 切换到 root 用户并使用 `tar xvzf squid-version.tar.gz` 提取源码包（其中 `version` 是 Squid 软件的最新版本号）。
2. 运行 `./configure --prefix=/usr/local/squid` 命令为你的系统配置 Squid 源码。
3. 运行 `make all; make install` 将 Squid 安装在 `/usr/local/squid` 目录。

## 第5章：Web 服务器性能

## 配置 SQUID 代理缓存服务器

在安装 Squid 之后，你必须对其进行配置。以下是配置 Squid 的方法。

1. 使用 `groupadd nogroup` 命令创建一个名为 `nogroup` 的组。该组供 Squid 使用。
2. 运行 `chown -R nobody:noggroup /usr/local/squid` 命令，将 `/usr/local/squid` 目录及其所有子目录的所有权交给 `nobody` 用户和名为 `noggroup` 的组。这使得 Squid（以 `nobody` 用户运行）能够创建缓存目录并写入日志。
3. 决定你想在哪个端口上运行代理缓存。大多数站点在 8080 端口运行代理缓存，因此我在这里使用该值。
4. 在 `squid.conf` 文件中添加以下行：

```
http_port 8080
```

这告诉 Squid 使用端口 8080 处理代理请求。

如果你倾向于使用不同的端口，请在此使用。不要使用已被其他服务器占用的端口。理想情况下，你希望使用 1024 以上的端口号。

5. 定义你想缓存数据的位置。在 `squid.conf` 中定义以下行：

`cache_dir ufs /usr/local/squid 100 256`

这告诉 Squid 将缓存数据存储在 `/usr/local/squid`。如果你有大量用户将使用此缓存，跨多个磁盘是一个好主意。

5. 为你的网络创建一个访问控制列表 (ACL)。默认情况下，Squid 不允许任何地方的连接；此安全特性使用简单的方法：拒绝所有人，只允许特定的人。例如，如果你的网络是 `192.168.1.0/255.255.0`，那么可以在 `squid.conf` 中定义以下行为你的网络创建 ACL。

`acl local_net src 192.168.1.0/255.255.0`

6. 在 `http_access deny all` 行之前添加以下行：

```
http_access allow local_net
```

这告诉 Squid 允许 `local_net` 访问

7. 告诉 Squid 使用管理器。如果你想使用 `webmaster@yourdomain.com` 作为管理器，在 `squid.conf` 文件中定义以下行：

```
cache_mgr webmaster
```

8. 告诉 Squid 应该以哪个用户和组运行。在 `squid.conf` 中添加以下行：

```
cache_effective_user nobody
cache_effective_group nogroup
```

在这里，Squid 被要求以办法 用户运行并使用名为 `nogroup` 的组。保存 `squid.conf` 文件并运行以下命令创建缓存目录。

```
/usr/local/squid/squid -z
```

现在你可以运行 `/usr/local/squid/bin/squid &` 启动 Squid。通过有很多方法验证其运行正常：

- Squid 出现在 `ps -x` 列表中。
- 运行 `client www.nitec.com` 将 页面文本输出到你的终端。
- `/usr/local/squid/logs` 目录下的 `cache.log` 和 `store.log` 文件显示 Squid 正在运行。
- 运行 `squid -k check && echo "Squid is running"` 查看 Squid 是否激活。
