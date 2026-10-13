
![](img/17f0db741e978e043c6f38c58e661452_548_0.png)

你可能听过 `insmod` 和 `rmmod` 命令。这些是旧的命令，不应该使用。`modprobe` 命令会分析内核模块的依赖关系，并加载所有模块依赖项。`insmod` 和 `rmmod` 则不具备这种功能。

## 使用特定选项加载内核模块

与其他系统中的驱动程序一样，内核模块也可以带有特定的驱动选项进行加载。如果你需要为某个模块启用特定选项，这将非常有用。使用 `modinfo` 命令加上模块名称可以查找特定模块哪些选项。在 `modinfo` 输出的末尾，你会看到一个参数列表，每个参数都以 `parse` 开头。这些就是可以使用的模块特定选项。列表 19.6 显示了其示例。

### 列表 19.6：使用 modinfo 查找模块的可用选项。

```
alias: pci:v0000086d0002A72sv=sd*bc03*ci*
alias: pci:v0000086d0002272sv=sd*bc03*ci*
alias: pci:v0000086d0002592sv=sd*bc03*ci*
alias: pci:v0000086d000258asv=sd*bc03*ci*
alias: pci:v0000086d0002582sv=sd*bc03*ci*
alias: pci:v0000086d00025772sv=sd*bc03*ci*
alias: pci:v0000086d0002358sv=sd*bc03*ci*
alias: pci:v0000086d00023582sv=sd*bc03*ci*
alias: pci:v0000086d00002562sv=sd*bc03*ci*
alias: pci:v0000086d00003577sv=sd*bc03*ci*
depends: drm,drm_helper,i2c-core,video,i2c-algo
vermagic: 2.62-320.x86_64 SMP_unload modversions
parm: modeset:int
arm: fbpercrt:int
arm: panel_ignore_3id:int
arm: powersave:int
arm: semaphores:int
arm: i915_enable_rc6:int
arm: i915_enable_fbc:int
arm: lvds_downclock:int
arm: lvds_use_ssc:int
arm: vbt_sdo_panel_type:int
arm: reset=boot
[root@hn1]#
```

遗憾的是，模块选项并没有很好的文档。通常，你可以在互联网上找到更多关于特定模块的功能。要启用特定模块功能，可以在 `/etc/modprobe.d` 目录下创建一个配置文件。文件名并不重要，只要以 `.conf` 结尾即可。内核在加载时会找到它。在该文件中，你会创建如下的行：

```
options b43 enable=0
```

在这个示例中，为 `b43` 指定了选项。更改选项后，使用 `modprobe -r` 重新加载模块。将在练习 19.4 中应用此技术。

## 练习 19.4：应用内核选项

在此练习中，你将更改 CD-ROM 的内核模块。默认情况下，软件会自动加载插入的光盘。通过更改内核模块，你可以禁用此选项。

- 在光驱中插入 CD-ROM 光盘。它会在图形界面自动加载，你会看到一个方便访问的图标。
- 使用 `modinfo cdrom`，查看命令末尾的 `auto-eject` 选项。
- 创建一个名为 `/etc/modprobe.d/cdrom.conf` 的文件，并确保内容如下：

```
options cdrom -r
```
- 执行 `modprobe -r cdrom`。你会发现因为 CD-ROM 已加载而失败。如果卸载后仍然失败，请重启电脑。（有时你需要这样做来重新加载模块）
- 如果没有重启电脑，使用 `modprobe cdrom` 加载内核模块。
- 再次插入 CD-ROM 光盘。它会自动加载。你会发现 eject 不工作。

## 升级内核

有时，红帽会发布新版本的内核。为了确保从其所有功能中受益，使用 `yum` 安装新内核是一个好主意。这不会移除旧内核。如果安装新内核后运行良好，你可以从 GRUB 菜单选择旧内核。

启动启动做了很多工作。在使用 `init` 启动服务多年后，Upstart 似乎是一个合格的继任者。然而，第一个 Linux 发行版刚刚开始将 Upstart 作为默认。当名为 systemd 的新方法开始统治世界时，在未来的几个月和几年里，systemd 将成为大多数甚至所有 Linux 发行版的标准。在此期间，作为管理员，你仍然必须处理 Upstart。

Upstart 是开发人员最重要的设计目标。旧方法是顺序执行的，花费了大量时间。Upstart 采用事件驱动的方法。在这种方法中，Upstart 进程（由 `/sbin/init` 实现）是 Linux 内核启动时第一个启动的内容。启动后，它执行几个处理所需服务的脚本。这些脚本位于 `/etc/init.d`。事件启动方法主要用于启动缓慢的桌面环境。对于服务器，启动速度的提升有限。理解正在发生什么的简单方法是查看 `/etc/initab` 文件的内容，如列表 19.7 所示。该文件用于配置红帽 Linux 的系统启动。为了方便管理员理解如何与 Upstart 工作，它包含了 Upstart 过程中使用的不同文件的提示。

### 列表 19.7：如果你想知道特定用途使用什么 Upstart 配置，请检查 /etc/initab。

```
[root@~]# cat /etc/initab
# initabb 仅供 Upstart 用于运行级别。
#
# 在此处添加其他配置对你的系统没有影响。
#
# 系统初始化由 /etc/init/rc.conf 启动。
#
# 个别运行级别由 /etc/init/rc.conf 启动。
#
# Ctrl-Alt-Delete 由 /etc/init/control-alt-delete.conf 处理。
#
# 终端 getty 由 /etc/init/tty.conf 和 /etc/init/serial.conf 处理，
# 配置位于 /etc/sysconfig/init。
#
# 关于 Upstart 事件处理器如何或
# Upstart 如何工作，请参 init(5)、init(8) 和 initctl(8)。
#
# 默认运行级别。运行级别如下：
# 0 halt（不要将 initdefault 设置为此）
# 1 单用户模式
# 2 - 多用户，不带 NFS（如果没有网络，则与 3 相同）
# 3 - 全多用户模式
# 4 - 未使用
# 5 - X11
# 6 重启（不要将 initdefault 设置为此）
id5:initdefault:
```
