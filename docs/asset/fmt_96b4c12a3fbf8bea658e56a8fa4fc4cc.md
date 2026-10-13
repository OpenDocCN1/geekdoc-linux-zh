
在大多数系统中，Apache 作为独立服务器安装，持续运行。如第 20 章中关于 init 脚本的讨论所述，您的系统会自动启动 Web 服务器守护进程，每当您启动系统时都会调用它。在 Red Hat 中，名为 `httpd` 的 Web 服务器启动脚本位于 `/etc/rc.d/init.d` 目录中。通过该脚本运行的符号链接位于对应的运行级别目录中。您通常会在运行级别 3 和 5 目录，即 `/etc/rc.d/rc3.d` 和 `/etc/rc.d/rc5.d` 中找到指向 `/etc/rc.d/init.d/httpd` 的 `S85httpd` 链接。您可以使用 `chkconfig` 命令或 System V Init 编辑器来设置 `httpd` 服务器启动的运行级别，并在相应的运行级别目录中创建链接。以下命令将设置 Web 服务器（`httpd`）在运行级别 3 和 5 启动（有关运行级别的更多细节，请参阅第 20 章和第 27 章）。

```
chkconfig --level 35 httpd on
```

在 Red Hat 中，您也可以使用 `service` 命令手动启动和停止 `httpd` 服务器。这在测试或修改服务器时可能很有帮助。带有 `start` 选项的 `httpd` 脚本启动服务器，`stop` 选项停止它，`restart` 选项重启它。直接杀死 Web 进程并不建议这样做。

```
service httpd restart
```

Apache 还提供了一种名为 `apachectl`（Apache 控制）的控制工具来管理您的 Web 服务器。使用 `apachectl`，您可以从命令行启动、停止和重启服务器。`apachectl` 接受几个参数：`start` 用于启动服务器，`stop` 用于停止，`restart` 用于关闭并重启服务器，`graceful` 用于优雅地关闭并重启。此外，您可以使用 `apachectl` 配合 `config` 参数来检查配置文件的语法。您还可以将 `apachectl` 用作 `/etc/rc.d` 目录中服务器的系统启动文件。

请记住，`httpd` 是一个调用实际 `httpd` 守护进程的脚本。您可以使用其完整路径名直接调用守护进程。该守护进程有几个选项。`-d` 选项允许您指定 `httpd` 程序的目录（如果与默认目录不同）。使用 `-f` 选项，您可以指定不同于 `httpd.conf` 的配置文件。`-v` 选项显示版本。

```
/usr/sbin/httpd -v
```

为了检查您的 Web 服务器，请启动您的 Web 浏览器并输入您系统的互联网域名地址。对于系统 `turtle.mytrek.com`，用户输入 `http://turtle.mytrek.com`。这应该显示您放在 Web 根目录中的主页。一个简单的做法是使用 `Lynx`，一个命令行 Web 浏览器。启动 `Lynx`，按 `g` 打开一行，以便输入您自己系统的 URL。`Lynx` 显示您的 Web 站点主页。请务必先在 `/var/www/html` 目录中放置 `index.html` 文件。

一旦服务器运行起来，您可以使用 Apache 也提供的 `ab` 基准测试工具检查其性能。`ab` 显示您的服务器一次能处理多少个请求。选项包括 `-v`，允许您控制显示的详细程度，`-n`，指定要处理的请求数量（默认为 1），以及 `-t`，指定时间限制。

注意 目前不支持在 `xinetd` 下运行 Apache。在 Apache 2.0 中，此类支持由选择专为 `xinetd` 设计的 MP 模块决定。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_507_0.png)

## ABC Amber CHM 转换器试用版

请注册以移除此横幅。

http://www.processestext.com/abchm.html

### Apache 配置文件

配置指令放置在 `httpd.conf` 配置文件中。已记录的 `httpd.conf` 配置文件版本会自动安装在 `/etc/httpd` 中。强烈建议您查阅系统上的此文件。它包含 Apache 指令的详细文档和默认条目。

主配置文件中的任何指令都可以使用位于目录内的 `.htaccess` 文件按目录 basis 覆盖。虽然最初仅设计用于访问指令，但 `.htaccess` 文件也可以保存任何资源指令，使您能够定制特定目录中 Web 页面的显示方式。您可以在 `httpd.conf` 文件中配置对 `.htaccess` 文件的访问。

注意 在 Apache 版本 1.3.4 和 2.0 中，所有配置指令都放置在一个文件中，即 `httpd.conf` 文件。旧版本使用了另外两个文件，即 `srm.conf` 和 `access.conf` 文件。

### Apache 配置和指令

Apache 配置操作以输入到 Apache 配置文件中的指令形式出现。有了这些指令，您可以输入基本配置信息，例如服务器名称，或执行更复杂的操作，例如实现虚拟主机。设计足够灵活，可以让您为特定目录和不同的虚拟主机定义配置功能。Apache 有各种不同的指令，执行的操作多种多样，如控制目录访问、分配文件图标格式和创建日志文件。大多数指令设置诸如 `DocumentRoot` 的值，其中包含服务器网页的根目录，或 `Port`，其中包含服务器在系统上侦听请求的端口。表 23-4 提供了更常用的 Apache 指令列表。简单指令的语法如下所示：

```
directive option option ...
```

某些指令创建能够容纳适用于特定服务器组件的指令的块（也称为区段指令）。例如，`Directory` 指令用于定义一个块，在该块中放置仅适用于特定目录的指令。块指令成对输入：开始指令和终止指令。终止指令定义块的结束，并由以斜杠开头的相同名称组成。块指令采用一个参数，指定指令适用的特定对象。对于 `Directory` 块指令，您必须指定要应用到的目录名称。`<Directory mydir>` 块指令创建一个块，其内部的指令适用于 `mydir` 目录。该块由 `</Directory>` 指令终止。`<VirtualHost hostaddress>` 块指令用于配置特定的虚拟 Web 服务器，必须包含用于该服务器的 IP 或域名地址。`</VirtualHost>` 是其终止指令。您放置在此块内的任何指令都将应用于该虚拟 Web 服务器。`<Limit method>` 指令指定您想要限制的访问方法类型，例如 `GET` 或 `POST`。位于块内的访问控制指令列出了您对这些方法施加的控制。块指令的语法如下：

```
<block-directive option ... >
directive option ...
directive option ...
</block-directive>
```

通常，指令放置在主配置文件之一中。这些文件中的 `Directory` 指令可用于配置特定目录。然而，Apache 也使用基于目录的配置文件。任何目录都可能有自己的 `.htaccess` 文件，其中包含指令仅用于配置该目录。如果您的站点有许多目录，或者任何目录有特殊的配置需求，您可以将它们的配置指令放在它们的 `.htaccess` 文件中，而不是用每个目录的特定 `Directory` 指令填充主配置文件。您可以控制 `.htaccess` 文件中的哪些指令优先于主配置文件中的指令。如果您的站点允许用户或客户端控制的目录，您可能希望仔细监控或禁用其中 `.htaccess` 文件的使用。（除非使用 `AllowOverride` 指令禁用，否则 `.htaccess` 文件中的指令可能会覆盖标准配置文件中的指令。）

Apache Web 服务器的大部分功能和灵活性来自于它使用模块来扩展其功能。Apache 采用一组核心指令实现。可以创建包含其他指令定义的模块。它们可以加载到 Apache 中，使您能够为服务器使用这些指令。Apache 发行版中包含一组标准模块，尽管您可以下载其他模块甚至创建自己的模块。例如，`mod_autoindex` 模块包含自动索引目录的指令（如以下部分所述）。`mod_mime` 模块包含 MIME 类型和处理程序指令。模块通过 `LoadModule` 指令加载。您可以在 `httpd.conf` 配置文件中找到大多数标准模块的 `LoadModule` 指令。

```
LoadModule mime_module modules/mod_mime.so
```

Apache 包提供的 `apxs` 应用程序可用于构建 Apache 扩展模块。使用 `apxs` 应用程序，您可以编译 Apache 模块源代码 C 并创建可通过 `LoadModule` 指令加载的动态共享对象。`apxs` 应用程序要求 `mod_so` 模块是您 Apache 应用程序的一部分。它包括广泛的选项，例如 `-n` 指定模块名称、`-a` 在 `httpd.conf` 文件中为其添加条目，以及 `-i` 在您的 Web 服务器上安装模块。

您可以在 Apache 网站 `http://apache.org` 上以及位于您站点网站根目录中的 Apache 手册中找到完整的 Apache Web 配置指令列表。在许多系统上，它位于发行版设置的网站默认目录中的 `manual` 子目录中（在 Red Hat 上，这是 `/var/www/manual`）。许多更常用的指令列在表 22-4 中。

### 服务器配置
