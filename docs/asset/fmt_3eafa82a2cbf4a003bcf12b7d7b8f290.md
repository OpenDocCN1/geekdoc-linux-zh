
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
