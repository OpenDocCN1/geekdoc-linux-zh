
一旦卷扩展完成，我们需要扩展实际的文件系统。这是通过 `xfs_growfs` 命令完成的：

```
xfs_growfs /dev/mapper/DATA-xfs1
```

取决于文件系统的活动程度，增长可能需要几分钟。`xfs_growfs` 命令的输出将在完成后显示文件系统的详情：

```
$root@fs # xfs_growfs /dev/mapper/DATA-xfs1
data /dev/mapper/DATA-xfs1 is now 10.05G in 2560 blocks (10.05G)
data /dev/mapper/DATA-xfs1:data size changed from 2.00G to 10.05G
$root@fs ~#
```

在 DNF 开发的这一阶段，大多数命令都是相同的，但 DNF 确实有一些“小技巧”，例如自动运行更新。

# DNF 自动更新

你可以设置 DNF 自动运行。要实现此功能，安装 `dnf-automatic` 包并使用以下命令启用服务：

```
yum install dnf-automatic
systemctl enable dnf-automatic.timer
systemctl start dnf-automatic.timer
```

接下来，编辑 `/etc/dnf/automatic.conf` 文件。该文件中包含一些技巧。你可以通过将 `apply_updates` 参数设置为 `yes` 来覆盖是否在下载时自动应用补丁。这将强制在任务运行时应用补丁。

不要忘记设置 `system_name` 参数，以便电子邮件和通知将显示正确的名称。

你还可以设置系统向你的邮箱发送一份安装报告。在 `[email]` 区域中设置电子邮件。如果使用电子邮件中继，请确保它不需要身份验证，或者根据需要将其添加到配置中。

作为最后一个技巧，你可以将 `emit_via` 参数从 `stdout` 改为 `motd`。当设置为 `motd` 时，系统 motd 文件将更新以反映安装了哪些补丁。当用户登录系统时，他们将看到完整的安装补丁列表以及安装时间，如下截图所示：

```
xorg-server-x86       x86_64 1.20.11-5.e18  ol8_x64_appstream      1.5 M
xorg-server-Xwayland  x86_64 21.1.3-2.el8  ol8_x64_appstream      963 k
xorg-server-common    x86_64 1.20.11-5.e18  ol8_x64_appstream      42 k
                                     x86_64 5.2.4-4.el8       ol8_x64_baseos      153 k
z-libs                                 x86_64 21.1.3-2.el8       ol8_x64_baseos      96 k
zlib                                   x86_64 12.1.18-5.el8  ol8_x64_baseos_latest  102 k
Installing module packages:
kernel-devel                           x86_64 5.14-21306.39.el8uk  ol8_x64_UEKR             109 M
Installing dependencies:
NetworkManager-encrypt-update      1.26.3-4.0.1.el8  ol8_x64_baseos_latest  137 k
autog-libs                             x86_64 6.18-12.el8       ol8_x64_appstream      75 k
glibc-common-ext                       x86_64 2.28-218.180.1.el8  ol8_x64_userspace_kcplice
gnutls-data                            x86_64 3.6.16-4.0       ol8_x64_appstream      1.6 M
gnutls-utils                           x86_64 3.6.16-4.0       ol8_x64_appstream      52 k
gdb2-tools-devel                       x86_64 1.12.2-03.el8  ol8_x64_baseos_latest  348 k
linux-firmware                        x86_64 2019.999-991  ol8_x64_baseos_latest  478 k
libgpg                                 x86_64 4.18.0-372.el8  ol8_x64_baseos_latest  14 M
kernel-core                           x86_64 4.18.0-372.el8  ol8_x64_appstream      32 M
space-helper                        x86_64 9.0.1-2.2021126gitifeff3f3.module+el18.6.0+206593dc7c70  184 k
libbpf                                 x86_64 0.4.3-0.8       ol8_x64_appstream      125 k
libd                                  x86_64 2.3.3-2.el8       ol8_x64_appstream      32 k
libtgms                               x86_64 9.0.1-2.2021126gitifeff3f3.module+el18.6.0+206593dc7c70
linux-firmware-core                   x86_64 2019.9200394  ol8_x64_baseos_latest  509 k
devt1                                 x86_64 1.2.0-2.el8  ol8_x64_appstream      745 k
qemu-kvm-deps                          x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70
qemu-kvm-us-bredir                   x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70  2.6 M
qemu-kvm-ui-opengl                   x86_64 15.6.2-1.el8.module+18.6.0+206593dc7c70  184 k
shadow-utils-subid                    x86_64 4.2-6.el8       ol8_x64_baseos_latest  223 k
swtpm                                 x86_64 0.7.0-2021110git9b7fd.module+el18.6.0+206593dc7c70  43 k
swtpm-libs                           x86_64 0.7.0-2021110git9b7fd.module+el18.6.0+206593dc7c70  44 k
swtpm-tools                          x86_64  ol8_x64_appstream      119 k

Transaction Summary
Install: 26 Packages
Upgrade: 62 Packages

Updates at Wed 22 Jun 2022 06:23 AM Activated: systemctl enable --now cockpit.socket
Last login: Wed 22 Jun 2022 12:25 from 192.168.56.1
```

默认情况下，在此进行的服务更改会影响 `/etc/systemd/system/timers.target` 文件。

```
[Unit]

Description=dnf-automatic timer

ConditionPathExists=/run/ostree

[Timer]

Calendar=*-.* 0:00

RandomizedDelaySec=60m

Persistent=true
```
