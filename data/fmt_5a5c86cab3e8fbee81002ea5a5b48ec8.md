
`username = mike`

`password = secret`

标准新闻服务器使用端口 `119` 来接收请求进行通信。如果您连接的新闻服务器使用其他端口，您可以使用 `port` 参数告诉 leafnode——例如，`port = 9020`。

您可以使用 `supplement` 参数为 leafnode 定义另一个与第一个一起使用的新闻服务器。此参数最常见的用途是当一个新闻服务器托管了另一个服务器上找不到的新闻组时。在此参数后跟随 `username` 和 `password` 参数，如果您的补充服务器需要它们。您可以通过为每个服务器定义一个 `supplement`、`username` 和 `password` 块来输入多个补充服务器。

如果某个补充服务器的连接很慢，您可以在 `supplement` 参数后立即使用 `timeout` 参数告诉 leafnode 给它更多时间。`timeout` 参数的值为等待的秒数。

您可以使用 `groupexpire` 参数定义新闻组过期时间——例如，如果某个特定新闻组非常有趣，您希望比其他组更长时间地保留其文章。此参数采用新闻组名称，后跟保留文章在您机器上的天数作为值。以下是一个示例：

```
groupexpire comp.os.linux =
```

您可以使用 `maxfetch` 参数控制 leafnode 从一个新闻组获取多少篇文章。这很有用，因为某些新闻组有数百篇文章。该参数的值为一次运行要获取的文章数。在此处输入低于 `1,000` 的数字是不推荐的。

当您订阅一个新闻组时，您可以告诉 leafnode 第一次只获取几篇文章。这将让您了解该组的大致内容，以便您决定是否获取所有文章。为此，请使用 `initialfetch` 参数，并以要获取的初始文章数作为值。

通常，您不会阅读 leafnode 为您获取的所有文章。因此，您可以通过告诉 leafnode 只下载文章头来节省带宽。然后，当您想要一篇文章时，leafnode 将为您获取正文。这是通过将 `delaybody` 参数设置为 `1` 来完成的。

您可以使用 `maxage` 参数告诉 leafnode 不要获取旧文章。如果您以天数为单位给出一个值，则任何比该天数更旧的文章都不会被获取。

这些是 leafnode 最常见和有趣的参数。然而，您必须配置的唯一参数是 `server` 和 `expire` 参数。其余的都可以保留为默认值。

## 运行 leafnode

最后一步是运行 leafnode。首先必须做的是告诉您的 SuSE Linux 在新闻客户端连接到您的机器时始终运行 leafnode。您需要手动编辑 `/etc/inetd.conf`。

使用您喜欢的编辑器打开 `/etc/inetd.conf`。请注意，您必须以 root 身份登录才能编辑该文件。找到以下行：

```
# nntp stream tcp nowait news /usr/sbin/tcpd /usr/sbin/leafnode
```

要启用 leafnode，请删除该行开头的井号（`#`）：

```
nntp stream tcp nowait news /usr/sbin/tcpd /usr/sbin/leafnode
```

保存文件并退出。要告诉 inetd 守护进程重新读取其配置文件，请以 root 身份运行以下命令：

```
# rcinetd restart
```

要测试您的配置，请在端口 `119` 上执行 telnet，如下所示：

```
$ telnet localhost 119
Trying 0.0.0.0...
Connected to 0.
Escape character is '^]'.
200 Leafnode NNTP Daemon, version 1.9.4 running at Shadow.nazeeh.com
```

好了！您的安装成功了；leafnode 回答了您的连接请求。只需输入 `quit` 即可退出此测试。

为了真正完成您的安装，您应该编辑文件 `/etc/crontab`，以确保文章过期程序将被安排由您的系统定期运行。

使用您喜欢的编辑器打开 `/etc/crontab`。同样，您必须以 root 身份才能编辑此文件。找到以下行：

```
#5 22 * * * root test -x /usr/sbin/texpire && /usr/sbin/texpire
```

删除前导井号（`#`）以启用您的系统调度程序处理此条目：

```
5 22 * * * root test -x /usr/sbin/texpire && /usr/sbin/texpire
```

现在您已经完全配置并安装了 leafnode，是时候运行它了。每次您希望 leafnode 从您的新闻服务器获取最新文章并将其保存在您的机器本地时，都必须以 root 身份运行命令 `fetchnews`。

此命令必须在您第一次运行 leafnode 时运行。如果您使用拨号连接，请连接到 Internet 并以 root 身份运行 `fetchnews`：

```
# fetchnews
```
