
# 目录

- 替换 LVM 硬盘 ... 22
- 不同硬盘上的 LVM 示例 ... 22
- LVM 快照 ... 25

## 配置 RAID 设备

- 主板 RAID 支持：`dm` ... 26
- Linux 软件层级 ... 27
- RAID 设备和分区：`md` 和 `fd` ... 29
- 从 RAID 设备启动 ... 29
- RAID 管理：`mdadm` ... 29
- 创建和安装 RAID 设备 ... 30

- 相应的硬盘分区 ... 35
- RAID 示例 ... 36

## 31 设备和模块

- `sysfs` 文件系统：`/sys`
- `proc` 文件系统：`/proc`
- `dev`：设备文件

### udev 配置

- 设备名称和 udev 规则：`/etc/udev/rules.d`
- 符号链接
- 程序字段、`IMPORT` 键和 `/lib/udev`
- `SYMLINK` 规则

### 硬件抽象层：`HAL`

- `HAL` 守护进程和 `device-manager` (`hal-gnome`) ... 53
- `HAL` 配置：`/etc/hal/fdi` 和 `/usr/share/hal/fdi` ... 53
- 设备信息文件：`fdi` ... 54
- 属性 ... 54
- 设备信息指令 ... 56

### 手动设备

- 设备类型 ... 58
- `MAKEDEV` ... 58
- `mknod` ... 59

### 安装和管理终端与调制解器

- 串口 ... 60
- `mingetty`, `mgetty` 和 `agetty` ... 61
- `termcap` 和 `initab` 文件 ... 61
- `tset` ... 61

### 输入设备

- 安装声卡、网卡和其他卡 ... 62
