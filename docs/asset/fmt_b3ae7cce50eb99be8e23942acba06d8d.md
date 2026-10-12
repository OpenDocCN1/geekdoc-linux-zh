
⁷¹⁹ (Empire Project, 2019), https://github.com/EmpireProject/Empire
⁷²⁰ (Will Schroeder, 2016), https://www.harmj0y.net/blog/empyre/building-an-empyre-with-python/
⁷²¹ (BC Security, 2019), https://github.com/BC-SECURITY/Empire
⁷²² (BC Security, 2019), https://github.com/BC-SECURITY/Empire/tree/dev

![](img/ec25e59d75726b7041242a56d3376832_717_0.png)

```bash
kali@kali:/opt/Empire$ sudo ./setup/install.sh
...
```

*列表 819 - 在 Kali Linux 上安装 PowerShell Empire*

Empire 允许渗透测试人员通过共享私钥，进而共享密码，在多个服务器之间进行协作。但是，我们只安装单个实例，因此我们按 `Return` 键在密码提示符处生成一个随机密码。

```text
[>] Enter server negotation password, enter for random generation:
```

*列表 820 - 生成随机的服务器协商密码*

安装完框架后，我们可以使用名为 `empire` 的 Python 脚本启动 Empire。

```bash
kali@kali:/opt/Empire$ sudo ./empire
...
=======================================================
[Empire]  Post-Exploitation Framework
=======================================================
[Version] 2.5 | [Web] https://github.com/empireProject/Empire
=======================================================
285 modules currently loaded
0 listeners currently active
0 agents currently active
(Empire) >
```

*列表 821 - 启动 PowerShell Empire*

#### 23.1.1 PowerShell Empire 语法

我们可以使用 `help` 来列出 Empire 中可用的各种命令，包括监听器、暂存器、代理和模块。

```text
(Empire) > help
Commands
=======
agents          Jump to the Agents menu.
creds           Add/disp;ay credentials to/from the database.
exit            Exit Empire
help            Displays the help menu.
interact        Interact with a particular agent.
list            Lists active agents or listeners.
```

![](img/ec25e59d75726b7041242a56d3376832_719_0.png)

| 命令 | 描述 |
| :------ | :---------- |
| listeners | 与活动监听器交互。 |
| load | 从非标准文件夹加载 Empire 模块。 |
| plugin | 加载插件文件以扩展 Empire。 |
| plugins | 列出所有可用和活动的插件。 |
| preobfuscate | 预先混淆 PowerShell module_source 文件 |
| reload | 重新加载一个（或所有）Empire 模块。 |
| report | 生成报告 CSV 和日志文件：sessions.csv, credentials.csv, mas |
| reset | 重置全局选项（例如 IP 白名单）。 |
| resource | 从文件读取并执行一系列 Empire 命令。 |
| searchmodule | 搜索 Empire 模块名称/描述。 |
| set | 设置全局选项（例如 IP 白名单）。 |
| show | 显示全局选项（例如 IP 白名单）。 |
| usemodule | 使用 Empire 模块。 |
| usestager | 使用 Empire 暂存器。 |

列表 822 - 来自 `help` 命令的 Empire 选项

### 23.1.2 监听器与暂存器

我们将通过简要介绍监听器和暂存器来开始对 Empire 的探索。相当于 Metasploit 的 `multi/handler`，监听器接受来自各种 Empire 代理的入站连接。

暂存器是由 Empire 生成的短小代码片段，在受害者机器上执行并回连到监听器。它们建立受害者和攻击者之间的连接，并执行其他任务以促进分阶段载荷的传输。

要开始 Empire 会话，我们首先进入监听器上下文，然后使用 `uselister` 打印可用监听器，随后按空格键和双 Tab 键以启用 Empire 的 Tab 补全功能。

```text
(Empire) > listeners
[!] No listeners currently active
(Empire: listeners) > uselister
  dbx  http_com    http_hop  meterpreter
  http  http_foreign http_map1 redirector
```

列表 823 - 列出监听器类型

`http` 监听器是最基本的监听器，就像 Metasploit 中的 `windows/meterpreter/reverse_http` 载荷一样，它通过一系列 HTTP GET 和 POST 请求进行通信，以模拟合法的 HTTP 流量。

> 重定向器（`redirector`）监听器也值得一提，因为它创建了一个枢轴点，使其能够通过被入侵的主机与内部网络进行通信。

一旦选择了监听器，我们可以运行 `uselister` 命令选择它，并运行 `info` 显示信息和语法：

```text
(Empire: listeners) > uselister http
(Empire: listeners/http) > info
```
