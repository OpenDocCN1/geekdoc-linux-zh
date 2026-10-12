
# 列表 75 - 查找 nmap SMB NSE 脚本

我们找到了一些有趣的 Nmap SMB NSE 脚本，它们可以执行各种任务，例如通过 SMB 进行操作系统发现和枚举。

> SMB 发现脚本仅在目标上启用 SMBv1 时有效，而这在现代 Windows 版本中并非默认情况。然而，许多旧系统仍在运行 SMBv1，我们已经在 Windows 宿主机上启了这个特定版本以模拟这种场景。

让我们在 Windows 11 客户端上尝试 `smb-os-discovery` 模块。

```
kali@kali:~ nmap -v -p 139,445 --script smb-os-discovery 192.168.50.12
```

```
PORT STATE REASON

139/tcp open netbios-ssn syn-ack

445/tcp open syn-ack

Host script results:

smb-os-discovery:

OS: Windows 10 (6.1)

OS CPE: cpe:windows:10

Computer name: CLIENT01

NetBIOS computer name: CLIENT01

Domain name: megatwo.com

Forest name: megatwo.com

FQDN: client01.megatwo.com

System time: 2022-03-17T11:54:54
```
