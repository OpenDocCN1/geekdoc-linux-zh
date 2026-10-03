
# BTFM：蓝队实战手册

## 前言

BTFM 命令行语法：

| 符号 | 说明 |
| --- | --- |
| `#` | 通用 Linux/*n shell 提示符，sudo 也可以配合 `$` 使用 |
| `C:\>` | Windows 提示符，可能需要管理员权限 CMD 提示符 |
| `PS C:\>` | Windows PowerShell |
| `>` | 通用提示符，多操作系统 |
| `<IP ADDRESS>`, `<PORT>`, `<USER>`, `<PASSWORD>`, 等 | 需要用户确定输入并移除 `<>` 括号 |
| `–` | 注意复制/粘贴时使用破折号/连字符 (en/em/dash ,,- hyphen –) |
| `spaces` | 确保检查检查命令中有空格和无空格的地方。 |

更新、编辑和补充材料：

参考 <http://www.bluetefieldmanual.com>

BTFM 基于 NIST 网络安全框架：

参考 <http://www.nist.gov/cyberframework/>

## 目录

- TCPDUMP
- TSHARK
- SNORT
- 网络捕获 (PCAP) 工具
  - EDITCAP
  - MERGECAP
- 蜜罐技术
  - WINDOWS
  - LINUX
- NETCAT
- 被动 DNS 监控
- 日志审计
  - WINDOWS
  - LINUX

## 4 响应（分析）

### 现场分查 - WINDOWS

- 系统信息
- 用户信息
- 网络信息
- 服务信息
- 策略、补丁和设置信息
- 自启动和自动加载信息
- 日志
- 文件、驱动器和共享信息

### 现场分查 - LINUX

- 系统信息
- 用户信息
- 网络信息
- 服务信息
- 策略、补丁和设置信息
- 日志
- 文件、驱动器和共享信息

### 恶意软件分析

- 静态分析基础
- 识别恶意软件
- 进程管理器
- 文件哈希分析
- 哈希查询
- 硬盘和内存取证
  - WINDOWS
  - LINUX

## 5 恢复（修复）

### 补丁

- WINDOWS
- LINUX

### 备份

- WINDOWS
- LINUX

### 杀死恶意软件进程

- WINDOWS
- LINUX

### OS 秘籍

- WINDOWS
- LINUX

### 解码

### 进制转换

### SNORT

- SNORT 规则

### DOS/DDOS

- 指纹识别 DOS/DDOS

### 工具工具

### 预构建、虚拟机和发行版

### 应急响应清单

- 识别任务
- 遏制任务
- 修复任务
- 其他 / 经验总结任务
- 恶意软件属性清单

### 事件记录与事件共享词汇 (VERIS)

- 概述
- 攻击者
- 行为
- 资产



# 识别（范围）

## 扫描与漏洞

对网络进行 Ping 扫描：

```bash
nmap -sn -PE <IP ADDRESS OR RANGE>
```

扫描并显示开放端口：

```bash
nmap --open <IP ADDRESS OR RANGE>
```

确定开放服务：

```bash
nmap -sV <IP ADDRESS>
```

扫描两个常用的 TCP 端口，HTTP 和 HTTPS：

```bash
nmap -p 80,443 <IP ADDRESS OR RANGE>
```

扫描 UDP 端口 DNS：

```bash
nmap -sU -p 53 <IP ADDRESS OR RANGE>
```

同时扫描 UDP 和 TCP，对单个主机开启详细模式并包含可选的跳过 Ping：

```bash
nmap -v -Pn -sU -sT -p U:53,111,137,T:21-25,80,139,8080 <IP ADDRESS>
```

### NESSUS

基础 Nessus 扫描：

```bash
nessus -q -x -T html <NESSUS SERVER IP ADDRESS> <NESSUS SERVER PORT 1241> <ADMIN ACCOUNT> <ADMIN PASSWORD> <FILE WITH TARGETS>.txt <RESULTS FILE NAME>.html
```

```bash
nessus [-vnh] [-c .rcfile] [-V] [-T format]
```

批量模式扫描：

```bash
nessus -q [-pPPS] <HOST> <PORT> <USER NAME> <PASSWORD> <targets-file> <result-file>
```

## 报告转换

```bash
nessus -i in. [nsr|nbe] -o out. [xml|nsr|nbe|html|txt]
```

### OPENVAS

第 1 步：安装服务器、客户端和插件包：

```bash
apt-get install openvas-server openvas-client openvas-plugins-base openvas-plugins-dfsg
```

第 2 步：更新漏洞数据库

```bash
openvas-nvt-sync
```

第 3 步：添加用户以运行客户端：

```bash
openvas-adduer
```

第 4 步：登录：`sysadm`

第 5 步：身份验证（密码/证书） `[pass]`: `[按回车键]`

第 6 步：登录密码：`<PASSWORD>`

随后你会被要求添加“用户规则”。

第 7 步：通过输入以下内容允许此用户扫描授权网络：

```text
accept <YOUR IP ADDRESS OR RANGE>
default deny
```

第 8 步：输入 `ctrl-D` 退出，然后接受。

第 9 步：启动服务器：

```bash
service openvas-server start
```

第 10 步：设置扫描目标：

创建一个包含要扫描主机/网络列表的文本文件。

```bash
vi scanme.txt
```

第 11 步：每行添加一个主机或网络：

`<IP ADDRESS OR RANGE>`

第 12 步：运行扫描：

```bash
openvas-client -q 127.0.0.1 9390 sysadm nsrc+ws scanme.txt openvas-output-.html -T txt -V -x
```

第 13 步：（可选）使用 HTML 格式运行扫描：

```bash
openvas-client -q 127.0.0.1 9390 sysadm nsrc+ws scanme.txt openvas-output.txt -T html -V -x
```

## WINDOWS

### 网络发现

基础网络发现：

```cmd
net view /all
```

```cmd
net view <HOST NAME>
```

基础 Ping 扫描并将输出写入文件：

```cmd
for /L %I in (1,1,254) do ping -w 30 -n 1 192.168.1.%I | find "Reply" >> <OUTPUT FILE_NAME>.txt
```

### DHCP

启用 DHCP 服务器日志：

```cmd
reg add HKLM\System\CurrentControlSet\Services\DhcpServer\Parameters /v ActivityLogFlag /t REG_DWORD /d 1
```

Windows 2003/2008/2012 默认位置：

```cmd
%windir\System32
```

### DNS

Windows 2003 默认位置：

```cmd
%windir\System32
```

Windows 2008 默认位置：

```cmd
%windir\System32
```

Windows 2012 默认位置：

```cmd
%windir\System32
```

启用 DNS 日志：

```cmd
%windir\System32
```

设置日志文件位置：

```cmd
%windir\System32
```

设置日志文件大小：

```cmd
%windir\System32
```

### 哈希校验 (HASHING)

文件完整性验证器 (FCIV)：

对文件进行哈希：

```cmd
fciv <FILE_PATH>
```

将所有文件哈希到数据库文件中：

```cmd
fciv c -r -md5 -xml
```

列出所有已哈希的文件：

```cmd
fciv -list -sha1 -xml
```

在文件系统中通过数据库验证之前的哈希值：

```cmd
fciv -v -sha1 -xml
```

注意：可能通过命令行创建基准并与所有系统进行对比。快速基线和差异分析。

```powershell
Get-FileHash <FILE TO HASH> | Format-List
```

```cmd
Get-Hash -algorithm md5 <FILE TO HASH>
certutil -hashfile <FILE TO HASH> SHA1
certutil -hashfile <FILE TO HASH> MD5
```

### NETBIOS

基础 nbtstat 扫描：

```cmd
nbtstat -A <IP ADDRESS>
```

缓存的 NETBIOS：

```cmd
nbtstat -A <IP ADDRESS>
```

### USER ACTIVITY

（此处省略重复内容，已在上方翻译）

## 网络发现

Net view 扫描：

```bash
smbtree -b
smbtree -D
smbtree -S
```

查看打开的 SMB 共享：

```bash
smbclient -L <HOST NAME>
smbstatus
```

基础 ping 扫描：

```bash
for ip in $(seq 1 254); do ping -c 1 192.168.1.$ip>/dev/null; [ $? -eq 0 ] && echo "192.168.1.$ip UP" || : ; done
```

### DHCP

查看 DHCP 租日志：

Red Hat 3:

```bash
cat /var/lib/dhcpd/dhcpd.leases
```

Ubuntu:

```bash
grep -Ei 'dhcp' /var/log/syslog.1
```

Ubuntu DHCP 日志：

```bash
tail -f dhcpd.log
```

### DNS

启动 DNS 日志：

```bash
rndc querylog
```

查看 DNS 日志：

```bash
tail -f /var/log/messages | grep named
```

### 哈希处理

对指定位置下的所有可执行文件进行哈希：

```bash
find /<PATHNAME TO ENUMERATE> -type f -exec md5sum {} >> md5sums.txt \
md5deep -rs / > md5sums.txt
```

### NETBIOS

基础 nbtstat 扫描：

```bash
nbtscan <IP ADDRESS OR RANGE>
```

### 密码

密码和用户名猜测或检查：

```bash
while read line; do username=$line; while line; do smbclient -L <TARGET IP ADDRESS> -U $username%$line -g -d 0; echo username:$line; done<<PASSWORDS.txt; done<<USERNAMES.txt
```

# 2 保护（防御）

## 禁用/停止服务

获取服务列表并禁用或停止：

```cmd
sc query
sc config "SERVICE NAME" start= disabled
sc stop "SERVICE NAME"
wmic service where name='<SERVICE NAME>' call ChangeStartmode Disabled
```

## 主机系统防火墙

显示所有规则：

```cmd
netsh advfirewall firewall show rule name=all
```

设置防火墙开启/关闭：

```cmd
netsh advfirewall set currentprofile state on
netsh advfirewall set currentprofile firewallpolicy blockinbound,allowoutbound
netsh advfirewall set publicprofile state on
netsh advfirewall set privateprofile state on
netsh advfirewall set domainprofile state on
netsh advfirewall set allprofile state on
netsh advfirewall set allprofile state off
```

```cmd
netsh advfirewall firewall add rule name="Open Port 80" dir=in action=allow protocol=TCP localport=80
```

```cmd
netsh advfirewall firewall add rule name="My Application" dir=in action=allow program="C:\MyApp\MyApp.exe" enable=yes
```

```cmd
netsh advfirewall firewall add rule name="My Application" dir=in action=allow program="C:\MyApp\MyApp.exe" enable=yes remoteip=157.60.0.1,172.16.0/16,LocalSubnet profile=domain
```

```cmd
netsh advfirewall firewall add rule name="My Application" dir=in action=allow program="C:\MyApp\MyApp.exe" enable=yes remoteip=157.60.0.1,172.16.0/16,LocalSubnet profile=private
```

```cmd
netsh advfirewall firewall delete rule name="rule" program="C:\MyApp\MyApp.exe"
```

```cmd
netsh advfirewall firewall delete rule name="rule" protocol=udp localport=500
```

```cmd
netsh advfirewall firewall set rule group="remote desktop" new enable=Yes profile=domain
```

```cmd
netsh advfirewall firewall set rule group="remote desktop" new enable=No profile=public
```

设置日志位置：

```cmd
netsh advfirewall set currentprofile logging <LOCATION>\<FILENAME>
```

Windows 防火墙日志位置和设置：

```cmd
more %systemroot%\system32\LogFiles\Firewall\pfirewall.log
```

```cmd
netsh advfirewall set allprofile logging maxfilesize 4096
```

```cmd
netsh advfirewall set allprofile logging droppedconnections enable
```

```cmd
netsh advfirewall set allprofile logging allowedconnections enable
```

### 显示防火墙日志

```powershell
$env:systemroot\system32\LogFiles\Firewall\pfirewall.log
```

### 密码

### 更改密码

```cmd
net user <USER NAME> * /domain
```

```cmd
net user <USER NAME> <NEW PASSWORD>
```

### 远程更改密码

参考 <https://technet.microsoft.com/en-us/sysinternals/bb897543>

```cmd
ppasswd.exe \\<IP ADDRESS or NAME OF REMOTE COMPUTER> -u <REMOTE USER NAME> -p <NEW PASSWORD>
```

### 远程更改密码

```powershell
ppasswd.exe \\<IP ADDRESS or NAME OF REMOTE COMPUTER>
```

### HOST 文件

### 刷新恶意域名/IP 的 DNS

```cmd
ipconfig /flushdns
```

### 刷新主机/IP 的 NetBios 缓存

```cmd
nbtstat -R
```

向 hosts 文件添加新的恶意域名并重定向到本地：

```cmd
echo 127.0.0.1 <MALICIOUS DOMAIN> >> C:\Windows\System32\drivers\etc\hosts
```

通过向 127.0.0.1 发送 ping 来检查 hosts 文件是否生效：

```cmd
ping <MALICIOUS DOMAIN> -n 1
```

### 白名单



使用代理自动配置 (PAC) 文件创建坏 URL 或 IP 列表（IE, Firefox, Chrome）：

```javascript
function FindProxyForURL(url
```

### 限制

AppLocker - Server 2008 R2 或 Windows 7 或更高版本：使用 GUI 向导进行配置：

- 可执行文件规则 (`.exe`, `.com`)
- DLL 规则 (`.dll`, `.ocx`)
- 脚本规则 (`.ps1`, `.bat`, `.cmd`, `.vbs`, `.js`)
- Windows 安装规则 (`.msi`, `.msp`, `.mst`)

### 采用 AppLocker 的步骤（数字签名应用限制需要 GUI）：

步骤 1：创建一个新的 GPO。

步骤 2：右键点击该项进行编辑，然后导航到计算机配置、策略、Windows 设置、安全设置、应用控制策略和 AppLocker。

点击“配置规则实施”。

步骤 3：在“可执行文件规则”下，勾选“强制规则”。

步骤 4：在左窗格中，点击“可执行文件规则”。

步骤 5：右键选择“新建规则”。

步骤 6：在“条件”屏幕上，点击“下一步”。

步骤 7：在“权限”屏幕上，点击“下一步”。

步骤 8：使用“浏览”按钮选择任何可执行文件。

步骤 9：点击“下一步”。

步骤 10：如果是你第一次创建 AppLocker 策略，Windows 将提示你创建。

步骤 11：确保 AppLocker 服务正在运行。

步骤 12：使用 AppLocker 策略测试是否允许“Everyone”组的员运行 `calc.exe` 和 `notepad.exe`。如果未指定组，则默认使用“Everyone”组。

### 显示任何本地规则的 GridView 列表：

```
PS C:\> Get-AppLockerPolicy -Local -Xml | OutGridView
```

### IPSEC

创建一个 IPSEC 本安全策略，适用于任何连接、任何协议并使用预共享密钥：

```
C:\> netsh ipsec static add filter filterlist=MyIPsecFilter srcaddr=Any dstaddr=Any protocol=ANY
```

```
C:\> netsh ipsec static add filteraction name=MyIPsecAction action=negotiate
```

```
C:\> netsh ipsec static add policy name=MyIPsecPolicy assign=yes
```

```
C:\> netsh ipsec static add rule name=MyIPsecRule policy=MyIPsecPolicy filterlist=MyIPsecFilter filteraction=MyIPsecAction conntype=all activate=yes k=<PASSWORD>
```

添加规则以允许通过 IPSEC 访问网页浏览端口 80 (HTTP) 和 443 (HTTPS)：

```
C:\> netsh ipsec static add filteraction name=Allow action=permit
```

```
C:\> netsh ipsec static add filter filterlist=WebFilter srcaddr=Any dstaddr=Any protocol=TCP dstport=80
```

```
C:\> netsh ipsec static add filter filterlist=WebFilter srcaddr=Any dstaddr=Any protocol=TCP dstport=443
```

```
C:\> netsh ipsec static add rule name=WebAllow policy=MyIPsecPolicy filterlist=WebFilter filteraction=Allow conntype=all activate=yes k=<PASSWORD>
```

### 显示名为 "MyIPsecPolicy" 的 IPSEC 本地安全策略：

```
C:\> netsh ipsec static show policy name=MyIPsecPolicy
```

### 停止或取消 IPSEC 策略：

```
C:\> netsh ipsec static set policy name=MyIPsecPolicy
```

### 创建一个适用于任何连接的 IPSEC 高级防火墙规则、策略以及预共享密钥：

```
C:\> netsh advfirewall consec add rule name="IPSEC" endpoint1=any endpoint2=any action=requireinrequireout qmsecethods=default
```

### 在所有出站请求上要求 IPSEC 预共享密钥：

```
C:\> netsh advfirewall firewall add rule name="IPSEC_Out" dir=out action=allow enable=yes profile=any localip=any remoteip=any protocol=any interfacetype=any security=authenticate
```

### 创建一个用于网页浏览的规则：

```
C:\> netsh advfirewall firewall add rule name="Allow Outbound Port 80" dir=out localport=80 protocol=TCP action=allow
```

### 创建一个 DNS 规则：

```
C:\> netsh advfirewall firewall add rule name="Allow Outbound Port 53" dir=out localport=53 protocol=UDP action=allow
```

## 删除 ISPEC 规则：

```
C:\> netsh advfirewall firewall delete rule name="IPSEC_RULE"
```

活动目录 (AD) – 组策略对象 (GPO)

### 获取并强制更新新策略：

```
C:> gpupdate /force
C:> gpupdate /sync
```

对用户 Bob 进行成功和失败审计：

```
C:> auditpath /set /user:bob /category:"Detailed Tracking" /include /success:enable /failure:enable
```

创建一个组织单元 (OU)，用于移动可疑或受感染的用户和机器：

```
C:> dsadd ou <QUARANTINE BAD OU>
```

将活动目录用户对象移动到新组：

```
PS C:\> Move-ADObject 'CN=<USER NAME>,CN=<OLD USER GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>' -TargetPath 'OU=<NEW GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>'
```

替代选项：

```
C:\> smove "CN=<USER NAME>,OU=<OLD USER OU>,DC=DOMAIN,DC=<OLD EXTENSION>" -newparent OU=<NEW GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>
```

### 不带活动目录 (AD) 的独立系统

禁止运行 .exe 文件：

```
C:\> reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer /v DisallowRun /t REG_DWORD /d 00000001 /f
```

```
C:\> reg add HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\DisallowRun /v badfile.exe /t REG_DWORD /d <BAD FILE NAME>.exe /f
```

禁用远程桌面：

```
C:\> reg add HKLM\SYSTEM\CurrentControlSet\Control\TerminalServer" /v fDenyTSConnections /t REG_DWORD /d 1
```

### 仅发送 NTLM2 响应/拒绝 LM 和 NTLM：

(Windows 7 默认)

```
C:\> reg add HKLM\SYSTEM\CurrentControl\Control\Lsa\ /v lmcompatibilitylevel /t REG_DWORD /d 5 /f
```

### 限制匿名访问：

```
C:\> reg add HKLM\SYSTEM\CurrentControl\Control\Lsa /v restrictanonymous /t REG_DWORD /d 1 /f
```

不允许对 SAM 账户和共享进行匿名枚举：

```
C:\> reg add HKLM\SYSTEM\CurrentControl\Control\Lsa /v restrictanomoussam /t REG_DWORD /d 1 /f
```

### 禁用 IPv6：

```
C:\> reg add HKLM\SYSTEM\CurrentControl\services\TCPIP6\Parameters / DisabledComponents /t REG_DWORD /d 255 /f
```

### 禁用粘滞键：

```
C:\> reg add "HKCU\Control Panel\Accessibility\StickyKeys" /v Flags /t REG_SZ /d 506 /f
```

### 禁用备切换键：

```
C:\> reg add "HKCU\Control Panel\Accessibility\ToggleKeys" /v Flags /t REG_SZ /d 58 /f
```

### 禁用过滤键：

```
C:\> reg add "HKCU\Control Panel\Accessibility\Keyboard Response" /v Flags /t REG_SZ /d 122 /f
```

### 禁用屏幕键盘：

```
C:\> reg add "HKCU\Control Panel\Accessibility\StickyKeys" /v Flags /t REG_SZ /d 506 /f
```

将活动目录用户对象移动到新组：

```
PS C:\> Move-ADObject 'CN=<USER NAME>,CN=<OLD USER GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>' -TargetPath 'OU=<NEW GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>'
```

将活动目录用户对象移动到新组：

```
PS C:\> Move-ADObject 'CN=<USER NAME>,CN=<OLD USER GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>' -TargetPath 'OU=<NEW GROUP>,DC=<OLD DOMAIN>,DC=<OLD EXTENSION>'
```

列出所有当前 iptables 规则：

```
### iptables -L
```

清空所有当前 iptables 规则：

```
### iptables -F
```

启动/停止 iptables 服务：

```
### service iptables start
```

```
### service iptables stop
```

启动/停止 ufw 服务：

```
### ufw enable
```

```
### ufw disable
```

启动/停止 ufw 日志：

```
### ufw logging on
```

```
### ufw logging off
```

备份所有当前 ufw 规则：

```
### cp /lib/ufw/{user.rules,user6.rules} /<备份路径>
```

```
### cp /lib/ufw/{user.rules,user6.rules} ./
```

简单的防火墙 (ufw) 命令示例（IP、IP 范围、端口封锁）：

```
### ufw status verbose
```

```
### ufw delete <RULE #>
```

```
### ufw allow for <IP ADDRESS>
```

```
### ufw allow all 80/tcp
```

```
### ufw allow all ssh
```

```
### ufw deny from <BAD IP ADDRESS> proto udp to any port 443
```

### 密码

更改密码：

```
$ passwd (针对当前用户)
$ passwd bob (针对用户 Bob)
$ sudo su passwd (针对 root)
```

### HOST 文件

向 hosts 文件添加新的恶意域名，并路由到本地：

```
### echo 127.0.0.1 <MALICIOUS DOMAIN> >> /etc/hosts
```

通过向 127.0.0.1 发送 ping 检查 hosts 文件是否生效：

```
### ping -c 1 <MALICIOUS DOMAIN>
```

Ubuntu/Debian DNS 缓存刷新：

```
### /etc/init.d/dns-clean start
```

四种方式刷新 nscd DNS 缓存：

```
### /etc/init.d/nscd restart
### service nscd restart
### service nscd reload
### nscd -i hosts
```

刷新 dnsmasq DNS 缓存：

```
### /etc/init.d/dnsmasq restart
```

### 白名单

使用代理自动配置 (PAC) 文件创建坏 URL 或 IP 列表：

```javascript
function FindProxyForURL(url, host) {
  // 将坏的 DNS 名称发送到代理
  if (dnsDomainIs(host, ".badsite.com")) {
    return PROXY http://127.0.0.1:8080;
  }
  // 将坏 IP发送到代理
  if (isInet(myIPAddress), "222.222.222.222", "255.255.255.0") {
    return PROXY http://127.0.0.1:8080;
  }
  // 所有其他流量绕过代理
  return "DIRECT"
}
```

### IPSEC

允许防火墙通过 IPSEC 流量：

- `# iptables -A INPUT -p esp -j ACCEPT`
- `# iptables -A INPUT -p ah -j ACCEPT`
- `# iptables -A INPUT -p udp --dport 500 -j ACCEPT`
- `# iptables -A INPUT -p udp --dport 4500 -j ACCEPT`

通过 IPSEC 流量：

步骤 1：在 `<HOST1 IP ADDRESS>` 和 `<HOST2 IP ADDRESS>` 上安装 Racoon 工具以在 Ubuntu 中启用 IPSEC 隧道。

- `# apt-get install racoon`

步骤 2：选择直接并编辑 `<HOST1 IP ADDRESS>` 和 `<HOST2 IP ADDRESS>` 上的 `/etc/ipsec-tools.conf`。

```
flush;
spdflush;
```

```
spdadd <HOST1 IP ADDRESS> <HOST2 IP ADDRESS> any -P out ipsec esp/transport//require;
spdadd <HOST2 IP ADDRESS> <HOST1 IP ADDRESS> any -P in ipsec esp/transport//require;
```

步骤 3：在 `<HOST1 IP ADDRESS>` 和 `<HOST2 IP ADDRESS>` 上编辑 `/etc/racoon/racoon.conf`。



```
log notify;
path pre_shared_key "/etc/racoon/psk.txt";
path certificate "/etc/racoon/certs";
remote anonymous {
  exchange_mode main,aggressive;
  proposal {
    encryption_algorithm aes_256;
    hash_algorithm sha256;
    authentication_method
    pre_shared_key;
    dh_group modp1024;
  }
  generate_policy off;
}
sainfo anonymous{
  pfs_group 2;
  encryption_algorithm aes_256;
  authentication_algorithm hmac_sha256;
  compression_algorithm deflate;
}
```

### 4：在两个主机上添加预共享密钥

在 HOST1 上：

```
### echo <HOST2 IP ADDRESS> <PRESHRED PASSWORD>
>>/etc/racoon/psk.txt
```

在 HOST2 上：

```
### echo <HOST1 IP ADDRESS> <PRESHRED PASSWORD>
>>/etc/racoon/psk.txt
```

### 5：在两个系统上重启服务

```
### service setkey restart
```

检查安全关联、配置和策略：

```
### setkey -D
```

```
### setkey -DP
```

## 3 探测（可见性）

## 网络监控

### TCPDUMP

查看 ASCII (`-A`) 或 HEX (`-X`) 流量：

```
### tcpdump -A
### tcpdump -X
```

查看带有时间戳且不转换地址并详细输出的流量：

```
### tcpdump -tttt -n -vv
```

在 1000 个数据包后找到流量最大的主机（潜在的 DDoS）：

```
### tcpdump -nn -c 1000 | awk '{print $3}' | cut -d - -f1-4 | sort -n | uniq -c | sort -nr
```

从目标主机和特定端口在任何接口上捕流量并输出到文件：

```
### tcpdump -w <FILENAME>.pcap -i any dst <TARGET IP ADDRESS> and port 80
```

仅查看两个主机之间的流量：

```
### tcpdump host 10.0.0.1 && host 10.0.0.2
```

查看除某个主机以外的所有流量：

```
### tcpdump not net 10.10 && not host 192.168.1.2
```

查看主机或两个主机中的一个：

```
### tcpdump host 10.10.10 && host 10.10.20
```

按循环大小保存 pcap 文件：

```
### tcpdump -n -s65535 -C 1000 -w host_%Y-%m-%d_%H:%M:%S.pcap
```

### 将 pcap 文件保存到远程主机

```
### tcpdump -w - | ssh <REMOTE HOST ADDRESS> cat >/tmp/remapture.pcap
```

获取包含单词 "pass" 的流量：

```
### tcpdump -n -A -s0 | grep pass
```

获取多个明文协议流量：

```
### tcpdump -n -A -s0 port http or port ftp or smtp or pop3 | egrep -i pass=|login=|username|=password|user|color --auto -buffered
```

获取吞吐量：

```
### tcpdump -w - | pv /dev/null
```

过滤 ipv6 流量：

```
### tcpdump not ipv6
```

过滤 ipv4 流量：

```
### tcpdump ip6
```

每小时捕获多个接口的 tcpdump 到文件的脚本：

```bash
#!/bin/bash
tcpdump -ni any -s65535 -G 3600 -w any_%Y-%m-%d_%H:%M:%S.pcap
```

将多个 tcpdump 文件移动到备位置的脚本：

```bash
#!/bin/bash
while true; do
  sleep 1;
  rsync -az --progress <USER>@<IP>:<DESTINATION>
done
```

### 寻找可疑和自签名 SSL 证书

```
### tshark -r -A '(tcp[12:1] & 0xf0):5:1 = 0x16'
```

### 获取 SSL 证书

```
### openssl s_client -connect <URL>:443 </dev/null | sed -ne '/BEGIN CERTIFICATE/,/-END CERTIFICATE/' > <CERT>.pem
```

### 检查并验证证书是否为自签名

```
### openssl x509 -text -in <CERT>.pem
```

```
### openssl x509 -text -in <CERT>.pem
```

### SNORT

对 snort 配置文件运行测试：

- `snort -T -c <PATH TO SNORT>/snort/snort.conf`

使用 snort(v=详细模式,d=导出数据包负载):

- `snort -dv -r <LOG FILE NAME>.log`

重放日志文件并匹配 icmp 流量：

- `snort -dvr packet.log icmp`

ASCII 格式的日志：

- `snort -K ascii -l <LOG DIRECTORY>`

二进制格式的日志：

- `snort -l <LOG DIRECTORY>`

将事件发送到控制台：

- `snort -q -A console -i eth0 -c /etc/snort/snort.conf`
- `snort -c snort.conf -l /tmp/so/console -A console`

创建单条 snort 规则并保存：

- `echo alert any any <SNORT RULE> > one.rule`

测试单条规则：

- `snort -T -c one.rule`

运行单条规则并输出到控制台和日志目录：

- `mkdir /logs`
- `snort -vd -c one.rule -r <PCAP FILE NAME>.pcap -A console -l logs`

# 网络捕获 (PCAP) 工具

### EDITCAP

用于编辑 pcap 文件（拆分为 1000 个数据包）：

```
> editcap -F pcap -c 1000 orginal.pcap out_split.pcap
```

用于编辑 pcap 文件（按每 1 小时拆分数据包）：

```
> editcap -F pcap -t+3600 orginal.pcap out_split.pcap
```

### MERGECAP

用于合并多个 pcap 文件：

```
> mergecap -w merged_cap.pcap cap1.pcap cap2.pcap cap3.pcap
```

### 蜜罐技术

#### WINDOWS

Windows 蜜罐端口：

参考自：http://securityweekly.com/wp-content/uploads/2013/06/howtogetbetterpentest.pdf

第 1 步：针对连接到端口 3333 的任何内容创建新的 TCP 防火墙阻止规则：

```
C:\> echo @echo off for /L %i in (1,1,1) do @for /f "tokens=3" %j in ('netstat -nao ^| find "^3333^"') do @for /f "tokens=1 delims=:" %k in ("%j") do netsh advfirewall firewall add rulename="HONEY TOKEN RULE" dir=in remoteip=%k localport=any protocol=TCP action=block >> BATCH FILE>.bat
```

第 2 步：运行批处理脚本

```
C:\> <BATCH FILE NAME>.bat
```

Windows 蜜罐端口 PowerShell 脚本：

参考：https://github.com/Pwdrkeg/honeyport/blob/master/honeyport.ps1

第 1 步：下载 PowerShell 文件脚本：

```
C:\> "%ProgramFiles%\Internet Explorer\iexpl.exe" https://github.com/Pwdrkeg/honeyport/blob/master/honeyport.ps1
```

第 2 步：运行 PowerShell 脚本：

```
C:\> honeyport.ps1
```

#### Windows 蜜罐哈希（也用于检测 Mimikatz 使用）

参考：https://isc.sans.edu/forums/diary/Detecting+Mimikatz+Use+On+Your+Network/19311/

第 1 步：创建虚假的蜜罐哈希。注意输入虚假密码并保持命令提示符打开以保持密码在内存中

```
C:\> runas /user:yourdomain.com\fakeadministratoraccount /netnoly cmd.exe
```

第 2 步：查询远程访问尝试：

```
C:\> weevutil q System /q:"*[System[(EventID=20274)]" /f:text /rd:true /c:1 /r:remotecomputename
```

第 3 步：查询失败登录尝试：

```
C:\> weevutil q Security /q:"*[System[(EventID=4624 or EventID=4625)]" /f:text /rd:true /c:5 /r:remotecomputename
```

第 4 步：（可选）在无限循环中运行查询并暂停 30 秒：

```
C:\> for /L %i in (1,0,2) do (Insert Step 2) & (Insert Step 3) & timeout 30
```

#### LINUX

Linux 蜜罐端口：

参考自：http://securityweekly.com/wp-content/uploads/2013/06/howtogetterbetterpent.pdf

第 1 步：运行 while 循环以创建 TCP 防火墙规则，阻止任何连接到端口 2222 的主机：

```bash
while [ 1 ] ; echo "started"; do IP=`nc -v -l -p 2222 2>&1 1 >/dev/null | grep from | cut -d' ' -f6
```

# Linux 蜜罐端口：

```bash
iptables -A INPUT -p tcp --dport 2222 -s $IP -j DROP
```

```cmd
C:\> auditpol /set /subcategory:"User Account Management" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Computer Account Management" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Security Group Management" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Distribution Group Management" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Application Group Management" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Other Account Management Events" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Directory Service Changes" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Directory Service Replication" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Detailed Directory Service Replication" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Directory Service Access" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Kerberos Service Ticket Operations" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Other Account Logon Events" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Kerberos Authentication Service" /success:enable /failure:enable
```

```cmd
C:\> auditpol /set /subcategory:"Credential Validation" /success:enable /failure:enable
```

检查可用日志列表、大小、保留限制：

```powershell
PS C:\> Get-EventLog
```

## 需要监控的关键安全日志审计事件部分列表

```powershell
PS C:\> Get-EventLog -newest 5 -logname application
Format-List
```

显示来自远程系统的日志：

```powershell
PS C:\> Get-EventLog -computername <SERVER NAME>
```

根据事件 ID 获取特定的事件列表：

```powershell
PS C:\> Get-EventLog Security | ? {$_.EventId -eq 4800}
```

```powershell
PS C:\> Get-WinEvent -FilterHashtable @{LogName="Security"; ID=4774}
```

账户登录 - 审计过去 14 天的凭据验证：

```powershell
PS C:\> Get-EventLog Security 4768,4771,4772,4769,4770,4649,4778,4779,4800,4801,52803,5378,5632,5633 -after ((get-date).addDays(-14))
```

账户 - 登录/注销：

```powershell
PS C:\> Get-EventLog Security 4625,4634,4647,4624,4625,4648,4675,6272,6273,6274,6275,6276,6277,6278,6279,6280,4649,4778,4779,4800,4801,4802,4803,5378,5632,5633,4964 -after ((get-date).addDays(-1))
```

账户管理 - 审计应用组：

```powershell
PS C:\> Get-EventLog Security 4783,4784,4785,4786,4787,4788,4789,4790,4741,4742,4743,4744,4745,4746,4747,4748,4749,4750,4751,4752,4753,4759,4760,4761,4762,4783,4727,4728,4729,4730,4731,4732,4733,4734,4735,4737,4754,4755,4756,4757,4765,4764,4724,4722,4723,4724,4725,4726,4738,4740,4765,4766,4767,4780,4781,4794,5376,5377 -after ((get-date).addDays(-1))
```



## 详细跟踪 - 审计 DPAPI 活动、进程终止、RPC 事件

```powershell
PS C:\> Get-EventLog Security 4692,4693,4694,4695,4689,5712 -after ((get-date).addDays(-1))
```

## 域服务访问 - 审计目录服务访问

```powershell
PS C:\> Get-EventLog Security 4662,5136,5137,5138,5139,5141 -after ((get-date).addDays(-1))
```

## 对象访问 - 审计文件共享、文件系统、SAM、注册表、证书

```powershell
PS C:\> Get-EventLog Security 4671,4698,4699,4700,4701,4702,5148,5149,5888,5890,4657,5039,4659,4660,4661,4663,4656,4658,4690,4874,4875,4880,4881,4882,4884,4885,4888,4890,4891,4992,4895,4896,4898,5145,5140,5152,5143,5144,5168,5140,5143,5144,5168,5140,5142,5143,5144,5168,4664,4985,5152,5153,5031,5140,5150,5151,5155,5156,5157,5158 -after ((get-date).addDays(-1))
```

## 策略更改 - 审计策略更改、微软保护服务、Windows 过滤平台



```powershell
PS C:\> Get-EventLog Security 4715,4719,4817,4902,4904,4905,4906,4907,4908,4912,47716,4707,4718,4739,4771,4772,4773,4774,4775,4776,4777,4778,4779,4780,4781,4782,4783,4784,4785,4786,4787,4788,4789,4790,4791,4792,4793,4794,4795,4796,4797,4798,4799,4800,4801,4802,4803,4804,4805,4806,4807,4808,4809,4810,4811,4812,4813,4814,4815,4816,4817,4818,4819,4820,4821,4822,4823,4824,4825,4826,4827,4828,4829,4830,4831,4832,4833,4834,4835,4836,4837,4838,4839,4840,4841,4842,4843,4844,4845,4846,4847,4848,4849,4850,4851,4852,4853,4854,4855,4856,4857,4858,4859,4860,4861,4862,4863,4864,4865,4866,4867,4868,4869,4870,4871,4872,4873,4874,4875,4876,4877,4878,4879,4880,4881,4882,4883,4884,4885,4886,4887,4888,4889,4890,4891,4892,4893,4894,4895,4896,4897,4898,4899,4900,4901,4902,4903,4904,4905,4906,4907,4908,4909,4910,4911,4912,4913,4914,4915,4916,4917,4918,4919,4920,4921,4922,4923,4924,4925,4926,4927,4928,4929,4930,4931,4932,4933,4934,4935,4936,4937,4938,4939,4940,4941,4942,4943,4944,4945,4946,4947,4948,4949,4950,4951,4952,4953,4954,4955,4956,4957,4958,4959,4960,4961,4962,4963,4964,4965,4966,4967,4968,4969,4970,4971,4972,4973,4974,4975,4976,4977,4978,4979,4980,4981,4982,4983,4984,4985,4986,4987,4988,4989,4990,4991,4992,4993,4994,4995,4996,4997,4998,4999,5000,5001,5002,5003,5004,5005,5006,5007,5008,5009,5010,5011,5012,5013,5014,5015,5016,5017,5018,5019,5020,5021,5022,5023,5024,5025,5026,5027,5028,5029,5030,5031,5032,5033,5034,5035,5036,5037,5038,5039,5040,5041,5042,5043,5044,5045,5046,5047,5048,5049,5050,5051,5052,5053,5054,5055,5056,5057,5058,5059,5060,5061,5062,5063,5064,5065,5066,5067,5068,5069,5070,5071,5072,5073,5074,5075,5076,5077,5078,5079,5080,5081,5082,5083,5084,5085,5086,5087,5088,5089,5090,5091,5092,5093,5094,5095,5096,5097,5098,5099,5100,5101,5102,5103,5104,5105,5106,5107,5108,5109,5110,5111,5112,5113,5114,5115,5116,5117,5118,5119,5120,5121,5122,5123,5124,5125,5126,5127,5128,5129,5130,5131,5132,5133,5134,5135,5136,5137,5138,5139,5140,5141,5142,5143,5144,5145,5146,5147,5148,5149,5150,5151,5152,5153,5154,5155,5156,5157,5158,5159,5160,5161,5162,5163,5164,5165,5166,5167,5168,5169,5170,5171,5172,5173,5174,5175,5176,5177,5178,5179,5180,5181,5182,5183,5184,5185,5186,5187,5188,5189,5190,5191,5192,5193,5194,5195,5196,5197,5198,5199,5200,5201,5202,5203,5204,5205,5206,5207,5208,5209,5210,5211,5212,5213,5214,5215,5216,5217,5218,5219,5220,5221,5222,5223,5224,5225,5226,5227,5228,5229,5230,5231,5232,5233,5234,5235,5236,5237,5238,5239,5240,5241,5242,5243,5244,5245,5246,5247,5248,5249,5250,5251,5252,5253,5254,5255,5256,5257,5258,5259,5260,5261,5262,5263,5264,5265,5266,5267,5268,5269,5270,5271,5272,5273,5274,5275,5276,5277,5278,5279,5280,5281,5282,5283,5284,5285,5286,5287,5288,5289,5290,5291,5292,5293,5294,5295,5296,5297,5298,5299,5300,5301,5302,5303,5304,5305,5306,5307,5308,5309,5310,5311,5312,5313,5314,5315,5316,5317,5318,5319,5320,5321,5322,5323,5324,5325,5326,5327,5328,5329,5330,5331,5332,5333,5334,5335,5336,5337,5338,5339,5340,5341,5342,5343,5344,5345,5346,5347,5348,5349,5350,5351,5352,5353,5354,5355,5356,5357,5358,5359,5360,5361,5362,5363,5364,5365,5366,5367,5368,5369,5370,5371,5372,5373,5374,5375,5376,5377,5378,5379,5380,5381,5382,5383,5384,5385,5386,5387,5388,5389,5390,5391,5392,5393,5394,5395,5396,5397,5398,5399,5400,5401,5402,5403,5404,5405,5406,5407,5408,5409,5410,5411,5412,5413,5414,5415,5416,5417,5418,5419,5420,5421,5422,5423,5424,5425,5426,5427,5428,5429,5430,5431,5432,5433,5434,5435,5436,5437,5438,5439,5440,5441,5442,5443,5444,5445,5446,5447,5448,5449,5450,5451,5452,5453,5454,5455,5456,5457,5458,5459,5460,5461,5462,5463,5464,5465,5466,5467,5468,5469,5470,5471,5472,5473,5474,5475,5476,5477,5478,5479,5480,5481,5482,5483,5484,5485,5486,5487,5488,5489,5490,5491,5492,5493,5494,5495,5496,5497,5498,5499,5500,5501,5502,5503,5504,5505,5506,5507,5508,5509,5510,5511,5512,5513,5514,5515,5516,5517,5518,5519,5520,5521,5522,5523,5524,5525,5526,5527,5528,5529,5530,5531,5532,5533,5534,5535,5536,5537,5538,5539,5540,5541,5542,5543,5544,5545,5546,5547,5548,5549,5550,5551,5552,5553,5554,5555,5556,5557,5558,5559,5560,5561,5562,5563,5564,5565,5566,5567,5568,5569,5570,5571,5572,5573,5574,5575,5576,5577,5578,5579,5580,5581,5582,5583,5584,5585,5586,5587,5588,5589,5590,5591,5592,5593,5594,5595,5596,5597,5598,5599,5600,5601,5602,5603,5604,5605,5606,5607,5608,5609,5610,5611,5612,5613,5614,5615,5616,5617,5618,5619,5620,5621,5622,5623,5624,5625,5626,5627,5628,5629,5630,5631,5632,5633,5634,5635,5636,5637,5638,5639,5640,5641,5642,5643,5644,5645,5646,5647,5648,5649,5650,5651,5652,5653,5654,5655,5656,5657,5658,5659,5660,5661,5662,5663,5664,5665,5666,5667,5668,5669,5670,5671,5672,5673,5674,5675,5676,5677,5678,5679,5680,5681,5682,5683,5684,5685,5686,5687,5688,5689,5690,5691,5692,5693,5694,5695,5696,5697,5698,5699,5700,5701,5702,5703,5704,5705,5706,5707,5708,5709,5710,5711,5712,5713,5714,5715,5716,5717,5718,5719,5720,5721,5722,5723,5724,5725,5726,5727,5728,5729,5730,5731,5732,5733,5734,5735,5736,5737,5738,5739,5740,5741,5742,5743,5744,5745,5746,5747,5748,5749,5750,5751,5752,5753,5754,5755,5756,5757,5758,5759,5760,5761,5762,5763,5764,5765,5766,5767,5768,5769,5770,5771,5772,5773,5774,5775,5776,5777,5778,5779,5780,5781,5782,5783,5784,5785,5786,5787,5788,5789,5790,5791,5792,5793,5794,5795,5796,5797,5798,5799,5800,5801,5802,5803,5804,5805,5806,5807,5808,5809,5810,5811,5812,5813,5814,5815,5816,5817,5818,5819,5820,5821,5822,5823,5824,5825,5826,5827,5828,5829,5830,5831,5832,5833,5834,5835,5836,5837,5838,5839,5840,5841,5842,5843,5844,5845,5846,5847,5848,5849,5850,5851,5852,5853,5854,5855,5856,5857,5858,5859,5860,5861,5862,5863,5864,5865,5866,5867,5868,5869,5870,5871,5872,5873,5874,5875,5876,5877,5878,5879,5880,5881,5882,5883,5884,5885,5886,5887,5888,5889,5890,5891,5892,5893,5894,5895,5896,5897,5898,5899,5900,5901,5902,5903,5904,5905,5906,5907,5908,5909,5910,5911,5912,5913,5914,5915,5916,5917,5918,5919,5920,5921,5922,5923,5924,5925,5926,5927,5928,5929,5930,5931,5932,5933,5934,5935,5936,5937,5938,5939,5940,5941,5942,5943,5944,5945,5946,5947,5948,5949,5950,5951,5952,5953,5954,5955,5956,5957,5958,5959,5960,5961,5962,5963,5964,5965,5966,5967,5968,5969,5970,5971,5972,5973,5974,5975,5976,5977,5978,5979,5980,5981,5982,5983,5984,5985,5986,5987,5988,5989,5990,5991,5992,5993,5994,5995,5996,5997,5998,5999,6000,6001,6002,6003,6004,6005,6006,6007,6008,6009,6010,6011,6012,6013,6014,6015,6016,6017,6018,6019,6020,6021,6022,6023,6024,6025,6026,6027,6028,6029,6030,6031,6032,6033,6034,6035,6036,6037,6038,6039,6040,6041,6042,6043,6044,6045,6046,6047,6048,6049,6050,6051,6052,6053,6054,6055,6056,6057,6058,6059,6060,6061,6062,6063,6064,6065,6066,6067,6068,6069,6070,6071,6072,6073,6074,6075,6076,6077,6078,6079,6080,6081,6082,6083,6084,6085,6086,6087,6088,6089,6090,6091,6092,6093,6094,6095,6096,6097,6098,6099,6100,6101,6102,6103,6104,6105,6106,6107,6108,6109,6110,6111,6112,6113,6114,6115,6116,6117,6118,6119,6120,6121,6122,6123,6124,6125,6126,6127,6128,6129,6130,6131,6132,6133,6134,6135,6136,6137,6138,6139,6140,6141,6142,6143,6144,6145,6146,6147,6148,6149,6150,6151,6152,6153,6154,6155,6156,6157,6158,6159,6160,6161,6162,6163,6164,6165,6166,6167,6168,6169,6170,6171,6172,6173,6174,6175,6176,6177,6178,6179,6180,6181,6182,6183,6184,6185,6186,6187,6188,6189,6190,6191,6192,6193,6194,6195,6196,6197,6198,6199,6200,6201,6202,6203,6204,6205,6206,6207,6208,6209,6210,6211,6212,6213,6214,6215,6216,6217,6218,6219,6220,6221,6222,6223,6224,6225,6226,6227,6228,6229,6230,6231,6232,6233,6234,6235,6236,6237,6238,6239,6240,6241,6242,6243,6244,6245,6246,6247,6248,6249,6250,6251,6252,6253,6254,6255,6256,6257,6258,6259,6260,6261,6262,6263,6264,6265,6266,6267,6268,6269,6270,6271,6272,6273,6274,6275,6276,6277,6278,6279,6280,6281,6282,6283,6284,6285,6286,6287,6288,6289,6290,6291,6292,6293,6294,6295,6296,6297,6298,6299,6300,6301,6302,6303,6304,6305,6306,6307,6308,6309,6310,6311,6312,6313,6314,6315,6316,6317,6318,6319,6320,6321,6322,6323,6324,6325,6326,6327,6328,6329,6330,6331,6332,6333,6334,6335,6336,6337,6338,6339,6340,6341,6342,6343,6344,6345,6346,6347,6348,6349,6350,6351,6352,6353,6354,6355,6356,6357,6358,6359,6360,6361,6362,6363,6364,6365,6366,6367,6368,6369,6370,6371,6372,6373,6374,6375,6376,6377,6378,6379,6380,6381,6382,6383,6384,6385,6386,6387,6388,6389,6390,6391,6392,6393,6394,6395,6396,6397,6398,6399,6400,6401,6402,6403,6404,6405,6406,6407,6408,6409,6410,6411,6412,6413,6414,6415,6416,6417,6418,6419,6420,6421,6422,6423,6424,6425,6426,6427,6428,6429,6430,6431,6432,6433,6434,6435,6436,6437,6438,6439,6440,6441,6442,6443,6444,6445,6446,6447,6448,6449,6450,6451,6452,6453,6454,6455,6456,6457,6458,6459,6460,6461,6462,6463,6464,6465,6466,6467,6468,6469,6470,6471,6472,6473,6474,6475,6476,6477,6478,6479,6480,6481,6482,6483,6484,6485,6486,6487,6488,6489,6490,6491,6492,6493,6494,6495,6496,6497,6498,6499,6500,6501,6502,6503,6504,6505,6506,6507,6508,6509,6510,6511,6512,6513,6514,6515,6516,6517,6518,6519,6520,6521,6522,6523,6524,6525,6526,6527,6528,6529,6530,6531,6532,6533,6534,6535,6536,6537,6538,6539,6540,6541,6542,6543,6544,6545,6546,6547,6548,6549,6550,6551,6552,6553,6554,6555,6556,6557,6558,6559,6560,6561,6562,6563,6564,6565,6566,6567,6568,6569,6570,6571,6572,6573,6574,6575,6576,6577,6578,6579,6580,6581,6582,6583,6584,6585,6586,6587,6588,6589,6590,6591,6592,6593,6594,6595,6596,6597,6598,6599,6600,6601,6602,6603,6604,6605,6606,6607,6608,6609,6610,6611,6612,6613,6614,6615,6616,6617,6618,6619,6620,6621,6622,6623,6624,6625,6626,6627,6628,6629,6630,6631,6632,6633,6634,6635,6636,6637,6638,6639,6640,6641,6642,6643,6644,6645,6646,6647,6648,6649,6650,6651,6652,6653,6654,6655,6656,6657,6658,6659,6660,6661,6662,6663,6664,6665,6666,6667,6668,6669,6670,6671,6672,6673,6674,6675,6676,6677,6678,6679,6680,6681,6682,6683,6684,6685,6686,6687,6688,6689,6690,6691,6692,6693,6694,6695,6696,6697,6698,6699,6700,6701,6702,6703,6704,6705,6706,6707,6708,6709,6710,6711,6712,6713,6714,6715,6716,6717,6718,6719,6720,6721,6722,6723,6724,6725,6726,6727,6728,6729,6730,6731,6732,6733,6734,6735,6736,6737,6738,6739,6740,6741,6742,6743,6744,6745,6746,6747,6748,6749,6750,6751,6752,6753,6754,6755,6756,6757,6758,6759,6760,6761,6762,6763,6764,6765,6766,6767,6768,6769,6770,6771,6772,6773,6774,6775,6776,6777,6778,6779,6780,6781,6782,6783,6784,6785,6786,6787,6788,6789,6790,6791,6792,6793,6794,6795,6796,6797,6798,6799,6800,6801,6802,6803,6804,6805,6806,6807,6808,6809,6810,6811,6812,6813,6814,6815,6816,6817,6818,6819,6820,6821,6822,6823,6824,6825,6826,6827,6828,6829,6830,6831,6832,6833,6834,6835,6836,6837,6838,6839,6840,6841,6842,6843,6844,6845,6846,6847,6848,6849,6850,6851,6852,6853,6854,6855,6856,6857,6858,6859,6860,6861,6862,6863,6864,6865,6866,6867,6868,6869,6870,6871,6872,6873,6874,6875,6876,6877,6878,6879,6880,6881,6882,6883,6884,6885,6886,6887,6888,6889,6890,6891,6892,6893,6894,6895,6896,6897,6898,6899,6900,6901,6902,6903,6904,6905,6906,6907,6908,6909,6910,6911,6912,6913,6914,6915,6916,6917,6918,6919,6920,6921,6922,6923,6924,6925,6926,6927,6928,6929,6930,6931,6932,6933,6934,6935,6936,6937,6938,6939,6940,6941,6942,6943,6944,6945,6946,6947,6948,6949,6950,6951,6952,6953,6954,6955,6956,6957,6958,6959,6960,6961,6962,6963,6964,6965,6966,6967,6968,6969,6970,6971,6972,6973,6974,6975,6976,6977,6978,6979,6980,6981,6982,6983,6984,6985,6986,6987,6988,6989,6990,6991,6992,6993,6994,6995,6996,6997,6998,6999,7000,7001,7002,7003,7004,7005,7006,7007,7008,7009,7010,7011,7012,7013,7014,7015,7016,7017,7018,7019,7020,7021,7022,7023,7024,7025,7026,7027,7028,7029,7030,7031,7032,7033,7034,7035,7036,7037,7038,7039,7040,7041,7042,7043,7044,7045,7046,7047,7048,7049,7050,7051,7052,7053,7054,7055,7056,7057,7058,7059,7060,7061,7062,7063,7064,7065,7066,7067,7068,7069,7070,7071,7072,7073,7074,7075,7076,7077,7078,7079,7080,7081,7082,7083,7084,7085,7086,7087,7088,7089,7090,7091,7092,7093,7094,7095,7096,7097,7098,7099,7100,7101,7102,7103,7104,7105,7106,7107,7108,7109,7110,7111,7112,7113,7114,7115,7116,7117,7118,7119,7120,7121,7122,7123,7124,7125,7126,7127,7128,7129,7130,7131,7132,7133,7134,7135,7136,7137,7138,7139,7140,7141,7142,7143,7144,7145,7146,7147,7148,7149,7150,7151,7152,7153,7154,7155,7156,7157,7158,7159,7160,7161,7162,7163,7164,7165,7166,7167,7168,7169,7170,7171,7172,7173,7174,7175,7176,7177,7178,7179,7180,7181,7182,7183,7184,7185,7186,7187,7188,7189,7190,7191,7192,7193,7194,7195,7196,7197,7198,7199,7200,7201,7202,7203,7204,7205,7206,7207,7208,7209,7210,7211,7212,7213,7214,7215,7216,7217,7218,7219,7220,7221,7222,7223,7224,7225,7226,7227,7228,7229,7230,7231,7232,7233,7234,7235,7236,7237,7238,7239,7240,7241,7242,7243,7244,7245,7246,7247,7248,7249,7250,7251,7252,7253,7254,7255,7256,7257,7258,7259,7260,7261,7262,7263,7264,7265,7266,7267,7268,7269,7270,7271,7272,7273,7274,7275,7276,7277,7278,7279,7280,7281,7282,7283,7284,7285,7286,7287,7288,7289,7290,7291,7292,7293,7294,7295,7296,7297,7298,7299,7300,7301,7302,7303,7304,7305,7306,7307,7308,7309,7310,7311,7312,7313,7314,7315,7316,7317,7318,7319,7320,7321,7322,7323,7324,7325,7326,7327,7328,7329,7330,7331,7332,7333,7334,7335,7336,7337,7338,7339,7340,7341,7342,7343,7344,7345,7346,7347,7348,7349,7350,7351,7352,7353,7354,7355,7356,7357,7358,7359,7360,7361,7362,7363,7364,7365,7366,7367,7368,7369,7370,7371,7372,7373,7374,7375,7376,7377,7378,7379,7380,7381,7382,7383,7384,7385,7386,7387,7388,7389,7390,7391,7392,7393,7394,7395,7396,7397,7398,7399,7400,7401,7402,7403,7404,7405,7406,7407,7408,7409,7410,7411,7412,7413,7414,7415,7416,7417,7418,7419,7420,7421,7422,7423,7424,7425,7426,7427,7428,7429,7430,7431,7432,7433,7434,7435,7436,7437,7438,7439,7440,7441,7442,7443,7444,7445,7446,7447,7448,7449,7450,7451,7452,7453,7454,7455,7456,7457,7458,7459,7460,7461,7462,7463,7464,7465,7466,7467,7468,7469,7470,7471,7472,7473,7474,7475,7476,7477,7478,7479,7480,7481,7482,7483,7484,7485,7486,7487,7488,7489,7490,7491,7492,7493,7494,7495,7496,7497,7498,7499,7500,7501,7502,7503,7504,7505,7506,7507,7508,7509,7510,7511,7512,7513,7514,7515,7516,7517,7518,7519,7520,7521,7522,7523,7524,7525,7526,7527,7528,7529,7530,7531,7532,7533,7534,7535,7536,7537,7538,7539,7540,7541,7542,7543,7544,7545,7546,7547,7548,7549,7550,7551,7552,7553,7554,7555,7556,7557,7558,7559,7560,7561,7562,7563,7564,7565,7566,7567,7568,7569,7570,7571,7572,7573,7574,7575,7576,7577,7578,7579,7580,7581,7582,7583,7584,7585,7586,7587,7588,7589,7590,7591,7592,7593,7594,7595,7596,7597,7598,7599,7600,7601,7602,7603,7604,7605,7606,7607,7608,7609,7610,7611,7612,7613,7614,7615,7616,7617,7618,7619,7620,7621,7622,7623,7624,7625,7626,7627,7628,7629,7630,7631,7632,7633,7634,7635,7636,7637,7638,7639,7640,7641,7642,7643,7644,7645,7646,7647,7648,7649,7650,7651,7652,7653,7654,7655,7656,7657,7658,7659,7660,7661,7662,7663,7664,7665,7666,7667,7668,7669,7670,7671,7672,7673,7674,7675,7676,7677,7678,7679,7680,7681,7682,7683,7684,7685,7686,7687,7688,7689,7690,7691,7692,7693,7694,7695,7696,7697,7698,7699,7700,7701,7702,7703,7704,7705,7706,7707,7708,7709,7710,7711,7712,7713,7714,7715,7716,7717,7718,7719,7720,7721,7722,7723,7724,7725,7726,7727,7728,7729,7730,7731,7732,7733,7734,7735,7736,7737,7738,7739,7740,7741,7742,7743,7744,7745,7746,7747,7748,7749,7750,7751,7752,7753,7754,7755,7756,7757,7758,7759,7760,7761,7762,7763,7764,7765,7766,7767,7768,7769,7770,7771,7772,7773,7774,7775,7776,7777,7778,7779,7780,7781,7782,7783,7784,7785,7786,7787,7788,7789,7790,7791,7792,7793,7794,7795,7796,7797,7798,7799,7800,7801,7802,7803,7804,7805,7806,7807,7808,7809,7810,7811,7812,7813,7814,7815,7816,7817,7818,7819,7820,7821,7822,7823,7824,7825,7826,7827,7828,7829,7830,7831,7832,7833,7834,7835,7836,7837,7838,7839,7840,7841,7842,7843,7844,7845,7846,7847,7848,7849,7850,7851,7852,7853,7854,7855,7856,7857,7858,7859,7860,7861,7862,7863,7864,7865,7866,7867,7868,7869,7870,7871,7872,7873,7874,7875,7876,7877,7878,7879,7880,7881,7882,7883,7884,7885,7886,7887,7888,7889,7890,7891,7892,7893,7894,7895,7896,7897,7898,7899,7900,7901,7902,7903,7904,7905,7906,7907,7908,7909,7910,7911,7912,7913,7914,7915,7916,7917,7918,7919,7920,7921,7922,7923,7924,7925,7926,7927,7928,7929,7930,7931,7932,7933,7934,7935,7936,7937,7938,7939,7940,7941,7942,7943,7944,7945,7946,7947,7948,7949,7950,7951,7952,7953,7954,7955,7956,7957,7958,7959,7960,7961,7962,7963,7964,7965,7966,7967,7968,7969,7970,7971,7972,7973,7974,7975,7976,7977,7978,7979,7980,7981,7982,7983,7984,7985,7986,7987,7988,7989,7990,7991,7992,7993,7994,7995,7996,7997,7998,7999
```

```cmd
```



# Windows 现场取证命令参考

## 系统服务与进程信息

```cmd
C:\> net start
C:\> sc query
C:\> wmic service list brief | findstr "Running"
C:\> wmic service list config
C:\> wmic process list brief
C:\> wmic process list status
C:\> wmic process list memory
C:\> wmic job list brief
```

```powershell
PS C:\> Get-Service | Where-Object { $_.Status -eq "running" }
```

```powershell
# 所有进程列表以及所有加载的模块
PS C:\> Get-Process | select modules | ForEach-Object { $_.modules }
```

## 策略、补丁与设置信息

```cmd
C:\> set
C:\> gpresult /r
C:\> gpresult /z > <OUTPUT NAME>.txt
C:\> gpresult /H report.html /F
C:\> wmic qfe
```

列出 GPO 安装的软件：

```cmd
C:\> reg query "HKLM\Software\Microsoft\Windows\CurrentVersion\Group Policy\AppMgmt"
```

# 自动运行与自动加载信息

## 启动信息

```cmd
C:\> wmic startup list full
C:\> wmic ntdomain list brief
```

## 查看启动文件夹目录内容

```cmd
C:\> dir "%SystemDrive%\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
C:\> dir "%SystemDrive%\Documents and Settings\All Users Start Menu\Programs\Startup"
C:\> dir %userprofile%\Start Menu\Programs\Startup
C:\> dir "%ProgramFiles%\Startup\"
C:\> dir C:\Windows\Start Menu\Programs\startup
C:\> dir "%Users%\username%\AppData\Roaming\Microsoft\Windows\Start Menu\Programs\Startup"
C:\> dir "C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"
C:\> dir "%APPDATA%\Microsoft\Windows\Start Menu\Programs\Startup"
C:\> dir "%ALLUSERPROFILE%\Microsoft\Windows\Start Menu\Programs\Startup"
C:\> dir "%ALLUSERPROFILE%\Start Menu\Programs\Startup"
C:\> type C:\Windows\winstart.bat
C:\> type %windir%\wininit.ini
C:\> type %windir%\win.ini
```

## 查看自动运行项，隐藏微软文件

参考：https://technet.microsoft.com/en-us/sysinternals/bb963902.aspx

```cmd
C:\> autorunsc -accepteula -m
C:\> type C:\Autoexec.bat
```

## 显示所有自动运行文件，导出到 CSV 并使用 VirusTotal 检查

```cmd
C:\> autorunsc.exe -accepteula -a -c -i -e -f -l -m -v
```

## 注册表自动运行键值查询

### HKEY_CLASSES_ROOT

```cmd
C:\> reg query HKCR\Comfile\Shell\Open\Command
C:\> reg query HKCR\Batfile\Shell\Open\Command
C:\> reg query HKCR\htafile\Shell\Open\Command
C:\> reg query HKCR\Exfile\Shell\Open\Command
C:\> reg query HKCR\Exefile\Shell\Open\Command
C:\> reg query HKCR\piffile\shell\open\command
```

### HKEY_CURRENT_USER

```cmd
C:\> reg query "HKCU\Control Panel\Desktop"
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Run
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Runonce
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\RunOnceEx
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\RunServices
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\RunServicesOnce
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Windows\Run
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Windows\Load
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Windows\Scripts
C:\> reg query "HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows" /f run
C:\> reg query "HKCU\Software\Microsoft\Windows NT\CurrentVersion\Windows" /f load
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RecentDocs
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedMRU
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSaveMRU
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\LastVisitedPidMRU
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\ComDlg32\OpenSavePidMRU /s
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\RunMRU
C:\> reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"
C:\> reg query "HKCU\Software\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders"
C:\> reg query HKCU\Software\Microsoft\Windows\CurrentVersion\Applets\RegEdit /v LastKey
C:\> reg query "HKCU\Software\Microsoft\Internet Explorer\TypedUrls"
C:\> reg query "HKCU\Software\Policies\Microsoft\Windows\Control Panel\Desktop"
```

### HKEY_LOCAL_MACHINE

```cmd
C:\> reg query "HKLM\SOFTWARE\Microsoft\Active Setup\Installed Components" /s
C:\> reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\User Shell Folders"
C:\> reg query "HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\Shell Folders"
C:\> reg query HKLM\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellExecuteHooks
C:\> reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects" /s
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\Explorer\Run
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Run
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Runonce
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\RunOnceEx
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Services
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\ServicesOnce
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Winlogon
C:\> reg query HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\ShellServiceObjectDelayLoad
C:\> reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Tasks"
C:\> reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Schedule"
C:\> reg query "HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\AppInit"
C:\> reg query "HKLM\SOFTWARE\Microsoft\WinRun"
```

## 列出加载的未签名 DLL

参考：https://technet.microsoft.com/en-us/sysinternals/bb896656.aspx

```cmd
C:\> listdlls.exe -u
C:\> listdlls.exe -u <PROCESS NAME OR PID>
```

## 离线恶意软件扫描 (Windows Defender)

参考：http://windows.microsoft.com/en-us/windows/what-is-windows-defender-offline

```cmd
C:\> MpCmdRun.exe -SignatureUpdate
C:\> MpCmdRun.exe -Scan
```

# 现场取证 – LINUX

## 系统信息

```bash
# uname -a
# uptime
# timedatectl
# mount
```

## 用户信息

查看已登录的用户：

```bash
# w
```

显示用户是否曾远程登录过：

```bash
# lastlog
# last
```

查看失败的登录记录：

```bash
# faillog -a
```

查看本地用户账户：

```bash
# cat /etc/passwd
# cat /etc/shadow
```

查看本地组：

```bash
# cat /etc/group
```

查看 sudo 权限：

```bash
# cat /etc/sudoers
```

查看 UID 为 0 的账户：

```bash
# awk -F: '$3 == "0" {print $1}' /etc/passwd
```

查看 root 用户的 SSH 密钥认证：

```bash
# cat /root/.ssh/authorized_keys
```

列出用户打开的文件：

```bash
# lsof -u <USER NAME>
```

查看 root 用户的 bash 历史记录：

```bash
# cat /root/.bash_history
```

## 网络信息

```bash
# ifconfig
# netstat -ant
# netstat
# route
# arp
# lsof -i
```

## 服务信息

```bash
# ps -aux
# lsmod
# lsof
# lsof -n | cut -f1 -d' '
# lsof -c <SERVICE NAME>
# lsof -p <PID>
# lsof -L
# ls -al /proc/<PID>/exe
# cp /proc/<PID>/exe /tmp/<SUSPICIOUS_FILE>.elf
# tail -F /var/log/messages
# systemctl list-units --type=service
```

## 策略与设置

```bash
# cat /etc/pam.d/common-*
# crontab -l
# crontab -u root -l
# cat /etc/cron.*
# cat /root/.bash_history
# last
```

## 文件、驱动器和共享信息

```bash
# df -ah
# ls -la /etc/init.d
# stat <FILE NAME>
# file <FILE NAME>
# lsattr -R /
# ls -la /root
# ls -alt | head
# find / -type d -perm -0002 -a -print
# find / -newermt 2017-01-02
# find / -printf "%m %AT\n"
# ls -alt <DIRECTORY>
# stat <FILE PATH>/<SUSPICIOUS_FILE>
# file <FILE PATH>/<SUSPICIOUS_FILE>
```

## Rootkit 检测工具

### 运行 unix-privsec-check

```bash
wget https://raw.githubusercontent.com/pentestmonkey/unix-privsec-check/master/unix-privsec-check
chmod +x unix-privsec-check
./unix-privsec-check > output.txt
```

### 运行 chkrootkit

```bash
# apt-get install chkrootkit
# chkrootkit
```

### 运行 rkhunter

```bash
# apt-get install rkhunter
# rkhunter --update
# rkhunter --check
```

### 运行 tiger

```bash
# apt-get install tiger
# tiger
# less /var/log/tiger/security.report
```



### 运行 lynis

```bash
apt-get install lynis
```

```bash
lynis audit system
```

```bash
more /var/log/lynis.log
```

### 运行 Linux恶意软件检测 (LMD)

```bash
wget http://www.rfx.com/downloads/maldet-current.tar.gz
```

```bash
tar xfz maldetect-current.tar.gz
```

```bash
cd maldetect-*
```

```bash
./install.sh
```

获取 LMD 更新：

```bash
maldetect -u
```

在目录上运行 LMD 扫描：

```bash
maldetect -a <DIRECTORY>
```

### 恶意软件分析

#### 静态分析基础

挂载实时 Sysinternals 工具驱动器：`\\live.sysinternals.com\tools`

dll、exe 文件的签名检查：
参考. http://technet.microsoft.com/en-us/sysinternals/bb897441.aspx

```cmd
C:\>sigcheck.exe -u -e C:\<DIRECTORY>
```

发送到 VirusTotal：

```cmd
C:\>sigcheck.exe -vt <SUSPICIOUS_FILE_NAME>
```

#### Windows PE 分析

查看 PE(exe 或任何文件) 的十六进制和 ASCII，可选参数 `-n` 显示前 500 字节：

```bash
hexdump -C -n 500 <SUSPICIOUS_FILE_NAME>
```

```bash
od -x somefile.exe
```

```bash
xxd somefile.exe
```

在 Windows 中使用调试工具（同样适用于 `.java` 文件）：

```cmd
C:\>debug <SUSPICIOUS_FILE_NAME>
> -d (只需输入 d 即可逐页获取十六进制)
> -q (退出调试器)
```

#### Windows PE 分析：Perl 脚本获取 PE 文件日期

下面是 PE 文件日期的 perl 脚本（仅适用于 Windows PE）。
参考. https://www.perl.org/get.html
参考. http://www.perlmonks.org/bare/?node_id=484287

```perl
#!/usr/bin/perl
use strict;
use warnings;
use File::Basename;

my $file = $ARGV[0] or die "Usage: $0 <file>\n";
open(my $fh, '<', $file) or die "Could not open $file: $!";
my $header = read($fh, my $buffer, 64);
die "File too small" if length($buffer) < 64;
my ($magic, $machine, $num_sections, $time_date) = unpack("V4", $buffer);
printf("Magic: 0x%X\n", $magic);
printf("Machine: 0x%X\n", $machine);
printf("Sections: %d\n", $num_sections);
printf("Timestamp: %s\n", localtime($time_date));
close($fh);
```

*(注：perl 脚本的 OCR 文本严重损坏；我根据常见的 PE 头重建了逻辑，但原始文本大部分不可读)。*

#### 查看 VirusTotal 结果列

### 步骤 5：停止并移除恶意软件

- 针对任何识别出的可疑进程，右键点击并选择挂起（Suspend）
- 右键点击并选择终止之前的挂起进程（Terminate Previous Suspended processes）

### 步骤 6：清理恶意文件重启时自动启动的地方

- 启动 `Autoruns`，勾选验证代码签名（Verify Code Signatures）和隐藏微软条目（Hide Microsoft entries）
- 在“全部”（everything）选项卡中查找之前步骤中的可疑进程文件并取消勾选。取消勾选比删除安全，以防发生错误。
- 按 `F5` 刷新 `Autoruns`，并确认恶意文件没有重新创建到之前取消勾选的自动启动项。

### 步骤 7：进程监视 (Process Monitor)

参考 https://technet.microsoft.com/en-us/sysinternals/processmonitor.aspx

- 如果恶意活动仍然持续，运行 `Process Monitor`。
- 寻找在之前的步骤终止后不久重新启动的新进程。

### 步骤 8：根据需要重复操作，以找到所有恶意文件和进程，并可能与其他工具和套件结合。

## 文件哈希分析 (FILE HASH ANALYSIS)

### 哈希查询 (HASH QUERY)

VirusTotal 在线 API 查询：

参考 https://www.virustotal.com/documentation/public-api/（前提：需要 VT API Key）

使用 CURL 将可疑哈希发送到 VirusTotal：

```bash
curl -v --request POST --url 'https://www.virustotal.com/vtapi/v2/file/report' -d apikey=<VT API KEY> -d 'resource=<SUSPICIOUS FILE HASH>'
```

使用 CURL 将可疑文件发送到 VirusTotal：

```bash
curl -v -F 'file=<PATH TO FILE>/<SUSPICIOUS FILE NAME>' -F apikey=<VT API KEY> https://www.virustotal.com/vtapi/v2/file/scan
```

Team Cymru API：

参考 https://hash.cymru.com, http://totalhash.com

使用 whois 进行 Team Cymru 恶意软件哈希查询：（注：输出为最后可见的时间戳和检测率）

```bash
whois -h hash.cymru.com <SUSPICIOUS FILE HASH>
```

### 硬盘和内存获取 (HARD DRIVE AND MEMORY ACQUISITION)

#### WINDOWS

远程创建内存转储：
参考 http://kromer.pl/malware-analysis/memory-forensics-using-volatility-toolkit-to-extract-malware-samples-from-memory-dump/
参考 http://sourceforge.net/projects/mdd/
参考 http://technet.microsoft.com/en-us/sysinternals/psexec.aspx

```cmd
C:\> psexec.exe \<HOST NAME OR IP ADDRESS> -u <DOMAIN>\<PRIVILEGED ACCOUNT> -p <PASSWORD> -c mdd_1.3.exe --o C:\memory.dmp
```

参考 https://github.com/volatilityfoundation/volatility

从内存转储提取 dll：

```cmd
C:\> volatility ddldump -f memory.dmp -D dumps/
C:\> volatility procmemdump -f memory.dmp -D dumps/
```

使用 dc3dd 创建 `C:\` 的硬盘镜像：

参考 https://sourceforge.net/projects/dc3dd/files/dc3dd/7.20%20%20Windows/

```cmd
C:\> dc3dd.exe if=\c: of=d:\<ATTACHED OR TARGET DRIVE>\<IMAGE NAME>.dd hash=md5 log=d:\<MOUNTED LOCATION>\<LOG NAME>.log
```

#### LINUX

创建内存转储：

```bash
dd if=/dev/fmem of=/tmp/<MEMORY FILE NAME>.dd
```

### 使用 LIME 创建内存转储

参考 https://github.com/504ensicslabs/lime

```bash
wget https://github.com/504ensicsLabs/LIME/archive/master.zip
```

```bash
unzip master.zip
```

```bash
cd LIME-master/src
```

```bash
make
```

```bash
cp lime-*.ko /media=/media/ExternalUSBDriveName/
insmod lime-3.13.0-79-generic.ko "path=/path/<MEMORY DUMP>.lime format=raw"
```

使用进程 ID 复制可疑进程：

```bash
cp /proc/<SUSPICIOUS PROCESS ID>/exe/<NEW SAVED LOCATION>
```

获取可疑进程的内存核心转储：

```bash
gcore <PID>
```

gcore 文件上的字符串：

```bash
strings gcore.*
```

创建带有日志和哈希选项的硬盘/分区拷贝：

```bash
dd if=<INPUT DEVICE> of=<IMAGE FILE NAME>
```

```bash
dc3dd if=/dev/<TARGET DRIVE EXAMPLE SDA OR SDA1> of=/dev/<MOUNTED LOCATION>\<FILE NAME>.img hash=md5 log=<MOUNTED LOCATION>/<LOG NAME>.log
```

通过 SSH 创建远程驱动/分区：

```bash
dd if=/dev/<INPUT DEVICE> | ssh <USER NAME@<DESTINATION IP ADDRESS> "dd of=<DESTINATION PATH>"
```

通过 netcat 发送压缩的硬盘镜像：

发送端：

```bash
bzip2 -c /dev/<INPUT DEVICE> | nc <DESTINATION IP ADDRESS> <PICK A PORT>
```

接收端：

```bash
nc -p <PICK SAME PORT> -l | bzip2 -d | dd of=/dev/sdb
```

通过 netcat 发送硬盘镜像：

发送端：

```bash
dd if=/dev/<INPUT DEVICE> bs=16M | nc <PORT>
```

带有 Pipe Viewer 计数器的接收端：

```bash
nc -p <SAME PORT> -l -vv | pv -r | dd of=/dev/<INPUT DEVICE> bs=16M
```

## 5 恢复 (REMEDIATE)

## 补丁 (PATCHING)

### WINDOWS

针对 Windows 7 或更高版本的单个热补更新：

```cmd
C:\> wusa.exe C:\<PATH TO HOTFIX>\Windows6.0-KB9343407-x86.msu
```

通过运行批量脚本设置 Windows 7 之前的系列单个热补更新：

```batch
@echo off
setlocal
set PATHTOFIXES=E:\hotfix
%PATHTOFIXES%\Q123456_w2k_sp4_x86.exe /Z /M
%PATHTOFIXES%\Q123321_w2k_sp4_x86.exe /Z /M
%PATHTOFIXES%\Q123789_w2k_sp4_x86.exe /Z /M
```

检查并更新 Windows 7 或更高版本：

```cmd
C:\> wuauclt.exe /detectnow /updatenow
```

### LINUX

Ubuntu:
获取可用更新列表：

```bash
apt-get update
```

强制升级当前软件包：

```bash
apt-get upgrade
```

安装更新（新包）：

```bash
apt-get dist-upgrade
```

Red Hat Enterprise Linux 2.1,3,4:

```bash
up2date
```

以非交互式方式进行更新：

```bash
up2date-nox --update
```

安装特定包：

```bash
up2date <PACKAGE NAME>
```

更新特定包：

```bash
up2date -u <PACKAGE NAME>
```

Red Hat Enterprise Linux 5:

```bash
pup
```

Red Hat Enterprise Linux 6:

```bash
yum update
```

列出已安装的特定包：

```bash
yum list installed <PACKAGE NAME>
```

安装特定包：

```bash
yum install <PACKAGE NAME>
```

更新特定包：

```bash
yum update
```

Kali:

```bash
apt-get update
```

## 备份 (BACKUP)

### WINDOWS

[此处的文本似乎不完整或已碎片化]

### LINUX

在单用户模式下重置 root 密码：

- 步骤 1：重启系统。

```bash
reboot -f
```

- 步骤 2：在 GRUB 界面按 ESC。
- 步骤 3：选择默认项并按 'e' 编辑。
- 步骤 4：向下滚动直到看到一行以 linux、linux16 或 linuxefi 开头的行。
- 步骤 5：在该行末尾留一个空格并添加不带引号的 `rw init=/bin/bash`
- 步骤 6：按 Ctrl-X 重启。
- 步骤 7：重启后，应将进入单用户模式并更改密码。

```bash
passwd
```

- 步骤 8：重启系统。

```bash
reboot -f
```

重新安装包：

```bash
apt-get install --reinstall <受损的包名>
```

重新安装所有包：

```bash
apt-get install --reinstall $(dpkg --get-selections | grep -v deinstall)
```

### 杀死恶意进程

#### WINDOWS

#### 恶意软件移除

Ref. http://www.gmer.net/

```cmd
C:\> gmer.exe (GUI)
```

杀死正在运行的恶意文件：

```cmd
C:\> gmer.exe -killfile C:\WINDOWS\system32\drivers\<恶意文件名>.exe
```

在 PowerShell 中杀死正在运行的恶意文件：

```powershell
PS C:\> Stop-Process -Name <进程名>
PS C:\> Stop-Process -ID <PID>
```

#### LINUX

杀死恶意进程：

```bash
kill <恶意 PID>
```

更改恶意进程的执行权限并移动位置：

```bash
chmod -x /usr/sbin/<可疑文件名>
mkdir /home/quarantine/
mv /usr/sbin/<可疑文件名> /home/quarantine/
```



# 6 大战术（技巧与窍门）

## 操作系统作弊技巧

### WINDOWS

将输出管道到剪贴板：
`C:\> some_command.exe | clip`

将剪贴板内容输出到文件：（需要 PowerShell 5）
`PS C:\> Get-Clipboard > clip.txt`

在日志文件中添加时间戳：
`C:\> echo %DATE% %TIME% >> <文本日志>.txt`

远程添加/修改注册表值：
`C:\> reg add \\<远程计算机名>\HKLM\Software\<注册键信息>`

远程获取注册表值：
`C:\> reg query \\<远程计算机名>\HKLM\Software\<注册键信息>`

测试注册表路径是否存在：
`PS C:\> Test-Path "HKCU:\Software\Microsoft\<配置项单元>"`

远程复制文件：
`C:\> robocopy C:\<源共享文件夹> \\<目标计算机>\<目标文件夹> /E`

检查目录是否包含某些文件扩展名：
`PS C:\> Test-Path C:\Scripts\Archive\* -include *.ps1, *.vbs`

显示文件内容：
`C:\> type <文件名>`

合并多个文件的内容：
`C:\> type <文件名> <文件名 2> <文件名 3> > <新文件名>`

桌面版，允许多个桌面屏幕：
Ref. https://technet.microsoft.com/en-us/sysinternals/cc817881

运行实时选项：
```
C:\> "%ProgramFiles%\Internet Explorer\iexplore.exe" https://live.sysinternals.com/desktops.exe
```

远程挂载，只读和读写：
```
C:\> net share MyShare_R=c:\<只读文件夹> /GRANT:EVERYONE, READ
```
```
C:\> net share MyShare_RW=c:\<读/写文件夹> /GRANT:EVERYONE, FULL
```

使用 PSESEC 远程执行任务：
Ref. https://technet.microsoft.com/en-us/sysinternals/psexec.aspx
```
C:\> psexec.exe \\<目标 IP 地址> -u <用户名> -p <密码> /c C:\<程序>.exe
```
```
C:\> psexec @C:\<目标文件列表>.txt -u <管理员级用户名> -p <密码> C:\<程序>.exe C:\<输出文件名>.txt
```
```
C:\> psexec.exe @C:\<目标文件列表>.csv -u <域名>\<用户名> -p <密码> /c C:\<程序>.exe
```

远程执行任务并将输出发送到共享：
```
C:\> wmic /node:ComputerName process call create "cmd.exe /c netstat -an > \\<远程共享>\<输出文件名>.txt"
```

比较两个文件的差异：
```
PS C:\> Compare-Object (Get-Content .<日志文件名 1>) -DifferenceObject (Get-Content .<日志文件名 2>.log)
```

使用 PowerShell 远程执行任务：
```
PS C:\> Invoke-Command -ComputerName <计算机名> {PS 命令}
```

PowerShell 命令帮助：
```
PS C:\> Get-Help <PS 命令> -full
```

### LINUX

通过 ssh 远程分析流量：
```bash
# ssh root@<目标主机的远程 IP 地址> tcpdump -i any -U -s 0 -w - 'not port 22'
```

手动向 syslog 添加注释/数据：
```
# logger "日志中需要记录的重要事项"
# dmesg | grep <注释>
```

简单的只读挂载：
```
# mount -o ro <设备> <挂载点>
```

通过 SSH 挂载：
```
# sshfs <用户名>@<远程主机>:<远程路径> <本地挂载点>
```

退出并重新登录：
```
# exit
login
```

在 Linux 中创建 SMB 共享：
```
# useradd -m <用户名>
# smbpasswd -a <用户名>
# echo [共享名] >> /etc/samba/smb.conf
# echo path = /路径 >> /etc/samba/smb.conf
# echo browseable = yes >> /etc/samba/smb.conf
# echo valid users = <用户名> >> /etc/samba/smb.conf
# echo guest ok = >> /etc/samba/smb.conf
# echo writable = yes >> /etc/samba/smb.conf
# service smbd restart
```

修改权限：
```
# echo read only = no >> /etc/samba/smb.conf
# echo public = yes >> /etc/samba/smb.conf
# echo browseable = yes >> /etc/samba/smb.conf
# echo valid users = no >> /etc/samba/smb.conf
# echo guest ok = no >> /etc/samba/smb.conf
# echo writable = yes >> /etc/samba/smb.conf
# service smbd restart
```

从远程系统访问共享：
`smb://<Linux IP 地址>`

将文件复制到远程系统：
`scp <文件名> <用户名>@<目标 IP 地址>:<远程文件夹>`

将 SMB 共享挂载到远程系统：
```
# mount -t smbfs -o username=<用户名> //<服务器名或 IP 地址>/<共享名> /mnt/<挂载点>/
```

网站或文件是否存在：
```bash
# while true; do curl -Ssr <URL> | head -n 1; sleep 60; done
```

检测 PSEXEC 流量的 Snort ：
Ref. https://github.com/John-Lin/docker-snort/blob/master/snortrules-snapshot-2972/rules/policy-other.rules
```
alert tcp $HOME_NET any -> $HOME_NET [139,445] (msg:"POLICY-OTHER use of psexec remote administration tool"; flow:to_server,established; content:"|FF|SMB|A2"; depth:5; offset:4; content:"5C00|p|00|s|00|e|00|x|00|e|00|c|00|s|00|v|00"; nocase; metadata:service netbios-ssn; reference:url, technet.microsoft.com/en-us/sysinternals/bb897553.aspx; clasastype:policy-violation; sid:24008; rev:1)

alert tcp $HOME_NET any -> $HOME_NET [139,445] (msg:"POLICY-OTHER use of psexec remote administration tool"; flow:to_server,established; content:"|FE|SMB|"; depth:8; nocase; within:2; distance:8; content:"|P|00|S|00|E|00|X|00|E|00|S|00|V|00|C|00|"; fast_pattern:only; metadata:service netbios-ssn; reference:url, technet.microsoft.com/en-us/sysinternals/bb897553.aspx; clasastype:policy-violation; sid:30281; rev:1)
```

## DoS/DDOS 指纹识别

识别 DoS/DDoS 类型：
Ref. https://www.trustwave.com/Resources/SpiderLabs-Blog/PCAP-Files-Are-Great-Arn-t-They--/

**流量型：带宽消耗**
例如，向 10Mb 连接持续发送 1Gb 的流量
Ref. http://freecode.com/projects/iftop
```
### iftop -n
```

**协议型：** 使用特定协议
例如，SYN 洪水、ICMP 洪水、UDP 洪水
```
### tshark -r <FILE NAME>.pcap -q -z io,phs
```
```
### tshark -c 1000 -q -z io,phs
```
```
# tcpdump -tnr $FILE NAME | awk -F '.' '{print $1"."$2"."$3"."$4}' | sort | uniq -c | sort -n | tail
```
```
### tcpdump -qnn "tcp[tcpflags] & (tcp-syn) != 0"
```
```
### netstat -s
```

例如，隔离一种协议或移除其他协议
```
### tcpdump -nn not arp and not udp
```
```
### tcpdump -nn
```

**资源型：状态耗尽**
例如，防火墙可以处理 10000 个并发连接，而攻击者发送了 20000 个。
```
### netstat -n | awk '{print $6}' | sort | uniq -c | sort -nr | head
```

**应用型：七层攻击**
例如，HTTP GET 洪水，针对大文件。
```
### tshark -c 10000 -T fields -e http.host | sort | uniq -c | sort -r | head
```
```
### tshark -r capture6 -T fields -e http.request.full_uri | sort | uniq -c | sort -r | head -n 10
```
```
# tcpdump -n 'tcp[32] = 0x474520' | cut -f 7 -d " "
```

例如，寻找过量的请求，GIF、ZIP、JPEG、PNG。
```
# tshark -Y "http contains ff:d8 || http contains GIF89a || http contains \x50\x4B || http contains \xff\xd8 || http contains PDF"
```

例如，寻找被滥用的 'user-agent' 模式。
```
# tcpdump -c 1000 -Ann | grep -Ei 'user-agent' | sort | uniq -c | sort -nr | head
```

例如，显示 HTTP 请求头。
```
# tcpdump -i en0 -A -s 500 | grep -i refer
# tcpdump -s 1024 -l -A dst <EXAMPLE.COM>
```

## 攻击：二层攻击

例如，ARP 毒投、DHCP
```
# tcpdump -tnr <SAMPLE TRAFFIC FILE>.pcap "arp or icmp" | awk -F '.' '{print $1"."$2"."$3"."$4}' | sort | uniq -c | sort -n | tail
```
```
# tshark -r <SAMPLE TRAFFIC FILE>.pcap -q -z io,phs | grep arp.address-detected
```



# 工具包

- **KALI**：渗透测试发行版。Ref. https://www.kali.org
- **SIFT**：取证工具包。Ref. https://sift.readthedocs.org
- **REMUX**：用于逆向工程和分析的 Linux 工具包。Ref. https://remux.org
- **OPENVAS**：开源漏洞扫描器和管理器。Ref. http://openvas.org
- **MOLOCH**：大规模数据包捕获 (PCAP)、索引和数据库系统。Ref. https://github.com/moloch/wiki
- **SECURITY ONION**：入侵检测、网络安全监控和日志管理的 Linux 发行版。Ref. https://security-onion-solutions.github.io/security-onion/
- **NAGIOS**：网络监控、告警和报告工具。Ref. https://www.nagios.org
- **OSSEC**：可扩展、多平台主机入侵检测系统。Ref. http://ossec.github.io
- **SAMURAI WTF**：预配置测试环境。Ref. http://samurai.inguians
- **RTIR**：事件响应跟踪器。Ref. https://www.bestpractical.com/rtir/
- **HONEYDRIVE**：预配置蜜罐软件。Ref. http://sourceforge.net/projects/honeydrive
- **ATTACK SURFACE ANALYZER BY MICROSOFT**：帮助防止漏洞被利用的工具。Ref. https://technet.microsoft.com/en-us/download/confirmation.aspx?id=24487
- **WINDOWS TO GO**：便携版 Windows 8。Ref. https://winfe.microsoft.com/en-us/library/hh8383.aspx
- **WINFE**：CD/USB 上的 Windows 取证环境。Ref. http://winfe.wordpress.com
- **DCEPT**：部署和检测 Active Directory 蜜罐（honeytokens）。Ref. https://www.secureworks.com/blog/dcept
- **TAILS**：匿名直播系统。Ref. https://tails.org

# 7 事件管理（检查清单）

> **注意**：本节作为事件响应指南。某些任务可能不相关、必要或合适。在实施每个步骤或其他步骤之前，请考虑您的环境。

## 识别任务

| 任务 | 优先级 | 工作量 | 状态 |
|---|---|---|---|
| 获取恶意文件副本进行分析？ | H/M/L | H/M/L | Open/Closed |
| 系统的恶意影响。获取计算机系统、文件、设置、注册表、添加/删除或停止/启动服务的已知更改详细列表。 | H/M/L | H/M/L | Open/Closed |
| 哪种防毒软件或恶意软件工具可以检测并移除恶意威胁？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件/攻击者何时离开网络？ | H/M/L | H/M/L | Open/Closed |
| 恶意的内外部站点/连接仍然活跃？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件在任何端口上监听？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件的原始感染方法和或弱点？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件尝试感染其他设备数据包？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件尝试与网络外通信的任何数据包并识别端口、IP、DNS 等方法？ | H/M/L | H/M/L | Open/Closed |
| 恶意软件是否对任何敏感数据（文件、凭据、知识产权、PII 等）构成威胁？ | H/M/L | H/M/L | Open/Closed |
| 受感染系统上的 DNS 条目是什么？ | H/M/L | H/M/L | Open/Closed |
| 是否可能检测到第一台受感染的系统？ | H/M/L | H/M/L | Open/Closed |
| 第一台系统的硬盘是否保存？ | H/M/L | H/M/L | Open/Closed |

## 修复任务

| 管理员 AD 密码更改 | | | |
|---|---|---|---|
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 本地管理员密码更改 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 用户 AD 密码更改 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 本地用户密码更改 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 服务账户密码更改 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 针对检测到的恶意软件推送杀毒软件更新 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 尝试多种杀毒工具 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 设置了哪些活动目录 GPO 策略（日志、限制等） | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 网络架构是怎样的？恶意软件将如何渗透？ | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 是否有额外的 IDS/IPS 分段需要覆盖以防止/检测爆发？ | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 第三方应用缺失补丁（Adobe, Java 等） | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 监控客户端电子邮件，以关注感兴趣的供应商或其他业务连续性事项 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 监控外部可访问 RDP 客户端系统上的 RDP 会话 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |

## 是否有正在使用的攻击应用程序？如果有，是否有替代方案？

| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
|---|---|---|
| 是否有基准系统来检查更改？ | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 监控用户名变体 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 管理和监控任务 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查边界路由器日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查 VPN（远程访问）日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| Citrix / VMware 或类似的日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查会计服务器日志和用户趋势 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| AD 服务器日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查反病毒软件（恶意代码服务）日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查电子邮件滥用通知和日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查 DNS 日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查帐户和策略滥用日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 检查主机防火墙日志 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |

## 其他 / 经验教训任务

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 根据生命周期重建计划重建所有系统 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 同步所有系统的时间服务 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 创建事件数据仓库 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 考虑主机主机 IPS | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 考虑网络访问控制 (NAC) | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |
| 第三方内部/外部安全和边界安全工具及评估服务 | | | |
| 优先级: 高/中/低 | 工作量: 高/中/低 | 开启/关闭 |

## 恶意软件属性清单

### 系统中的恶意软件存在：

| | 是 | 否 | 未知 | 不适用 |
|---|---|---|---|---|
| 仅在内存中运行 | | | | |
| 从注册表运行，或 | | | | |
| 磁盘上的产物 | | | | |
| 磁盘文件被隐藏，存储在未分配空间、空闲/碎片空间或已加密 | | | | |
| 有图标 | | | | |
| 无描述或公司名称 | | | | |
| 未签名的 Microsoft 镜像经过封装并可能加密 | | | | |
| 可疑的 DLL 或服务 | | | | |
| 备份并将自身交换到真实文件的位置 | | | | |
| 以文件对的形式持续运行 | | | | |
| 发现于嵌入式设备、工业控制和 IoT | | | | |

### 恶意软件活动

| | 是 | 否 | 未知 | 不适用 |
|---|---|---|---|---|
| 下载新代码/功能 | | | | |
| 利用跳板系统和网络路径离开受害者网络，包括 VPN/拨号、HTTP/HTTPS 以及其他标准或非标准服务和端口 | | | | |
| 利用移动设备和其他可移动介质的能力 | | | | |
| 检测并利用已验证的 Web 代理的能力 | | | | |
| 在受害者客户端系统上变异 | | | | |
| 根据其检测到的环境包含红鲱鱼（误导/分散注意力）特征 | | | | |
| 遍历所有已知操作系统的能力 | | | | |
| 移动到嵌入式设备的能力 | | | | |

### 恶意软件能力

| 能力 | 是 | 否 | 未知 | 不适用 |
|---|---|---|---|---|
| 执行大多数基于 Windows 的活动目录命令的能力 | | | | |
| 上传和下载文件/负载的能力 | | | | |
| 能为所需的服务构建内置服务或专门定制的恶意软件 | | | | |
| 具有若干持久化特征，使恶意软件对杀毒防御具有极强的韧性 | | | | |
| 暴力破解的能力 | | | | |
| 执行大多数基于 Windows 的活动目录命令的能力 | | | | |
| DoS 工具 | | | | |
| 窃取凭据的能力 | | | | |
| 权限提升 | | | | |
| 勒索软件能力 | | | | |
| 主机 IPS | | | | |
| 沙箱感知 | | | | |
| C2 技术 | | | | |
| C2 通信 | | | | |
| 隐写术 | | | | |
| 内存感知 | | | | |
| 虚拟机感知 | | | | |
| IP 感知 | | | | |
| 恶意软件反混淆 | | | | |

## VERIS 事件识别

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 已确认 | | | |
| 怀疑 | | | |
| 高 | | | |
| 中 | | | |
| 低 | | | |

## 时间线单位

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 秒 | | | |
| 分钟 | | | |
| 小时 | | | |
| 天 | | | |
| 周 | | | |
| 月 | | | |
| 年 | | | |

## 影响程度

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 无 | | | |
| 轻微 | | | |
| 中等 | | | |
| 主要 | | | |
| 灾难性 | | | |

## 影响评分

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 0 | | | |
| 1 | | | |
| 2 | | | |
| 3 | | | |
| 4+ | | | |

## 发现方法

| 优先级 | 工作量 | 状态 |
|---|---|---|
| NIDS | | | |
| HIDS | | | |
| 杀毒软件 | | | |
| 审计 | | | |
| 监控 | | | |
| 事件响应 | | | |
| 执法部门 | | | |
| 报告 | | | |
| 用户 | | | |
| 其他 | | | |

## 纠正措施

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 简单 | | | |
| 中等 | | | |
| 困难 | | | |

## 目标

| 优先级 | 工作量 | 状态 |
|---|---|---|
| 机会性 | | | |
| 针对性 | | | |

## 国家

| 优先级 | 工作量 | 状态 |
|---|---|---|
| AED | | | |
| AFN | | | |
| ALL | | | |
| AMD | | | |
| AOA | | | |
| ARS | | | |
| ASM | | | |
| AUD | | | |
| AWL | | | |
| AZN | | | |
| BAM | | | |
| BDT | | | |
| BHD | | | |
| BGN | | | |
| BFA | | | |
| BRL | | | |
| BWP | | | |
| CAD | | | |
| CDF | | | |
| CLP | | | |
| COP | | | |
| CRC | | | |
| CZK | | | |
| DJ | | | |
| DOP | | | |
| DZD | | | |
| EGP | | | |
| ETB | | | |
| EGN | | | |
| EUR | | | |
| FJD | | | |
| FKP | | | |
| GEL | | | |
| GNF | | | |
| GIP | | | |
| GBP | | | |
| GYD | | | |
| HKD | | | |
| HNL | | | |
| HT | | | |
| HUF | | | |
| ID | | | |
| IMP | | | |
| INR | | | |
| IQ | | | |
| ISK | | | |
| J | | | |
| JEP | | | |
| JOD | | | |
| KES | | | |
| KGS | | | |
| KHR | | | |
| KZT | | | |
| LAK | | | |
| LSL | | | |
| LSD | | | |
| LKR | | | |
| MAD | | | |
| MKD | | | |
| MGA | | | |
| MNT | | | |
| MWK | | | |
| MUR | | | |
| MYR | | | |
| MZN | | | |
| NGN | | | |
| NIO | | | |
| NOK | | | |
| NPR | | | |
| OAB | | | |
| OAF | | | |
| OOA | | | |
| PEN | | | |
| PKR | | | |
| PLG | | | |
| PNR | | | |
| QAR | | | |
| QOR | | | |
| RUB | | | |
| RWF | | | |
| SAR | | | |
| SBD | | | |
| SCR | | | |
| SEK | | | |
| SGD | | | |
| SHP | | | |
| SLL | | | |
| SOS | | | |
| SPL | | | |
| SRD | | | |
| STD | | | |
| SVC | | | |
| SZL | | | |
| THB | | | |
| TJS | | | |
| TMT | | | |
| TND | | | |
| TOP | | | |
| TRY | | | |
| TTD | | | |
| TVD | | | |
| TWD | | | |
| TZS | | | |
| UAH | | | |
| UGX | | | |
| USD | | | |
| UYU | | | |
| UZS | | | |
| VEF | | | |
| VND | | | |
| VUV | | | |
| WST | | | |
| XAF | | | |
| XCD | | | |
| XDR | | | |
| XOF | | | |
| XPF | | | |
| YER | | | |
| ZAR | | | |
| ZMK | | | |
| ZWD | | | |

# 攻击者 (ACTOR)

| actor.x.motive (攻击者动机) |
| :--- |
| 未知、不适用、间谍、恐惧、财务、乐趣、怨恨、意识形态、便利、其他 |
| actor.external.variety (攻击者外部类型) |
| 未知、活动分子、审计员、竞争对手、客户、不可抗力、前员工、国家级、组织犯罪、熟人、政府关联、恐怖分子、无关联、其他 |
| actor.internal.variety (攻击者内部类型) |
| 未知、审计员、叫中心、收银员、终端用户、执行人员、财务、帮助台、人力资源、维护、经理、保安、开发者、系统管理员、其他 |

# 动作 (ACTION)

## action.malware.variety (恶意软件种类)

未知、广告软件、后门、暴力破解、捕获应用数据、捕获存储数据、客户端攻击、点击欺诈、C2（命令与控制）、破坏数据、禁用控制、DoS、下载器、利用漏洞、导出数据、数据包嗅探、密码提取程序、内存抓取、勒索软件、Rootkit、扫描网络、垃圾邮件、间谍软件/键盘记录器、SQL注入、管理软件、蠕虫、其他

## action.malware.vector (恶意软件矢量)

未知、直接安装、通过恶意软件下载、邮件自动执行、邮件链接、邮件附件、即时消息、网络传播、远程注入、可移动介质、网页路过、网页下载、其他

## action.hacking.variety (黑客种类)

未知、功能滥用、暴力破解、缓冲区溢出、缓存中毒、会话预测、CSRF、XSS、密码分析、DoS、足迹探测、强制浏览、格式化攻击、模糊测试、HTTP响应走私、HTTP请求拆分、HTTP响应走私、HTTP注入、邮件命令注入、中间人攻击 (MitM)、空字节注入、离线破解、操作系统命令、路径遍历、RFI（远程文件包含）、反向工程、路由转向、会话固定、会话重放、Soap数组滥用、特殊元素注入、SQLi、SSI注入、URL重定向滥用、使用后门或C2、使用盗取的凭据、XML属性溢出、XML实体扩展、XML实体、XML注入、XPath注入、Xquery注入、虚拟机逃逸、其他

## action.hacking.vector (黑客矢量)

未知、第三方桌面、后门或C2、桌面共享、物理访问、命令行壳、合作伙伴、VPN、Web应用、其他

| action.social.variety (社交工程攻击种类) |
| :--- |
| 未知、诱饵、贿赂、诱导、勒索、伪造、影响、诈骗、钓鱼、社交装扮、宣传、垃圾邮件、其他 |
| action.social.vector (社交工程攻击矢量) |
| 未知、文档、邮件、面对面、即时消息、电话、可移动介质、短信、社交媒体、软件、网站、其他 |
| action.social.target (社交工程攻击目标) |
| 未知、审计员、叫中心、收银员、客户、终端用户、执行人员、财务、前员工、帮助台、人力资源、维护、经理、合作伙伴、保安、开发者、系统管理员、其他 |
| action.misuse.variety (滥用种类) |
| 未知、知识滥用、权限滥用、贪污、数据处理不当、邮件滥用、网络滥用、非法内容、未经批准的解决方案、未经批准的硬件、未经批准的软件、其他 |
| action.misuse.vector (滥用矢量) |
| 未知、物理访问、LAN访问、远程访问、非企业、其他 |
| action.physical.variety (物理攻击种类) |
| 未知、攻击、破坏、窥视、监控、篡改、盗窃、监听、连接、其他 |
| action.physical.location (物理攻击位置) |
| 未知、合作伙伴设施、合作伙伴车辆、个人住宅、个人车辆、公共设施、公共车辆、受害者安全区域、受害者工作区域、受害者公共区域、受害者场地、其他 |
| action.physical.vector (物理攻击矢量) |
| 未知、特权访问、访问权限、绕过控制、禁用控制、不受控位置、其他 |

## action.error.variety (错误种类)

未知、分类错误、数据输入错误、处置错误、失误、损失、维护错误、配置错误、投递错误、错误信息、遗漏、物理事故、容量不足、编程错误、发布错误、故障、其他

## action.error.vector (错误矢量)

未知、随机错误、疏忽、人员不足、流程不完善、技术不足、其他

## action.environmental.variety (环境种类)

未知、恶化、地震、电磁干扰 (EMI)、静电释放 (ESD)、温度、火灾、洪水、危险品、湿度、飓风、冰、滑坡、闪电、陨石、颗粒、病原体、停电、龙卷、海啸、虫害、火山、泄漏、风、其他

# 资产 (ASSET)

| asset.variety (资产种类) |
| :--- |
| 未知、S-认证、S-备份、S-数据库-DHCP、S-目录、S-DCS、S-DNS、S-文件、S-日志、S-邮件、S-大型机、S-支付交换中心、S-POS控制器、S-打印、S-代理、S-远程访问、S-SCADA、S-Web应用、S-代码库、S-虚拟机主机、S-其他、N-访问阅读器、N-摄像头、N-防火墙、N-HSM、N-IDS、N-宽带、N-PBX、N-私有WAN、N-PLC、N-公共WAN、N-RTU |

# 草稿

# 10 索引 (A-Z)

A
活动目录 (Active Directory). 17, 18, 19, 31
AdFin ................ 19
备用数据流 (Alternate Data Streams). ............ 77
Apache. ............ 63
AppLocker .......... 26
auditd . ........... 64
Auditpol. 32, 56, 57, 58, 59, 97

C
Certutil ........... 107
Cron . ............ 63
cncURL. ............ 90

D
dc33dd. ........ 91, 92
dd 91
解码 (Decoding) ........ 107
DHCP . ........... 14, 20
DNS... ........ 14, 25, 39
DNSCmd .......... 15
dnstop .......... 55
sadadd ........... 32
dsmove. ........ 32
dcovery. ....... 17, 18
editcap. ......... 51

F
文件校验完整性验证器 (FCIV) ........ 15
forlives. ....... 77

G
GMER. .......... 101
gpresult ....... 69
gpgupdate ....... 32
组策略对象 (Group Policy Object) n......... 31

H
哈希 (Hashing). ....... 15, 21
hexdump ........ 85

I
iftop. ......... 112
initcl. ........ 36
IPSEC. ......... 30, 40
iptables ........ 37, 38, 40
IPv6. ........... 33

L
labrea. ......... 54
Idfde .......... 19
LiME. .......... 92
Linux 防火墙.. 77
Linux 脚本... 20, 21, 46, 53, 106
Linux 服务 .. 36
ListDLLs ........ 78

M
Mergecap ...... 51
微软基础安全分析器 (MSEA). ........... 17
Microsoft IIS.. 62
Mimikz. ...... 53
Mklin. ........ 97
mount. ........ 106

N
nbtscan ....... 21
nbtat. ......... 16
Nessus . ....... 11
net user ....... 25
net view. ........ 14
Netcat. ........ 54
netdom. ........ 18
Netsh 23, 24, 25, 30, 31, 68
Nmap. ......... 11

O
OpenSSL ....... 47
OpenVAS. ....... 12

P
passwd. ........ 39
PowerShell .. .. 29, 59, 60, 62, 76, 98, 105, 108
代理自动配置 (PAC). ....... 26
ps 36
PsExec. ........ 91, 04
Psinfo. ....... 67
PsLoggedon.. 16
PsLogist ........ 75
spassword ........ 22

R
Racoon. ....... 40
远程桌面协议 (RDP) 32
Robocopy 103
runas. ............ 53

S
SC 23, 99
scp ......... 106
sigcheck....... 77, 85
sbmclient...... 20
smbtree...... 20, 109, 110, 111
SSH ........ 80, 105
sldump ........ 47
粘滞键 (Sticky Keys). .. T
tcpdump 45, 46, 112, 112, 113
Team Cymru .. .. 90
TShark.... .. 47, 48, 49, 112, 113

U
ufw ........... 38
unix-privsec-check 83
uptart. ....... 36
用户账户控制 (UAC) ............................ 35
Wget.................................................. 54
Windows 注册表 (Windows Registry) 32, 33, 34, 56, 71, 72, 73, 74
V ...................................................... 90
Windows 自动启动 (Windows Autorun) ............................... 69, 70
Windows 脚本 (Windows Scripting) ............ 14, 16, 52, 77
Volatility ........... 87, 91
Windows Defender (Windows Defender) ............................. 78
wmic ........................... 23, 67, 69
Volrest ............................. 98
Windows 事件日志 (Windows Event Log) .......................... 60, 61
wusa ............................................ 95
Vssadmin ....... 97, 98
Windows 防火墙 (Windows Firewall) ................ 23, 31, 35
X xsearch............... 107
W
Wevtutil. 53, 56, 75, 76
