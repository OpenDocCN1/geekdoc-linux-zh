
GRUB 的一个很棒的地方在于，你可以交互式地管理引导过程。这是 LILO 无法很好做到的事情。你不必局限于 `menu.lst` 或 `grub.conf` 文件中配置好的内容，你可以随时定制自己的引导过程。要做到这一点，请完成以下操作：

- 在 GRUB 菜单中，按 `esc` 键。
- 当提示你正在离开图形化引导菜单时，选择确定。这样做时，将显示基于文本的 GRUB 菜单，如图 6-8 所示。

**图 6-8**

基于文本的 GRUB 菜单

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_240_0.png)

- 如果你想要编辑菜单项，请按 `E`。这样做时，将显示图 6-9 中的屏幕。

在此屏幕上，你可以使用向上或向下箭头选择适当的行，然后再次按 `E` 进行编辑。如果你想要添加一行，请按 `O`。按 `D` 删除一行。当你准备好开始引导过程时，请按 `B`。你也可以按 `ESC` 返回到 GRUB 菜单。

**图 6-9**

编辑 GRUB 菜单项

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_240_1.png)

- 你还可以通过按 `c` 访问 GRUB 提示符。这样做时，将显示图 6-10 中的屏幕。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_241_0.png)

你可以在 `grub>` 提示符下输入 `help` 来显示有关从 `grub>` 提示符创建 GRUB 菜单行的信息。你还可以按 `TAB` 查看可以在 `grub>` 提示符下输入的命令列表。你也可以按 `ESC` 返回到 GRUB 菜单。

> **注意** 你也可以从正在运行的 Linux 系统中访问 `grub>` 提示符。要做到这一点，只需在 shell 提示符下输入 `grub` 即可。

GRUB 菜单可以是一个极其有用的工具。在大多数发行版中，GRUB 菜单中默认显示引导选项字段。示例如图 6-11 所示。

你可以使用此字段向 Linux 内核发送未包含在 GRUB 菜单项中的引导选项，以定制内核的工作方式。要做到这一点，你首先选择所需的 GRUB 菜单项，然后在引导选项字段中输入想要使用的适当内核选项。例如，如果你的 Linux 系统由于某种未知原因无法再引导，你可以使用引导选项字段来告诉内核在启动时不要加载 `init` 进程，而是加载另一个程序。

> **注意** 我们将在本章后面更详细地讨论 `init` 进程。

要做到这一点，你在引导选项字段中输入 `init=program_name`。例如，要跳过加载 `init` 进程并改为加载 `bash` shell，你需要在引导选项字段中输入 `init=/bin/bash`。当你引导系统时，`bash` shell 会被加载，你将拥有对系统的完整 `root` 级别访问权限，允许你诊断和修复导致系统无法正常引导的问题。这如图 6-12 所示。

> **提示** 系统不会提示你提供 `root` 密码。因此，如果你忘记了 `root` 用户的密码，可以使用此技术来救援系统。

**图 6-12**

用 `bash` shell 替换 `init`

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_241_1.png)

然而，请注意，在某些发行版中，根 (`/`) 文件系统将以只读模式挂载。如果是这种情况，你需要在 shell 提示符下输入 `mount -o remount,rw,sync -t filesystem device_name mount_point` 以将其重新挂载为读写模式，然后才能修改配置文件。进行必要的更改后，你可以通过在 shell 提示符下输入 `exec /sbin/init` 来让内核通过 `init` 恢复正常的引导过程。

虽然定制 GRUB 及其菜单项的能力非常有用，但也可能存在一些安全风险。如上所述，它可能会在无需提供密码的情况下赋予任何知道如何操作的人 `root` 级别的系统访问权限。这可能是一件非常糟糕的事情，尤其是在可能包含敏感或专有信息的 Linux 系统上。

为了提高 GRUB 菜单的安全性，你可以添加 GRUB 密码。一旦配置完毕，只有在提供正确的密码后，你才能修改 GRUB 引导选项。最简单的方法是编辑 GRUB 配置文件（`menu.lst` 或 `grub.conf`）并输入以下内容：

```
password password
```

例如：

```
password natasxa01
```

请注意，在配置文件中添加此参数将导致 GRUB 以纯文本模式显示其菜单。示例如图 6-13 所示。

当 GRUB 以这种方式配置时，用户仍然可以在没有密码的情况下选择任何菜单项，但编辑任何 GRUB 菜单项都将要求他们输入你指定的密码。如果你还想要求用户在选择菜单项之前输入密码，你需要在 GRUB 配置文件中适当的 `title` 元素内添加 `lock` 参数，如本例所示：

```bash
fs2:~ $ cat /boot/grub/menu.lst
###### Modified by YaST2. Last modification on Wed Jan 19 10:37:45 MST 2011
###### THIS FILE WILL BE PARTIALLY OVERWRITTEN by perl-Bootloader
###### Configure custom boot parameters for updated kernels in
/etc/sysconfig/bootloader

default 0
timeout 8
##YaST - generic_mbr
gfxmenu (hd0,1)/message
##YaST - activate
password natsas80l

###Don't change this comment -- YaST2 identifier: Original name: linux###
title Desktop -- openSUSE 11.3 -- 2.6.34-12
  lock
  root (hd0,1)
  kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 resume=/dev/sda1
  splash=silent quiet showopts vga=0x317
  initrd /boot/initrd-2.6.34-12-desktop
###Don't change this comment -- YaST2 identifier: Original name: failsafe###
title Failsafe -- openSUSE 11.3 -- 2.6.34-12
  lock
  root (hd0,1)
  kernel /boot/vmlinuz-2.6.34-12-desktop root=/dev/sda2 showopts sppm=off
  nomresume edd=off powersaved=off nohz=off highres=off processor.max_cstate=1
  nomodeset x11failsafe vga=0x317
  initrd /boot/initrd-2.6.34-12-desktop
###Don't change this comment -- YaST2 identifier: Original name: floppy###
title Floppy
  lock
  rootnoverify (fd0)
  chainloader +1
fs2:~ $
```

**图 6-13**

在 GRUB 配置文件中使用密码

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_242_0.png)

在此配置中，用户必须输入你指定的密码才能选择一个 GRUB 菜单项。这是通过按下 `P` 键然后输入相应密码来完成的。如果他们不这样做，将会显示图 6-14 中所示的屏幕。

请注意在前述示例中，`password` 指令放置在文件的全球部分（global section）。这定义了其后所有 `title` 指令的密码。在此配置中，所有 GRUB 菜单项都使用相同的密码。如果你想为每个 GRUB 菜单项定义不同的密码，你可以将 `password password` 指令放置在每个 `title` 元素内。

同样请注意在前述示例中，密码是以明文形式存储在 GRUB 配置文件中。这稍微有些不安全。如果用户获取了 GRUB 配置文件的读取权限（默认情况下不应该如此，但事故确实会发生），那么他们就可以轻松获取你设置的 GRUB 密码。

为了使配置更加安全，你可以加密配置文件中的 GRUB 密码。这样，即使用户访问了 GRUB 配置文件，他们也无法读取你指定的密码。要加密密码，请执行以下操作：

1. 打开一个终端会话并切换到 `root`。
2. 在 shell 提示符下，输入 `grub-md5-crypt`。
