
## 598 第 15 章：系统管理

列在 `gid=` 之后的组是你当前的、或称为主组。你创建的任何文件都与此组关联。

**注意**
`newgrp` 命令的工作原理是每次运行时都会创建一个新的 shell。退出该新 shell 将带你回到你之前使用的 shell（和组）。如果你登录时间很长并频繁使用 `newgrp`，你可能会发现自己深陷在 shell 中，并在注销之前逐个退出每个 shell。

如果你在目录权限中设置了组 ID 位（第 80 页），那么在该目录中创建的所有文件将获得与目录相同的组。这是避免必须使用 `newgrp` 的方法，并可以设置为某些类型文件系统的默认行为。

### `/etc/mtab`
挂载表文件包含所有当前挂载设备的列表，命名为 `/etc/mtab`。当你不带任何参数调用 `mount` 时，`mount` 会查询此表并显示挂载设备列表。`mount` 和 `umount` 工具保持 `/etc/mtab` 的更新。

### `/etc/motd`
`/etc/motd` 文件包含当日消息（message of the day），每次有人登录时都会显示。该文件应该保持简短，因为用户往往会多次看到消息。通常 `/etc/motd` 由 `rc.m` 脚本自动创建。

### `/etc/pam.conf` 或 `/etc/pam.d/*`
`/etc/pam.conf` 文件指定了系统可能使用的 PAM（可插拔模块）应用程序的验证方法。或者，在 `/etc/pam.d` 目录下可能存在独立的配置文件。如果 `/etc/pam.d` 存在，则忽略 `/etc/pam.conf`。除非你了解如何配置 PAM，否则更改 `/etc/pam.conf` 或 `/etc/pam.d/*` 的内容可能会导致你的系统无法使用。目前只有少数 Linux 使用 PAM。

### `/etc/passwd`
`/etc/passwd` 中的每个条目占一行，有七个字段，描述系统的一个用户。冒号分隔每个字段与相邻字段。

```
login-name:password:user-ID:group-ID:comment:directory:program
```

`login-name` 是用户的登录名——用户在响应登录提示时输入的名称。`password` 是用户密码的加密副本，或者如果使用了影子密码（第 600 页），则为字符 `x`。虽然允许空密码字段，但为了更好的安全，请确保每个账户都有密码。

```
PS1='\h:\w$'

PS2='>'

alias ls='ls -F'

alias dir='ls -1'

umask 022
```

`/etc/profile`

## User-specific initialization files

These files reside in each user's home directory and contain customizations to each environment. Which files are used depend upon which shell is running. See the chapter for the specific details for.

## Run Command (rc) files

The init program executes a run command, or rc file each time it changes state or run. The level run scripts perform tasks as mounting filesystems (when the system goes multiuser), removing temporary files (after the filesystems are mounted), and unmounting filesystems (when the system is returned to single-user mode). The layout used to hold the system initialization varies with the distribution you install. There are three basic layouts.

The simplest layout, based on early releases of BSD, uses two files: `/etc/rc` and `/etc/rc.local`. The first file, `/etc/rc`, holds machine-independent initializations and rarely needs to be modified, while `/etc/rc.local` holds any special operations for initialization. Put any changes to your system initialization in `/etc/rc.local`.

The second method of handling the rc files is based on an adaptation to BSD UNIX from System V and puts all the rc files into the directory `/etc/rc.d`. This directory holds a number of shell scripts. For example, the `/etc/rc.d/rc.S` is a script that is executed when the system starts, while `/etc/rc.d/rc.M` is run when the system is brought up to multiuser mode.

The final method is based on UNIX V Release 4 and spreads the rc files across a series of directories. There is one directory for each level. For example, `/etc/rc.0` holds the rc scripts to run entering level 0.

To reduce the chance of the user inadvertently running a Trojan Horse program (page 584), the assignment to PATH in the above example puts `.` at the end of the list:

# `/etc/profile`

```bash
export OPENHOME=/usr/bin

export PATH=$PATH

PS1='\h:\w$'

alias ls='ls -F'

alias dir='ls -1'

umask 022
```

## `/etc/shadow`

Under normal circumstances the encrypted passwords stored in the `/etc/passwd` file provide adequate security. When an additional layer of security is called for, it can be provided by shadow passwords. If shadow passwords are used, the password fields in the `/etc/passwd` file are replaced with an `x`, and the encrypted passwords are stored in the `/etc/shadow` file. Unlike the `/etc/passwd` file, the `/etc/shadow` file must be readable - only by the Superuser. This makes the set of encrypted passwords inaccessible to all.

## 重要文件与目录 601

防止其他用户访问并防止他人使用与加密密码匹配的特殊程序。你不应该直接编辑此文件；而应该使用 shadow 密码支持提供的 `useradd` 和 `usermod` 等程序。除了加密密码外，shadow 密码文件还包含账户信息。每个条目有九个字段，用冒号分隔：

`login-name:password:last-mod:min:max:warn:inactive:expire:flag`

登录名（Login-name）是用户的登录名——密码是 `passwd` 工具存入此文件的加密密码。如果未经授权的访问不是问题，密码字段最初可以为空（`::`）。当用户登录时，他们可以运行 `passwd` 来选择密码。否则，你可以在超级用户（Superuser）身份运行 `passwd` 来为用户分配一个初始密码，用户可以更改它。

`last-mod` 字段是一个数字，表示最后修改密码的时间。`min` 值是更改密码前必须经过的最少天数；`max` 是密码前的最大天数；`warn` 指定在密码过期前多少（天）通知用户。如果密码过期且在 `inactive` 字段指定的的天数内没有尝试登录，则账户将失效且不允许登录。一旦发生这种情况，用户必须联系系统管理员来重新激活账户。`expire` 字段是一个数字，表示密码过期的时间，给出自 1970 年 1 月 1 日以来的天数。在 `expire` 字段指定的日期，账户也将失效。条目中的最后一个字段 `flag` 预留供以后使用。

如果你没有安装 shadow 密码并想安装，可以从 Linux SHADOW-HOWTO 获取获取和安装 shadow 密码系统的详细信息。请参阅第 918 页的“我如何使用 ftp 获取 Linux 软件和文档？”。

此文件包含 `fsck` 默认检查的文件系统列表。它也被 `mount` 和 `unmount` 工具用于获取有关它们要挂载和卸载的文件系统相关信息。

```
# cat /etc/fstab
/dev/sda swap swap defaults
/dev/hdb2 swap swap defaults
/dev/hdb1 / ext2 defaults
/dev/db4 /tmp ext2 defaults
/dev/hda1 /usr ext2 defaults
/dev/sda5 /usr/tmp ext2 defaults
/dev/sda1 /usr/X386 ext2 defaults
/dev/sda3 /usr/local ext2 defaults
/dev/sda6 /store ext2 defaults
/dev/hdb3 /home ext2 defaults
/dev/hda2 /C: msdos umask=000
/dev/scd0 /cdrom iso9660 u,auto,ro
none /proc defaults
```

## 602 第 15 章：系统管理

`/etc/fstab` 文件包含四个六六字段（前面的示例仅使用了前几个字段），字段用空格或制表符（TAB）分隔。从左到右，字段指定：

- 块设备名称，提供文件系统的物理位置（关于块设备的讨论请参阅第 587 页）
- 文件系统的挂载点，即存放挂载文件系统根（root）目录的目录名称
- 设备或文件系统类型
- 挂载文件系统时使用的任何选项
- 如果存在，一个数字用于确定 `dump` 工具（如果使用）何时备份该文件系统
- 如果存在，一个数字用于 `fsck` 工具确定检查文件系统的顺序

例如，在此处显示的示例 `/etc/fstab` 中，根文件系统（`/`）位于标识为设备 `/dev/hdb1` 的磁盘分区上，文件系统类型为 `ext2`。`/dev/hda2` 包含一个要挂载到目录 `/C:` 的 DOS 文件系统。一个光驱（文件系统类型为 `iso9660`）作为设备 `/dev/scd0` 存在，其选项表明任何用户都可以挂载该光驱设备（通常情况下，只有超级用户可以挂载文件系统），在系统启动时不应自动挂载该光驱，且该设备应作为只读（readonly）文件系统挂载。前两行显示了两个磁盘分区被保留为交换空间（swap space），用于为你的系统提供比物理内存更多的虚拟内存。

上述 `/etc/fstab` 的最后一行显示了一个带有 `none`（显示在第一个字段）和文件系统类型 `proc` 的特殊条目。该文件系统是特殊的。它不存在于任何磁盘上，而是 Linux 使用的一种方法，将计算机内存中的信息提供给程序和用户。例如，看起来像 `/proc/kcore` 的文件只是使用 Linux 访问方法访问计算机内存的一种。`ls -l /proc/kcore` 显示了你系统上的字节数。

`/vmlinux` 此文件包含启动系统时加载的 Linux 系统内核。名称中的最后一个字符（`z`）表示内核以压缩格式存储。未经过压缩的内核通常被命名为 `/vmlinux`。

`/sbin/shutdown` 使用此程序正常地关闭系统（第 593 页）。

## 603 日常系统管理

### 日常系统管理

除了启动和关闭系统外，你还有其他职责。本节涵盖了这些职责中最重要的部分。

### 备份文件

系统管理员最忽视的任务之一是定期对文件制作备份副本。备份副本在两种情况下至关重要：系统发生故障文件丢失，以及用户（或系统管理员）意外删除了文件。

你必须定期备份文件系统。备份文件通常存储软磁盘或磁带上，由你决定。具体的备份频率取决于你的系统和需求。标准是：“如果系统崩溃，你愿意丢失多少工作？”理想情况下，你应该每几分钟备份一次系统上的所有文件，这样你只会丢失几分钟的工作。

备份过程通常会减慢机器速度，并且需要你存储所使用的介质。使用系统的人越多，你应该越频繁地备份。常见的计划可能是每天执行一或两次部分备份，每周执行一次完整备份。在更改系统硬件或 Linux 内核之前，始终对系统进行完整备份，因为这些活动最可能导致严重问题。

部分备份制作自上次备份完成以来创建或修改的文件副本。完整备份制作所有文件的副本，无论何时创建或访问。

### 使用什么备份你的系统

传统的个人电脑使用软磁盘执行备份。然而，这是不可行的。如果你的系统有一个 GB 磁盘，执行一次完整备份需要 600 多张软磁盘。即使在备份时对文件进行压缩，软磁盘的数量也是无法管理的的。如果你的计算机连接到网络，那么你可以将备份写入到另一个系统的磁带驱动器中。在网络化计算机中经常这样做，以避免为网络中的每台计算机配备磁带驱动器的成本，并简化对许多计算机进行备份的管理。你可能希望使用磁带系统备份计算机。由于磁带驱动器可以持有数百兆字节到五 GB 或更多的数据，磁带简化了备份系统的任务，使你更有可能定期执行这项重要任务。备份的其他选项是光驱和可移动式硬盘。这些设备虽然在成本效益或存储容量上不如磁带系统，但它们提供了比磁带更便利且更优的性能。

# 604 第 15 章：系统管理

有很多工具可以帮助你备份系统，大多数工具都适用于上述任何一种介质。大多数 Linux 备份工具都是基于归档程序之一——`tar`、`cpio` 或 `afio`——并在这些基础程序的基础上增加了账目记录功能，以便方便地管理备份。

基于 `tar`、`cpio` 或 `afio` 的工具中，没有一个能完全满足你作为系统管理员的需求，某些备份工具并不依赖于这些程序。`taper` 工具非常方便，因为它能提供一个基于菜单的界面，引导你完成制作备份或从备份中恢复文件的过程。你还可以配置 `taper` 在深夜以无人值守的进程方式运行。

# tar、cpio 和 afio 工具

你可以使用这三种工具之一（`tar`、`cpio` 或 `afio`）来构建系统的完整备份或部分备份。每个工具程序都会创建一个包含（或归档化）其他文件的大文件。除了文件内容外，归档文件还包含其中每个文件的文件头部信息。这些文件头部信息可以在从归档中提取文件时使用，用于恢复文件权限和修改日期。归档文件可以保存到磁盘、直接写入磁带，或者在创建时发送到网络。

除了帮助备份系统外，这些程序对于将文件打包在一起发送到其他站点也非常方便。`tar` 程序经常用于此目的，互联网上提供的许多软件包都以 `tar` 归档包的形式打包。

`Tar`（磁带归档）工具从归档中存储和检索文件。它可以压缩归档以节省空间。你可以使用 `-f` 选项指定归档设备。如果你不指定归档设备，`tar` 将使用 `/dev/rmt0`。使用 `-f` 选项时，`tar` 将参数 `-f` 作为归档设备的名称。你可以使用此选项引用网络上另一台计算机系统上的设备。虽然 `tar` 有很多可用选项，但在许多情况下，你只需要其中几个。你可以通过以下命令查看完整列表：

```
$ tar --help
```

`tar` 的大多数选项可以以短形式（单个字母）或描述性单词的形式给出。描述性选项以两个破折号开头，如之前所示的 `--help` 选项。单字母选项可以组合成单个命令行参数，且不以破折号开头（尽管使用破折号也是好习惯）。尽管这两个命令看起来非常不同，但它们以相同的顺序指定 `tar` 选项。第一个版本将单字母选项组合成单个命令行参数，而第二个版本对相同的选项使用描述性单词。两个命令都告诉 `tar` 从 `/dev/st0` 磁带上生成一个 (t, list) 目录 (t, list)，并使用 `gzip` 解压文件。

```
$ tar -ztvf /dev/st0
```

```
$ tar --gzip --list --verbose --file /dev/st0
```
