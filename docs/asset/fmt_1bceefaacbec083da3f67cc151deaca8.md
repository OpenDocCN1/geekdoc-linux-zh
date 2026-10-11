
商业发行版中大多数的包管理器都使用这种方法。遵循这种方法的包管理器示例包括 RPM（顺便说一下，它是 Linux 标准基准规范所需的）、`pkg-utils`、`Debian` 和 Gent 的 Portage 系统。关于如何为 LFS 系统采用这种风格的包管理的提示位于 `http://www.linuxfromscratch.org/hints/downloads/files/fakeroot.txt`。

创建包含依赖信息的软件包是复杂的，这超出了 LFS 的范围。Slack 使用基于 tar 的系统来处理软件包存档。该系统刻意没有像复杂的包管理器那样处理软件包依赖关系。有关 Slack 软件包管理细的详细信息，请参阅 `http://www.slackbook.org/html/package-management.html`。

## 6.3.2.7. 使用基于的管理

这种方案是 LFS 特有的，由 Matthias Benmann 设计，并可以在 Hints 项目中找到。在这种方案中，每个软件包都作为一个单独的用户安装到标准位置。通过检查用户 ID（UID），可以轻松识别属于某个软件包的文件。这种方法的优点和缺点过于复杂，无法在本节中详细描述。更多细节请参阅 `http://www.linuxfromscratch.org/hints/downloads/files/more_control_and_pkg_man.txt` 中的提示。

## 6.3.3. 在多个系统上部署 LFS

LFS 系统的优势之一是，磁盘系统上的文件位置没有差异文件。要将 LFS 克隆以构建另一台与基础系统架构相同的计算机，只需在包含根目录的 LFS 分区（一个基础 LFS 构建解压缩后为 250MB）上使用 `tar`，通过网络传输或 CD-ROM 将其拷贝到新系统并解压。从这一点起，必须更改一些配置文件。可能需要更新的配置文件有：`/etc/hosts`、`/etc/fstab`、`/etc/passwd`、`/etc/group`、`/etc/shadow`、`/etc/ld.so.conf`、`/etc/sysconfig/rc.site`、`/etc/sysconfig/network` 以及 `/etc/sysconfig/ifconfig.eth`。

根据硬件差异和原始内核配置，可能为新系统构建自定义内核。

> 有报告指出，在相似但非完全相同的架构之间拷贝时会出现问题。例如，Intel 系统的指令与 AMD 处理器并不相同，且某些处理器的后续版本可能包含早期版本中不可用的指令。

最后，必须通过第 8.4 节“使用 GRUB 设置引导过程”使新系统变得可引导。

## 6.4. 进入 chroot 环境

现在是进入 chroot 环境开始构建和安装最终的 LFS 系统了。以 root 用户身份运行以下命令，进入目前仅包含临时工具的领域：

```
chroot "$LFS" /tools/bin/env -i \
HOME=$root \
TERM=$TERM \
PS1=\u:\w$ \
PATH=$usr/bin:/usr/sbin:/usr/bin:/tools/bin \
/tools/bin/bash --login -h
```

`env` 命令的 `-i` 选项将清除 chroot 环境的所有变量。之后，将设置 `HOME`、`TERM`、`PS1` 和 `PATH` 变量。`TERM=$TERM` 将 chroot 内部的 TERM 变量设置为与外部相同的值。这是 `vim` 和 `less` 等程序正常运行所必需的。如果需要其他变量（例如 `CFLAGS`），这里是再次设置它们的好地方。

从现在开始，不再需要使用 `$LFS` 变量了，因为所有工作将受限制在 LFS 文件系统中。因为 Bash 已经被告知 `$LFS` 现在就是根（`/`）目录。

注意 `/tools/bin` 位于 `PATH` 的最后。这意味着一旦安装了最终版本，临时工具将不再被使用。这发生在 shell 不“记住”已执行二进制文件位置的情况下——为此原因，通过向 `bash` 传递 `+h` 选项关闭了哈希功能。

注意 `bash` 提示符会显示 I have no name!（我没有名字！）。这是正常的，因为 `/etc/passwd` 文件尚未创建。

- 本章剩余部分及后续章节中的所有命令必须在 chroot 环境内运行，这一点。。如果由于原因离开了此环境（例如重启），请确保按照第 6.2.2 节“挂载并填充 `/dev`”和第 6.2.3 节的说明挂载了虚拟内核文件系统。

## 6.5. 创建目录

是时候为 LFS 创建目录结构了。为了 LFS，我们使用以下命令创建必要的目录：

```bash
mkdir -p /dev /etc /lib /lib64 /root /opt /var /usr /usr/local /usr/bin /usr/sbin /usr/lib /usr/lib64 /usr/include /usr/share /usr/sbin
```

## 6.6. 创建文件

有些程序使用了硬编码的路径。为了满足这些需求，创建一些符号链接：

```bash
ln -s /tools/bash /bin/bash
ln -s /tools/cat /bin/cat
ln -s /tools/echo /bin/echo
ln -s /tools/pwd /bin/pwd
ln -s /tools/stty /bin/stty
ln -s /tools/perl /usr/bin/perl
ln -s /tools/lib/libgcc.so.1 /usr/lib/libgcc.so.1
ln -s /tools/lib/libstdc++.6 /usr/lib/libstdc++.6
ln -s /tools/lib/libstdc++.la /usr/lib/libstdc++.la
```

每个链接的作用：

- `/bin/bash`：许多 `bash` 脚本指定 `/bin/bash`。

- `/bin/cat`：Glibc 配置脚本硬编码了它。

- `/bin/echo`：为了满足 Glibc 测试套件中的某项测试需要。

- `/bin/pwd`：某些配置脚本（特别是 Glibc 的）硬编码了此路径。

- `/bin/stty`：Expect 使用此路径，因此为了 Binutils 和 GCC 测试套件的通过。

- `/usr/bin/perl`：许多 Perl 脚本硬编码了 `perl` 程序的路径。

- `/usr/lib/libgcc.so.1`：Glibc 需要它来线程库。

- `/usr/lib/libstdc++.6`：Glibc 测试套件中的几项测试以及 GMP 的 C++ 支持需要它。

- `/usr/lib/libstdc++.la`：在安装 GCC 后，防止 `/usr/lib/libstdc++.la` 中出现工具引用。

- `/bin/sh`：许多 shell 脚本硬编码了 `/bin/sh`。

运行以下命令创建 `/etc/passwd` 文件：

```
cat /etc/passwd << "EOP"
root:x:0:0:root:/root:/bin/bash
bin:x:1::dev/null:/bin/false
daemon:x:6:6:Daemon User:/dev/null:/bin/false
messagebus:x:18:18:D-Bus Message Daemon User:/var/run/dbus:/bin/false
nobody:x:99:99:Unprivileged User:/dev/null:/bin/false
EOP
```

root 的实际密码（这里使用的 "x" 只是一个占位符）

运行以下命令创建 `/etc/group` 文件：

```bash
cat /etc/group << "EOP"
root:x:0:
bin:x:1:daemon
sys:x:2:
kmem:x:3:
tape:x:4:
tty:x:5:
daemon:x:6:
floppy:x:7:
disk:x:8:
lp:x:9:
dialout:x:10:
audio:x:11:
video:x:12:
utmp:x:13:
usb:x:14:
cdrom:x:15:
mad:x:16:
messagebus:x:18:
syssystemd-journal:x:23:
input:x:24:
mail:x:34:
nogroup:x:99:
users:x:999
EOP
```

创建的组并不是任何标准的一部分——这些组部分取决于本章中 Udev 配置的要求，以及许多 Linux 发行版的约定。此外，某些测试仅依赖特定的用户或组。Linux 标准基础（LSB，可用 `http://www.linuxbase.org`）仅建议存在组 ID (GID) 为 0 的 root 组 GID 为 1 的 bin 组。所有其他组和 GID 都可以由系统管理员选择。良好的程序不依赖 GID 数字，而是使用组名。

要移除“I have no name!”提示，请启动一个新的 shell。由于在第 5 章中安装了完整的 Glibc 并且已经创建了 `/etc/passwd` 和 `/etc/group` 文件，现在用户名和组名解析将可以工作了：
