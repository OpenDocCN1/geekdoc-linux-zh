
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
