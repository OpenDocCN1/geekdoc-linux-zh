
INetSim process started (PID 3544)    labMalwareLab: $ `netstat -an`
Active Internet connections (servers and established) State
Proto Recv-Q Send-Q Local Address         Foreign Address       State
udp 0               0 127.0.0.1:*               0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:*               0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:123          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:113          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:117          0.0.0.0:*               LISTENER
tp 000 00..0..011000000.00.00                                00  000.0.0.1.1          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:14311         0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:53          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:113          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:117          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:14667         0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:11110         0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:123          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:111          0.0.0.0:*               LISTENER
tp 0               0 127.0.0.1:511          0.0.0.0:*               LISTENER
tudp 0               0 127.0.0.1:113          0.0.0.0:*               LISTENER
tudp 0               0 127.0.0.1:117          0.0.0.0:*               LISTENER
tudp 0               0 127.0.0.1:117          0.0.0.0:*               LISTENER
tudp 0               0 0.0.0.0:3337         0.0.0.0:*               LISTENER
tudp 0               0 127.0.0.1:149         0.0.0.0:*               LISTENER
tudp 0               0 127.0.0.1:123          0.0.0.0:*               LISTENER
FIGURE 6.23-使用 INetSim 解析 DNS 查询

另一种简单的解决方案是修改系统 hosts 文件——通过将 IP 地址与主机名相关联来作为解析主机名的手段。在 Linux 系统上，hosts 文件位于 `/etc` 目录。

要修改 hosts 文件中的项，请进入 `/etc` 目录并使用 `vi` 或偏好的文本编辑器打开 hosts 文件。编辑文件时确保你拥有正确的用户权限，以便保存更改。

通过输入你希望域名解析到的 IP 地址，通常是虚拟 Linux 系统的 IP 地址，后跟一个空格，然后是需要解析的目标域名来添加相关域名。hosts 文件提供了示例项作为参考。

## 网络轨迹：链式追踪

在调整环境解析样本的域名，并将域名指向实验室网络上虚拟服务器的 IP 地址后，监控样本的反应及其对受害系统的影响。

- 密切跟踪网络流量，因为添加新的域名项可能会样本表现出新的行为。例如，为了追踪图 6.24 中恶意软件发起的请求，数字调查人员应在指向的虚拟 Linux 主机上启动 Web 服务器；这样受感染系统就可以加入其命令控制结构，见图 6.25。

FIGURE 6.24—网络轨迹

FIGURE 6.25—在 Web 服务器日志中捕捉样本的请求

# 网络特征与网络痕迹证据

网络特征证据包括归因于可疑程序的网络流量中的痕迹和人工制品。同样，网络痕迹证据是指可疑恶意软件的执行和表现而引入网络流量并最终进入受害者系统的文件或其他人工制品；反之，也是受害者在线活动产生。从网络特征和痕迹证据中可以获取以下调查科学信息：

- 解析域名的目的。在解析域名后，恶意软件样本会揭示其为了维持感染生命周期所需的远程资源的性质和目的。例如，如果解析出的域名显示恶意样本正在请求 Web 服务器，并在实验室环境中使用 Web 服务器来捕获轨迹，Web 服务器日志可能会揭示可疑程序需要解析该域名以返回并下载额外文件。

- 模块化恶意代码的标识符可能作为痕迹证据被引入受害者系统。如果识别出证据并可能获取痕迹文件，请模拟恶意软件样本像在真实环境中那样完全执行。如果可能，离散地检索并分析请求的文件，并将它们内部托管在您的恶意软件实验室服务器上，以执行样本的运行轨迹。

- 功能解释。在网络特征证据中捕获的样本所显示的功能，可以提供关于可疑样本性质和目的的进一步见解。例如，如果特征证据显示木马程序尝试连接到其他在线资源，如 Web 或 FTP 服务器并秘密下载额外的恶意软件文件，那么它可能是一个木马下载器。

- 元数据。嵌入在捕获 Web 流量中的网络特征是 user-agent 字符串。user-agent 字符串识别 Web 浏览器并提供如浏览器访问的 Web 服务器等某些系统细节。在图 6.25 中，user-agent 字符串为“Opera/9.80 (X11; Linux i686) Presto/2.12.388 Version/12.16。”数字调查人员应研究并记录与 user-agent 字符串相关的发现；这些元数据可能为攻击者或恶意软件的功能和目的提供进一步见解。

> 65 关于针对 Linux 及其他操作系统的木马下载器示例，请参见：http://www.zdnet.com/cross-platform-trojan-checks-your-os-attacks-windows-mac-linux-7000000656/ .

# LINUX 系统恶意软件取证指南

## 使用 Netcat 监听器

用于拦截 Web 请求内容和其他网络连接的另一种方法是在实验室网络中的另一台主机上建立 netcat 监听器。

- 回想之前的章节，`netcat` 是一个强大的网络实用程序，它通过 TCP/IP 或用户数据报协议 `UDP` 跨网络连接进行读写。这对于在可疑程序用于连接的随机 TCP 和 UDP 端口上建立网络监听器非常有帮助：`netcat` 因其灵活性和用途的多样性成为许多数字调查人员喜爱的工具，而且它是许多 Linux 发行版中原生安装的。在获可疑程序请求连接的远程端口后，数字调查人员可以在恶意软件实验室 Linux 服务器的目标端口上建立 netcat 监听器来利用 `netcat`。

- 使用图 6.25 中的示例，可疑程序请求通过 80 端口从 Web 服务器下载文件：要在 Linux 服务器的 80 端口上建立 netcat 监听器，请使用 `nc` 命令并配合 `-v` 详细、`-l` 监听和 `-p` 端口开关，并识别目标端口号。`-v` 开关不是必须的，没有它也能提供更多回复，如图 6.26 所示。

```
root@MalwareLab:~# nc -lv -p 80
Listening on [172.16.16.130] [family 2, port 80]
Connection from [172.16.16.130] [http] accepted (family 2, sport 52005)
GET /index.html HTTP/1.1
User-Agent: Opera/9.0 (X; Linux 1686) Presto/2.12.388 Version/12.16
Host: 172.16.16.130
Accept: text/html,application/xml;q=0.9,application/xhtml+xml,image/png,image/webp,image/jpeg,image/gif,image/x-xmap,*;q=0.1
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
GET /index.html HTTP/1.1
User-Agent: Opera/9.0 (X; Linux 1686) Presto/2.12.388 Version/12.16
Host: 172.16.16.130
Accept: text/html,application/xml;q=0.9,application/xhtml+xml,image/png,image/webp,image/jpeg,image/gif,image/x-xmap,*;q=0.1
Accept-Language: en-US,en;q=0.9
Accept-Encoding: gzip, deflate
Connection: Keep-Alive
```

FIGURE 6.26- 用于收集网络特征证据的 netcat 监听器

## 检查进程活动

- 在对可疑程序进行动态分析期间，数字调查人员希望获取进程上下文，或作为生成进程的全视角，以及……

## 恶意样本分析

- 使用 Linux 系统原生的 `top` 命令来获取实时 CPU 使用率。数字调查人员特别感兴趣的是按 CPU 消耗降序排列的进程。默认情况下，`top` 每 5 秒刷新一次，图 6.27。

## 使用 top 评估系统使用

- 除了使用 `top` 确定资源使用外，使用 `ps` 命令检查所有进程也是很有用的。使用 `aux` 或者 `-ef` 开关允许数字调查人员获取有关进程名的详细信息，这通常表现为伪装。

## 使用 pstree 运行进程

- 显示运行进程的另一种工具是 `pstree`，它以树图显示运行进程。在恶意软件分析中，尝试评估进程关系时 `pstree` 特别有用，因为它本质上提供了进程的“祖视图”。在图 6.28 中，在 `pstree` 中发现了可疑进程 `WIFIAPT`。

```
malwarelab@MalwareLab:~ pstree
<excerpt>
init--NetworkManager--dhclient
--dnsmasq-[NetworkManager]
--WIFIAPT--(WIFIAPT)
--accounts-daemon--acpid
--anacron--sh--run-processes--apt-get
```

FIGURE 6.28— 通过 pstree 发现可疑进程

- 要获取有关 `pstree` 显示进程的更细粒的信息，请使用 `-a` 开关显示显示进程的命令行参数，并使用 `-p` 开关显示分配的 PID，图 6.29。

```
malwarelab@MalwareLab:~ pstree -a -p
<excerpt>
init,1
--NetworkManager,943
--dhclient,982 -d -4 -sf
--dnsmasq,1199 --no-resolve --keep-in-foreground
--(NetworkManager),952
--NetworkManager),983
--WIFIAPT,3783
--(WIFIAPT),3784
--accounts-daemon,1421
--acpid,1109 -s /etc/acpi/events -s /var/run/acpid.socket
--anacron,1106 -s
--sh,2463 -c nice run-processes --report /etc/cron.daily
--run-parts,2464 --report /etc/cron.daily
```

FIGURE 6.29— 使用 pstree 识别命令行信息和 PID

# 使用 GUI 工具检查运行进程

- 某些数字取调查人员倾向于在对可疑二进制文件进行运行时分析时，使用基于图形的实用程序检查运行进程。

- 使用 Linux Process Explorer⁶⁹ 或类似的分析工具收集基本的进程信息，如进程名称和 PID。在随后的查询中，寻求特定的进一步细节以获取进程详情：

- 进程名称和 PID

- 时间上下文

- 内存消耗

- 进程执行的程序映射

- 进程与用户的映射

- 子进程

- 线程

- 被调用的库和依赖项

- 用于调用该进程的命令行参数

- 进程的内存内容

- 与系统状态和产物的关联上下文

- 此外，通过在 Linux Explorer 主面板中对可疑进程点击右键，数字取调查人员将看到许多其他可用于进一步处理的功能，例如进程环境、线程和相关的 TCP/IP 连接，如图 6.30 所示。

![](img/aa19fd7b1fc75dc422144821b9c6657c_474_0.png)

图 6.30—使用 Linux Process Explorer 分析进程

⁶⁹ 有关 Linux Process Explorer 的更多信息，请访问 http://sourceforge.net/projects/procexp/

# 进程内存映射

除了检查受感染系统上的进程外，数字取调查人员还应该考虑在查看可疑程序处于执行状态并作为进程运行时其内存映射。

- 应将内容与之前通过进程监控实用程序捕获以及在 `/proc/<pid>/maps` 文件中识别出的信息进行比较，以发现任何不一致或异常。

- `pmap` 大多数 Linux 发行版的原生工具⁷ 可以识别进程调用的模块，并揭示相应库加载的内存偏移，如图 6.31 所示。

# 获取和检查进程内存

在获取有关受感染系统上运行进程的充分上下文，特别是由恶意软件样本创建的进程后，捕获进程的内存内容以便进一步检查非常有帮助。

- 正如第 2 节所述，有许多方法和工具可以从 Linux 系统上的运行进程中转储进程内存，其中某些依赖于 Linux 系统的原生实用程序，而另一些则需要实现额外的工具。

- 在获取可疑进程的内存内容后，这些内容包含任何关于可疑程序的详细线索。如第 2 节提到的，数字取调查人员可以使用 Linux 系统的原生工具 `strings` 解析内存转储内容，以查找任何有意义的文本引用。此外，如果使用 `gcore`⁷ 获取了核心镜像，格式为 ELF 格式，可以使用 `gdb`⁷、`objdump`⁷ 和其他工具进行探测，以检查文件内部结构。

- 同样，实现 Tobias Klein 的 Process Dumper⁷ 并结合 Memory Parser⁷，将允许数字取调查人员获取并彻底解析可疑进程的状态、关联数据、代码映射、元数据和环境，以寻找任何正确或异常的信息。

⁷⁰ 有关 `pmap` 的更多信息，请访问 procps.sourceforge.net/.

⁷¹ 有关 `gcore` 的更多信息，请访问 http://manpages.ubuntu.com/manpages/lucid/man1/gcore.1.html。

⁷² 有关 `gdb` 的更多信息，请访问 http://www.gnu.org/software/gdb/

⁷³ 有关 `objdump` 的更多信息，请访问 http://www.gnu.org/software/binutils/

⁷⁴ 有关 Process Dumper 的更多信息，请访问 http://www.trapkit.de/research/forensic/pd/

⁷⁵ 有关 Memory Parser 的更多信息，请访问 http://www.trapkit.de/research/forensic/mmp/index.html。

# 第 6 章恶意软件样本分析

```
malwarelab@MalwareLab:~$ pmap -x 3783
```
