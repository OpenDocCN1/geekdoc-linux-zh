
```bash
#!/bin/bash
### 自动捕获 WPA 握包
airmon-ng start wlan0
airodump-ng --bssid <BSSID> -c <channel> -w capture wlan0mon & sleep 5
aireplay-ng --deauth 10 -a <BSSID> wlan0mon
```

### 2. 分布式破解

为了加速 WPA/WPA2 破解，你可以使用 `Hashcat` 或 `John the Ripper` 等工具将破解任务分配到多台机器上，这两个工具在破解大型数据集方面非常高效。

### 3. 将 Aircrack-ng与其他工具集成

对于更高级用法，可以将 `Aircrack-ng` 与用于数据包分析的 `Wireshark` 或用于额外的无线网络检测和监控的 `Kismet` 集成。

## 后渗透技术与横向移动

在渗透测试或真实攻击中获得初始访问后，开始后渗透。此阶段涉及探索受损系统、收集凭据、提升权限、维持访问以及在网络内部横向移动以扩大控制并访问敏感资产。

后渗透的最终目标包括建立持久化、收集情报、提升权限、横向扩散并在最终不被发现的情况下渗透数据。

## 维持访问与持久化

持久化确保攻击者在系统重启或用户注销后仍能保留对受损机器的访问。这一步对于长期利用、数据窃取或远程访问至关重要。

### 1. 常见的持久化技术

#### a. 计划任务 / Cron 任务

在 Windows 和 Linux 系统上，可以调度恶意脚本或可执行文件定期间隔运行。

Windows:

```
schtasks /create /tr "Updater" "C:\evil.exe" /sc minute /mo 5
```

Linux:

```bash
echo "@reboot /usr/bin/evil.sh" >> /etc/crontab
```

#### b. 启动文件夹 / 注册表 Run Keys

攻击者可以将恶意执行文件放入 Windows 启动文件夹或修改注册表项以确保持久化。

注册表：

```reg
reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Run /v "Updater" /t REG_SZ /d "C:\evil.exe"
```

#### c. DLL 劫持与 COM 劫持

破坏系统 DLL 路径或 COM 对象，在执行合法进程期间加载攻击者控制的代码。

#### d. 后门与反弹 Shell

建立一个启动时回拨攻击者系统的反弹 Shell。

- 工具：`Netcat`, `Metasploit` 持久化模块, `ncat`, `Empire`。

#### e. 植入 SSH 密钥

在 Linux 上，向 `.ssh/authorized_keys` 添加公钥可以实现无密码登录。

```bash
echo "ssh-rsa AAAAB3..." >> ~/.ssh/authorized_keys
```

## 权限提升技术

在获得脚点后，攻击者通常以低权限运行。权限提升涉及利用配置错误或漏洞来获取 root 或 SYSTEM 级访问。

### 1. Windows 权限提升

#### a. 利用存在漏洞的服务

寻找以 SYSTEM 权限运行但具有写权限或配置错误的的服务。

- 工具：`accesschk`, `winPEAS`, `PowerUp`

#### b. 未加引号的服务路径

如果服务路径包含空格且未加引号，Windows 将尝试执行它找到的第一个匹配文件。

```
sc qc "Service Name"
```

#### c. 不安全的注册表权限

如果用户可以写入被 SYSTEM 进程使用的注册表项，就可以提升权限。

#### d. 令牌仿充 / 特权令牌

使用劫取或提升的令牌以另一个用户的身份运行命令（例如 NT AUTHORITY\SYSTEM）。

#### e. 利用内核漏洞

已知漏洞如 `MS10-015`、`MS16-032` 或 `PrintNightmare`。

### 2. Linux 权限提升

#### a. Sudo 配置错误

拥有特定二进制文件 sudo 权限的用户可以被利用。

```
-l
```

`sudo` 允许运行 `vim`、`bash`、`perl` 等，这可以导致 root shell。

#### b. SetUID 二进制文件

识别设置了 SetUID 位的可以利用的二进制文件。

```bash
find / -perm -4000 -type f 2>/dev/null
```

#### c. 弱的文件权限

由 root 执行的可写配置文件或脚本可能会被劫持。

#### d. 内核漏洞利用

如 `Linux Exploit Suggester`、`LinPEAS` 或 `dirtycow` 等工具可以利用已知的 Linux 内核漏洞。

## 内部网络中的横向移动

横向移动是指在同一个网络内的一个渗透系统移动到另一个系统，以到达更高价值的目标。

### 1. 凭据重用与哈希传递

一旦获取了用户凭据或密码哈希值，请在其他系统上尝试。

- `Pass-the-Hash`: 使用 `Mimikatz` 或 `pthwinexe` 等工具使用 NTLM 哈希。
- `Pass-the-Ticket`: 重用 Kerberos TGT（黄金票 / 银色票攻击）。

### 2. 远程服务与管理工具

a. Windows:

- `PsExec`: 使用 SMB 和管理员凭据执行远程命令。
- `WMI`: 使用 Windows 管理规范进行远程访问。
- `WinRM` / `PowerShell Remoting`: 通常用于域环境。

b. Linux:

- `SSH`: 重用凭据或密钥访问邻近系统。
- `Rsync`, `NFS`, `SSHFS`: 用于文件移动或远程命令执行。

### 3. 网络枚举

识别其他系统、服务和用户。

- 工具：`BloodHound`, `SharpHound`, `CrackMapExec`, `rpcclient`, `enum4linux`

### 4. 跳板与隧道

使用被渗透的系统作为跳板机或代理，访问未外部暴露的内部资源。

- `SOCKS` 代理：通过 `proxychains` 或 `Metasploit` 跳板实现。

## SSH 隧道

```
ssh -L 9999:target.internal:3389 user@pivot-host
```

## 凭据收集与数据外泄

### 1. 凭据收集

a. `Mimikatz`:

从内存中提取明文密码、哈希、PIN 和 Kerberos 票据。

```
privilege::debug
sekurlsa::logonpasswords
```

b. Windows 库与凭据管理器

使用 `VaultCmd` 或 `Mimikatz` 等工具提取存储的凭据。

c. 浏览器凭据导出

从 Chrome、Firefox、Edge 中收集存储的密码。

d. 记录器与剪贴板抓取

使用脚本或恶意软件捕捉输入的密码或剪贴板内容。

e. 导出 SAM & SYSTEM 注册表单元

```
reg save HKLM\SAM sam.save
reg save HKLM\SYSTEM system.save
```

然后使用 `secretsdump.py` 或 `pwdump`。

### 2. 数据外泄

a. 手动文件提取

复制感兴趣的文件，进行压缩和加密后提取。

```
tar -czf secrets.tar.gz /sensitive/data
```

b. 阶段准备与上传

使用 FTP、SCP、HTTP、DNS 隧道或 C2 通道（例如 `Metasploit Meterpreter`）。

c. 通过云服务或 Web 服务外泄

将数据上传到 Dropbox、Google Drive、Pastebin 或攻击者控制的服务器。

d. 隧道与隐蔽通道

使用 DNS 或 ICMP 等协议在不被发现的情况下将数据传出网络。

## 清除痕迹与反取证策略

为了保持不被发现或阻碍调查人员，攻击者可能会采取**反取证**策略来擦除或隐藏其活动的证据。

### 1. 清除日志

a. Windows

清除事件查看器日志：

```
wevtutil cl System
wevtutil cl Security
```

b. Linux

手动删除日志：

```bash
rm /var/log/auth.log /var/log/syslog
```

- 使用工具覆盖日志或注入伪条目。

### 2. 时间戳修改 (Timestomping)

修改时间戳使文件看起来合法或更老旧。

- 工具：`Metasploit`, `touch`, `SetMACE`

### 3. 隐藏持久化机制

使用无文件恶意软件、仅内存内存负载或加密加载器。

- 隐藏在计划任务、注册表或备用数据流 (ADS) 中。

```
cmd.exe /c echo malicious > file.txt:secret
```
