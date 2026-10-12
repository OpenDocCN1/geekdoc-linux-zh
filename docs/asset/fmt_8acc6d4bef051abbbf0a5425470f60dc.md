
# 第7章 高级安装

- 11. 点击左侧窗格中的显示配置（Display Configuration）。选择 X Window 系统并确保适当的颜色深度和分辨率。确保默认桌面为 GNOME，并勾选在启动时启动 X Window 系统（Start the X Window System on boot）。在首次启动时，设置向程序（Setup Agent）选择“启用”（Enabled）。

- 12. 点击显卡（Video Card）选项卡，确保已勾选探测显卡（Probe for video card）。

- 13. 点击显示器（Monitor）选项卡，确保已勾选探测显示器（Probe for monitor）。

- 14. 点击左侧窗格中的软件包选择（Package Selection）。选择所有可用软件包并确保勾选自动刷新依赖项（Automatically Refresh Dependencies）。

- 15. 点击文件（File）菜单并选择保存文件（Save File）。在保存文件界面中，确保 `ks.cfg` 被列为文件名，并点击 OK。

- 16. 关闭 Kickstart 配置器并退出 GNOME 桌面。

- 17. 按 `Ctrl+Alt+F2` 切换到命令行终端（ty2），并使用 `root` 用户和 `secret` 密码登录终端。

- 18. 在命令提示符下，输入 `less ks.cfg` 并回车。查看 Kickstart 配置器在文件中创建的条目，完成后按 `q` 退出。

- 19. 在命令提示符下，输入 `less anaconda-ks.cfg` 并回车。查看在实验项目 3-1 中红 Hat 安装程序在文件中创建的条目。完成后按 `q` 退出。

- 20. 输入 `exit` 并回车退出 shell。

## 项目 7-2

在本次实验项目中，你将执行 kickstart 安装。完成 kickstart 安装后，你将手动运行第一个向导来配置系统设置。

- 1. 按 `Ctrl+Alt+F2` 切换到命令行终端（ty2），并使用 `root` 用户和 `secret` 密码登录终端。

- 2. 接下来在命令提示符下输入 `vi anaconda-ks.cfg` 命令并回车。替换文件的以下部分：

```
# 以下是你所请求的分区信息
# 注意，你删除的任何分区都不会在此处表示
# 除非你先清除所有分区，否则这里
```

![](img/8fe037bf1ed016dccb79dbd1a27184f2_340_0.png)

```
# 不保证能工作
#clearpart --linux
#part /--fstextype3 --onpart hda1
#part swap --onpart hda2
```

替换如下文本，其中 A 是从预安装检查清单中获得的“文件系统可用空间”的值（即对于 7000MB 输入 7000），B 是从预安装检查清单中获得的“交换分区所需空间”的值（即对于 600MB 输入 600）：

```
zerombeb yes
clearpart --all --initlabel
part /--fstype3 --size A
part swap --size B
```

完成后，保存更改并退出 `vi` 编辑器。

- 3. 在软驱驱动器中插入空白软盘。

- 4. 在命令提示符下，输入 `mkfs /dev/fd0` 并回车，在软盘设备上创建一个 ext2 文件系统。接着输入 `mount /dev/fd0` 并回车。

- 5. 在命令提示符下，输入 `anaconda-ks.cfg /mnt/firstboot`。

- 6. 在命令提示符下，输入 `unmount /mnt/firstboot`。

- 7. 在命令提示符下，输入 `reboot /dev/fd0`。

- 8. 在命令提示符下，输入 `anaconda-ks.cfg /mnt/firstboot`。

- 9. 在恭喜界面，点击重启。

- 10. 使用 `root` 和 `secret` 密码登录 GNOME 桌面。

- 11. 在命令提示符下，输入 `vi /etc/sysconfig/firstboot`。将 `RUN_FIRSTBOOT=NO` 修改为 `RUN_FIRSTBOOT=YES`。

- 12. 退出 `vi` 编辑器。

- 13. 在 firstboot 向导欢迎界面，点击下一步。

- 14. 在许可协议界面，选择“我同意许可协议”并点击下一步。

- 15. 在日期和时间界面，确保本地日期时间正确并点击下一步。

- 16. 在显示界面，选择你优的分辨率和颜色深度并点击下一步。

- 17. 在用户账户界面，在指定区域输入以下信息：

用户名：user1

全名：sample user

密码：secret

确认：secret

完成后，点击网络登录（Network Login）按钮，点击认证（Authentication）选项卡。确保勾选了使用 MD5（Use MD5）和使用影子密码（Use Shadow Passwords），点击 OK。点击下一步。

- 18. 在附加 CD 界面，点击下一步。

- 19. 在完成设置界面，点击下一步。

- 20. 退出 GNOME 桌面。

## 项目 7-3

在本次实验项目中，你将查看系统信息。

- 1. 你的 Linux 系统完成 firstboot 向导后，你将处于图形终端（tty7）。按 `Ctrl+Alt+F2` 切换到命令行终端（ty2），并使用 `root` 用户和 `secret` 密码登录终端。

- 2. 在命令提示符下输入 `install.log` 命令并回车，查看文件中的条目。软件包安装期间是否有错误？按 `q` 退出 less 工具。

- 3. 在命令提示符下输入 `install.log.syslog` 命令并回车，查看文件中的条目。该文件中显示了什么信息？按 `q` 退出 less 工具。

- 4. 在命令提示符下，输入 `ls -F /proc/cpuinfo` 并回车，查看 proc 文件的目录内容。

- 5. 在命令提示符下，输入 `less /proc/cpuinfo` 并回车。安装是否正确检测了你的 CPU？按 `q` 退出 less 工具。

![](img/8fe037bf1ed016dccb79dbd1a27184f2_342_0.png)

- 6. 在命令提示符处输入 `less /proc/dma` 并按回车。系统在使用哪些 DMA 通道？你如何修复任何差异？按 `q` 退出 less 实用程序。

- 7. 在命令提示符处输入 `less /proc/interrupts` 并按回车。系统在使用哪些 IRQ 以及哪些设备？你如何修复任何差异？按 `q` 退出 less 实用程序。

- 8. 在命令提示符处输入 `less /proc/ioports` 并按回车。系统上占用了哪些 I/O 地址？你如何修复任何差异？按 `q` 退出 less 实用程序。

- 9. 在命令提示符处输入 `less /proc/modules` 并按回车。显示了什么？每个条代表什么？这与第 6、7、8 步中的信息如何对应？按 `q` 退出 less 实用程序。

- 10. 在命令提示符处输入 `less /proc/meminfo` 并按回车。你的 Linux 系统识别了电脑中的所有内存吗？如果没有，你可以做什么？按 `q` 退出 less 实用程序。

- 11. 在命令提示符处输入 `less /proc/pci` 并按回车。关于你电脑中的 PCI 设备显示了哪些信息？按 `q` 退出 less 实用程序。

- 12. 在命令提示符处输入 `dmesg | less` 并按回车。观察这些目。它们与你在第 5 到 11 步中看到的硬件信息如何对应？完成后，按 `q` 键退出 less 实用程序。

- 13. 在命令提示符处输入 `less /var/log/messages` 并按回车。每个条目代表什么？这些条目与第 12 步看到的信息如何对应？完成后，按 `q` 键退出 less 实用程序。

- 14. 输入 `exit` 并按回车退出你的 shell。

### 目录练习

- 1. 确定关于你系统的以下信息：

    a. 使用了哪些 IRQ？

    b. 使用了哪些 DMA 通道？

    c. 使用了哪些 I/O 地址？

    d. Linux 内核位于何处？

    e. 系统是否有 PCI 设备？

    f. 哪些模块被加载到了内核中？

    g. 收集关于系统物理内存的信息。

- 2. 根据第 1 题的信息，如果你想添加额外的硬件设备：

    a. 有哪些 IRQ 可供使用？

    b. 有哪些 DMA 通道可供使用？

- 3. 在假设你有互联网连接和功能网络浏览器的情况下，收集关于三种执行 RAID 5 级的商业 RAID 控制器的信息，并写一份短报告，比较并对比它们的特征和成本。在什么情况下你会使用每一种？

- 4. 在假设你有互联网连接和功能网络浏览器的情况下，在互联网上搜索人们过去在 Linux 安装过程中遇到的五个与本章描述不同的问题。解决方案是什么？如果你在安装过程中遇到了类似的困难，该如何寻求帮助？

# 第 8 章
