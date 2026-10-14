

![](img/9129877170834ca9d5fdac5319bf5f12_609_0.png)

如果在 initrd 中未包含密钥，AutoYaST 安装将忽略 updates 目录中的文件，除非你在 AutoYaST 控制文件中包含接受未知密钥的指令：

```
<general>
<signature-handling>
<accept_unknown_gpg_key
config:type="boolean">true</accept_unknown_gpg_key>
</signature-handling>
```

8. 在安装过程中，选择 Add-on Products 然后选择 Add，以便在 Software 对话框中选择你的软件包。

## 配置 NFS 服务器

要通过 NFS 使目录可用，你需要完成以下步骤：

1. 编辑 /etc/exports 文件。该文件定义了哪些目录与哪些机器共享。你还可以定义限制；例如，你可以使目录变为只读。要了解该文件的语法，请查看命令 man 5 exports 的输出。

使 /export/sled10 目录对所有机器以只读模式可用的条目如下所示：

```
/export/sled10 *(ro,sync)
```

![](img/9129877170834ca9d5fdac5319bf5f12_609_1.png)

要了解该文件中可使用的其他选项，请查看 man 5 exports 手册页。

2. 通过输入以下命令启动 NFS 服务器
rcnfsserver start

3. 通过输入以下命令确保 NFS 服务器在系统启动时自动启动
insserv nfsserver

4. （条件性）如果 SuSEFirewall 正在运行，你必须启动 YaST，选择 Security and Users > Firewall，并在 Allowed Services 对话框中添加 NFS Server。如果省略这些步骤，客户端可能无法连接到你的 NFS 服务器。

## 使用安装服务器

要使用安装服务器，你需要在初始启动屏幕显示时指定服务器。使用 Down 键移动到 Installation；按 F3 然后按 F4。在菜单中，选择你想要使用的安装服务器类型，如图 15-4 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_610_0.png)

Figure 15-4

在出现的对话框中，输入服务器的主机名和服务器上的目录。根据服务器类型，你可能需要输入额外的参数。

代替在菜单中选择 NFS 并在对话框中输入 IP 地址和路径，你可以在 Boot Options 行中输入 `install=nfs://IP_address/path/`。

按 Enter 后，安装系统会连接到安装服务器并通过网络加载安装所需的所有文件。

![](img/9129877170834ca9d5fdac5319bf5f12_611_0.png)

## Exercise 15-2: Set Up an Installation Server

在本练习中，你将安装 DVD 的文件复制到一个目录，并使用 NFS 通过网络使该目录可访问。

创建 /export/sled10 目录。将 DVD 中的所有文件复制到此目录。编辑 /etc/exports 并启动 NFS 服务器以通过网络使这些文件可访问。

### Detailed Steps to Complete This Exercise

要设置安装服务器，请执行以下操作：

- 1. 在终端窗口中，运行 su -- 命令切换到 root（密码 n0v311）。
- 2. 通过输入以下命令创建 /export/sled10 目录
  `mkdir -p /export/sled10`
- 3. 插入 SUSE Linux Enterprise Desktop DVD。通过输入以下命令将 DVD 的内容复制到你刚创建的目录
  `cp -a /media/mountpoint/* /export/sled10`
- 4. 由于复制内容需要一些时间，请打开另一个终端窗口并切换到 root（su -，密码 n0v311）。
- 5. 编辑 /etc/exports 文件以添加以下行：
  `/export/sled10 *(ro,sync)`
- 6. 通过输入以下命令启动 NFS 服务器
  `rcnfsserver start`
- 7. 通过输入以下命令确保 NFS 服务器在系统每次启动时都启动
  `insserv nfsserver`

你也可以使用 YaST Runlevel Editor 代替 insserv。

## Objective 5—Automated Installation

要启动自动安装，请将 AutoYaST 控制文件提供给待安装的机器。这可以与任何安装方法结合使用，无论是从安装介质，还是网络中的安装服务器。

要执行自动安装，你需要：

- Provide the Control File
- Boot and Install the System

### Provide the Control File

存在多种使控制文件可用的方法。

一种方法是将文件复制到包含 FAT 文件系统格式的软盘中。

![](img/9129877170834ca9d5fdac5319bf5f12_612_0.png)

不要使用 Ext2 文件系统格式的软盘。

如果你在软盘上将文件命名为 autoinst.xml 并插入软盘，它将被自动使用。如果使用不同的名称，你必须在安装的启动提示符下的内核命令行中添加以下内容：

```
autoyast=floppy:///myconfig.xml
```

另一种使控制文件可用的方法是使用网络。这在与安装服务器结合使用时尤其有用。在这种情况下，内核命令行将类似于以下内容：

```
autoyast=nfs://10.0.0.254/export/sled10/myconfig.xml
```

### Boot and Install the System

一旦你创建并测试了控制文件，你有几个选项可以使用它来安装机器：

- Boot and Install from DVD
- Boot from DVD, Install from an Installation Server
- Boot via PXE, Install from an Installation Server

### Boot and Install from DVD

可以结合使用控制文件（在软盘上或导出的文件系统上）和安装 DVD 来启动和安装计算机。然而，对于大规模部署，这并不真正高效。虽然它节省了输入配置信息的时间，但你仍然必须从一台计算机走到另一台计算机，插入介质并手动启动安装。之后，你必须回来再次取出安装介质。

### Boot from DVD, Install from an Installation Server

即使使用 DVD 或软盘启动，安装服务器的优势在于你可以在实际安装开始后立即移除启动介质。

前提是你有一个在安装期间提供所有网络信息的 DHCP 服务器，步骤如下：

- 1. 将安装 DVD 插入你的机器并启动引导过程。
- 2. 在第一个启动屏幕上，选择 Installation（确保在 10 秒内完成；否则系统将从硬盘启动）。
- 3. 提供你希望与 AutoYaST 一起使用的信息。

在启动提示符下，输入以下参数（我们假设这里安装仓库可通过 NFS 从 10.0.0.254/export/sled10/ 获取，并且控制文件位于同一位置）：

```
autoyast=nfs://10.0.0.254/export/autoinst.xml
install=nfs://10.0.0.254/export/sled10
splash=verbose
```

最后一个参数在引导过程中切换到详细显示，以便你可以轻松查看引导消息。

短暂时间后，YaST 启动。此时，你可以移除启动介质。安装按常规进行，但由于控制文件，无需用户交互。经过一些检查后，软件包从 NFS 服务器复制。

系统在安装过程结束时重新启动。重新启动后，如果 AutoYaST 配置文件中未设置密码，你可能可以无需密码以 root 身份登录。在这种情况下，你应立即为 root 设置密码。

### Boot via PXE, Install from an Installation Server

使用 PXE 安装的优势在于你不必将单独的启动介质带到计算机上。通过合适的配置，你可以提供一个菜单来选择要安装的内容。

事实上，如果网卡支持 Wake on LAN，你甚至不必走到机器旁。

本课程不涵盖通过网络启动的支持设置。信息可在 /usr/share/doc/packages/autoyast2/autoyast.pdf 中找到。

![](img/9129877170834ca9d5fdac5319bf5f12_613_0.png)

## Exercise 15-3: Perform an Automated Installation of SLED 10

在本练习中，你将执行 SUSE Linux Enterprise Desktop 10 的自动安装。

如果你的机器上存在你在课程期间创建并希望保留的任何文件，请将它们复制到外部介质（如 USB 闪存盘），因为在本练习后它们将被删除。

在本练习中，你将与合作伙伴一起工作。一台机器充当安装服务器；另一台将被重新安装。

如果没有合作伙伴（例如在自学环境中），你可以将安装服务器设置在 da1 虚拟机上，或使用 DVD 作为安装介质。

### Detailed Steps to Complete This Exercise

要开始安装 SUSE Linux Enterprise Desktop 10，请执行以下操作：

- 1. 确定你将使用哪台机器作为安装服务器，哪台机器将被重启。
- 2. 在将充当安装服务器的机器上，创建 /export/sled10/autoyast/ 目录并将 autoyast 文件复制到此目录中作为 sled10.xml。

