
## 资源控制器 (SRC)

使用 `stopsrc` 命令来停止子系统。例如：

```bash
# stopsrc -g tcip  # 停止 TCP/IP 子系统组
```

在更新操作系统或一组产品时，通过关闭到维护模式来降低系统活动通常更为方便。这将停止所有应用程序和子系统，并限制除系统控制台外对系统的访问。

```bash
# shutdown -m  # 关闭到维护模式
```

如果不需要维护模式，你可以通过创建一个 `/etc/nologin` 文件来临时禁止非 root 用户的登录访问。每当非 root 用户尝试登录时，`/etc/nologin` 文件的内容都会显示出来。例如：

```text
由于系统维护活动，登录访问暂时被禁止。请在上午 7:30 之后重试。
```

`/etc/nologin` 文件可以是一个空文件。禁止非 root 登录的是 `/etc/nologin` 文件的*存在本身*，而不是文件的*内容*。如果 `/etc/nologin` 文件存在，它将在启动过程的第三阶段作为正常部分从系统中移除。请记住，如果你已经禁用了系统的远程 root 登录（这是强烈推荐的做法），那么当 `/etc/nologin` 文件存在时，你必须在控制台上才能登录系统！如果你不需要重启机器，请别忘了移除该文件，否则在你的维护窗口完成后，所有用户将继续被锁定在外。

### 更新现有的 AIX 系统

如果你将用户文件系统和本地产品数据保留在非 rootvg 卷组中，那么向现有 AIX 系统安装升级或维护会容易得多。在安装升级或维护之前，可以导出非 rootvg 卷组，从而保护它们免受更新问题的影响。

> **注意** 在导出卷组之前，记录逻辑卷的所有 `/dev` 设备的所有权关系至关重要。非 root 用户（如 db2adm）拥有逻辑卷的 `/dev` 设备是很常见的。当你导入逻辑卷时，所有的 `/dev` 逻辑卷都将归 root 所有。为了记录所有权关系，请运行命令 `ls -l /dev > /usr/local/etc/dev.lst`。

导入卷组后，你需要手动或通过脚本恢复所有权关系。

在卸载所有文件系统后，你可以使用以下命令导出卷组：

```bash
# exportvg <VGname>
```

更新完成后，可以使用以下命令将卷组重新导入系统：

```bash
# importvg -y <VGname> <PhysicalVolume>
```

例如：

```bash
# importvg -y appvg hdisk10
# mount -a
```

如果你需要为此卷组导入指定卷组*主设备号*（major number），例如在 HACMP 集群中，你可以添加 `-V major_number` 命令参数，如下例所示：

```bash
# importvg -V 46 -y appvg hdisk10
```

上述命令指定 46 是 **appvg** 卷组的主设备号。

要找到系统上下一个可用的主设备号，请使用以下命令：

```bash
# lsvlmajor
```

如果你的系统处于 HACMP 集群中，你必须保持设备主设备号的一致性，以便两台机器都知道每个共享卷组的主设备号是什么。

> **说明** 对于多物理卷（multi-pv）卷组，在使用 `importvg` 命令时，你只需指定卷组中的一个磁盘即可。

执行升级有两种方式。如果 AIX 的版本和修订号保持不变，而你正打算进行新的修改和修复级别（例如，你当前在 4.3.2.0，想要升级到 4.3.3.0），则存在一种快速升级路径。仅在这种情况下，你只需停止所有应用程序，锁定所有用户，导出所有非 rootvg 卷组，然后运行 `smitty update_all`。如果你有可用的磁盘空间，你可能希望使用 APPLY（应用）更新而不是使用 COMMIT（提交）。使用 APPLY，如果你希望更新未按预期工作，你有能力拒绝这些更新。此方法仅在 AIX 的版本和修订号保持不变时有效。但是，如果你要使用 APPLY 安装选项，你必须首先 COMMIT 系统中当前的所有内容。在命令行上，运行命令 `smitty install_commit`。接受所有默认值并按两次 ENTER。一旦之前 APPLY 的所有文件都处于 COMMIT 状态，你就可以继续升级了。

如果你要升级到新的 AIX 版本或发行版（例如，如果你要从 AIX 4.3.3.0 升级到 AIX 版本 5.1.0.0），则必须使用新的安装 CD-ROM 将系统引导到维护模式。在这种情况下，你正在同时升级版本和发行版级别。如果你要升级到不同的版本，例如从 5.1.0.0 升级到 5.2.0.0，你也必须从安装 CD-ROM 引导。

- 如果你拥有 PCI 总线机器，请从安装介质启动（对于 IBM 发布的 AIX 5.1，CD-ROM 是唯一选项）。将 CD-ROM 插入驱动器，如有必要打开电源，并在键盘初始化且发出蜂鸣声后立即按下相应的功能键（参见第 7 章）。
  > **说明** 并非所有机器都支持服务模式的启动列表（参见附录 A）。

- 如果你拥有一台带有钥匙开关的微通道（Micro Channel）机器，请将钥匙转到服务位置，将 CD-ROM 插入驱动器，重启或打开电源，并按照提示识别控制台并选择语言和安装方法。

在开始迁移安装之前，运行 `bootinfo -b` 命令以查找最后一个启动设备，并记下 `hdisk#` 以便日后参考。在开始保留安装（preservation install）之前，记录安装过程将使用的每个物理卷的位置、布局和空间。首先显示物理卷名称。

```bash
# lsvg
hdisk0        00008a3d84178021        rootvg
hdisk1        00008a3d1384358b        rootvg
hdisk2        00008a3d1382b3f9        appvg
hdisk3        00008a3d1382b821        appvg
hdisk4        00008a3d1382bb65        appvg
hdisk5        00008a3d1382beac        appvg
hdisk6        00008a3d1382ce16        appvg
hdisk7        00008a3d1382c512        appvg
```

对于每个物理卷，显示位置信息。

```bash
# lsdev -C -l hdisk0
hdisk0 Available 10-60-00-80,0 16 Bit SCSI Disk Drive
```

使用 `df` 和 `lsvg` 来统计构成根文件系统和根卷组的已用和空闲空间。

```bash
# df -v / /usr /tmp /var
Filesystem Total KB used    free     Sused iused ifree    tused Mounted
/dev/hd4      32768     29796  2972    90%     1864  6328    22%      
/dev/hd2      499712   456704 43008  91%      17428 107490 13%  /usr
/dev/hd3      323584    21968 30216  6%      103  83137   0%   /tmp
/dev/hd9var 1048576    227520 821056  21%    1635 260509 0%   /var
```

```bash
# lsvg rootvg
VOLUME GROUP:     rootvg            VG IDENTIFIER:   000b8a3bd3105eb23
VG STATE:              active          PP SIZE:       16 megarbyte(s)
VG PERMISSION:        read/write      TOTAL PPs:     1084 (17344 megarbytes)
MAX LVs:          256               FREE PPs:      710 (11360 megarbytes)
LVs:               9                 USED PPs:      374 (5984 megarbytes)
OPEN LVs:             8                 QUORUM:          1
TOTAL PVs:         2                 VG DESCRIPTORS:  1
STALE PVs:         0                 STALE PPs:         0
ACTIVE PVs:         2                 AUTO ON:         yes
MAX PPs per PV:  1016                MAX PVs:           32
LVG size:         128 kilobyte(s)    AUTO SYNC:       no
HOT SPARE:          no
```

### 克隆 AIX 系统

当你在*相同*的硬件（完全相同的硬件！）上克隆 AIX 系统时，你只需使用可引导的备份映像 *mkssysb* 即可。要将系统克隆到*不同*的硬件，你必须遵循特殊程序并从 IBM 提供的安装介质启动。使用 *mkssysb* 磁带在不同硬件上启动的问题在于，备份磁带上没有针对不同硬件架构所需的所有驱动程序。为了解决这个小小的问题，我们使用安装 CD-ROM 启动，同时将新的 *mkssysb* 磁带放在磁带驱动器中。当我们到达选项菜单时，我们选择 **Start Maintenance Mode For System Recovery**（为维护模式启动以进行系统恢复），然后在列表底部选择 **Install From A System Backup**（从系统备份安装）。然后菜单会提示你选择装有 *mkssysb* 磁带的磁带驱动器。系统将从磁带安装系统，并使用 CD-ROM 获取特定机器的适当驱动程序和文件集。这相当于在 CD 驱动器中插入基础操作系统 CD-ROM 并运行 *smitty* *cfgmgr*，以自动向系统添加驱动程序。

## 安装 AIX

如果你正在安装全新的 *pSeries* 或 *RISC System/6000*，基础操作系统（BOS）和部分产品运行时环境可能已预安装在系统中。请注意，预安装的系统并不代表完整的产品或维护集。在将系统配置为可用之前，你必須完成剩余产品和维护的安装。

如果你将在控制台使用串行连接的 TTY，请在 TTY 上使用以下设置：

- 9600 bps
- 8,1,none
- 24 × 80 显示

