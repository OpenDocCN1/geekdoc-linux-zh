
- **物理标识符** — 记录系统的序列号、制造商、型号以及任何其他唯一标识系统并为收集的信息提供背景的系统物理属性。

- **主机名** — 使用`hostname`命令记录系统名称。拥有目标系统的主机名对于区分与本地或远程系统相关的数据很有用，例如日志和配置文件中的条目（图 1.19）。

```bash
# /media/cdrom/Linux-IR/hostname
victim13.<domain>.com
```

**图 1.19** — 使用`hostname`命令。

- **用户名** — 除了识别目标系统的主机名外，还使用`whoami`、`logname`和`id`命令确定系统中的当前有效用户（图 1.20 和 1.21）。

```bash
# /media/cdrom/Linux-IR/whoami
bentley
```

**图 1.20** — 使用`whoami`命令。

```bash
# /media/cdrom/Linux-IR/logname
bentley
```

**图 1.21** — 使用`logname`命令。

- `id`命令提供有关当前用户的其他详细信息，包括`uid`、`gid`以及用户所属的组，如图 1.22 所示。

```bash
# /media/cdrom/Linux-IR/id
uid=1000(bentley) gid=1000(bentley) group=1000(bentley),4(adm),20(dialout),24(cdrom),46(plugdev),111(lpadmin),119(admin),122(sambashare)
```

**图 1.22** — 使用`id`命令收集当前用户的用户和组信息。

### 网络配置

在记录目标系统配置时，要留意异常项目。

- 查找配置了虚拟专用网络（VPN）适配器但不合法使用 VPN 的系统。
- 确定目标系统的网卡是否处于`混杂模式`，这通常表示正在运行嗅探器。
- 使用`ifconfig`记录目标系统网卡的 IP 地址和硬件地址，这提供了用于分析日志和配置文件的调查背景，如图 1.23 所示。

![](img/a8917580079d3ca10155fb6d19f8d4a3_44_0.png)

**图 1.23** — 使用`ifconfig`记录目标系统的网络配置。

- 上述`ifconfig`输出中存在的“PROMISC”表明网卡已被嗅探器置于混杂模式。
- 如果正在运行嗅探器，请使用`lsof`命令定位嗅探器日志，并如本书后续章节所述，检查日志中是否有其他被入侵账户和计算机的迹象。

### 系统正常运行时间

- 使用`uptime`命令确定目标系统已运行了多长时间，即系统正常运行时间。
- 建立系统运行时长有助于数字调查人员了解系统最近一次重启的时间。
- `uptime`命令还显示系统在开机期间繁忙程度。当检查系统上的活动时，包括正在运行的进程，此信息可能很有用。
- 知道目标系统在安装恶意软件后没有重启可能很重要，这将促使数字调查人员更仔细地查找内存中可能被销毁的已删除进程和其他信息。
- 要确定系统正常运行时间，请从你受信任的工具包中调用`uptime`实用工具，如图 1.24 所示。

![](img/a8917580079d3ca10155fb6d19f8d4a3_44_1.png)

**图 1.24** — 使用`uptime`命令查询系统。

## 系统环境

- 在对 Linux 系统进行调查时，记录目标系统的一般详细信息（包括操作系统版本、内核版本、主目录和桌面环境）是很有用的。
- 系统环境信息可能显示系统已过时，因此容易受到某些攻击的影响。
- 可以使用`uname -a`命令获取一组简洁的系统环境描述符（`-a`标志表示“所有信息”），该命令显示以下内容：
  - 内核名称
  - 网络节点主机名
  - 内核发行版
  - 内核版本
  - 机器硬件名称
  - 处理器类型
  - 硬件平台
  - 操作系统（图 1.25）
- 通过使用`printenv`和`env`命令（图 1.26），可以获得目标系统环境和状态的详细快照，其中包含上述部分详细信息。

```text
# /media/cdrom/Linux-1R/uname -a
Linux ubuntu 2.6.35-22-generic #33-Ubuntu SMP Sun Sep 19 20:34:50 UTC 2010 i686 GNU/Linux
```

**图 1.25** — 使用`uname -a`命令收集系统环境信息。

```text
# /media/cdrom/Linux-1R/printenv
[excluded for brevity]
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games
PWD=/home/bentley
GDM_KEYBOARD_LAYOUT=us
LANG=en_US.UTF-8
GNOME_KEYRING_PID=2355
GDM_LANG=en_US.UTF-8
GDMSESSION=gnome
SPEECHD_PORT=7540
SHVL=1
HOME=/home/bentley
GNOME_DESKTOP_SESSION_ID=this-is-deprecated
LOGNAME=victim13
malwareforensics.com
DISPLAY=:0.0
XAUTHORITY=/var/run/gdm/auth-for-victim13-HhRHU/database
_=/usr/bin/printenv
```

**图 1.26** — 使用`printenv`命令收集的部分系统环境信息。

- 操作系统和内核的版本对于执行内存取证和其他分析任务至关重要。
- `/proc/version`文件中还包含额外的版本信息以及一些额外细节，例如编译器版本，如图 1.27 所示。

```text
# /media/cdrom/Linux-1R/cat /proc/version
Linux version 2.6.35-22-generic (buildd@otherbox) (gcc version 4.4.5 (Ubuntu/linaro 4.4.4-14ubuntu2)) #31-Ubuntu SMP Sun Sep 19 20:34:50 UTC 2010
```

**图 1.27** — 从`/proc`收集系统版本详细信息。

### 调查考虑事项

- `"/proc"`目录中还提供了有关系统环境的更多信息，包括`"/proc/cpuinfo"`中关于 CPU 的细节以及`"/proc/cmdline"`中用于启动内核的参数。

## 系统状态

- 收集有关目标系统状态的信息，以观察与目标系统上的恶意软件相关的活动。
- 当启用账户审计时，`sa`命令提供系统中已执行命令的摘要。例如，图 1.28 显示了`sa`命令的输出，其中包含安装新应用程序的条目、可能未经授权的添加新用户账户的条目，以及与后门安装相关的可疑`tar`和`irpd`命令。
