
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```

[/content]

Wait that's example. Need actual processing.

Let's redo properly.

[content]
- `chkconfig` - 用于配置在运行级别启动的守护进程。

- `cron` - 根据 crontabs 信息定期执行命令的系统服务。

- `crontab (cron table)` - 指定由 cron 守护进程运行的命令的文件。

- `crontab` 命令 - 用于查看和编辑用户 cron 表。

- `daemon process` - 不与终端关联系统进程。

- `dmesg` 命令 - 用于查看 `/var/log/messages` 的内容。

- `fg` 命令 - 将后台进程移动到前台。

- `foreground process` - 在终端中运行的进程。

- `getty` - 在基于字符的终端上显示登录提示的程序。

- `Grand Unified Bootloader (GRUB)` - SLES 的默认引导加载程序。

- `grub` 命令 - 用于在后台启动进程。

- `grub-install` - 用于安装 GRUB。

- `halt` 命令 - 用于将系统带入级别0。

- `hwinfo` - 用于显示硬件信息。

- `init` - 内核启动期间启动的第一个进程。

- `Initial RAM File System (initramfs)` - 存储驱动的小内存磁盘。

- `inserv` - 用于启用启动设备的脚本。

- `iostat` - 用于显示输入输出统计数据。

- `job ID` - 给进程的 ID。

- `jobs` 命令 - 用于查看后台进程。

- `kernel ring buffer` - 存储内核消息的内存区域。

- `kill` 命令 - 通过 PID 发送信号。

- `killall` 命令 - 按名发送信号。

- `lilo` 命令 - 安装 LILO 配置。

- `logrotate` 命令 - 用于归档日志文件。

- `Master Boot Record (MBR)` - 存储分区表和活动分区位置的硬盘区域。

- `mkinitrd` - 用于创建初始 RAM 系统。

- `netstat` 命令 - 显示网络接口和端口统计数据。

- `nice` 命令 - 用于在进程启动时更改其优先级。

- `nice value` - 代表进程的优先级。较高的 nice 值会降低进程的优先级。

- `parent process` - 启动另一个进程的进程。

- `Parent Process ID (PPID)` - 父进程的 PID。

- `poweroff` 命令 - 用于快速将系统带入运行级别 0 并关闭系统。

- `process` - 当前加载到内存并在 CPU 上运行的程序。

- `Process ID (PID)` - 分配每个进程的唯一标识符。

- `program` - 可执行以创建进程的文件。

- `ps (process status)` 命令 - 用于列出系统上运行的进程。

- `pstree` 命令 - 用于列出系统上运行的进程及其父子关系。

- `reboot` 命令 - 用于快速将系统带入运行级别 6。

- `renice` 命令 - 用于更改运行进程的优先级。

- `runlevel` - Linux 系统上守护进程数量和类型的类别。

- `runlevel` 命令 - 用于显示当前和最近的运行级别。

- `sar (system activity reporter)` 命令 - 显示系统区域的性能统计数据。

- `shutdown` 命令 - 用于在特定时间切换到运行级别 0。

- `signal-controlled daemon` - 在系统发生事件时启动的守护进程。

- `sologin` - 在运行级别 1 的字符终端上仅为 root 用户显示登录提示的程序。

- `sysctl` 命令 - 用于查看和配置 `/proc` 目录中的参数。

`syslog-ng` – `syslogd` 进程的替代品，具有更好的消息过滤能力和守护进程支持。它代表新一代系统日志守护进程（System Log Daemon）。

`syslog` – 负责 Linux 系统大部分日志记录的进程。它代表系统日志守护进程（System Log Daemon）。

`telinit` 命令 – `init` 命令的快捷方式。

`top` 命令 – 用于查看、调整优先级并杀死系统中占用最多 CPU 时间的进程。

`uname` 命令 – 显示系统架构和名称信息。

`uptime` 命令 – 显示系统运行时间和负载统计。

`user` 进程 – 由用户启动并运行在终端上的进程。

`vmstat` 命令 – 显示系统使用和虚拟内存统计数据。

`xosview` 命令 – 在图形桌面环境中显示关键系统使用统计数据。

### 章节练习

## 练习 5-1 管理 Linux 进程

在此练习中，你将练习启动和停止进程以及更改优先级。

在练习的第一部分，你将启动并挂起 `gcaltool`，将其移动到后台和前台，然后停止它。

在第二部分，你将启动 `gcaltool` 并将运行程序的优先级设置为 `nice` 值 `-5`。然后你将启动一个 `nice` 值为 `10` 的 `xeyes`。

### 完成练习的详细步骤

- 第一部分：将进程移动到后台
- 第二部分：修改进程优先级

## 第一部分：将进程移动到后台

要将进程移动到后台和前台，请执行以下操作：

1. 如必要，以用户 `geeko` 身份使用密码 `novel` 登录你的 `da-host` 工作站。

2. 打开终端窗口并使用密码 `novel` 通过 `su -` 切换到 `root`。

3. 在命令行中，输入以下命令显示当前由 `geeko` 拥有的进程

```
ps -LU geeko
```

注意是小写的 `L`。

4. 输入以下命令显示当前由 `root` 拥有的进程

```
ps -U root
```

注意是小写的 `L`。

5. 在 shell 提示符输入 `gcaltool` 启动 Gnome 计算器程序。

注意，终端无法接收新命令，因为没有显示新行符。这是因为计算器程序正在前台运行。

6. 调整计算器窗口和终端窗口，使你能同时看到它们，然后选择终端窗口以激活它。

7. 按 `Ctrl+z` 挂起计算器程序。

8. 尝试使用计算器工具计算几个数字。

由于其进程被挂起，计算器没有响应。

9. 输入以下命令查看后台作业

```
jobs
```

你应该能看到 `gcaltool` 任务处于停止状态。

10. 输入以下命令查看从当前终端运行的 `gcaltool` 进程

```
ps -l
```

注意是小写的 `L`。

该进程状态为 `T`，表示它正在被追踪或停止。

11. 输入 `bg 1` 恢复在后台运行的计算器程序。

注意计算器程序再次开始运行。由于它在后台运行，你现在可以使用终端窗口输入其他命令。

12. 输入 `jobs` 验证作业状态为正在运行。

你应该能看到 `gcaltool` 任务现在正在运行。

13. 通过 `pstree -p | grep gcaltool` 查看进程树中的 `gcaltool` 分支。

注意 `gcaltool` 进程列在树的末端。

14. 输入 `fg 1` 将 `gcaltool` 进程带回前台。

15. 关闭计算器程序。

16. 输入 `nohup gcaltool&` 在后台启动计算器。

> 注意：`nohup` 命令运行命令的方式使其忽略任何发送给它的挂断信号（hangup kill signals）。

17. 关闭终端窗口。

计算器程序保持运行。

18. 打开一个新的终端窗口。

19. 输入 `top` 启动 `top` 程序。

20. 输入 `u` 然后输入 `root`，仅查看由 `root` 启动的进程。

21. 检查 `top` 中列出的计算器程序 (`gcaltool`)。

22. （条件性）如果你找不到 `gcaltool` 程序，请最大化终端窗口。你也可以激活计算器窗口并用它计算几个数字。这应该导致 `gcaltool` 进程移动到 `top` 输出的顶部。

你可以在 `top` 中输入 `F` 并选择 `PID` 为排序列。如果需要，还可以通过按 `R` 来反转排序顺序。

23. 记录 `gcaltool` 进程的 `PID`：

24. 输入 `q` 退出 `top`。

25. 输入 `ps PID_of_gcalctool_process` 查看关于 `gcaltool` 进程的信息。

26. 使用 `su -` 命令和密码 `novell` 切换到你的 `root` 用户。

27. 输入以下命令停止计算器程序并检查状态：

```
kill PID_of_gcaltool
ps aux | grep gcalctool
```

28. 输入 `xeyes&` 在后台启动 `xeyes` 程序。

29. 输入 `killall xeyes` 杀死 `xeyes` 程序。

## 第二部分：修改进程优先级

要修改进程优先级，请执行以下操作：

1. 在 shell 提示符输入 `exit` 切换回你的 `gecko` 用户。

2. 输入 `gcaltool&` 在后台启动 `gcaltool` 程序。

3. 记录 `gcaltool` 的 `PID`（显示在...）
