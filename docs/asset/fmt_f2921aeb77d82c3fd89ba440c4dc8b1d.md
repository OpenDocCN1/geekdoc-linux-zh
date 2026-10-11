
- 对于 `systemd`，此处显示的相同结果意味着 `sshd` 已转换为 `systemd`：

```bash
# systemctl status sshd.service

sshd.service - OpenSSH server daemon

Loaded: loaded (/lib/systemd/system/sshd.service; enabled)

Active: active (running) since Mon, 30 Apr 2015 12:35:20...
```

# 附录 B：练习答案

- 如果前面的测试没有相同结果，请为 `SysVinit` 进程尝试以下命令。如果此处有结果而前面的测试为负结果，则 `sshd` 仍在使用 `SysVinit` 守护进程。

```bash
# service ssh status

sshd (pid 2390) is running...
```

### 3. 要确定服务器的上一个当前运行级别，使用 `runlevel` 命令。它适用于所有 init 守护进程：

```bash
$ runlevel

n 3
```

### 4. 要更改你 Linux 服务器上的默认运行级别或目标单元，可以执行以下操作之一（取决于服务器的 init 守护进程）：

- 对于 `SysVinit` init 守护进程，编辑 `/etc/inittab` 并将 `id:#initdefault:` 行中的 `#` 更改为 2、3、4 或 5。
- 对于 `Upstart` init，编辑 `/etc/inittab` 并将 `id:#initdefault:` 行中的 `#` 更改为 2、3、4 或 5。
- 对于 `systemd`，将 `default.target` 符号链接更改为所需的 `runlevel3.target`，其中 `#` 为 2、3、4 或 5。以下显示了如何更改目标为 `runlevel3.target` 的符号链接。

```bash
# ln -sf /lib/systemd/system/runlevel3.target
/etc/systemd/system/default.target
/lib/systemd/system/runlevel3.target
```

### 5. 要列出你服务器上的服务（运行中或活动），你需要根据你使用的 init 守护进程使用不同的命令。

- 对于 `SysVinit` 守护进程，使用示例所示的 `service` 命令：

```bash
# service --status-all | grep running... | sort

anacron (pid 2162) is running...
atd (pid 2172) is running...
...
```

- 对于 `Upstart` 守护进程，使用 `initctl` 命令。然而，务必使用 `service` 命令，因为并非所有服务都已迁移到 `Upstart`：

```bash
# initctl list | grep start/running

tty (/dev/tty3) start/running, process 1163
```

## 第六部分：附录

- 对于 `systemd`，使用 `systemctl` 命令，如下：

```bash
# systemctl list-unit-files --type=service | grep -v disabled

UNIT FILE STATE
abrtt-ccpp.service enabled
abrtt-oops.service enabled
...
```

- 6 要列出你的 Linux 服务器上运行（或活动）的服务，请使用答案 5 中根据你服务器正在使用的 init 守护进程确定的相应命令。

- 7 对于每个 init 守护进程，命令将显示特定服务的当前状态：

  - 对于 `SysInit` 守护进程，使用 `service service_name status` 命令。
  - 对于 `Upstart` init 守护进程，使用 `initctl status service_name` 命令。
  - 对于 `systemd`，使用 `systemctl status service_name` 命令。

- 8 要显示你的 Linux 服务器上 `cups` 守护进程的状态，请使用以下操作：

  - 对于 `SysInit` 守护进程：

```bash
# service cups status

cupsd (pid 8236) is running...
```

  - 对于 `Upstart` init 守护进程：

```bash
# initctl status cups

cups start/running, process 2390
```

记住，如果某个服务尚未迁移到 `Upstart`，你将需要使用 `systemd` 命令而不是 `initctl`。

  - 对于 `systemd`：

```bash
# systemctl status cups.service

cups.service - CUPS Printing Service
Loaded: loaded (/lib/systemd/system/cups.service; enabled)
Active: active (running) since Tue, 01 May 2015 04:43:5...
Main PID: 17003 (cuped)
CGroup: system=/system/cups.service
17003 /usr/sbin/cups -f
```

- 9 要尝试重启你的 Linux 服务器上的 `cups` 守护进程，请使用以下操作：

  - 对于 `SysInit` 守护进程：

```bash
# service cups restart

Stopping cups: [ OK ]
Starting cups: [ OK ]
```

  - 对于 `Upstart` init 守护进程：

```bash
# initctl restart cups

cups start/running, process 2490
```

- 附录 B：练习题答案

记住，如果某个服务尚未迁移到 `Upstart`，你将需要使用 `service` 命令而不是 `initctl`。

  - 对于 `systemd`：

```bash
# systemctl restart cups.service
```

- 10. 要尝试重新加载你的 Linux 服务器上的 `cups` 守护进程，请使用以下操作：

  - 对于 `SysVinit` 守护进程：

```bash
# service cups reload

Reloading cups: [ OK ]
```

  - 对于 `Upstart` init 守护进程：

```bash
# initctl reload cups
```

记住，如果某个服务尚未迁移到 `Upstart`，你将需要使用 `service` 命令而不是 `initctl`。

  - 对于 `systemd`，这是一个陷阱。你无法在 `systemd` Linux 系统上重新加载 `cups` 守护进程！

```bash
# systemctl reload cups.service
```
Failed to issue method call: Job type reload is not applicable for any cups service.

## 第 16 章：配置打印服务器

对于涉及打印机的问题，大多数情况下你可以使用图形界面或命令行工具。关键在于确保你获得了后续答案中所示的结果。这里的答案结合了图形界面和命令行解决练习的方法。（看到 `#` 提示符时切换到 `root` 用户。）

- 1. 要使用打印机配置窗口向你的系统添加新打印机（通用 Ghostscript 打印机，连接到端口），在 Fedora 16 中执行以下操作：

  - a. 从 GNOME 3 桌面，选择 Applications（应用程序）➤ Printing（打印）。
  - b. 选择 Add（添加）按钮（如果提示，输入 `root` 密码）。
  - c. 选择串口、LPT或其他端口作为设备并点击 Forward（下一步）。
  - d. 对于打印机，选择 Generic（通用）并点击 Forward；然后选择 PostScript 打印机并点击 Forward。
  - e. 点击 Forward 跳过任何可安装选项。
  - f. 打印机名称命名为 `myprinter`，提供任何你喜欢的 Description（描述）和 Location（位置），并点击 Apply（应用）。
  - g. 点击 No（否），不打印测试页。打印机应该出现在打印机配置窗口中。

- 2. 要使用 `lpc` 命令查看所有打印机的状态，输入以下内容：

```bash
# lpc status

myprinter:
  queuing is enabled
  printing is enabled
  no entries
  daemon present
```
