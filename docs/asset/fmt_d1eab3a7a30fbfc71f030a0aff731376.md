
此输出显示了如果你使用了无法识别的指令 `http_deny` 和 `anonymize_headers` 时会看到的内容。当你解决配置中的任何错误后，使用启动命令启动 Squid：

```
$ sudo systemctl start squid
```

你现在完成了基础的 Squid 代理配置。

## 配置设备使用 Squid

接下来，你需要为每个使用该代理的设备配置代理设置。我们将解释如何配置 Windows、macOS 和 Linux 设备。

### Windows

1. 在你的 Windows 主机上，打开 Windows 设置对话框。
2. 在“查找设置”框中，搜索“代理设置”。
3. 在“代理”窗口中打开“使用代理服务器”开关。
4. 输入你的代理服务器的 IP 地址和端口——例如 `192.168.1.50:3128`。
5. 确保勾选“对于本地(内网)地址不使用代理服务器”复选框。

### macOS

1. 打开系统偏好设置。
2. 选择“网络”，选择你的无线或以太网适配器。
3. 点击“高级”-“代理”。
4. 勾选“Web 代理(HTTP)”。输入你的代理服务器的 IP 地址和端口号——例如 `192.168.1.50:3128`。对之前在 `/etc/squid/squid.conf` 文件中配置的每个协议执行此操作。
5. 将你的本地网络输入到“这些主机和域的代理设置”（Bypass Proxy Settings for these Hosts & Domains）框中。
6. 点击“确定”，然后点击“应用”。

### Linux

1. 在你的 Linux 终端上，打开设置对话框。
2. 转到“网络” ► “网络代理”。
3. 将代理设置为“手动”，并输入 HTTP 代理 IP 地址和端口号——例如 `192.168.1.50:3128`。
4. 确保在“忽略主机”框中输入你的本地网络，然后关闭任何打开的设置窗口。

## 测试 Squid

在配置好 Squid 服务器和至少一台设备后，请确保该设备确实在使用代理，并且代理功能符合预期。在 Squid 服务器上，使用以下命令来查看正在填充的 Squid 代理日志文件：

```
$ sudo tail -f /var/log/squid/access.log
```

```
--snip----
1619747519519 54 172.168.90.1 TCP_TUNNEL/200 39 CONNECT
play.google.com:443 HIER_DIRECT/172.217.25.174 -
1619747519755 54 172.168.90.1 TCP_TUNNEL/200 39 CONNECT
mail.google.com:443 HIER_DIRECT/216.58.200.101 -
1619747519776 55 172.168.90.1 TCP_TUNNEL/200 39 CONNECT
mail.google.com:443 HIER_DIRECT/216.58.200.101 -
1619747520190 161 172.168.90.1 TCP_MISS/200 98 GET
--snip--
```

你的输出将取决于你在网络中使用的应用程序。如果没有看到任何输出（且主机无法浏览），请使用步骤更新 iptables 或防火墙规则，允许流量进入 3128 端口的 Squid：

如果在运行 `tail` 命令期间从配置了代理的主机访问 Facebook，你应该会在日志中看到此请求：

```
--snip
1584414232.470 3 172.168.1.51 NONE/503 0 CONNECT
pixel.facebook.com:443 HIER_NONE/-
1584414237.647 0 172.168.1.51 NONE/503 0 CONNECT
pixel.facebook.com:443 HIER_NONE/-
1584414242.652 0 172.168.1.51 NONE/503 0 CONNECT
pixel.facebook.com:443 HIER_NONE/-
1584414247.864 23 172.168.1.51 TCP_TUNNEL/200 642 CONNECT
static.fbcdn.com:443 HIER_DIRECT/-
1584414248.566 0 172.168.1.51 NONE/503 0 CONNECT
pixel.facebook.com:443 HIER_NONE/-
1584414254.535 0 172.168.1.51 NONE/503 0 CONNECT
pixel.facebook.com:443 HIER_NONE/-
--snip--
```

如果无效，请尝试重启代理服务器、主机或两者。

## 阻止和允许域名

现在你的代理已经工作了，你可能想要阻止（黑名单）或允许（白名单）某些域名。例如，如果你有孩子，你可能想防止他们访问分心或不适当的网站。要这样做，请使用文本编辑器编辑 `squid.conf` 文件：

```
$ sudo nano /etc/squid/squid.conf
```

现在，找到显示 `INSERT OWN RULE(S) HERE` 的注释。在该部分中，你可以定义自己的规则（即 ACL）。如所述，一个 ACL 由 ACL 名称、ACL 类型（如允许或拒绝）以及元素列表（如 IP 地址或域名）组成。你的配置将由一个或多个此类规则组成，识别哪些允许通过代理。（之前你启用了 `http_access allow localnet` 和 `http_access deny !Safe_ports` 等推荐最小配置规则。）

例如，要阻止 Facebook，在 `include` 指令后输入以下行：

```
--snip
include /etc/squid/conf.d/*
acl denylist .facebook.com
http_access deny denylist
--snip--
```

列表开头的 `acl` 指令告诉 Squid 将后续内容视为允许或拒绝的项目列表。接下来，`denylist` 是列表的唯一名称；只要由字母数字组成，你可以选择任何名称。`dstdomain` 指令指示后续是目标域名列表。域名开头的点表示 Squid 应该阻止整个域名，包括子域名。例如，`www.facebook.com` 是一个顶级域名，可能有子域名 `campus.facebook.com` 或 `her.facebook.com`。如果你掉了前面的点，Squid 将阻塞父域名（facebook.com）。最后，`http_access` 指令禁止代理连接 ACL 中指定的域名或 URL。

保存配置文件并重载 Squid 使更改生效：

```
$ sudo systemctl reload squid
```

现在，从配置了使用代理服务器的主机访问 `www.facebook.com`。你应该看到如图 6-1 所示的错误页面。

![](img/8fad00e2c75135eb78018c62b7973377_151_0.png)

**图 6-1:** Squid 引起的浏览器错误

要再次允许 Facebook，请删除或注释你添加的行，保存配置文件并重载 Squid。
你可以通过将额外的域名添加到同一个 `denylist` ACL 中重复此过程：

```
acl denylist .facebook.com .twitter.com .linkedin.com
```

或者，你可以根据需要为每个网站或网站组/类别创建单独的 ACL。
白名单的工作方式几乎相同；任何添加到白名单的域名都将允许访问，但仅针对对代理进行身份验证的用户：

```
--snip
include /etc/squid/conf.d/*
allowlist dstdomain .facebook.com .twitter.com .linkedin.com
http_access allow CONNECT allowlist
--snip--
```

如果你添加了新的 ACL 规则，请注意它们在配置文件中的相对位置。Squid 将按照它们出现的顺序解释 ACL 规则，就像防火墙一样。如果 ACL 规则列表开头有一个 `deny all` 规则，Squid 将首先解释此规则并

然后忽略文件中的任何后续规则。这意味着您应该将任何自定义规则放在以下行之前：

```
--snip---
# 最后最后拒绝对此代理的所有其他访问
http_access deny all
--snip--
```

# 使用 Squid 保护个人信息

Squid 高度可配置，允许您作为管理员设置希望向互联网暴露的关于用户及其设备的多少信息。默认情况下，从客户端设备通过代理传输到互联网的流量不会经过匿名化处理。

为了防止网络外部人员获知您流量的来源（即服务器信息，或者您可能引用了哪个网站或资源，如 Amazon 或博客），请使用 `request_header_access` 指令来拒绝这些信息：

```
--snip---
