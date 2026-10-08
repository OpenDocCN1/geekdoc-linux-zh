

示例中列出的许多服务并非 Windows 的原生服务。例如，MeasureWare（HP 性能工具）和 Oracle 服务。这些服务可以分别使用 NET START 和 NET STOP 命令进行启动和停止。

## NET STATISTICS

**NET STATISTICS** - 使用此命令来显示服务的统计日志。不带选项发出 NET STATISTICS 命令可显示所有服务的统计信息。

以下是 **NET STATISTICS** 命令的摘要：

```
C:\ NET STATISTICS /?
NET STATISTICS [WORKSTATION | SERVER]
```

一些常用选项如下：

- SERVER：显示服务器服务统计信息。
- WORKSTATION：显示工作站服务统计信息。

以下示例展示了不带选项发出 **NET STATISTICS** 命令的情况：

```
C:\ NET STATISTICS
Server Statistics for \NISDEV

Statistics since 1/21/98 8:49 AM

Sessions accepted                    3
Sessions timed-out                   32
Sessions errored-out                 32

Kilobytes sent                       165941
Kilobytes received                   33118

Mean response time (msec)            0

System errors                        0
Permission violations                2
Password violations                  0

Files accessed                       12787
Communication devices accessed       0

Print jobs spooled                   0

Times buffers exhausted              0

Big buffers                          0

Request buffers                      0

The command completed successfully.
```

## NET STOP

**NET STOP** - 此命令用于停止使用 NET START 命令启动的服务。

以下是 **NET STOP** 命令的摘要。

```
C:\ NET STOP /?
NET STOP service
```

**NET STOP** 命令的一个选项是：

| 选项 | 描述 |
| :--- | :--- |
| service | 可以停止的服务的名称。 |

## NET TIME

**NET TIME** - 此命令用于显示计算机的时间，或将计算机的时钟与另一台计算机的时钟进行同步。

以下是 **NET TIME** 命令的摘要。

```
C:\ NET TIME /?
NET TIME (\\computername | /DOMAIN[:domainname]) [/SET]
```

一些常用选项如下：

- \\computername：您想要同步时间的计算机，或您想要显示其时间的计算机。
- /DOMAIN[:domainname]：您想要同步时间的域名。
- /SET：使用指定计算机或域上的时间来设置计算机的时间。

## NET USE

**NET USE** - 列出计算机的连接，或建立或移除共享资源。如果不带选项，此命令将列出计算机的连接。

以下是 **NET USE** 命令的摘要。

```
C:\ NET USE /?
NET USE [devicename | *] [//computername\\sharename([volume]) [password | *]]
[\\USER:[domainname\\username]
[[DELETE] | [/PERSISTENT:{YES | NO}]]
NET USE [devicename | *] [password | *] [/HOME]
NET USE [PERSISTENT:{YES | NO}]
```

一些常用选项如下：

- devicename：指定要连接或断开的名称。可能的名称包括驱动器、打印机等。
- \\computername：这是控制共享资源的计算机的名称。
- /sharename：共享设备的网络名称。
- password：访问共享资源所需的密码。
- *: 为试图使用该共享资源的用户产生密码提示。
- /USER：为连接指定不同的用户名。
- domainname：使用与当前域不同的域。
- username：指定用户登录名称。
- /HOME：将用户连接到其主目录。
- /DELETE：取消网络连接并将其从持久连接列表中移除。
- /PERSISTENT {yes | no}：指定 yes 表示连接将在下次登录时重新建立。指定 no 则不为未来的登录保存该连接。

以下示例展示了不带选项发出 NET USE 命令的情况：

```
C:\ NET USE
New connections will be remembered.

Status  Local  Remote             Network
-----  -----  -----------------  ----------------
   OK   P:\    \\DEVSYS\Disk_C    Microsoft Windows Network

The command completed successfully.
```

远程系统 DEVSY S 上的目录 Disk_C 在本地系统下以 P: 形式显示。

## NET USER

**NET USER** - 此命令用于创建和修改计算机上的账户。也可以不带选项使用该命令来列出账户。

以下是 **NET USER** 命令的摘要。

```
C:\ NET USER /?
NET USER [username [password | *]] [options] [/DOMAIN]
username [password | *] /ADD [options] [/DOMAIN]
username [/DELETE] [/DOMAIN]
```

一些常用选项如下：

- /ADD：添加用户账户。
- /DELETE：删除用户账户。
- username：要操作的账户名称。您可以添加、删除、修改或查看该账户。
- password：分配或更改用户账户的密码。
- *: 显示密码提示。
- /DOMAIN：操作将在主要域控制器上执行。

还有许多其他选项，例如账户的过期日期、用户登录配置文件的路径等。

以下示例展示了不带选项发出 **NET USER** 命令的情况：

```
C:\ NET USER

User accounts for \\NIS2DEV

Administrator    arleo_j        burgos_c
Guest            IUSR_NIS2DEV   IUSR_NISDEV
johnt            leung_k        marty
mckenna_b

The command completed successfully.
```

使用前面所示命令的第二种形式，我们可以向系统添加一个新用户：

```
C:\ NET USER amyp /ADD

Type a password for the user:
Retype the password to confirm:

The request will be processed at the primary domain controller for domain DEV.

The command completed successfully.
```

**NET USER** 命令中的星号表示我们想要为新建用户 *amyp* 提示输入密码。

## NET VIEW

**NET VIEW** - 此命令列出计算机上正在共享的资源。您可以不带选项使用此命令来显示域中计算机的列表。

以下是 **NET VIEW** 命令的摘要。

```
C:\ NET VIEW /?
NET VIEW [\\computername | /DOMAIN[:domainname]]
NET VIEW /NETWORK:NW [\\computername]
```

一些常用选项如下：

- \\computername：指定要查看共享资源的计算机的名称。
- /DOMAIN:domainname：指定要查看共享资源的域名。
- /NETWORK:NW：显示网络中的 NetWare 服务器。

以下示例展示了不带选项发出 **NET VIEW** 命令的情况，这会产生当前域中计算机的列表：

```
C:\ NET VIEW

Server Name                Remark
-------------------------- ----------
\\NIS2DEV
\\NISDEV

The command completed successfully.
```

以下示例展示了在指定要查看的 *DOMAIN* 时发出 **NET VIEW** 命令的情况：

```
C:\ NET VIEW /DOMAIN:nisdomain

Server Name                Remark
-------------------------- ----------
\\HPSYSTEM1
\\KITTY
\\NIS

The command completed successfully.
```

以下示例展示了在指定当前域中特定计算机名称进行查看时发出 NET VIEW 命令的情况：

```
C:\ NET VIEW \\hpssystem1

Shared resources at \\hpssystem1

Share name    Type    Used as    Comment
------------  ------  ---------  -------------------------
HPLaserJ5     Print   HP LaserJet 5MP
measure        Disk
net_share      Disk
NETLOGON       Disk   Logon server share

The command completed successfully.
```

## POSIX 实用程序

Microsoft Windows NT Server 资源工具箱（在本章中称为资源工具箱）中包含几个 POSIX 实用程序，UNIX 系统管理员在使用 Windows 时觉得这些工具很有用。资源工具箱通常是一个出色的系统管理资源。虽然本书将仅关注 POSIX 实用程序，但资源工具箱中包含了大量信息。资源工具箱是

