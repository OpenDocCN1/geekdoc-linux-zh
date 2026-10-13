
# Profile

The information shown below is your profile for installing Solaris software.
It reflects the choices you've made on previous screens.

```
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
>
> 我通常在初始软件安装后才设置这些挂载。很多时候，此时系统尚未连接到生产网络，因此挂载点不可用。也是个人偏好将此任务保存到安装后阶段，当我设置用户、打印机等时。我有一份安装软件后需要完成的所有事情的清单，设置挂载点是其中之一。

> 注意
>
> 分区大小和磁盘空间需求已在第 3 章中讨论。如果您不确定安装程序设置的分区和大小，请查看该章节。

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

## 19. 对此问题回答“n”。然后会提示以下内容：

```
Autoshutdown has been disabled.
Do you want the system to ask about this again, when you next reboot? (This gives you the chance to try it before deciding whether to keep it.) [y,n,?]
```

> 注意
>
> 请参阅本节末尾关于 Autoshutdown 功能的评论。

## 20. 对此问题回答“n”。按下 Enter 后，将显示以下消息：

```
Please specify the media from which you will install Solaris 8 (SPARC) Software.
Alternatively, choose the selection for "Skip" to skip this CD and go on to the next one.

Media:
1. CD
2. Network File System
3. Skip
```

在本例中，我将从 CD 安装，因此我回答 1 并按下 Enter。

当前位于 CD-ROM 驱动器中的光盘将被弹出，并出现以下消息：
