

它们是自解释的：第一条说，“允许本地计算机通过 HTTP 访问，但拒绝其他所有人。” 这是前面提到的默认规则。现在先保留它，并运行 service squid start 以使用默认设置启动服务器。如果你尚未配置本地网页浏览器使用你的 Squid 服务器，现在就进行配置，以便你可以测试默认规则。

在你的网页浏览器中（从这里开始假设使用 Firefox，但差别不大），访问 URL http://www.ubuntulinux.org。你应该能在浏览器中正常看到它，但在日志窗口中你应该会看到大量信息滚动，因为 Squid 正在为你下载该站点并将其存储在其缓存中。这都是被允许的，因为默认配置允许访问 localhost。

返回配置编辑器窗口，并在最后两条 http_access 行之前添加以下内容：

```
http_access deny localhost
```

因此，最后三行应如下所示：

```
http_access deny localhost
http_access allow localhost
http_access deny all
```

保存文件并退出编辑器。然后，运行以下命令：

```
kill -SIGHUP `cat /var/run/squid.pid`
```

这会查找 Squid 守护进程的进程 ID（PID），然后向其发送 SIGHUP 信号，强制其在运行时重新读取配置文件。你应该会在日志窗口中看到一系列信息，表示 Squid 正在重新读取其配置文件。如果你现在返回 Firefox 并输入新的 URL，你应该会看到 Squid 错误页面，告知你无法访问请求的站点。

你现在被代理阻止的原因是 Squid 按顺序从上到下读取其 ACL 行。如果它找到一条明确允许或拒绝请求的规则，就会停止读取并采取相应操作。因此，在之前的行中，localhost 在第一行被拒绝，然后在第二行被允许。当 Squid 看到 localhost 请求某个站点时，它首先读取 deny 行并立即发送错误页面——甚至不会走到 allow 行。在底部保留一条 deny all 行是强烈推荐的，这样只有你明确允许的才能使用代理。

返回编辑配置文件并删除 deny localhost 和 allow localhost 行。这只留下 deny all，会阻止所有人（包括 localhost）访问代理。现在我们将添加一些条件允许语句：我们只在满足某些条件时才允许 localhost。

定义访问条件是通过 acl 行完成的，因此在 deny all 行上方添加以下内容：

```
acl newsites dstdomain news.bbc.co.uk slashdot.org
http_access allow newsites
```

第一行定义了一个名为 newsites 的访问类别，其中包含一个域名列表（dstdomain）。域名为 news.bbc.co.uk 和 slashdot.org，因此整行读作，“创建一个名为 newsites 的新访问类别，应按域名过滤，并包含列出的两个域名。” 它没有说明应允许还是拒绝该类别的访问；这在下一行中说明。行 http_access allow newsites 的意思是，“允许访问 newsites 类别且无进一步限制。” 它不限于 localhost，这意味着适用于连接到代理服务器的每台计算机。

保存配置文件并重新运行之前的 kill -SIGHUP 行以重启 Squid；然后返回 Firefox 并尝试加载 http://www.ubuntulinux.org。你应该会看到与之前相同的错误，因为它不在我们的 newsites 类别中。现在尝试 http://news.bbc.co.uk，应该可以工作。然而，如果你尝试 http://www.slashdot.org，它将无法工作，你可能还注意到 BBC 新闻网站上的图片也没有出现。这里的问题是指定 slashdot.org 作为网站是具体的：它意味着 http://slashdot.org 可以工作，而 http://www.slashdot.org 则不行。BBC 新闻站点将其图片存储在站点 http://newsimg.bbc.co.uk 上，这就是它们不出现的原因。

返回配置文件，并将 newsites ACL 编辑为以下内容：

```
acl newsites dstdomain .bbc.co.uk .slashdot.org
```

在域名前加上句点（并且在 BBC 的情况下，还去掉 news），意味着 Squid 将允许该站点的任何子域名工作，这通常是你想要的。如果你想要更模糊的匹配，你也可以只指定 .com 以匹配 *.com 地址。

继续，你也可以对站点使用时间条件。例如，如果你想在晚上允许访问新闻站点，你可以使用以下行设置一个时间类别：

```
acl freetime time MTWHFAS 18:00-23:59
```

这次，类别名为 freetime，条件为 time，这意味着我们需要指定类别应包含什么时间。后面七个字符是星期几：星期一、星期二、星期三、星期四、星期五、星期六和星期日。星期四和星期六使用大写 H 和 A，以免与星期二和星期日冲突。

定义了该类别后，你可以将 http_access 行更改为包含它，如下所示：

```
http_access allow newsites freetime
```

对于 Squid 现在允许访问，它必须同时匹配两个条件——请求必须是 *.bbc.co.uk 或 slashdot.org 之一，并且在指定的时间内。如果任一条件不匹配，该行就不会匹配，Squid 会继续查找下面的其他匹配规则。你在此处指定的时间在两端都包含，这意味着 freetime 类别中的用户将能够从 18:00:00 浏览到 23:59:59。

