

# 使用 Kali Linux 进行 OffSec 渗透测试

72.16:39.9829 192.168.118.4.domain > 192.168.50.645080: 1649 1/0/0 MX
385b015e08dec1277c9af57250ba4.feline.corp 10 (12)
72.17:26.58 192.168.50.493550 > 192.168.118.4.domain : 5278+ [1] MX
c6f0140b6a7ebd06d26193658f0fc.feline.corp (75)
72.17:26.9327 192.168.118.4.domain > 192.168.50.49350: 5272 1/0/0 MX
d5f0a93d3e8b555a88888.feline.corp 40 (126)
72.17:47.0879 192.168.50.645821 > 192.168.118.4.domain : 39215 MX?
c6df7015e08e255662b8f0123f3311.feline.corp. (114)
72.17:40.8397 192.168.50.645821 > 192.168.118.4.domain : 39215 MX?
b395d015e0888dadc6ce55f777250ba4.feline.corp. (106)
72.17:22.5134 192.168.50.47351 > 192.168.118.4.domain : 51139 [TXT]
49e60601b855f9a2f428bf80711c4733de.feline.corp.
72.17:26.1620 192.168.118.4.domain > 192.168.50.49726: 51139 1/0/0 TXT
b8a3d0461e22b0b5b5b3c72233eff8f06c42ea4 (111)
72.18:41.1721 192.168.50.645085 > 192.168.118.4.domain : 52736 [TXT]
c3e605305e8e2c6c2a4f02a0b5dc5.feline.corp. (64)
72.17:24.4190 192.168.118.4.domain > 192.168.50.645085: 52736 1/0/0 TXT
54d105ee9264101d8be1f441f5f77250ba4
72.18:22.7752 192.168.50.640433 > 192.168.118.4.domain : 7172? [TXT]
d3f4a0db6b443d77a79b4c2153ad7d660.feline.corp. (75)
72.18:27.2847 192.168.118.4.domain > 192.168.50.64033: 7172 1/0/0 TXT
17a00005e8f8f66a2c551888f06c42ea4 (111)
72.19:22.4756 192.168.50.645028 > 192.168.118.4.domain : 53513 [CNAME]
d0b1e5d1017e62c6a1a56c5122782bcc.feline.corp. (64)
be6e015e08e2c6c8e262c3a1f4f5dc5.feline.corp. (124)
72.19:35.7212 192.168.118.4.domain > 192.168.50.645085: 52736 1/0/0 TXT
54d105ee9264101d8be1f441f5f77250ba4
72.18:22.7752 192.168.50.640433 > 192.168.118.4.domain : 7172? [TXT]
d3f4a0db6b443d77a79b4c2153ad7d660.feline.corp. (75)
72.18:27.2847 192.168.118.4.domain > 192.168.50.64033: 7172 1/0/0 TXT
17a00005e8f8f66a2c551888f06c42ea4 (111)
72.19:22.4756 192.168.50.645028 > 192.168.118.4.domain : 53513 [CNAME]
d0b1e5d1017e62c6a1a56c5122782bcc.feline.corp. (64)
be6e015e08e2c6c8e262c3a1f4f5dc5.feline.corp. (124)
72.19:35.7212 192.168.118.4.domain > 192.168.50.645085: 52736 1/0/0 TXT
54d105ee9264101d8be1f441f5f77250ba4
72.18:22.7752 192.168.50.640433 > 192.168.118.4.domain : 7172? [TXT]
d3f4a0db6b443d77a79b4c2153ad7d660.feline.corp. (75)
72.18:27.2847 192.168.118.4.domain > 192.168.50.64033: 7172 1/0/0 TXT
17a00005e8f8f66a2c551888f06c42ea4 (111)
72.19:22.4756 192.168.50.645028 > 192.168.118.4.domain : 53513 [CNAME]
d0b1e5d1017e62c6a1a56c5122782bcc.feline.corp. (64)
be6e015e08e2c6c8e262c3a1f4f5dc5.feline.corp. (124)

### 监听器信息

根据帮助输出，listen 的工作方式类似于 ssh-L。我们现在应该已经熟悉它了。让我们尝试通过 DNS 隧道连接到 SHARED 端口。我们将在 FELINEITY 的回环接口上设置本地端口 445，并转发到 HRSHARES。

### 从 FELINEITY 到 PGDATABASE01 的端口转发

来自其他 felineauthority:-$ smclient 的 SMB 共享，其 如下：
- 共享 
- 密码=2345

| 共享名称 | 类型 |
|---|---|
| ADMIN$ | Disk |
| IPC$ | Disk |
| IPC$ | Disk |
| Users$ | Disk |

### Metasploit 框架

在过去的几年中，开发了多个漏洞和后渗透框架，包括 Metasploit、Covenant、Cobalt Strike 和 PowerShell Empire。虽然像 Cobalt Strike 这样的框架是商业性的，但 ...

### 总结

在本模块中，我们涵盖了以下：

- 熟悉 Metasploit
- 使用 Metasploit 攻击负载
- 使用 Metasploit 进行后渗透
- 自动化 Metasploit

Metasploit 框架由 Rapid7 维护，其作者描述为“开发、测试和使用漏洞代码的高级平台”。该项目最初作为一个便携网络框架，后来演变为渗透测试、漏洞开发和漏洞研究的强大工具。该框架已逐渐成为安全领域领先的漏洞收集和开发框架。Metasploit 频繁更新新漏洞，并由 Rapid7 和安全社区不断改进开发。Kali Linux 包含了 metasploit-framework 软件包，其中包含 Metasploit 项目的开源元素。Metasploit 的初学者通常会被 ...

