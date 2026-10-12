
# 教程

## 计算机安全

- 均应用于安全

由于`TensorFlow`积累了经验，一些开源项目被用于利用部分自动化的攻击，这些攻击可以识别入站请求并执行网络攻击。

其中一个项目是`SecIt`（基于`Keras`构建，高层神经网络可以在其上运行）。

`Nmap`扫描带有许多实用的脚本 - 它们的列表请参见`https://nmap.org/nse/`。

我们尽可能倾向于寻找漏洞，而不是与目标进行主动交互。我们利用了`Exploit-DB`，即漏洞与利用数据库(`https://rapid7.db.com/`)。

`Exploit-DB`的一个惊人特点是它有一个用于查询数据库的`bash`脚本`SearchSpot(all, paa0817)`。如果你不确定系统的版本，可以使用`Nmap Audit`来检查漏洞，对`OS`进行审计，然后在所有页面执行扫描。将结果粘贴到这里的“`List of Pages`”中，输入`ls_release -d -f`。现在返回。所有有漏洞的包将带有它们的`CVSS`分数显示。如果你点击它们，将看到你已经在目标上建立了立脚点。然后你可以尝试寻找提升权限的方法，如果你发现由于你的你安装了潜在的漏洞包，你可以使用`Nikto`(`https://github.com/cytolis/nikto`)等工具进行修补，甚至使用必须复制到目标的扫描器，表明事情并不总是那么。

例如，`GitHub`发布了去年由扫描器检测到的漏洞，标记了公共仓库中有漏洞的依赖项：`https://github.com/libjson-c/`

在`recon-recon`内部创建一个工作区，并为工作区`TEST`添加新域名/添加域名`TARGETDOMAIN`。

添加公司名称：`add companies NAME-DESCRIPTION`。然后你需要开始从`TARGETDOMAIN`获取主机来填充`Recon-database`。

使用该模块网站：`use recon-domains/google_site_web`。执行它。运行后，你将获得一个`TARGETDOMAIN`的主机列表。现在通过名称解析所有主机：使用`recon-hosts/resolve`。执行运行。如果需要反查主机的`IP`地址，且存在额外的主机，请使用`recon-hosts/reverse_run`；

最后，让我们使用`census`模块：`use recon-ports/Censys`。由于我们已经收集了`IP`地址，将其查询设置为输出`'hosts'`表的查询结果，如下：`SELECT * FROM hosts WHERE ip_address IS NOT NULL`。最后，执行该模块并运行以完成。

## 快速指南

## 核心渗透测试工具

- 被动发现：`Recon-The Harvest`, `FOCA`
- 主动发现：`nmap`, `WhatWeb`
- 漏洞搜索：`Searchsploit`, `Vulncheck & Exploitation Database`, `LinEnum`
- 暴力破解：`ffuf`, `DirBuster`
- 密码破解：`John the Ripper`, `hashcat`
- 字典列表：`FuzzDB`, `Seclists`, `CrackStation`
- Web 攻击：`ZAP`, `mitmproxy`, `WPScan`, `sqlmap`
- 网络攻击：`arpspo`, `BetterCAP`, `Wireshark`
- 逆向工程：`Gdb`, `radare2`
- 二进制分析：`Radare2(ESIL)`, `Binwalk`, `VirusTotal`, `Firmalyzer`
- 框架：`Metasploit`, `Veil Framework`, `OWASP ZC`, `Word Exploit Framework`

![](img/301dc180ffb6e12d0783cd1567376047_42_0.png)

```
nmap -sV -sC --script all=/usr/share/nmap/scripts/arp-scan.script --script-args=-rate=1000
Starting scan injector.py http://192.168.1.20:8080
Nmap started at 2023-10-27 10:00:00 (CEST+0200)
Target: 192.168.1.0/24
Nmap scan report for 256 hosts (1 host up)
Host: 
192.168.1.20:80/tcp open apache httpd 2.4.41 (Ubuntu)
192.168.1.20:443/tcp open ssl httpd 2.4.41 (Ubuntu)
192.168.1.20:22/tcp open ssh 8.2p1 OpenSSH 8.2p1 Ubuntu
192.168.1.20:139/tcp open smb-windows-net-bi Samba 4.6.18-Ubuntu
192.168.1.20:445/tcp open smb Samba 4.6.18-Ubuntu
192.168.1.20:8080/tcp open http-proxy 2.4.41 (Ubuntu)
Nmap scan completed: 12.45 seconds, 256 IP addresses (1 host up), 0.47% rate)
```

你可以通过查询`recon-database`获取所有端口：显示端口仅列在列表中：`SELECT * FROM ports WHERE port is open`。若要进一步探索：`recon-database`有许多选项可供你轻松扩展其功能。
