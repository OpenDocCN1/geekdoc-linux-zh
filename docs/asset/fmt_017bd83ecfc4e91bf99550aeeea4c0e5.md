
> ⁴⁶² (Microsoft, 2019), https://docs.microsoft.com/en-us/windows-server/networking/technologies/netsh/netsh-contexts

![](img/ec25e59d75726b7041242a56d3376832_516_0.png)

规则名称：`@{Microsoft.Windows.Photos.2018.18022.15810.1000_x86___8wekyb3d8bbw`

已启用：是
方向：出站
配置文件：域、专用、公用
分组：Microsoft Photos
本地 IP：任意
远程 IP：任意
协议：任意
边缘遍历：否
操作：允许

规则名称：`@{Microsoft.XboxIdentityProvider_12.39.13003.1000_x86___8wekyb3d8bb`

...

---

### 列表 531 - 列出 Windows 上的所有防火墙规则

根据上述列出的两条防火墙规则，Microsoft Photos 应用程序被允许使用任意协议与任意 IP 地址建立入站和出站连接。请注意，并非所有防火墙规则都有用，但某些配置可能有助于我们扩大攻击面。

在基于 Linux 的系统上，我们需要 root 特权才能使用 `iptables` 列出防火墙规则。^463 然而，根据防火墙的配置方式，我们可能能够以标准用户身份获取有关规则的信息。

例如，在 Debian Linux 上，`iptables-persistent`^464 包默认将防火墙规则保存在 `/etc/iptables` 目录下的特定文件中。系统使用这些文件在启动时恢复 `netfilter`^465 规则。这些文件通常权限较弱，允许目标系统上的任何本地用户读取。

我们还可以搜索由 `iptables-save` 命令创建的文件，该命令用于将防火墙配置转储到用户指定的文件中。然后，该文件通常用作 `iptables-restore` 命令的输入，用于在启动时恢复防火墙规则。如果系统管理员曾经运行过此命令，我们可以搜索配置目录（`/etc`）或对文件系统进行 grep 搜索 `iptables` 命令以定位该文件。如果文件具有不安全的权限，我们可以使用其内容推断系统正在运行的防火墙配置规则。

463 (Herve Eychenne, 2003), https://linux.die.net/man/8/iptables
464 (Debian, 2019), https://packages.debian.org/search?keywords=iptables-persistent
465 (Netfilter, 2014), https://www.netfilter.org/

### 18.1.1.7 枚举计划任务

攻击者通常在权限提升攻击中利用计划任务。

充当服务器的系统通常会定期执行各种自动化的计划任务。这些服务器上的调度系统通常具有某种令人困惑的语法，用于执行用户创建的可执行文件或脚本。当这些系统配置错误，或者用户创建的文件被遗留了不安全的权限时，我们可以修改这些将由调度系统以高权限级别执行的文件。

我们可以使用 `schtasks` ^466 命令在 Windows 上创建和查看计划任务。`/query` 参数显示任务，而 `/FO LIST` 将输出格式设置为简单的列表。我们还可以使用 `/V` 请求详细输出。

```
c:\Users\student>schtasks /query /fo LIST /v

Folder: \

INFO: There are no scheduled tasks presently available at your access level.

Folder: \Microsoft

INFO: There are no scheduled tasks presently available at your access level.

Folder: \Microsoft\Office

HostName:          CLIENT251

TaskName:         \Microsoft\Office\Office 15 Subscription Heartbeat

Next Run Time:    11/12/2019 3:18:24 AM

Status:           Ready

Logon Mode:       Interactive/Background

Last Run Time:    11/11/2019 3:49:25 AM

Last Result:      0

Author:           Microsoft Office

Task To Run:      %ProgramFiles%\Common Files\Microsoft Shared\Office16\OLicenseHeartbeat.exe

Start In:         N/A

Comment:          Task used to ensure that the Microsoft Office Subscription licensing is current.

Scheduled Task State: Enabled

Idle Time:        Disabled

Power Management: Stop On Battery Mode

Run As User:      SYSTEM

Delete Task If Not Rescheduled: Disabled

Stop Task If Runs X Hours and X Mins: 04:00:00

Schedule:          Scheduling data is not available in this format

Schedule Type:    Daily

Start Time:       12:00:00 AM

Start Date:       1/1/2010

End Date:         N/A

Days:             Every 1 day(s)

Months:           N/A

Repeat: Every:    Disabled

Repeat: Until: Time: Disabled

Repeat: Until: Duration: | Disabled

Repeat: Stop If Still Running: | Disabled
```

^466 (Microsoft, 2018), https://docs.microsoft.com/en-us/windows/win32/taskschd/schtasks

#### 列表 532 - 列出 Windows 上的所有计划任务

由 `schtasks` 生成的输出包含大量有用的信息，例如要运行的任务、下次运行的时间、上次运行的时间以及关于其运行频率的详细信息。

基于 Linux 的作业调度器被称为 `Cron`。^467 计划任务列在 `/etc/cron.*` 目录下，其中 `*` 代表任务运行的频率。例如，每天运行的任务可以在 `/etc/cron.daily` 中找到。每个脚本都列在其自己的子目录中。

```
student@debian:~$ ls -lah /etc/cron*

-rw-r--r--  1 root root 722 Oct  7 2017 /etc/crontab

/etc/cron.d:

-rw-r--r--  1 root root  285 May 29 2017 anacron

-rw-r--r--  1 root root  712 Jan  1 2017 php

-rw-r--r--  1 root root  102 Oct  7 2017 .placeholder

/etc/cron.daily:

-rwxr-xr-x  1 root root  311 May 29 2017 @anacron

-rwxr-xr-x  1 root root  539 Mar 30 2018 apache2

-rwxr-xr-x  1 root root  1.5K Sep 13 2017 apt-compat

-rwxr-xr-x  1 root root  355 Oct  25 2016 bsmandintults

-rwxr-xr-x  1 root root  384 Dec 12 2012 cracklib-runtime

-rwxr-xr-x  1 root root  1.6K Feb 22 2017 dpkg

-rwxr-xr-x  1 root root   89 May  5 2015 logrotate

-rwxr-xr-x  1 root root  1.1K Dec 13 2016 man-db

-rwxr-xr-x  1 root root  249 May 17 2017 passwd

-rw-r--r--  1 root root  102 Oct  7 2017 .placeholder
```
