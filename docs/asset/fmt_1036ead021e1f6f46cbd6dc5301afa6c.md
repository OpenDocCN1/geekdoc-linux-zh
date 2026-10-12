
```
[root@redhat /etc]# rpm -qi kernel
Name     : kernel
Version    : 2.2.14
Release    : 5.0
Install date: Wed 01 Nov 2000 06:58:30 PM EST
Group      : System Environment/Kernel
Size       : 11973135
Packager   : Red Hat, Inc. <http://bugzilla.redhat.com/bugzilla>
Summary    : The Linux kernel (the core of the Linux operating system).
Description :
The kernel package contains the Linux kernel (vmlinuz), the core of your
Red Hat Linux operating system.  The kernel handles the basic functions of
the operating system: memory allocation, process allocation, device
input and output, etc.
Relocations: (not relocatable)
Vendor: Red Hat, Inc.
Build Date: Tue 07 Mar 2000 09:13:08 PM EST
Build Host: porky.devel.redhat.com
Source RPM: kernel-2.2.14-5.0.src.rpm
License: GPL
```

如果您想显示您尚未安装的软件包的此信息，请使用 `-p` 选项。

```
rpm -qp package_file.rpm
```

### 打印软件包脚本

某些软件包包含在安装前或安装后运行的脚本。要显示这些脚本，请使用以下命令：

```
rpm -qp --scripts package_file.rpm
```

例如，要显示当软件包 `kernel-2.2.14-5.0.i686.rpm` 安装时运行的脚本，您将执行以下操作：

```
[root@redhat /root]# rpm -qp --scripts
/mnt/cdrom/RedHat/RPMS/kernel-2.2.14-5.0.i686.rpm
preinstall script (through /bin/sh):
/sbin/modprobe loop 2>/dev/null >/dev/null
exit 0
postinstall script (through /bin/sh):
cd /boot
ln -sf vmlinuz-2.2.14-5.0 vmlinuz
ln -sf System.map-2.2.14-5.0 System.map
ln -sf module-info-2.2.14-5.0 module-info

# Allow clean removal of modules directory
preuninstall script (through /bin/sh):
rm -f /lib/modules/2.2.14-5.0/modules.dep
```

### 验证软件包文件

您有时需要检查自软件包安装以来文件是否已更改。您可能对某些配置文件进行了更改，现在需要知道哪些被修改了。`rpm` 工具通过 `-V` 验证选项提供此功能。

```
rpm -V package_name
```

当执行验证时，`rpm` 检查已安装文件的一系列特征，并显示那些已更改的文件以及已更改的项目。每个文件在 `RPM` 数据库中都有一个条目，存储其 `MD5` 校验和、文件大小、符号链接指针、修改时间、用户和组所有者，以及权限和文件类型。如果文件是设备，则还会检查主要和次要设备号。表 3-1 显示了针对任何已更改文件的验证输出。

#### 表 3-1 软件包验证特征

| 项目 | 含义 |
| :--- | :--- |
| `.` | 此特征无变化 |
| `S` | `MD5` 校验和已更改 |
| `L` | 文件大小已更改 |
| `D` | 符号链接已更改 |
| `D` | 设备主要和/或次要号已更改 |
| `U` | 用户所有者已更改 |
| `G` | 组所有者已更改 |
| `M` | 权限和/或文件类型已更改 |

例如，要查看由 `setup` 软件包安装哪些配置文件已更改，您将输入以下内容：

```
[root@redhat /etc]# rpm -V setup
S.5....T c /etc/hosts.allow
......G c /etc/profile
S.5....T c /etc/services
```

此输出显示，对于 `hosts.allow` 文件和 `services` 文件，文件大小、`MD5` 校验和和修改时间已更改。对于 `profile` 文件，组所有者已更改，但其他未变。

要通过使用软件包文件名验证软件包，请使用 `-p` 选项。

```
rpm -Vp package_file.rpm
```

要验证系统上安装的每个软件包，请使用 `-a` 选项。这是查看自系统安装以来哪些文件已更改的快速方法。

```
rpm -Va
```

### 从源代码软件包创建二进制软件包

并非所有 `RPM` 软件包都分发二进制文件。有些分发电源码和安装脚本，让您构建自己的二进制 `RPM`。当您想要优化或更改软件包时，这些很有用。这些软件包具有略微不同的命名方案，因为它们不依赖于特定的系统架构。

```
package-version-patch.src.rpm
```

源代码 `RPM` 的安装方式与二进制软件包相同，使用 `rpm -i` 命令。这将不同的部件放入 `/usr/src/redhat` 目录层次结构中。表 3-2 显示了此树中目录的用途。

> **考试提示**
>
> 对于考试，您应该知道如何从源代码软件包构建二进制软件包，包括如何修改 `spec` 文件。

#### 表 3-2 `/usr/src/redhat` 树中的子目录

| 目录 | 用途 |
| :--- | :--- |
| `/usr/src/redhat/SOURCES` | 包含应用程序源代码 |
| `/usr/src/redhat/SPECS` | 包含 `RPM` `spec` 文件 |
| `/usr/src/redhat/BUILD` | 源代码构建的位置 |
| `/usr/src/redhat/RPMS` | 包含最终的二进制 `RPM` |
| `/usr/src/redhat/SRPMs` | 包含过程中构建的源代码 `RPM` |

软件包的 `spec` 文件控制软件包如何编译以及在安装或移除时运行的脚本。此文件命名为 `/usr/src/redhat/SPECS/package_name.spec`。`spec` 文件有八个部分，如表 3-3 所示。

#### 表 3-3 `spec` 文件部分

| `spec` 文件部分 | 描述 |
| :--- | :--- |
| `Header` | 一般信息，如摘要、名称、版本等 |
| `Prep` | 在执行编译过程前进行任何必要工作的 `Shell` 脚本 |
| `Build` | 构建 `spec` 文件并编译源代码的命令 |
| `Install` | 在系统上安装软件所需的命令 |
| `Clean` | 可选命令，用于清理构建环境，以防此软件包再次重新构建 |
| `Optional Install and Uninstall Scripts` | 可能在软件包安装或卸载期间运行的脚本 |
| `File List` | 软件包中的文件列表 |
| `Changelog` | 您对软件包所做任何更改的日志 |

### Debian 软件包管理

#### 2.2 安装与软件包管理

- **使用 Debian 软件包管理。** 使用 `Debian` 软件包管理系统，通过命令行（`dpkg`）和交互式工具（`dselect`）。

    - 能够查找包含特定文件或软件包；从档案中选择和获取它们；安装、升级或卸载它们；获取状态信息，如版本、内容、依赖项、完整性、安装状态；并确定安装了哪些软件包以及特定文件来自哪个软件包。能够在 `Debian` 系统上安装非 `Debian` 软件包。涉及使用以下命令和程序：`dpkg`、`dselect`、`apt`、`apt-get`、`alien`。涉及检查或编辑以下文件和目录：`/var/lib/dpkg/*`。

`Debian` 发行版及其基于它的发行版使用的软件包系统与 `Red Hat` 使用的不同。`Debian` 系统通常被认为更强大、更健壮。该系统中最常使用的四个组成部分如下：

- `dpkg`
- `dselect`
- `apt-get`
- `alien`
