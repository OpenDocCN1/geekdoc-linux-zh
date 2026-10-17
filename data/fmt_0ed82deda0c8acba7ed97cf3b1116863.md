
```text
MON> log
INFO:CPU0:MON:[20:16:31 10/1/2001 GMT] VPAR Monitor version 0.2 started
INFO:CPU0:MON:Version string: @(#) $Revision: vpmong:
  vw: -- selectors: CUP
  11.11_BL2001_0616            'cup_cvinod_vpar_ncf_trial'
  'cup_Shepf_r11.11'   Tue Sep 25 18:2
  L12 PGT 2001: $INFO:CPU0:MON:Partition uhnj1vp1 monarch set to 37
INFO:CPU0:MON:Partition uhnj1vp2 monarch set to 45
```

## ls directory

类似于 UNIX 的 `ls` 命令，列出一个目录的内容。在撰写本文时，*目录* 必须是 HFS 格式。默认使用 `/stand` 目录。你还可以添加 `-a` 以列出所有条目，`-l` 以显示长格式列表，`-n` 以显示数字条目，`-i` 以显示 inode，以及 `-F` 以在输出末尾添加文件类型，例如在目录后添加斜杠 `/`。以下使用 `-l` 选项的示例：

```text
MON> ls -l /stand
drwxr-xr-x   2 0       8192 lost+found
-rw-rw-rw-   1 0        5416 iconfig
drwxr-xr-x   4 0       2048 build
-rwxr-xr-x   1 0     15273152 vmunix
drwxrwxrwx   5 0        1024 .dkkm
vmunix.prev
-rw-r-r-r---  1 0         19 bootconf
-r-r-r-r-T--- 1 0          82 kernel
-rw----------  1 0         12 rootconf
-r-r-r-rT--- 1 0       1040 system
-r-r-r-rT--- 1 0       1035 system.prev
drwxr-xr-x   1 0     14488016 vmunix.prev
drwxrwxrwx   5 0        1024 .dkkm
drwxr-xr-x   2 0       1024 system.d
drwxr-xr-x   2 0       1024 krs
drwxr-xr-x   2 0       1024 krs.tmp
drwxr-xr-x   2 0       1024 krs_lkg
-R-XR-XR-X   1  2      2      845680 vpmcon
-rw-------    1  0      0     102640 vpmcon.dmp
-rw-------     2  0      0      8232 vpdb
```

`cbuf` `partition_name`

显示指定虚拟分区的控制台缓冲区中的信息。如果缓冲区中没有信息，你将收到以下消息：

```text
MON> cbuf uhnjlvp1
   Buffer is empty
```

`MON>` 提示符下的许多命令都具有信息展示功能。现在我们继续了解 vPars 的状态。

### 虚拟分区启动状态

在第二章中创建和修改 vPars 时，我们已经看到了许多处于不同启动状态的 vPars 示例。当我们启动虚拟分区时，它会经历 `load`（加载）阶段，然后是 `boot`（启动）阶段，最后进入 `up`（运行）状态。虚拟分区还可能处于其他状态。表 3-1 总结了在撰写本文时虚拟分区的状态：

### 表 3-1 虚拟分区状态

| vPars 状态 | 描述 |
| :--- | :--- |
| load | 虚拟分区的内核映像正在被虚拟分区监视器加载到内存中。 |
| boot | 虚拟分区正在启动过程中。内核映像已成功由虚拟分区监视器加载。 |
| up | 虚拟分区已成功启动并正在运行。 |
| shut | 虚拟分区正在关闭过程中。 |
| down | 虚拟分区未运行，已停止。 |
| crash | 虚拟分区经历了恐慌（panic）并正在崩溃。 |
| hung | 虚拟分区无响应并挂起。 |

在第二章创建虚拟分区并通过连续发出 `vparstatus` 命令观察其启动时，我们已经看到过其中的几种状态。以下示例显示了虚拟分区 `cable2` 的启动过程：

```text
# vparboot -p cable2
# vparstatus
[Virtual Partition]
Virtual Partition Name  State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Load Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn.Manl /stand/vmunix
cable2 Boot Dyn.Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
# vparstatus
[Virtual Partition]
Virtual Partition Name State Attributes Kernel Path Boot Opts
------------------------------------------
cable1 Up Dyn_Manl /stand/vmunix
cable2 Up Dyn_Manl /stand/vmunix

[Virtual Partition Resource Summary]
Virtual Partition Name CPU Num Memory (MB)
                        Min/Max Bound/ IC # Ranges/ Total MB
                        Unbound devs /stand/vmunix
cable1 2/4 2 0 4 0/0 2048
cable2 2/2 2 0 4 0/0 1024
```

此示例显示 `cable2` 依次进入 `load`，然后 `boot`，最后 `up` 状态。`cable2` 是从运行在同一硬件上的 `cable1` 启动的。当 `cable1` 启动时，系统已经完成了启动过程。由于大部分硬件已在运行，`cable2` 的启动速度非常快。第一个虚拟分区的启动时间与非虚拟分区系统的启动时间相当，但随后的 vPars 启动要快得多。

### setboot 命令和 vPars

在第二章我们的 vPars 示例中，我们将虚拟分区的 autoboot（自动启动）设置为关闭。在非 vPars 系统上，`setboot` 命令从稳定存储读取并写入数据。在 vPars 系统上，`setboot` 命令与虚拟分区数据库交互。在 vPars 系统上运行 `setboot` 的效果如表 3-2 所示：

### 表 3-2 setboot 和虚拟分区

| vPars setboot 选项 | 描述 |
| :--- | :--- |
| -a | 更改虚拟分区的备用启动路径。设置备用启动路径：`# setboot -a 0/8/0/0.8,0.5,0.0.0` |
| -b | 设置虚拟分区的 autoBoot（自动启动）属性。设置 AutoBoot 开启：`# setboot -b on` |
