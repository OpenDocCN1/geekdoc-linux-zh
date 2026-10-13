
[student@server ~]$ sudo hostnamectl set-hostname server-review4.lab.com

[student@server ~]$ hostname

```
5. 在 server 上，编辑 `/etc/hosts` 文件，将 `client-review4` 设置为服务器 IPv4 地址 172.25.250.10 的规范名。
```
5.1. 编辑 `/etc/hosts` 文件，将 `client-review4` 添加为 172.25.250.10 IPv4 地址的名称。你可以使用 `vim /etc/hosts` 编辑该文件。
```
172.25.250.10 servera
```
5.2. 使用 `ping` 命令验证你可以通过规范名 `client-review4` 访问 172.25.250.10。
```
[student@server ~]$ ping -c2 client-review4

PING client-review4 (172.25.250.10): 56-byte byte data

64 bytes from client-review4 (172.25.250.10): icmp_seq=1 ttl=64 time=259 ms

64 bytes from client-review4 (172.25.250.10): icmp_seq=2 ttl=64 time=291 ms

--- client-review4 statistics

2 packets transmitted, 2 received, 0% packet loss, time 300ms

rtt min/avg/max/mdev = 259/275/291/16 ms
```
6. 在 serverb 接口上配置额外的 IPv4 地址 172.25.250.211，子网掩码 255.255.255.0。不要删除现有的 IPv4 地址。确保当在其接口上静态配置的连接激活时，serverb 响应所有地址。
6.1. 使用 `nmcli` 命令为 `static` 连接添加 IPv4 地址。
```
[student@server ~]$ sudo nmcli connection modify static ipv4.addresses "+172.25.250.211/24"
```
6.2. 使用 `nmcli` 命令激活连接。
```
[student@server ~]$ sudo nmcli connection up static
```
6.3. 在 workstation 上使用 `ping -c2` 命令验证你可以访问主机 172.25.250.211。
```
[student@workstation ~]$ ping -c2 172.25.250.211

PING 172.25.250.211: 56-byte byte data

64 bytes from 172.25.250.211: icmp_seq=1 ttl=64 time=0.246 ms

64 bytes from 172.25.250.211: icmp_seq=2 ttl=64 time=0.296 ms

--- 172.25.250.211 statistics

2 packets transmitted, 2 received, 0% packet loss, time 50ms

rtt min/avg/max/mdev = 0.246/0.271/0.296/0.025 ms
```
7. 在 serverb 上，通过激活原始网络连接并停用你手动创建的静态网络连接，恢复原始网络设置。
7.1. 回到控制台并使用 `nmcli` 命令激活原始连接配置文件。
```
[student@server ~]$ sudo nmcli connection up "Wired connection 1"
```
原始连接配置文件的名称在你的服务器上可能不同。请用你系统中实际看到的名称替换解决方案中所示名称。如果你忘记了，可以使用 `nmcli connection show` 找到它。
7.2. 在 workstation 上，以 student 身份通过 SSH 连接到 serverb，以确保原始网络设置已成功激活。
```
[student@workstation ~]$ ssh serverb

[student@server-review4 ~]$
```
7.3. 从 server-review4 退出 workstation 上的所有终端。
```
[student@server-review4 ~]$ exit

logout

Connection to serverb closed.

[student@workstation ~]$
```

## 完成

在 workstation 上，运行 `lab rhcsa-rh124-review4 finish` 来完成综合回顾。此脚本将删除在综合回顾开始期间创建的文件和目录，并确保 `serverb` 上的环境保持干净。
```
[student@workstation ~]$ lab rhcsa-rh124-review4 finish
```
综合回顾此结束。

# 挂载文件系统和查找文件

在本次回顾中，你将挂载一个文件系统并根据不同的标准查找文件。

## 目标
你应该能够：
- 挂载已有的文件系统。
- 根据文件名、权限和大小查找文件。

# 准备工作
使用密码 student 以 student 身份登录 workstation。

在 workstation 上，运行 `lab rhcsa-rh124-review5 start` 开始综合回顾。此脚本将创建必要的文件系统、用户账户和用户组账户。
```
[student@workstation ~]$ lab rhcsa-rh124-review5 start
```

# 指令
在 serverb 上完成任务以结束练习。
- 在 serverb 上，存在一个包含 XFS 文件系统的块设备但尚未挂载。确定该块设备并将其挂载到 `/review5-disk` 目录。如有必要，创建 `/review5-disk` 目录。
- 在 serverb 上，找到名为 review5-path 的文件。创建一个名为 `/review5-disk/review5.txt` 的文件，其中包含单行内容，即 review5 文件的绝对路径。
- 在 serverb 上，找到所有所有者用户分别为 contractor1、组均为 contractor 的文件。这些文件还必须具有 640 的八进制权限。将这些文件的列表保存到 `/review5-disk/review5-perms.txt` 中。
- 在 serverb 上，找到所有大小为 100 字节的文件。将这些文件的绝对路径保存到 `/review5-disk/review5-size.txt` 中。

## 评估

在 workstation 上，运行 `lab rhcsa-rh124-review5 grade` 命令以确认本次练习成功。
```
[student@workstation ~]$ lab rhcsa-rh124-review5 grade
```

## 完成

在 workstation 上，运行 `lab rhcsa-rh124-review5 finish` 完成综合回顾。此脚本将删除在综合回顾开始期间创建的文件系统、用户账户和用户组账户，并确保 serverb 上的环境保持干净。
```
[student@workstation ~]$ lab rhcsa-rh124-review5 finish
```
综合回顾此结束。

# 挂载文件系统和查找文件

在本次回顾中，你将挂载一个文件系统并根据不同的标准查找文件。

## 目标
你应该能够：
- 挂载已有的文件系统。
- 根据文件名、权限和大小查找文件。

# 准备工作

使用密码 student 以 student 身份登录 workstation。

在 workstation 上，运行 `lab rhca5-rh124-reviews5` 开始综合回顾。此脚本将创建必要的文件系统、用户账户和用户组账户。
```
[student@workstation ~]$ lab rhca5-rh124-reviews5 start
```
