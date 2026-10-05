
当安装程序失败时，它会显示一个相当没有帮助的界面，如图 4.26 所示的“安装步骤失败”第 96 页]。

![](img/4d5d0d3397277b3d6e29d1328d013586_121_0.png)

图 4.26 安装步骤失败

此时，了解安装程序使用了多个虚拟控制台是有用的：你看到的主屏幕运行在第五个控制台（对于图形化安装程序，使用 CTRL+Shift+F5），或者运行在第一个控制台（对于文本安装程序，使用 CTRL+Shift+F1）。在这两种情况下，第四个控制台（CTRL+Shift+F4）都会显示正在发生的日志，你通常可以在那里看到更有用的错误信息，例如图 4.27 所示的“安装程序的日志屏幕”第 97 页]，该日志揭示了安装程序磁盘空间不足。

```
option:
Apr 15 19:04:24 main-menu(8331): (process:5559): lib error:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559):
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/choose_partition/60partition_tree/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): lib error:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559):
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/free_space/50new/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): lib 226:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559):
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/free_space/50new/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): lib 226:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559):
Apr 15 19:04:24 main-menu(8331): (process:5559): (libc1): package doesn't exist (ignored)
Apr 15 19:04:24 base-installer: INFO: Menu item 'live-installer' selected
Apr 15 19:04:24 base-installer: installing squashfs for /cdrom/live/filesystem/squashfs
Apr 15 19:04:24 base-installer: auto-install: kernel-squashfs-4.3.0-kalli-amd64-di: package doesn't exist (ignored)
Apr 15 19:04:24 kernel: [00485] DEGBUS: kernel [165.79501261]: version 4.4.0 (2009/01/31) Phillip Lougher
Apr 15 19:04:24 kernel: [00485] 165.79501261: module loaded
Apr 15 19:04:45 base-installer: error: The tar process copying the live system failed (only 9238 out of files have been copied, last ...)
Apr 15 19:04:45 base-installer: error: tar: write error: No space left on device
Apr 15 19:04:45 main-menu(8331): (process:8491): tar: write error: Broken pipes
Apr 15 19:04:45 main-menu(8331): WARNING ==: Configuring 'live-installer' failed with error code 1
```
