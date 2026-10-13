
# 为 super 编写脚本

在为 `super` 编写脚本时要极度小心。当以 `setuid-root` 身份运行时，许多命令可能会被用于恶意目的。确保脚本仅完成绝对必要的任务，并仔细规定用户可能的副作用和替代用途。始终检查脚本的副作用和替代用途。

## 编写 super 脚本

编写一个脚本，允许用户将文件移动到受限目录 `/usr/management/docs`。该脚本还应更改文件组为 `manage`，更改文件权限以允许组成员完全的读取、写入和执行权限，并拒绝文件所有者和其他用户的所有权限。

## 问题

1. 在给出的文件（`/etc/sudoers`）中，用户 `user` 拥有哪些权限？
2. 使用 `super`，可以对 `sudo` 未提供的命令进行哪些限制？

## 回答

1. 用户可以运行 `SHUTDOWN` 别名中的命令，在服务器上运行 `/etc/reboot`，以及在 `HUB` 机器上运行 `SHELLS` 别名之外的任何命令。

2. `super` 允许管理员设置命令的时间，以及可以发布命令的精确机器。它还提供了脚本，允许非信任用户在没有 `root` 权限的情况下执行 `root` 任务。

# 高级问题

1. 系统管理员有三个用户：`joe`、`john` 和 `mary`。他创建了一个名为 `ALL` 的别名，包含 `joe` 和 `mary`。然后他将 `SHUTDOWN` 命令别限制限制用户别名 `ALL`。谁能够执行 `SHUTDOWN` 别名命令？为什么？

# 实验 XVI 加固 LILO 启动器

## 目的

本实验目的是防止攻击者通过重启获取系统的访问。首先，将修改并移除 `CTRL-ALT-DEL` 重启命令。然后，提高 Linux 加载器 `LILO` 启动器和基本输入输出系统 `BIOS` 抵御此类攻击的安全性。

## 理论

攻击者获取系统权限最简单的方法之一是以单用户模式启动计算机。网络上的大多数系统如果由于任何原因关闭，会自动重启；单用户模式通常默认授予 `root` 权限。本实验提供了几种防止此类攻击的方法。

## 移除 CTRL-ALT-DEL 重启

与此类攻击相关的一个系统弱点是 `CTRL-ALT-DEL` 功能。通常，此命令被设置为重启系统，为攻击者提供了以单用户模式启动计算机的机会。

`CTRL-ALT-DEL` 定义在 `/etc/inittab` 文件中。它通常设置为在所有三个键都被按下时运行 `shutdown`，但此文件可以设置为运行任何程序或命令。该命令将类似于：

```
ca:crtaltdel:/sbin/shutdown -t5 -r now
```

此行指令计算机运行 `shutdown`，在发送进程、警告和杀死信号之间等待五秒，在关机后重启，并规定何时执行所有操作。

为了防止这一点，请从 `/etc/inittab` 文件中删除上一行。这样 `CTRL-ALT-DEL` 在系统上将不再具有功能。

### 示例 INITTAB 文件

```
# 运行级别
id:2:initdefault
```

```
# 其他操作之前的系统初始化。
si:sysinit:/etc/rc.d/bcheckrc
```

```
# 运行级别 0,6 是停止和重启，1 是维护模式。
10:0:wait:/etc/rc.d/rc.halt
11:1:wait:/etc/rc.d/rc.single
12:2345:wait:/etc/rc.d/rc.multi
16:6:wait:/etc/rc.d/rc.reboot
```

```
# 执行“三指礼”时执行的操作
ca:crtaltdel:/sbin/shutdown -t -rf now
```

```
# 运行级别 2&3：控制台上的 getty，级别 3 也在调制解调器端口上也有 getty。
1:23:respawn:/sbin/getty tty1 VC linux
2:23:respawn:/sbin/getty tty2 VC linux
3:23:respawn:/sbin/getty tty3 VC linux
4:23:respawn:/sbin/getty tty4 VC linux
S2:3:respawn:/sbin/ugetty tty2 M19200
```

## 加固 lilo.conf 文件

`lilo.conf` 是 `LILO` 启动器的配置文件。它管理不同操作系统的启动和参数。

### 示例 LILO.CONF 文件

```
boot = /dev/hda
delay = 40
compact
vga = normal
```

```
root = /dev/hda1
read-only
image = /zImage-2.5.99
label = try
image = /zImage-1.0.9
label = 1.0.9
image = /tamu/vmlinuz
label = tamu
root = /dev/hda2
vga = ask
other = /dev/hda3
label = dos
table = /dev/hda
```

### LILO.CONF 选项说明

- `Boot`: 建立引导引导区的设备名称。
- `Map`: 设置映射文件的位置。
- `Install`: 将文件安装为新的引导扇区。
- `Timeout`: 设置 `LILO` 等待键盘输入的时间。
- `Prompt`: 在启动提示符处要求用户输入。
- `Default`: 指定默认镜像。
- `Delay`: 指定 `LILO` 在启动第一个镜像之前等待的时期（以十分之一秒为单位）。
- `Compact`: 尝试将相邻扇区的读取请求合并为单个请求。
- `Vga`: 指定启动时选择的 `VGA` 文本模式。
- `Normal`: 80x25 文本模式。
- `Extended`: 80x50 文本模式。
- `Ask`: 在启动时请求用户输入。
- `Root`: 指定应挂载为根的设备。
- `read-only`: 将根文件监控为只读。
- `image`: 指定带有 Linux 内核启动镜像的文件或设备。
- `label`: 镜像的引用名称。
- `other`: 指定要启动的任意系统。
- `table`: 指定扇区。

### 示例 LILO.CONF 文件

```
boot = /dev/hda
delay = 40
compact
vga = normal
```

```
root = /dev/hda1
read-only
image = /zImage-2.5.99
label = try
image = /zImage-1.0.9
label = 1.0.9
image = /tamu/vmlinuz
label = tamu
root = /dev/hda2
vga = ask
other = /dev/hda3
label = dos
table = /dev/hda
```

### LILO.CONF 选项说明

- `Boot`: 建立引导引导区的设备名称。
- `Map`: 设置映射文件的位置。
- `Install`: 将文件安装为新的引导扇区。
- `Timeout`: 设置 `LILO` 等待键盘输入的时间。
- `Prompt`: 在启动提示符处要求用户输入。
- `Default`: 指定默认镜像。
- `Delay`: 指定 `LILO` 在启动第一个镜像之前等待的时期（以十分之一秒为单位）。
- `Compact`: 尝试将相邻扇区的读取请求合并为单个请求。
- `Vga`: 指定启动时选择的 `VGA` 文本模式。
- `Normal`: 80x25 文本模式。
- `Extended`: 80x50 文本模式。
- `Ask`: 在启动时请求用户输入。
- `Root`: 指定应挂载为根的设备。
- `read-only`: 将根文件监控为只读。
- `image`: 指定带有 Linux 内核启动镜像的文件或设备。
- `label`: 镜像的引用名称。
- `other`: 指定要启动的任意系统。
- `table`: 指定扇区。
