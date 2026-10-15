
# Squid 配置文件

Squid 配置文件为 `/etc/squid.conf`。用你喜欢的编辑器打开它。搜索字符串 `acl;`，这会将你带访问控制部分。`acl` 行构成了你的访问控制列表。这些行中的前 16 行定义了设置监听端口的最小推荐配置等。你可以安全地忽略它们。如果你继续向下滚动（越过另一个短注释块），转到 `http_access` 行，它们与 `acl` 行结合，规定谁可以做什么。你（并且应该）匹配每个 `acl` 和 `http_access` 行，以保持你的配置易于阅读。

![图 36.1 设置 Squid](https://example.com/img/cc2511072ab1772b1564720642.png)

> 注意
>
> Squid 的默认端口为 3128，你可以通过编辑 `http_port` 行来更改它。或者，你可以通过设置多个 `http_port` 行让 Squid 监听多个端口；80、8000 和 8080 都是代理服务器的常用端口。

在第一块 `http_access` 行下方是一个注释 `# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS.`。这正是你现在需要做的事情。不过，先再向下滚动几行，直到看到以下两行（它们在实际文件中并不一定相邻）：

```
http_access allow localhost
http_access deny all
```

这些行是不言自明的。第一行写着：“允许本地计算机的 HTTP 访问，但拒绝其他人。如前面提到的，这是默认规则。暂时保持不变，并运行 `service squid start` 以默认设置启动服务器。如果你还没有配置本地浏览器使用你的 Squid 服务器，现在可以配置了，这样就可以测试默认规则了。”

在你的网络浏览器中（从这里起假设 Firefox，因为它是标准 Ubuntu 安装中的默认浏览器，但区别不大），访问 URL `www.ubuntu.com`。你应该能在浏览器中正常地看到它，但在日志窗口中，你应该看到大量信息滚动通过，Squid 正在为你你下载该站点并将其存储在缓存中。这一切都是允许的，因为默认配置允许访问 localhost。

回到配置编辑器窗口，在最后几行 `http_access` 之前添加以下内容：

```
http_access deny localhost
```

所以，最后三行看起来如下：

```
http_access deny localhost
http_access allow localhost
http_access deny all
```

保存文件并退出编辑器。然后运行此命令：

```
mathew@seymour:$ kill -SIGHUP /var/run/squid.pid
```

此过程获取 squid 守护进程的 ID `PID`，然后向其发送 `SIGHUP` 信号，强迫它在运行时重新读取配置文件。你应该会在日志窗口中看到一串信息，因为 Squid 正在重新加载其配置。如果你回到 Firefox 输入一个新 URL，你将看到一个 Squid 错误页面，告知你没有访问所请求站点的权限。

你现在被代理拦截的原因是 Squid 按顺序读取其 ACL 行，如果它发现某一行能够确定性地允许或拒绝某个请求，它就会停止读取并采取相应的操作。因此，在之前的几行中，localhost 在第一行被拒绝，然后在第二行被允许。当 Squid 看到 localhost 请求某个站点时，它读取了 `deny` 行并立即发送错误页面；它甚至没有读到 `allow` 行。在末尾添加一个 `deny all` 是被极力建议的，这样只有你显式允许的用户才能使用代理。

回到编辑配置文件，并删除 `deny localhost` 和 `allow localhost` 行。这留下了所有人（包括 localhost）都可以访问代理。现在你正在添加一些条件允许 `allow` 语句。你希望仅在 localhost 符合特定标准时才允许其访问。

定义访问标准是通过 `acl` 行完成的，因此在 `deny all` 行之上，内容如下：

```
acl newsites domain www.bbc.co.uk slashdot.org
http_access allow newsites
```

## 访问控制列表 `ACL`

第一行定义了一个名为 `newsites` 的访问类别，它包含一个域名列表 `dstdomain`。域名是 `news.bbc.co.uk` 和 `slashdot.org`，所以整行的意思是：“创建一个名为 news sites 的新访问类别，根据域名进行过滤并包含列出的两个域名。”它没有说明是否授予或拒绝该类别的访问；这由下一行决定。`http_access allow newsites` 行意味着“允许无限制地访问 news sites 类别”。它并不局限于 localhost，这意味着它适用于连接到代理的每台计算机。

保存配置并在重启 Squid 之前运行 `kill -SIGHUP` 行；然后回到 Firefox 尝试加载 `my.ubuntu.com`。你将看到之前的错误，因为这不在你的 `newsites` 类别中。现在尝试 `http://news.bbc.co.uk`，它应该可以正常工作。然而，如果你使用 `slashdot.org`，它将无法工作，你可能还会注意到 BBC 新闻网站上也没有出现图片。问题在于指定 `slashdot.org` 为网站是：这意味着 `http://slashdot.org` 将工作，而 `slashdot.org` 则不行。BBC 新闻站点将其图像存储在 `http://news.bbc.co.uk` 站点上，这就是为什么它们没有显示。

回到配置文件并将 `newsites` ACL 修改为：

```
acl newssites dstdomain .bbc.co.uk .slashdot.org
```

在域名前面加点（在 BBC 的情况下，也包含了 news）意味着 Squid 将允许该站点的任何子域名运行，这通常是你想要的。如果你希望更加模糊，可以指定 `.com` 来匹配所有 `*.com` 地址。

接下来，你还可以为站点使用时间条件。如果你想在晚上访问新闻网站，可以使用此行设置一个时间类别：

```
acl freetime time MTWFAS 18:00-23:59
```

此时，该类别名为 `freet`，条件是 `time`，这意味着你需要指定该时间类别包含什么。随后的七个字符是一周的几天：周一、周二、周三、周四、周五、周六和周日。周四可以大写 H 和 A，以免与周二和周日冲突。

定义完成后，你可以修改 `http_access` 行来包含它，如下所示：

```
http_access allow newsites freetime
```

要让 Squid 现在允许，它必须同时匹配两个条件——请求必须针对 `*.bbc.co.uk` 或 `slashdot.org`，并且必须在指定的时间范围内。如果任何一个条件不匹配，该行就不会被匹配，Squid 将继续允许下方的其他匹配规则。你在此指定的时间两端都是包含在内的，这意味着 `freetime` 类别中的用户可以从 18:00:00 上上网到 23:59。

每行都有一个 IP 地址，后面跟着一个斜杠和一个数字。最后那个数字定义了你所涵盖的地址范围，并指的是 IP 地址中的位数。IP 地址是一个 32 位数字，通常以点分十位法表示：`A.B.C.D`。这些四组数字中的每一个都介于 0 到 255 之间（其中某些被保留用于特殊用途），每个数字都以 8 位数字的形式存储。

上代码中的第一行涵盖了从 192.0.0.0 开始的 IP 地址；`/8` 部分意味着前 8 位（第一个组，192）是固定的，其余部分是灵活的。因此，Squid 将所有从 192.0.0.0 到 192.0.0.255、192.0.1.0 直到 192.255.255.255 的地址视为在范围内。

第二行使用 `/16`，意味着 Squid 允许从 192.168.0.0 到 192.168.255.255 的 IP 地址。最后一行有 `/24`，允许 192.168.0.0 到 192.168.0.255。

这些地址被放置在 `src ACL` 行中，如下：

```
acl internal_network src 10.0.0.0/24
```

这创建了一个从 10.0.0.0 到 10.0.0.255 的地址组。你可以这样组合多个地址组：

```
acl internal_network src 10.0.0.0/24 10.3.0.0/24 10.5.0.0/24 192.168.0.1
```

这个示例允许 10.0.0.0 到 10.0.0.255，然后是 10.0.3.0 到 10.0.3.255，最后是单体地址 192.168.0.1。

请记住，如果你正在使用本地机器，并且有网络浏览器来通过 127.0.0.1 使用代理，那么客户端 IP 地址也将是 127.0.0.1。因此，请确保为 localhost 设置了相应的规则。
