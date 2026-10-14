
在继续本节之前，你必须已经解决了 DNS 和 Sendmail 的问题。在以太网章节中，没有是不需要路由的。你的主服务器会处理它的。请参考食谱示例中的那些页面。唯一的区别在于，在你的 DNS 表中，你需要为虚拟域名使用与主服务器相同的 IP，而不是给它分配一个新的 IP。

第一步是确保你正在运行 Apache 1.1b1 或更高版本。你可以向你的 `httpd` 进程发送一个 HEAD 请求，或者在命令行输入 `httpd -v` 来获取服务器的版本号。验证这些信息后，请继续。确保你对配置文件（位于 `/var/local/etc/httpd/conf/`）具有完全访问权限。

首先，你需要将主机名添加到你的 DNS 表中。如果你将进行虚拟托管，那么为这些域名运行本地主 DNS 是非常重要的。你的目标是让新域名的 IP 与主服务器的 IP 相同。同时确保 InterNIC 知道你的域名。

接下来，我们需要让 `httpd` 服务器知道要响应哪些主机以及用哪些文件响应请求。在你的 `httpd.conf` 文件中添加以下行：

```
ServerName www.virtual.com
ServerAlias virtual.com *.virtual.com
DocumentRoot /usr/local/etc/httpd/web/virtual/
...
```

现在你可以在此部分中添加其他变量/指令，以为虚拟主机的使用创建一个 `cgi-bin` 目录。现在，让我们确保所有的浏览器都能访问我们的新站点。将以下内容添加到你的 `httpd.conf` 文件中（位于虚拟主机部分之外），通常在文件的顶部。这将允许我们的站点通过 `http://www.virtual.com` 或 `http://www.virtual.com/virtual/` 查看：

`Alias /virtual /usr/local/etc/httpd/web/virtual/`

在为新主机进行 HTML 编程时创建链接和/或锚点，你可以使用相对链接，或者将 `/virtual/` 作为处理任何内容之前的第一个路径。

这里是 `httpd.conf` 中完整部分的示例：

```
<VirtualHost www.gosmedix.com>
ServerAdmin webmaster@gosmedix.com
DocumentRoot /usr/local/etc/httpd/gosmedix
ServerName www.gosmedix.com
ScriptAlias /cgi-bin/ /usr/local/etc/httpd/cgi-qox
ErrorLog logs/gosmedix-error_log
AddType application/x-httpd-cgi .cgi
TransferLog logs/gosmedix-access_log
</VirtualHost>
```

以下是你需要添加到 `access.conf` 的内容：

```
<Directory /usr/local/etc/httpd/gosmedix>
Options Indexes FollowSymLinks Includes
AllowOverride All
<Limit GET>
order allow,deny
allow from all
</Limit>
</Directory>
```

# Apache 的其他版本

你可以选择编译并安装不同版本的 Apache Web 服务器。总有一个最新版本可能更适合你的需求。如果你想检查是否有新版本，只需将你的 Web 浏览器指向 `http://www.apache.org/` 即可，那里提供了最新版本的下载。Apache 网站上有关于重新编译 Web 服务器的指导。这其实相当简单。

从网上获取 Apache Web 服务器后你可以安装它。首先从下载文件的位置移动文件。

```
cd /cdrom/internet
```

你可以使用以下命令行移动文件：

```
cp apache_1_1.tar /usr/local/etc
```

在这个示例中，我们把文件移动到 `/usr/local/etc`。你可以替换为你自己的位置。

> 注意 如果你直接从 Apache 网站获取源代码，可能会有不同的归包文件名。

然后你将使用 `tar` 命令和适当的选项解压缩文件：

```
tar -xvf apache_1_1.tar
```

`tar` 命令会告诉你它正在做什么（`v` 选项或详细详细的作用），即设置目录和归档文件。它将创建一个名为 `apache_1_1` 的 Apache 主目录。在这个目录中，有一个包含源代码的目录，名为 `/src`。将此目录设置为当前目录。

与大多数 UNIX 软件一样，Apache 使用 Makefile 来配置特定的硬件和软件设置。这意味着你需要编辑一个名为 `Configure` 的文件，使安装特定于 Linux。需要编辑的行并不多。你需要通过如下所示编辑 CC 行来确保你正在使用 GNU C 编译器：

```
CC=gcc
```

你还需要更改。`Configure` 中还有其他你需要更改的内容。

## 第 4 章：设置 Web 服务器

在本章中，你将学习关于然后：

```
configure
make
```

完成这些任务后，你可以继续。附带的 CD-ROM 是最。然而，它将很容易地适应任何的更改。（我们有更多的模块需要适应。）

223

这些阶段有更多的槽位。在大多数情况下，这些是留给服务器核心或另一个组件的，并应谨慎地进行修改。

# 基本概念

我们开始概述 API 背后的基本概念以及它们在代码中是如何体现的

## 处理程序、模块和请求

Apache 将请求处理分为一系列步骤，在某种程度上与 Netscape 服务器的方法相同（尽管此 API 有更多阶段，作为未来的钩子）。这些步骤是：

- URI -> 文件名翻译

- 身份验证（用户是他所声称的吗？）

- 权限检查（用户在此授权了吗？）

- 权限之外的检查

- 确定对象的 MIME 类型

- 修复——目前还没有，但该阶段旨在用于 SetEnv 等无法很好放在其他地方的扩展。

- 实际向客户端发送响应

- 记录请求

这些阶段通过查看一系列模块来处理，查看每个模块是否具有该阶段的处理程序，如果有，则尝试调用。处理程序通常可以执行三件事之一：

- 处理请求并通过返回魔数常量 `OK` 表示已完成。

- 拒绝处理请求，通过返回魔数整数常量 `DECLINED`。在这种情况下，服务器的行为就像该处理程序根本不存在一样。

# Apache API 注意事项

以下内容对想要添加功能的人感兴趣。它摘自 Apache 在线文档。

这些关于 API 以及你必须处理的数据结构的注释。它们远非完整，但可以帮助你了解情况。请记住 API 仍可能发生变化（查看 TODO 文件了解可能发生的内容）。

这里是一些关于通用风格的注意事项。为了简洁起见，这里所有的结构声明都是不完整的——这些

## 第 4 章：设置 Web 服务器

- 通过返回其中一个 HTTP 错误代码来指示错误。这将终止对请求的正常处理，尽管可能会调用 `ErrorDocument` 来尝试清理，但无论如何，错误都会被记录。

大多数阶段都由第一个处理它们的模块终止；然而，对于日志记录、修复（fixups）和非访问身份验证检查，所有处理器始终都会运行（除非发生错误）。此外，响应阶段的独特之处在于，模块可以通过以请求对象的 MIME 类型为键的派发表，为其声明多个处理器。模块可以声明一个可以处理任何请求的响应阶段处理器，只需给它键值 `/*`；然而，通配符处理器只有在服务器已经尝试但未能为请求对象的 MIME 类型 找到更具体的响应处理器（要么是不存在，要么所有处理器都拒绝了）时，才会被调用。

处理器本身是接受一个参数（例如 `request_rec` 结构体）的函数，如前所述，这些函数返回一个整数。

### 模块简览

此时，我们需要解释模块的结构。我们的候选对象将是那些最复杂的模块之一：CGI 模块——它同时处理 CGI 脚本和 `ScriptAlias` 配置文件命令。它实际上比大多数模块都要复杂得多，但如果我们只举一个例子，那么最好就是这个“无处不在手指”的例子。

让我们从处理器开始。为了处理 CGI 脚本，模块为它们声明了响应处理器。由于 `ScriptAlias` 的存在，它还有名称翻译阶段的处理器（用于识别 `ScriptAlias` 过的 URI）和类型检查阶段的处理器（任何 `ScriptAlias` 请求都被类型化为 CGI 脚本）。

模块需要维护一些每个（虚拟）服务器的信息，即生效的 `ScriptAliases`；因此，模块结构体包含指向两个函数的指针：一个用于构建这些结构体的函数，另一个用于合并两个结构体的函数（以防主服务器和虚拟服务器都声明了 `ScriptAliases`）。

最后，该模块还包含用于处理 `ScriptAlias` 命令本身的代码。这个特定的模块只声明了一个命令，但可能还有更多，因此模块拥有命令表来声明它们的命令，并描述它们允许在何处使用以及如何被调用。
