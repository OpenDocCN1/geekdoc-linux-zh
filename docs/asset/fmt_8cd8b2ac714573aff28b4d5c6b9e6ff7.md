
```
subnet 192.168.0.0 netmask 255.255.255.0 {
  range 192.168.0.20 192.168.0.250;
}
```

在我的本地网络中，我使用了相同的子网，但我限制了可用网络地址范围用于其他本地系统。

# 第 20 章：虚拟机与终端服务器

根据需要，我可以使用 `domain-name` 指令指定本地网络的域，并使用 `domain-name-servers` 指令指定该客户端的 DNS 服务器。请替换适用于你网络的域名和 DNS 服务器地址：

```
option domain-name "example.com"
option domain-name-servers 192.168.0.1;
```

`broadcast-address` 指令如其名所示，用于分配广播地址。如果你配置了不同的网络，请记住为该网络替换相应的广播地址：

```
option broadcast-address 192.168.0.255
```

`subnet-mask` 指令可以覆盖之前的 `netmask` 指令，这对于被划分为更离散网络的网络非常有用。默认的 `subnet-mask` 指令与默认的 `netmask` 指令匹配。`routers` 指令指定网络的网关地址。请根据网络进行相应替换：

```
option routers 192.168.0.1
option subnet-mask 255.255.255.0
```

后续指令实际上是将 PXE 启动系统指向正确的文件和目录。默认根路径（`root-path`）通过 `ltsp-build-client` 命令配置：

```
option root-path "/var/tftpboot/ltsp/i386";
```

但对于与客户端相关的配置，以下指令将 PXE 启动系统指向正确的文件和目录：

```
option root-path "/var/tftpboot/ltsp/i386";
```

对于与 TFTP 服务器相关的客户端配置，需要如下：

```
option root-path "/var/tftpboot/ltsp/i386";
```

以下指令如下：

```
if substring(option-class-identifier, 0, 9) = "PXEClient" {
    filename "/ltsp/nbi";
} else {
```

配置好客户端后，可以通过以下命令启动相关服务：

```
option root-path "/var/tftpboot/ltsp/i386";
```

（注：由于原文中存在部分逻辑重复或断句，翻译时已根据上下文对指令逻辑进行了对齐，确保技术代码块的完整性）

# Linux 终端服务器项目

假设你正在运行前述描述的命令来安装 LTSP 服务器，你很快就会运行以下命令：

```
$ sudo ltsp-build-client
```

但现在先不要运行此命令，除非你已经阅读了将要使用的所有命令开关。如果你想在 `/var/lib/tftpboot` 目录下创建客户端，你需要添加 `--base /var/lib/tftpboot` 选项：

```
$ sudo ltsp-build-client --base /var/lib/tftpboot/ltsp
```

如果你正在为不同的架构构建客户端，请注意 `--arch` 开关。例如，当我在 AMD 64 位桌面系统上构建 i386 LTSP 客户端时，我运行了以下命令。如果你在 i386 架构的系统上运行，使用 `--arch i386` 开关也不会有任何影响。你还可以根据 `/usr/share/debootstrap/scripts` 目录下的脚本为不同的发行版设置服务器。

```
$ sudo ltsp-build-client --base /var/lib/tftpboot/ltsp --arch i386 \
--dist hardy --mirror http://mirrors.kernel.org
```

此命令需要几分钟或更长时间（取决于硬件能力）来构建客户端系统。在每个终端服务器首次重启后，你可能需要运行 `ltsp-update-image` 以及可能的 `ltsp-update-sshkeys` 命令。要更新相应的目录，请使用以下命令更新镜像：

```
$ sudo ltsp-update-image --base /var/lib/tftpboot/ltsp --arch i386
```

# 启动 LTSP 客户端

如果你使用之前描述的 PXE 启动，假设 DHCP 和 TFTP 服务器正在运行且没有被任何防火墙拦截，客户端网络应该会自动启动 LTSP 系统。成功后，你将看到类似于图 20-13 中的屏幕。

要排除 LTSP 客户端的问题，打开 `/var/lib/tftpboot/ltsp/i386/pxelinux.cfg` 目录下的默认文件。删除 `quiet` 和 `splash` 指令。下次启动 LTSP 客户端时，你将看到与启动过程相关的日志信息。换言之，它可以帮助你识别 LTSP 客户端在何处遇到问题。

![](img/28cf881509dedde88f9e34e8cefb7020_551_0.png)

## 总结

Ubuntu 提供了许多虚拟机选项。通常情况下，虚拟机包含一个被配置为硬盘的大文件。它还包含了 PC 主要组件的虚拟化版本。由于资源必须与主机系统共享，因此需要进行一些规划，以确保为主机以及你配置的任何虚拟客体都有足够的内存（RAM）。

两个流行的第三方选项是 VMware Server 和 VirtualBox。虽然 VMware Server 不是开源的，但它是免费提供的，且其创建者是虚拟化领域的领导者。相比之下，Ubuntu 包含了由 Sun Microsystems 开发的开源版 VirtualBox。两种解决方案都可以针对各种 Linux、Microsoft 以及其他操作系统进行定制。

Linux 系统原生虚拟化解决方案是 KVM 和 Xen。虽然 Ubuntu Hardy Heron 版本针对 KVM 进行了优化，但它要求系统具有多个 CPU 或具有硬件虚拟能力的多核 CPU。可以使用 `virt-install` 命令和虚拟机管理器（Virtual Machine Manager）来创建虚拟机。

无盘客户端需要配置相同的服务，包括 DHCP、NFS 和 TFTP。Ubuntu 的无盘客户端实现基于 Linux 终端服务器项目的工作。如果你认真对待 LTSP，请尝试 Ubuntu 的 Edubuntu 版本。

# 术语表

- 波浪号 (`~`) 代表当前活动用户的家目录。

- `aa-audit` 命令将 AppArmor 安全策略文件设置为审计模式（audit mode）。

- `aa-autodep` 命令建议一个 AppArmor 配置文件。

- `aa-complain` 命令将 AppArmor 安全配置文件设置为投诉模式（complain mode）。

- `aa-genprof` 命令生成一个 AppArmor 配置文件。

- `aa-status` 命令显示 AppArmor 状态。

- `aa-unconf` 命令将 AppArmor 配置文件设置为无限制模式（unconfined mode）。

- **访问控制列表 (ACL)** 在 Linux 中，访问控制列表 (ACL) 定义了权限。

### Ubuntu 服务器管理

- **地址解析协议 (ARP)** 地址解析协议将 IP 地址映射到硬件地址。

- **高级配置和电源接口 (ACPI)** 高级配置和电源接口 (ACPI) 允许电源管理。

- **AppArmor** AppArmor 是由 Novell 开发的强制访问控制 (MAC) 系统。

- **Alpha 版本** 对于大多数软件而言，Alpha 版本是用于测试的早期版本。

- **备用 CD**  Alternate CD 包含了安装程序。

- `apache2ctl` 命令可启动、停止和优雅地重启 Apache 服务。

- `apt-cache` 命令在所有仓库中搜索包信息。

- `apt-file` 命令使用包数据库搜索文件。

- `apt-ftarchive` 命令创建一个仓库。

- `apt-get` 命令允许安装和移除软件包。

- `apt-mirror` 命令可以创建仓库的本地镜像。

- `aptitude` 命令可以作为许多 apt-* 命令的前端。

### Ubuntu 服务器管理
