
COM 依赖于某部分闭源 Windows API (`Win32`) 的可用。VB 绑定到 COM，因此 VB 方言在 Windows 之外的用性小得多，特别是在 Linux 中。Visual Basic 家族面向 `Win32` COM，并不是用于 Linux/Windows 可移植性或互操作性的语言。它之所以包含在本书中，是因为 VB 的 Windows 开发人员比任何其他语言都多。

# JavaScript

JavaScript 也称为 ECMA Script 或 Jscript（取决于实现），它像 Java 一样类似于 C 语言。JavaScript 不是 Java 的轻量级版本，但两种语言都使用了大量的 C 语言语法。

JavaScript（微软对 JavaScript 的命名）是 Windows XP 默认安装的三脚本语言之一。

JavaScript 是一种无处不在的语言，用于 Web 客户端和服务端脚本，IE 和 Netscape 浏览器都支持 JavaScript 来操作各自的 DOM。JavaScript 也用于 ASP 中的服务端脚本，但 VBScript 在那里拥有同样的关注者。JavaScript 和 VBScript 是 Windows XP 和 Windows 2000 捆的 WSH 语言。

JavaScript 的对象模型是底层文档对象模型，或者对于命令行，是 Windows 的 `Wscript` 模型。JavaScript 经常结合 DOM 用于 Web 页面，如下。

```javascript
<script>
<!-- Hide old browsers
function startTime() {
  var now = new Date();
  var hours = now.getHours();
  var minutes = now.getMinutes();
  var seconds = now.getSeconds();
  var day = now.getDate();
  var month = now.getMonth() + 1;
  var year = now.getFullYear();
  var dateTime = "" + month + "/" + day + "/" + year;
  var timeValue = "" + (hours > 12) ? "0" : hours + ":" + minutes;
  timeValue += (minutes < 10) ? "0" : minutes + ":" + seconds;
  timeValue += (hours >= 12) ? " P.M." : " A.M.";
  document.clock.face.value = dateTime + ", " + timeValue;
  document.clock.weeks.value = cndownWeeks();
  document.clock.days.value = cndownDays();
  document.clock.hrs.value = cndownHours();
  document.clock.mins.value = cndownMins();
  document.clock.secs.value = cndownSecs();
  var timerID = setTimeout("showTime()", 1000);
  timerRunning = true;
}
<!-- Hide old from browsers
</script>
```

> 图 4-20 是结果，所有其他实时输出字段都通过类似代码实现。该应用程序是一个高中同学聚会的在线手册。

# 可移植性

如果创建一个源代码实例，使其在 Windows 和 Linux 上都无需更改即可运行，我们就宣布该语言在 Windows 和 Linux 之间是可移植的。尽管如此，脚本应用程序最终可能因为语言之外的其他支持而变得不可移植。

![](img/9e81145387d1e3c67216814bd87285fe_110_0.png)

图 4-20 JavaScript 中的实时更新。可移植性什么时候重要？一个位于公共文件共享上的脚本，宣传供任何桌面机（无论 Linux 还是 Windows）上的任何人使用情况如何？例如，它可以是一个在给出姓氏前几个字母时查找员工电话的脚本。因此，我们只需要支持这一个文件，该功能在 ElSolutions 的所有类型桌面机上可用。请参见第 15 节“目录集成”，查看访问轻量级目录访问协议 (`LDAP`) 员工目录的脚本示例。

Java 是本章提到的唯一增加二进制可移植性的语言。这意味着 Java 编译器的输出可以在 Windows 或 Linux 上执行而无需重新编译。大多数脚本语言可以用于定义可移植的程序，因为脚本语言的属性允许我们在概念上执行源代码。我们只需要在每个端点上有一个接受该源代码的实现。

记住，利用特定平台功能的程序在任何实现语言中都是不可移植的。考虑到这一点，这里是我们在表 4-4 中的可移植脚本语言列表。

### 表 4-4 Windows XP 和 Linux 中的可移植脚本语言

| 语言 | Windows XP | Red Hat Linux 7.1 |
| :--- | :--- | :--- |
| VBScript | Std (WSH, Internet Information Services) | Free |
| Java | Std | Std |
| Perl | Add-on | Std |
| JavaScript | Std | Std |
| Shell | Std | Std |
| Awk | Std | Std |
| Tcl/Tk | Std | Std |
| Python | Std | Std |
| REXX | Free | Free |

*(注：上面的表格是根据碎片化文本重建的。)*

# 第 4 章 脚本

在服务器端，JavaScript、VScript、Perl、PHP 或其他脚本语言可以实现应用的服务器端。这些语言中，可能 VScript 之外，任何一种都可以在运行在 Red Hat Linux 7.1 或 Windows XP 的 Web 服务器上执行。

## 管理

脚本的高效用途是处理重复的、非平凡的企业级或管理任务，这些任务的数量超过了交互式用户可以轻松完成的范围。此类任务必须频繁执行，并可能需要定期重复。例如，一位教授 CS 101 的大学教授可能需要为 150 名计算机专业的学生建立账户并填充文件。她需要在学期末删除这些账户。此外，作为操作的副产物，她还需要一个邮件列表。脚本非常适合这类任务，特别是当任务跨越 Windows XP 和 Red Linux 7.1 平台时。

另一种任务可能涉及在 Windows 或 Linux 的登录配置文件中获取文件和打印共享。登录脚本将调用 Windows 中的代码。这些代码通过 Windows 2000 或 Windows XP 域中的组策略对象按组设置。在 Linux 中，它将来自用户主目录下的配置脚本。

脚本将使用 `net` 命令将共享映射到逻辑设备。共享可能存在于 Windows 或 Linux Samba 上，取决于 Windows 管理员设置的认证类型。Samba 是一个开源软件套件，为 SMB/CIFS 客户端提供文件和打印共享服务。

Linux 登录脚本将使用 Samba `mount` 命令将共享映射到逻辑设备。只要安全设置正确，这些设备就可以跨越 Windows 和 Linux 系统。注意的是，Windows 2000 或 Windows XP 的 Kerberos 认证在 Samba 中不起，因此必须为 Windows XP 或 Windows 2000 机器启用 NT LAN Manager (`NTLM`) 或基本认证。

另一个有趣的场景是在跨平台枚举资源。在 Linux 上，`mount` 命令将列出给定 SMB/CIFS 主机的可用资源。OS/2 Samba 以及其他使用 CIFS（通用文件系统）协议的平台（在 Windows 上以前称为 SMB mount）也将列出网络上可见的工作组和域。在 Windows 2000 或 Windows XP 上，我们可以从 Windows 命令行使用 `net view network` 命令列出网络上的服务器。

以下是从 Linux 发出的环境命令显示的浏览列表。顶部分显示了中间部分名为 MAGET 的服务器上的可用资源。底部分显示了网络上可见的所有工作组和域。只要客户端已通过验证，就可以重新发布 `smclient` 命令以深入其中任何一个工作组。这可以通过使用 Perl 或 Awk 等模式匹配脚本解析输出来递归完成。互操作性的关键在于，`smclient` 是从 Linux 机器上运行的。它的目标是 NT 4 机器，并混合使用了 Linux 和 Windows 域及工作组。

```
trying default locations.
added interface ip=192.168.0.1 bcast=192.168.0.255 nmask=255.255.255.0
Password:
Domain=[BELLMEADE] OS=[Windows 5.0] Server=[Windows 2000 LAN Manager]

| Server | Comment |
| --- | --- |

| Workgroup | Master |
| --- | --- |
```

列表是在 Red Hat 7.1 系统上使用此简单脚本和 Samba `smclient` 程序获得的：

```sh
# /bin/sh
HOST=MAUGET
smbclient -L $HOST
```

操作性的 `smclient` 语句可以参数化并整合到较大的脚本中。等效操作可以在 Windows 上使用 VBScript、JavaScript 或任何带有 COM 的 Perl、Rexx、Tel 或 Python 版本编写的自动化或 WMI 组件完成。示例输出所示：

- 共享: Documents and Settings
- Share: pub
- Share: IPC$
- Share: print$
- Share: ncfarmureau
- Share: download
- Share: vnc
- Share: MySamples
- Share: HP810C
- Share: ADMINS
- Share: C$

用于列出或操作网络共享的 WMI 组件名为 `Win32_Share`。用于编写此对象的 VBScript 为：

```vbscript
Dim Host
Host = "MAUGET1"
Set ComputerSet = \
GetObject("winmgmts:(impersonationLevel=impersonate)!\\" \
& Host).InstancesOf("Win32_Share")
```

```vbscript
WScript.Echo Host & " Shares:"
```

```vbscript
for each Object in ComputerSet
  WScript.Echo "Share: " & Object.Name
next

Set ComputerSet = Nothing
```

可能性仅限于想象力。这些语言具有辅助快速开发、原型设计、管理或一次性操作的能力。

## 管理场景

脚本对于启动需要建立环境的本地进程非常方便。Java 应用通常从脚本启动，因为必须为特定的类路径和初始类启动 Java 虚拟机。这些通常是微不足道的，但如果没有脚本，用户将需要手动输入信息。例如，这里有一个 Windows 批处理文件，它可以创建一个 Java 进程从基于 XML 的导入文件中加载 ZIP 码数据库。

```batch
rem 假设 1: 当前目录下有 zip.xml 文件
rem 假设 2: Mysql 服务正在运行
rem 假设 3: 已安装 Java 1.2+
java -cp import.jar mauget.mysql.test.ImportZipcodes
```

此文件可以轻松转换为 bash 脚本。

# 管理基础 101

```perl
my @host;
my @port;

if (! $entry) {
    print "No entries found.\n";
} else if ($entry) {
    while (@host = $entry->getValues("provider")) {
        @port = $entry->getValues("servicearea");
        $entry = $conn->nextEntry();
    }
}
$conn->close();
```

## 显示值

```perl
print "Host: @host[0]\n";
print "Port: @port[0]\n";
```

以下是管理员用于设置 DBMS 位置的脚本。请注意，这种服务发布和位置方案适用于任何类型的服务。

```perl
#!/usr/bin/perl
#-
# 使用 PerLDAP 设置新主机
#- Louis E. Mauget, 2001年7月8日
#-
use strict;
use Mozilla::LDAP::Conn;

my $host = "pavillion.bellmead.solutions.com";
my $port = 389;
my $bind = "cn=root, o=elsolutions, c=us";
my $pswd = "secret";
my $cert = "";

my $conn = new Mozilla::LDAP::Conn($host, $port, $bind, $pswd, $cert);
die "Couldn't connect to LDAP server $host:$port" unless $conn;
```

## 对 objectClass=* 进行搜索

```perl
my $base = "service=dbms, cn=root, o=Web-Farm, c=us";
my $srchbase = "subtree"; # 一个基础；subtree 或无
my @attr = ("provider","serviceArea");
my $filter = "(objectClass=service)";
my $entry = $conn->search($base, $srchbase, $filter, 0, @attr);
```
