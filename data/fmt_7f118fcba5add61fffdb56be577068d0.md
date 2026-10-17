
# `lpr -P myprinter myprintfile.doc`

`lpr` 命令的其他巧妙技巧包括指定打印份数：

```
lpr -P printer -K10 myprintfile.doc
```

同样很棒的功能是，当作业打印完成后，可以通过电子邮件发送给自己发送通知：

```
lpr -P printer -m username@server.com myprintfile.doc
```

这将导致配置正确的机器（具有可用 SMTP 服务的机器）向你发送一份关于指定打印作业的极其详尽的信息集。例如：

```
printer xeroxn40 job root@localhost+363 was successful.
```

状态：

```
waiting for subserver to execute at 2001-06-30-22:40:52.885 A=<NULL>

number=0 process=1987

processing 'dfa986localhost', size 18043, format 'f', IF filter 'filter'

at 2001-06-30-22:40:52.892 ## A=root@localhost+986 number=986

process=1988 *
```

`IF` filter 'filter' finished at 2001-06-30:22:40:53.136 ##
A=root@localhost+number=986 process=1988
printing finished at 2001-06-30:22:40:53.136 A=root@localhost+986
number=986 sending job 'root@localhost+986' to 192.168.21 at 2001-06-30-22:40:53.137 A=root@localhost+986 number=986
process=1988 connecting to '192.168.21', attempt 1 at 2001-06-30-22:40:53.137 A=root@localhost+986 number=986
connected to '192.168.21' at 2001-06-30-22:40:53.144 A=root@localhost+986 number=986
process=1988 requester 192.168.21 at 2001-06-30-22:40:53.144 A=root@localhost+986 number=986
process=1988 sending control file 'cfa986@localhost' to 192.168.21 at 2001-06-30-22:40:53.145 A=root@localhost+986 number=986
process=1988 completed 'cfa986@localhost' to 192.168.21 at 2001-06-30-22:40:53.154 A=root@localhost+986 number=986
process=1988 sending data 'cfa986@localhost' to 192.168.21 at 2001-06-30-22:40:53.155 A=root@localhost+986 number=986
process=1988 completed 'cfa986@localhost' to 192.168.21 at 2001-06-30-22:40:53.155 A=root@localhost+986 number=986
process=1988 done job 'root@localhost+986' to 192.168.21 at 2001-06-30-22:40:53.195 A=root@localhost+986 number=986
process=1988 subserver pid 1988 exit status 'SUCCESS' at 2001-06-30-22:40:53.220 A<NULL> number=0 process=2234
xerom40@localhost: job 'root@localhost+986'
```

将某人称为打印客户端，因为实际应用程序是向打印子系统发送请求。

## 打印任务

Windows 2000 生成的打印任务在接收到 SMB 数据时，通常不会由打印服务进行格式化。打印任务通常在后台打印目录中显示为两个独立的文件：

```
%systemroot%\System32\spool\PRINTERs
```

这可能有所不同且易于更改

如果你想查看打印任务的样子，可以暂停打印机，打印一个任务，然后查看后台打印目录。通常情况下，该目录每个打印任务会有两个文件，两个文件都有编号，并分别以 `.shd`（控制文件）和 `.spl`（后台打印文件或数据文件）作为结尾。

## 本地打印提供程序

打印任务由 `LPP` (`Localspl.dll`) 接收，该实体负责生成后台打印（`.spl`）文件并将作业控制信息放入影子（`.shd`）文件中，以确保在任务被中断或必须重启时，后台打印文件可以重新打印或被处理。

## 远程打印提供程序

由于我们主要关注打印服务的集成，我们需要仔细查看 Windows 2000 中的 `RPP`。总共有三个提供程序 (`RP`)，其功能是接收来自客户端的打印任务。

当连接到服务器并发送打印任务时，它会对比打印提供程序列表中的打印机名称，将打印任务发送给名称与打印任务控制文件项匹配的程序。

当 Windows 2000 打印服务器接收到打印任务时，它会对后台打印服务（`spoolsv.exe`）建立 RPC 连接，该服务转调用打印机路由（`spool.dll`），由后者将打印任务提交给本地打印提供程序，就像发送者是本地客户端一样。

## 打印服务器

打印服务器服务是检查后台打印信息并判断后台打印程序是否需要修改打印文档的组件。一旦检测到任何更改，它就会修改影子文件中的作业格式和备注数据类型。

如果打印任务不是可识别的数据类型，后台打印程序可以将其原样转发。对于任何不是来自 Windows NT 或 Windows 2000 机器的打印任务，打印服务器服务通常会将数据类型设置为 `RAW`（意味着已准备好打印，不要触动！）。

Unix 打印服务通常接受来自 Linux/Unix 主机的 `RAW` 格式打印任务，除非数据另有指示，否则它们不会更改其格式数据。向 Postscript 驱动程序打印的 Linux 和 Unix 将根据需要格式化打印任务，只要目标打印机是兼容 Postscript 的打印机，打印任务就不需要重新格式化。

## 打印池

Windows NT 和 Windows 2000 的另一个强大功能是可以定义单一打印机接口来管理多个物理打印设备。设备应该是相似或相同的，以减少格式错误的可能性。你也可以完全相反，定义具有不同选项的多个打印机接口，以控制特定组的打印，为彩色打印机设置时间限制，并总体分离打印机用户以便更好地控制。

## PostScript 打印机驱动程序

Windows 2000 符合 Adobe 4.3 版本 Postscript 打印机描述标准的 PostScript 打印机驱动程序。这种支持对于使用 Postscript 的 Linux 用户非常重要。通常，打印设备能够打印 Linux 用户提交的几乎任何任务，仅仅因为双方使用的都是 Postscript 语言。

# 在混合环境中查找打印机

为了添加打印机（特别是未连接到本地计算机的打印机），你必须首先找到设备！如果它位于网络上并且是活动目录（`Active Directory`）中目录的对象，你可以使用多种选项来查找它。

现在你可以通过以下几种方法查找打印机：

- 浏览网络
- 输入 UNC (`\\server\printer`) 名称
- 浏览到 IPP（互联网打印协议）打印机的 URL
- 使用活动目录功能搜索打印机

## 添加新发现的打印机

当你找到打印机后，既可以通过“添加打印机向导”（旧方法）添加它，也可以使用新的“点按打印”(`Point and Print`) 选项。点按打印的独特之处在于，服务器将解释你的打印请求，收集驱动程序和文件将该打印机添加到你的计算机配置中，并自动通过网络发送！点按打印通常通过在“我的网络位置”中右键点击打印机，然后点击“连接”来实现。

同时，在你的本地机器上，你可以通过导航到“添加打印机向导”轻松添加打印机。即插用对于支持它或被它支持的打印机效果非常好。如果没有，你可以通过向导轻松添加打印机，指定打印机的品牌和型号，并决定是否共享。

## 什么是 IPP？

大多数 Windows 2000 管理员并不知道自己启用了互联网打印，直到他们无意中发现，或者用户发现。你实际上通过在 Windows 2000 中安装互联网信息服务器（`IIS 5`）来启用 IPP 服务。
