
这这些术语已经足够你开始了。

（注：此处后续部分原文存在重复或逻辑混乱，根据指令已已翻译，逻辑逻辑的翻译内容）

## 软件

Net-SNMP 是一个非常出色的免费软件包，包含了你在在本章中跟随的所有内容。Net-SNMP 将为你提供命令（`snmpget`、`smpset`、`snmpwalk`、`snmtrap`）、一个 SNMP 代理以及标准的 MIB 文件。通常情况下，命令和代理运行在不同的系统上，但为了简单起见，你将在同一个系统上运行。如果你有两个可用系统，你可以在两个系统上都进行完整安装；然后你可以在一个系统上运行 `snmpget`（例如），并与另一个系统上的代理通信。如果你使用两个系统，请记住将本章代码中所有的 `localhost` 或 `127.0.0.1` 更改为运行 SNMP 代理系统的名称或地址。

## 安装 SNMP

在安装之前，请检查你的系统是否已经安装了 Net-SNMP——许多常见的 Linux 发行版都提供了它的某个版本。如果你使用的是非常旧的 Linux 发行版（如 Red Hat 7.x），你可能会找到 UCD-SNMP；这是一个较旧的版本——是 Net-SNMP 的父级。尽管它的行为与 Net-SNMP 非常相似，但它们之间的差异足以让任何试图遵循本教程的人感到困惑；你应该删除它，并按照说明安装 Net-SNMP。如果你发现安装了另一个软件包，请务必在继续之前将其删除。

> ¹ 互联网工程任务组（IETF）始于 1986 年，是互联网的主要组织。参与是自愿的并对所有人开放。它的大部分工作在工作组（WGs）中形成，这些是由对特定主题感兴趣的相关组成的临时小组。

如果你的系统尚未安装 Net-SNMP，它可能包含在你的 Linux 发行版中，所以请检查你的 CD。但请注意，不同的 Linux 发行版可能修改了 Net-SNMP 以符合它们对默认文件位置的理念，并且可能包含不同的补丁。自然，请将你的 Net-SNMP 版本视为本章中使用的版本（版本 5.2.1），与这里显示的版本越接近越好。

## 下载与安装

如果你的 Linux 发行版未包含 Net-SNMP，你可以从 `http://net-snmp.sourceforge.net` 下载。你可以选择从 RPM 安装（假设你正在运行基于 RPM 的发行版，如 Fedora）或从源码安装，但现在让我们先安装二进制 RPM。顺便说一下，如果 rpm 抱怨缺少依赖项，你可能需要先处理它们然后再重试命令。

```
$ -Uvh net-snmp-5.2.1.fc4.1686.rpm

Preparing... ########################### [100%]

1:net-snmp ################# [100%]
```

## 检查安装情况

现在测试它是否工作正常。首先测试代理。

```
$ /usr/bin/snmpd --version
```

NET-SNMP version: 5.2.1
Web: http://www.net-snmp.org/
net-snmp-coders@lists.sourceforge.net

$ 

现在检查工具。使用 `which` 找到它们安装的位置，然后用 `ls` 列出该目录下所有以 `snmp` 开头的命令。

```
$ which snmpwalk

/usr/bin/snmpwalk

$ ls /usr/bin/snmp*
/usr/bin/snmpd /usr/bin/snmpstatus
/usr/bin/snmpus /usr/bin/snmpwalk /usr/bin/snmpget
/usr/bin/snmptable /usr/bin/snmpvacm /usr/bin/snmpcheck
/usr/bin/snmpgetnext /usr/bin/snmptest /usr/bin/snmpwalk
/usr/bin/snmpconf /usr/bin/snmpnetstat /usr/bin/snptranslate
/usr/bin/snmpdelta /usr/bin/snmpset /usr/bin/snptrap
```

（注：由于提供的原文后半部分存在大量内容重复和乱码，根据“一定不要重复输出原文”的原则，此处仅保留核心逻辑翻译）

这些这些术语已经足够你入门了。

```
$snmptranslate -0f .1.3.6.1.2.1.1.1
iso.org.internet.mgmt.mib-2.system.sysDescr $
```

如果你可以访问任何其他网络设备，你可以尝试查询它们。例如，这里有一个针对 Apple AirPort 基站（Base Station）运行的 `snmpwalk` 命令：

```
$ snmpwalk -c public 10.0.0.1
snmpV2-MIB::sysDesc.0 = STRING: Apple Base Station V3.84 Compatible
snmpV2-MIB::ObjectID.0 = OID: SNMPv2-dotZero
DISMAN-EVENT-MIB::sysTimeInstance = timeticks:(4971188) 24:31:88
snmpV2-MIB::sysContact.0 = STRING: me@myaddr.com
snmpV2-MIB::sysName.0 = STRING: MyAirport
snmpV2-MIB::sysServices.0 = INTEGER: 79
snmpV2-MIB::sysServices.0 = No more variables left in the MIB View (It is past the end of the MIB tree)
```

显然，设备的 `sysDesc.0`（系统描述）识别出这是一台 Apple 基站。你还能识别该设备的 `syslocation`（物理位置）和 `sysContact`（联系方式）信息。该设备没有提供大量信息，但足以识别它是什么、它在哪里，以及当你发现这台设备出现任何问题时该如何联系（尽管你可能会发现它运行异常）。系统联系方式和位置的可用性取决于该系统的管理员，由他在目标设备上配置这些值。一个疏忽的系统管理员可能会让你独自苦战。

注意，对于这次查询，我们使用了 `snmpwalk` 而不是 `snmpget`，因为我们想查看此设备可能提供的哪些其他信息。`snmpget` 命令使用 SNMP GET 数据单元检索单个对象实例，而 `snmpwalk` 使用多个 SNMP GETNEXT 来“遍历”整个 MIB。你选择一个起点，`snmpwalk` 会请求词法顺序上的下一个实例；代理程序（agent）返回该对象及其 OID，然后 `snmpwalk` 请求新 OID 之后的下一个对象实例。最终，代理程序响应没有更多可返回的内容，遍历终止。

## 用于可读名称的 MIB

为 OID 显示友好且可读的名称（如 `sysDesc` 和 `sysLocation`）取决于在你的客户端系统上注册了正确的 MIB 文件。在 Net-SNMP 的情况下，注册意味着将这些文件放在正确的目录下，然后让 SNMP 命令（如 `snmpget` 和 `snmpwalk`）使用它们。你可以设置几个环境变量来为你完成这项工作。只需将这些行放入你的 shell 启动文件（例如 `.bashrc`）中：

```
export MIB-ALL
export MIBDIRS=/usr/share/snmp/mibs
```

当你安装 Net-SNMP 时，它在 `/usr/share/snmp/mibs` 中放置了一组标准 MIB 文件，如下列表所示。这些都是使用人类可读且机器可解析语法编写的文本文件。

其中一些实际上描述了 MIB。另一些是支持文件，用于定义描述 MIB 的文件所需的信息，就像 C 语言中头文件一样。

```
$ /usr/share/snmp/mibs
AGENT-MIB.txt             RFC1155-SMI.txt
DISMAN-EVENT-MIB.txt      RFC1213-MIB.txt
DISMAN-SCHEDULE-MIB.txt   RFC-1215.txt
DISMAN-SCRIPT-MIB.txt      RMON-MIB.txt
EtherLike-MIB.txt         SNMP-MIB.txt
HCNUM-TC.txt               SNMP-COMMUNITY-MIB.txt
HOST-RESOURCES-MIB.txt    SNMP-FRAMEWORK-MIB.txt
HOST-RESOURCES-TYPES.txt  SNMP-MPD-MIB.txt
IANA-ADDRESS-NUMBERS-MIB.txt SNMP-NOTIFICATION-MIB.txt
IANAftype-MIB.txt         SNMP-PROXY-MIB.txt
IANA-LANGUAGE-MIB.txt      SNMP-TARGET-MIB.txt
```
