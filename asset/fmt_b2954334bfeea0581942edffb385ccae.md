
编写 preseed 文件最简单的方法是手动安装系统。然后，`debconf-get-selections ---installer` 将提供你提供给安装程序的答案。你可以通过 `debconf-get-selections` 获取指向其他软件包的答案。然而，更整洁的解决方案是从示例开始，然后通过查阅文档来编写 preseed 文件。通过这种方法，只有需要覆盖默认答案的问题才会被写入。提供 `priority=critical` 启动参数以指示 debconf 仅询问关键问题，并对其他问题使用默认答案。

> **安装指南附录** 在线提供的 Debian 安装指南在附录中包含了关于使用 preseed 文件的详细文档。它还包含一个详尽且带有注释的示例文件，可以作为本地定制的基础。

- https://www.debian.org/releases/stable/amd64/apb.html

- https://www.debian.org/releases/stable/example-preseed.txt

但请注意，上述链接文档的是 Debian 的稳定版，而 Kali 使用测试版，因此你可能会遇到细微差异。你也可以咨询 Debian-installer 项目网站托管的安装手册，它可能会更新。

- http://d-i.alioth.debian.org/manual/en.amd64/apb.html

## 4.4. ARM 安装

Kali Linux 运行在各种基于 ARM 的设备（例如，笔记本电脑、嵌入式计算机和开发板）上，但你不能在这些设备上使用传统的 Kali 安装程序，因为它们在内核或启动配置方面特定特定要求。为了让这些设备更易使用，Offensive Security 开发了构建即用镜像的脚本。这些镜像可以在他们的网站上找到：

- https://github.com/offensive-security/kali-arm

由于这些镜像是可用的，你在 ARM 上安装 Kali 的任务被大大简化。以下是基本步骤：

1. 下载适用于你设备的镜像，并确保校验和与网站上提供的匹配（参见 2.1.3 节，“验证完整性与真实性”）。注意镜像通常是 xz 压缩的，确保使用 xz 进行解压。

2. 使用 `dd` 将镜像拷贝到存储设备（类似于第 2.1.4 节，“在 USB 闪盘上拷贝镜像”）：

```
dd if=kali-image.img of=/dev/sdX bs=512k
```

3. 将介质插入你的 ARM 设备。

4. 启动设备并登录（“root”）。如果没有屏幕，使用嗅探器查找 DHCP 流量。

5. 修改 root 密码并生成新的 SSH 密钥，特别是设备将永久运行在公共网络上。

6. 享受你运行 Linux 的新 ARM 设备！

| 特殊情况和更详细文档 | 这些说明是通用的，虽然适用于大多数设备，但总有例外。例如，Chromebook 需要开发者模式，其他设备需要按下特殊键才能从外部介质启动。 |

| | 请参考专门的“Kali ARM”

## 4.5. 安装故障排除

安装程序非常可靠，但你可能会遇到 Bug 或面临外部问题，如：网络问题、镜像源损坏以及磁盘空间不足。因此，能够排除安装过程中出现的问题是非常有用的。

当安装程序失败时，它会显示一个相当没有帮助的界面，如图 4.26 所示，“安装失败”（第 96 页）。

![](img/f888cd88b4fb3dd45062e14ce223cc4f_121_0.png)

图 4.26 安装失败

此时，最好知道安装程序利用了多个虚拟控制台：你看到的界面运行在第五个控制台（图形化安装程序，CTRL+Shift+F5）或第一个控制台（文本安装程序，CTRL+Shift+F1）上。在两种情况下，第四个控制台（CTRL+Shift+F4）都会显示正在发生的日志，你通常可以在这里看到更有用的错误信息，例如图 4.27 中的“安装程序的日志屏幕”（第 97 页），它揭示了安装程序已耗尽磁盘空间。

```
Apr 15 19:04:24 main-menu(8331): (process:5559): lib: error:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559)
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/choose_partition/60partition_tree/do_op
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559)
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/free_space/50new/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559)
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/free_space/50new/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559)
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/free_space/50new/do_option:
Apr 15 19:04:24 main-menu(8331): (process:5559): /lib/partman/active_partition/choices: not found
Apr 15 19:04:24 main-menu(8331): (process:5559)
Apr 15 19:04:24 main-menu(8331): (process:5559): (libc1): package doesn't exist (ignored)
Apr 15 19:04:25 base-installer: INFO: Menu item 'live-installer'
Apr 15 19:04:25 base-installer: installing squashfs-modules for cdrom/lib/filesystem/squashfs
Apr 15 19:04:25 kernel: error: squashfs-linux-4.3.0-kalli-amd64-di4: package doesn't exist
Apr 15 19:04:25 base-installer: (ignored)
Apr 15 19:04:25 kernel [04585]: DEBI:
Apr 15 19:04:25 kernel: [165.7960591] loaded version 4.0 (2009/01/31) Philipp Lougher
Apr 15 19:04:25 kernel: [165.7960591] module loaded
Apr 15 19:04:25 base-installer: error: tar copying the live system failed (9238 out of)
Apr 15 19:04:25 base-installer: Files have been copied, last: tar: write error: No space left on device
Apr 15 19:04:25 main-menu(8331): (process:8491): tar: write error: Broken pipes
Apr 15 19:04:25 main-menu(8331): WARNING == Configuring 'live-installer' failed with error code 1
Apr 15 19:04:25 main-menu(8331): WARNING == Menu item 'live-installer' failed.
```

> 图 4.27 安装程序的日志屏幕
