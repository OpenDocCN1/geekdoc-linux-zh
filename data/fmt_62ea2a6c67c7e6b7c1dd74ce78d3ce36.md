
`netstat` 程序也可以用于查找远程主机上的名称。以下示例列出了服务器上的名称：

# 在 Windows 98 上工作

第9 章

`C:\WINDOWS>nbtstat -n -a mainserv`

NetBIOS 远程机器名称表

| 名称 | 类型 | 状态 |
| --- | --- | --- |
| MAINSERV | <00> UNIQUE | 已注册 |
| MAINSERV | <03> UNIQUE | 已注册 |
| MAINSERV | <20> UNIQUE | 已注册 |
| ..MSBROWSE_ | <01> GROUP | 已注册 |
| MYGROUP | <00> GROUP | 已注册 |
| MYGROUP | <1C> GROUP | 已注册 |
| MYGROUP | <1D> UNIQUE | 已注册 |
| MYGROUP | <1E> GROUP | 已注册 |

MAC 地址：00-00-00-00-00-00
`C:\WINDOWS>`

某些名称存储在缓存中。可以通过 `nbtstat -c` 命令可以看到它们：
`C:\WINDOWS>nbtstat -c`

节点 IP 地址: `[192.168.100.201]` 范围 ID: []
NetBIOS 远程缓存表

| 名称 | 类型 | 主机地址 | 寿命 [秒] |
| --- | --- | --- | --- |
| MAINSERV | <00> UNIQUE | 192.168.100.1 | 360 |

`C:\WINDOWS>`

想知道你的 WINS 解析是如何工作的吗？尝试 `nbtstat -r` 命令：
`C:\WINDOWS>nbtstat -r`

NetBIOS 名称解析和注册统计数据

通过广播解析 = 0
通过名称服务器解析 = 6
通过广播注册 = 1
通过名称服务器注册 = 8
`C:\WINDOWS>`

`route` 命令是一个至关重要的故障排除工具，允许对路由进行观察和操作。详细描述超出了本章的范围，你可能想查看 `route /?` 命令。

![](img/3a3dd42091ecc215c9b779bbd31cd990_332_0.png)

# 寻找捉摸的共享

可浏览性（Browsability）被赋予了极重要的地位，因为大多数普通 Windows 用户认为 Windows 资源管理器中的可浏览性证明其不存在。他们完全不知道如何将驱动器映射到他们看不见的共享，或者使用命令行访问共享。可浏览性问题必须迅速解决。

第一个问题是该共享是否应该被看到。如果它包含 `browseable=no`、`browse=no` 或 `browse ok=no`，或者由于 `[global]` 中的 `browseable=no` 参数而默认为 `browseable=no`，则它不是设计用来看到的。

你可以使用此命令在 Linux主机上确认预期的可浏览性：

```
$ smclient -NL servername
```

如果前面的命令没有显示可浏览的共享，说明 Samba 配置正在执行某些意料之外的操作，必须对此进行调查。如果此命令显示了共享，则必须调查 Windows 环境，以及子网浏览器的是否存在。

首先，使用以下两个命令之一查看共享是否显示：

```
C:\WINDOWS>net view \mainserv
```

或者

```
C:\WINDOWS>net view /workgroup:mygroup
```

接下来，使用以下两个命令之一查看它是否出现在“网络邻域”中：

```
C:\WINDOWS>net view \mainserv
```

或者

```
C:\WINDOWS>net view /workgroup:mygroup
```

现在列出共享的目录：

```
C:\WINDOWS>dir \mainserv\test
```

如果完全无法访问，那情况就完全不同了。

# WINS 服务器

WINS 代表 Windows Internet Naming Service（Windows 命名服务）。它是一种不依赖广播的 NetBIOS 名称解析服务。Samba 服务器依赖访问 WINS 服务器来完成工作。WINS 在第 34 章中有详细介绍。

当设置正确时，WINS 通过减少广播使网络更高效。然而，如果使用不当，可能会导致问题。首先，每个子网必须有一个 WINS 服务器。其次，一切必须设置正确；否则 WINS 实际上可能会增加网络流量。

`BROWSING.txt` 文件详细描述了 WINS 服务器。

## DHCP

DHCP 代表动态主机配置协议。它是配置连接到 Samba 服务器的任何主机的极工具，减少了客户端/服务器 Samba 不兼容的概率。阅读 Samba 文档中的 `DHCP-Server-configuration.txt` 作为 `dhcp` 和 `dhcp-options` 页面。以下是 Samba 兼容性最重要的选项：

- option broadcast-address 192.168.100.255;
- option netbios-name-servers 192.168.100.1;
- option netbios-dd-server 192.168.100.1;
- option netbios-node-type 8;

> 注意
`option netbios-node-type` 指客户端的 NetBIOS 节点类型。值 1 对应于 NetBIOS B-节点，仅通过广播解析名称。2 对应于 P-节点，仅使用单播。4 对应于 M-节点，首先尝试广播，在广播失败后尝试单播。8 将客户端配置为 H-节点，其中先尝试单播，在单播失败后后尝试广播。

这是一个基本的 Samba 配置选项。

# Samba 客户端编程

许多 Windows 程序从 Samba 服务器访问数据。有时 DOS 程序必须访问 Samba 服务器上的数据，因此需要预先存在的驱动器。

## 列表 9.2 netuse.pl 程序映射并使用驱动器号，然后删除它

```
use strict;

my($driveletter) = '';

sub mapdrive

{

    if ($0 eq '') {

        my($output) = 'net use \mainserv\test';

        print "\nmapdrive:\n$output;

        $output =~ m/(.+): connected to/;

        my($driveletter) = $1;

    }

}

sub deldrive

{

    my($driveletter) = $_[0];

    my($delcmd) = 'net use $driveletter: /delete';

    print "\ndeldrivemap($driveletter):\n" . $delcmd;

}

sub usedrive

{

    my($dir) = $_[0] . ":";

    opendir(SHARE, $dir);

    my($files) = readdir(SHARE);

    closedir(SHARE);

    print "\nusedrive($dir)\n$files\n";

}

&mapdrive();

&usedrive();

&deldrive();
```

# 从 Windows 触发服务器进程

之前的程序没有错误检查或处理异常状态的代码。一种异常发生在共享自上次 Windows 重启后从打印机变为目录共享。另一种涉及所有驱动器号都被占用的罕见情况。当然，另一种异常状态是共享无法访问。生产环境程序会测试这些及其他情况。

此示例程序使用 Perl 编写，是因为 Perl 被广泛使用、功能强大以及通过反引号运算符捕获输出的能力。

这种编程可以用任何语言完成。例如，在 DOS C 中，Perl 的反引号运算符可以通过系统调用模拟，如下存根 C 程序所示：

```c
#include<stdio.h>
#include<process.h>
void main(void) {
    system("net use * \\mainserv\\test > test.txt");
}
```

程序可以读取并解析 file.txt 来定义驱动器号。

## 网络化开始菜单图标组

通常情况下，许多用户需要一系列特定的图标。在很多时候，使用漫游配置或其他“标准化桌面”是不切实际的。Samba 提供了一个极佳的解决方案——网络化开始菜单图标组。

假设手机计费系统需要几个图标，并且希望通过用户名对这些图标进行集中化管理。你可以创建如下共享：

```
[icongrps]
path=/home/username/icongrps
read only=yes
write list-username
```

自然，`icongrps` 目录必须对所有用户具有读取和执行权限，且其上级目录必须具有执行权限以便于导航。

接下来，以 `username` 身份登录 Windows，并创建手机计费图标组目录（因为该用户在 `write list` 参数列表中）。在 Windows 资源管理器中导航到 `icongrps` 共享，并创建一个名为 `phonechrg` 的目录。

现在，将 `phonechrg` 目录拖到 Windows 开始按钮上。这会在开始菜单顶层放置一个指向 `phonechrg` 目录的快捷方式。任何在开始菜单中放置目录快捷方式的方法都能正常工作。观察点击开始菜单上的此快捷方式是如何打开目录的。

现在放置图标。假设手机计费系统的三个 Windows 端程序为 `acc.exe`、`validate.exe` 和 `input.exe`。在上一段中打开的 `phonechrg` 目录中为这三个程序创建快捷方式。最简单的方法是选中这三个可执行文件，将它们复制到剪贴板，然后在 `phonechrg` 目录中右键并选择“粘贴快捷方式”。可以通过右键点击图标并在弹出菜单中选择“属性”来更改快捷方式的名称和图标。

由于此共享对 `username` 外的任何人都是只读，其他用户无法意外删除图标。用户从开始菜单选择手机计费快捷方式打开快捷方式目录，该目录是持久存在的。然后点击该目录中的图标来运行程序。

## Windows 98 Samba 客户端故障排除

前两步是使用 ping 检查连通性，并确定问题是否适用于所有 Windows 9x 客户端。在排查 Samba 问题之前，你必须解决所有连接问题。

如果问题适用于所有 Windows 9x Samba 客户端，则根源在 Samba 服务器上，必须在服务器上借助 `smclient` 程序进行故障排除。如果问题仅出现在一个客户端上，你可以利用该客户端与正常客户端之间的差异。

如果问题发生在一组 Windows 客户端上，请总结无法工作客户端的共同点，并利用这两组之间的差异。

可浏览问题可能会让人抓狂。第一步是确保共享在 `smclient` 中被意图为可浏览的；然后通过 `smclient -NLname` 确认服务器上的浏览性。一旦确认服务器上可浏览，请在 Windows 上尝试使用 `view \servername` 和 `net view /workgroup:workgroup` 命令。如果这些命令显示了共享但 Windows 资源管理器没有显示，可能可能是浏览器选举问题（browser election），可以按照本章描述的方法修复。然而，如果共享在这些命令中的一个或两个中未显示（但客户端或服务器显示了，即在 `smclient -NL servername` 中显示），则说明存在严重的协议问题，此时与其他客户端进行对比至关重要。

对于协议问题，检查 `smclient -NL client` 是否返回结果。如果没有，则存在基础协议问题的证据。许多此类问题发生在尝试在用户级别共享客户端资源时。Windows 9x 在这方面并不理想，需要网络上有一个合法的 PDC（主域控制器）。查看在“网络控制”对话框中更改共享级访问控制后问题是否消失。然后相应地进行故障排除。

## 总结

Samba 主要用途是为 Windows 98 客户端提供文件。这要求 Windows 客户端配置正确。这可以通过网络对话框和 TCP/IP 属性对话框手动完成，也可以通过 DHCP 动态完成。

## 创建即用 Samba 系统

第二部分

在 Windows 98 中，浏览通常是一个挑战，特别是在 Windows 资源管理器中。访问（映射驱动器等）是完全独立的属性。浏览性通过 `browseable` 共享参数 `-NL server` 命令进行验证。在 Windows 客户端上，通过 `net` 命令进行验证。如果某些内容在 `view` 中可见但在 Windows 资源管理器中不可，可能是主节点问题（master-blem）。以下行会在 Samba 重启后启动选举，并使 Samba 服务器倾向于赢得选举：

```
os level=65
local master=yes
preferred master=yes
wins support=yes
```

浏览器选举大约需要 30 秒。可以使用以下命令进行观察：

```
$ tail -n0 -f log.nmb
```

上述命令必须在包含 `log.nmb` 的目录下运行——通常是 `/var/log/samba` 或 `/usr/local/samba/var/`。有时浏览器选举可以从 Windows 9x 客户端通过以下命令触发：

```
C:\WINDOWS>net view /workgroup:workgroupname
```

每个子网应仅只有一个首选服务器和一个 WINS 服务器。

Samba 共享通常通过两个 `net view` 命令之一进行浏览：

```
C:\WINDOWS>net view \\servername
```

或者

```
C:\WINDOWS>net view /workgroup:workgroupname
```

实际访问通过直接向共享或从共享复制，或在原地修改来完成：

```
C:\WINDOWS>notepad \\servername\sharename\filename.ext
```

某些程序（尤其是旧的 16 位程序）无法通过这种方式访问文件。在这种情况下，映射如下：

```
C:\WINDOWS>net use \\servername\sharename
```

或者，映射如下：

```
C:\WINDOWS>net use \\servername\sharename
```
