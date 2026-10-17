
在你的网络浏览器中（从这里起假设使用的是 Firefox，但区别不大），访问 URL `http://www.ubuntulinux.org`。你应该应该在浏览器中看到它正常显示，但在日志窗口中，你应该能看到大量信息滚动通过，显示 Squid 正在为你加载内容并将其存储在缓存中。这些都是被允许的，因为默认配置允许访问 `localhost`（本地主机）。

回到配置编辑器窗口，在最后两行 `http_access` 之前添加以下内容：

```
http_access deny localhost
```

因此，最后三行看起来应该是这样：

```
http_access deny localhost
http_access allow localhost
http_access deny all
```

保存文件并退出编辑器。然后，运行此命令：

```
kill -SIGHUP cat /var/run/squid.pid
```

该命令查找 Squid 守护进程的进程 ID `PID` 并向其发送 `SIGHUP` 信号，强制它在运行时重新读取配置文件。你会在日志窗口中看到一串信息，显示 Squid 正在重新加载配置文件。如果你现在回到 Firefox 并输入一个新的 URL，你应该看到 Squid 的错误提示，告知你没有访问请求站点的权限。

你现在被代理拦截是因为 Squid 从上到下顺序读取其 ACL 行。如果它找到某一行是明确允许或拒绝的，它就会停止读取并采取相应行动。因此，在之前的几行中，`localhost` 在第一行被拒绝，然后在第二行被允许。当 Squid 看到 `localhost` 请求某个站点时，它首先读取拒绝行，并立即发送错误页面——它甚至没有读到允许的行。在底部添加一行 `deny all` 是非常有建议价值的，这样只有你显式允许的用户才能使用代理。

回到编辑配置文件，删除 `deny localhost` 和 `allow localhost` 行。这只留下了 `deny all`，它阻止了所有人（包括 `localhost`）访问代理。现在我们将添加一些条件语句：我们希望只有当 `localhost` 符合某些标准时才允许其访问。

访问标准是通过 `acl` 行定义的，因此在 `deny all` 行之上添加以下内容：

```
acl newsites dstdomain news.bbc.co.uk slashdot.org
http_access allow newsites
```

第一行定义了一个名为 `newsites` 的访问类别，它包含一个域名列表 `dstdomain`。域名是 `news.bbc.co.uk` 和 `slashdot.org`，因此整行的含义是：“创建一个名为 `newsites` 的新访问类别，它应该根据域名进行过滤，并包含列出的两个域名。”它没有说明是否对该类别授予或拒绝访问；那在下一行定义。`http_access allow newsites` 行意味着：“无限制地允许访问 `newsites` 类别”。它并不局限于 `localhost`，这意味着它适用于所有连接到代理服务器的计算机。

保存配置文件并重新运行之前的 `-SIGHUP` 命令行以重启 Squid，然后回到 Firefox 加载 `http://www.ubuntulinux.org`。你将看到与之前相同的错误，因为那不在我们的 `newsites` 类别中。现在尝试 `http://news.bbc.co.uk`，它应该是可以运行的。然而，如果你尝试 `http://slashdot.org`，它将无法工作，你可能已经注意到 BBC 新闻网站上的图片也没有出现。问题在于指定 `slashdot.org` 作为网站是特定的：这意味着 `http://slashdot.org` 不会被匹配，而 `http://www.slashdot.org` 则会。BBC 新闻站将其图片存储在站点 `http://news.bbc.co.uk` 上，这就是为什么它们没有显示。

回到配置文件，将 `newsites` ACL 修改为：

`acl newsites dstdomain .bbc.co.uk .slashdot.org`

将其放在域名之前（在 BBC 的情况下，去掉 `news.` 部分）意味着 Squid 将允许该站点的任何子域名工作，这通常是你想要的。如果你想要更模糊一些，可以只指定 `.com` 来匹配。

继续，你还可以使用时间条件用于站点。例如，如果你想在晚上允许访问新闻，可以使用此行设置 `freetime` 类别：

`acl freetime time MTWHAS 18:00-23:59`

此时，类别名为 `freetime`，条件是 `time`，我们需要指定该类别包含的时间。接随其后的字符是星期：周一、二、三、四、五、六、日。使用 `H` 和 `A` 是为了确保它们不冲突。定义该类别后，你可以将 `http_access` 行更改如下：

`http_access allow newsites freetime`

为了让 Squid 允许访问，必须满足两个条件——请求必须是 `.bbc.co.uk` 或 `.org`，且在指定的时间内。如果不满足任何一个，该行就不会被匹配，Squid 将继续查找规则。你指定的时间是包含的，这意味着 `freetime` 类别的用户可以在 18:00 到 23:59 之间上网。

## 代理

你可以添加尽可能多的规则，但要注意顺序要符合逻辑。记住，行中的所有条件都必须匹配行才能生效。这是一个复杂的例子：

- 你想要一个工作时需要的 `newsites` 类别。
- 你想要一个工作时不需要的 `playsites` 类别。
- 你想要一个从 09:00 到 18:00 的 `worktime` 类别。
- 你想要一个从 18:00 到 20:00 的 `freetime` 类别。
- 你想要在工作时间内允许人们访问新闻站点，但不允许访问娱乐站点。
- 你想要在空闲时间允许人们访问新闻站点，也允许访问娱乐站点。

为了实现这一点，你需要以下规则：

```
acl newsites dstdomain .bbc.co.uk .slashdot.org
acl playsites dstdomain .com .ubuntulinux.org
acl worktime time MTWHF 09:00-18:00
acl freetime time MTWHAS 18:00-20:00
http_access allow newsites worktime
http_access allow newsites freetime
http_access allow playsites freetime
```

> 注意：`D` 等于 `MTWHF`，意味着“所有每天”。

注意 `newsites` 类别有两个 `http_access` 行：一个针对 `worktime`，一个针对 `freetime`。这是你可以写成：

`http_access allow newsites worktime freetime`

然而，如果你这样做，并且有人在周二下午 2:30 `14:30` 访问 `news.bbc.co.uk`，Squid 的工作如下：

- 站点在 `newsites` 类别中吗？是的，继续。
- 时间在 `worktime` 类别内吗？是的，继续。
- 时间在 `freetime` 类别内吗？不是；不匹配规则，继续搜索。

这是因为 `worktime` 类别需要两行。

过滤请求的一种特别有效的方法是 `url_regex` 行。它允许你指定正则表达式对每个请求进行检查：如果表达式匹配请求，则条件匹配。

例如，如果你想阻止人们下载可执行文件，你会使用此行：

```
acl noexec url_regex -i exe
```

`$` 符号表示“URL 的结尾”，这意味着它会匹配 `http://www.sites.com/virus.exe` 但不会匹配 `http://www.executable.com/innocent.html`。`-i` 部分意味着“忽略大小写”，所以规则将匹配 `.exe`、`.EXE`、`.Exe` 等。你可以使用符号 `^` 表示“URL 的开头”。

例如，你可以使用此 ACL 阻止某些色情网站：

```
acl noporn url_regex -i sex
```

不要忘记每次更改 Squid 时都运行 `kill -SIGHUP` 命令；否则它不会重新读取你的更改。你可以通过以 root 运行 `squid -k parse` 来检查配置文件。如果你没有看到错误，说明你的配置是正确的。

> 至关重要的是，每次更改配置时都要运行 `kill -SIGHUP` 命令并提供 Squid 守护进程的 PID；没有这样做，Squid 将不会重新读取配置文件。

## 指定客户端 IP 地址

到目前为止配置选项都是基础的，你可以使用更多选项来增强你想要的代理系统。

在你决定了哪些规则适用于本地之后，是时候将它们扩展到其他机器了。你通过指定应允许或禁止访问的 IP 范围来实现这一点，并使用 ACL 行将这些输入 Squid。
