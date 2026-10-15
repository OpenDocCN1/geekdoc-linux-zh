

## 检查磁盘空间要求。
## 检查与已安装软件包的冲突。
## 检查 setuid/setgid 程序。

以下文件正在以 setuid 和/或 setgid 权限安装：

/opt/VirtualBox/amd64/VBoxHeadless <setuid root>
/opt/VirtualBox/amd64/VBoxNetAdpCtl <setuid root>
/opt/VirtualBox/amd64/VBoxNetDHCP <setuid root>
/opt/VirtualBox/amd64/VBoxNetNAT <setuid root>
/opt/VirtualBox/amd64/VBoxSDL <setuid root>
/opt/VirtualBox/amd64/VirtualBox <setuid root>
是否要将这些文件安装为 setuid/setgid 文件？
[y,n,?,q] y

这个软件包包含一些脚本，它们将在安装此软件包的过程中以超级用户权限执行。

是否要继续安装
<SUNWvbox>？ [y,n,?] y
正在将 Oracle VM VirtualBox 安装为 <SUNWvbox>
## 正在安装第 1 部分，共 1 部分。
/etc/hostname.vboxnet0
/opt/VirtualBox/64/VBoxPython.so
/opt/VirtualBox/64/VBoxPython2_4.so
/opt/VirtualBox/64/VBoxPython2_6.so
/opt/VirtualBox/LICENSE
/opt/VirtualBox/UserManual.pdf
输出已截断...
[ 正在验证类别 <manifest> ]
## 正在执行安装后脚本。
正在检查旧版本...
正在安装新版本...
检测到 Solaris 11 版本 175
正在加载 VirtualBox 内核模块...
  - 已加载：主机模块
  - 已加载：NetAdapter 模块
  - 已加载：NetFilter（Crossbow）模块
  - 已加载：USBMonitor 模块
  - 已加载：USB 模块
正在配置服务...
  - 已加载：区域访问服务
正在安装 MIME 类型和图标...
正在安装 Python 绑定...
  - 已安装：Python 2.6 的绑定
正在更新启动归档...
<SUNWvbox> 安装成功。

![](img/02e070097d401d3bf7de4bf1c470b267_1324_0.png)

**图 25.3** VirtualBox 虚拟机管理器界面。

![](img/02e070097d401d3bf7de4bf1c470b267_1324_1.png)

**图 25.4** 创建虚拟机向导。

![](img/02e070097d401d3bf7de4bf1c470b267_1324_2.png)

**图 25.5** 选择为虚拟机预留的内存大小。

在 VirtualBox 管理器或向导的任何界面中，你都可以随时点击“< Back”按钮返回上一步，或点击“Cancel”按钮终止新客户机虚拟机的创建。

- 2. 要创建新的客户机虚拟机，请点击“New”按钮启动“Create Virtual Machine”向导（[图 25.4](#)）。
- 
- 3. 由于我们的客户机虚拟机将安装 Solaris，请键入 `Solaris`。点击“Operating System”下拉菜单并选择“Solaris”。在“Version”下拉菜单中，选择“Oracle Solaris (64 bit)”。点击“Next >”按钮继续（[图 25.5](#)）。

基础内存大小必须更改为至少 1536 MB。如果你的系统有大量 RAM，可以使用更多内存。在我们的例子中，我们使用了 2000 MB。滑块下方绿色区域内的任何数值都被视为不会使计算机速度过慢的值。点击“Next >”按钮继续。

- 4. 下一个界面用于创建虚拟硬盘，即主机操作系统硬件上可供虚拟机客户机使用的磁盘空间量。如果这是你的第一个虚拟机，请保留默认选项“Create a virtual hard drive now”，然后点击“Create”继续。

- 5. 在下一个界面中，选择“VDI（Virtual Disk Image，虚拟磁盘映像）”，然后点击“Next”按钮。

- 6. 现在你可以选择“Dynamically allocated”（动态分配）或“Fixed size”（固定大小）存储。第一个选项会按需使用磁盘空间，直至达到你在下一个界面中设置的最大大小。第二个选项会创建一个与指定磁盘空间大小相同的磁盘，无论是否使用。如果你担心磁盘空间，请选择第一个选项；否则，选择第二个选项，因为它能让 VirtualBox 运行得稍快一些。点击“Next >”按钮继续。

- 7. 现在你可以设置虚拟机的大小（或上限）。如果你计划在虚拟机中安装 Solaris，请将大小增加到至少 100 GB，否则在 Solaris 安装期间会收到错误提示。无论你设置多大，请确保计算机有足够的空闲磁盘空间来支持它。使用文件夹图标浏览到磁盘上有足够空间容纳虚拟机的目录。

- 8. 做出选择并按下“Next”后，你将看到所选内容的摘要。如果你想更改任何值，可以使用“Back”按钮返回上一个界面。否则，点击“Create”关闭向导。你的虚拟机现在应该会出现在 VirtualBox 虚拟机管理器界面的左侧框中，如图 25.6 所示。

- 9. 配置存储设备：在我们的安装中，当我们想要从系统上已挂载在串行高级技术附件（SATA）端口 1 的 DVD 驱动器安装 Solaris 时，此步骤已自动配置。

你可能需要根据安装介质来配置它以使用该介质。点击“Storage”区域中的存储超链接（即“Storage”一词）

![](img/02e070097d401d3bf7de4bf1c470b267_1325_0.png)

图 25.6 用于 Solaris 的新虚拟机。

