
## 跳板机和代理跳转 - 通过中间主机透明连接到远程主机

`ssh -J user1@jump-host user2@remote-host`
`ssh -o "ProxyJump user1@jump-host" remote-host`
与 `jump-host` 建立 SSH 连接并将 TCP 流量转发到 `remote-host`。如果 `jump-host` 拥有访问远程的 SSH 权限，该命令可以直接工作。如果没有，你可以使用代理转发（agent forwarding）将本地计算机的 SSH 身份转发到远程。
`img/4541d1f2c9832b9303a6df6c92f86f6_238_0.png`

### ssh -J jump-host1,jump-host2 ssh-server
指定用逗号分隔的跳板机。
`img/4541d1f2c9832b9303a6df6c92f86f6_238_1.png`

### ssh -o ProxyCommand="nc -X 5 -x localhost:3000 %h %p" user@remote-host
通过本地的 SOCKS 代理连接到远程服务器。从服务器的角度来看，源 IP 来自 `proxy-host`。但 SSH 连接本身是端到端加密的，因此代理主机只看到加密流量流。
`img/4541d1f2c9832b9303a6df6c92f86f6_238_2`

为了启用转发，你需要 `ssh-add` 你的本地身份。该命令将用于代理主机的检查。

## 可靠隧道 - 在网络故障期间保持 SSH 隧道开启

上述方法在特定的特定的主机上有效，但如果你想通过网络故障或不稳定的连接维护 SSH 隧道，你需要进行额外的设置。默认情况下，TCP 连接在空闲一段时间后可能会超时。为了防止超时，你可以在服务器和客户端配置发送心跳包，将其加入 `/etc/ssh/ssh_config`：

服务器端：
`ClientAliveInterval 15`
`ClientAliveCountMax 4`

客户端端：
`ServerAliveInterval 15`
`ServerAliveCountMax 4`

## 使用 AutoSSH 建立掉线的连接

虽然上述选项可以防止连接因空闲而掉线，但它们不会重新建立掉线的连接。为了确保 SSH 隧道重新建立，请使用 `autssh`，它构建隧道并监控其健康。`AutoSSH` 接受与端口转发相同的参数。
`img/4541d1f2c9832b9303a6df6c92f86f6`

```bash
autossh -R 2222:localhost -M 0 -o ServerAliveInterval 10 -o ServerAliveCountMax 3-host
```

使用 `-M 0` 标志允许 SSH 客户端处理健康检查。在此示例中，SSH 客户端期望服务器每 10 秒发送一次心跳。如果连续 3 次心跳失败，SSH 客户端将退出，`AutoSSH` 将重新建立新连接。

## 私有网络远程资源的透明访问

假设私有网络上有一个仓库只能通过网络上的私有服务器访问。该服务器无法从公网访问。你无需 VPN 即可访问私有网络。
`img/4541d1f2c9832b9303a6df6c92f86f6_239_0`

为了方便，你想让这个后门更加方便，可以在你本地的 `~/.ssh/config` 中添加一些指令：

```ssh
Host git.private.network

HostName git.private.network

ForwardAgent yes

ProxyCommand ssh nc %h %p
```

```ssh
Host private

HostName localhost

Port 2222

User private-user

ForwardAgent yes

ProxyCommand ssh tunnel@intermediate-host nc %h %p
```

现在，如果你从 `intermediate-host` 连接到端口 `2222`，你就连接到了私有网络上的服务器。现在你可以像在私有网络上一样访问 git 仓库。
`img/4541d1f2c9832b9303a6df6c92f86f6_239_1`

# Soccat 命令任务要求

## Soccat 示例

## Netcat 示例

连接/数据传输：

- TCP 连接：
- UDP 连接：
- 连接到远程系统
- 连接到串口设备
- 发送文件
- 接收文件

```
soccat tcp-listen:fork,fork=tcp:<port>

soccat udp-listen:fork,fork=udp:<port>

soccat tcp:<host>:<port>,fork=(connect to specific port)

soccat device:<device>,fork=tcp:<host>:<port>

soccat file:<file>,fork=tcp:write:file
```

```
nc -l <port> -c "<protocol>" (支持的协议)

nc -u -l <port> -c "<protocol>" (支持的协议)

nc <host> <port> # 连接到特定端口

nc <port> -e # SSH 映射到 TCP

nc -l <port> > <file
```

隧道隧道与代理：

- 创建基础隧道
- 建立嵌套隧道
- SSL/TLS 隧道（穿透防火墙）
- SOCKS 隧道（代理）
- PKI 认证
- SSH 隧道：
- 代理连接
- ICMP 转发
- 端口转发：
- UDP 打洞
- 连接多路用：

```
使用 SSH 隧道比 soccat 更好

soccat tcp-listen:fork,fork=<port> -remote-user-password

soccat tcp:<host>:<port>,fork=tcp:<port2>,fork

soccat tcp:<remote_host>:<remote_port>
```

访问 `https://rootmary.com/ssh-tunnels/`

```
nc -c <remote_host>:<remote_port>

nc -l -p <port1> && nc <port2> && nc <remote_host>_remote_port

nc -l -p <port1> -e /bin/sh #

proxys-nc -l -p <port1> -e nc:<host>:<port> -proxy_port <remote_host>

sh -i /bin/bash/user@<host> -nc -l <port>

nc -l:localhost:<remote_host> -user:<port> && ssh

nc -l -p <port1> -e <port2> (用这个效果更好)

nc -l -p <port1> -e <port2> (用这个效果更好)

nc -l -p <port1> -e <port2>

nc -u -l <port> -e "nc <port2>"
Netcat 并不是真的为此设计的，但你可以在脚本中使用它来实现，这已经超出了“单行命令”的范围
```

其他网络功能：

- 服务通信
- 域套接字
- 流量整形和带宽限制
- 负载均衡和故障转移
- DNS 解析
- 采集网络流量：
- 检查并修改数据：

```
soccat serial:<device,raw,echo:<host>:<port>

soccat unix-listen:path=unix-connect:path

soccat unix-bind:path=unix-soccat tcp:<host>:<port>,fork=bandwidth=<bandwidth> -link=<link>
(bandwidth) 受限制并会产生交互延迟

soccat tcp-listen:fork,fork=tcp:<port> -port

soccat tcp-listen:fork=reuse (仅已连接)

soccat tcp-listen:fork,addr=dns:53

soccat tcp-listen:fork,port=<port> -port

write:*filename

soccat tcp:<port>,fork=tcp:<port> -port

exec:
```

```
nc -l <port> - # 用于扫描的 TCP

nc -l -p <port> - | bash - SSH 更好- soccat 和 nc 都不安全（此处指传输安全）

配合 nmap 使用，但 nmap 本身做不到，所以建议这样做

nc -l <port> - | traffic.log

nc -l -p <start_port>-<end_port> (直接用 nmap 不吗?)
```
