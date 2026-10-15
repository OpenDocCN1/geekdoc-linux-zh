
```
The following base operating system subsets are mandatory and will be installed automatically unless you choose to exit without installing any subsets:
* AdvFS Kernel Modules
* Base System
* Base System - Hardware Support
* Base System Management Applications and Utilities
* Basic Networking Configuration Applications
* Basic Networking Services
* Basic X Environment
* CDE Desktop Environment
* CDE Mail Interface
* CDE Minimum Runtime Environment
* Compaq Management Agents Version 2.1b
* Compiler Back End
* DECwindows 100dpi Fonts
* DECwindows 75dpi Fonts
* Doc. Preparation Tools
* Graphical Base System Management Utilities
* Graphical Print Configuration Application
* Graphical System Administration Utilities
* Hardware Kernel Header and Common Files
* Hardware Kernel Modules
* Java 1.1.8-10 Environment
* Kernel Header and Common Files
* Local Printer Support
* Logical Storage Manager Kernel Modules
* NFS(tm) Configuration Application
* NFS(tm) Utilities
* Netscape Communicator V4.76
* PCXAL Keyboard Support
* Service Tools
* Standard Kernel Modules
* Tcl Commands
* Tk Toolkit Commands
* Tru64 UNIX Base System
* X Fonts
* X Servers Base
* X Servers for PCbus
```

```
Space used after mandatory subsets (root/usr/var): 81.3 MB/307 MB/4.9 MB
```

#### 5.4.4.2 选择部分可选软件子集

在安装的这一部分，我们会被提示选择被视为 Tru64 UNIX 操作可选的软件子集。

由于我们希望集群能够增长和扩展以满足当前及未来的计算需求，我们建议安装所有与硬件相关的子集，这样如果您添加具有不同硬件配置的系统，它将被自动识别，而无需安装额外的软件子集。我们还建议您通过阅读 Tru64 UNIX 安装指南附录 C 中子集的描述，运用最佳判断来确定要安装哪些软件子集。换句话说，在进行安装之前，花时间规划您将要安装的内容。您应该真正了解并理解系统上将安装哪些软件以及原因。

> NOTE:
>
> The output shown is from a V5.1A installation. The number of subsets will differ from version to version.

可选的 Tru64 UNIX 软件子集按以下类别分组：

- General Applications
- Kernel Build Environment
- Kernel Software Development[^4]
- Mail Applications
- Network-Server/Communications
- Obsolete Components
- Printing Environment
- Reference Pages
- Software Development
- Supplemental Documentation
- System Administration
- Text Processing
- Windowing Environment
- Windows Applications

以下输出被删减以节省一棵或两棵树。每个类别将包含一个或多个可供选择的子集。

![](img/a0df85c2e542a8d6c913113908553aa4_119_0.png)

[^4] Subsets cannot be chosen in the initial installation.

已使用空间 (`root/usr/var`): 93.6 MB/589 MB/10.1 MB

添加到您的选择中，或按 RETURN 键确认选择。

输入 `c` 取消您的选择并重新显示此菜单。

选择（例如 `1 2 4-6`）：`1 3-4 6 8-9 12 14 18-39 41-49 51-55 57-59 62 63`

#### 5.4.4.3 验证可选软件子集

安装软件会要求我们确认是否要安装所有选定的软件子集，并确认这些软件子集将被加载以进行安装。

```
The following subsets will be loaded:
```

此时，将显示选定的（以及强制的）子集，随后是所需的磁盘空间，以及一个用于确认选择是否正确的提示。（输出已被截断。）

```
Space required in (root/usr/var): 93.6 MB/600 MB/10.3 MB

Are these the software subsets that should be loaded (y/n) ? Y
```

既然我们已经选择了所有想要安装的内容，我们应该已一切就绪。对吧？嗯，还不完全是。

### 5.4.5 选择要构建到 UNIX 内核中的内核选项

现在我们已经告诉安装软件要安装的软件子集，接下来需要告诉它，在完成所有软件子集的安装和配置后，如何构建 UNIX 内核。如下面的输出所示，有三个选择。

```
*** Kernel Options Selection ***

The following options are available:

 o Select "All Options" to automatically build all mandatory and all optional kernel components into the tailored kernel.

 o Select "Mandatory Only" to automatically build only the mandatory kernel components into the tailored kernel.

 o Select "Customize" to manually select the optional kernel components. You will be prompted for your selection later in the installation process after all software subsets have been loaded and the system has been rebooted from the new system disk. The mandatory kernel components will be automatically included in the custom-built kernel.
```

```
1) All Options
2) Mandatory Only
3) Customize
```

```
Enter your choice: 3
```

我们将选择选项“3”来选择我们知道将要使用的内核选项。只选择需要的内核选项可以生成更小的 UNIX 内核，与使用所有内核选项构建的内核相比，它可能具有更好的性能和更高的效率。

> **注意：**
>
> 选择选项“1”或“2”时，安装程序将在不要求您进一步输入的情况下构建内核。换句话说，一旦安装过程开始，它将在无人值守的情况下继续运行。选择选项“3”时，安装过程将在构建内核之前停止，以请求要添加到内核的选项。

### 5.4.6 选择用于操作系统文件系统的文件系统类型

接下来的几个提示涉及我们是否使用逻辑存储管理器（LSM）、我们将使用哪种文件系统类型，以及本地系统磁盘的文件系统布局。关于 LSM 的提示用于封装操作系统磁盘。由于在创建集群期间，这不会传播到集群磁盘，因此我们建议您在出现提示时回答“否”。
