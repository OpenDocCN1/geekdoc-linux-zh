
![](img/2eff90170b8c94cce3a908ab927e38c2_246_0.png)

## 重启与关机

要从命令行关闭或重启系统，可以使用 `systemctl` 命令。

`systemctl poweroff` 停止所有正在运行的服务，卸载所有文件系统（在无法卸载时将其重新挂载为只读），并关闭系统。

`systemctl reboot` 命令停止所有正在运行的服务，卸载所有文件系统并重启系统。

您也可以使用较短版本的命令 `poweroff` 和 `reboot`，它们是其 `systemctl` 等效命令的符号链接。

> `systemctl halt` 和 `halt` 命令也可用以停止系统；与 `poweroff` 命令不同，它们不会关闭电源。

## 选择 systemd 目标

systemd 目标是系统为了达到所需状态应该激活的一组单元。下表列出了重要的目标。

### 常用目标

| 目标 | 目的 |
|---|---|
| `graphical.target` | 支持多用户、图形界面登录。 |
| `multi-user.target` | 支持多用户，仅限文本登录。 |
| `rescue.target` | 救援模式，初始化完成。 |
| `emergency.target` | 紧急模式，initramfs 切换完成且系统只读挂载。 |

目标可以是另一个目标的一部分。例如，`graphical.target` 包含了 `multi-user.target`。可以通过此命令查看这些依赖关系：

```
$host ~]$ systemctl-dependencies graphical.target | grep target
* multi-user.target
  * paths.target
  * slices.target
  * sockets.target
  * sysinit.target
  * cryptsetup.target
```

## 控制启动过程

```
--integritysetup.target
--local-fs.target
...
```

要列出可用目标，使用以下命令：

```
[user@ ~]$ systemctl list-units --type=target --all
UNIT                               LOAD ACTIVE SUB DESCRIPTION
basic.target                        loaded active active Basic System
...
cloud-config.target                loaded active active Cloud-config
cloud-init.target                  loaded active active Cloud-init target
cryptsetup-preset.target          loaded inactive dead
cryptsetup.target                   loaded active active Local Enc Volumes
```

## 运行时选择目标

在运行的系统中，管理员可以使用 `systemctl isolate` 命令切换到不同的目标。

```
[root@ ~]$ systemctl isolate multi-user.target
```

隔离目标会停止该目标及其依赖项不需要的服务，并启动任何未启动运行的服务。并非所有目标都可以隔离。您只能隔离单元文件中带有 `AllowIsolate=yes` 的目标。例如，您可以隔离 `graphical.target`，但不能隔离 `cryptsetup.target`。

```
[user@ ~]$ systemctl cat graphical.target
# /usr/lib/systemd/system/graphical.target
...output...
[Unit]
Description=Graphical Interface
Documentation=man:systemd.spec(7)
Requires=multi-user.target
Wants=display-manager.service
Conflicts=rescue.target rescue.target
After=multi-user.target rescue.target rescue.target display-manager.service
AllowIsolate=yes
[user@ ~]$ systemctl cat cryptsetup.target
# /usr/lib/systemd/system/cryptsetup.target
...output...
[Unit]
Description=Local Encrypted Volumes
Documentation=man:systemd.spec(7)
```

## 设置默认目标

当系统启动时，systemd 会激活 `default.target` 目标。通常 `/etc/systemd/system/` 中的默认目标是指向 `graphical.target` 或的符号链接。

`multi-user.target`。无需手动编辑此符号链接，`systemctl` 命令提供了两个子命令来管理此链接：`get-default` 和 `set-default`。

```
[root@#] systemctl get-default
multi-user.target
[root@#] systemctl set-default graphical.target
Removed symlink /etc/systemd/etc/systemd/default.target -> /usr/lib/systemd/system/
graphical.target.
[root@#] systemctl get-default
graphical.target
```

# 在启动时选择不同的 Target

若要在启动时选择不同的 target，请从引导加载程序的内核命令行中添加 `systemd.unit=target.target` 选项。

例如，为了将系统引导到救援 shell（其中你可以在没有服务运行的情况下更改系统配置），请从引导加载程序的内核命令行中添加以下选项：

```
systemd.unit=rescue.target
```

此配置更改仅影响单次启动，因此是排除启动故障的有用工具。

要使用此方法选择不同的 target，请遵循以下步骤：

- 1. 启动或重启系统。
- 2. 按任意键中断引导加载器菜单倒计时（回车键将启动正常启动）。
- 3. 将光标移动到你想启动的内核条目。
- 4. 按 `e` 编辑当前条目。
- 5. 将光标移动到以 Linux 开头的行。此行即内核命令行。
- 6. 附加 `systemd.unit=target.target`。例如：`systemd.unit=emergency.target`。
- 7. 按 `Ctrl+x` 使用这些更改启动。

## 参考文献

`bootup(7)`, `dracut.bootup(7)`, `lsinitrd(!)`, `systemd.target(5)`, `systemd.special(7)`, `sulogin(8)`, 以及 `systemctl(!)` 手册页

欲了解更多信息，请参阅《配置基础系统服务指南》中的“使用 systemd 管理服务”章节，地址：

`https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/configuring_basic_system_settings/index#managing-services-with-systemd`

## 引导练习

# 选择启动 Target

在本次练习中，你将确定系统引导的默认 target，并将系统引导到其他 target。

## 预期结果

- 更新系统默认 target 并从引导加载程序使用临时 target。

## 准备工作

作为工作站机器上的学生，使用 `lab` 命令为本次练习准备系统。

此命令可确保所有所需的资源都是可用的。

```
[student]@workstation ~$ lab start boot-selecting
```

## 指令

- 1. 在工作站机器上，打开终端并确认默认 target 为 graphical-target。

```
[student]@workstation ~$ systemctl get-default
graphical.target
```

- 2. 在工作站机器上，无需重启即可手动切换到 multi-user target。使用 `sudo` 命令，如果系统提示，请使用 `student` 作为密码。
