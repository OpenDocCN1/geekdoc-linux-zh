
最重要的是，我们需要添加新行 `SetOptions UserGroup scripter-user`——这确定了拥有虚拟主机文件的用户，正如我们之前讨论过的，脚本将以哪个组运行。在我们准备测试之前，只剩下一项需要配置了！

```apache
## /etc/apache2/sites-enabled/000-default.conf
<VirtualHost *:80>
  ServerName localhost
  DocumentRoot /var/www/html
  ScriptAlias /cgi-bin/ /home/user/scripts/
  Options +ExecCGI
  SetOptions UserGroup scripter-user
</VirtualHost>
```

## 14 设置 SuExec 目录

记得在教程中，我们在讨论安装自定义版本的 SuExec 以及我们如何使用自定义虚拟目录吗？编辑 SuExec 配置文件 `/etc/apache2/suexec/www-data` 并添加行 `/home/user/scripts/`。现在我们将脚本的子目录视为运行 CGI 的有效位置。

## 15 重启 Apache

记得在教程中，我们正在讨论安装自定义版本的 SuExec 以及我们如何使用自定义虚拟目录吗？编辑 SuExec 配置文件 `/etc/apache2/suexec/www-data` 并添加行 `/home/user/scripts/`。现在我们将脚本的子目录视为运行 CGI 的有效位置。

## 16 SuExec 与环境

记得在教程中，我们正在讨论安装自定义版本的 SuExec 以及我们如何使用自定义虚拟目录吗？编辑 SuExec 配置文件 `/etc/apache2/suexec/www-data` 并添加行 `/home/user/scripts/`。现在我们将脚本的子目录视为运行 CGI 的有效位置。

## 17 SuExec 与变量

记得在教程中，我们正在讨论安装自定义版本的 SuExec 以及我们如何使用自定义虚拟目录吗？编辑 SuExec 配置文件 `/etc/apache2/suexec/www-data` 并添加行 `/home/user/scripts/`。现在我们将脚本的子目录视为运行 CGI 的有效位置。

## 18 故障排除

我们能向网络应用程序开发人员提供的最佳建议是，在执行任务之前了解理论，以及如何编写使用 `TCP` 的软件。`SSH` 生成的加密流量在没有完美网络应用程序的情况下无法解密。记住，没有 `TCP` 就没有互联网，在创建网络应用程序时要小心。

## Erlang 教程

Mihalis Tsoukalos 管理员、程序员和数学家。他从 1993 年起就开始编写代码。你可以通过 Twitter `@msoukalos` 或 `mtskalos.eu` 与他联系。

我们的 Erlang 系列将继续介绍创建过程，我们将涵盖网络编程，这主要包括 `TCP/IP` 服务器的开发。

## 资源

最新安装的 Erlang 文本编辑器，如 `Emacs` 或 `vi`

## gen_tcp

`MODULE` `gen_tcp`

### MODULE 摘要

`TCP/IP` sockets 的接口。

### 描述

此模块提供了使用 `TCP/IP` 协议与 sockets 进行通信的函数。

下面的代码片段是客户端连接到 5678 端口服务器并关闭连接的简单示例。

```erlang
client() ->
  {Socket = gen_tcp:connect(binary, packet, 0), % 为了能在一台机器上运行
  {ok, Bin} = gen_tcp:connect(socket, "localhost", 5678, "Data"),
  {ok, Connection} = gen_tcp:open(Bin)}
```

在另一端，监听 5678 端口的服务器接受连接并返回二进制数据：

```erlang
server() ->
  {ok, Socket} = gen_tcp:accept(5678, active),
  {ok, Bin} = gen_tcp:recv(Socket, B),
  {ok, List} = list_to_binary(Bin)}
```

更多示例请参见 `Examples`（示例）章节。

![](img/a6a91935f07f13d62210d3016f91c5fc_46_0.png)

### MODULE

`MODULE` 摘要

访问 `TCP/IP` 协议。

### 描述

此模块提供了对 `TCP/IP` 协议的访问。

另见 `inet:configuration` 获取更多关于如何配置 Erlang 运行时系统和使用通信的信息。

以下两个 `TCP` 连接参数会影响开放 Erlang 节点上所有 sockets 的行为：

- `inet_connect_options`：当节点关闭时返回时，它包含所有 sockets 的选项列表。
- `inet_listen_options`：包含在调用监听 socket 时使用的选项列表。

当使用 `accept` 时，监听 socket 选项的值会被继承。没有此类的应用程序变量。

### 有用的 Erlang 包

有三个 Erlang 包可以帮助我们在 Erlang 中开发网络应用：`gen_tcp`、`gen_udp`。这两个包提供了低级功能，而第三个包允许我们创建任何原始的 `TCP/IP` sockets。
