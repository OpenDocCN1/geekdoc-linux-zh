
```port_forwarding_and_tunneling/ssh_remote_forwarding.sh```

# 使用 Kali Linux 2.0 进行渗透测试

创建此隧道的命令语法将包括本地 IP 和端口、远程端口以及指定远程转发的 `-R`：

```
ssh -N -R [bind_address:]port username@address
```

列表 638 - 使用 SSH 进行远程端口转发的原型

在这种情况下，我们将 Kali 机器作为用户（`kali@10.11.0.4`），指定无命令（`-N`）和远程转发（`-R`）。我们在 Kali 机器（`10.11.0.4:2221`）的 TCP 端口 `2221` 上打开监听器，并将连接转发到内部 Linux 机器的端口 `3306` (`127.0.0.1:3306`)。

```
student@~$ ssh -N -R 10.11.0.4:2221:127.0.0.1:3306 kali@10.11.0.4

kali@10.11.0.4 password:
```

列表 639 - 将 TCP 端口 `2221` 远程转发到被入侵 Linux 机器上的 TCP 端口 `3306`

这将 Kali 系统本地端口 `2221` 上的所有入流量通过 SSH 隧道 (`TCP 22`) 转发到被入侵机器的 `3306` 端口，允许我们访问 MySQL 端口，即使该端口在防火墙上被过滤了。

我们的连接可以如图 299 所示：

![](img/f99f528ca9845f4c256ce54e882b1345_604_0.png)

图 299：远程端口转发图

隧道建立后，我们可以切换到 Kali 机器，验证 TCP 端口 `2221` 正在监听，并扫描端口上的本地主机，这将识别目标 MySQL 服务的指纹：

```
kali@kali:~ ss -antp | grep "2221"

LISTEN      0       128     127.0.0.1:2221      0.0.0.0:*      users:(("sshd",pid=2294,fd=9)

LISTEN      0       128     [::]:2221          users:(("sshd",pid=2294,fd=8))
```

```
kali@kali:~ sudo nmap -sS -sV 127.0.0.1 -p 2221
```

Nmap scan report for localhost (127.0.0.1)
Host is up (0.00039s latency).

| PORT | STATE | VERSION |
|---|---|---|
| 2221/tcp | open | mysql 5.5.15-10.26-MariaDB-0+deb9 |

Nmap done: 1 IP (1 host) scanned in 0.56 seconds

列表 640 - 通过隧道访问机器上的 MySQL 服务

既然可以扫描端口，我们应该没有任何问题地使用任何 Kali 安装的工具跨隧道与 MySQL 服务进行交互。

## 2.2.2 练习

- 1. 通过 SSH 连接到你的专用实验环境并以 root 身份运行 `/root/port_forwarding_and_tunneling/clear_rules.sh`。
- 2. 关闭到专用实验环境的所有 SSH 连接，然后使用桌面以 student 身份连接并运行 `/root/port_forwarding_and_tunneling/ssh_remote_forwarding.sh`。
- 3. 尝试复制上述场景中的 SSH 远程端口转发，并你可以与 MySQL 服务交互。

## 2.2.3 SSH 端口转发

现在到了真正的部分。SSH 动态端口转发允许我们设置一个本地监听端口，并通过代理将流量隧道到任何远程目标。

在场景中（类似于 SSH 本地端口转发部分使用的场景），我们入侵了基于 Linux 的目标并提升了权限。对被入侵的 Linux 客户端进行进一步枚举后，我们发现除了连接到当前网络 (`10.11.0.x`) 外，它还有一个网络接口似乎连接到了另一个网络 (`192.168.1.x`)。在这个内部子网上，我们发现了一台可用共享的 Windows Server 2016 机器。

# 使用 Kali Linux 进行渗透测试 2.0

为了在实验室环境中模拟这一场景，我们将再次从我们的 fuzzed Linux 客户端运行 `ssh_local_port_forwarding` 脚本。

环境搭建完成后，我们可以使用 `ssh -D` 来指定本地动态 SOCKS4 应用端口转发（再次通过 SSH 隧道），语法如下：

```
ssh -N -D <address to bind to>:<port to bind> <username>@SSH server address
```

列表 641 - 通过 SSH 进行动态端口转发的命令行提示符

考虑到上述语法，我们可以在 Kali Linux 机器上通过 TCP 端口 `8080` 创建一个本地 SOCKS4 应用代理 (`-N -D`)，该代理将所有流量通过被攻的 Linux 机器隧道到网络中的目标主机，我们以学生身份 `(`student@10.11.0.128`)` 登录该机器：

```
kali@~$ sudo ssh -N -D 127.0.0.1:8080 student@10.11.0.128

student@10.11.0.128$ password:
```

列表 642 - 在 TCP 端口 `8080` 上到目标网络创建动态 SSH 隧道

虽然我们已经启动了一个可以通过 SSH 隧道将应用流量路由到目标网络的代理，但我们必须以某种方式引导侦察和攻击工具使用该代理。在 `ProxyChains`⁵⁹³ 的帮助下，我们可以通过 HTTP、SOCKS4 和 SOCKS5 代理运行任何网络应用程序。

要配置 Proxchains，我们只需编辑主配置文件 (`/etc/proxchains.conf`) 并我们的 SOCKS4 代理添加到：

```
kali@~$ cat /etc/proxchains.conf

...

[ProxyList]

# add proxy here ...

# meanwhile

# defaults set to "tor"

socks4 127.0.0.1 8080
```

列表 643 - 将我们的 SOCKS4 代理添加到 ProxyChains 配置文件

该配置如图 340 所示：

![](img/f99f528ca9845f4c256ce54e882b1345_606_0.png)

> ⁵⁹³ (Adam Hamsik, 2017), https://github.com/haad/proxychains

# 使用 Kali Linux 进行渗透测试 2.0

# 攻击性安全

![](img/f99f528ca9845f4c256ce54e882b1345_606_0.png)

防火墙没有入站或出站过滤器。动态端口转发：`sudo ssh -D 127.0.0.1:8080 student@10.11.0.128`

拥有 root 权限和暴露的服务后，我们可以在机器的 TCP 端口 `8080` 上设置 SOCKS 代理。我们通过目标主机 Linux 客户端 Attacker-Windows Server 2016 建立一个动态 SSH 隧道。图 300：动态端口转发图

通过 SOCKS4 代理运行我们的工具，在每个命令前加上 `proxychains`。例如，让我们尝试使用 `nmap` 扫描内部网络上的 Windows Server 2016 机器。在本例中，除了参数外，我们没有对 `proxychains` 应用任何选项：

```
kali@kali: sudo proxychains nmap -sT -Pn 192.168.1.110
```
