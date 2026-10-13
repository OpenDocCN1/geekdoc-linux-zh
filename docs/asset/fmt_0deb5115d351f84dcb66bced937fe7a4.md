
Feb 21 14:43:47 deep Pluto: 'mail' #3: responding to Main Mode

Feb 21 14:43:47 deep Pluto: 'mail' #3: sent MR3, ISAKMP established

Feb 21 14:43:49 deep Pluto: 'mail' #4: responding to Quick Mode

Feb 21 14:43:50 deep Pluto: 'mail' #4: IPsec SA

- 在两个网关上，`/proc/net/`中现在应该存在以下条：

```
[root@]# ls -l /proc/net/ipsec *
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_route
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_klidbug
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_spi
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_spigrp
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_spine
-r-xr--r-- 1 root 0 Feb 02 05:30 /proc/net/ipsec_version
```

IPSEC 接口应该挂载在指定的接口上。通过以下命令确认：

```
[root@]# cat /proc/net/ipsec_tncfg
ipsec0 -> eth0 mtu=1500
ipsec1 -> NULL mtu=0
ipsec2 -> NULL mtu=0
ipsec3 -> NULL mtu=0
```

现在执行以下命令显示最少信息并查看输出是否：

```
[root@]# ipsec look
```

## Socket（网络服务）
第 6 章

```
192.168.1.32 -> 192.168.1.32 esp
ah50894c@192.168.1.2, HMAC; dirout in=32 bits=0xffffff alem=128
life(c,h)+bytes(6140,0)add(5156,0)use(5068,0)packets(115,0,0) idle=99
ah50894c@192.168.1.2, AH, dirout in=32 bits=0xffffff alem=128
```

- 尝试 ping `192.168.1.2` 从 `192.168.1.1` 客户端。如果通了，说明你设置正确。如果不通，请确保 TCP-IP 转发已启用，并且没有防火墙规则拦截数据包，或者对它们进行了伪装。

关于 FreeSWAN 安装的最后一点，如果你遇到了一个无法解决的问题，可以使用以下命令获取一组调试信息（文件内容、日志选取等）相关的 IPSec 加密/认证系统，并发送给 Linux-IPSec 邮件列表 (`linux-ipsec@client.fi`) 寻求帮助。

- 使用以下命令制作调试信息的输出：`[root@]# ipsec bar >` 用于远程调试；这是一个单命令，可以打包所有诊断 IPSec 问题所需的信息。

## 更多文档

- `$ man ipsec (8)`
- `$ man ipsec addr, addaddr (3)`
- `$ man ipsec asors (3)`
- `$ man ipsec atbytes, bytesta (3)`
- `$ man ipsec adata, dalatao (3)`
- `$ man ipsec anseta, satoa (3)`
- - 在 Internet 地址与 ASCII 之间转换
- - 将 ASCII转换为 Internet 地址、子网或范围
- - 将二进制数据与 ASCII 格式之间转换
- - 将 IPSec 安全关联 ID 与 ASCII 之间转换

Copyright 1999 - 2000 Gerhard Mauroni, Open Network Architecture & and OpenDocs Publishing

# 服务器软件（工程网络服务）

## 第 6 章

- `$ man ipsec auto, ultimo (3)`
- `$ man ipsec auto (8)`
- `$ man ipsec barf (8)`
- `$ man ipsec bitomask (3)`
- `$ man ipsec route (8)`
- `$ man ipsec subnet (3)`
- `$ man ipsec hostof (7)`
- `$ man ipsec klipsdebug (8)`
- `$ man ipsec look (8)`
- `$ man ipsec autobits (3)`
- `$ man ipsec optionsfrom (3)`
- `$ man ipsec pluto (8)`
- `$ man ipsec randits (8)`
- `$ man ipsec rangeoa (3)`
- `$ man ipsec raasaikey (8)`
- `$ man ipsec spi (8)`
- `$ man ipsec subgroup (8)`
- `$ man ipsec subnetof (3)`
- `$ man ipsec tncfg (8)`
- `$ man ipsec whack (8)`
- `$ man ipsec conf (5)`
- `$ man ipsec atdoaddr, addroa (3)`
- `$ man ipsec atasser (3)`
- `$ man ipsec alotes, byostec (3)`
- `$ man ipsec indotata, ultimo (3)`
- `$ man ipsec atosa, satoa (3)`
- `$ man ipsec outsetubnet, subnetoa (3)`
- `$ man ipsec auto (8)`
- `$ man barf (8)`
- `$ man bitomask (3)`
- `$ man ipsec goodmask (3)`
- `$ man ipsec hostof (7)`
- `$ man ipsec klipsdebug (8)`
- `$ man ipsec look (8)`
- `$ man ipsec manual (8)`
- `$ man ipsec makbottis (3)`
- `$ man ipsec optionsfrom (3)`
- `$ man ipsec pluto (6)`
- `$ man randits (8)`
- `$ man ipsec rangeota (3)`
- `$ man ipsec raasaikey (8)`
- `$ man ipsec setu (8)`
- `$ man ipsec whiff (8)`
- `$ man ipsec spipgrp (8)`
- `man man ipsec whack (8)`
- 将无符号长整数在 ASCII 之间进行转换
- 控制自动密钥的 IPSEC 连接
- 路由收集 IPSEC 调试信息
- 将位计数转换为 Internet 子网
- 操作 IPSEC 扩展路由表
- Internet 子网掩码是否是有效的？
- 给定 Internet 地址和子网掩码，返回主机部分
- 显示调试信息
- 手动启动和关闭手动密钥的 IPSEC 连接
- 将子网掩码转换为位计数
- 从文件读取额外的“命令行”选项
- IPSEC ike 密钥
- 以 ASCII 形式生成随机位
- 将 Internet 地址范围转换为 ASCII
- 生成 RSA 签名密钥
- 控制 IPSEC 子系统
- 管理 IPSEC 安全关联
- 分组/分组 IPSEC 安全关联
- 给定 Internet 地址和子网掩码，返回子网数量
- 将 IPSEC 虚拟接口与真实接口关联
- 控制 IPSEC ike 守护进程的接口
- IPSEC 配置和连接
- Ike/IPSEC 认证密钥
- 调用实用程序
- 在 Internet 地址和 ASCII 之间进行转换
- 将 ASCII 转换为 Internet 地址、子网或范围
- 将二进制数据字节转换为 ASCII 格式
- 将 IPSEC 安全关联 ID 在 ASCII 之间进行转换
- 将子网掩码在 ASCII 之间进行转换
- 自动密钥的 IPSEC 调试信息
- 操作 IPSEC 扩展路由表
- Internet 子网掩码是否是有效的？

## 安装文件

```
> /etc/rc.d/initd.ipsec
> /etc/rc.d/rc0.K68ipsec
> /etc/rc.d/rc1.K68ipsec
> /usr/share/man/3/ipsec_atoaddr.3
> /usr/share/man/3/ipsec_rangeota.3
> /usr/share/man/3/ipsec_atodata.3
> /etc/rc.rcd2/S47ipsec
> /etc/rc.rcd3/S47ipsec
```
