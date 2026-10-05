

# 将你的内容放置就位

将 Apache 自动显示的内容放置在 `/var/www` 中。如前所示，Apache 会自动显示此目录中名为 `index.html` 的文件。执行以下命令来创建一个页面以替换默认页面：

```
$ sudo tee /var/www/index.html
<html><body>This is <my> test page.</p></body></html>
<html><body>This is <my> test page.</p></body></html>
```

## 控制

tee 实用（第 254 页）将输入复制到你作为参数提供的文件中以及标准输出（第 243 页）。由于这种重定向，在你按下回车键后，tee 会重复你插入每行内容。创建完成后后，在浏览器中刷新页面（如果它仍在运行）或重新启动它并指向服务器。浏览器应该显示你创建的页面。

# 配置 Apache

本节介绍了你可以用来简化工作的配置工具。它还告诉了你可以在设置和修改 Apache 服务器时，可以在何处找到许多需要的文件。大多数配置文件位于 `/etc/apache2` 层次结构中。

# 配置工具

本节介绍了管理 `/etc/apache2` 层次结构中某些文件的实用程序。这些工具是 `apache22-common` 包的一部分，在安装 apache2 时作为依赖项安装。

`a2mod`（Apache 2 启用模块）和 `a2dismod`（Apache 2 禁用模块）用于启用和禁用 Apache 模块。`/etc/apache2/mods-available` 目录包含 `LoadModule` 指令（第 928 页）以及本地系统上安装模块的选项。`/etc/apache2/mods-enabled` 目录通过包含（下一节）将符号链接引入到其配置中。Apache 在 `mods-available` 中整合这些链接。`a2mod` 实用程序从 `available` 目录在 `mods-enabled` 目录中创建链接。它对基名为参数的文件进行操作。

```
$ sudo -1
# cd /etc/apache2
# ln -s mods-available/userdir*
mods-available/userdir.conf mods-available/userdir.load
# ln -s mods-enabled/userdir*
ls: mods-enabled/userdir: No such file or directory
# a2mod userdir
Enabling module userdir.
Run '/etc/init.d/apache2 restart' to activate new configuration!
# ls mods-enabled/userdir*
mods-enabled/userdir.conf mods-enabled/userdir.load
# exit $
```

# 第 26 章 Apache：设置 Web 服务器

`a2dis` 实用程序删除 `a2enmod` 创建的符号链接。在应用这些一个或多个更改后，你必须重新加载 Apache（902 页），更改才会生效。

`a2enmod` 和 `a2dis` 实用程序简化了 Apache 管理。与其在 `httpd.conf` 或 `apache2.conf` 中添加或注释掉 `LoadModule` 指令，你可以使用这些程序来启用或禁用模块。这种设置允许 APT 或 Synaptic 在安装包后，通过 `dpkg` 后置脚本调用 `a2enmod`，然后重新加载 Apache，以便更改在安装后立即生效。

`a2ensite`（Apache 2 启用站点）和 `a2dissite`（Apache 2 站点禁用）实用程序用于启用和禁用 Apache 虚拟主机（第 937 页）。这些命令的描述与之前类似。首先在 `/etc/apache2/sites-available` 目录中设计虚拟主机文件。然后用站点名称作为参数调用 `a2ensite`，在 `/etc/apache2/sites-enabled` 目录中创建一个符号链接。`a2dissite` 删除符号链接以禁用虚拟主机。

# Include指令

在 Ubuntu 下，主配置文件是 `/etc/apache2/apache2.conf`。该文件使用 `Include` 指令（第 927 页）合并其他文件：

```
$ grep '^Include' /etc/apache2/apache2.conf
Include /etc/apache2/mods-enabled/*..load
Include /etc/apache2/mods-enabled/*.conf
Include /etc/apache2/httpd.conf
Include /etc/apache2/ports.conf
Include /etc/apache2/conf.d/
Include /etc/apache2/sites-enabled/
```

`apache2.conf` 通常情况下，当你配置 Apache 时，你不对 `apache2.conf` 更改；而是使用 `Include` 指令。你还可以使用上一节描述的配置工具。这种设置允许 Apache 的更新更改 `apache2.conf` 而不影响服务器。

当 Apache 读取其配置文件时，如果在 `Include` 文件中发现多次指令多次，它将使用最后遇到的指令所分配的值。

在 `apache2.conf` 中，针对 `httpd.conf` 的 `Include` 指令出现在设置全局环境的指令之后，其中包含了各种超时和限制，如表 26-1 所示。要更改这些任何指令，请将其复制到 `httpd.conf` 并进行更改。正如本节所解释的，你必须更改其他包含文件中出现在 `Include httpd.conf` 指令之后的指令。

针对 `/etc/apache2/conf.d` 的 `Include` 指令（它包含该目录下的所有文件）出现在 `httpd.conf` 的 `Include` 指令之后，中间仅隔了少数行以及针对 `/etc/apache2/ports.conf` 的 `Include` 指令。该目录是存放小型配置片段的好地方，或者当 `httpd.conf` 变得太大时将其部分拆分。

# 表 26-1 你可以覆盖的指令

| AccessFileName | MaxRequestsChild |
| :--- | :--- |
| DefaultType | MaxSpareThreads |
| ErrorLog | MinSpareThreads |
| Hostname | Pid |
| KeepAlive | StartServers |
| KeepAliveTimeout | ThreadsPerChild |
| LockFile | Timeout |
| LogLevel | Types |
| MaxAliveRequests | User |

控制格式、索引、MIME 处理的指令出现在 `/etc/apache2/sites-enabled` 的 `Include` 指令之后。如果你管理多个站点，将自定义代码分开是好的。你可以使用 `diff` 查看更改。

# 文件布局

本节列出了 Apache 使用的二进制文件、脚本和模块的位置：

- /etc/apache2/: 配置文件
- /usr/sbin/apache2: 启动和停止 Apache
- /usr/sbin/apachectl: 控制 Apache
- /usr/sbin/rotatelogs: 滚动日志文件
- /etc/apache2/mods-available: 包含 `LoadModule` 指令的文件（第 928 页）
- /etc/apache2/mods-enabled: 指 `mods-available` 的链接
- /etc/apache2/apache2.conf: 主配置文件
- /etc/apache2/envvars: 保存修改环境的变量
- /etc/apache2/ports.conf: 包含 `Listen` 指令（第 910 页）
- /etc/apache2/sites-available: 包含虚拟主机的文件
- /etc/apache2/sites-enabled: 指 `sites-available` 的链接
- /etc/apache2/httpd.conf: 本地配置指令
- /etc/apache2/conf.d: 配置文件
- /var/log/apache2/access_log: 记录对服务器的请求
- /var/log/apache2/error_log: 记录请求和运行时服务器错误
- /var/www/: CGI 脚本默认路径
- /usr/lib/cgi-bin: 包含 CGI 脚本（第 942 页）
- /usr/share/apache2/error: 错误错误
- /usr/share/apache2/icons: 用于显示目录条目的图标

并且默认启用。两个最常用的模块是 `mod_perl`（属于 `apache2-mod-perl`）和 `mod_python`（属于 `apache2-mod-python` 元软件包）。位于 `/usr/apache2/modules`（第 941 页）的加载文件配置这些模块。参阅第 905 页有关使用 `a2mod` 启用模块的信息。

