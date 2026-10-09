
# Apache 模块

`apache2-mod-macro` - 在 `apache` 配置文件中创建宏

`apache2-mod-perl` - 将 `perl` 集成到服务器

`apache2-mod-perl-dev` - 将 `perl` 集成到服务器

`apache2-mod-perl-doc` - 将 `perl` 集成到服务器文档

`apache2-mod-php` - 嵌入 `PHP` 脚本语言的 2

`apache2-mod-phpfilter` - 嵌入 `PHP` 脚本语言的...

`apache2-mod-python` - 在服务器中嵌入 `python` 的 2

```bash
$ apt-cache search apache2-mod-ruby | grep ruby
```

## 模块

`Apache` 是一个骨架程序，依赖外部模块（称为共享对象）来提供大部分功能。除了 `Ubuntu` 自带的模块外，还有许多可用模块。更多信息请见 `httpd.apache2/modules`。启用模块请参阅第 905 页。

## 配置模块

你可以通过编辑 `mods-available` 目录中相应的 `.conf` 文件来配置某些模块。模块文件名以 `apache2-mod-` 为前缀。以下命令显示模块列表。你可以通过 `grep` 过滤列表找到你需要的模块。关于 `apt-cache` 请见第 530 页。

## `mod_cgi` 与 `CGI` 脚本

`CGI`（通用网关接口）允许外部应用程序与 `Web` 服务器交互。任何运行时（在请求时运行）并将其输出传递给客户端的程序都是 `CGI` 程序。各种脚本（包括 `shell`、`Perl`、`Python` 和 `PHP`）是最常见的 `CGI` 程序，因为脚本可以调用程序并为客户端格式化输出。

`Apache` 可以以不同的方式处理 `CGI` 请求。最常见的方法是将 `CGI` 程序放在 `cgi-bin` 目录并仅允许在该目录下执行。`ScriptAlias` 指令（第 929 页）指定的 `cgi-bin` 目录位置为 `/usr/lib/cgi-bin`。或者，可以使用 `AddHandler` 指令（第 923 页）通过正则表达式识别脚本扩展名。如果你还需要在相应的 `<Directory>` 容器的 `Options` 中指定 `ExecCGI` 选项。必须加载 `mod_cgi` 模块才能访问和执行 `CGI` 脚本。

以下是 `Perl CGI` 脚本显示 `Apache` 环境。此脚本仅用于调试，因为如果远程客户端可以访问它，则存在安全风险：

```perl
#!/usr/bin/perl
##
## printenv - 打印环境的演示 CGI 程序
##
```

```perl
print "Content-Type: text/plain\n";
foreach $var (sort(keys(%ENV))) {
  $val = $ENV{$var};
  $val = s/\n/\\n/g;
  $val = s/\/\\\/g;
  print "$var=$val\n";
}
```

## `mod_ssl`

`SSL`（安全套接层）由 `mod_ssl` 模块实现，具有两个功能：允许客户端验证服务器的身份，并确保客户端与服务器之间安全的双向通信。`SSL` 用于网页，并配合需要密码、信用卡号或其他敏感数据的表单。

`Apache` 使用 `HTTPS` 协议而非 `HTTP` 进行通信。当 `Apache` 使用 `SSL` 时，它会在第二个端口（默认为 `443`）上监听连接，并在向客户端发送请求内容之前执行一个 `SSL` 握手序列（`MYSQL` sequence）。

服务器验证对于金融交易至关重要。毕竟，你不想把信用卡号提供给一个伪装成知名公司的欺诈网站。`SSL` 使用证书来确定地识别服务器。在互联网等公共网络上，只有当证书包含来自 `VeriSign` 或 `Thawte` 等权威源的数字签名时，该身份才是可靠的。网页是由以 `https://` 开头的 `URI` 生成的。

数据加密可以防止恶意用户窃听互联网连接并复制个人信息。为了加密通信，`SSL` 位于网络和应用程序之间，并加密服务器与客户端之间的通信。

## 设置 `mod_ssl`

`mod_ssl` 包作为 `apache2` 软件包的一部分进行安装——你不需要单独安装它。`/etc/apache2/mods-available/ssl.conf` 文件配置了同一目录下的 `mod_ssl.load` 并加载了它。你必须使用命令 `aenmod ssl` 来启用该模块。该文件前几个指令设置了 `SSL` 操作的参数。

你可以在 `sites-available` 目录中为 `SSL` 设置虚拟主机，并使用 `aensite` 启用它（第 906 页）。与任何虚拟主机一样，`SSL` 虚拟主机也持有需要配置的指令，如 `ServerName` 和 `ServerAdmin`。此外，它还持有 `SSL` 相关的指令。请参见第 940 页的示例。

## 使用自签名证书进行加密

如果你需要 `SSL` 进行加密和验证——也就是说，如果客户端已经信任服务器——你可以生成并使用自签名证书，从而跳过获取数字签名证书的时间和费用。当你连接到服务器时，自签名证书会产生警告：大多数浏览器会显示一个对话框，允许你检查并接受证书。示例守护也使用了证书（第 736 页）。

以下示例创建了一个自签名证书。（如果系统中缺少 `apache2-ssl-certificate`，请参考 `www.apache.org/docs/2.8/ssl_faq.html#ToC28` 中的步骤。对于自签名证书，你不需要提交 `CSR`。）

### 第 944 页 第 26 章 APACHE：设置 Web 服务器

```bash
$ sudo apache2-ssl-certificate
正在创建自签名证书体系 (CA)
用由证书颁发机构签名的证书替换它
```

在 `Common Name` 提示处输入你的 `ServerName`

如果你希望证书在 `x` 天后过期，请使用 `-days x` 运行此程序

正在生成 `1024` 位的 `RSA` 私钥

```
++++++++
...... 正在将新的私钥写入 '/etc/apache2/ssl/apache.pem'
```

你将被要求输入一些将合并到你的证书请求中的信息。

你即将输入的内容被称为别名（`Distinguished Name`，简称 `DN`）。

那里有许多字段会有默认值，

如果你输入 `'.'`，该字段将留空。

```
Country Name (2 letter code) [GB]:US
State or Province Name (full name) [Some-State]:California
Locality Name (eg, city) [:San Francisco
Organization Name (eg, company; recommended) [:Sobell Associates Inc.
Organizational Unit (eg, section) []nserver name (eg, ssl.domain.tls; required!!) [:www.sobell.com
Email Address []msgs@sobell.com
```

前五个问题的答案是任意的：它们可以帮助客户端在检查证书时识别网站。第六个问题（服务器名称）的答案是至关重要的。因为证书与服务器名称绑定，你必须准确输入服务器的完全限定域名（`FQDN`）。如果你输错了这些信息，服务器名称和证书名称将不匹配。每次建立连接时，浏览器都会生成警告消息。

现在你在 `/etc/apache2/sites-available` 中创建一个启用 `SSL` 的虚拟主机。基于主机名的虚拟主机无法配合 `SSL` 工作，因为客户端发送的 `HTTP` 请求头是加密的。每个 `IP` 地址只能使用一个证书。在启用模块后，`Apache` 将收到一个错误。以下是 `SSL` 的设置：

```
<VirtualHost *:443>
  ServerName www.sobell.com
  SSLEngine On
  SSLCertificateFile /etc/apache2/ssl/apache.pem
  DocumentRoot /var/www/html
</VirtualHost>
```

该语言易于设置，语法与 `Perl` 和 `C` 相似，并带有大量与 `Web` 相关的函数。

## 多进程模块 (MPMs)

如果 `Apache` 仅在一个进程中运行，那么每当客户端请求页面时，`Apache` 都必须在从磁盘读取该页面（或等待 `CGI` 脚本生成它）时忽略其他请求。在读取页面后，它可以将页面发送给客户端并响应下一个请求。在这样的设置下，`Apache` 每次只能服务一个客户端。

`Apache 1.3` 及更早版本通过派生（`fork`）服务器来响应多个客户端。`Apache 2` 将派生行为移动到了 `prefork` 多进程模块 (`MPM`)。`MPM` 引入了在各种多进程处理技术之间切换的能力。

`prefork MPM` 使用 `fork()` 系统调用创建一个 `Apache` 进程的精确副本来服务每个请求。`MaxServers`、`MaxSpareServers` 和类似的指令控制同时运行的 `Apache` 进程数量。由于操作系统需要花费时间在 `Apache` 进程之间进行上下文切换，且每个进程都有自己的内存，`prefork MPM` 在繁忙的服务器上会产生巨大的开销。

`worker MPM` 通过使用线程减少了这种开销。线程类似于进程，它可以独立于其他线程或进程执行。在一个线程中等待读取完成不会停止（阻塞）其他线程的执行。线程和进程的区别是，所有在一个进程下运行的内容共享相同的内存，并且由程序而不是操作系统负责管理线程。`worker MPM` 维护一个线程池，可以使用它可以服务每个请求。`worker MPM` 不是像 `prefork` 那样让 `Apache` 派生子进程来服务每个请求的内容，而是使用线程来服务内容请求。

由于所有这些都运行在同一个进程下，它们共享相同的内存。不是线程安全的代码（参见第 1168 页的重入性 `reentrant`）可能会导致不一致的结果。例如，某些 `PHP` 库使用 `strtok()` 函数将字符串转换为标记（`tokens`）。该函数维护内部变量。如果它被共享相同内存的多线程调用，`strtok()` 的内部变量将处于不一致状态。

如果你想使用 `PHP`，必须使用 `prefork MPM`；或者，如果你想使用 `worker MPM` 和 `PHP`，则必须移除 `apache2-mod-php5` 并将 `PHP` 作为 `CGI` 脚本运行（第 942 页）。

可用的 `MPM` 包括：

- `apache2-mpm-prefork`—传统的 `MPM`。
- `apache2-mpm-worker`—高速线程型 `MPM`。
- `apache2-mpm-event`—事件驱动型 `MPM`。

## 第 948 页 第 26 章 APACHE：设置 Web 服务器

`apache2-mpm-worker`、`apache2-mpm-event`、`apache2-mpm-prefork` 都提供了 `apache2` 二进制文件，并且它们相互冲突。你不能同时安装这些模块中的多个。当你安装这些包之一时，安装程序会自动移除当前的 `MPM`。

## `webalizer`：分析 Web 流量

`webalizer` 包在 `/var/www/webalizer` 创建一个目录，并在 `/etc/cron.daily/webalizer` 创建一个 `cron` 文件（第 605 页）。每天一次，`cron` 文件会生成使用数据并将其放在 `webalizer` 目录中；你可以通过将浏览器指向 `http://server/webalizer/` 查看这些数据，其中 `server` 是服务器的主机。

`/etc/webalizer/webalizer.conf` 文件控制 `webalizer` 工具的行为。如果你更改了 `DocumentRoot` 或日志文件的位置，必须编辑此文件以反映这些更改。关于 `webalizer` 的更多信息，请参阅 `webalizer` 手册以及第 901 页“更多信息”列出的页面。

## `MRTG`：监控流量负载

`Multi Router Traffic Grapher` (`MRTG`; `mrtg` 包) 是一个开源应用程序，用于通过 `SNMP`（简单网络管理协议）提供的统计数据绘制图表。`SNMP` 信息在所有高端路由器和交换机上，以及某些网络设备（如打印机和无线访问点）上可用。

一旦安装并运行 `MRTG`，你可以在 `http://server/mrtg` 查看报告，其中 `server` 是服务器的主机。更多信息请参阅 `mrtg` 页面以及第 901 页“更多信息”下列的网站。

## 错误代码

以下是 `Apache` 错误代码列表：

| 代码 | 消息 | 代码 | 消息 |
| :--- | :--- | :--- | :--- |
| 100 | Continue (继续) | 404 | Not Found (未找到) |
| 101 | Switching Protocols (切换协议) | 405 | Method Not Allowed (方法不允许) |
| 200 | OK (正常) | 406 | Not Acceptable (不可接受) |
| 201 | Created (已创建) | 407 | Proxy Authentication Required (需要代理认证) |
| 202 | Accepted (已接受) | 408 | Request Timed out (请求超时) |
| 203 | Non-Authoritative Info... (非权威信息...) | 409 | Conflict (冲突) |
| 204 | No Content (无内容) | 410 | Gone (已删除) |
| 205 | Reset Content (重置内容) | 411 | Length Required (需要长度) |
| 206 | Partial Content (部分内容) | 412 | Precondition Failed (预条件失败) |
| 300 | Multiple Choices (多选) | 413 | Request Entity Too Large (请求实体过大) |
| 301 | Moved Permanently (永久移动) | 414 | Request-URI Too Large (URI 过大) |
| 302 | Moved Temporarily (临时移动) | 303 | See Other (查看其他) |
| 304 | Not Modified (未修改) | 305 | Use Proxy (使用代理) |
| 400 | Bad Request (错误请求) | 401 | Unauthorized (未授权) |
| 402 | Payment Required (需要付款) | 403 | Forbidden (禁止) |
| 415 | Unsupported Media Type (不支持的媒体类型) | 500 | Internal Server Error (内部错误) |
| 501 | Implemented (未实现) | 502 | Bad Gateway (网关错误) |
| 503 | Service Unavailable (服务不可用) | 504 | Gateway Time-out (网关超时) |
| 505 | HTTP Version Supported | | |

## 章总结

`Apache` 是互联网上最流行的 `Web` 服务器。它既健壮又灵活。`Apache` 可以响应多个 `IP` 地址或主机名，就像有多个服务器一样。每个 `IP` 地址或主机名都可以提供不同的内容。`CGI`（通用网关接口）允许外部应用程序与 `Web` 服务器交互。如果程序实时运行并将输出传递给请求客户端，它就是 `CGI` 程序。`SSL`（安全套接层）有两个功能：验证服务器的身份，以及启用客户端与服务器之间的双向通信。

## 练习

- 如何告诉 `Apache` 你的内容位于 `/usr/www`？
- 如何指示 `Apache` 服务器监听 `81` 端口而不是 `80` 端口？
- 如何允许 `Sam` 发布其 `~` 目录中的网页而不允许其他人发布？
- 为什么 `Apache` 必须以 `root` 权限启动？为什么这种操作不会产生安全风险？

## 高级练习

- 如果你在防火墙系统上运行 `Apache`（例如显示防火墙配置的 `Web` 前端），如何确保它仅从本地网络访问？
- 为什么使用 `mod_php` 或 `mod_perl` 运行脚本比通过 `CGI` 运行更高效？
- `SSL` 提供哪两个功能？如果证书是自签，情况会有何不同？
- `Web` 网站每次被访问时通过从数据库检索数据并使用 `PHP` 或 `CGI` 插入模板来生成动态内容。为什么这种做法主意意？
- 假设你想在托管公司网站的同一服务器上为员工提供 `Webmail` 访问。网站地址为 `example.com`，你想使用 `mail.example.com` 用于 `Webmail`，而 `Webmail` 应用程序位于 `/var/www/webmail`。描述两种设置这种内容的方法。
- `Web` 网站的一部分是私人内网。描述你如何防止公司内部 `192.168.0.0/16` 网络之外的人访问该站点。该站点定义如下：

```
<VirtualHost>
  ServerName example.com
  DocumentRoot /var/www
  <Directory /var/www/intranet>
    AllowOverride AuthConfig
  </Directory>
</VirtualHost>
```

# 第六部分

编程工具

## 第 27 章

编程 `BOURNE AGAIN SHELL` 953

## 第 28 章

`PERL` 脚本语言 1041

# 27

## 编程 `BOURNE AGAIN SHELL`

## 本章节选

- 控制结构 ................................. 954
- 文件描述符 ................................... 987
- 参数与变量 ...................... 990
- 数组变量 ..................................... 990
- 变量的局部性 ............................ 992
