

# 第15章 攻击者使用的技术

你可以看到 FreeNetEnumerator 提供与 NSAuditor 相同的信息，但格式更易于阅读（见图 15-13）。该工具是为网络枚举方面的初学者设计的。

![](img/b9022ea8d49ef539d37d0ec09f73f71c_427_0.png)

图 15-13 FreeNetEnumerator 结果

这些只是互联网上可用的少量枚举工具。攻击者访问你的网络后，他可以使用这些工具之一来映射网络的其余部分，并了解网络上有哪些计算机、服务器、共享文件夹和用户。他还可以了解每台机器使用的操作系统。这些宝贵的信息让攻击者能够规划他的攻击。

# Nmap

Nmap（网络映射器）是最广泛使用的端口扫描工具。攻击者、网络管理员和渗透测试人员都使用它。它可以从 https://nmap.org/ 免费下载。还有一个图形界面版本 ZenMap。

Nmap 还允许你设置许多标志位（无论是使用 Nmap 的命令行版本还是 Windows 版本）来定制你的扫描。允许的标志位列在此处：

- -O 检测操作系统
- -sP Ping 扫描
- -sT TCP 连接扫描
- -sS SYN 扫描
- -sF FIN 扫描
- -sX Xmas 树扫描
- -sN NULL 扫描
- -sU UDP 扫描
- -sO 协议扫描
- -sA ACK 扫描
- -sW Windows 扫描
- -sR RPC 扫描
- -sL 列表/DNS 扫描
- -sI 空闲扫描
- -Po 不 ping
- -PT TCP ping
- -PS SYN ping
- -PI ICMP ping
- -PB TCP 和 ICMP ping
- -PM ICMP 子网掩码
- -oN 正常输出
- -oX XML 输出
- -oG 可搜索的输出
- -oA 所有输出

时间控制：
- -T0 偏执型 (Paranoid)
- -T1 潜行 (Sneaking)
- -T2 礼貌 (Polite)
- -T3 正常 (Normal)
- -T4 激进 (Aggressive)
- -T5 疯狂 (Insane)

这里是一些非常基础的 Nmap 扫描，从扫描单个 IP 地址开始：

```
nmap 192.168.1.1
```

扫描一个 IP 地址范围：

```
nmap 192.168.1.1-20
```

扫描以检测操作系统，使用 TCP 扫描，并使用潜行速度：

```
nmap -O -PT -T1 192.168.1.1
```

# Shodan.io

这个网站是一个漏洞的搜索引擎。它能发现具有某些漏洞的面向网络的 IP 地址（Web 服务器、路由器等）。你可以在 https://www.shodan.io/ 找到该网站。你需要注册免费账户才能使用它，但对于渗透测试人员来说，识别漏洞是无价之宝。你也可以确定攻击者会充分利用这个网站。你可以在图 15-14 中看到该网站。

![](img/b9022ea8d49ef539d37d0ec09f73f71cc_429_0.png)

图 15-14 Shodan.io

在使用 Shodan.io 搜索时有许多选项可以使用，这里给出了一些：

- 搜索默认密码：
    - default password country:US
    - default password hostname:chuckeastom.com
    - default password city:Chicago
- 查找 Apache 服务器：
  apache city:"San Francisco"
- 查找摄像头：
  webcamxp city:Chicago
  OLD IIS
  "iis/5.0"

上述列表提供了搜索术的示例，包括过滤器。你可以使用的过滤器包括：

- city: 查找特定城市的设备
- country: 查找特定国家的设备
- geo: 根据坐标（即纬度和经度）进行搜索
- hostname: 查找匹配特定主机名的值
- net: 根据 IP 或 /x CIDR 搜索
- os: 根据操作系统搜索
- port: 查找特定的开放端口
- before/after: 在特定时间范围内的结果

例如，图 15-15 显示了我搜索 `default city:Miami` 的结果。

![](img/b9022ea8d49ef539d370ec09f73f71c_430_0.png)

图 15-15 Shodan 搜索结果

当你执行渗透测试时，搜索公司域名以寻找通过 Shodan 可以发现的任何内容是一个好主意。这可以指导你的渗透测试工作，而且你再次可以确定潜在攻击者将使用这个工具。你可以将搜索限制在雇佣你进行渗透测试的客户的主机名或域名。你可以在目标网络中寻找默认密码、旧的 Web 服务器、不安全的摄像头或其他漏洞。

# 手动扫描

还有手动方法可以扫描系统漏洞。也许最常用的是 `telnet` 命令，它在 Linux 或 Windows 中均可用，用于尝试连接到机器以执行管理任务。默认情况下，telnet 使用端口为 23。然而，你可以尝试连接到任何你想要的端口进行 telnet。你只需要打开命令行窗口，输入 `telnet`、你想要连接的地址或 URL 以及端口。

# 物理访问

如果攻击者可以坐在任何机器面前，他有很多方法可以访问网络。

# 绕过密码

一种进入 Windows 的令人兴奋的方法是绕过密码。这基本上需要 Linux 启动盘。以下是步骤：

1. 使用任何 Linux 启动盘，有些人偏好某种发行版，但并不重要。
2. 启动到 CD。
3. 进入 Linux 后，找到并访问 NTFS 分区。以下命令可以实现（注意你的 NTFS 分区可能是 sda）：
```
fdisk -l | grep NTFS
mkdir -p /mnt/windows
mount -t ntfs-3g /dev/sda /mnt/windows
```
4. 进入 System32 目录并放大功能创建备份。如下所示：
```
cd /mnt/windows/Windows/System32
mv Magnify.exe Magnify.bak
```
5. 复制 `cmd.exe`（命令行提示符）并重命名为 `Magnify.exe`。
```
cp cmd.exe Magnify.exe
```
6. 重启进入 Windows（无论哪个版本）。当机器启动时，不要登录，选择辅助选项。

启动的是具有系统权限的命令行提示符。

# 使用 OphCrack

本地进入机器的一种流行工具是 OphCrack，你可以从 http://ophcrack.sourceforge.net/ 下载。它基于对 Windows 密码工作原理的理解。Windows 密码存储在系统目录中的哈希文件中，通常位于 C:\WINDOWS\system32\config 中的安全账户管理器 (SAM) 文件。由于该文件包含哈希值，你无法直接读取用户名和密码。如果你尝试随机密码，大多数系统在几次尝试后锁定你，所以如果你能从 Windows 获取 SAM 文件并尝试破解就太好了。然而，它是一个锁定文件。操作系统不允许你复制或对其进行任何操作。OphCrack 在 Linux 中启动系统，这样 Windows 操作系统就不会加载，SAM 文件也不会受到保护。它使用过程为所有可能的字符组合创建彩虹表。OphCrack 在 SAM 中搜索匹配项。当它找到时，它就知道用户名和密码，如图 15-17 所示。

