

## 文件系统

尽管 Linux 系统中的所有文件都连接成一个整体的目录树，但该树的某些部分可能位于不同的存储设备上，例如硬盘或 CD-ROM。特定存储设备上的文件被组织成所谓的 文件系统。文件系统是一个已格式化的设备，具有自己的目录和文件树。你的 Linux 目录树可能包含多个文件系统，每个文件系统位于不同的存储设备上。在一个具有多个分区的硬盘上，你将为每个分区拥有一个文件系统。文件本身被组织成一个无缝的目录树，从根目录开始。例如，如果你将 CD-ROM 连接到系统，一个路径名将直接从硬盘分区的文件系统上的根目录通向 CD-ROM 文件系统中的文件。

> 提示 在 Linux 中，你可以挂载不同类型的文件系统，包括由其他操作系统创建的文件系统，如 Windows、IBM OS、Unix 和 SGI。在 Linux 内部支持多种文件系统，包括 ReiserFS 和 ext3 等几种日志文件系统。

文件系统将其文件组织在其自己的目录树中。你可以将其视为必须附加到主目录树的子树。该树在你专门将其连接之前，与系统的目录树保持分离。例如，带有 Linux 文件的软盘具有自己的目录树。你需要将此子树附加到硬盘分区上的主树上。在它们连接之前，你无法访问软盘上的文件。

## 文件系统层次结构标准

Linux 将其文件和目录组织成一个从根目录开始并延伸到系统和用户目录的整体互连树。系统目录的组织和布局由文件系统层次结构标准（Filesystem Hierarchy Standard，FHS）确定。FHS 提供了一个标准化的布局，所有 Linux 发行版在设置其系统目录时都应遵循该布局。例如，必须有 /etc 目录来保存配置文件，以及 /dev 目录用于设备文件。你可以在 www.pathname.com/fhs 了解有关 FHS 的更多信息，包括官方文档。Linux 发行版、开发人员和管理员都遵循 FHS，以为 Linux 文件系统提供一致的组织。

Linux 使用多个特定命名的目录用于专门的系统管理任务。所有这些目录都位于你的主 Linux 文件系统最顶层，即用单个斜杠 / 表示的文件系统根目录。例如，/dev 目录保存设备文件，而 /home 目录保存用户主目录及其所有用户文件。你只能以系统管理员身份访问这些目录和文件（尽管用户通常只有只读访问权限）。你需要以 root 用户登录，将自己置于一个特殊的 root 用户管理目录 /root 中。从这里，你可以访问 Linux 文件系统上的任何目录，无论是管理目录还是用户目录。

## 根目录：/

根目录 / 中包含的子目录在表 30-1 中列出，同时还有其他有用的子目录。作为管理员，你可能经常访问的目录有保存配置文件的 /etc 目录、保存设备文件的 /dev 目录，以及

| Directory | Function |
|---|---|
| / | Begins the file system structure—called the root. |
| /boot | Holds the kernel image files and associated boot information and files. |
| /home | Contains users' home directories. |
| /sbin | Holds administration-level commands and any commands used by the root user. |
| /dev | Holds file interfaces for devices such as the terminal and the printer. |
| /etc | Holds system configuration files and any other system files. |
| /etc/opt | Holds system configuration files for applications in /opt. |
| /etc/X11 | Holds system configuration files for the X Window System and its applications. |
| /bin | Holds the essential user commands and utility programs. |
| /lib | Holds essential shared libraries and kernel modules. |
| /lib/modules | Holds the kernel modules. |
| /mnt | Used to hold directories for mounting file systems like CD-ROMs or floppy disks that are mounted only temporarily. |
| /opt | Holds added software applications (for example, KDE on some distributions). |
| /proc | Process directory, a memory-resident directory containing files used to provide information about the system. |
| /tmp | Holds temporary files. |
| /usr | Holds those files and commands used by the system; this directory breaks down into several subdirectories. |
| /var | Holds files that vary, such as mailbox, Web, and FTP files. |

TABLE 30-1 Linux File System Directories

以及保存 DNS、Web、邮件和 FTP 服务器数据文件，以及系统日志和计划任务的 /var 目录。对于管理不同版本的内核，你可能还需要访问 /boot 和 /lib/modules 目录以及 /usr/src/linux。/boot 目录保存你安装的任何新内核的内核映像文件，而 /lib/modules 目录保存不同内核的模块。

## 系统目录

你的 Linux 目录树包含某些目录，其文件用于不同的系统功能。对于基本系统管理，你应该熟悉用于存放应用程序的系统程序目录、系统配置目录（/etc）

