
# 和客户端（仅在启用客户端身份验证时存在）的 PEM 编码证书。

# 这可以将证书导入到 CGI 脚本中。

```apache
# 导出环境变量：

# 这导出标准的 SSL/TLS 渲染 "SSL_* 环境变量"。

# 默认出于性能考虑，此导出是关闭的，

# 因为提取步骤是一个昂贵的操作，且对于提供静态

# 内容通常没有用。通常只对 CGI 和 SSI 请求

# 启用导出。
```

# 配置 Apache

```apache
# CompatEnvVars:

# 此项为了向后兼容导出了过时的环境变量

# 适用于 Apache-SSL 1.x, mod_ssl 2.0.x, Sioux 1.0 和 Stronghold 2.x。使用此项

# 为现有的 CGI 脚本提供兼容性。

# o StrictRequire:

# 当应用 "SSLRequireSSL" 或 'SSLRequire' 时，将拒绝访问，即使

# 在 "Satisfy any situation" 的情况下（即当满足访问时也会被拒绝

# 且没有其他模块可以更改）。

# o OptRenotiate:

# 当在每个目录上下文中启用 SSL 指令时，此项将启用 SSL 连接重协商 own处理。

#SSLOptions <FakeBasicAuth+ExportCertData+CompatEnvVars+StrictRequire

<Files "\.(cgi|shtmlhtml)">

SSLOptions +StdEnvVars

</Files>

<Directory "/var/www/cgi-envVars">

SSLOptions +StdEnvVars

</Directory>
```

> # 注意：大多数客户端连接的问题也与 HTTP
> # 保持连接（keep-alive）机制有关，因此你通常还想为
> # 客户端禁用保持连接。使用变量 "nokealive" 执行此。
> SetEnvIf User-Agent "*,MSIE;*" nokealive ssl-unclean-shutdown

```apache
# 服务器级日志：

# 自定义 SSL 日志文件的所在地。当你希望基于虚拟主机

# 生成一个紧凑的非错误 SSL 日志文件时，使用此项。

CustomLog /var/log/httpd/ssl_request_log \
  %t %h %(SSL_PROTOCOL)x %(SSL_CIPHER)x "%r" %b

<VirtualHost>
```

<IfDefine>

你应该首先注意到此文件由注释和实际的配置项组成。注释以井号 (`#`) 开头。配置项由一个条目名称及其对应的值组成。

`httpd.conf` 文件中有三个主要部分：全局环境、主服务器配置和虚拟主机。让我们详细查看每个部分。

## 全局环境

此部分中的指令和模块控制整个 Apache 服务器进程的运行。你在这里看到的内容适用于所有 Apache 主机，无论它们是主服务器还是后续章节中讨论的任何虚拟主机。

### ServerType

你将学习的第一个指令是 `ServerType`。Apache 服务器可以以两种方式运行：以带有独立进程监听连接的独立模式运行，或者以 inet 模式运行（你在网络章节中见过这种模式）。在 inet 模式下，inet 监听连接并在当连接到来时启动 Apache 进程。如果这是你第一次运行 Web 服务器，那么你将以独立模式运行 Apache，除非你熟悉 inet、正在使用 Unix 类的，并且有充分的理由以这种方式运行服务器。

### ServerRoot

`ServerRoot` 用于指定服务器配置文件和日志文件的基础目录。Red Hat 将其设置为 `/etc/httpd` 目录。该目录下有一个 `conf` 目录，其中包含三个配置文件，以及一个指向 `/var/log/httpd` 的 `logs` 目录链接。

你可以自由地将该目录移动到系统的任何位置，以匹配你正在使用的管理风格。然而，通常将它们保留在 Linux 发行版存放的地方是最简单的。

### 加载模块

第一个主要部分由一系列 `LoadModule` 指令组成，随后是一系列 `AddModule` 指令。Apache 的功能通过使用模块来创建和扩展。在 Apache 的早期版本中，这些模块被组合到可执行的 `httpd` 文件中。从 Apache 1.3 版本开始，现在可以创建在服务器启动时加载的模块。

由于这些模块大部分通过指令进行配置，因此在 `httpd.conf` 文件中出现任何其他指令之前，加载所有相关模块是非常重要的。

对于最基础的安装，默认模块列表已经足够，你不需要更改它。如果你需要扩展或更改，请参考 Apache 官方文档。

## 主服务器配置

此部分包含配置 Apache 服务器的常用指令。

紧随 `order` 指令的是 `allow` 指令，它表示所有用户都应该允许访问。如果你想完全理解如何拒绝用户，应该阅读位于 `http://httpd.apache.org` 的在线 Apache 文档。

### UserDir

`UserDir` 是一个指令，当 Web 管理员希望系统上的每个用户都能拥有自己的个人网站，并通过其主目录下的子目录对其进行管理时，该指令非常有用。此指令指示了其主目录中应被视为 Web 目录的子目录名称。

通常的做法是使用 `public_html`。因此，如果用户 `tester` 有目录 `/home/tester/public_html`，那么可以通过 URL `http://servername/~tester` 通过 Web 该目录。

### DirectoryIndex

`DirectoryIndex` 是一个重要的指令，因为它指示了哪些文件应该被视为默认文件。通过这种方式，像 `http://www.mommabeas.com` 这样的 URL 才能访问正确的文件。

例如，在上面的示例 `httpd.conf` 文件中，为目录索引（Directory Index）提供了七个条目：`index.html`、`index.htm`、`index.shtml`、`index.php`、`index.php4`、`index.php3` 和 `index.cgi`。这意味着对于任何指定了文件名但仅给出目录的 URL，服务器将首先尝试从指定的目录返回 `.html` 文件。如果该文件不存在，则返回 `index.htm`；如果该文件仍不存在，则向客户端发送 `index.shtml`。如果没有找到任何匹配的文件，服务器将根据其他配置选项返回目录列表或错误信息。

### AccessFileName

`AccessFileName` 用于指定包含给定目录访问控制信息的文件名。访问控制信息可以存储在 `httpd.conf` 文件中，也可以存储在每个主目录下的 `.htaccess` 配置文件中。

示例文件表明，如果目录存在名为 `.htaccess` 的文件，则该文件包含该目录的访问控制信息。

### ScriptAlias

设置 `ScriptAlias` 指令非常重要，这样就可以设置一个目录来存储 CGI 程序和脚本。`ScriptAlias` 指定了使用哪个目录用于 CGI 脚本以及该目录的 URL 是什么。除非根据文件扩展名赋予运行 CGI 权限（你将在下一节关于 `AddHandler` 指令的讨论中看到），否则此目录中的文件将自动被视为 CGI 程序。

例如，使用以下指令的示例文件：

```
ScriptAlias /cgi-bin/ /var/www/cgi-bin
```

此行表示 URL `http://www.mommbears.com/cgi-bin/` 指向 `/var/www/cgi-bin/`。在此目录中，文件被视为 CGI 脚本，服务器接受执行这些文件而不是将其直接返回给请求客户端。

### 启用 CGI 目录

与之前描述的 HTML 目录项相比，CGI 目录项看起来有点不同：

```
<Directory /var/www/cgi-bin>
AllowOverride None
Options ExecCGI
Order allow,deny
Allow from all
</Directory>
```
