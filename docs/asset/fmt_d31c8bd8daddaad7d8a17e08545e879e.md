
`sudo apt-get update cmake -y`

现在在终端中输入解压和安装类型：

```
tar xvf ettercap*.tar.gz      #解压 ettercap
cd ettercap/                   #进入目录
mkdir build                     #创建新目录
cd build                        #切换到 build/ 目录
cmake                          #使用 cmake 编译 ettercap
make
make install                    #将二进制文件/帮助页和配置安装到系统
```

# 使用 apt-get 在 Debian/Ubuntu 上安装 Ettercap

在终端中运行：
`sudo apt-get install ettercap -y`

# 扫描子网

我将使用2 个工具来演示网络扫描和进一步渗透测试的概念。

- `nmap` - 用于扫描子网并对设备进行进一步的渗透测试
- `Ettercap` - 用于扫描子网并嗅探网络

我们将在 `nmap` 中更详细地学习 `Ettercap`，因为它将向你展示如何扫描和嗅探网络以收集通过器的凭据、如何操作以及应对措施。
让我们开始吧，

## 使用 nmap 扫描子网

在终端中运行：
语法：`nmap <IP地址>/24`

```
nmap 192.168.0.100/24
```

> `192.168.0.100` 是 Kali Linux 的 IP 地址，`/24` 用作掩码即 `255.255.255.0`。检查你的网络配置，它可能有所不同。

此命令将扫描 `192.168.0.1-192.168.0.254` 范围，并输出显示 IP 地址以及设备上运行相应的的服务。
`nmap` 提供了计时选项以减少扫描时间或网络压力，并/规避 IDS（入侵检测系统）。

输出仅在扫描完成后显示，尽管你可以按 `<TAB>` 来检查扫描进度，但一直按 `<TAB>` 并不总是方便的。因此我们使用一些 `nmap` 参数来加速扫描并显示实时输出。

语法：`nmap <IP地址>/24 -T <参数> -v`

这里，`-T` 告诉 `nmap` 使用计时选项，`-v` 代表详细输出
`nmap` 提供了 6 种计时选项。

```
0: 谨慎 (Paranoid)
1: 狡猾 (Sneaky)
2: 礼 (Polite)
3: 正常 (Normal)
4: 激进 (Aggressive)
5: 疯狂 (Insane)
```

```
nmap 192.168.0.100/24 -T 5 -v
```

默认情况下，`nmap` 使用选项 3，即正常扫描。

前两个用于 IDS 检测。礼模式降低扫描速度以使用更少的带宽和目标机器。正常模式是默认设置，因此 `-T3` 无作用。激进模式通过假设你处于一个相当快且可靠的网络中来提高速度。最后，疯狂模式假设你处于一个极快的网络中，或者愿意为了速度牺牲某些准确性。

输出：

```
Nmap scan Report for 192.168.0.1
Host is up (0.023ms latency).
Not shown: 997 closed ports
PORT   STATE SERVICE
80/tcp   open http
1000/tcp open upnp
49152/tcp open unknown
MAC Address: 00:0E:E2:63:5B:B4 (TP-Link Technologies Co.)
Initiating Scan for 192.168.0.1 (1000 ports)
Discovered open ports: 80/tcp, 1000/tcp, 49152/tcp
Scan complete: 0.07 seconds
1000 ports (0 hosts filtered)
```

等待，让我们仔细处理提供的输出以确保没有错误：

```
Nmap scan Report for 192.168.0.1
Host is up (0.023ms latency).
Not shown: 997 closed ports
PORT   STATE SERVICE
80/tcp   open http
1000/tcp open upnp
49152/tcp open unknown
MAC Address: 00:0E:E2:63:5B:B4 (TP-Link Technologies Co.)
Initiating Scan for 192.168.0.1 (1000 ports)
Discovered open ports: 80/tcp, 1000/tcp, 49152/tcp
Scan complete: 0.07 seconds
1000 ports (0 hosts filtered)
```

![](img/ac8a7ada56be8fa0ece47a14bb6f46cd_122_0.png)

`Etercap` 将管理攻击，你只需要监控在下方列显示的输出即可。

当我开始嗅探时，我打开了 Windows 上的浏览器，即受害者 (`192.168.0.102`)，通过 Wi-Fi 连接并打开了路由器 Web 界面 (`192.168.0.1`)，尝试了 3 种“用户名：密码”组合，前两个是错误的，第三个是正确的，我使用正确的凭据登录后就成功了。这在 `Etercap` 窗口中也有输出。

| 删除主机 | 添加到目标 1 | 添加到目标 2 |
| --- | --- | --- |
| 192.168.0.102 7C:E9:D3:30:9F:F1 | | |

```
HTTP:192.168.0.180 -> USER: admin pass: admininf INFO:192.168.0.1/
HTTP:192.168.0.180 -> USER: tester pass: testpass INFO:192.168.0.1/
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/dynaform/common.js
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/localizati/char_set.js
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/dynaform/css_main.css
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/frames/top.htm
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/UserformRpm.htm
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/UserRpm/MenuRpm.htm
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/help/status
HTTP:192.168.0.180 -> USER: root pass: rootshill INFO:192.168.0.1/dynaform/custom.js
```
