
-   用于运行命令的命令行 shell 对话框，其输出显示在主通信窗口中
-   用于设置调制解调器速度、奇偶校验和停止位的按钮

如果你创建了指向 /dev/modem 的符号链接，seyon 程序会自动识别并与你的调制解调器配合使用。你要做的就是输入包含拨号号码的 AT 命令字符串以拨出并连接另一台计算机。

如果你需要告诉 seyon 客户端调制解调器的具体设备，请在 seyon 命令中心窗口中单击 Set 按钮（启动客户端时会自动出现）以打开设置窗口。在设置窗口中单击 Port 按钮，并在 Values? 窗口中输入设备名称，例如 /dev/cua1。图 9.7 显示了 seyon 及其设置窗口。

## 图 9.7

X11 客户端 seyon 提供了调制解调器设置的点选便利性。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_228_0.png)

主 seyon 窗口

主 seyon 控制

帮助窗口

波特率设置

通信设置

单击 OK 按钮，然后单击设置窗口的 Close 按钮。如果你想以默认的调制解调器速度、位数或奇偶校验启动 seyon 程序，请编辑文件 $HOME/.seyon/。该目录在安装 seyon 程序时会自动安装。你可以在启动文件中更改以下行：

```
# set baud
set baud 19200

# can be 5, 6, 7, or 8
# set bits 8
set bits 8

# can be 0 (= no parity), 1 (= odd parity), or 2 (= even parity)
# set parity 0
set parity 0

# can be 1 or 2
# set stopBits 1
set stopBits 1
...
```

如果在使用 seyon 程序时需要帮助，可以在 seyon 命令中心窗口中单击 Help 按钮。会弹出一个窗口显示 seyon 手册页，你可以滚动文本以获取帮助（帮助屏幕显示在图 9.7 中）。

## 设置 Linux 系统以便拨入

你还可以设置 OpenLinux 系统，使计算机的调制解调器接听电话并允许你登录。然后你可以运行公告板系统（BBS）、文字处理器和电子表格程序。如果你至少连接了两台调制解调器到计算机并在家中有两条电话线，甚至可以拨出另一条线路。

大多数细节和自定义配置都在 /usr/doc/HOWTO 和 /usr/doc/getty_ps 目录下的 Serial-HOWTO 中，但这里概述的三个基本步骤应该适用于几乎任何调制解调器。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_229_0.png)

> 设置 OpenLinux 系统以接受来电涉及编辑 /etc/inittab 文件，如果操作有误可能会导致系统挂起。务必随身携带备份启动盘，并在更改前复制 /etc/inittab 文件。

首先，以 root 操作员身份登录并运行 minicom。使用 AT 命令 &V 显示调制解调器的配置文件或默认设置，例如：

```
AT&V
ACTIVE PROFILE:
B1 E1 L1 M1 N1 Q0 T V1 W0 X4 Y0 &C1 &D2 &G0 &J0 &K3 &O5 &R1 &S0 &T5 &X0 &Y0 -Z0
```

```
S00:000 S01:000 S02:043 S03:013 S04:010 S05:008 S06:004 S07:045 S08:002 S09:006
S10:014 S11:095 S12:050 S18:000 S25:005 S26:001 S36:007 S37:000 S38:020 S44:020
S46:138 S48:007 S51:012 S52:012 S53:010 S54:010 S95:000
```

你可能会看到调制解调器内部配置文件和寄存器的其他值，但你需要确保调制解调器至少设置为以下内容：

```
E1 Q0 V1 S0=1 &C1 &S0
```

你可以使用 AT 命令将调制解调器设置为这些值，例如：

```
ATE1Q0V1S0=1&C1&S0&W
OK
```

请注意，在 AT 命令字符串末尾，使用 &W AT 命令会将调制解调器配置保存为默认值。输入字符串后，你还可以看到调制解调器回显的 OK 提示，并且可以再次发出 AT&V 命令来验证设置。

第二步是在 /etc 目录下创建一个名为 default 的目录，如下所示：

```
# mkdir /etc/default
```

然后，使用 cp 命令从 /usr/doc/getty_ps 目录复制文件 ugetty.autoanswer，并将文件名重命名以匹配调制解调器的串行端口设备，如下所示：

```
# cp /usr/doc/getty_ps-2.0.7h/Examples/ugetty.autoanswer /etc/default/ugetty ttyS0
```

该命令行显示所需的串行端口为 /dev/ttyS0，对应于 DOS COM1 端口。现在使用你喜欢的文本编辑器编辑复制的文件，并查找以下行：

```
ALTLOCK=cua2
```

将 cua2 的默认值更改为与调制解调器的扩展名和串行端口相匹配，如下所示：

```
ALTLOCK=ttyS0
```

保存文件并退出编辑器。

最后一步涉及对 /etc/inittab 系统初始化表的单行编辑。如果查看此文件，你会看到以下行：

```
# less /etc/inittab
...
# Run gettys in standard runlevels
```

```
1:12345:respawn:/sbin/getty tty1 VC linux
2:2345:respawn:/sbin/getty tty2 VC linux
3:2345:respawn:/sbin/getty tty3 VC linux
4:2345:respawn:/sbin/getty tty4 VC linux
5:2345:respawn:/sbin/getty tty5 VC linux
6:2345:respawn:/sbin/getty tty6 VC linux
...
```

每行代表 /etc/inittab 文件开头记录的不同 Linux 运行级别。本讨论不涉及运行级别或 OpenLinux 启动的细节，但要为 Linux 系统启用拨入登录，你只需更改以下行：

```
3:2345:respawn:/sbin/getty tty3 VC linux
```

按如下方式更改：

```
3:2345:respawn:/sbin/ugetty ttyS0 38400 vt100
```

保存文件，并使用 shutdown 命令重新启动系统。此 inittab 条目告诉 OpenLinux 在启动后启动 getty 命令，并让 getty 监视你的 /dev/ttyS0 串行端口的来电。值 38400 不是调制解调器波特率，而是 /etc/gettydefs 文件中的自适应波特率条目（可在 38400 或更低速度下工作）。如果你拨入 OpenLinux 系统，调制解调器会与呼叫调制解调器的速度同步，然后显示登录提示。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_231_0.png)

当你登录 OpenLinux 时，/etc/issue 文件的内容会在登录提示符之前打印在显示屏上。该文件由 /etc/rc.d 目录中的启动脚本 rc.local 在每次启动 OpenLinux 作为启动过程的一部分时创建。作为 root 操作员，你可以自定义 rc.local 脚本来更改 /etc/issue 文件的内容，如果你想要不同的登录横幅。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_231_1.png)

如果你设置系统接受来电并想使用 minicom，请以 root 操作员身份运行 minicom。然后在配置菜单的串行端口设置下配置串行设备名称，使其与调制解调器的实际设备名称匹配，例如 /dev/ttyS1，并确保该名称不是符号链接，例如 /dev/modem。

## 发送和接收传真

如果你的调制解调器支持传真协议，很可能你可以使用 OpenLinux 发送和接收传真。在 OpenLinux 下发送和接收传真涉及对接收文件和要发送的文件进行图形转换。CD-ROM 上的 OpenLinux 发行版包含 efax 传真软件家族和文档。在开始之前，请准备好调制解调器的文档，并仔细阅读 /usr/doc/efax 目录下的 efax 手册页和文档。

## 使用 efax 系统传真

由 Ed Casas 开发的 efax 系统是一个简单易用的传真系统，根据其文档，最适合单用户独立 Linux 系统。该软件由一系列程序和脚本组成，并支持 Class 1 和 2 传真调制解调器。

该系统由以下程序组成：

-   `/usr/bin/efax`—传真程序
-   `/usr/bin/efix`—用于准备文本文件以便传真或将文件转换为不同图形格式的图形转换程序
-   `/usr/bin/fax`—用于创建、发送、接收、显示或打印传真文件的 shell 脚本

如果你想预览或传真 PostScript 图形文件，还需要在系统上安装 gs PostScript 解释器和配套查看器 gv。对于查看接收到的传真，可以使用 X11 客户端 xv（在第 16 小时“图形工具”中讨论）。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_232_0.png)

> 你需要编辑 /usr/bin/fax 脚本来配置传真。但在更改脚本之前，请先为自己做个好事，先复制一份。如果出现错误或删除文件，你需要一份副本来重新安装 efax 软件。

在开始发送或接收传真之前，请查看 /usr/bin/fax shell 脚本。该程序是 efax 传真服务的前端，但你需要检查文件中的几个部分以确保脚本配置正确。例如，第一部分列出了 efax 程序的名称：

```
FAX=/usr/bin/fax
EFAX=/usr/bin/efax
EFIX=/usr/bin/efix
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_232_1.png)
