
此显示表示有五个守护进程，目前没有一个处于活跃状态。`s` 表示进程正在睡眠。其他可能的状态字母是活跃 (`r`)、正在启动 (`t`) 或死亡 (` `)。在示例中，所有进程都处于睡眠状态。

更好的监控器是 `server-status` 监控器。要使用此监控器，它必须被编译到 `httpd` 中，或者被安装为动态加载模块。Red Hat `httpd.conf` 配置文件中的这两行安装了可加载模块：

```apache
LoadModule status_monitor      modules/mod_status.so
...
AddModule mod_status.c
```

为了从 `server-status` 显示获取尽可能的信息，请向你的 `httpd.conf` 文件添加 `ExtendedStatus` 选项。例如：

```apache
ExtendedStatus on
```

通过插入 `Location /server-status` 部分来启用 `srm.conf` 文件的监控。例如：

```apache
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from foobirds.org
</Location>
```

## 管理你的 Web 服务器 271

使用身份验证数据库可以提供非常显著的性能提升。如果你有大型网站，请务必使用此功能。

## 设置文档级访问控制

`Location` 指令用于提供文档层面的访问控制。它的用法与 `Directory` 标签一样，但命令行上使用的不是目录名，`Location` 标签在命令行上是来自 URL 的文档名：

```apache
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from foobirds.org
</Location>
```

如果 Apache 服务器接收到 `www.foobirds.org/server-status` 的请求，它将应用这些访问控制。`/server-status` 是文档名，而不是目录名。事实上，这是一个显示服务器状态的特殊文档，由一个特殊的处理器构建。这些访问控制使得服务器状态对我们域内的所有人都可用，但拒绝所有外部人员访问。在下一节中，你将看到如何使用 `server-status` 页面来监控你的 Web 服务器。

## 管理你的 Web 服务器

尽管三个配置文件文件中存在大量的选项，但在运行 Web 服务器时，配置并不是你承担的最主要任务。当服务器首次安装时，配置通常只需要调整几个配置选项。

另一方面，监控服务器的使用情况和性能并确保其可靠性和安全性是日常任务。但请不要担心——Apache 服务器提供了一些工具来简化这些任务。

![](img/0a4925a63d7144788f84b23689a2d0da_296_0.png)

## 监控你的服务器

Apache 提供了监控服务器状态的工具以及日志，这些日志记录了系统随时间推移的使用和性能历史。你已经在我们对配置文件的讨论中见过关于这些内容了。其中之一就是 ScoreBoard 文件。

当 Apache 启动时，它会创建几个持久的守护进程。当需求较高时，额外的守护进程会被添加到守护进程群中。当需求较低时，额外的守护进程会被杀死。守护进程的状态被写入 `scoreboard` 文件，并可以使用 `httpd_monitor` 命令查看。

`httpd_monitor` 包含在 Apache 分发版中。如果你使用的是 Linux 发行版附带的 Apache 软件，它可能不包含此程序。如果没有，你可以在 `www.apache.org` 上的 Apache 发布版本的支持子目录中找到它。运行 `httpd_monitor` 会显示 `scoreboard` 文件的内容：

```bash
# httpd_monitor
ssss (0/5)
```

此显示表示有五个守护进程，目前没有一个处于活跃状态。`s` 表示进程正在睡眠。其他可能的状态字母是活跃 (`r`)、正在启动 (`t`) 或死亡 (` `)。在示例中，所有进程都处于睡眠状态。

更好的监控器是 `server-status` 监控器。要使用此监控器，它必须被编译到 `httpd` 中，或者被安装为动态加载模块。Red Hat `httpd.conf` 配置文件中的这两行安装了可加载模块：

```apache
LoadModule status_monitor      modules/mod_status.so
...
AddModule mod_status.c
```

为了从 `server-status` 显示获取尽可能的信息，请向你的 `httpd.conf` 文件添加 `ExtendedStatus` 选项。例如：

```apache
ExtendedStatus on
```

通过插入 `Location /server-status` 部分来启用 `srm.conf` 文件的监控。例如：

```apache
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from foobirds.org
</Location>
```

## 管理你的 Web 服务器

使用身份验证数据库可以提供非常显著的性能提升。如果你有大型网站，请务必使用此功能。

## 设置文档级访问控制

`Location` 指令用于提供文档层面的访问控制。它的用法与 `Directory` 标签一样，但命令行上使用的不是目录名，`Location` 标签在命令行上是来自 URL 的文档名：

```apache
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from foobirds.org
</Location>
```

如果 Apache 服务器接收到 `www.foobirds.org/server-status` 的请求，它将应用这些访问控制。`/server-status` 是文档名，而不是目录名。事实上，这是一个显示服务器状态的特殊文档，由一个特殊的处理器构建。这些访问控制使得服务器状态对我们域内的所有人都可用，但拒绝所有外部人员访问。在下一节中，你将看到如何使用 `server-status` 页面来监控你的 Web 服务器。

## 管理你的 Web 服务器

尽管三个配置文件文件中存在大量的选项，但在运行 Web 服务器时，配置并不是你承担的最主要任务。当服务器首次安装时，配置通常只需要调整几个配置选项。

另一方面，监控服务器的使用情况和性能并确保其可靠性和安全性是日常任务。但请不要担心——Apache 服务器提供了一些工具来简化这些任务。

![](img/0a4925a63d7144788f84b23689a2d0da_296_0.png)

## 监控你的服务器

Apache 提供了监控服务器状态的工具以及日志，这些日志记录了系统随时间推移的使用和性能历史。你已经在我们对配置文件的讨论中见过关于这些内容了。其中之一就是 ScoreBoard 文件。

当 Apache 启动时，它会创建几个持久的守护进程。当需求较高时，额外的守护进程会被添加到守护进程群中。当需求较低时，额外的守护进程会被杀死。守护进程的状态被写入 `scoreboard` 文件，并可以使用 `httpd_monitor` 命令查看。

`httpd_monitor` 包含在 Apache 分发版中。如果你使用的是 Linux 发行版附带的 Apache 软件，它可能不包含此程序。如果没有，你可以在 `www.apache.org` 上的 Apache 发布版本的支持子目录中找到它。运行 `httpd_monitor` 会显示 `scoreboard` 文件的内容：

```bash
# httpd_monitor
ssss (0/5)
```

此显示表示有五个守护进程，目前没有一个处于活跃状态。`s` 表示进程正在睡眠。其他可能的状态字母是活跃 (`r`)、正在启动 (`t`) 或死亡 (` `)。在示例中，所有进程都处于睡眠状态。

更好的监控器是 `server-status` 监控器。要使用此监控器，它必须被编译到 `httpd` 中，或者被安装为动态加载模块。Red Hat `httpd.conf` 配置文件中的这两行安装了可加载模块：

```apache
LoadModule status_monitor      modules/mod_status.so
...
AddModule mod_status.c
```

为了从 `server-status` 显示获取尽可能的信息，请向你的 `httpd.conf` 文件添加 `ExtendedStatus` 选项。例如：

```apache
ExtendedStatus on
```

通过插入 `Location /server-status` 部分来启用 `srm.conf` 文件的监控。例如：

```apache
<Location /server-status>
SetHandler server-status
order deny,allow
deny from all
allow from foobirds.org
</Location>
```

- `304`: 未修改 (Not Modified) 请求的文档未修改。
- `400`: 请求错误 (Bad Request) 请求无效。
