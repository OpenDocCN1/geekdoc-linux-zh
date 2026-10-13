
你在示例中看到的内容表明环回接口存在且激活。`addr` 分配给 `localhost` 的 `127.0.0.1` 配合广播掩码 `255.255.255` 表示该接口有少量活动（RX = 接收，TX = 发送）。如果你的输出与上述不同，你必须在完成本节剩余部分后配置 localhost 接口。

# 手动配置环回接口

localhost 接口的 IP 地址在 Fedora 用于记录全网 IP 地址的配置文件中指定。文件 `/etc/hosts` 通常在系统中存在，即使它是空的。该文件被 Linux 内核和其他网络工具用于访问本地 IP 地址和主机名。如果你没有配置环回接口，必须编辑 `/etc/hosts`。

`/etc/hosts` 中的每一行都定义了环回接口 `127.0.0.1` 以及广播掩码 `255.255.255`，并且该接口有少量活动（RX = 接收，TX = 发送）。如果你的输出与上述不同，你必须在完成本节剩余部分后配置 localhost 接口。

TCP/IP 协议（参见本章稍后的“使用 TCP/IP 网络”）使用此接口为你的计算机分配 IP 地址，这是 Fedora 建立 PPP 接口所需的。

# 检查环回接口的可用性

通常情况下你不需要手动创建环回接口，因为 Fedora 在安装过程中会自动为你创建一个。要检查它是否已设置，你可以在 root 身份运行 `ifconfig` 命令，显示如下内容：

```
/sbin/ifconfig
lo: Loopback
  inet addr:127.0.0.1 Mask:255.0.0.0
  UP RUNNING MTU:16384 Metric:1
  RX packets:1 errors:0 overruns:0 frame:0
  TX packets:1 errors:0 overruns:0 carrier:0
  collisions:0 txuel:0
  RX bytes:760 (760.0 b) TX bytes:760 (760.0 b)
```

你在示例中看到的内容表明环回接口存在且激活。`addr` 分配给 `localhost` 的 `127.0.0.1` 配合广播掩码 `255.255.255` 表示该接口有少量活动（RX = 接收，TX = 发送）。如果你的输出与上述不同，你必须在完成本节剩余部分后配置 localhost 接口。

你应该能够使用 ping 来检查接口是否正常：

```
/bin/ping -c 3 localhost
PING localhost.domain (127.0.0.1) from 127.0.0.1 : 56(84) bytes of data.
64 bytes from localhost.domain (127.0.0.1) : icmp_seq=1 ttl=255 time=21
64 bytes from localhost.domain (127.0.0.1) : icmp_seq=2 ttl=255 time=80
64 bytes from localhost.domain (127.0.0.1) : icmp_seq=3 ttl=255 time=50
```
