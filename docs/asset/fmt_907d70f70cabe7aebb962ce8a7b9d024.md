
```
c:\vmware
c:\vmware\windows2000master
c:\vmware\windows2000vm1
c:\vmware\windows2000vm2
```

- 4. 为你的第一台虚拟机创建一个目录并将剩余的（`.vmx` `.sav` 和 `nvram` 等）文件移入该目录。原始目录现在为空。

- 5. 现在用编辑器打开第一台虚拟机的 `.vmx` 文件并找到指定虚拟磁盘的行。在我的示例中，这是 `IDE0:0` 磁盘：

```
ide0:0.fileName = "Windows 2000 Professional.vmdk"
```

用指向主 VMDK 文件的完整路径编辑此行。

```
ide0:0.fileName =
"c:\vmware\windows2000master\Windows
  2000
  Professional.vmdk"
```

- 6. 使用第一台虚拟机的 `.vmx` 配置文件打开 VMware。在虚拟机设置中，为此虚拟机锁定快照。

![](img/25fe75b93b97a021effaba85db112a52_114_0.png)

Figure 7.5: Locking a snapshot is only available in Workstation version 4.x and GSX Server 3.x.

图 7.5：锁定快照仅在 Workstation 版本 4.x 和 GSX Server 3.x 中可用。

7. Copy the `.vmx` file (and if important for your configuration, also the `nvram` bios file) to the directory for the second virtual machine.

7. 将 `.vmx` 文件（如果对你的配置很重要，还包括 `nvram` bios 文件）复制到第二个虚拟机的目录中。

8. You can now power both virtual machines on. They will both read from the shared master disk, but all changes to the disk will go into `.REDO` files which you will find in the virtual machine directory for each machine. This happens because the `.REDO` files do not have an absolute path; instead, they are stored in a path relative to the machine (the VM directory itself).

8. 现在你可以同时启动这两个虚拟机。它们都将从共享的主磁盘读取，但对磁盘的所有更改都将写入 `.REDO` 文件，你可以在每个机器的虚拟机目录中找到这些文件。这是因为 `.REDO` 文件没有绝对路径；相反，它们存储在相对于机器的路径中（即 VM 目录本身）。

```
ide0:0.redo=".\Windows 2000 Professional.vmdk.REDO_a03292"
```

> Tip: If you use the configuration with a separate swap disk for your guest operating system (as described in section 9.1: “Performance tips”) in combination with this shared disk setup, then assign every virtual machine a separate swap disk and set the disk to be an independent. Keep the swap disk `.vmdk` file in the directory with the virtual machine configuration files. This way, the swap disk will not be affected by the snapshot. There is no need to keep the page file contents consistent between pre and post Snapshot configurations.

> 提示：如果你在这种共享磁盘设置中同时使用为来宾操作系统单独的交换磁盘的配置（如第 9.1 节“性能提示”中所述），则为每个虚拟机分配一个单独的交换磁盘并将磁盘设置为独立。保留交换磁盘 `.vmdk` 文件在与虚拟机配置文件相同的目录中。这样，交换磁盘将不受快照影响。无需在快照前后的配置之间保持页面文件内容一致。

> Tip: Copying the virtual machines will make exact copies of everything in the operating system, including the identity, SID, computer name, IP address, etc. All these settings can be re-configured to allow the virtual machines to work simultaneously. If there is no need for the machines to interact with each other (the network, or the host), leave the configuration in place and set the network interfaces to different host-only networks.

> 提示：复制虚拟机会对操作系统中的所有内容进行精确复制，包括身份、SID、计算机名、IP地址等。所有这些设置都可以重新配置以允许虚拟机同时工作。如果机器之间无需相互交互（网络或主机），请保留配置并将网络接口设置为不同的仅主机网络。

For example, you can run a virtual machine on `VMnet5` without having to set up `VMnet5` in your host operating system. This configuration procedure is explained in section: 11.2 “Configure host-only and bridged networking”.

例如，你可以在 `VMnet5` 上运行虚拟机，而无需在主机操作系统中设置 `VMnet5`。此配置过程在第 11.2 节“配置仅主机和桥接网络”中进行了说明。

### 7.3 Using Virtual Disk Manager

#### 7.3 使用虚拟磁盘管理器

This utility enables you to work with virtual disks outside of the VMware Workstation environment. Typically only your guest virtual machines have access to the virtual disks. With this program you can access them directly from the command line. Some of the main features of the VMware Virtual Disk Manager utility are:

此实用程序使你能够在 VMware Workstation 环境之外处理虚拟磁盘。通常只有来宾虚拟机可以访问虚拟磁盘。通过此程序，你可以直接从命令行访问它们。VMware 虚拟磁盘管理器实用程序的主要功能包括：

- Expanding the size of virtual disks.

- 扩展虚拟磁盘的大小。

- Converting virtual disks from dynamically growing to fixed size and vice versa.

- 将虚拟磁盘从动态增长转换为固定大小，反之亦然。

- Create, modify, and defragment virtual disks from a command line utility which you can use to script virtual disk operations.

- 从命令行实用程序创建、修改和碎片整理虚拟磁盘，你可以使用它来脚本化虚拟磁盘操作。
