
# 第5章：Web 服务器性能

`ProxyPass /myapps http://127.0.0.1:8080/myapps`

你可以将 `/myapps` 更改为任何喜欢的名称。如果你确实更改了它，请确保在提到它的其他所有地方也进行更改。在这里，我们告诉处理静态页的 Apache 服务器，所有对 `/myapps` URL 的请求都应通过代理模块处理，它应该从运行在同一 Linux 系统（`127.0.0.1` 是本地主机）但端口为 `8080` 上的 Apache 服务器获取响应。

## 配置 mod_perl 脚本位置

在 `httpd-8080.conf` 中添加以下配置以创建一个 mod_perl 脚本位置。

```apache
<Location /myapps>
SetHandler perl-script
</Location>
```

当你开始使用许多 mod_perl 脚本时，你会发现 Apache 子进程的尺寸变大了。你可以使用 `top` 命令。只要你有足够的 RAM，通常就没问题。然而，没有人会拥有过剩的 RAM。避免依赖于大量内存作为你的解决方案是一个好主意。

如果你发现 Apache 子进程由于加载到它们中的许多 mod_perl 脚本而变大，可以考虑建立一个仅提供动态内容的专用脚本服务器。图 5-1 显示了这可以如何工作。

当用户请求名为 `www.domain.com` 的网站主页时，处理静态页的 Apache 服务器向客户端返回 `index.html` 页面。该页面包含静态和动态内容的嵌入链接。图中显示了两个链接：登录（login）和隐私（privacy）。当终端用户点击登录链接时，它请求 `http://myapps.domain.com/login`，在理想世界中，这与 `www.domain.com` 服务器是不同的 Apache 服务器。然而，并不是所有人都能负担得起这样分离动态和静态内容，这并不适用于所有人。

![](img/6d176ba5e3d859ca2b04a3bba254354c_135_0.png)

图 5-1：分离静态和动态（mod_perl 脚本生成）内容

如果你必须将 mod_perl 和静态内容留在运行 Apache 的同一 Linux 系统上，你仍然可以确保庞大的 Apache 子进程不提供静态页面。这是一个类似的解决方案：

1. 为你的 Apache Web 服务器编译并安装 `mod_proxy` 模块。
2. 将现有的 `httpd.conf` 文件复制到 `httpd-8080.conf`，并将 `Port` 指令修改为 `Port 8080` 而不是 `Port 80`。从 `httpd.conf` 中移除所有 mod_perl 特有的配置，以便你所有的 mod_perl 特有配置都在 `httpd-8080.conf` 文件中。
3. 修改 `httpd.conf` 文件以包含以下代理指令：

`ProxyPass /myapps http://127.0.0.1:8080/myapps`

你可以将 `/myapps` 更改为任何喜欢的名称。如果你确实更改了它，请确保在提到它的其他所有地方也进行更改。在这里，我们告诉处理静态页的 Apache 服务器，所有对 `/myapps` URL 的请求都应通过代理模块处理，它应该从运行在同一 Linux 系统（`127.0.0.1` 是本地主机）但端口为 `8080` 上的 Apache 服务器获取响应。
4. 在 `httpd-8080.conf` 中添加以下配置以创建一个 mod_perl 脚本位置。

```apache
<Location /myapps>
SetHandler perl-script
</Location>
```

### 使用 FastCGI

类似于 mod_perl 脚本，FastCGI 应用持续运行（初始加载后），因此比 CGI 脚本具有显著的性能优势。表 5-2 总结了 FastCGI 应用与 mod_perl 之间的差异。

### 表 5-2：FastCGI 应用与 mod_perl 脚本的差异

| 主题 | FastCGI 应用 | mod_perl 脚本 |
| --- | --- | --- |
| 依赖 Apache | 否。FastCGI 应用可以在非 Apache 服务器（如 IIS 和 Netscape Web Server）上运行。 | 是。只有 Apache 支持 mod_perl 模块 |
| Perl 解决方案 | 否。FastCGI 应用可以使用许多语言开发，如 C、C++ 和 Perl。 | 是 |
| 作为外部进程运行 | 是 | 否 |
| 可以在远程机器运行 | 是 | 否 |
| 运行多个应用程序/脚本实例 | 通常运行单个 FastCGI 应用来响应许多队列中的请求。然而，如果负载很高，会运行同一应用程序的多个实例。 | mod_perl 脚本的实例数量等于 Apache 子进程的数量。 |
| 广泛支持 | 是。然而，有时我总觉得 FastCGI 的开发正在放缓，但我无法证实或支持这一观点。 | 是。互联网上有许多关于 mod_perl 的网站，并可以通过 Usenet 或 Web 获取支持。 |
| 数据库连接 | 由于所有请求都发送到单个 FastCGI 应用，你只需要与后端数据库服务器维持单个数据库连接。然而，当负载过高导致 Apache FastCGI 进程管理额外的 FastCGI 应用实例时，可能会发生变化。尽管如此，应用程序的 FastCGI 实例数量可能少于 Apache 子进程的数量。 | 由于每个 Apache 进程都会运行 mod_perl 脚本，每个子进程都可能拥有指向后端数据库的连接。这意味着即使仅从一个 Apache 服务器系统，你最终可能产生数百个数据库连接。 |

与 mod_perl 一样，FastCGI 的 Apache 模块 `mod_fastcgi` 未包含在标准 Apache 分发中。你可以从 `www.fastcgi.com` 下载。以下是安装方法。

#### 为 Apache 安装并配置 FastCGI 模块

假设你已经将 Apache 源码包安装在 `/usr/src/redhat/SOURCES/apache_x.y.z`（其中 `x.y.z` 是 Apache 的最新版本）。要为 Apache 安装 `mod_fastcgi` 模块，请执行以下操作：

1. 切换到 root。
2. 使用 `tar xzvf mod_fastcgi.x.y.z.tar` 命令解压 mod_fastcgi 源码包。将 mod_fastcgi 源码目录拷贝到 `/usr/src/redhat/SOURCES/apache_x.y.z/src/modules/fastcgi` 目录。
3. 使用配置脚本 `configure` 并以下选项配置 Apache：

`--active-module=src/modules/fastcgi/libfastcgi.a`

如果你已经使用许多其他选项编译了 Apache 并希望保留它们，只需在 `/usr/src/redhat/SOURCES/apache_x.y.z` 目录下运行以下命令：

`./config.status --activate-module=src/modules/fastcgi/libfastcgi.a`
4. 在同一目录下运行 `make; make install` 命令，以编译并安装支持 `mod_fastcgi` 的新 Apache。
5. 现在已准备好配置 Apache 来运行 FastCGI 应用了。首先确定你想将 FastCGI 应用和脚本放在放在。理想情况下，你想将此目录放在 `DocumentRoot` 指令指定的目录之外。例如，如果你将 `DocumentRoot` 设置为 `/www/mysite/htdocs`，考虑使用 `/www/mysite/fast-bin` 作为 FastCGI 应用/脚本目录。我假设你会采纳我的建议这样做。要告诉 Apache 你已创建了新的 FastCGI 应用/脚本目录，只需使用以下配置：

```
Alias /apps/ "/www/mysite/fast-bin"
<Directory "/www/mysite/fast-bin">
Options ExecCGI
SetHandler fastcgi-script
</Directory>
```

这告诉 Apache 别名 `/apps/` 指向 `/www/mysite/fast-bin` 目录 —— 该目录包含通过 `fastcgi-script` 处理器运行的应用程序（或脚本）。
