
## 初始化本地硬件（键盘、调制解调器、鼠标、PCMCIA）

### hardware – 硬件设置

```
DEVICES_FORCE_IDE_DMA_ON=""
```
为列出的 IDE 设备开启 DMA。

```
DEVICES_FORCE_IDE_DMA_OFF=""
```
为列出的 IDE 设备关闭 DMA。

### clock – 时间设置

```
GMT="-u"
```
如果你的硬件时钟设置为 `GMT`（格林尼治标准时间），请将其设为 `-u`。否则设为 `--localtime`。此设置对于自动切换夏令时和冬令时非常重要。

```
TIMEZONE="CET"
```
时区对于夏令时和冬令时的切换也很重要。这会设置 `/usr/lib/zoneinfo/localtime`。

### console – 控制台设置：串行控制台、键盘、帧缓冲

```
SER_CONSOLE_SESSION="console"
```
控制台会话名称

```
SER_CONSOLE_SCREENRC="/usr/share/cyclades/screenrc"
```
屏幕配置文件

```
SER_CONSOLE_OWNER="root"
```
串行控制台会话的所有者

```
SER_CONSOLE_DEVICE="/dev/ttyC0"
```
第一个串行控制台设备，例如 Cyclades-Z 的 `/dev/ttyC0`。

```
KEYTABLE="de-latin1-nodeadkeys"
```
定义键盘布局。如果你使用美式键盘，此变量可以留空。

```
KBD_NUMLOCK="no"
```
将其设为 `no` 后，启动时不会启用 (NumLock)。

```
KBD_CAPSLOCK="no"
```
启动时不要启用 (CapsLock)。

```
KBD_TTY="tty1 tty2 tty3 tty4 tty5 tty6"
```
将 (NumLock) 和 (CapsLock) 限制在特定的 TTY 上。`""` 表示所有 TTY。

```
KBD_RATE="30,0"
```
键盘自动重复的速率。将其设为每秒 2 到 30 次之间的值。还需要设置延迟变量。

```
KBD_DELAY="250"
```
设置自动按键重复开始前的延迟。可能的值：250、500、750 和 1000（毫秒）。同时设置变量 `KBD_RATE`。

```
CONSOLE_FONT=""
```
启动时加载的控制台字体。其他设置包括：`CONSOLE_SCREENMAP`、`CONSOLE_UNICODEMAP` 和 `CONSOLE_MAGIC`。

```
COMPOSETABLE="clear winews shiftctrl latin1.add"
```
要加载的 Compose 表。

### irda – IrDA 是红外接口，例如笔记本电脑使用的接口。

```
IRDA_PORT="/dev/ttyS1"
```
当前默认配置支持 UART（SIR）模式。如果你希望使用 FIR（4 Mbit/s，仅少数芯片组支持），请参阅 IrDA HOWTO，位于 `/usr/doc/howto/en/IRDA-HOWTO.gz`。变量 `IRDA_PORT` 设置所使用的串行端口。请查看你的 BIOS 设置以确定哪个端口是正确的。

### mouse – 鼠标设置

```
MOUSE="/dev/ttyS0"
```
指定鼠标所连接的接口。YaST2 或 SuSEconfig 会创建一个指向该设备的链接 `/dev/mouse`。

```
GPM_PROTOCOL=""
```
鼠标设备（来自变量 `MOUSE`）的 gpm 协议。默认值由 YaST2 定义。

```
GPM_PARAM="-t $GPM_PROTOCOL -m $MOUSE"
```
gpm 的默认参数。

### joystick – 摇杆配置

```
GAMEPORT_MODULE_0=""
```
游戏端口模块名称，例如 ns558（用于传统游戏端口支持）。

```
JOYSTICK_MODULE_0=""
```
摇杆模块名称，通常为 analog。

```
JOYSTICK_MODULE_OPTION_0=""
```
摇杆模块选项，例如 analog 的 `gameport`。

```
JOYSTICK_CONTROL_0=""
```
要激活的声卡驱动控制名称（通过 alsactl）。

```
JOYSTICK_CONTROL_PORT_0=""
```
要使用的端口（通过 alsactl）。某些声卡（如 ens1371）需要端口地址（通常为 0x200）。

### pcmcia - PCMCIA 系统和 PC 卡。

```
PCMCIA_SYSTEM="external"
```
将该变量设置为 `external` 或 `kernel`。

```
PCMCIA_PCIC=""
```
为所选 pcmcia 系统指定插槽驱动程序。对于外部 pcmcia 系统，可能的值是 `i82365` 或 `tcic`；对于内核 pcmcia，则为 `yenta_socket`、`i82365` 或 `tcic`。如果留空，启动脚本将尝试确定正确的驱动程序或使用合理的默认值。

```
PCMCIA_PCIC_OPTS=""
```
插槽驱动程序时序参数。这些参数在手册页 i82365（或 man tcic）中有描述。

```
PCMCIA_CORE_OPTS=""
```
pcmcia_core 选项，如 man pcmcia_core 中所述。更多信息请参阅 `/usr/doc/packages/pcmcia` 下的 PCMCIA-HOWTO 中的“CORE_OPTS”。

### powermanagement - apmd。

```
APMD_WARN_LEVEL="10"
APMD_WARN_ALL="no"
APMD_WARN_STEP="0"
APMD_CHECK_TIME="0"
APMD_DEBUG="no"
APMD_ADJUST_DISK_PERF="no"
APMD_BATTERY_DISK_TIMEOUT="12"
APMD_AC_DISK_TIMEOUT="1"
APMD_BATTERY_DATA_TIMEOUT="30"
APMD_BATTERY_LOW_SHUTDOWN="0"
```
以分钟为单位。

```
APMD_SET_CLOCK_ON_RESUME="no"
APMD_SUSPEND_ON_AC="yes"
APMD_PCMCIA_SUSPEND_ON_SUSPEND="no"
APMD_PCMCIA_EJECT_ON_SUSPEND="no"
APMD_INTERFACES_TO_STOP=""
APMD_INTERFACES_TO_UNLOAD=""
APMD_LEAVE_X_BEFORE_SUSPEND="no"
APMD_LEAVE_X_BEFORE_STANDBY="no"
APMD_LOCK_X_ON_SUSPEND="no"
APMD_STOP_SOUND_BEFORE_SUSPEND="no"
APMD_KBD_RATE=""
APMD_KBD_DELAY=""
APMD_TURN_OFF_IDE_DMA_BEFORE_SUSPEND=""
```

## 安全与本地管理服务

### security - 系统安全设置

```
CHECK_PERMISSIONS="set"
```
SuSEconfig 是否应使用 `/etc/permissions` 检查文件权限？值 `set` 将纠正错误的设置，`warn` 会产生警告。使用 `no` 禁用此功能。

```
PERMISSION_SECURITY="easy local"
```
在 `/etc/permissions.paranoid`、`/etc/permissions.secure` 和 `/etc/permissions.easy` 中预定义了安全级别。请输入 `easy`、`secure` 或 `paranoid`。如果你选择 `paranoid`，某些系统服务可能不再可用。如有需要，请显式启用它们。

```
CONSOLE_SHUTDOWN="reboot"
```
该变量决定 init 进程如何处理 `Ctrl` + `Alt` + `Del`。必须将 `CHECK_INITTAB` 设为 `yes` 才能激活此功能。可能的设置是 `ignore`、`reboot` 和 `halt`。默认值是 `reboot`。

### backup - RPM 数据库的备份

```bash
RPMDB_BACKUP_DIR="/var/adm/backup/rpmdb"
```
RPM 数据库的 cron.daily 备份应存储在何处？如果你不需要备份，请将变量设置为 `""`。

```bash
MAX_RPMDB_BACKUPS="5"
```
RPM 数据库的备份数量。

```bash
MAX_RCONFIG_BACKUPS="5"
```

## cron

系统上的日常管理工作。
