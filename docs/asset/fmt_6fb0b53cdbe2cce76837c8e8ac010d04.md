
此命令主要是为了方便远程调试，它通过单一命令即可打包（向上并标记标签）所有可能与诊断 IPSEC 问题相关的信息。

## 进一步文档
欲了解更多详细信息，可以阅读以下几个页面：

- `$ ipsec (8)` - 转换 IPSEC 程序
- `$ ipsec ataddr, addroa (3)` - 将 IPSEC 地址转换为 ASCII 或反之
- `$ ipsec atasr (3)` - 转换 IPSEC 互联网地址、子网或范围
- `$ ipsec abytes, bytestoa (3)` - 将二进制数据字节在 ASCII 格式之间转换
- `$ ipsec atdata, dataato (3)` - 将二进制数据在 ASCII 格式之间转换
- `$ ipsec atosa, atosa (7)` - 将 IPSEC 安全关联 ID 转换为 ASCII 或反之
- `$ ipsec atosubnet, subnetoa (3)` - 将子网/掩码 ASCII 形式转换为地址或反之
- `$ ipsec asroup (6)` - 将无符号/符号数字转换为 ASCII 或反之
- `$ ipsec auto (8)` - 控制自动密钥的 IPSEC 连接
- `$ ipsec barf (8)` - 导出调试信息
- `$ ipsec bitmask (3)` - 将 IPSEC 子网转换为位计数
- `$ ipsec secrets (4)` - 守护进程
- `$ ipsec route (8)` - 管理 IPSEC 路由表
- `$ ipsec goodmask (3)` - 此 IPSEC 子网是否有效？
- `$ ipsec hostof (8)` - 给定互联网地址和子网，返回主机
- `$ ipsec klidebug (8)` - 设置内核（支持 IPSEC）调试功能和长度
- `$ ipsec leak (8)` - 显示协商信息
- `$ ipsec manual (8)` - 手动密钥的 IPSEC 连接
- `$ ipsec maskbits (3)` - 将互联网子网掩码转换为位计数
- `$ ipsec optionfrom (3)` - 从命令行读取额外选项
- `$ ipsec ranbits (8)` - 以 ASCII 格式生成随机位
- `$ ipsec rangeato (3)` - 将互联网范围转换为 ASCII
- `$ ipsec raisikey (6)` - 生成 RSA 签名
- `$ ipsec spi (8)` - 管理 IPSEC 子系统
- `$ ipsec spigrp (8)` - 组/升级 IPSEC 安全关联
- `$ ipsec subsetof (7)` - 给定互联网地址和子网，返回子网数量（带真实接口）
- `$ ipsec whack (8)` - 控制 IPSEC 守护进程
- `$ ipsec conf (5)` - IPSEC 配置和连接
- `$ ipsec secrets (5)` - 用于 IKE 的密钥
- `$ ipsec ataddr, addroa (3)` - 将互联网地址转换为 ASCII 或反之
- `$ ipsec atasr (3)` - 将 ASCII 转换为互联网地址、子网或范围
- `$ ipsec abytes, bytestoa (3)` - 将二进制数据在 ASCII 格式之间转换
- `$ ipsec atosa, atosa (7)` - 将 IPSEC 安全关联 ID 转换为 ASCII 或反之
- `$ ipsec atosubnet, subnetoa (3)` - 将子网/掩码 ASCII 形式转换为地址或反之
- `$ ipsec atoul, utloa (3)` - 将无符号/符号数字转换为 ASCII 或反之
- `$ ipsec auto (8)` - 控制自动密钥的 IPSEC 连接
- `$ ipsec barf (8)` - 输出调试信息
- `$ ipsec bitmask (3)` - 将 IPSEC 子网转换为位计数
- `$ ipsec eroute (8)` - ...（剩余列表）
- `$ setw` - 收集 IPSEC 调试信息
- `$` - 互联网子网掩码
- `$ manipulate` - 管理 IPSEC 扩展路由表
- `$` - 此互联网子网掩码有效吗？
- `$` - 给定互联网地址和子网掩码，返回主机
- `$` - 设置内核（支持 IPSEC）调试功能和长度
- `$` - 显示协商信息
- `$` - 手动密钥的 IPSEC 连接和关闭
- `$` - 将互联网子网转换为位计数
- `$` - 从命令行读取额外选项
- `$` - IPSEC 守护进程
- `$` - 管理 IPSEC 安全关联
- `$` - 组/无组的 IPSEC 安全关联
- `$` - 给定互联网地址和子网掩码，返回子网数量（带真实接口）
- `$` - 控制 IPSEC 守护进程
- `$` - IPSEC 配置和连接
- `$` - 用于 IKE/sec 认证的

## 已安装文件
- `/etc/rc.d0/init`
- `/etc/rc.d0/K68ipsec`
- `/etc/rc.d1/K68ipsec`
- `/etc/rc.d2/S47ipsec`
- `/etc/rc.d3/S47ipsec`
- `/etc/rc.d4/S47ipsec`
- `/etc/rc.d5/S47ipsec`
- `/etc/rc.d6/K68ipsec`
- `/etc/ip.conf`
- `/etc/ip.secrets`
- `/usr/lib/ipsec`
- `/usr/lib/spi`
- `/usr/lib/ipsec/eroute`
- `/usr/lib/ipsec/scyp`
- `/usr/lib/ipsec/tncgf`
- `/usr/lib/ipsec/klipsdebug`
- `/usr/lib/ipsec/pluto`
- `/usr/lib/ipsec/whack`
- `/usr/lib/ipsec/`
- `/usr/lib/ipsec/barf`
- `/usr/lib/ipsec/manual`
- `/usr/lib/ipsec/auto`
- `/usr/lib/ipsec/look`
- `/usr/lib/ipsec/showfault`
- `/usr/lib/ipsec/include`
- `/usr/lib/ipsec/read`
- `/usr/lib/ipsec/keyensor`
- `/usr/lib/ipsec/secrector`
- `/usr/lib/ipsec/updown`
- `/usr/lib/ipsec/ranbits`
- `/usr/lib/ipsec/rasigkey`
- `/usr/lib/ipsec/setup`
- `/usr/sbin/ipsec`

© Copyright 1999-2000 Gerard Mourrai and Open Network Architecture ®

## 第 17 章 服务器软件（数据库网络服务）
在本章中

- Linux OpenLDAP 服务器
- 配置
- 保护 OpenLDAP
- OpenLDAP 创建与维护工具
- OpenLDAP 用户工具
- 用于 LDAP 的 Netscape 地址簿客户端

## Linux PostgreSQL 数据库服务器
从你的 Postgres 超用户账户创建数据库
- 配置
- 命令

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_315_0.png)

# Linux OpenLDAP 服务器

## 概述
到目前为止，我们在书中讨论的是安全和优化，那么我们为什么要讨论 OpenLDAP 呢？OpenLDAP 目录服务器通过许多可能性扩展我们的视野。我们可以利用其复制能力，将不同的信息集中到服务器上，供网络中的其他节点使用。想象一下，通过单一操作就可以在专用服务器上禁用 Unix 账户、访问受限 Web 服务器、设置邮件地址以及别名，这就像 NIS 服务的工作方式，但通过 SSL 加密更安全，通过面向对象的层次结构更快速。

正如 Openldap 网站解释过的：
LDAP（轻量级目录访问协议）是一种访问信息服务的开放标准。该协议运行在互联网传输协议（如 TCP）之上，可以访问独立的目录服务器或 X.500 目录。

![](img/4e12ba68f8ecabb49a9835b8d88a1c6d_316_0.png)

## Tar 包
在安装 OpenLDAP 之前对系统文件列列表是一个好习惯，之后使用 `diff` 对它们进行比较，以找出它将文件放在了哪里。只需运行

在安装软件之前，执行 `find /* > ldp1`，在安装后执行 `find /* > ldp2`，然后使用 `diff ldp1 ldp2 > ldp` 来获取变更列表。

## 编译

解压 tar 包 (`tar.gz`)。

```
[root@deep ~]# cp openldap-version.tgz /var/tmp

[root@deep ~]# cd /var/tmp/

[root@deep tmp ~]# tar xzpf openldap-version.tgz
```
