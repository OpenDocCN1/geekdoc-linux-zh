
To: "Clive Krahe" <clive@better_you.com>

Subject: You are an idiot

Date: 04 Jan 2000 13:27:21 -0600

在接收（Received）行中，Clive 看到了 `208.275.18.1` IP 地址，这很可能是 Martin 的真实机器。

```
clive$ host 208.275.18.1
1.18.275.208.IN-ADDR.ARPA domain name pointer box1.martin.sardoit.com
```

```
clive$ host box1.martin.sardoit.com
box1.martin_sardoit.com has address 208.275.18.1
box1.martin_sardoit.com is handled by (pri10) by mail.isp_central.net
```

Clive 使用 `nmap` 看看 Martin 正在使用什么样的机器：

```
clive$ nmap -O box1.martin.sardoit.com
Starting nmap V. 2.54BETA1 by fyodor@insecure.org (www://insecure.org/nmap/ )
Interesting ports on box1.martin.sardoit.com (208.275.18.1)
(The 1517 ports scanned but not shown are in state: closed)
Port Service
22/tcp ssh
25/tcp smtp
TCP Sequence Prediction: Class-random
Difficulty=396696
Remote system guess: Linux 2.122
Nmap run completed -- 1 IP address (1 host) scanned in 0 seconds
```

## 尝试登录

`nmap` 输出显示机器运行 Linux，提供 SSH 和邮件服务。Clive 尝试登录 Martin 的机器：

```
clive$ -v box1.martin.sardoit.com -l martin
Ssh Version OpenSSH-2.1, protocol 1.5/2.0.
Compiled with SSL (0x090581),
debug: Registering configuration data /home/clive/.ssh/config
debug: Registering configuration data /etc/ssh/ssh_config
debug: Applying options for *
debug: Seeding random generator
debug: ssh_connect: getuid 1500 getuid 0 anon 0
debug: Connecting to box1.martin.sardoit.com [208.275.18.1] port 22.
debug: Seeding random generator
debug: Allocated local port 617.
debug: Connection established.
ssh_exchange_identification: Connection closed by remote host
debug: Calling cleanup 0x80bcbc0 (0x0)
clive$
```

由于尝试登录之前就被断开了，Clive 推测 Martin 使用了 TCP 封装（wrappers）来限制哪些 IP 可以连接他的机器。知道密码毫无用，Clive 需要一台允许连接到 Martin 机器的机器。哪里最高？

## 寻找另一扇门

对 Martin 的域名进行 `whois` 查询返回：

```
clive$ whois MARTIN_SARDOIT.COM
Domain: SARDOIT.COM
Registrar: SOLUTIONS, INC.
URL: www.solutions.com
Name Server: NS1.CENTRAL.NET
Name Server: NS2.CENTRAL.NET
Updated: Jun 17 2000
```
