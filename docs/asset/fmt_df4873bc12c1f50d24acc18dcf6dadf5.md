
与 `KILL_ROUTE` 条目一样，在取消注释后，`PortEntry` 将自动运行。

## 优化 PortEntry 以感知攻击类型

攻击系统的方法有很多。黑客可以扫描 UDP 数据包来扫描系统，也可以进行全 TCP 扫描或仅进行“半开放”扫描。因此，启动 `PortEntry` 有多种方法。你可以根据想要检测的攻击类型以各种方式启动 `PortEntry`。例如，如果你发现许多扫描是使用半开放扫描进行的，你可以使用 `-tcp` 选项，该选项稍后会讨论。你在 `portentry.conf` 文件中指定的选项也会影响你启动 `PortEntry` 的方式。例如，如果你想监听 UDP 流量，可以配置 `portentry.conf` 文件包含对 UDP 端口的额外引用。`PortEntry` 的启动命令包括：

- `portentry -tcp` 将程序作为标准的基于 TCP 的 IDS 。`PortEntry` 仅监听你指定的开放 TCP 端口。
- `portentry -udp` 将程序作为标准的 UDP 主机 IDS 。`PortEntry` 仅监听你指定的开放 UDP 端口。

![](img/a7a9caa80ec85507179284d91e216f9f_228_0.png)

# 第 4 章 • 实现入侵检测系统

- `portsentry-stcp` 允许 `PortSentry` 监听隐蔽 TCP 扫描。该参数与简单的 `-tcp` 参数之间的主要区别在于，`PortSentry` 打开一个套接字来捕获 FIN、半开放连接和全连接扫描。
- `portsentry-atcp` 配置 `PortSentry` 阻止所有连接到你在 `portsentry.conf` 中指定端口的主机。你必须显式地排除任何合法使用列出端口的主机，否则它们将被阻止。正如你可能猜到的那样，此功能可能会导致误报。一种可能的结果是当你尝试使用 FTP、Web 和电子邮件站点时，你可能会将自己屏蔽在外面。
- `portsentry-sudp` 允许 `PortSentry` 监听 UDP 扫描，类似于 `-stcp` 选项。
- `portsentry-audp` 配置 `PortSentry` 对 UDP 扫描变得极度敏感。除了该选项让 `PortSentry` 绑定到 UDP 端口外，它的行为与 `-atcp` 参数完全一致。

根据每个系统的功能及其在网络中的位置，对你拥有的每个系统进行自定义。例如，如果你有任何位于非军事化区（DMZ）的系统——DMZ 是一个通常托管 DNS、Web 甚至电子邮件服务器的特殊网络——你可能希望使用 `-atcp` 选项，以便 `PortSentry` 阻止主机。

## 练习：安装并配置 PortSentry

- 1. 从 `www.psionic.com` 获取 `PortSentry`。
- 2. 将 tar 包置于 `/root/` 目录下。
- 3. 使用以下命令提取文件：

```
tar -zkvf portsentry-1.0.tar.gz
```

- 4. 进入 `portsentry-1.0` 目录。
- 5. `PortSentry` 的安装过程要求你使用带有适用于你操作系统的选项的 `make` 命令。要在你的 Linux 系统上安装 `PortSentry`，请输入以下命令：

```
make linux
```

# 实现入侵检测系统 • 第 4 章 225

- 6. `make` 将编译二进制文件。通过执行以下命令将这些二进制文件安装到 `/usr/local/psionic/portsentry/` 目录：

```
make install
```

- 7. 切换到 `/usr/local/psionic/portsentry/` 目录。
- 8. 使用你喜欢的文本编辑器（如 `pico` 或 `vi`）打开 `portsentry.conf` 文件。
- 9. 滚动到端口配置（Port Configuration）部分，注意中间设置没有被取消注释。这意味着列出的 TCP 和 UDP 端口正在被监控。如果你需要，可以向列表中添加端口。确保使用逗号分隔你想要监控的端口，并用引号结束整个列表。
- 10. 滚动到丢弃路由（Dropping Routes）部分。在经过时检查默认设置。
- 11. 找到通用 Linux（Generic Linux）条目，然后向下滚动到数据包过滤选项。
- 12. 找到 `KILL_ROUTE="/sbin/ipchains -I input -s $TARGET -j DENY -"` 并取消注释。该条目使用 `ipchains` 命令将连接的主机添加到 Ipchains 表中。如果主机扫描你的系统甚至连接到该主机，`PortSentry` 将导致拒绝该主机之间的所有连接。注意：并非所有内核都支持 `ipchains`。如果你想使用 `iptables` 代替，
- 13. 滚动到 TCPWrap 部分并取消注释。
- 14. 最后，滚动到 Banner 部分。
- 15. 编辑 `portsentry.conf` 后，确保保存更改。

img/a7a9caa80ec85507179284d91e216ff_230_0.png

- 16. 使用以下命令启动 PortEntry：

```
portsentry -tcp
```

- 17. 使用以下命令查看 PortEntry 是否正在运行：

```
ps aux | grep portentry
```

- 18. 确认 PortEntry 运行后，使用 `/etc/hosts.deny` 查看添加了什么：

```
cat /etc/hosts.deny
```

- 19. 列出 `iptables` 表：

```
iptables -L
Chain input (policy ACCEPT):
target     source             destination         
DENY       all                ----- yournetwork.com
```

- 20. 该输出显示来自你的所有流量都被拒绝。尝试使用任何 Web 浏览器、FTP 客户端或 Telnet 访问该主机。你将被拒绝。你无法 ping 该主机。

## 练习：清除 ipchains

- 1. 你可能允许被阻止的主机与你的系统通信。通过编辑 `/etc/hosts.deny` 文件消除你刚刚屏蔽的主机的引用来实现。
- 2. 使用以下命令删除第一个 `ipchains` input 条目：

```
ipchains -D input 1
```

- 3. 你可能需要在 input 链中删除额外的规则。如果是，你可以指定额外的规则：

```
ipchains -D input 2
```

- 4. 然后你可以再次列出所有链以确保已阻止所有流量。使用 flush 命令清除所有入口：

```
ipchains -F
```

## 练习：使用 PortSentry 运行外部命令

虽然在所有情况下都不适用，但你可以配置 `PortSentry` 运行外部命令。在本例中，你将对扫描主机运行 `Nmap`。记住，这可能不是最佳选择，因为扫描你的人可能伪造了连接，导致你屏蔽错误的 IP 地址。本练习中显示的命令是使用 `PortSentry` 的一个示例。

- 1. 打开 `/usr/local/psionic/portsentry/portsentry.conf` 文件。
- 2. 滚动到外部命令（External Command）部分，将以下内容写在一行：

```
KILL_RUN_CMD="/usr/bin/nmap -O $TARGET$ >> /usr/local/psionic/portsentry/scan.txt"
```

img/a7a9caa80ec85507179284d91e216f9f_231_0.png

3. 退出文件并保存更改。

4. 彻底杀死 `portsentry`：

```
ps aux | grep pid
```

5. 以标准模式重启 `portsentry`。此模式在使用外部命令时会产生较少的误报：

```
portssentry -tcp
```

6. 确保所有的 `/etc/hosts.deny` 和 Ipchains 条目均已删除。

7. 从远程主机进行扫描。

8. 扫描完成后，检查 Ipchains 和 `/etc/hosts.deny` 文件，确认 `portsentry` 是否已添加了路由。现在，检查 `/usr/local/portsentry/scan.txt`。你会发现你的系统已经连接了来自 `Nmap` 的反向连接。考虑一下如果恶意用户使用 `Nmap` 伪造你的默认网关会发生什么。

9. 执行以下命令持续读取 `/var/log/messages`：

```
tail -f /var/log/messages
```
