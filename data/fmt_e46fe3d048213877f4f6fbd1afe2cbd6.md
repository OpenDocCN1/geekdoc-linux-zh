
或者，可以通过命令行选项 `-nat` 启用 PPP NAT。`/etc/rc.conf` 中还有一个名为 `ppp_nat` 的控制旋钮，它是默认开启的。

如果你使用此功能，你可能还会发现以下 `/etc/ppp/ppp.conf` 选项用于启用接入连接转发：

```
nat port tcp 10.0.0.2:ftp
```

```
nat port tcp 10.0.0.2:http
```

或者完全不信任外部：

```
nat deny_incoming_yes
```

## 23.2.1.4 最终系统配置

你已经配置了 `ppp`，但在它工作之前还有几件事需要完成。它们都涉及编辑 `/etc/rc.conf` 文件。

从该文件从上往下操作，确保设置了 `hostname=` 行，例如：

```
hostname="foo.example.com"
```

如果你的 ISP 为你提供了静态 IP 地址和名称，最好使用此名称作为你的主机名。

查找 `network_interfaces` 变量。如果你想配置系统按需拨号 ISP，确保将 `tun0` 设备添加到列表中，否则将其删除。

```
network_interfaces="lo0 tun0"
ifconfig_tun0=
```

> 注意：`ifconfig_tun` 变量应该为空，并且应该创建一个名为 `/etc/start_if.tun0` 的文件。该文件应包含以下行：

```
ppp -auto mysystem
```

该脚本在网络配置时执行，以自动模式启动你的 `ppp` 守护进程。如果你有一个以此为网关的局域网，你可能还想使用 `-alias` 关。参阅手册页获取更多详细信息。

确保 `/etc/rc.conf` 中的以下行将路由器程序设置为 NO：

```
router_enable="NO"
```

确保 `routed` 守护进程不启动，因为 `routed` 倾向于删除由 `ppp` 创建的默认路由表条目。

可能值得确保 `sendmail_flags` 这一行不包含 `-q` 选项，否则 `sendmail` 将不时尝试进行网络查找，并可能导致你的机器拨号。

```
sendmail_flags="-bd"
```

此方法的缺点是，每当 `ppp` 链路启动时，你必须通过输入以下命令强制 `sendmail` 重新检查邮件队列：

```
# /usr/sbin/sbin -q
```

你可能希望在 `ppp.linkup` 中使用 `!bg` 命令来自动执行此：

```
1 provider:
2 delete ALL
3 add 0 0 HISADDR
4 !bg sendmail -bd -q30m
```

如果你不喜欢，可以设置一个“过滤器”来阻止 SMTP 流量。更多细节请参阅示例文件。

最后剩下的就是重启机器。重启后，你现在可以：

```
# ppp
```

并拨号 `provider` 以启动 PPP 会话；或者，如果你希望 `ppp` 在有出站流量时自动建立会话（如果你还没有创建 `start_if.tun0` 脚本），输入：

```
# ppp -auto provider
```

## 23.2.1.5 总结

总结一下，在首次设置 `ppp` 时，以下步骤是必要的：

客户端：

- 1. 确保 `tun` 设备已编译到你的内核中。
- 2. 确保 `tun` 设备文件在 `/dev` 目录下可用。
- 3. 在 `/etc/ppp/ppp.conf` 中创建一个条目。对于大多数 ISP，`ppemand` 示例足够。
- 4. 如果你有动态 IP 地址，在 `/etc/ppp/ppp.link` 中创建一个条目。
- 5. 更新你的 `/etc/rc.conf` 文件。
- 6. 如果你需要拨号，请创建一个 `start_if.tun0` 脚本。

服务器端：

- 1. 确保 `tun` 设备已编译到你的内核中。
- 2. 确保 `tun` 设备在 `/dev` 目录下可用。
- 3. 在 `/etc/passwd` 中创建一个条目（使用 `vipw(8)` 程序）。
- 4. 在用户主目录下创建一个运行 `ppp -direct direct-server` 或类似命令的配置。
- 5. 在 `/etc/ppp/ppp.conf` 中创建一个条目。`direct-server` 示例足够。
- 6. 在 `/etc/ppp/ppp.linkup` 中创建一个条目。
- 7. 更新你的 `/etc/rc.conf` 文件。

## 23.3 使用内核 PPP

部分最初由 Gennady B. Sorokupid 和 Robert Huff 贡献。

## 23.3.1 设置内核 PPP

在你的机器上启动 PPP 之前，请确保 `pppd` 位于 `/usr/sbin` 且 `/etc/ppp` 目录存在。
`pppd` 可以以两种模式工作：

- 1. 作为“客户端”——你想要通过 PPP 串口连接或调制解调器线路将你的机器连接到外部世界。
- 2. 作为“服务器”——你的机器位于网络上，用于通过 PPP 连接其他计算机。

在这两种情况下，你都需要设置选项（`/etc/ppp/options` 或如果你的机器上有多个使用 PPP 的用户，则使用 `-/.ppprc`）。
你还需要一些调制解调器/串口软件（优先使用 `comms/kermit`），以便拨号并与远程主机建立连接。

## 23.3.2 使用 pppd 作为客户端

基于 Trev Royhouse 提供的信息。
以下 `/etc/ppp/options` 可能用于连接到 Cisco 终端服务器 PPP 链路。

```
# 启用硬件流控
# 调制解调器控制线
# 远程 PPP 服务器必须提供你的 IP 地址
# 如果远程主机在 IPCP 协商期间没有发送你的 IP
# 请移除此选项
# 等待 LCP 数据包
crtscts
modem
noipdefault
passive
domain ppp.foo.com # 在此处输入你的域名
:::<remote_ip> #在此处输入远程 PPP 主机的 IP
# 它将被用于通过 PPP 链路路由数据包
# 如果没有指定 noipdefault 选项
```

# 第 23 章 PPP 和 SLIP

# 将此行更改为 <local_ip>:<remote_ip>
defaultroute # 如果你希望 PPP 服务器成为你的
# 默认路由器请放置此项

要连接：

- 1. 使用 Kermit（或其他调制解调器程序）拨接到远程主机，并输入你的用户名和密码（或启用远程主机 PPP 所需的任何内容）。
- 2. 退出 Kermit（不要挂断线路）。
- 3. 输入以下内容：
`# /usr/src/usr.sbin/ppppd /dev/tty01 19200`
确保使用适当的速度和设备名称。

现在你的电脑已通过 PPP 运行。如果连接失败，你可以向 `/etc/ppp/options` 文件中添加 `debug` 选项，并检查控制台消息以跟踪问题。
后续 `/etc/ppp/pppup` 脚本将使所有三个阶段都自动化：

```
#!/bin/sh
ps ax | grep pppd | grep -v grep
pid=$(ps ax | grep pppd | grep -v grep | awk '{print $1}')
if [ "X$pid" != "X" ]; then
	echo 'killing pppd, PID=$pid'
	kill -9 $pid
fi
```

```
set flow none
```

```
pau 1
out +++
inp 5 OK
out ATH0\13
inp 5 OK
echo \13
out ATS0=1\13      ; 如果想禁用此项，请更改为 ATS0=0\13
      ; 应答模式
```

```
inp 5 OK
echo \13
exit
```

名为 `/etc/ppp/kermit.dial` 的脚本用于拨号到远程主机进行身份验证。你需要根据需要对其进行自定义。请将你的登录名和密码放在此脚本中；你可能还需要根据调制调器和远程主机的响应更改输入语句（input statement）。

```
;
填写连接到调制调器的 com 线路:
set line /dev/tty01
;
在此处填写调制调器速度:
; set speed 19200
set file type binary      ; 全 8 位文件传输
set names literal
set win 8
set rec pack 1024
set send pack 1024
set block 3
set term bytesize 8
set command bytesize 8
set flow none
set modem hangup off
set dial hangup          ; 如果必要，使用 CARRIER，
set dial display on       ; 如果必要，使用 DIAL，
```
