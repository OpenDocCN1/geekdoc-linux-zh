
接下来指定安装方法。可选两个关键字是`cdrom`和`nfs`。不支持其他安装方法。`nfs`关键字需要`--server`和`--dir`参数来指定要使用的服务器以及该服务器上ISO9660或NFS镜像的路径。

## device（设备）

安装程序将自动探测并检测IDE控制器和PCI总线卡。如果存在无法通过其他方式发现的设备（主要是：ISA卡），则使用`device`关键字。选项有`ethernet`、`scsi`和`cdrom`。`--opts`参数用于传递任何所需的模块参数，具体见《RedHat Linux 6.0 安装指南》的附录E。可以声明多个同种类型的设备。通常情况下，每类设备只会被发现一个。如果配置需要多个不同类型但同类的适配器，则使用`--continue`子句来检测同一适配器的多个实例：

```
device ethernet --opts "io=300, irq-9"
device ethernet --opts "io=270, irq-5"
device ethernet --opts "io=270, irq-5"
device scsi ahal --continue
device scsi 53cxx --continue
```

## keyboard（键盘）

`keyboard`关键字用于指定键盘映射。可以使用`keyboard`命令来确定系统中当前使用的键盘映射。最常见的值是`us`。

### noprobe（不探测）

`noprobe`关键字禁用设备的自动探测。仅当Linux无法成功探测系统时使用此项。此时需要指定`device`语句来配置系统。

### zerombr（零引导记录）

`zerombr`接受单个参数（`yes`或`no`），用于控制安装是否将清零引导记录（MBR）。如果不确定当前MBR是否有效，建议使用`yes`。

### clearpart（清除分区）

`clearpart`关键字决定是否应该清除分区表。这是一个可选关键字。该关键字的选项有`--all`（清除所有分区）和`--linux`（仅清除Linux相关的分区）。

### Partitioning with part（使用 part 进行分区）

`part`关键字用于指定启动设备上的分区数量和大小。每个分区都会发布一个`part`语句，用于交换分区、分区大小、`--grow`选项和`--maxsize`选项。`--grow`选项表示分区可以调整大小以适应更大的设备，而`--maxsize`选项则限制增长的绝对值。如果给多个分区指定了`--grow`选项，则额外的空间将平均分配给它们。

## Installation or Upgrade（安装或升级）

配置文件中的下一个语句必须指示系统是安装的还是升级。正在升级的系统仅需要定义以下关键字：安装机制（`cdrom`或`nfs`）、任何所需的设备规格、键盘类型、升级本身以及鼠标语句。

### Mouse Configuration（鼠标配置）

`mouse`关键字配置鼠标系统。`mouse`关键字的参数与`mousesetup`命令相同。`kickstart`选项是强制性的。如果没有检测到鼠标，则假设在`com1`（`/dev/tty0`）上有一个串口鼠标。在运行的Linux系统上运行`mousesetup --help`可以找到各种鼠标类型。

### Setting the Time Zone（设置时区）

系统级时区通过`timezone`关键字设置。时区信息数据库存储在`/usr/share/zoneinfo`目录中。例如，美国东部的`timezone`语句如下：

```
timezone US/Eastern
```

有一个选项需要特殊说明：`--utc`选项指定计算机时钟的时间为协调世界时（UTC，以前称为格林尼治标准时间）。UNIX系统传统上将内部时间表示为自1970年1月1日起的UTC秒数。内部时间是显示正确本地时间的本地区域数据。从实践角度考虑，笔记本电脑和台式机上应设置此值，以便在旅行期间无需调整时间即可正确设置时区。在配置为启动Windows操作系统的计算机上不应设置`--utc`选项。这些操作系统缺少适当的时区支持，期望硬件时钟反映本地时区。

### X Window System Configuration（X窗口系统配置）

`xconfig`关键字配置X Window系统。通常会探测视频硬件以自动确定其配置可能性，此关键字的目的是指定显示器类型。`--monitor`参数引入显示器类型。然而，某些视频硬件可能无法正常探测，因此偶尔需要使用`--server`选项指定特定的卡。运行`xconfig --help`将显示显示器和图形适配器的可能选择。这是一个探测正常的适配器的典型示例：

```
xconfig --monitor "nokia 45xi"
```

最后，通过使用`--hsync`和`--vsync`选项指定显示器的频率可以支持数据库中未出的显示器。可以通过逗号列出多个频率，并用破折线表示范围。这里是一个明确指定适配器且显示器未列在数据库中的系统示例：

```
xconfig --server "B514" --hsync "30.0-102.0" --vsync "50.0-120.0"
```

### Configuring a Root Password（配置根密码）

根密码可以通过`rootpw`语句设置。可以指定为加密或未加密形式。`--isencrypted`选项指定密码是加密的。作者建议使用加密形式作为一种实际的安全措施。

## Configuring NIS（配置 NIS）

`auth`配置密码安全和NIS。选项如下：

- `--usershadow` 启用影子密码机制。出于安全考虑建议使用。
- `--enable5` 启用加密强度更高的密码机制。出于安全考虑建议使用。
- `--enablenis` 配置系统使用NIS。如果给出此选项，则需要`--nisdomain`选项。
- `--nisdomain` 此选项接受一个参数，指定NIS域名。
- `--nisserver` 选项提供系统要绑定的NIS服务器名称。如果不使用此选项，系统将广播寻找NIS服务器。

## LILO

LILO是基于Intel的机器上启动Linux的标准机制。在配置文件的此处声明`lilo`关键字以安装和配置LILO。三种配置选择是`mbr`、`partition`和`none`。这些通过`--location`选项引入。`mbr`选项将此LILO引导程序安装在磁盘的主引导记录（MBR）中，允许LILO作为磁盘上所有操作系统的引导管理器。`partition`选项指示LILO安装到根分区。在这种情况下，安装在MBR中的任何引导管理器将用于启动LILO。

安排使用备用引导程序，例如`loadlin`。最后，可以使用`--append`选项指定内核启动选项。

## 指定软件包选择

`%package`关键字允许系统管理员在安装期间指定要启用的软件包。软件包名每行一个，直到文件末尾或遇到可选的`%post`语句。除了软件包名外，还可以指定软件包组（称为组件）。可用的组件定义在Red Hat Linux CD-ROM上的，位于`RedHat/base/comps`文件中。`kickstart`安装过程将始终加载“base”组件。通过修改`RedHat/base/comps`文件，可以创建特定站点的组件。

通过在`RedHat/RPMS`目录中包含更新或额外的软件包，然后在`kickstart`配置文件的软件包（`packages`）部分中引用它们，也可以创建特定站点的发布版本。

## 安装后脚本

所有大型站点都维护着一套本地化的定制和规范。`%post`关键字引入了在安装过程结束时执行的`shell`命令，这样就就不需要手动进行这些更改。典型的安装活动示例包括配置`ntp.conf`和添加自动挂载映射。如果一组定制内容非常多，最好如前提到的，将其封装为一个软件包并包含在自定义的发行版中。

## 使用 mkickstart 自动生成 Kickstart 配置

`mkickstart`工具可以提供巨大的帮助。它能为运行该程序的系统生成一个有效的`kickstart`配置文件。对于已经运行Linux并使用`kickstart`重新安装或升级系统的安装，可以在每个系统上运行`mkickstart`，并将配置文件存储在安装服务器上。对于要安装的每种类型的硬件，手动安装一个系统并运行`mkickstart`来为该硬件生成模板。这些模板将作为自动化配置文件生成机制的一部分，该机制将在下文中描述。

## 实现系统配置（Profiles）

系统配置（Profiles）是描述系统配置的抽象原型。`kickstart`配置文件包含了构建系统的具体规则，包含许多不适用于系统配置的细节。事实上，表达系统配置所需的数据仅包含在`part`、`%package`和`%post`部分中。考虑这个用于邮件服务器的配置：

# 实现系统配置 183

| 分区 | 大小 |
| :--- | :--- |
| `/` | 100MB |
| `swap` | 256MB |
| `/tmp` | 100MB |
| `/usr` | 500MB |
| `/usr/local` | 500MB |
