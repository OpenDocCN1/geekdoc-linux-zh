
### 描述

`Bdftopcf` 是用于 X 服务器和字体服务器的字体编译器。任何架构都可以读取可移植编译格式的字体，尽管文件结构允许特定架构无需重新格式读取。这允许在相应的机器上进行快速读取，但在其他机器上文件仍然具有移植性（尽管读取速度较慢）。

### 选项

`-pn`

设置字体字符填充。字体中的每个字符的扫描行将填充为 n 字节的倍数，其中 n 为 1, 2，4 或 8。

`-u`

设置字体扫描行单位。当字体顺序与字体顺序不同时，扫描行单位描述了要交换的数据单元（字节）；单位 i 可以是 1, 2 或 4 字节。

`-m`

将字体顺序设置为最高有效位（MSB）优先。每个字符的位将按此顺序排列；即屏幕上最左边的位将是每个单元中的最高位。

`-l`

将字体顺序设置为最低位（LSB）优先。

`-M`

将字体顺序设置为最高有效位（MSB）优先。

`-L`

将字体顺序设置为最低位（LSB）优先。

`-t`

将字体顺序设置为最低位（LSB）优先。

`-i`

将字体顺序设置为最高有效位（MSB）优先。

`-outputfile`

设置输出文件的名称。

`-v`

打印版本信息并退出。

### 作者

Keith Packard, MIT 联盟

# 另参

`X(7)`

# bdftuncate

从 BDF 生成截断的 BDF

### 概要

```
bdftuncate threshold source.bdf > destination.bdf
```

### 描述

`bdftuncate` 允许生成一个对于阈值以上的字符未编码的 BDF 字体。这通常是必要的，因为 Xlib API 和 X11 协议结构在处理稀疏字体时效率极低。

## 示例

命令

```
bdftuncate 0x3200 < 6x13t.bdf > 6x13t.bdf
```

将生成 6x13t.bdf，其中字符未编码。

# 另参

`ucs2any(1)`

### 作者

`bdftuncate` 由 Markus Kuhn 编写。Brandon Robinson 为 Debian 项目编写了此手册页。

## 名称

`bond2team` – 将绑定配置（bonding configuration）转换为团队（team）

### 概要

```
bond2team [options]
```

### 描述

`bond2team` 是一个用于将绑定选项转换为 team 尝试的工具，尽可能保留原始功能。

生成的文件默认使用 ifcfg 样式并保存在临时目录中。在转换 ifcfg 文件时，它会将绑定选项转换为 team 选项，并保留所有其他选项。在这种情况下，它会将相应的从机（slave）ifcfg 文件转换为 team 端口，同样保留它们的所有其他选项。如果从命令行给定的绑定选项进行转换，工具可以使用指定的端口作为 team 端口。

### 选项

- `--master <interface>`

指定要转换的接口名称或 ifcfg 文件。如果指定了接口名称，工具将在 `/etc/sysconfig/network-scripts/` 中查找对应的 ifcfg 文件。

- `--rename <interface>`

这是一个方便的选项，用于将原始接口名称替换为指定的名称。例如，如果 `--rename` 指定了 `bond0`，则可以使用 `--rename team0` 将最终接口名称更改为 `team0`。

- `--ifcfg`

将输出格式设置为 ifcfg 配置样式。[默认]

- `--json`

将输出格式设置为 JSON 样式。更多细节请参见 `teamd.conf(5)`。

指定要转换的绑定选项，而不是从 ifcfg 文件中读取。

- `--port <interface>`

将指定的接口设置为 team 端口。

- `--configdir <directory>`

将 ifcfg 配置路径从 `/etc/sysconfig/network-scripts` 为指定的 `<directory>`。

- `--stdout <directory>`

将输出目录设置为 `<directory>`。

- `--stdout`

将结果打印到屏幕而不是写入文件。

- `--debug`

增加调试级别。

- `--quiet`

禁止向控制台打印任何消息。

- `--version`

将工具版本信息打印到控制台并退出。

- `--help`

将帮助文本打印到控制台并退出。

- `--examples`

将常用示例打印到控制台并退出。

## 示例

将当前的 'bond0' ifcfg 配置转换为 team ifcfg：

```
# bond2team --master bond0
```

将当前的 'bond0' ifcfg 配置转换为 team ifcfg，并将接口名称重命名为 'team0'。**注意：** 可能绑定到原始接口名称的防火墙规则、别名接口等在重命名后可能会损坏，因为工具只会更改 ifcfg 文件，不会更改其他内容。

```
# bond2team --master bond0 --rename team0
```

在没有 ifcfg 的情况下转换带有端口的给定绑定参数：

```
# bond2team --bonding_opts 'mode=1 miimon=500 primary=eth1 primary_reselect=0' --port eth1 --port eth2 --port eth3 --port eth4
```

更多示例请参见选项 `--examples`。

## 注意事项

该工具不会转换任何可能绑定到当前设置的配置。例如，防火墙规则、别名接口、桥接等。

### 作者

Flavio Leitner 是该工具的原始作者。Jiri Pirko 是 libteam 的原始作者和当前维护者。

### 参见

`teamd(8)`, `teamdctl(8)`, `teamd.conf(5)`, `teamnl(8)`

## BOOTCTL

## 名称

`bootctl` - 控制固件和启动管理程序设置

### 概要

```
bootctl [OPTIONS... ]status
bootctl [OPTIONS...]update
bootctl [OPTIONS...]install
bootctl [OPTIONS...]remove
```

### 描述

`bootctl`

检查、更新、安装或删除当前系统中的引导程序。

`bootctl status` 检查并打印当前安装的引导程序二进制文件以及所有当前的 EFI 启动变量。

`bootctl update` 更新所有已安装的 systemd-boot 版本，如果版本比 EFI 系统分区中安装的版本新。这包括 `/EFI/Boot\*.efi` 中的 EFI 默认/备用 loader。如果 EFI 启动变量中没有条目，则创建一个 systemd-boot 条目。创建的条目将被添加到启动列表的末尾。

`bootctl install` 将 systemd-boot 安装到 EFI 系统分区。systemd-boot 的副本将作为 EFI 默认/备用 存储在 `/EFI/Boot\*.efi`。在 EFI 启动变量中创建一个 systemd-boot 条目并将其添加到启动列表的最顶部。

`bootctl remove` 从 EFI 系统分区中删除所有已安装的 systemd-boot 版本并从 EFI 启动变量中删除 systemd-boot。

如果没有传递命令，则隐含为 status。

### 选项

支持以下选项：

- `-h`, `--help`

打印简短的帮助文本并退出。

- `--version`

打印简短的版本字符串并退出。

- `--path`

指向 EFI 系统分区的路径。默认是 `/boot`。

- `--no-variables`

不要碰 EFI 启动变量。

## 退出状态

成功时返回 0，否则返回非零失败代码。

### 参见

引导程序规范

Systemd 引导程序接口

## 备注

1. 引导程序规范

`http://www.freedesktop.org/wiki/BootSpec`

2. Systemd 引导程序接口

`http://www.freedesktop.org/wiki/Software/Loader`

## 名称

`brtty` - Linux (Unix-like) 可刷新盲文显示器

### 概要

```
brtty [options]
```

### 描述

`brtty` 是一个后台进程（守护进程），为文本转盲文提供盲文显示器访问。它还为文本转语音提供驱动程序。

### 选项

选项可以通过以下数字方式传递给 `brtty`。从高到低为：

1. 命令行

2. 参数

3. 环境变量

4. 配置文件

5. 默认值

## 命令行

选项按顺序处理。如果指定了多次，则最后一次具有优先级。支持以下选项：

- `-a`, `--attributes=`

指向属性表的路径。相对路径相对于 `/etc/brtty`。atb 扩展为可选。

- `-b`, `--driver=`

驱动程序。默认为 auto。

- `-c`, `--contraction=`

指向收缩表的路径。相对路径相对于 `/etc/brtty`。ktb 扩展为可选。

- `-d`, `--device=`

目标设备。默认为 auto。
