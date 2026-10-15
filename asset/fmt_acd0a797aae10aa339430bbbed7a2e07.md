
- `firstboot`: 如果启用，设置代理（Setup Agent）将在系统首次启动时运行。
- `reboot`, `halt`: 指定安装完成后要采取的操作。

> **注意**：在 Kickstart 文件中，缺失值会导致安装程序进行交互式提示回答。

## 第 12 章 安装 Red Hat Enterprise Linux

### 将 KICKSTART 文件发布到 ANACONDA

通过将 Kickstart 文件放置在以下位置之一，使安装程序能够使用该文件：

- 安装时通过 FTP、HTTP 或 NFS 可访问的网络服务器。
- 可用的 USB 盘或 CD-ROM。
- 待安装系统上的本地硬硬盘。

安装程序必须访问 Kickstart 文件以开始自动化安装。最常用的方法是使用网络服务器，如 FTP、Web 或 NFS 服务器。网络服务器便于 Kickstart 文件的维护，因为可以对其进行更改，并立即用于未来的多次安装。

在 USB 或 CD-ROM 上提供 Kickstart 文件也十分方便。Kickstart 文件可以嵌入到用于启动安装的介质中。然而，当 Kickstart 文件发生变化时，你必须生成新的安装介质。

在本地磁盘上提供 Kickstart 文件可以让你快速地重建系统。

### 启动 ANACONDA 并指向 Kickstart 文件

一旦选择了 Kickstart 方法，将通过向安装内核传递 `inst.ks=LOCATION` 参数来告诉安装程序 Kickstart 文件的位置。某些示例为：

- `inst.ks=http://server/dir/file`
- `inst.ks=ftp://server/dir/file`
- `inst.ks=nfs:server/dir/file`
- `inst.ks=hd:device/dir/file`
- `inst.ks=cdrom:device`

![](img/3c5dfc78dee328600013666607c8aa7b_379_0.png)

**图 12.4：** 安装期间指定 Kickstart 文件的位置

对于使用 Virtual Machine Manager 或 virt-manager 的虚拟机安装，可以在“URL Options”下方的框框中指定 Kickstart URL。在安装物理机时，启动安装介质并按 Tab 键中断启动过程。向安装内核添加 `inst_ks=LOCATION` 参数。

### 参考文献

- 《执行高级 RHEL 安装》中的 Kickstart 安装基础章节，地址：https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/performing_an_advanced_rhel_installation/kickstart-installation-basics_installing-rhel-as-an-experienced-user#kickstart-installation-basics_installing-rhel-as-an-experienced-user
- 附录 B 中安装程序配置和流控制章节下的 Kickstart 命令。《执行高级 RHEL 安装》中的 Kickstart 命令和选项参考，地址：https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/performing_an_advanced_rhel_installation/kickstart-installation-basics_installing-rhel-as-an-experienced-user#kickstart-commands-for-installation-program-configuration-and-flow-control-kickstart-commands-and-options-reference
- 《执行高级 RHEL 安装》中的启动选项章节，地址：https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/8/html-single/performing_an_advanced_rhel_installation/kickstart-installation-basics_installing-rhel-as-an-experienced-user#kickstart-and-advanced-boot-options-installing-rhel-as-an-experienced-user

## 第 12 章 | 安装 Hat Enterprise Linux

### 引导练习

#### 使用 KICKSTART 实现自动化安装

在本实验中，你将创建一个 kickstart 文件并验证其语法。

##### 成果

你应该能够：

- 创建一个 kickstart 文件。
- 使用 `kswalidator` 验证 kickstart 文件的语法。

##### 准备工作

使用密码 `student` 以 student 用户身份登录。

在工作站上，运行 `lab installing-kickstart start` 命令。该命令运行一个启动脚本来确定 servera 机器在网络上是否可用。它会验证 servera 上是否安装并配置了 Apache。

```
[student@workstation ~]$ lab installing-kickstart start
```

1. 使用 `ssh` 命令以 student 用户身份登录 servera。系统已配置为使用 SSH 密钥进行身份验证，因此不需要密码。

```
[student@workstation ~]$ ssh student@servera

...省略输出...

[student@servera ~]$
```

2. 将 servera `/root/anaconda-cs.cfg` 复制到名为 `/home/student/kickstart.cfg` 的文件中，以便 student 可以编辑。使用 `sudo cat /root/anaconda-cs.cfg > ~/kickstart.cfg` 将 `/root/anaconda-cs.cfg` 的内容复制到 `/home/student/kickstart.cfg`。如果 `sudo` 提示 student 用户密码，请使用 `student` 作为密码。

3. 对 `/home/student/kickstart.cfg` 进行以下更改。

3.1. 注释掉重启指令：

```
#reboot
```

3.2. 注释 BaseOS 仓库的 repo 命令。将 AppStream 的 repo 内容修改为教室的 AppStream 仓库：

```
#repo --name="koji-override-0" --baseurl=http://download-node-0
```

## 第 12 章 | 安装 Red Hat Enterprise Linux

Red Hat 支持运行以下操作系统的虚拟机：

- Red Hat Enterprise Linux 6 及更高版本
- Microsoft Windows 10 及更高版本
- Microsoft Windows Server 2016 及更高版本

### 将 RED HAT ENTERPRISE LINUX 物理系统配置为虚拟化主机

管理员可以将 Red Hat Enterprise Linux 配置为虚拟化主机，适用于开发、测试、训练或需要同时在多个操作系统中工作的情况。

### 安装虚拟化工具

安装 virt yum 模块准备系统成为虚拟化主机。

```
[root@host ~#] yum module list

Name            Profiles        Summary

virt            rhel [d]         common [d]      Virtualization module

Hint: [d]default, [enabled], [x]disabled, [i]installed
[root@host ~#] yum module install virt

... omitted...
```

### 验证系统要求

KVM 需要带有 VT-X 和 Intel 64 扩展的 Intel 处理器（用于 x86 系统）或带有 AMD-V 和 AMD64 扩展的 AMD 处理器。使用 `virt-host-validate` 命令验证您的硬件并检查系统要求。

```
[root@host ~#] virt-host-validate

QEMU: Checking for hardware virtualization              : PASS
```
