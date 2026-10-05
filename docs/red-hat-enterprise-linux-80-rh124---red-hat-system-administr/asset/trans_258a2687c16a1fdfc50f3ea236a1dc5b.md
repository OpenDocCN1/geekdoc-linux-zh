

-   在 serverb 具有现有静态网络设置的同一接口上，配置 IPv4 地址 172.25.250.211，子网掩码 255.255.255.0。不要删除现有的 IPv4 地址。确保当在其接口上静态配置的连接激活时，serverb 响应所有地址。
-   在 serverb 上，通过激活原始网络连接并停用你手动创建的静态网络连接，恢复原始网络设置。

## 评估

在 workstation 上，运行 `lab rhcsa-rh124-review4 grade` 命令以确认本次练习的成功。

```
student@workstation ~]$ lab rhcsa-rh124-review4 grade
```

## 完成

在 workstation 上，运行 `lab rhcsa-rh124-review4 finish` 完成综合性复习。此脚本将删除在综合复习开始期间创建的文件和目录，并确保 serverb 上的环境是干净的。

```
student@workstation ~]$ lab rhcsa-rh124-review4 finish
```

综合复习此结束。

## 解决方案

## 管理网络

在本次复习中，你将配置并测试网络连接性。

## 结果

你应该能够：

-   配置网络设置。
-   测试网络连接性。
-   为系统设置静态主机名。
-   使用本地可解析规范主机名连接到系统。

## 开始之前

使用用户 student 和密码 `student` 登录 workstation。

在 workstation 上，运行 `lab rhcsa-rh124-review4` 开始综合复习。此脚本将创建必要的文件以正确设置环境。

```
$student@workstation~$ lab rhcsa-rh124-review4
```

## 指令

在 server 上的以太网接口及其激活的连接配置文件上完成以下任务。

-   确定以太网接口的名称
-   在 server 上，为可用的以太网接口创建一个名为 `static` 的新连接配置文件，本地设置网络设置且不使用 DHCP。它应该基于下表中的设置。

| IPv4 地址 | 172.25.250.111 |
| :--- | :--- |
| 子网掩码 | 255.255.255.0 |
| 网关 | 172.25.250.254 |
| DNS 服务器 | 172.25.250.254 |

将服务器的以太网接口设置为使用上表所示的更新网络设置。

-   确保服务器名称被静态设置为 `server-review4.lab.example.com`。
-   在 server 上，为 `servera.lab.example.com` 的 IPv4 地址 `172.25.250.10` 设置 `client-review4` 为规范主机名。

## 综合复习

-   在 serverb 具有现有静态网络设置的同一接口上，配置 IPv4 地址 172.25.250.211，子网掩码 255.255.255.0。不要删除现有的 IPv4 地址。确保当在其接口上静态配置的连接激活时，serverb 响应所有地址。
-   在 serverb 上，通过激活原始网络连接并停用你手动创建的静态网络连接，恢复原始网络设置。

1. 以用户 student 身份登录 serverb 的“物理”控制台：
   在控制你实验环境的网页界面中，点击 serverb 的 `CONSOLE` 按钮。浏览器将打开一个标签页，显示 serverb 的控制台会话。在提示符处以 student 登录。
   从服务器控制台进行网络更改是一个良好的习惯，无论是本地、通过用于远程控制台访问的特殊硬件，还是通过远程访问的串口控制台。如果你使用 ssh 调整网络设置，在更改连接配置文件时很容易导致会话挂起或被锁在服务器的远程访问之外。

2. 确定 serverb 上以太网接口的名称及其正在使用的连接配置文件名称。

```
[serverb]$ nmcli device status
DEVICE TYPE STATE CONNECTION
ens3 ethernet connected Wired connection 1
lo loopback unmanaged --
```

在此例中，`ens3` 是系统上以太网接口的名称。你将为此接口创建连接配置文件。
网络接口名称和初始连接配置文件的名称在 serverb 上可能有所不同。如果是如此，请在解决方案的后续步骤中使用你系统显示的名称代替本解决方案中使用的名称。

3. 在 serverb 上，为可用的以太网接口创建一个名为 `static` 的新连接配置文件。静态设置网络设置以便不使用 DHCP。基于下表设置：

| IPv4 地址 | 172.25.250.111 |
| :--- | :--- |
| 子网掩码 | 255.255.255.0 |
| 网关 | 172.25.250.254 |
| DNS 服务器 | 172.25.250.254 |

serverb 的以太网接口应使用前表中提到的更新网络设置。

3.1. 使用 `nmcli` 使用给定的网络设置创建连接 `static`。

```
[serverb]$ sudo nmcli connection add --name static type ethernet \
ifname ens3 ipv4.addresses '172.25.250.211/24' ipv4.gateway '172.25.250.254' \
ipv4.dns '172.25.250.254' ipv4.method manual
```
连接 'static' 已成功添加。

3.2. 使用 `nmcli` 命令激活连接。

```
[student@server ~]$ sudo nmcli connection up static
```

4. 使用 `hostnamectl` 命令静态设置服务器名称为 `server-review4.lab.com`，并使用 `hostname` 命令进行验证。

```
[student@server ~]$ sudo hostnamectl set-hostname server-review4.lab.com
[student@server ~]$ hostname
```

5. 在 server 上，编辑 `/etc/hosts` 文件，将 `client-review4` 设置为服务器 IPv4 地址 172.25.250.10 的规范名。

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
