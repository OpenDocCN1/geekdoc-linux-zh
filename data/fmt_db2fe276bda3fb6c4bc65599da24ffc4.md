
```
[root@usannah] chkconfig --list squid

squid 0:off 1:off 2:off 3:off 4:off 5:off 6:off

[root@usannah] chkconfig --level 345 on

[root@usannah] chkconfig --list squid

squid 0:off 1:off 2:off 3:on 4:on 5:on 6:off
```

## 配置客户端

在配置新的 Squid 服务器之前，你应该设置本地浏览器使用 Squid。这允许你在处理配置文件时测试你的规则。

要配置 Firefox，从“编辑”菜单中选择“首选项”。在弹出的对话中，点击“连接设置”按钮（通用选项卡底部），并选择“手动代理配置”。勾选下方的“为所有协议使用代理”，然后输入 `127.0.0.1` 作为 IP 地址，`3128` 作为端口号。参见第 26.1 节了解其用法。如果你正在配置远程客户端，请指定代理服务器的 IP 而 `127.0.0.1`。

对于 Konqueror，进入“设置”菜单并选择“配置 Konqueror”。在左侧标签中，滚动到“代理”，选择“代理设置”，然后点击“设置”。输入 `127.0.0.1` 作为代理地址，`3128` 作为端口。对于 Firefox，如果你正在配置远程客户端，请指定代理服务器的 IP 而 `127.0.0.1`。

Internet Explorer 的代理设置在“工具/Internet 选项”中。在“连接”选项卡中，点击“LAN 设置”按钮，并启用“为 LAN 使用代理服务器”选项。输入地址为 Squid 机器的 IP，并指定 `3128` 作为端口。

# 访问控制列表 (Access Control Lists)

![](img/c4a0ea5ab3561ff33a8da88887702720_730_0.png)

**图 26.1** 设置 Firefox 使用 `127.0.0.1` 将其所有网络请求通过 Squid 。

## 访问控制列表

Squid 的主配置文件是 `/etc/squid/squid.conf`，Fedora 的默认配置文件包含了大量的注释以引导你操作。默认配置允许访问本地机器，但拒绝你网络中的其他部分。这是一个安全的起点；我们建议你在将规则推送到其他机器之前，先在自己（localhost）上尝试所有规则。

在开始之前，以 root 身份打开两个终端窗口。在第一个窗口中，切换到目录 `/var/log/squid` 并运行此命令：

```
tail -f access.log cache.log
```

该命令读取两个文件的最后几行，并（由于使用了 `-f` 标志）持续跟踪它们，这样任何更改都会显示在其中。这允许你在人们访问 Squid 时观察它正在做什么。我们将此窗口称为“日志窗口”，请保持其打开。在另一个窗口中（记住要以 root 身份），用你喜欢的编辑器打开文件 `/etc/squid/squid.conf`。此窗口将称为“配置编辑器”，你也应该保持其打开。

要开始操作，搜索字符串 `acl`——这会带你进入访问控制部分，那里是大部分需要工作的地方。你可以在其他地方配置很多内容，但除非你有特殊需求，否则可以保持默认设置不变。

注意

Squid 的默认端口是 `3128`，但你可以通过编辑 `http_port` 行来更改它。或者，你也可以通过设置多个 `http_port` 行让 Squid 监听在多个端口上：`80`、`8000` 和 `8080` 都是代理服务器的常用端口。

`acl` 行构成了你的访问控制列表。前 16 行左右定义了设置监听端口的最小推荐配置。你可以安全地忽略它们。如果你继续向下滚动（越过另一个简短的注释块），你就会来到 `http_access` 行，它们与 `acl` 行结合，决定了你可以做什么。你可以保持你的配置文件易于读写。

在第一块 `http_access` 行正下方是注释 `# INSERT YOUR OWN RULE(S) HERE TO ALLOW ACCESS FROM YOUR CLIENTS.`。这正是我们要做的。不过，先再向下滚动几行，你应该能看到这两行：

```
http_access localhost

http_access deny all
```

它们是自言自明的：第一行意思是“允许对本地计算机进行 HTTP 访问，但拒绝其他人”。这就是前面提到的默认规则。现在保持它不变，并运行 `service squid start` 来以默认设置启动服务器。如果你尚未配置本地网络浏览器使用你的 Squid 代理，请现在进行操作，以便你可以测试规则。

在你的网络浏览器中（从现在起假设 Firefox，但区别不大），访问 URL `http://fedora.redhat.com`。你应该能看到它在浏览器中正常显示，但在日志窗口中，你应该能看到日志消息在滚动，因为 Squid 正在为你下载该站点并将其存储在缓存中。这一切都是允许的，因为默认配置允许访问 localhost。

回到配置编辑器窗口，在最后两个 `http_access` 行之前添加以下内容：

```
http_access deny localhost

http_access allow localhost

http_access deny all
```

所以，最后三行应该像这样：

保存文件并退出编辑器。然后，运行此命令：

```
kill -SIGHUP `cat /var/run/squid.pid`
```

该命令查找 Squid 守护进程的 PID，然后向它发送 SIGHUP 信号，强迫它在运行时重新读取其配置文件。你应该会在日志窗口中看到一串消息，因为 Squid 正在重新读取它的配置文件。如果你现在回到 Firefox 并输入一个新的 URL，你应该会看到 Squid 错误页面，提示你没有访问请求站点的权限。

你现在被代理拦截的原因是 Squid 从上到下按顺序读取它的 ACL 行。如果它发现某行可以确定性地允许或拒绝某项请求，它就会停止读取并采取相应操作。因此，在之前的行中，localhost 在第一行和第二行中都被拒绝了。当 Squid 看到 localhost 请求站点时，它会先读取拒绝行并立即发送错误——它甚至没有读到允许行。强烈建议在底部放置一条拒绝行，这样只有你显式允许的人才能使用代理。

回到编辑配置文件并删除 `deny localhost` 和 `allow localhost` 行。这留下了 `deny all`，它阻止了所有人（包括 localhost）使用代理。现在我们将添加一些条件允许语句：我们只想在 localhost 符合标准时才允许它访问。

定义访问标准是通过 `acl` 行完成的，因此在 `deny` 行上方，添加以下内容：

```
acl newswites dstdomain news.bbc.co.uk slashdot.org

http_access_allow newswites
```

第一行定义了一个名为 `newswites` 的访问类别，它包含一个域名列表 (`dstdomain`)。域名是 `news.bbc.co.uk` 和 `slashdot.org`，所以整行读起来是“news.bbc.co.uk 和 slashdot.org”。（注：此处原文存在大量重复的 OCR 错误，已清理）。

![](img/c4a0ea5ab3561ff33a8da88887702720_732_0.png)

## 建立代理服务器

接下来，你还可以使用时间条件。例如，如果你想在晚上允许访问新闻，可以使用此行设置一个时间类别：

```
acl freetime time
```

这次，类别名为 `freetime`。接随其后的七个字符是周几：一、二、三、四、五、六和日。在定义了 `freetime` 类别后，你可以更改 `http_access` 行包含它，如下所示：

```
http_access allow newswites
```

要让 Squid 现在允许访问，它必须匹配两个条件——请求必须针对 `*.bbc.co.uk` 或 `slashdot.org`，并且在指定时间内。如果任一条件不匹配，该行就不会匹配，Squid 将继续向下查找匹配的规则。你在这里指定的时间是两端包含的，这意味着 `freetime` 类别的用户可以在从 `18:00` 到 `23:59` 上网。

你可以添加任意数量的规则，但你应该小心尝试调整排序，使其符合逻辑。记住，行中的所有条件都必须匹配该行才会生效。这里有一个更复杂的例子：

- 你想要一个 `newssites` 类别，包含人们工作需要的网站。
- 你想要一个 `playsites` 类别，包含人们工作不需要的网站。
- 你想要一个 `worktime` 类别，时间从 `09:00` 延伸到 `18:00`。
- 你想要一个 `freetime` 类别，时间从 `18:00` 延伸到 `20:00`（办公室关闭）。
- 你希望人们在上班时间内访问新闻网站，但不能访问游戏网站。
- 你希望人们在空闲时间可以访问新闻网站和游戏网站。

为了实现这一点，你需要以下规则：

```
acl newssites ddomain .bbc.co.uk .slashdot.org
```
