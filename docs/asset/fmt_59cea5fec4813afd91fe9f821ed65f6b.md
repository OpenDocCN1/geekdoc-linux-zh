
# 列表 13.2 AIsysconfig.ksh shell 脚本列表。（续）

正如列表 13.2 所示，我们在该 shell 脚本中有一个函数列表。在创建这些函数时，我尝试按照我想在 shell 脚本中执行的顺序来放置每一个函数。只要你不在函数定义之前使用它，这种做法并不是必要的。因为 Korn shell 是解释执行的，而不是编译的，所以执行流是从上到部的。因此，在代码中使用函数的上方定义该函数是有合逻辑的。如果我们不小心将函数定义在用用它的位置下方，那么我们可能会收到错误消息，也可能不会。是否收到错误消息取决于函数的预期功能以及函数在 shell 脚本中是如何执行的。

从列表 13.2 shell 脚本的开始，我们首先定义了需要的变量。机器的主机名总是有用的，而且在报告文件的定义以及报告本身中都是必需。接下来，我们创建一个日期/时间戳。这个 `$DATETIME` 变量也用于报告文件的定义。我们需要日期和时间，因为此脚本可能会在一天内被执行多次。我们定义了工作目录。我喜欢使用 `/usr/local/reboot`，但你可以使用任何你目录。最后，我们定义了报告文件，并将其分配给 `$SYSINFO_FILE`。

下一部分是定义所有函数的地方。注意，其中一些函数只包含一条命令，而另一些则有更多代码。在像这样的 shell 脚本中，将每个命令放在单独的函数中是一个好主意。使用这种方法允许你通过简单更改命令来适配不同的操作系统，而保持基础 shell 脚本不变。这个 shell 脚本中的函数太多，无法逐一介绍，但该脚本的输出显示在列表 13.3 中。有关 AIX 命令的详细信息，请参考 AIX 文档和 AIX 系统上的 man 页面。

在 `START OF MAIN` 处，我们开始执行实际工作。第一步是确保操作系统是 AIX。如果 shell 脚本在其他 Unix 变体上执行，许多命令将失败。如果检测到非 AIX Unix 变体，用户将收到错误消息并带返回代码 1 退出。其中一个测试是检查 `$WORKDIR` 目录是否存在，在该 shell 脚本中被定义为 `/usr/local/reboot`。如果目录不存在，将尝试创建该目录。并不是所有用户都有权限在此创建目录。如果创建失败，用户将收到错误消息，并被手动创建目录后运行 shell 脚本。

如果操作系统是 AIX 且 `$WORKDIR` 存在，我们就创建报告并开始生成报告。注意，报告的所有函数和命令列表都包含在大括号 `{ }` 中。然后，在 shell 脚本末尾最后一个大括号之后，所有输出都管道到 `tee -a` 命令。通过此管道到 `tee-a` 命令，允许用户在生成报告的同时看到它，同时输出被写入大括号，为了让输出显示在屏幕和报告文件中花费了很大精力。基本语法所示。

```bash
{
report command
report command
report command
} | tee -a $SYSINFO_FILE
```

在括号内，我们首先设置报告表头信息，包括主机名、时区、实际内存、机器类型、操作系统、操作系统版本以及操作系统版本的维护级别补丁。

当表头完成后，脚本将执行此处 `DEFINE FUNCTIONS` 部分中列出的函数。正如我之前提到的，我尝试按照执行顺序来定义函数。在每个函数执行之前，会写入一行井号以隔开每个报告部分，然后为特定任务写入某些部分标题。在最后，紧接结束大括号之前，会向用户显示报告文件名，以指示报告文件的位置。

让我们看看列表 13.3 中的简略输出。

```
AIsysconfig.ksh - Jul 25 09:46:58 EDT 2022
Saving system information...
System: AIX
Time Zone: EST
Real Memory: 131072KB
Machine Type: powerpc
Operating System: AIX
OS Version: 5.1.0.0
Current OS Maintenance Level:
Not all filesets for 5.0.0.0_AIX were found.
Not all filesets for 5.1.0.0_AIX were found.
############################################
### Installed and Configured Devices
| Name | Status | Description |
| :--- | :--- | :--- |
| sys0 | Available | 00-00 System |
| sysplan0 | Available | 00-00 Planar |
| ioplan0 | Available | 00-00 I/O |
| io0 | Available | 00-00 Planar |
| hdisk0 | Available | 00-00-S-00, 2.0 GB SCSI Drive |
| hdisk1 | Available | 00-00-S-01, 2.0 GB SCSI Drive |
| rmt0 | Available | 00-00-S-05, 5.0 GB Tape Drive |
| cd0 | Available | 00-00-S-06, Multimedia-ROM Drive |
| proc0 | Available | 00-00 Processor |
| mem0 | Available | 00A 32 MB SIMM |
| mem1 | Available | 00B 32 MB SIMM |
| mem2 | Available | 00C 32 MB SIMM |
| mem3 | Available | 00D 32 MB SIMM |
| fd0 | Available | 00-00-D-00 Diskette Drive |
| vdd | Available | LVM Driver |
| tty0 | Available | 00-00-S1-00 Asynchronous Terminal |
| rootvg | Defined | Volume group |
| hd5 | Defined | Logical volume |
| hd6 | Defined | Logical volume |
Listing 13.3 AIsysconfig.ksh shell script in action. (续)
############################################
### Long Device /dev
| Permissions | Links | Owner | Group | Size | Time | Name |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| crw-rw-rw | 1 | root | system | 19, | Jun 23 15:23 | rmt0 |
| crw-rw-rw | 1 | root | system | 19, | Mar 29 13:49 | rmt0.1 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.2 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.3 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.4 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.5 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.6 |
| crw-rw-rw | 1 | root | system | 19, | Jul 26 2021 | rmt0.7 |
| crw-rw------ | 1 | root | system | 10, | Jul 26 2021 | rootvg |
| crw-rw------ | 1 | root | system | 10, | Jul 29 2021 | scripts_lv |
| crw-rw-rw | 1 | root | system | 13, | Jul 26 2021 | sad |
| crw-rw-rw | 1 | root | system | 10, | Jul 26 2021 | scripts_lv |
| crw-rw-rw | 1 | root | system | 11, | Jul 26 2021 | scsi10 |
| crw-rw-rw | 1 | root | system | 13, | Jul 26 2021 | slog |
| crw-rw-rw | 1 | root | system | 13, | Jul 26 2021 | spx
```
