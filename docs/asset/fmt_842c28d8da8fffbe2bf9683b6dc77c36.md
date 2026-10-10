
```
eth0: flags=6163,BROCAST,RUNNING,MULTICAST> mtu 1500
  inet 172.16.77.159  netmask 255.255.0.0 broadcast 172.16.255.255
  inet6 fe80::a00e:ff42:e906/64 scope link 
      eth0:08:42:56:00len 1000 (Ethernet)
  RX packets 2268 bytes 43088 (KiB) errors 0 coll 0
  TX packets 2469 bytes 44562 (KiB) errors 0 coll 0
lo: flags=73,LOOPBACK,RUNNING  mtu 65536
  inet 127.0.0.1  netmask 255.255.0.0
  inet6 ::1  prefix 64 scope host
  RX packets 1572 bytes 13058 (KiB) errors 0 coll 0
  TX packets 1572 bytes 13058 (KiB) errors 0 coll 0
```

图 11.3 – `p0f` 输出

你也可以使用 `p0f -L` 命令列出所有接口。

4. 图 11.3 中的输出显示有两个接口：`eth0` 是 IP 为 172.16.77.159 的以太网接口，`127.0.0.1` 是回环地址。通过输入以下命令使用 `eth0` 接口：

```
sudo p0f -i eth0
```

接下来的截图显示了上述命令的输出。

```
kali@kali:~$ sudo 
p0f 3.09b 由 Michal Zalewski <lcamtuf@coredump.cx>
[+] 关闭
[+] 加载了 32 个签名来自 /etc/p0f.fp
[+] 正在拦截接口 eth0 上的流量
[+] 默认配置完成
[+] 进入循环
```

图 11.4 - `p0f` `eth0` 输出

## 遗留、恶意软件与勒索软件分析

这可能需要运行一时间，但在接下来的图中，我们可以看到 IP 地址和操作系统的输出。

```
[+] 关闭
[+] 加载了 32 个签名来自 /etc/p0f.fp
[+] 正在拦截接口 eth0 上的流量
- 172.16.77.161/33364 -> 172.16.77.159 (syn)
  client    = 172.16.77.161/33364
  os        = 通用
  dist      = Linux 2.2.3-x
  params    = 0
  raw_sig   = 4:64.0:1460:65535,7:mss,ts,nop,ws:df,id=0
- 172.16.77.161/33364 -> 172.16.77.159 (mtu)
  client    = 172.16.77.161/33364
  link      = 以太网或调制解调器
  raw_mtu   = 1500
```

图 11.5 - `p0f` 结果输出

让我们通过打开浏览器进一步检测其他主机可能正在通信。

5. 在 Kali 中打开网络浏览器，你会看到终端填充了更多 IP 信息。默认情况下，Firefox 浏览器首页会将我们带到 Offensive Security 网站，`p0f` 显示有关连接和到服务器的信息。

6. 尝试浏览一个网站。我在浏览器中打开了 `www.cidr.com`。`p0f` 实时更新终端信息，第一条记录显示了从 172.16.77.159（我的 Kali 机器）到 185.230.60.211 80端口的 SYN 请求。我还可以看到关于我的 Kali 机器的信息，例如由 `p0f` 识别出的操作系统（Linux 2.2.3-x）：

### 使用 `p0f` 识别设备和操作系统

```
[ 172.16.77.159/53382 -> 185.230.60.211/80 (syn) ]
client = 172.16.77.159/53382
os = Linux 2.2-x-3.x
dist = 0
params = 通用
raw_sig = 4:64.0:1460:mss*44,7:mss,sok,ts,nop,ws:df,id+0
```

```
[ 172.16.77.159/53382 -> 185.230.60.211/80 (mtu) ]
client = 172.16.77.159/53382
link = 以太网或调制解调器
raw_mtu = 1500
```

图 11.6 - 浏览后的 `p0f` 输出

让我们获取更多 IP 地址 185.230.60.211 的信息。在终端窗口中，点击文件 | 新标签页。在新标签页中，输入以下内容：

```
whois 185.230.60.211
```

在下面的输出中，可以看到 IP 指向 `wix.com`，它是 `www.cidr.com` 网站的主机：

```
inetnum: 185.230.60.0 - 185.230.60.255
netname: wix_com_inc
Country: US
adminc-: SP17239-RIPE
tech-: SP17239-RIPE
status: LIR-PARTITIONED PA
mnt-by: il-wicom-sys-mnt
mnt-by: il-wicom-1-mnt
created: 2018-05-21T11:00:58Z
last-modified: 2019-10-10T07:20:09Z
source: RIPE
person: Stanislav Panich
address: Namal Tel Aviv 40
phone: +972 3 5454980
nnic-hdl: SP17239-RIPE
el-wicom-sys-mnt
created: 2018-05-09T15:30:17Z
last-modified: 2018-05-09T15:30:17Z
source: RIPE
```

图 11.7 - `whois` 输出

250 伪迹、恶意软件与勒索软件分析

- 8. 滚动 `pof` 输出以查看其他其他信息，包括服务器的运行时间以及路径上的 IP 地址和跳数：

```
### [ 172.16.77.159/47460 -> 185.230.60.211/443 (uptime) ]-
| server = 185.230.60.211/443
| uptime = 33 days 15 hrs 14 min (modulo 49 days)
| raw_freq = 1003.42
```

```
### [ 172.16.77.159/52308 -> 35.241.16.116/443 (syn) ]-
| client = 172.16.77.159/52308
| os = Linux 2.2.x-3
| dist = 0
| params = generic
| raw_sig = 4:6+0:0:1460:mss,44,7:mss,ts,nop,ws,df,id+:0
```

图 11.8 - 额外的 `pof` 输出

现在我们已经学习了如何安装和使用 `pof` 来检测与我们的设备通信的其他操作系统，让我们转向另一个名为 `swap_digger` 的工具来探索 Linux 伪迹。

## 查看 `swap_digger` 工具以探索 Linux 伪迹

`swap_digger` 对 Linux 交换文件（`swap file`）进行自动分析，并检索系统密码、用户名和表单凭据，甚至是 Wi-Fi 信息（如 SSID），这些信息可能被存储在交换文件中。

### 安装和使用 `swap_digger`

按照以下步骤安装并使用 `swap_digger` 进行交换分析：

- 1. 在终端中切换目录到桌面，并输入以下命令将 `swap_digger` 克隆到桌面：

```
git clone https://github.com/sevagas/swap_digger.git
```

### 查看 `swap_digger` 工具以探索 Linux 伪迹

接下来的截图显示了安装 `swap_digger` 的前一个命令的输出。

```
(kali@kali) ~~/Desktop
$ git clone https://github.com/sevagas/swap_digger.git
Cloning into swap_digger
remote: Enumerating objects: 147, done.
remote: Counting objects: 100 (30/30), done.
remote: Compressing objects: 100 (19/19), done.
remote: Total 147 (delta 15), reused 21 (delta 11), pack-received 117
Receiving objects: 100 (147/147), 357.52 KiB/s, done.
Resolving deltas: 100 (69/69), done.
```
