
此条目告诉 `ldirectord` 使用 `syslog` 设施记录错误消息。（查看文件 `/etc/syslog.conf` 以确定 "info" 级别的消息是如何写入的。）你也可以输入目录和文件名来写入日志消息（在条目前加 `/`）。如果没有提供条目，日志消息将写入 `/var/ldirectord.log`。

`virtual=209.100.100.3:80`

这一行指定了我们……的 VIP 地址和端口号。

（注：提示中的 OCR 文本包含大量重复和片段。将根据提供的页面逻辑提供一个干净的版本。）

`checkpoint=80`

此行表示 http 服务的健康检查请求应在端口 80 上执行。

`protocol=tcp`

此项指定了该虚拟服务将使用的协议。协议可以设置为 `tcp`、`udp` 或 `fwm`。如果你使用 `fwm` 来表示标记的数据包或 `fmarked` 数据包，那么你必须已经在与这些缩进行关联的 `virtual=` 行中使用了 Netfilter 标记数字（或 `fmark`），而不是 IP 地址。

`scheduler=wrr`

`scheduler` 节点表示我们想要使用加权轮询负载均衡技术（参见上文的 `real` 行，其中显示了集群中每个真实服务器分配的权重）。有关 LVS 支持的调度方法的描述，请参阅第 11 章。`ldirectord` 程序不会检查此条目的目的有效性；`ldirectord` 只是会将你在此处通过 `ipvsadm` 命令输入的任何内容传递下去，以创建虚拟服务。

`checktype=negotiate`

此选项描述了 `ldirectord` 守护进程应该使用何种方法对该 VIP 的真实服务器检查。`checktype` 可以设置为以下之一：

### negotiate

此方法连接到真实服务器并发送你指定的请求字符串。如果在 `checkimeout` 期间没有从真实服务器收到你指定的回复字符串，则该节点被认为已死亡。你可以为每个节点指定请求和回复字符串，正如我们在示例中所做的（参见本节早些对 `real` 行的讨论），你也可以通过在 `lirector` 配置文件中添加两个新行来指定一个适用于所有真实服务器的请求字符串和一个回复字符串：

```
request="healthcheck.html"
receive="OKAY"
```

### connect

此方法简单地连接到指定 `checkpoint`（或真实服务器指定的端口）真实服务器，如果真实服务器接受了基础的 TCP/IP 连接，则假设真实服务器上一切正常。对于检测运行在真实服务器上的资源守护进程（如 HTTP）出现的问题，此方法不如 `negotiate` 方法那样可靠。当你想要监控的服务没有可用的 `negotiate` 检查时，`connect` 检查非常有用。

### Number（数字）

如果你在此处输入数字而不是单词 `negotiate` 或 `connect`，`ldirector` 将执行指定次数的连接测试，然后执行一次 `negotiate` 测试。这种方法减少了真实服务器在响应健康检查时的处理能力消耗，并减少了真实服务器上服务健康监控所需的集群网络流量。²¹

`off`

这禁用了 `lirector` 对真实服务器的健康监控。

```
fallback=127.0.0.1
```

`fallback` 地址是当 IPVS 表中没有真实服务器可以满足客户端对服务的请求时，客户端连接应重定向到的 IP 地址和端口号。通常，这将是环回地址 `127.0.0.1`，以便强制客户端连接到本地运行的守护进程，该守护进程至少能够通知用户存在问题，并可能让他们知道联系谁寻求额外帮助。

你也可以为 `fallback` 网页指定一个特殊的端口号：

```
fallback=127.0.0.1:9999
```

> 注意 我们没有使用 `persistence` 来创建虚拟服务表。在 `lirector.conf` 文件中通过 `persistent` 条目启用 `persistence`，并指定持续秒数。关于 LVS `persistence` 的讨论，请参阅第 14 章。

## 创建健康检查网页

现在，在每个真实服务器和 Director 上输入类似所示的命令来创建一个简单的健康网页：

```
#echo "OKAY" / /www/htdocs/.healthcheck.html
```

> 注意 此处使用的目录应该是你在 `httpd.conf` 文件中指定的 `DocumentRoot`。还要注意此示例中文件名前的点 (.)。²²

²¹ 它减少了多少网络流量取决于服务的类型以及真实服务器必须发送以验证其运行正常的响应包大小。
² 这不是一种源自 Unix 系统概念的延续，即以点 (.) 开头的文件名不会被 `ls` 命令列出（除非使用 `-a` 选项），因此对普通用户隐藏。

第 15 章

使用以下命令检查健康检查网页是否在每个真实服务器上正常显示：

```
# lynx -dump 127.0.0.1/.healthcheck.html
```

# 手动启动 lirector 并测试你的配置

稍后我们将使用 Heartbeat 启动 `lirector` 监控守护进程，但你首先需要尝试在 Director 上启动守护进程，查看你的 IPVS 表已创建。

- 1. 输入此命令：

```
#/etc/ha.d/resource.d/ldirector -d lirector-209.100.100.3conf start
```

你应该能看到 `lirector` 的调试输出，指示 `ipvsadm` 命令已运行以创建虚拟服务器，随后是如下命令：

```
DEBUG: check_http http://209.100.100/.healthcheck.html is down
```

- 2. 现在，如果你访问了 IP 地址为 209.100.100.100 的真实服务器，且它正在运行 Apache Web 服务器，`ldirector` 的调试输出消息应变为：

```
DEBUG: check_http http://209.100.100/.healthcheck.html is up
```

- 3. 检查以确保 IPVS 表已创建。

- 4. 一旦你对 `lirector` 配置满意，请通过以下命令退出调试模式：

```
#ipvsadm -L
```

- 5. 使用以下命令以 `-d` 模式启动 `lirector`：

```
#/usr/sbin/ldirector-209.100.100.3conf start
```

- 6. 然后使用 `watch` 命令自动更新显示：

```
#watch ipvsadm -L
```

你你会看到如下 ipvs 表：

```
Virtual Server version x.x
Prot LocalAddress:Port Scheduler
-> RemoteAddress:Port Weight ActiveConn
TCP 209.100.100.100:80 wrr 1
```

- 7. 通过关闭真实服务器来测试 `lirector`。在设定的 `checkimeout` 时间内，真实服务器的权重应变为 0。

- 8. 重启真实服务器上的 Apache，你会看到其权重返回 1。

# 将 lirector 加入 Heartbeat

现在我们要让 Heartbeat 知道你的 `lirector` 配置，以便它能自动启动守护进程。

- 1. 如果你还没有这样做，请按照第 7 章安装 Heartbeat 程序；然后在 `/etc/hasfiles` 中创建条目：

```
primarydomain.com 209.100.100.3 lirectord
```

其中 `primarydomain.com` 是主 Director 的主机名（通过 `uname -n` 获取）。`hasresources` 条目告诉 Heartbeat 名为 `primarydomain.com` 的机器应该拥有 VIP `209.100.100.3` 的 `lirectord`。

- 2. 使用以下命令停止 `lirectord`：

```
#/etc/ha.d/resource.d/ldirector-209.100.100.3conf stop
```

- 3. 检查 `lirectord` 是否不再运行：

```
#ps -elf | grep lirectord
```

如果 `lirectord` 未运行，此命令将不会返回任何输出。如果你在这里看到运行的进程，请在继续下一个命令之前杀死它。

- 4. 使用命令确保 `lirectord` 不作为启动脚本启动：

```
#chkconfig --del lirectord
```

- 5. 使用命令停止 Heartbeat：

```
#/etc/rc.d/init.d/heartbeat stop
```

- 6. 使用命令清理 ipvs 表，使其不包含任何测试信息：

```
#ipvsadm -C
```

- 7. 现在启动 守护进程：

```
#/etc/rc.d/init.d/heartbeat start
```

使用以下命令观察守护进程的输出：
