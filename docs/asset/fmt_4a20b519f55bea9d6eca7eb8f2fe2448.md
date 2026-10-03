
- 64. 退出系统并重新登录，现在的提示符包含用户 ID、主机和路径。

```
Compaq Tru64 UNIX V5.1A (Rev. 1885) (rac1) (pts/1)

login: root
Password: ********

Last login: Fri Oct 12 09:47:29 CDT 2001 on console
Compaq Tru64 UNIX V5.1A (Rev. 1885); Fri Oct 12 09:26:47 CDT 2001
....

root : /
rac1>
```

# 管理 Tru64 UNIX 软件子集

`setld` 命令用于在 Tru64 UNIX 中加载、删除和查看已安装的软件。

- 65. 查看系统上安装的所有软件子集。
```
rac1> setld -i
```

| Subset | Status | Description |
| --- | --- | --- |
| OSFACT520 (Administration) | installed | 系统统计工具 (系统管理) |
| OSADVFS520 | installed | AdvFS 命令 (系统管理) |
| OSADVFSBIN520 | installed | AdvFS 内核模块 (内核构建环境) |
| OSADVFSBINJECT520 | not installed | AdvFS 内核对象 (内核软件开发) |
| OSADVFSADAEMON520 | installed | AdvFS 守护进程 (系统管理) |
| OSPAM520 | installed | Adobe 字体度文件 (打印环境) |
| OSFXPRT520 | installed | Print X Server (Windows 应用) |
| OSFSYSMAN520 (System Administration) | installed | 图形基础系统管理工具 |
| OSFES520 | installed | 虚拟 X 帧 (Windows 应用) |
| TCRBADES520 | installed | TruCluster 基础组件 (TruCluster软件) |
| TCRMAN520 (TM) Software) | installed | TruCluster 参考页 (TruCluster) |
| TCRMRATE520 (TM) Software) | installed | TruCluster 迁移组件 (TruCluster) |

# 安装用于远程访问的 X-Server

如果你的服务器没有图形，你需要在安装 Oracle 之前安装 X-Server。所有流行的桌面都有良好的 X-Server。这些 X-Server 运行在桌面以显示控制台。在桌面运行 X-Server 的缺点是，如果桌面关闭连接将被终止。

名为虚拟计算（VNC）的免费工具由 AT&T 研究提供。VNC 服务器将安装在 Tru64 UNIX 上，并使用客户端查看。这种方法的优点是允许桌面重启或重新连接。

下载 Tru64 UNIX (DEC OSF) 的服务器以及用于桌面电脑的客户端。

```
http://www.research.att.com/
```

- 66. 启动 `vncserver`。首次运行时必须设置密码。VNC 密码与 UNIX 密码分开。
```
rac1> ./vncserver
```

```
访问桌面需要密码。
Password: ******
Verify: ******

新的 'X' 桌面是 rac1.domain.com:1

创建启动脚本 /home/oracle/.vnc/xstartup
启动 /home/oracle/.vnc/xstartup 中指定的应用程序
日志文件为 /home/oracle/.vnc/rac1.domain.com:1
```

- 67. 使用大多数操作系统提供的 `vncviewer` 连接到 VNC 桌面。客户端连接包含 `vncserver` 启动期间分配的服务器端口。在图 3-2 中，服务器名为 `rac1.domain.com`，会话为 1。

![](img/c5e29563e8b7ebaf2f5af630a4e1eb9_108_0.png)

图 3-2 VNC X-Window 显示，默认启动屏幕

- 68. 设置 `DISPLAY` 环境变量并运行 `xclock` 等 X 程序测试连接。允许其他用户连接到此桌面需要在设置 `DISPLAY` 后执行 `xhost +` 命令。

```bash
rac1> export DISPLAY=rac1.domain.com:1.0

rac1> xclock &

rac1> xhost +
```

- 69. 要启动标准 CDE 环境，按所示注释掉 `xstartup` 文件中的行并在文件末尾添加 `/usr/dt/bin/Xsession`，这将启动图 3-3 所示的 CDE 环境。`xstartup` 文件存储在用户家目录下的 `.vnc` 目录中。

```bash
rac1> cd ~/.vnc

rac1> cat xstartup

#!/bin/sh

# xrdb $HOME/.Xresources

# xsetroot -solid grey

# xterm -geometry 80x24+10+1 -ls -title "$VNCDESKTOP Desktop" &

# twm &

/usr/dt/bin/Xsession &
```

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_109_0.png)
图 3-3 VNC 桌面环境 (CDE) 启动会话

## 使用 Sysman 查看硬件信息

启动 `sysman` 工具以启动图形界面，用于监控和管理单节点或集群系统。图 3-4 所示的示例为默认视图，显示没有任何警告或警报。

```bash
rac1> sysman -station
```

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_109_1.png)
图 3-4 Sysman 工作站视图

从 `sysman -station` 视图，还可以看到硬件视图。Sysman 为已安装的硬件组件创建一个图形视图。硬件视图如图 3-5 所示。

![](img/c5e29563e8b7ebaf2f5afc630a4e1eb9_110_0.png)
图 3-5 Sysman 工作站硬件视图

| 类别 | Tru64 UNIX 安装摘要 |
| :--- | :--- |
| boot (启动) | 从硬件控制台发出 `boot` 命令以启动 Tru64 UNIX 安装。<br><br>使用 `device` 命令定位您的 CD-ROM 驱动器。您的系统设备可能与此示例不同。<br><br>`p000> boot dga0` |
| Hardware Manager (硬件管理器) | 使用 `hwmgr` 命令管理磁盘等硬件组件。<br><br>检查集群磁盘设备的编号。<br>`# hwmgr -show scsi`<br>`# hwmgr -delete scsi -did 10`<br>`# hwmgr -scan scsi`<br>`# hwmgr -view devices` |
| License Management (许可证管理) | 使用 `lmf` 命令管理 Tru64 UNIX 许可产品。<br><br>将许可证注册到许可证数据库中。<br>`# lmf register`<br><br>使用 `reset` 选项将信息从许可证数据库复制到正在运行的内核中。<br>`# lmf reset`<br><br>使用 `list` 选项查看许可证数据库中注册的许可证。<br>`# lmf list`<br><br>提供一个 X Window GUI 来管理软件许可证。<br>`# dclienses` |
| Tru64 UNIX Management (Tru64 UNIX 管理) | Tru64 UNIX 5.1A 提供了几个实用的管理工具。大多数可用的管理工具都是基于文本和图形的，为管理员提供了更大的灵活性。<br><br>`checklist` 实用程序用于配置 Tru64 UNIX 操作系统参数。此应用程序需要 X-Window 图形显示。`checklist` 的选项包括：快速设置、自定义设置或克隆信息。 |

## checklist

设置程序是一个基于文本菜单的程序，具有与 `checklist` 相同的功能。

```bash
# setup
```

`sysman` 工具是一个用于管理 Tru64 UNIX 系统的常用菜单界面。该工具以文本程序、X-Windows 和 Java 的形式提供。

要启动 `sysman`，请输入以下命令。默认将显示 `sysman` 的 X-Windows 版本。

```bash
# sysman
```

要强制使用基于文本菜单的 `sysman`，你可能需要取消定义 `DISPLAY` 环境变量。

```bash
# unset DISPLAY

# sysman
```

列出所有 `sysman` 菜单快捷键。

```bash
# sysman -help
```

`sysman` 指向网络菜单的快捷键。

```bash
# sysman -network
```

`setld` 命令用于加载、查看和删除可选的 Tru64 UNIX 软件子集。

使用 `setld -l` 命令加载可选的软件子集。

```bash
# setld -l
```

要删除软件子集，使用 `setld` 命令的 `delete` 选项。使用 `setld -i` 命令显示的软件子集名称。在 `-` 之后可以添加多个软件子集。

```bash
racl> dsfmgr -m dsk13 dsk17

racl> dsfmgr -m dsk12 dsk16

racl> dsfmgr -m dsk11 dsk15

racl> dsfmgr -m dsk10 dsk14

racl> dsfmgr -m dsk9 dsk13

racl> dsfmgr -m dsk8 dsk12
```

3. 使用硬件管理器再次查看设备。确认所有重编号的磁盘设备与控制器标识符匹配。

```bash
racl> hwmgr -view device
```
