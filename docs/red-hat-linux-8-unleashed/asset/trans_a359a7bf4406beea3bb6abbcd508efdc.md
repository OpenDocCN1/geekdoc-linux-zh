

# 检测和配置调制解器

usb.c: registered new driver serial
usbserial.c: USB Serial support registered for Generic
usbserial.c: USB Serial Driver core v1.4
usbserial.c: USB Serial support registered for Keyspan PDA
usbserial.c: Keyspan PDA converter detected
usbserial.c: Keyspan PDA converter not attached to ttyUSB0 (or usb/tty/0 for devs)
usbserial.c: USB Serial support registered for Keyspan PDA - (prerunation)
usbserial.c: USB Serial support registered for Xircom PGS - (prerunation)
usbserial.c: USB Serial support registered for Integra PGS - (prerunation)
keyspan_pda.c: USB Keyspan PDA Converter driver v1.1

# 配置传真调制解器

当设备插入时，Red Hat Linux 会自动识别并配置指定的串口（例如示例中的 `/dev/ttyUSB`）。Red Hat Linux 还附带了许多传真实用程序，用于配置系统接收传真。最容易配置的传真实用程序之一是 `fax` 命令。作为 root 用户，你可以通过编辑 `/usr/bin/fax` 脚本中的几个条目来配置软件：

```
DEV=modem
FROM="1 555 555-1212"
NAME="Company Name"
```

最重要的条目是 `DEV=`，只要 `/dev/modem` 指向一个激活的传传真调制解器，就不需要更改。你也可以编辑 `/usr/bin/fax` 来自定义其他条目，例如传真查看命令。使用 test 命令行选项检查设置，例如：

```
# fax test
```

使用 `fax` 命令发送传真非常简单：

```
# fax send 5551212 document.txt
```

# 配置 minicom 用于调制解器

使用 `minicom` 或 `xminicom` 脚本（在 X 会话期间在终端窗口启动 minicom）进行拨号连接以及与远程 Red Hat Linux 系统的终端会。要配置此终端程序以用于连接的调制解器，以 root 身份使用 `-s` 或 `setup` 选项运行客户端：

```
# minicom -s
```

# 第 4 章 安装后配置

按下回车键后，你会看到一个设置对话框。选择 Serial-Port Configuration（串口配置）并按回车。你将看到一个如图 4.9 所示的 Configuration Settings（配置设置）框，可以使用它配置程序与连接的调制解器工作。

![](img/446be023486a7fde572450.png)
图 4.9 使用 minicom 的设置对话框配置程序与连接的调制解器工作。

# 为笔记本电脑配置无控制器调制解器

关于调制解器的其他问题集中在使用无控制器调制解器的笔记本用户。这些调制解器使用专用软件仿真硬件。尽管已经发布了一些二进制驱动，但它们仍然是笔记本和桌面用户的困恼。你可能会找到对 Lucifer（但不支持 AMR）、Motorola SM56 型、IBM Wave 和 Conexant HSF 的支持。在本文写作时，尚未对 COM 或 USB 提供支持。有关驱动程序的链接和更多信息，请访问 Linux 页面 `http://www.redhat.com`。

# 在 Red Hat Linux 中配置电源管理

高级电源管理（APM）允许工作站和服务器在接收关闭指令时自动关闭。Red Hat Linux 移动用户经常使用 APM，APM 可以通过智能电路、CPU“节流”（类似于但不同于 Pentium III 和 IV CPU 中包含的热节流）以及对显示器和硬盘的控制来帮助延长电池寿命。大多数 PC 都通过 BIOS 和硬件支持 APM。APM 支持的配置、启用以及整合到 Linux 内核中的信息不断在文件 `/proc/apm` 中更新，其内容可能如下所示：

```
# /proc/apm
14 0x03 0x01 0x09 10800
```

此示例提供了有关电池电量的信息，以及剩余的时间和百分比。从左到右，示例分别是驱动程序版本、BIOS 版本、AC 状态、电池状态、电池状态以及剩余寿命秒数。某些 X11 客户端（如 `apm` 和 `apload`）解析此文件并以更易格式显示信息。这些客户端对笔记本用户特别有帮助。Red Hat 包含的所有内核都支持 APM。然而，硬件问题或 APM 配置错误可能会导致某些硬件发生内核崩溃（kernel panic），导致无法启动。当发生这种情况时，你必须重新配置 APM，然后编译并安装新的 Linux 内核（更多信息请参考第 2 章）。

基本的内核 APM 配置选项包括：

- CONFIG_APM—是否配置 APM 支持
- CONFIG_APM_IGNORE_USER_SUSPEND—忽略键盘挂起
- CONFIG_APM_DO_ENABLE--启动时启用 APM
- CONFIG_APM_CPU_IDLE--未使用时让 CPU 空闲
- CONFIG_APM_DISPLAY_BLANK--启用显示器或 LCD 屏空白
- CONFIG_APM_RTC_IS_GMT--确定时钟设置
- CONFIG_APM_ALLOW_INTS--在使用 APM 允许中断（如串口活动）
- CONFIG_APM_REAL_MODE_POWER_OFF--启用关电

Red Hat Linux 包含了几个与 APM 相关的命令——例如打印 APM 信息的 `apm` 以及用于在特定时间睡眠和唤醒笔记本硬件的 `apmsleep`。Red Hat Linux 笔记本用户可以这样使用 `apm` 命令：

```
$ apm -v
APM BIOS 1.2 (kernel driver 1.16)
AC on-line, battery status: 95%
```

# 第 4 章 安装后配置

内核中包含的其他电源管理包括对外设组件接口（PCI）设备的控制以及显示器的电源管理信号（DPMS），它们可以通过在设定时间后将设备置于低功耗状态来节省能量。正如精明的 Red Hat Linux 系统管理员和用户所知，屏幕保护程序不再需要保护显示器免受图像“烧屏”。屏幕保护程序启用的密码保护仅提供物理安全手段。

硬件监控由 `lm_sensors` 软件包支持，该软件包因早期版本导致 IBM ThinkPad 笔记本遭受永久损坏而闻名。然而，管理桌面 PC 的系统管理员可以从 `sensors` 命令等应用程序中受益，它利用了 `lm_sensors` 库的硬件监控功能。

你可以通过编辑（root）文件 `/etc/sensors.conf` 来自定义 `sensors` 的输出，但默认设置适用于你的计算机。要启用传感器读取，使用 `sensors-detect` 命令来确定需要加载哪些内核模块以启用传感器输出：

```
# /usr/sbin/sensors-detect
```

此程序将帮助你确定为了有效使用 `lm_sensors` 需要加载哪些 I2C/SMBus 模块。

在使用此实用程序的某些功能之前，你需要已执行 `make install`、发布 `depmod -a` 并确保 `/etc/conf.modules`（或 `/etc/modules.conf`）包含相应的模块路径。请阅读 `doc/modules` 获取更多信息。

此外，你需要是 'root'，或者至少拥有对 `/dev/i2c-*` 文件的访问权限。如果你还没有这些 `/dev` 文件，可以使用 `prog/mkdev.sh` 来创建它们。

如果你已经补丁了内核并内置了驱动程序，那么在被要求加载某些模块时可以安全地回答 NO。在这种情况下，情况可能会看起来有些困惑，但它们仍然可以正常工作。

我们可以从探测 (PCI) I2C 或 SMBus 适配器开始。
此不需要任何特殊权限。
现在要进行探测吗？(YES/no):

