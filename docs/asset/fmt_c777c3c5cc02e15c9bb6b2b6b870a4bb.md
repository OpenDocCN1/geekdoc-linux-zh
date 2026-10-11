
此基础目标配置文件具有以下选项：

- Description—这只是对目标的一个自由格式描述。
- Requires—如果此 `multi-user.target` 被激活，列出的单元也会被激活。如果列出的单元被去激活或失败，则 `multi-user.target` 将被去激活。如果存在 After 和 Before 选项，则 `multi-user.target` 和列出的目标同时激活。
- Conflicts—此设置避免了服务的冲突。启动 `multi-user.target` 会停止列出的目标和服务，反之亦然。
- After—此设置配置顺序。换句话说，它决定了启动此服务之前应该激活哪些单元。
- AllowIsolate—这是一个 yes 或 no 的布尔设置。如果是 yes，则此单元 `multi-user.target` 将与其依赖项一起激活，并且全部去激活。
- ExecStart—此命令启动服务。
- ExecReload—此命令重新加载服务。
- Alias—通过此命令，systemd 创建一个从命名单元到此 `multi-user.target` 的符号链接。

要获取更多关于这些配置文件及其选项的信息，请在命令行输入 `man systemd.service`、`man systemd.target` 和 `man systemd.unit`。

对于使用 systemd 的 Linux 服务器，一旦你理解了系统目标，启动过程现在变得更容易了。在启动时，systemd 激活去激活的 `deactivated.target` 单元。该单元被别名为 `multi-user.target` 或 `graphical.target`。因此，取决于别名，目标目标指向的服务将启动。

如果你需要帮助理解 systemd 守护进程，可以在命令行输入 `man-systemd` 以获取帮助页中各种 systemd 工具文档的列表。

## 学习系统对 SysVinit 的向后兼容

systemd 守护进程维持了对 SysVinit 守护进程的向后兼容。这允许 Linux 发行版缓慢迁移到 systemd。

虽然运行级别（runlevels）并不是 systemd 的真正组成，但 systemd 基础设施的创建是为了与运行级别的概念兼容。专门创建了 7 个目标单元配置文件以实现对 SysVinit 的向后兼容：

- `runlevel0.target`
- `runlevel1.target`
- `runlevel2.target`
- `runlevel3.target`
- `runlevel4.target`
- `runlevel5.target`
- `runlevel6.target`

正如你可能已经发现的那样，七个经典 SysV 单元中的每一个都有一个目标单元配置文件。这些目标单元配置文件通过符号链接到与原始运行级别理念最匹配的目标单元配置文件。在接下来的示例中，符号链接是用于 runlevel 目标单元的。注意，runlevel 2、3 和 4 的目标单元都链接到 `multi-user.target`。`multi-user.target` 单元类似于传统的扩展多用户模式。

```
# ls -l /lib/systemd/system/*.target

lrwxr-xr. 1 root 15 Mar 27 15:39
/lib/systemd/system/runlevel0.target -> poweroff.target

lrwxr-xr. 1 root 13 Mar 27 15:39
/lib/systemd/system/runlevel1.target -> rescue.target

lrwxr-xr. 1 root 17 Mar 27 15:39
/lib/systemd/system/runlevel2.target -> multi-user.target

lrwxr-xr. 1 root 17 Mar 27 15:39
/lib/systemd/system/runlevel3.target -> multi-user.target

lrwxr-xr. 1 root 17 Mar 27 15:39
/lib/systemd/system/runlevel4.target -> rescue.target

lrwxr-xr. 1 root 16 Mar 27 15:39
/lib/systemd/system/runlevel5.target -> graphical.target

lrwxr-xr. 1 root 13 Mar 27 15:39
/lib/systemd/system/runlevel6.target -> reboot.target
```

`/etc/initab` 文件存在，但它只包含了说明此配置不再使用的以及一些 systemd 信息。以下是使用 systemd 的 Linux 服务器上的 `/etc/initab` 示例。

```
# cat /etc/initab

# 使用 systemd 时，initab 不再使用。

#

# 在此处添加配置对系统没有影响。

#

# Ctrl-Alt-Delete 由以下处理

# /etc/systemd/ctrl-alt.target
```

### 15章：启动和停止服务

```
# systemd 使用目标代替运行级别。
# 默认情况下有两个主要目标：

# multi-user.target：类比运行级别 3
# graphical.target：类比运行级别 5

# 要设置默认目标，运行：
# ln -s /lib/systemd/system/<target name>.target
# /etc/systemd/default.target
```

`/etc/initab` 解释了如果你想要类似于经典的 3 或 5 运行级别作为你的默认运行级别，你需要从 `default.target` 单元到你选择的目标单元创建一个符号链接。要检查 `default.target` 当前链接到哪里（在旧术语中检查默认运行级别），可以使用此处所示命令。你可以看到在 Linux 服务器，服务器将在级别三启动。

```
# ls -l /etc/systemd/system/default.target

lrwxr-wx. 1 root root 36 Mar 13 17:27
/etc/systemd/system/default.target ->
/lib/systemd/system/runlevel3.target
```

使用 `init` 或 `telinit` 命令切换运行级别的能力仍然可用。执行时，每个命令都会被转换为 systemd 单元激活请求。因此，在命令行输入 `init 3` 实际上执行的是 `systemctl isolate multi-user.target` 命令。此外，你仍然可以使用 `runlevel` 命令来确定当前级别，但不建议这样做。

## 检查服务的状态

作为一名 Linux 管理员，你需要检查服务器上提供的各种服务的状态。出于安全考虑，你应该通过该过程禁用并移除任何发现的未使用的系统。对于故障排除而言，最重要的是，你需要能够快速知道 Linux 服务器上应该运行和不应该运行的内容。

# 第四部分：成为 Linux 管理员

当然，了解 Linux 服务器正在使用哪些初始化服务是获取的第一条信息。为了确定这些内容在本章的“理解初始化守护进程”部分是如何涵盖的，本节的其余部分将由各种初始化守护进程的子章节组成。

## 检查 SysInit 系统的服务

要查看 Linux SysInit 守护进程提供的所有服务，请使用 `chconfig` 命令。下面的示例显示了经典 SysInit Linux 服务器上可用的服务。注意，每个运行级别（0–6）都会显示每个服务，状态为 on（开启）或 off（关闭）。状态表示特定服务是否已启动（on）或未启动（对应运行级别）。

```
# chconfig --list

ConsoleKit 0:off 1:off 2:off 3:on 4:on 5:on 6:off

NetworkManager 0:off 1:off 2:off 3:off 4:off 5:off 6:off
  crond 0:off 1:off 2:on 3:on 4:on 5:on 6:off
  cups 0:off 1:off 2:off 3:on 4:on 5:on 6:off
  sshd 0:off 1:off 2:on 3:on 4:on 5:on 6:off
  syslog 0:off 1:off 2:on 3:on 4:on 5:on 6:off
  tux 0:off 1:off 2:off 3:off 4:off 5:off 6:off
  udev-post 0:off 1:off 2:off 3:on 4:on 5:on 6:off
  vncserver 0:off 1:off 2:off 3:off 4:off 5:off 6:off
  winbind 0:off 1:off 2:off 3:off 4:off 5:off 6:off
```
