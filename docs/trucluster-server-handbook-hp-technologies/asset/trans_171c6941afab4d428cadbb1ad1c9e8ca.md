

## 5.4.4 选择要安装的软件

在安装的这一部分，我们会被提示选择将要安装的软件子集。

```
*** Software Selection ***
** Reviewing available software for:
Tru64 UNIX V5.1A Operating System ( Rev 1885 )
Please wait ...

The following options are available:
 o Select "All Software" to install all mandatory and all optional software for the operating system. You will be given the opportunity to view all software after selecting this option and to confirm your choice.
 o Select "Mandatory Only" to install the minimum required software. No optional software will be installed. You will be given the opportunity to view the mandatory software after selecting this option and to confirm your choice.
 o Select "Customize" to interactively select software from a numbered list of software subsets. You will then be given the opportunity to confirm your choices.
1) All Software
2) Mandatory Only
3) Customize
```

```
Enter your choice: 3
```

我们选择了“3”或“Customize”，因为我们想要选择将要安装的软件子集。

### 5.4.4.1 选择强制性软件子集

以下输出显示了自定义安装后将被安装的强制性软件组件：

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

### 5.4.4.2 选择部分可选软件子集

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

