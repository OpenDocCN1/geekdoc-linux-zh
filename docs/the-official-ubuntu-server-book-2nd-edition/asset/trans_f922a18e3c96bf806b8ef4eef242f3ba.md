

当然，Ubuntu 甚至提供了简化此操作的工具。要启用一个模块，只需运行 `a2enmod` 然后加上你想要启用的模块名称。要像上面那样启用 CGI 模块，我只需运行

```
$ sudo a2enmod cgi
```

同样，`a2dismod` 程序也可以为你禁用一个模块。它的语法与 `a2enmod` 相同，所以要禁用 CGI，输入

```
$ sudo a2dismod cgi
```

## /etc/apache2/sites-available/

Ubuntu 对 Apache 虚拟主机的组织方式与模块类似。在 Apache 出现之前，市场上的可用 Web 服务器软件只能在一台物理服务器上托管单个站点。Apache 引入了虚拟主机的概念，使其能够在一台物理服务器上托管多个站点。每个虚拟主机可以拥有完全不同的域名和完全不同的文档根目录。在 Ubuntu 下，每个可由 Apache 在本机上提供服务的虚拟主机或站点，其配置都放在 `sites-available` 下的一个单独文件中。默认情况下，该目录中唯一的 文件是恰如其名 的 `default` 文件，它定义了默认虚拟主机，如果没有其他配置，或如果没有其他站点的配置与请求的 主机名 匹配时，该虚拟主机就会显示。

## /etc/apache2/sites-enabled/

与 `mods-enabled` 类似，此目录包含指向 `sites-available` 中配置文件 的符号链接。因此，当你想向 Apache 添加一个新的虚拟主机时，只需在 `sites-available` 下为该主机创建一个新的配置文件，其中包含完整的 `<VirtualHost>` 块，然后在此处创建符号链接：

```
$ sudo ln -s /etc/apache2/sites-available/mysite \
/etc/apache2/sites-enabled/mysite
```

或者你可以使用 `a2ensite` 脚本，它的工作方式与 `a2enmod` 相同。只需运行 `a2ensite` 并将你想要启用的站点作为参数传入。要启用 mysite，我会输入

```
$ sudo a2ensite mysite
```

要禁用它，我可以使用 `a2dissite`：

```
$ sudo a2dissite mysite
```

默认站点是一个特例，它在 `sites-enabled` 下的符号链接前加上 `000`，以确保它最先加载并能作为默认虚拟主机正常工作。

- **/var/www/**
  这是 Apache 的默认文档根目录。任何可被 Apache 读取并放置在此目录中的 HTML 文件，一旦你将 Web 浏览器指向服务器，就会可用。该目录中已有一个默认的 `index.html`。
- **/usr/lib/cgi-bin/**
  这是 CGI 脚本的默认位置。Web 服务器上通过 `/cgi-bin` 引用的任何脚本都将指向此处。
- **/var/log/apache2/**
  这是 Apache 日志存储的标准目录。`access.log` 文件包含有关 Web 服务器上访问了哪些文件的 信息，而 `error.log` 文件列出了任何 Apache 错误。例如，如果你启动 Apache 时遇到问题，请查看 `error.log` 以寻找线索。

## apache2ctl

`/usr/sbin/apache2ctl` 程序是你将在 Ubuntu 下管理 Apache 时主要使用的命令行程序。该命令的语法相当直接。从命令行运行 `apache2ctl` 并将单个命令作为参数传递给它。简单的命令 start、stop 和 restart 将分别启动、停止和重启 Apache 进程。你也可以通过 apache2 初始化脚本实现相同的功能，因此执行相同操作的三个命令是

```
$ sudo apache2ctl restart
$ sudo /etc/init.d/apache2 restart
$ sudo service apache2 restart
```

### 优雅地停止 Apache

restart 和 stop 命令存在潜在风险。当你使用这些命令重启或停止 Apache 时，所有当前运行的 Apache 进程都会被杀掉，即使它们正在为用户提供文件服务。如果你在一个用户正在加载页面的过程中发出重启命令，它只会加载当前已有的信息然后停滞——迫使用户重新加载页面。为避免这种情况，`apache2ctl` 提供了 `graceful` 和 `graceful-stop` 命令。这两个命令分别重启和停止 Apache，但在执行时，它们会先等待每个进程完成任何未完成的请求。在一个活跃的站点上，优雅重启甚至不会被任何使用该服务的人察觉。一般来说，除非你知道站点当前没有提供流量服务，或除非你不在意是否关闭所有活动连接，否则你应该使用 `graceful` 和 `graceful-stop`。唯一的例外是在你为站点添加新的 SSL 证书或进行其他需要完全重启 Apache 才能生效的更改时。

### 诊断 apache2ctl 命令

`apache2ctl` 的其他主要命令提供了更多诊断功能。第一个是 `configtest`，它会测试当前 Apache 配置文件是否存在错误。如果你决定自动化部署 Apache 脚本，这会非常有用。当你设置脚本来部署配置文件并重启 Apache 时面临的一个挑战是，如果你在配置文件中犯了错误，Apache 可能无法重新启动。如果你将同一文件部署到整个 Web 农场，一个语法错误和一个盲目部署并重启 Apache 的脚本就可能导致整个农场瘫痪。使用 `configtest`，你可以在部署脚本中设置逻辑，只有在服务器通过 `configtest` 后才重启 Apache。

随着 Apache 服务器接收流量，你通常希望从中获取诊断信息，例如有多少 Apache 进程处于活动状态，这些进程在做什么，以及你还有多少可用空闲槽。`status` 和 `fullstatus` apache2ctl 命令为你提供了大量优秀的诊断数据。`status` 命令输出 Apache 服务器的通用整体状态，包括服务器已运行多久、活动请求数量以及空闲进程数量，此外还输出所有可用进程的 ASCII 艺术图，不同字母代表不同的进程状态，如图 5-1 所示。`fullstatus` 命令输出类似的信息，只是更多、更详细。

