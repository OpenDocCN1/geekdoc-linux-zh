
@ target_selections]

## swremove(1M) 惠普特公司
`swremove(1M)`

### 名称
`swremove` - 取消配置并移除软件产品

### 用法
```
swremove [Toolkit Options] [-i] [-p] [-v] [-d][-r] [-x option=value] -X option_file] [-f software_file] [-t target_file] -C session_file] [-S session_file] [-Q date] [-J jobid] [software_selections] @ target_selections]
```

## swverify(1M) 惠普特公司
`swverify(1M)`

### 名称
`swverify` - 验证软件产品

### 用法
```
swverify [-v] [-d][-r] [-x option=value] [-X option_file] [-f software_file] [-t target_file] -C session_file] [-S session_file] [-Q date] [-J jobid] [software_selections] [@ target_selections]
```

## 第三章 构建 HP-UX

### 修改并构建 HP-UX 内核
你可能需要以某种方式修改 HP-UX 11i 内核，例如更改内核参数，然后重建内核。你可能需要创建一个新的 HP-UX 内核以便驱动程序或子系统、调整内核以提高性能、更改配置参数或更改 dump 和交换设备。如果更新或修改内核的动态元素（如本章示例所示），则需要。更新或修改静态元素需要重启并可能还需要额外的步骤。对于所有发生的变化，不需要重建内核。在 11i 中，许多动态可调内核参数和动态加载模块可以修改内核但不需要重启。结合 11i 中提供的许多补丁，你不需要频繁重启。在下一节中，我们将修改动态可调内核，从而修改内核而无需重启系统即可生效。然后我们将看到完整的重建过程，包括重启。这不能替代第 10 章涵盖的系统管理员 (SAM)。因此，当你有 SAM 为你执行此操作时可以了解更多。在本章中，我讨论了与内核生成相关的各种命令，并涵盖了手动创建内核的过程。11.0 引入了动态加载模块。在 11x 中，该功能的基础已经建立，为每个模块提供了独立的文件。11.0 允许特殊创建的模块在无需重启系统或模块未使用的情况下加载到内核。有关此高级功能的详细信息可以查看 HP-UX 11.x 发布说明。IT 资源网站 (`itrc.hp.com`) 包含该主题的信息，包括开发者指南。

### 构建内核
首先，让我们看看在书中许多示例使用的 HP-UX 11i 系统上的现有内核。`sysdef` 命令用于分析和报告当前运行系统的调参数。如果你不想使用当前运行系统，可以指定特定文件进行分析。以下是 11i 系统上运行的 `sysdef` 部分列表：

| 名称 | 数值 | 启动 | 最小-最大单位 | 标记 |
| --- | --- | --- | --- | --- |
| acctresume | 4 | | 100-100 | |
| acctusend | 2 | | 100-100 | |
| allocate_fs_swapmap | 0 | | | |
| nbufferpage | 32768 | | | |
| create_fastlinks | 0 | | | |
| dbc_max_pct | 5 | | | |
| dbc_mlcpt | 0 | | | |
| default_dir_ir | 0 | | | |
| deckless_node = 0 | | 0-1 | | |
| eis_estimate | 768 | | | |
| emqmaize | 10 | | 0 | | |
| fs_async | 0 | | 0-1 | | |
| hpux_as_override | 0 | | 0-6 | | |
| nproc | 400 | | | | |
| pmty | 60 | | | | |
| nnstrpcy | 60 | | 1-25 | | |
| swapdev | 10 | | 1-25 | | |
| swapsiz | 10 | | | | | |
| public_shlibs | 1 | | | | | | |
| remote_ntfs_swap | 0 | | | | | | |
| trsched_numpri | 32 | | 0-1 | | | | |
| sema | 412876 | | 4-4 | | | | |
| shmem | 0 | | | | | | |
| shmnei | 200 | | 3-1024 | | | | |
| shhemi | 0 | | 0 | | | | |
| streamapipes | 1 | | | | | | |
| swchunk | 2048 | | 2048-16384 | kBytes | | | |
| timeslice | 10 | | -1-23147483648 | Ticks | | | | |

# 第3章 构建 HP-UX 内核

除了可调参数外，你可能还想查看系统中发现的所有硬件的报告。`ios` 命令可以为你完成此工作。通过使用 `sysdef` 和 `iscan`，你可以查看可调参数的设置情况，以及系统中存在哪些硬件。你将了解系统的设置情况，然后对内核进行修改。以下是 HP-UX 11i L-Class 系统执行 `sysdef` 后的输出：

![](img/6969df54e516231f8e64fd1177ac1127_161_0.png)

![](img/6969df54e516231f8e64fd1177ac1127_161_1.png)

```
# /usr/sbin/iscan -
```

| Class | I/W Path | Driver | S/W State | H/W Type | Description |
|---|---|---|---|---|---|
| root | | | root | CLAIMED | BUS NEXUS | 系统总线适配器 (582) |
| ica | | | | sba | CLAIMED | BUS NEXUS | 本地 PCI 适配器 (782) |
| ba | 0/0 | | | CLAIMED | | |
| lan | 0/0/0/0 | btlan | CLAIMED | INTERFACE | PCI 100/Base-TX 核心 |
| target | 0/0/1/0 | | c720 | CLAIMED | DEVICE | 快速宽链路 |
| ctl | 0/0/1/0.7 | | scl1 | CLAIMED | DEVICE | 启动器 |
| root | 0/1/1/2 | tgt | | CLAIMED | DEVICE | SCSI C896 超宽末端 |
| dcl | 1/0/1/2 | | sdisk | CLAIMED | DEVICE | SEAGATE ST31820LC |
| target | 0/0/1/7 | tgt | scl1 | CLAIMED | DEVICE | |
| ext | 0/0/1/0.7 | | c720 | CLAIMED | DEVICE | 启动器 |
| Single-Ended | | | | | | DEVICE | SCSI C875 超宽末端 |
| target | 0/3/0/2 | tgt | | CLAIMED | DEVICE | |
| dcl | 0/0/2/0.2 | sdisk | CLAIMED | DEVICE | SEAGATE ST318230LC |
| target | 0/4/0.7 | tgt | | CLAIMED | DEVICE | |
| ctl | 0/0/0/0 | | scl1 | CLAIMED | DEVICE | 启动器 |
| ext | 0/3/2/0/1 | | c720 | CLAIMED | INTERFACE | SCSI C875 超宽末端 |
| target | 5/0/21/4 | tgt | | CLAIMED | DEVICE | |
| dcl | 0/2/1/4.0 | sdisk | CLAIMED | DEVICE | TOSHIBA DA-RM-62017A |
| target | 0/3/1/0.7 | tgt | scl1 | CLAIMED | DEVICE | |
| tty | 0/0/4/0 | | asioq | CLAIMED | INTERFACE | PCI 串口 (10348) |
| ba | 1/0/5/0 | | asioq | CLAIMED | INTERFACE | 本地 PCI 适配器 (10348) |
| ba | 2/2 | | | CLAIMED | BUS NEXUS | 本地 PCI 适配器 (782) |
