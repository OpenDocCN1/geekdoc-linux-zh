
```text
VMFSET2760I VMFSETUP processing completed successfully
VMFSRV2760I SERVICE processing completed successfully for GCS BUILD
VMFSUT2760I VMFSUTFB processing started
VMFSUT2760I VMFSUTFB processing completed successfully
VMFSRV2760I SERVICE processing completed successfully
Ready; T=28.63/30.61 09:50:31
CMS

                         RUNNING   VMGUEST
```

### 9.6.1  调用 PUT2PROD

在执行完之前的步骤后，我们运行了 exec PUT2PROD。在 PUT2PROD 处理期间，我们遇到了其中一个 PTF 的问题。我们发现该特定问题已被记录为已知错误，其中还包含规避该问题的必要操作。在执行了记录的操作后，我们成功运行了 PUT2PROD exec。

完成后，我们从 MAINT 发出了以下命令：

```text
SHUTDOWN REIPL
```

发出该命令后表明 CP 级别现在已达到更高的 RSU 级别：

```text
Q CPLEVEL
```

### 9.6.2  安装额外的 PTF

然后我们应用了自 RSU 发布以来提供的额外 PTF。它们本应在 PUT2PROD 之前使用 SERVICE 安装，以避免我们最初遇到的问题。这些 PTF 的安装未成功完成。我们了解到 500 虚拟设备应处于读写模式（R/W），可能是因为在 SERVICE 过程中有一个临时构建过程正在使用该磁盘。纠正此问题后，SERVICE 成功完成，PUT2PROD 也成功完成。

> **重要：** 在使用 PUT2PROD 之前应用 PTF，以避免 PUT2PROD 中的错误。
> 
> 在安装 PTF 之前，请确保 500 虚拟设备处于 R/W 模式。

## 9.7 将已维护的 z/VM 投入生产

在对 z/VM 进行维护服务后，需要进行 IPL，因为它可能是对 CP 的服务。

在方便时，根据您的服务时间或其他条件，对系统进行 IPL。与任何其他操作系统一样，所有用户，或在这种情况下，所有虚拟机，都会被关闭。z/VM 具有执行 SHUTDOWN REIPL 的能力，前提是它是由具有执行此操作适当特权类的虚拟机发出的¹。需要始终运行的虚拟机可以在 IPL 期间自动注销（AUTOLOG）。

¹ 不必像 z/OS IPL 那样从 HMC 控制台执行

## 交叉引用：z/OS、z/VM 和 Linux 命令

本附录提供了 z/OS 命令和概念与其 z/VM 和 Linux 对应的交叉引用。虽然这里没有列出所有命令和概念，但我们认为这对于 z/OS 系统程序员更熟悉 System z 上的 z/VM 和 Linux 来说是一个良好的开端。

在我们的示例中，我们在需要具体说明时引用 SLES10 命令。我们建议检查您的 Linux 发行版以验证命令是否保持不变。

本附录包含以下表格：

- Table A-1 on page 400, Commands for file editing
- Table A-2 on page 400, General commands
- Table A-3 on page 401, FTP and TCP/IP commands
- Table A-4 on page 401, General concepts

### Table A-1 Commands for file editing

| z/OS-ISPF Edit | z/VM CMS XEDIT | Linux vi | Description |
|---|---|---|---|
| r | " | yy | Repeat or copy a line |
| d | d | dd | Delete a line |
| cc..cc line command | cc ...cc | :1,3co$ | Block copy |
| mm...mm line command | mm...mm | :1,3m$ | Block move |
| dd...dd | dd...dd | :1,3d | Block delete |
| find <xxxx> | /<xxxx> | /<xxxx> | Find keyword (below) |
| find <xxxx> prev | -/<xxxx> | ?<xxxx> | Find keyword (above) |
| ex xxx | — | — | Exclude lines containing a character string (xxx) |
| del all excluded | — | — | Delete the lines that you excluded using the command "ex xxx" |
| )n line command | — | — | Indent n spaces to the right |
| (n line command | — | — | Move n spaces to the left |

### Table A-2 General commands

| z/OS command | z/VM command | Linux command | Description |
|---|---|---|---|
| d u,,b120,1 | q b120 | ls -la /dev/<device> | Display a single device named b120 (replace b120 with your device) |
| d u,,b120,8 | q b120-b127 | ls -la /dev/sd* | Display string of devices |
| v b120,online | vary on b120 | mount /dev/<device> <mnt_point> | Vary on a device |
| v b120,offline | vary off b120 | umount mnt_point | Vary off a device |
| — | q paths b120 | — | Display paths to a device |
| — | q chpid 18 | — | Display devices on a chpid |
| D M=CPU | q proc | cat /proc/cpuinfo | Display number of processors |

