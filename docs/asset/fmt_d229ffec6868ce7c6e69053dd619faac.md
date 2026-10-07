
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

# 结合 UNIX 和 AQUA

## 额外

另外两个命令可以配合资源分叉工作，以确保 Mac OS Finder 可以访问元数据。这两个命令是 `CpMac` 和 `MyMac`。`CpMac` 是 `cp` 的版本，用于复制带有资源分叉的文件；`MyMac` 是 `mv` 的版本，用于在保留资源分叉的同时移动文件。

`CpMac` 和 `MyMac` 命令并没有自动安装在所有 Mac OS X 上，但位于 Mac OS X Developer Tools CD 中。有关安装 Developer Tools 的更多信息，请参见第 12 章。

`CpMac` 和 `MyMac` 的执行文件存储在 `/Developer/Tools` 目录下。如果你没有将该目录添加到 shell 的路径中，你需要输入完整路径来使用这些命令。

示例：

```bash
[--]user du -s cat-pics/
48744 cat-pics/
[--]user cp -r cat-pics/ cat-pics-cp
[--]user du -s cat-pics-cp
39782 cat-pics-cp
[--]user /developer/Tools/CpMac -r cat-pics/ cat-pics-MyMac
[--]user du -s cat-pics-MyMac
48744
```

# 复制目录

- 1 输入 `ditto -rsrcfork` 和一个空格。
- 2 输入目录名和一个空格。
- 3 输入目标目录名并按回车。`ditto` 命令会创建目录的副本并复制资源分叉。

# 从 SHELL 运行 APPLESCRIPT

你可以从命令行运行 AppleScript 命令或文件，让你能够访问并控制 Mac OS。AppleScript 是一种内置于 Mac OS 的简单但强大的编程语言。因为它使用的语法与英语相似，因此非常容易阅读和理解。例如，要显示一个弹出对话框，你可以使用以下 AppleScript：

第一个版本运行 AppleScript；你不需要设置脚本文件。如果你省略了脚本文件，`oscript` 命令将从标准输入读取脚本行。

命令的第二个版本执行命令行上指定的单行脚本。如果你想执行多行脚本，可以包含 `-e` 参数。

```applescript
tell Application "Finder" to display dialog "Good morning"
```

AppleScript 遵循开放脚本架构 (OSA) 标准。要查看计算机上安装的 OSA 语言完整列表，你可以输入 `oscript` 命令。从命令行执行 OSA 语言脚本有两种方法：

```bash
osascript -e 'line of script'
```

你使用 AppleScript 语言的方式比这里显示的更多。你可以使用 AppleScript 控制 Mac OS 应用程序。要了解更多 AppleScript 语言，请访问 www.apple.com/applescript。

# 运行单行 APPLESCRIPT

# 让你的 UNIX SHELL 说话

- 输入 `oscript` 和一个空格。
- 输入 `-e` 和一个空格。
- 在引号内输入一行 AppleScript，并按回车。

`oscript` 命令会执行该 AppleScript 行。

- 输入 `oscript -e`、一个空格和一个单引号。
- 输入 `tell` 后加一个空格和双双引号。

`oscript` 命令告诉应用程序朗读文本。

## 应用它

你可以使用 `osascript` 在每次使用 `cd` 命令时宣布新目录。它使用了特殊的 `tcsh` 命令。

- 创建一个存放脚本的目录，例如 `~/Library/osascript`。
- 在该目录下创建一个 shell 脚本 `say-dir.sh`，内容为 `osascript -e 'tell system to say $cwd'`
- 在你的 `.tcsh` 文件中添加别名来设置 `cwd`：`alias cwd='source ~/Library/osascript/say-dir.sh'`
- 输入 `source ~/.tcsh` 来加载别名。

每当你切换目录时，`cwd` 别名会执行。因为当前路径使用了 AppleScript `say` 命令。

使用这种方法有一个小问题：`cd` 命令直到路径朗读完才会结束。

# 运行 APPLESCRIPT 文件

- 使用文本编辑器创建一个包含 AppleScript 的文本文件。
- 输入 `osascript` 和一个空格。
- 输入脚本名称并按回车。

`osascript` 命令执行该 AppleScript 文件。

# 创建可点击的 SHELL 脚本

你可以创建可以通过双击 Mac OS X Finder 中的图标运行的 shell 脚本。如果脚本文件名以 `.command` 结尾，则它是可点击的。

普通的 shell 脚本不是可点击的。双击脚本图标会在文本编辑器中打开它而不是运行它。要使其变为可点击，你可以通过 `chmod` 命令处理脚本并以 `.command` 命名。

当你双击 .command 文件时，终端程序会打开一个新窗口并执行窗口中的命令。例如，如果你想在 shell 窗口中运行 `top` 程序，可以编写这样的脚本：

```csh
#!/bin/csh
# top.command:
# 此脚本将根据你喜欢的选项启动 top 命令。
# 可以双击 Finder 中的文件图标运行。
```

```csh
top -u -s5 # 按 CPU 排序，每 5 秒更新一次
```

如果你将此文件保存为 top.command 并将其设置为可执行，你就可以通过双击图标来启动 top 命令。你也可以通过将其重命名为 .command 文件来制作其他类型的可执行程序。

## 将路径拖入终端窗口

你可以通过将 Mac OS Finder 中的任何文件图标拖到终端（Terminal）窗口来使用该文件。文件的路径出现得就像是你手动输入的一样。当你深处于文件夹层级中，并且想要对找到的文件使用 shell 命令时，这种方法非常有用。通过这种方式你可以省去打字时间，并大大减少输错路径的概率。例如，要查看文件的目录列表，可以输入部分命令并加一个空格：

松开鼠标按钮，文件不会移动（通常你将图标拖到新文件夹时，文件会移动）。相反，文件的完整路径将粘贴到你的终端窗口中：

```
ferro@user ls -l
/Users/user/Pictures/kitty/orolin1.jpg
```

然后按下回车键（Return）来执行命令。此操作适用于任何文件（包括文件夹），可以将拖入文件夹的目录路径粘贴到终端。

如果你正在输入一个带有多个参数的命令（例如 `diff` 命令），可以将多个文件一起拖到终端。你需要在每个文件之间输入空格，否则路径将不会分开，并被视为一个很长的路径。

```
ferro@user ls -
```

然后切换到 Finder 并找到该文件。点击并按住文件图标上的鼠标键，将其拖到终端窗口可见的任何部分。你不需要看到整个窗口，只需看到部分即可。当：

- 输入一个带有文件名参数的命令时。
- 在 Mac OS X Finder 上找到文件图标。
- 松开鼠标按钮。文件的完整路径将插入到光标处。
- 点击并将图标拖到终端窗口上。

## 连接互联网

互联网是遍布全球的系统和网络的松散连接集合。这个超级网络让新泽西的人能够向埃塞俄俄的人发送电子邮件，让加利福尼亚的人能够在网络上找到他们宾夕法尼亚州祖母的食谱，并让人们能够与可能从未面对面交流的人聊天并建立有意义的关系。

如果你的 Macintosh 是家庭系统，你可能会使用拨号上网或 DSL 连接到网络。如果你的 Macintosh 放在办公桌上，你可能会连接到安装整座建筑内的网络布线。连接后，你可以从客户端使用互联网的所有服务，如 `telnet` 和 `ftp`、访问网页和浏览。

将 Mac OS X 连接互联网相对简单。根据你的资源和情况，你可以建立拨号、数字用户用户线路（DSL）和局域网（LAN）连接。

Unix 系统的设计初衷就是网络化的。事实上，第一批 Unix 系统以及在第一个互联网工作网上连接不同位置系统的首次尝试是同时代的。Mac OS X 也不例外。Mac OS X 网络——即一组被称为传输控制协议/网协议（TCP/IP）的协议——正是。

- 系统偏好（System Preferences）窗口打开。
- 你的拨号连接已建立。
- 在“网络与网络”（Internet & Network）下选择“网络”（Network）。

## 使用网络命令

### 额外内容

连接互联网允许你利用丰富的信息和服务。了解这种连接的工作原理，将有助于你在问题发生时更容易地报告和解决问题。

对于拨号账户，你通常不需要担心系统将使用的 IP 地址、子网掩码、DNS 服务器或默认路由器的设置。尽管这些信息对你的网络连接至关重要，但你的互联网服务提供商（ISP）会在你连接时将其分配给你。如果你的 Macintosh 连接到局域网，你可以使用静态 IP 地址——或者使用 DHCP 服务器在你启动系统时分配的地址。

无论这些信息如何被分配，你的系统都需要一个唯一的 IP 地址来识别其为网络成员，一个子网掩码允许系统确定局域网的范围，一个默认路由器来引导远程连接，以及一个 DNS 服务器允许你通过名称定位系统。

| 系统偏好 | 编辑 | 视图 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- |
| 显示全部 | 显示 | 声音 | 网络 | 启动磁盘 |
| 位置 | 自动 | | | |
| 显示 | 内置以太网 | | | |
| TCP/IP | PPPOE | PPPoE | AppleTalk | 代理 |
| 配置 | 手动 | | | |
| IP 地址 | | | | |

| 系统偏好 | 编辑 | 视图 | 窗口 | 帮助 |
| :--- | :--- | :--- | :--- | :--- |
| 显示全部 | 显示 | 声音 | 网络 | 启动磁盘 |
| 位置 | 自动 | | | |
| 显示 | 内置以太网 | | | |
| TCP/IP | PPPOE | PPPoE | AppleTalk | 代理 |
| 配置 | 手动 | | | |
| IP 地址 | | | | | |

- 系统偏好窗口打开。
- 你的拨号连接已建立。
- 在“网络与网络”（Internet & Network）下选择“网络”（Network）。

## 设置网络

- 系统偏好窗口打开。
- 你的拨号连接已建立。
- 在“网络与网络”（Internet & Network）下选择“网络”（Network）。

## 设置拨号连接

- 系统偏好窗口打开。
- 你的拨号连接已建立。
- 在“网络与网络”（Internet & Network）下选择“网络”（Network）。

## 查询互联网地址

你可以查询 IP 地址以验证你是否在同一网络上。`nslookup` 命令允许你查找互联网主机的 IP 地址。

子网掩码允许系统确定局域网的范围。子网掩码是一个值为 255.255.255.0 的值，标记了网络部分结束的位置。默认路由器引导远程连接。DNS 服务器允许你通过名称定位系统。

所有这些地址对于网络连接都至关重要，最好使用完全限定域名（如 `www.apple.com`）而不是 IP 地址（如 `17.254.0.91`）连接互联网。为了实现这种可能，你需要使用一种将名称转换为 IP 地址并反之亦然的服务。这种代替 IP 地址转换名称的服务被称为域名系统，简称 DNS。`nslookup` 命令允许你在命令行中使用 DNS 服务。

- 系统偏好窗口打开。
- 你的拨号连接已建立。
- 在“网络与网络”（Internet & Network）下选择“网络”（Network）。

### 额外

只有当你的系统进行 DNS 查询时，你才能有效使用互联网。服务器能够将域名解析为 IP 地址，并将 IP 地址解析回域名记录。仅包含此类信息的 DNS 记录已经建立，并通过分布式查找服务作为 DNS 提供支持。如果一个系统没有建立 DNS 记录，你只有在知道其 IP 地址的情况下才能在互联网上定位该系统。DNS 已知的系统都经过了注册。

没有任何 DNS 服务器知道所有已注册的系统。相反，每个 DNS 服务器只知道它被认为具有权威性的本地注册系统。然而，DNS 服务器还知道如何与其他服务器通信，以便无论系统和 DNS 服务器相距有多远，查询请求都能得到响应。

尽管很少有用户意识到 DNS 的活动，但他们每次连接到远程系统或浏览网站时都会使用该服务。要检查你的系统在何处查找 DNS 服务，请使用 `cat` 命令显示存储这些信息的 `/etc/resolv.conf` 文件。

| 输入此： |
| [ferro]- cat /etc/resolv.conf |

将显示 `resolv.conf` 文件中 DNS 配置数据的内容。

| 终端 文件 编辑 滚动 字体 窗口 帮助 |
| - |

```
 [ferro]- user nslookup
Default Server: syslo.corenet
Address: 162.33.160.100

- apple.com
Server: syslo.corenet
Address: 162.33.160.100

Non-authoritative answer:
Name: apple.com aknads.net
Address: 172.25.0.9
Aliases: apple.com

- 172.25.0.9
Server: syslo.corenet
Address: 162.33.160.100
```

| 终端 文件 编辑 滚动 字体 窗口 帮助 |
| - |

```
 [ferro]- user nslookup
Default Server: syslo.corenet
Address: 162.33.160.100

- apple.com
Server: syslo.corenet
Address: 162.33.160.100

Non-authoritative answer:
Name: apple.com aknads.net
Address: 172.25.0.9
Aliases: apple.com

- 172.25.0.9
Server: syslo.corenet
Address: 162.33.160.100

- [
[ferro]- user ]
```

- * 输入你输入的 IP 地址返回的 IP 域名。
- * 输入 `exit` 并按回车键。

# 查询域名信息

你可以使用 `nslookup` 或 `whois` 命令收集关于域名的大量信息。如果你想知道如何访问某个域名，这些命令在排故障时非常有用。

DNS 的首要功能是将 IP 地址转换为完全限定域名（如 `www.apple.com`）。次要功能是将完全限定域名转换为 IP 地址。这些是 DNS 为全球范围内系统提供的最直观的服务。DNS 还提供其他有用功能。例如，它维护关于域名及其注册的信息。

你可以通过使用 `nslookup` 命令请求 SOA（起始区域记录）记录来获取关于域名的信息。SOA 记录包含了关于服务器权威性的说明——通常是联系方式。它还包含序列号以及关于区域过期的信息。

DNS MX（邮件交换）记录识别域名的邮件服务器。这些记录决定当另一个系统需要向该域名地址发送电子邮件时连接哪些系统。你也可以使用 `nslookup` 命令获取这些信息。

`whois` 命令查询网络中心（NIC）数据库中的信息。这包括负责注册的服务器。如果你对某个域名好奇或想确定是否可以购买它，`whois` 命令将为你提供一些基础信息。

# 查询域名信息

![](img/8d9b2c31cb5eb6571f0b2dfd7634cf_149_0.png)

```
[-] user%whois apple.com
```

![](img/8d9b2c31cb5eb6571f0b2dfd7634cf_149_1.png)

```
++ Last update of whois database: Thu, Jan 1 UTC
The Registry database包含 COM, NET, ORG, EDU 域名和注册商。
whois _
```

为了执行此项任务，你必须连接到互联网。

- 输入 `whois` 后加一个空格。
- 屏幕显示指定域名的 NIC 信息。

### 额外

DNS 记录包括下表定义的记录。

| 记录类型 | 功能 |
| --- | --- |
| A | 将域名映射到 IP 地址 |
| CNAME | 为系统提供替代名称或别名 |
| PTR | 将 IP 地址映射到域名 |
| MX | 识别域名的邮件交换服务器 |
| SOA | 提供整个域名的信息 |

完全限定域名和 IP 地址之间并不一定是一一对应的关系。一个完全限定域名可以解析为多个 IP 地址。这表明到这些系统的连接是根据整体流量分布的。简单的系统可能有任意数量的完全限定域名，这对于为成百上千客户提供服务的互联网提供商（ISP）来说很常见。对于这项工作，这些名称中的每一个都解析到同一个 IP 地址![](img/8d9b2c31cb5eb6571f0b2dfd7634cf_150_0)
