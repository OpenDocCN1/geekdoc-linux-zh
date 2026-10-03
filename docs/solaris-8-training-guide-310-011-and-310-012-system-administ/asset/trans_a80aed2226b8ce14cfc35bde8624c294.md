
```
[ ] /usr/openwin
[ ] /var
[X] swap
F2_Continue   F5_Cancel   F6_Help
```

## 11. 进行选择，然后按 F2。

例如，我选择了这些额外的文件系统。你将看到以下对话框：

```
File System and Disk Layout

The summary below is your current file system and disk layout, based on the information you've supplied.

NOTE: If you choose to customize, you should understand file systems, their intended purpose on the disk, and how changing them may affect the operation of the system.
```

| 文件系统/挂载点 | 磁盘/切片 | 大小 |
|---|---|---|
| / | c0t0d0s0 | 80 MB |
| /var | c0t0d0s1 | 34 MB |
| overlap | c0t0d0s2 | 4102 MB |
| swap | c0t0d0s3 | 147 MB |
| /opt | c0t0d0s5 | 25 MB |
| /usr | c0t0d0s6 | 1159 MB |
| /export/home | c0t0d0s7 | 2655 MB |

```
F2_Continue   F3_Go Back   F4_Customize   F5_Exit   F6_Help
```

## 12. 此时，你可以通过按 F4 来进一步自定义切片大小。然后会提供一个菜单让你为每个分区选择新的大小。我将更改几个分区大小，所以我将按 F4。以下菜单将被显示：

```
Customize Disk: c0t0d0
Boot Device: c0t0d0s0
===================================
Slice  Mount Point      Size (MB)
0      /               80
1      /var            34
2      overlap         4102
3      swap            147
4                     0
5      /opt            25
6      /usr            1159
/export/home          2655
===================================
                Capacity:   4102 MB
                Allocated:  4100 MB
                Rounding Error:  2 MB
                Free:       0 MB
```

> 注意
我建议将 /usr、/var 和 /opt 作为单独的文件系统添加。/usr 为大多数 Solaris 二进制文件提供单独的文件系统。/var 为系统日志文件、已排队的软件包以及可能占用大量磁盘空间的其他内容提供空间。不建议将 /var 作为根文件系统的一部分。/usr 和 /opt 将为以后添加的额外软件包提供空间。同样，不建议将 /opt 和 /usr 作为根文件系统的一部分。

## 13. 我首先将 /export/home 的大小减小到 1174MB。我将 / 增加到 120MB。我将为 /var 分配 300MB，为 /opt 分配 200MB。然后我将添加另一个名为 /data 的分区，并将其设为 1000MB。当你对切片大小满意时，按 F2 继续。以下对话框将被显示：

文件系统和磁盘布局

下面的摘要是您当前的文件系统和磁盘布局，基于您提供的信息。

注意：如果您选择自定义，您应该了解文件系统、它们在磁盘上的预期用途，以及更改它们可能如何影响系统的运行。

| 文件系统/挂载点 | 磁盘/切片 | 大小 |
|---|---|---|
| / | c0t0d0s0 | 120 MB |
| /var | c0t0d0s1 | 300 MB |
| overlap | c0t0d0s2 | 4102 MB |
| swap | c0t0d0s3 | 147 MB |
| /data | c0t0d0s4 | 1000 MB |
| /opt | c0t0d0s5 | 200 MB |
| /usr | c0t0d0s6 | 1159 MB |
| /export/home | c0t0d0s7 | 1174 MB |

## 14. 仔细检查你的选择，并在准备进入下一步时按 F2。这是一个验证所有选择的良好时机。确保 swap 对于你要安装的服务器类型是足够的。似乎在 swap 空间；或 /var、/opt、/usr 文件系统上永远不会太大。换句话说，宁可过大，不要过小。

今天的许多服务器都配备了 18GB 的磁盘驱动器。我将整个驱动器用于操作系统。我的大多数服务器还运行第三方性能监控软件包，该软件包可在 /var 中创建巨大的日志文件。操作系统补丁也可能占用 /var 中的大量空间。由于你支持的各种应用程序和硬件组件，你会发现自己不断地向服务器添加补丁。我通常会疯狂地为每个文件系统分配几个千兆字节。

此外，很难估计服务器的 swap 需求。这些服务器可能数月不重启，并且可能支持多个数据库应用程序或用户。再次，分配充足的 swap——不少于 RAM 的两倍。如果分配过多的 swap 空间，系统性能不会下降。过多的 swap 空间只会浪费磁盘空间。然而，磁盘空间是便宜的，与

在高峰生产期间用完 swap 并导致应用程序崩溃的成本相比。当你对选择满意时，按 F2，然后将显示以下对话框：

```
Mount Remote File Systems?
Do you want to mount software from a remote file server? This may be necessary if you had to remove software because of disk space problems.

F2_Continue  F3_Go Back  F4_Remote Mounts  F5_Exit  F6_Help
```

## 15. 按 F2 继续，除非你想设置远程挂载。

你将看到以下对话框：

```
Profile
The information shown below is your profile for installing Solaris software.
It reflects the choices you've made on previous screens.

================================================================================

    Installation Option: Initial
        Boot Device: c0t0d0
        Client Services: None

        Software: Solaris 8, Entire Distribution 64-bit

File System and Disk Layout: /               c0t0d0s0   120 MB
                            /var            c0t0d0s1   300 MB
                            swap            c0t0d0s3   147 MB
                            /data           c0t0d0s4  1000 MB
                            /opt            c0t0d0s5   200 MB
                            /usr            c0t0d0s6  1159 MB
                            /export/home    c0t0d0s7  1174 MB

F2_Continue    F4_Change    F5_Exit    F6_Help
```

## 16. 验证信息，如果同意则按 F2。

你将看到以下对话框：

```
Reboot After Installation?

After Solaris software is installed, the system must be rebooted. You can choose to have the system automatically reboot, or you can choose to manually reboot the system if you want to run scripts or do other customizations before the reboot. You can manually reboot a system by using the reboot(1M) command.

    [X] Auto Reboot
    [ ] Manual Reboot

F2_Begin Installation    F5_Cancel
```

> 注意
我通常在初始软件安装后才设置这些挂载。很多时候，此时系统尚未连接到生产网络，因此挂载点不可用。也是个人偏好将此任务保存到安装后阶段，当我设置用户、打印机等时。我有一份安装软件后需要完成的所有事情的清单，设置挂载点是其中之一。

> 注意
分区大小和磁盘空间需求已在第 3 章中讨论。如果您不确定安装程序设置的分区和大小，请查看该章节。

## 17. 做出选择，然后按 F2 开始安装。这完成了交互式安装。软件正在安装时，你将看到以下对话框：

```
Preparing system for Solaris install
Configuring disk (c0t0d0)
  - Creating Solaris disk label (VTOC)
Creating and checking UFS file systems
  - Creating / (c0t0d0s0)
  - Creating /var (c0t0d0s1)
  - Creating /data (c0t0d0s4)
  - Creating /opt (c0t0d0s5)
  - Creating /usr (c0t0d0s6)
  - Creating /export/home (c0t0d0s7)
Beginning Solaris software installation
Solaris Initial Install
    MBytes Installed:    0.00
    MBytes Remaining:  711.51
```

屏幕底部会出现一个计量表，显示安装的进度。当它达到 100% 时，系统将提示你输入密码，显示以下消息：

```
On this screen you can create a root password.
A root password can contain any number of characters, but only the first eight characters in the password are significant. (For example, if you create `a1b2c3d4e5f6` as your root password, you can use `a1b2c3d4` to gain root access.)
You will be prompted to type the root password twice; for security, the password will not be displayed on the screen as you type it.
> If you do not want a root password, press Enter twice.
Root password:
Press Enter to continue.
```

## 18. 输入你的 root 密码。

你将看到以下另一条消息显示如下：

```
System identification is completed.
================================================
This system is configured to conserve energy.
================================================
After 30 minutes of idle time on this system, your system state will automatically be saved to disk, and the system will power-off. Later, when you want to use the system again, and you turn the power back on, your system will be restored to its previous state, including all the programs that you were running. Do you want this automatic power-saving shutdown? (If this system is used as a server, answer n) [y,n,?]
```
