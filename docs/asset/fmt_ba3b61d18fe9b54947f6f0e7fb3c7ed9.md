
使用 Kali Linux 2.0 进行渗透测试

- 列表 728 - 使用 DCSync 为 Administrator 转储密码哈希值

转储内容包含与最后二十九个使用的用户密码相关的多个哈希值，以及用于上述 AES 加密的的哈希值。

使用上述技术，我们可以向域控制器请求复制更新，并在获取 Active Directory 中每个账户的密码哈希值时，无需登录域控制器。

### 21.6 总结

本模块提供了 Active Directory 及其相关安全的概述和一些见解。虽然这里提到了并解释了许多技术，但还有许多其他值得探索的技术。

特别应该注意的是，本模块中对操作安全（`opsec`）的关注较少，取决于客户的成熟程度，在执行枚举和横向移动时，如果不盲目执行所示的每一个命令和技术，花些精力避免被检测，这可能是值得的。

![](img/f99f528ca9845f4c256ce54e882b1345_676_0.png)

[+] 其他特定模块参数为：`missing`, `advanced`, `evasion`, `targets`, `ac`

列表 734 `show` 命令的帮助标志

要激活一个模块，请使用 `use` 命令后接模块名称（例如示例中的 `auxiliary/scanner/portscan/tcp`）。此时，提示符将显示该模块。我们可以使用 `back` 退出当前上下文并返回主 `msf5`：

```
msf5 > use auxiliary/scanner/portscan/tcp
```

```
msf5 auxiliary(scanner/portscan/tcp) > back
```

```
msf5 >
```

列表 735 - Metasploit `use` 和 `back` 命令

`back` 的变体是 `previous`，它可以让我们切换到上一个选择的模块而不是返回提示符：

```
msf5 > use auxiliary/scanner/portscan/tcp
```

```
msf5 auxiliary(scanner/portscan/tcp) > use auxiliary/scanner/portscan/syn
```

```
msf5 auxiliary(scanner/portscan/syn) > previous
```

```
msf5 auxiliary(scanner/portscan/tcp) >
```

列表 736 - Metasploit `previous` `previous` 命令

大多数模块在运行之前都需要选项（`show options`）。我们可以使用 `set` 配置选项，并使用 `set` 和 `unset` 分别可以移除全局选项。

```
msf5 auxiliary(scanner/portscan/tcp) > show options
```

模块选项 (`auxiliary/scanner/portscan/tcp`):

| 名称 | 当前设置 | 强制 | 描述 |
|---|---|---|---|
| `CONCURRENCY` | 10 | yes | 每个线程检查的并发端口数 |
| `DELAY` | 0 | yes | 每个线程的连接之间的延迟 |
| `JITTER` | 0 | yes | 延迟抖动因子（按宽度最大值） |
| `PORTS` | 1-1000 | yes | 要扫描的端口（例如 22-25,80,110-900） |
| `RHOSTS` |  | yes | 目标地址或 CIDR 标识符 |
| `THREADS` | 1 | yes | 并发线程数 |
| `TIMEOUT` | 1000 |  | 套接字连接超时时间（毫秒） |

列表 737 - `auxiliary/scanner/portscan/tcp` 的选项

例如，要使用 `scanner/portscan/tcp` 模块对我们的 Windows 工作站进行扫描，必须先用 `set` 命令设置远程主机 IP 地址（`RHOSTS`）。

```
msf5 auxiliary(scanner/portscan/tcp) > set RHOSTS 10.11.0.22
RHOSTS => 10.11.0.22
```

列表 738 - `RHOSTS` 选项

配置好模块后，我们可以运行它：

```
# msf5 auxiliary(scanner/portscan/tcp) > run
```

- [+] 10.11.0.22: - 10.11.0.22:80 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:135 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:139 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:445 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:3389 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:5040 - TCP OPEN
- [+] 10.11.0.22: - 10.11.0.22:9121 - TCP OPEN

[*] 扫描了 1 个主机主机 (100% 完成)

[*] 辅助模块执行完成

列表 730 - 使用 Metasploit 进行端口扫描

### 22.1.2 Metasploit 数据库访问

如果 `postgresql` 服务正在运行，Metasploit 将把发现的主机、服务或凭据的结果和信息记录在一个方便、可访问的数据库中。

在以下列表中，数据库已经填充了我们在上一节运行的 TCP 扫描结果。我们可以使用 `services` 命令显示这些结果：

```
msf5 auxiliary(scanner/portscan/tcp) > services
Services
host             port proto name state info
---- ---- ---- ---- ---- 
10.11.0.22       80   tcp               open
10.11.0.22       135  tcp               open
10.11.0.22       139  tcp               open
10.11.0.22       445  tcp               open
10.11.0.22       3389 tcp               open
10.11.0.22       5040 tcp               open
10.11.0.22       9121 tcp               open
```

列表 740 - 数据库中的 TCP 端口扫描结果

`basic services` 命令显示所有端口，但我们通过端口号 (`-p`)、服务名称 (`-s`) 进行过滤，并在 `services -h` 的帮助输出中查看更多内容。
