

## 将内容放置到位

将 Apache 需要提供的内容放置在 **/var/www** 目录中。如前所述，Apache 会自动显示此目录中名为 **index.html** 的文件。请执行以下命令来创建这样一个页面，以替换默认页面：

```bash
$ sudo tee /var/www/index.html
<html><body><p>This is <i>my</i> test page.</p></body></html>
CONTROL-D
```

**tee** 实用程序（第 254 页）会将标准输入（第 243 页）复制到你作为参数提供的文件中，同时也复制到标准输出（第 243 页）。由于这种重定向，**tee** 会在你按下 RETURN 键后重复显示你输入的每一行。创建此文件后，你可以刷新浏览器页面（如果它仍在运行中），或者重新启动浏览器并将其指向服务器。浏览器应该会显示你刚刚创建的页面。

## 配置 Apache

本节描述了你可以用于简化工作的配置工具。它还告诉你可以在哪里找到在设置和修改 Apache 服务器时可能需要处理的大多数文件。大多数配置文件位于 **/etc/apache2** 目录层级中。

### 配置工具

本节描述了管理 **/etc/apache2** 层级中部分文件的实用程序。这些实用程序是 **apache2.2-common** 包的一部分，该包在安装 **apache2** 时作为依赖项安装。

- **a2enmod** 和 **a2dismod**
  - **a2enmod**（Apache 2 启用模块）和 **a2dismod**（Apache 2 禁用模块）实用程序用于启用和禁用 Apache 模块。**/etc/apache2/mods-available** 目录包含包含 LoadModule 指令（第 928 页）和本地系统中已安装模块选项的文件。**/etc/apache2/mods-enabled** 目录包含指向 **mods-available** 中文件的符号链接。Apache 通过使用 Include 指令（下一节）将这些链接纳入其配置文件中。**a2enmod** 实用程序在 **mods-enabled** 目录中创建指向 **mods-available** 目录中配置文件的符号链接。它作用于以其参数给出的基名为依据的文件。

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

**a2dismod** 实用程序会移除 **a2enmod** 创建的符号链接。在执行一条或多条这些命令后，必须重新加载 Apache（第 902 页），它们才能生效。

**a2enmod** 和 **a2dismod** 实用程序简化了 Apache 的管理。无需在 **httpd.conf** 或 **apache2.conf** 文件中添加或注释掉 LoadModule 指令，你可以使用这些程序来启用或禁用模块。这种设置允许 APT 或 Synaptic 在安装软件包后，通过 **dpkg** **postinst** 脚本调用 **a2enmod**，然后重新加载 Apache，使得软件包在安装后即可用。

- **a2ensite** 和 **a2dissite**
  - **a2ensite**（Apache 2 启用站点）和 **a2dissite**（Apache 2 禁用站点）实用程序用于启用和禁用 Apache 虚拟主机（第 937 页）。这些命令的工作方式类似于前文所述的模块命令。首先，你在 */etc/apache2/sites-available* 目录中的文件中设计一个虚拟主机。然后，你调用 **a2ensite** 并将站点名称作为参数，以便在 */etc/apache2/sites-enabled* 目录中创建符号链接。**a2dissite** 实用程序会移除该符号链接，从而禁用虚拟主机。

### Include 指令

在 Ubuntu 中，主要配置文件是 */etc/apache2/apache2.conf*。该文件使用 Include 指令（第 927 页）引入其他文件：

```bash
$ grep 'Include' /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*.load
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```

- **apache2.conf**
  - 通常，在配置 Apache 时，你不会对 **apache2.conf** 进行修改；相反，你会修改 Include 指令中指定的文件。你也可以使用上一节中描述的配置工具。这种设置允许 Apache 的更新修改 **apache2.conf**，而不会影响服务器。
  - 当 Apache 读取其配置文件时，如果发现同一指令出现多次，即使在 Include 文件中也是，它也会使用它遇到的最后一个指令所分配的值。
  - 在 **apache2.conf** 文件中，**httpd.conf** 文件的 Include 指令位于设置全局环境的指令之后，其中包括表 26-1 中所示的各种超时和限制。若要更改这些指令中的任意一个，请将其复制到 **httpd.conf** 中并在那里进行修改。你必须在本节中解释的其他 Include 文件中更改位于 **httpd.conf** Include 指令之后的那些指令。

*/etc/apache2/conf.d* 的 Include 指令（它包含该目录中的所有文件）位于 **httpd.conf** 的 Include 指令之后，中间只隔了几行以及 */etc/apache2/ports.conf* 的 Include 指令。该目录是放置小型配置片段的好地方，或者如果 **httpd.conf** 变得太大，可以将其中的一部分拆分到这里。

### 表 26-1 可以在 **httpd.conf** 中覆盖的指令

| 列 1 | 列 2 |
|---|---|
| AccessFileName | MaxRequestsPerChild |
| DefaultType | MaxSpareThreads |
| ErrorLog | MinSpareThreads |
| Group | PidFile |
| HostnameLookups | ServerRoot |
| KeepAlive | StartServers |
| KeepAliveTimeout | ThreadsPerChild |
| LockFile | Timeout |
| LogLevel | TypesConfig |
| MaxClients | User |
| MaxKeepAliveRequests | |

控制日志格式、索引选项、MIME 处理以及浏览器 Bug 处理的指令位于 **httpd.conf** 的 Include 指令之后，但位于 /etc/apache2/sites-enabled 的 Include 指令之前，后者是 **apache2.conf** 的最后一行。你可以通过将这些指令复制到 sites-enabled 目录中的各个站点文件中并在那里进行修改，来按站点覆盖这些指令。

如果你管理多个 Ubuntu Web 服务器，最好将所有自定义配置代码与主配置分开。这样，你可以使用 scp 将文件复制到每个新服务器上。或者，你可以将自定义代码放在版本控制系统中，并将其签出以配置新系统。与使用 diff 查找系统之间更改了什么相比，这种技术要容易得多。

## 文件系统布局

本节列出了你在配置 Apache 和提供 Web 页面时将要处理的文件的位置和用途。

Apache 服务器及相关二进制文件保存在几个目录中：

- **/usr/sbin/apache2**—Apache 服务器（守护进程）。
- **/usr/sbin/apache2ctl**—启动和停止 Apache。apache2 初始化脚本会调用 apache2ctl。
- **/usr/bin/htpasswd**—创建和维护 Apache 身份验证模块（第 945 页）使用的密码文件。
- **/usr/sbin/rotatelogs**—轮换 Apache 日志文件，以免这些文件变得过大。有关轮换日志文件的信息，请参阅 logrotate（第 622 页）。
- **/etc/apache2/mods-available**—保存包含各自模块 LoadModule 指令（第 928 页）的文件。alias.conf 文件保存在此目录中并默认启用。两个最常用的模块二进制文件是 `mod_perl`（属于 `libapache2-mod-perl2` 包）和 `mod_python`（属于 `libapache2-mod-python` 元包）。此目录中的 `*.load` 文件从 `/usr/lib/apache2/modules` 目录（第 941 页）加载模块。`*.conf` 文件用于配置模块的使用。有关使用 `a2enmod` 启用模块的信息，请参阅第 905 页。
- **/etc/apache2/mods-enabled**—保存指向 `mods-available` 中文件的链接。使用 `a2enmod` 创建链接，使用 `a2dismod` 移除链接（第 905 页）。

Apache 配置文件保存在 `/etc/apache2` 层级中：

- **/etc/apache2/apache2.conf**—保存配置指令。此文件是主要的 Apache 配置文件。通常你不会对修改此文件，而是将任何配置指令放入 `httpd.conf` 和其他文件中。
- **/etc/apache2/envvars**—保存修改 Apache 运行环境的变量。
- **/etc/apache2/ports.conf**—保存 `Listen` 指令（第 910 页），该指令控制 Apache 监听的 IP 地址和端口。
- **/etc/apache2/sites-available**—保存包含描述虚拟主机代码的文件。有关使用 `a2ensite` 启用站点的信息，请参阅第 906 页。
- **/etc/apache2/sites-enabled**—保存指向 `sites-available` 中文件的链接。使用 `a2ensite` 创建链接，使用 `a2dissite` 移除链接（第 906 页）。
- **/etc/apache2/httpd.conf**—保存本地配置指令。此文件扩充了同一目录中的 `apache2.conf` 文件。关于配置指令的讨论从第 909 页开始。
- **/etc/apache2/conf.d**—保存配置文件。

日志保存在 `/var/log/apache2` 中：

- **/var/log/apache2/access_log**—记录发送到服务器的请求。
- **/var/log/apache2/error_log**—记录请求和运行时服务器错误。

Web 文档（包括客户端浏览器显示的 Web 页面）、自定义错误消息和 CGI 脚本默认保存在 `/var/www` 中：

- **/usr/lib/cgi-bin**—保存 CGI 脚本（第 942 页）。此目录别名为 `/cgi-bin/`。
- **/usr/share/apache2/error**—保存默认错误文档。你可以修改这些文档以符合你的 Web 站点风格。此目录别名为 `/error/`。参见 `ErrorDocument`（第 924 页）。
- **/usr/share/apache2/icons**—保存用于显示目录条目的图标。此目录别名为 `/icons/`。
- **/usr/share/doc/apache2-doc/manual/index.html**—*Apache HTTP Server Version 2.2 Documentation*。在 Apache 运行且安装了 `apache2-doc` 的情况下，将

