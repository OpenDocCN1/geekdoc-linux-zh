
从文件读取设备配置。当你希望使用许多命令行选项生成 QEMU 进程但不想超出命令行字符限制时，这种方法非常有用。

### `-writeconfig` 文件

将设备配置写入文件。该文件可以是用于将命令行和设备配置保存到文件中的文件名，或者是破折号（`-`）字符，用于将输出打印到标准输出。这可以稍后用作 `-readconfig` 选项的输入文件。

### `-no-defconfig`

通常 QEMU 在启动时从 `sysconfdir` 和 `datadir` 加载配置文件。`-no-defconfig` 选项将阻止 QEMU 加载其中任何配置文件。

### `-no-user-config`

`-no-user-config` 选项使 QEMU 不加载 `sysconfdir` 上任何用户提供的配置文件，但不会跳过 `datadir` 中 QEMU 提供的配置文件。

### `-trace [events=file],[file=file]`

指定跟踪选项。

- `events=file`：立即启用文件中列出的事件。文件必须每行包含一个事件名称（如 `trace-events` 文件中所述）。仅当 QEMU 使用简单或 stderr 跟踪后端编译时，此选项才可用。
- `file=file`：将日志输出跟踪到文件。仅当 QEMU 使用简单跟踪后端编译时，此选项才可用。

### `-enable-fips`

启用 FIPS 140-2 合规模式。

### `-msg timestamp=[on|off]`

在每个日志消息前添加时间戳。（默认：`on`）

### `-dump-vmstate`

`*file*`

将当前机器类型的 json 编码 `vmstate` 信息转储到 `*file*` 中的文件。

### 通用对象创建

### `-object typename,[prop1=value1,...]`

创建一个新对象，类型为 `typename`，并按指定顺序设置属性。请注意，`id` 属性必须设置。这些对象放置在 `'/objects'` 路径中。

#### `-object memory-backend-file, id=id,size=size,mem-path=dir,share=on|off`

创建一个内存文件后端对象，可用于使用大页支持客户机 RAM。`id` 参数是一个唯一 ID，将在配置 `-numa` 参数时用于引用此内存区域。`size` 选项提供内存区域的大小，并接受常见后缀，例如 `500M`。`mem-path` 提供共享内存或大页文件系统挂载的路径。`share` 布尔选项确定内存区域是标记为 QEMU 私有还是共享。后者允许协作的外部进程访问 QEMU 内存区域。

#### `-object rng-random, id=id,filename=/dev/random`

创建一个随机数生成器后端，从主机上的设备获取熵。`id` 参数是一个唯一 ID，将从 `virtio-rng` 设备引用此熵后端。`filename` 参数指定从哪个文件获取熵，如果省略则默认为 `/dev/random`。

#### `-object rng-egd, id=id,chardev=chardevId`

创建一个随机数生成器后端，从主机上运行的外部守护程序获取熵。`id` 参数是一个唯一 ID，将从 `virtio-rng` 设备引用此熵后端。`chardev` 参数是字符设备后端的唯一 ID，提供与 RNG 守护程序的连接。

### 图形键盘快捷键

在图形会话期间，你可以使用特殊的按键组合来更改模式。默认的按键映射如下所示，但如果你使用 `-alt-grab`，则修饰键是 `Ctrl-Alt-Shift`（而不是 `Ctrl-Alt`）；如果你使用 `-ctrl-grab`，则修饰键是右 `Ctrl` 键（而不是 `Ctrl-Alt`）：

- `Ctrl-Alt-f`：切换全屏
- `Ctrl-Alt-+`：放大屏幕
- `Ctrl-Alt--`：缩小屏幕
- `Ctrl-Alt-u`：恢复屏幕的未缩放尺寸
- `Ctrl-Alt-n`：切换到虚拟控制台 `'n'`。标准控制台映射为：
  - `1`：目标系统显示
  - `2`：监视器

### 串行端口

在虚拟控制台中，你可以使用 `Ctrl-Up`、`Ctrl-Down`、`Ctrl-PageUp` 和 `Ctrl-PageDown` 在日志中上下移动。

`Ctrl-Alt` 切换鼠标和键盘抓取。

在仿真期间，如果你使用了 `-nographic` 选项，请使用 `Ctrl-a h` 获取终端命令：

- `Ctrl-a h`
  打印此帮助信息
- `Ctrl-a ?`
  打印此帮助信息
- `Ctrl-a x`
  退出模拟器
- `Ctrl-a s`
  将磁盘数据保存回文件（如果使用 `-snapshot`）
- `Ctrl-a t`
  切换控制台时间戳显示
- `Ctrl-a b`
  发送中断信号（在 Linux 中为魔法系统请求键）
- `Ctrl-a c`
  在控制台和监视器之间切换
- `Ctrl-a Ctrl-a`
  发送 `Ctrl-a`

以下选项专用于 PowerPC 仿真：

- `-g WxH[xDEPTH]`
  设置初始 VGA 图形模式。默认为 `800x600x32`。
- `-prom-env string`
  在 NVRAM 中设置 OpenBIOS 变量，例如：
```
qe-system-ppc -prom-env 'auto-boot?=false' \
 -prom-env 'boot-device=hd:2,\yaboot' \
 -prom-env 'boot-args=config=hd:2,\yaboot.conf'
```
这些变量不被 Open Hack'Ware 使用。

以下选项专用于 Sparc32 仿真：

- `-g WxH[xDEPTH]`
  设置初始图形模式。对于 `tcx`，默认为 `1024x768x8`，可选 `1024x768x24`。对于 `cgthree`，默认为 `1024x768x8`，可选 `1152x900x8` 供希望使用 OBP 的用户使用。
- `-prom-env string`
  在 NVRAM 中设置 OpenBIOS 变量，例如：
```
qe-system-sparc -prom-env 'auto-boot?=false' \
-prom-env 'boot-device=sd(0,2,0):d' -prom-env 'boot-args=linux single'
```

`-M [SS-4|SS-5|SS-10|SS-20|SS-600MP|LX|Voyager|SPARCClassic] []|SPARCbook]`

设置仿真的机器类型。默认为 `ss-5`。

以下选项专用于 Sparc64 仿真：

`-prom-env string`

在 NVRAM 中设置 OpenBIOS 变量，例如：
```
qe-system-sparc64 -prom-env 'auto-boot?=false'
```

`-M [sun4u|sun4v|Niagara]`

设置仿真的机器类型。默认为 `sun4u`。

### 另请参阅

有关更详细的信息，请参见 `QEMU` 的 `HTML` 文档，以及 `Linux` 用户模式 `模拟器` 的调用方式。

### 作者

Fabrice Bellard

### QUOTA（配额）

### 名称

`quota` - 显示磁盘使用情况和使用限制

### 概要

```
quota [-F format-name] [-guqvswi] [-l|-Q|-A|-m]
quota [-F format-name] [-qvswi] [-l|-Q|-A|-m] -u user...
quota [-F format-name] [-qvswi] [-l|-Q|-A|-m] -g group...
quota [-F format-name] [-qvswugQm] -f filesystem...
```

### 描述

`quota` 显示用户的磁盘使用情况和使用限制。默认情况下仅打印用户配额。默认情况下，空间使用情况和使用限制以千字节显示（出于历史原因，它们被称为块）。

`quota` 报告在 `/etc/mtab` 中列出的所有文件系统的配额。对于通过 NFS 挂载的文件系统，将在服务器机器上调用 `rpc.rquotad` 以获取信息。

### 选项

- `-F, --format=format-name`
  显示指定格式的配额（即，不执行格式自动检测）。可能的格式名称包括：`vfso1` 原始配额格式，具有 16 位 UID / GID；`vfsv0` 具有 32 位 UID / GID、64 位空间使用量、32 位 inode 使用量和限制的配额格式；`vfsv1` 具有 64 位配额限制和使用量的配额格式；`rpc` （NFS 上的配额）；`xfs` （XFS 文件系统上的配额）
- `-g, --group`
