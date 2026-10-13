
# 具有超线程技术的处理器 201

# 列表 8.2 继续

```
processor : 0
vendor_id : GenuineIntel
cpu family : 15
model : 3
model name : GenuineIntel(R) CPU 3.20GHz
stepping : 3
cpu Mhz : 2793.829
cache size : 1024 KB
physical id : 0
sibling : 2
core id : 0
cpu cores : 1
fdiv_bug : no
hlt_bug : no
f00f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 5

wp : yes
flags : fpu vme de pse tsc msr pae mce cx8 apic mtrr pge mca
```

```
cmov pat pse36 clflush dts acpi mmx fxsr sse s2 ss ht tm pbe pni
monitor ds_cpl id
bogomips               : 5592.02

processor           : 1
vendor_id           : GenuineIntel
cpu family           : 15
model               : 3
model name           : Genuine Intel(R) CPU 3.20GHz
stepping            : 3
cpu Mhz              : 2793.829
cache size           : 1024 KB
physical id          : 0
sibling            : 2
core id              : 0
cpu cores           : 1
fdiv_bug            : no
hlt_bug             : no
f0f_bug             : no
coma_bug            : no
fpu                 : yes
fpu_exception      : yes
cpuid level         : 5
wp                  : yes
flags               : fpu vme de se tsc msr mce cex axic mttr pge pbe pni
cmov pat pse36 clflush dts acpi mmx fxsr sse ss ht tm pbe pni
monitor ds_cpl id
bogomips               : 5585.63
```

与之前的多核处理器示例类似，请查看物理、core id 和 cpu 字段，以验证该系统是否被识别为具有 HT 技术的系统。处理器计数从 0 变到 1，这表明在操作系统看来，有两个处理器可以发送数据执行。两者的物理 id 均为 0，意味着只有一个处理器。cpu cores 的值为 1，且 id 的值为 0，意味着该处理器不是多核的。因此，由于处理器计数为 2，处理器必须具有 HT 技术。

在启动时可以使用 GRUB 引导加载程序通过内核选项禁用超线程。此过程仅禁用一个实例。在后续的启动中必须重复此操作。步骤如下：

1. 当出现 GRUB 启动菜单时，使用向上和向下箭头选择内核。
2. 按 E 键向内核添加内核选项。
3. 在行尾添加一个空格，然后添加内核选项。
4. 按回车键返回 GRUB 启动菜单。
5. 按 B 键启动系统。

如果内核被添加到 GRUB 文件中，则可以在后续启动时禁用超线程。以 root 身份打开 `/etc/grub.conf`，找到要禁用的内核行，在末尾添加空格并添加列表 8.3 所示的内核选项。

# 列表 8.3 使用 GRUB 禁用超线程

```
default=0
timeout=5
splash
image=(hd0,0)/boot/splash.gz
hidden
title Red Hat Linux (2.6.16)
root=(hd0,0)
kernel /boot/mlin-2.6.16 quiet
initrd /boot/initrd-2.6.16
```

## 总结

本章介绍了在 64 位、多核以及具有超线程系统上使用 Red Hat Linux 时需要注意的内容。对于多核系统，检测到了处理器核心数并安装了相应的内核。

# 第三部分 系统管理

在本部分中：

- 第 9 章 用户和组 (205)
- 第 10 章 备份与恢复技术 (221)
- 第 11 章 使用脚本自动化任务 (239)

## 第 9 章 用户和组

在本章中：

- 什么是用户和组？
- 管理用户
- 管理组
- 如何工作
- 最佳实践

对于 Red Hat Linux，所有用户必须输入用户名和密码以使用操作系统和应用程序的安全性。可以根据用户名授予或拒绝特定文件和目录的访问。因此，管理员的职责是管理用户数据库、存储以及迁移到不同的部门。

本章解释了如何管理本地用户和组。本地用户和组由登录的系统进行验证。用户名、组和密码都在本地系统中。用户和组也可以从网络服务器进行验证。有关允许中央服务器进行身份服务的详情，请参考第 12 章“身份管理”。

即使你使用远程身份管理，建议阅读第一节“什么是用户和组？”和最后一节“最佳实践”。最后一节提供了关于管理用户名、管理密码、删除帐户和结构化目录的提示。本节的方法适用于在本地系统或从远程服务器进行验证。

### 什么是用户和组？

Red Hat Enterprise 系统为每个允许访问系统的用户用户名，每个系统都有用户组。用户组是一个或多个用户的组。用户可以是多个组的成员。正如第 4 章“理解 Linux 概念”中“文件权限”节所述，可以为文件所有者、文件关联组和系统所有用户授予目录权限。

用户组可以是你决定的任何分组：部门用户、相同物理位置的用户或基于安全访问的用户组。在实施之前，为公司规划用户组是非常重要的。如果更改不当，会导致文件的组权限错误。

### 管理用户

Red Hat Linux 系统上的每个用户都分配有一个唯一的用户标识，称为 UID。500以下的 UID 留给系统用户，如 root 用户。系统用户还包括为特定服务添加的用户，例如 NFS 服务的 nfsnobody、rpc 和 rpuser。

在 Red Hat Linux 中，默认添加用户时会创建一个私组——这意味着创建一个同名的用户组，且新用户是该组中的唯一用户。

Red Hat Linux 包含一个管理用户和组的图形化程序。这需要 `system-config-users` 包。当用户自动选择 RHEL Web 或 YUM 时安装它。从桌面顶部面板的系统菜单中选择管理、用户和组来启动用户组工具，或执行命令 `system-config-users`。如果以 root 用户身份运行程序，在提示时输入 root 密码。如图 9.1 所示，所有现有用户列在用户选项卡上。

默认情况下，用户不在列表中显示。要在列表中显示用户，从下拉菜单中选择编辑、选项。在选项对话框中，取消勾选隐藏系统用户和组并点击关闭。

### 添加和修改用户

要添加新用户，点击添加用户显示图 9.2 中的对话框。

为新用户配置用户名、全名和密码。新用户的默认登录 shell 为。创建 `/home/username/` 作为用户的家目录，并为该用户创建一个私组。这些选项可以如图 9.2 所示进行修改。系统会自动为用户选择 500 以上的 UID。要手动设置 UID，选择手动指定 ID 然后选择一个 UID。点击确定将用户添加到系统。该用户会立即出现在主窗口的用户选项卡上，并被添加到系统中。

# 管理用户 207

![](img/60a952f475fd10259ba425768b115659_216_0.png)

图 9.1 现有用户列表

![](img/60a952f475fd10259ba425768b115659_216_1.png)

图 9.2 添加新用户

要为新用户或任何现有用户配置更高级的用户选项，请从列表中选择该用户并点击属性。会出现图 9.3 所示的对话框，显示当前为功能配置选项。账户过期、密码锁定、密码过期以及用户所属的组等功能都可以在用户属性对话框中配置。

![](img/60a952f475fd10259ba425768b115659_217_0.png)

图 9.3 修改用户属性

# 删除用户
