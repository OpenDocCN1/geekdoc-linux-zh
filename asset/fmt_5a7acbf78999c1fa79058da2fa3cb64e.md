
```
cd
tar xvzf apache_1.3.14.tar.gz
```

现在使用以下命令将 `apache_1.3.14+ssl_1.42.tar.gz` 复制到 `/usr/src/apache+ssl/apache_1.3.14` 目录：

```
cp apache_1.3.14+ssl_1.42.tar.gz apache_1.3.14/
```

解压 `apache_1.3.14+ssl_1.42.tar.gz` 将将内容放置在与其他 Apache 文件相同的目录中。执行此操作请使用以下命令：

```
tar xvzf apache_1.3.14+ssl_1.42.tar.gz
```

# 使用 mod_sslnSupport 编译 Apache

下一步是对 Apache 应用 SSL 补丁。Apache+SSL 附带了一个在系统中无法运行的脚本，应使用 `patch` 命令手动应用补丁。（有关使用 `patch` 的更多信息，请参阅 man 手。此外，请参考 `README.SSL` 文件以获取有关编辑 `/usr/src/apache+ssl/apache_1.3.14/src/Configuration` 所需配置设置的信息）。接下来，使用 Fixpatch 脚本应用补丁：

```
/Fixpatch
```

Apache 现在已准备好安装和配置。应该执行以下操作：

```
./configure --enable-module=so
make
make install
```

默认情况下，Apache 文件被放置在 `/usr/local/apache` 目录。如果一切运行正常，应该显示以下输出：

> | 你现在已成功构建并安装了
> | Apache 1.3 HTTP 服务器。要验证 Apache 实际上
> | 正常工作，你现在应该首先检查
> | （最初创建或保留的）配置文件
> | `/usr/local/apache/conf/https.conf`|
> | 然后你应该能够通过运行
> | 立即启动第一次 Apache：
> | `/usr/local/apache/bin/httpsctl start`|
> | 感谢使用 Apache。Apache 
> | http://www.apache.org/

# 验证 Apache 已用 mod_ssi 编译

下一步涉及创建证书。进入 `/usr/src/apache+ssl/apache_1.3.14/src` 目录并制作证书：

```
cd src
make certificate
```

生成以下输出（填写与系统相关的信息）：

你将被要求输入将包含在证书请求中的信息。

你正要输入的内容被称为特权名称（Distinguished Name，简称 DN）。

字段很少，但你可以留一些空白。

某些字段将有一个默认值。

如果你输入 "."，该字段将留空。

国家名称（2 位代码） [GB]:

州或省份名称（全称） [Some-State]:

地区名称（例如，城市） [];

组织名称（例如，公司，推荐） [];

组织单位名称（例如，部门） [];

服务器名称（例如，ssl.domain.tld，必须提供！） [];

电子邮件地址 []:

# 在 浏览器中测试示例页面

最后一步是用 SSL 替换 Apache 配置文件 (`httpd.conf`)。`httpd.conf` 文件的位置随发行版而异。以下文件显示了 Red Hat 的默认位置：

默认设置在大多数情况下都是有效的。如果对 `httpd.conf` 进行了更改，请在启动 Apache 守护进程之前检查配置，如下所示：

```
/usr/local/apache/bin/apachectl configtest
/usr/local/apache/bin/apachectl start
```

可以通过调出浏览器并连接到 `http://localhost` 来检查服务器。屏幕上应该显示一个 OpenSSL 证书。

# 问题

- 1. 提供一种检查 Apache+SSL 安装是否运行正常的方法。
- 2. “普通用户”可以使用 `apachectl` 吗？
- 3. 为什么 SSL 和 Apache 分别分发？

# 答案

- 1. 从服务器端运行 `Lynx localhost`，或者在 Netscape Navigator、Internet Explorer 或其他浏览器中访问 `http://localhost`。
- 2. 不，`apachectl` 必须以 root 身份运行。
- 3. 由于美国和其他国家实施的出口限制，某些软件无法带有特定类型和级别的加密进行分发。因此，Apache 只能在不包含 SSL 提供的加密和其他功能的情况下分发。

# 高级问题

- 1. Apache+SSL 如何在服务器和客户端之间协商内容？
- 2. Apache+SSL 提供哪些加密方法？

# 配置 Apache 执行常见任务

## 目的

本实验的目的是设置一个具有多种常用 Web 服务器功能的 Apache 服务器。Apache 是最常用的 Web 服务器，因为它是免费提供的，并且可以自定义以适应几乎任何 Web 服务器的需求。

在本次实验中，你将执行以下步骤：

- 1. 使用多个守护进程实例
- 2. 添加虚拟主机

## 理论

与基于 IP 的托管类似，基于名称的托管允许多个服务器名称指向一台机器。其优势之一是多个主机可以使用单个 IP 地址，避免了获取额外 IP 地址的需求。基于名称的托管是因为大多数浏览器都提供了该功能。当浏览器请求页面时，标头中包含了目标名称。Apache 能够使用此信息并将请求重定向到位置。

配置系统使用基于名称的托管是在 `httpd.conf` 文件中进行的。在大多数发行版中，虚拟主机部分被注释掉了；实现虚拟主机简单的方法是移除注释。以下步骤显示如何向站点添加基于名称的托管：

- 1. 使用文本编辑器 Apache 配置文件 (`httpd.conf`)。
- 2. 在文件中添加以下文本：

```
<VirtualHost 123.45.67.89 - 指定用于名称托管的 IP 地址
ServerName www.sitel.com - 第一个网站的请求名称
ServerAdmin webmaster1@sitel.com - 管理员电子邮件
DocumentRoot /home/web/sitel - 第一个网站的目录
ErrorLog /var/log/sitel-error_log - 第一个站点的错误日志
</VirtualHost>
#第二个主机
<VirtualHost 123.45.67.89 - 指定用于名称托管的 IP 地址
ServerName www.sitel2.com - 第二个网站的请求名称
ServerAdmin webmaster2@sitel2.com - 管理员电子邮件
DocumentRoot /home/web/site2 - 第二个网站的目录
ErrorLog /var/log/sitel2-error_log - 第二个站点的错误日志
</VirtualHost>
```

3. 确保指定的目录包含适当的内容。

使用 `apachectl graceful` 重启 `httpd` 进程以读取新配置。

# 实验练习

为了执行这些练习，你需要找到并理解 `/usr/local/apache/` 下的 Apache 配置文件。所有其他 Apache 信息也位于此处。在继续之前，确保你已找到配置文件。

为了成功调试这些练习，定位 Apache 日志（特别是错误日志 error log）对你非常有帮助。再次，这些日志位于不同的地方。Red Hat 将它们放在 `/var/log/httpd`（并从 `/etc/httpd/logs` 建立符号链接）。Apache 发行版（未修改的）将它们放在 `/usr/local/apache/logs/`。

一旦找到了合适的 Apache 文件和日志，请按照以下步骤操作：

- 1. 重新配置 Apache，为每个用户（`~username` 路径）提供一个私有的 `cgi-bin` 目录，可以位于用户的 Web 文根目录下，也可以位于用户家目录的其他地方。
- 2. 通过编写一个很小的 Perl 脚本或打印 hello 的脚本来测试 `cgi-bin` 目录。
- 3. 为 Apache 绑定第二个 IP 地址（`192.168.1.250`）以作为虚拟站点使用。
- 4. 配置 Apache 使用新的 IP 地址作为 IP 虚拟服务器。

# 问题

- 1. 单台机器最多可以容纳多少基于基于虚拟主机（name-based virtual hosts）？
- 2. 通常使用什么脚本来重启 `httpd` 进程？
- 3. 列出三种用于生成 CGI 脚本的常用语言。

# 答案

- 1. 没有上限。但是，虚拟主机越多意味着消耗的资源越多，这会影响系统的性能。
- 2. `apachectl`。
- 3. Perl、JavaScript 和 PHP。

# 高级问题

- 1. 为什么你想将 `cgi-bin` 目录放在文档根目录之外？
- 2. 在服务器上散布多个 `cgi-bin` 目录有什么危险？

# 创建简单的 CGI 脚本

## 目的
