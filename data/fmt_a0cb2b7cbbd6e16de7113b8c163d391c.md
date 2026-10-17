
- **术语：服务器和进程**：Apache **服务器** 与 Apache **进程** 是同一个概念。Apache 子进程用于处理传入的客户端请求；因此被称为服务器。

- **防火墙**：Apache 服务器通常使用 `TCP 80` 端口；安全服务器使用 `TCP 443` 端口。如果 Apache 服务器系统正在运行或位于防火墙之后，你必须打开这些端口中的一个或两个。为了开始，请打开 `80` 端口（`HTTP`）。使用 `guvw`（第 876 页），通过设置允许 `HTTP` 和/或 `HTTPS` 服务的策略来打开这些端口。

- **以 root 权限运行**：由于 Apache 在特权端口上提供服务，因此必须以 `root` 权限启动它。出于安全原因，Ubuntu 设置 Apache 生成以用户和组 `www-data` 运行的进程。

- **区域设置**：`apache2` 守护进程默认使用 `C` 区域设置启动。你可以修改此行为——例如，使用配置的系统区域设置——通过在 `/etc/init.d/apache2` 文件中设置 `LANG` 变量（在以 `ENV="env -i LANG=C ..."` 开头的行中）。

Apache 提供内容的目录层级的根目录称为*文档根*，由 `DocumentRoot` 指令控制（第 913 页）。该指令定义了服务器上的一个目录，映射到 `/`。对于浏览网站的用户来说，这个目录表现为根目录。在 Ubuntu 的发行版中，文档根是 `/var/www`。

在 Ubuntu 默认的 Apache 配置中，只有拥有*root*权限（使用 `sudo`）的用户才能添加或修改 `/var/www` 中的内容。为了避免人们在操作内容时以*root*身份工作，请创建一个组（例如 `webwork`），将需要处理 Web 内容的人员放入该组，并创建从 `/var/www`（或其他文档根）开始的目录层级，使该组可写。此外，如果你给目录层级设置 `setgid` 权限，那么在此层级内创建的所有新文件都将属于该组，这将有助于文件共享。下面前三个命令添加了新组，将文档根的权限更改为 `setgid`，并更改文档根所属的组。最后一个命令将 `username` 添加到 `webwork` 组；你需要为想要添加到该组的每个用户重复执行此命令。

```bash
$ sudo addgroup webwork
$ sudo chmod g+s /var/www
$ sudo chown :webwork /var/www
$ sudo usermod -aG webwork username
```

有关使用组的更多信息，请参见第 597 页。

Ubuntu 运行 Apache 版本 2.2。

## 运行 Web 服务器（APACHE）

本节介绍了如何安装、测试和配置基本的 Web 服务器。

## 前提条件

安装以下软件包：

- `apache2`

安装 `apache2` 软件包时，`dpkg` `postinst` 脚本将启动 `apache2` 守护进程。配置好 Apache 后，调用 `apache2` 初始化脚本来重启 `apache2` 守护进程：

```bash
$ sudo service apache2 restart
```

在活动的服务器上更改 Apache 配置后，使用 `reload` 代替 `restart` 来重新加载 Apache 配置文件，而不会干扰连接到服务器的客户端。

`mod_ssl` 软件包作为 `apache2` 软件包的一部分安装——你无需单独安装它。你可能希望安装以下可选软件包：

- `apache2-doc`——Apache 手册
- `webalizer`——Web 服务器日志分析器（第 948 页）
- `awstats`——Web 服务器日志分析器
- `libapache2-mod-perl2`——嵌入式 Perl 脚本语言（`mod_perl`）
- `libapache2-mod-python`——安装嵌入式 Python 脚本语言（`mod_python`）的元软件包
- `libapache2-mod-php5`——嵌入式 PHP 脚本语言，包括 `IMAP` 和 `LDAP` 支持（`mod_php`）
- `mrtg`——`MRTG` 流量监控器（第 948 页）

## apache2ctl 实用程序和优雅地重启 Apache

**提示：** `apache2` 初始化脚本调用 `apache2ctl` 来启动和停止 Apache。`reload` 参数调用该实用程序并传入 `graceful` 参数，这不会干扰连接到服务器的客户端。`restart` 和 `force-reload` 参数则以 `stop` 和 `start` 参数调用它；这对命令在重启之前完全关闭服务器。

## JUMPSTART：让 Apache 运行起来

要让 Apache 运行起来，请按照本节描述修改 `/etc/apache2/sites-available/default` 配置文件。第 910 页的“指令 I：你开始时可能需要修改的指令”更详细地解释了这个文件，并探讨了你想要对其进行的其他更改。

## 修改配置文件

Apache 按安装状态运行，但向 `/etc/apache2/sites-available/default` 配置文件添加本节描述的三行是一个好主意。如果你不添加这些行，Apache 将分配可能不适合你的值。修改此文件后，你必须重启 Apache（第 902 页）。

`ServerName` 行用于建立服务器名称。向 `/etc/apache2/sites-available/default` 添加以下其中一行，将服务器名称设置为服务器的域名，或者如果你没有域名，则设置为服务器的 IP 地址。将此行添加到文件顶部附近的 `ServerAdmin` 行下方。

```apache
ServerName example.com
```

或者

```apache
ServerName IP_address
```

其中 `example.com` 是服务器的域名，`IP_address` 是服务器的 IP 地址。如果你未连接到网络，可以使用 `localhost` 地址 `127.0.0.1`，以便启动服务器并对其进行实验。有关 `ServerName` 指令的更多信息，请参见第 934 页。

当客户端从服务器获取信息时遇到麻烦，服务器通常会显示一个标识问题的错误页面。例如，当 Apache 找不到请求的页面时，它会显示一个写着 **Error 404: Not Found** 的页面。每个错误页面都可以包含一个 `mailto:` 链接，用户可以点击该链接向服务器管理员发送邮件。`ServerSignature` 指令可以指定你希望在错误页面上显示电子邮件链接。此链接在浏览器中显示为用户调用的域名。`ServerAdmin` 指令指定当用户点击错误页面上的链接时，服务器发送邮件的电子邮件地址。将这两行添加到名为 `default` 的文件中。

在 `ServerAdmin` 指令后添加这两个指令。

```apache
ServerAdmin email_address
ServerSignature Email
```

其中 `email_address` 是需要在人们使用服务器遇到麻烦时得知情况的人的电子邮件地址。确保有人经常检查此电子邮件账户。但也要参见第 912 页上的提示“`ServerAdmin` 吸引垃圾邮件”。

如果你使用角色别名（例如，`webmaster@example.com`）代替具体的用户名（例如 `max@example.com`）作为 `email_address`，可以使系统管理变得更加容易。有关电子邮件别名的讨论，请参见第 722 页。

在更改了名为 `default` 的文件之后，按照第 902 页的说明重启 `apache2`。

## 测试 APACHE

重启 `apache2` 守护进程后，你可以通过将浏览器指向本地（服务器）系统的 `http://localhost/` 来确认 Apache 是否正常工作。从远程系统，将浏览器指向以 `http://` 开头，后接你在上一节中指定的 `ServerName`。如果你正在显示来自非本地系统的页面，本地系统必须知道如何解析你输入的域名（例如，通过 `DNS` 或 `/etc/hosts` 文件）。例如，你可以使用以下任一 URI 格式：`http://192.168.0.16` 或 `http://example.org`。

当你将浏览器指向包含名为 `index.html` 的文件的目录时，Apache 会让浏览器显示该文件的内容（否则它显示目录列表）。响应你的请求，浏览器应该显示存储在服务器 `/var/www/index.html` 上的页面。在这种情况下，浏览器应该显示 It works!

如果服务器位于防火墙之后，请打开 `TCP 80` 端口（第 901 页）。如果你在让 Apache 工作时遇到问题，请参见第 940 页的“故障排除”。

## 将内容放置到位

将 Apache 需要提供的内容放置在 `/var/www` 目录中。如前所述，Apache 会自动显示此目录中名为 `index.html` 的文件。请执行以下命令来创建这样一个页面，以替换默认页面：

```bash
$ sudo tee /var/www/index.html
<html><body><p>This is <i>my</i> test page.</p></body></html>
CONTROL-D
```

`tee` 实用程序（第 254 页）会将标准输入（第 243 页）复制到你作为参数提供的文件中，同时也复制到标准输出（第 243 页）。由于这种重定向，`tee` 会在你按下 `RETURN` 键后重复显示你输入的每一行。创建此文件后，你可以刷新浏览器页面（如果它仍在运行中），或者重新启动浏览器并将其指向服务器。浏览器应该会显示你刚刚创建的页面。

## 配置 Apache

本节描述了你可以用于简化工作的配置工具。它还告诉你可以在哪里找到在设置和修改 Apache 服务器时可能需要处理的大多数文件。大多数配置文件位于 `/etc/apache2` 目录层级中。

### 配置工具

本节描述了管理 `/etc/apache2` 层级中部分文件的实用程序。这些实用程序是 `apache2.2-common` 包的一部分，该包在安装 `apache2` 时作为依赖项安装。

- `a2enmod` 和 `a2dismod`
  - `a2enmod`（Apache 2 启用模块）和 `a2dismod`（Apache 2 禁用模块）实用程序用于启用和禁用 Apache 模块。`/etc/apache2/mods-available` 目录包含包含 `LoadModule` 指令（第 928 页）和本地系统中已安装模块选项的文件。`/etc/apache2/mods-enabled` 目录包含指向 `mods-available` 中文件的符号链接。Apache 通过使用 `Include` 指令（下一节）将这些链接纳入其配置文件中。`a2enmod` 实用程序在 `mods-enabled` 目录中创建指向 `mods-available` 目录中配置文件的符号链接。它作用于以其参数给出的基名为依据的文件。

```bash
$ sudo -i
# cd /etc/apache2
# ls mods-available/userdir*
mods-available/userdir.conf  mods-available/userdir.load
# ls mods-enabled/userdir*
ls: mods-enabled/userdir*: No such file or directory
# a2enmod userdir
Enabling module userdir.
Run '/etc/init.d/apache2 restart' to activate new configuration!
# ls mods-enabled/userdir*
mods-enabled/userdir.conf  mods-enabled/userdir.load
# exit
$ (press ENTER)
```

`a2dismod` 实用程序会移除 `a2enmod` 创建的符号链接。在执行一条或多条这些命令后，必须重新加载 Apache（第 902 页），它们才能生效。

`a2enmod` 和 `a2dismod` 实用程序简化了 Apache 的管理。无需在 `httpd.conf` 或 `apache2.conf` 文件中添加或注释掉 `LoadModule` 指令，你可以使用这些程序来启用或禁用模块。这种设置允许 `APT` 或 `Synaptic` 在安装软件包后，通过 `dpkg` `postinst` 脚本调用 `a2enmod`，然后重新加载 Apache，使得软件包在安装后即可用。

- `a2ensite` 和 `a2dissite`
  - `a2ensite`（Apache 2 启用站点）和 `a2dissite`（Apache 2 禁用站点）实用程序用于启用和禁用 Apache 虚拟主机（第 937 页）。这些命令的工作方式类似于前文所述的模块命令。首先，你在 `/etc/apache2/sites-available` 目录中的文件中设计一个虚拟主机。然后，你调用 `a2ensite` 并将站点名称作为参数，以便在 `/etc/apache2/sites-enabled` 目录中创建符号链接。`a2dissite` 实用程序会移除该符号链接，从而禁用虚拟主机。

### Include 指令

在 Ubuntu 中，主要配置文件是 `/etc/apache2/apache2.conf`。该文件使用 `Include` 指令（第 927 页）引入其他文件：

```bash
$ grep 'Include' /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```

- `apache2.conf`
  - 通常，在配置 Apache 时，你不会修改 `apache2.conf`；相反，你会修改 `Include` 指令中指定的文件。你也可以使用上一节中描述的配置工具。这种设置允许 Apache 的更新修改 `apache2.conf`，而不会影响服务器。
  - 当 Apache 读取其配置文件时，如果发现同一指令出现多次，即使在 `Include` 文件中也是，它也会使用它遇到的最后一个指令所分配的值。
  - 在 `apache2.conf` 文件中，`httpd.conf` 文件的 `Include` 指令位于设置全局环境的指令之后，其中包括表 26-1 中所示的各种超时和限制。若要更改这些指令中的任意一个，请将其复制到 `httpd.conf` 中并在那里进行修改。你必须在本节中解释的其他 `Include` 文件中更改位于 `httpd.conf` `Include` 指令之后的那些指令。

`/etc/apache2/conf.d` 的 `Include` 指令（它包含该目录中的所有文件）位于 `httpd.conf` 的 `Include` 指令之后，中间只隔了几行以及 `/etc/apache2/ports.conf` 的 `Include` 指令。该目录是放置小型配置片段的好地方，或者如果 `httpd.conf` 变得太大，可以将其中的一部分拆分到这里。

### 表 26-1 可以在 `httpd.conf` 中覆盖的指令

| 列 1 | 列 2 |
|---|---|
| `AccessFileName` | `MaxRequestsPerChild` |
| `DefaultType` | `MaxSpareThreads` |
| `ErrorLog` | `MinSpareThreads` |
| `Group` | `PidFile` |
| `HostnameLookups` | `ServerRoot` |
| `KeepAlive` | `StartServers` |
| `KeepAliveTimeout` | `ThreadsPerChild` |
| `LockFile` | `Timeout` |
| `LogLevel` | `TypesConfig` |
| `MaxClients` | `User` |
| `MaxKeepAliveRequests` | |

控制日志格式、索引选项、`MIME` 处理以及浏览器 Bug 处理的指令位于 `httpd.conf` 的 `Include` 指令之后，但位于 `/etc/apache2/sites-enabled` 的 `Include` 指令之前，后者是 `apache2.conf` 的最后一行。你可以通过将这些指令复制到 `sites-enabled` 目录中的各个站点文件中并在那里进行修改，来按站点覆盖这些指令。

如果你管理多个 Ubuntu Web 服务器，最好将所有自定义配置代码与主配置分开。这样，你可以使用 `scp` 将文件复制到每个新服务器上。或者，你可以将自定义代码放在版本控制系统中，并将其签出以配置新系统。与使用 `diff` 查找系统之间更改了什么相比，这种技术要容易得多。

## 文件系统布局

本节列出了你在配置 Apache 和提供 Web 页面时将要处理的文件的位置和用途。

Apache 服务器及相关二进制文件保存在几个目录中：

- `/usr/sbin/apache2`—Apache 服务器（守护进程）。
- `/usr/sbin/apache2ctl`—启动和停止 Apache。`apache2` 初始化脚本会调用 `apache2ctl`。
- `/usr/bin/htpasswd`—创建和维护 Apache 身份验证模块（第 945 页）使用的密码文件。
- `/usr/sbin/rotatelogs`—轮换 Apache 日志文件，以免这些文件变得过大。有关轮换日志文件的信息，请参阅 `logrotate`（第 622 页）。
