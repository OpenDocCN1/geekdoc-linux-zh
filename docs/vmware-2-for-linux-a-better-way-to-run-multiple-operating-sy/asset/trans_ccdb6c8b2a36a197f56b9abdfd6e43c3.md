

![](img/b2b6702758c230ce537468351fc8af15_280_0.png)

Figure 13.14 Before you load FreeBSD for the first time, use the network configuration tools to assign IP information to your bridged networking or PPP device.

图 13.14 在首次加载 FreeBSD 之前，使用网络配置工具为你的桥接网络或 PPP 设备分配 IP 信息。

> If you elect to enable NFS service, you are given the opportunity to edit /etc/exports. You might need to consult FreeBSD documentation to configure this file because FreeBSD's /etc/exports file uses a different format than Linux. If you are an NFS novice, consult Appendix B, "File Sharing with Samba and NFS in VMware," for information on configuring your Linux host as an NFS server.

> 如果你选择启用 NFS 服务，你将有机会编辑 /etc/exports。你可能需要查阅 FreeBSD 文档来配置此文件，因为 FreeBSD 的 /etc/exports 文件使用与 Linux 不同的格式。如果你是 NFS 新手，请参阅附录 B，“在 VMware 中使用 Samba 和 NFS 进行文件共享”，以获取有关将你的 Linux 主机配置为 NFS 服务器的信息。

- 23. Leave your console options set to the default, for now, when asked. Configure your time zone as appropriate.

- 23. 被询问时，暂时将控制台选项保持为默认值。按需配置你的时区。

- 24. When you are asked about Linux binary compatibility, I suggest enabling it. (You'll have a much easier time finding programs to run in FreeBSD if you enable this.) This requires additional loading from the FreeBSD CD-ROM.

- 24. 当被询问关于 Linux 二进制兼容性时，我建议启用它。 （如果你启用此功能，在 FreeBSD 上找到可运行的程序会容易得多。）这需要从 FreeBSD CD-ROM 额外加载。

- 25. Answer Yes when prompted about the mouse, and follow the simple instructions to test and configure the mouse driver.

- 25. 被提示关于鼠标时回答 Yes，并按照简单的说明测试和配置鼠标驱动。

- 26. Answer Yes to X Server configuration, and use the shell-based xf86config tool. Follow the on-screen instructions. Because you have not yet installed VMware Tools, configure a generic 16-color VGA display adapter and low-spec VGA monitor.

- 26. 对 X Server 配置回答 Yes，并使用基于 shell 的 xf86config 工具。按照屏幕上的说明操作。由于你尚未安装 VMware Tools，请配置通用的 16 色 VGA 显示适配器和低规格 VGA 显示器。

![](img/b2b6702758c230ce537468351fc8af15_281_0.png)

Other versions of FreeBSD might have slightly different X configuration sequences. In general, remember to always choose the most low-end, basic VGA options possible until you can install VMware Tools and the advanced X server support.

FreeBSD 的其他版本可能具有略有不同的 X 配置序列。总的来说，请记住在能够安装 VMware Tools 和高级 X 服务器支持之前，始终选择尽可能低端、基础的 VGA 选项。

27. If you want to install more software, answer Yes when asked to browse the collection of programs. Install anything that looks useful to you from the screen shown in Figure 13.15, or wait. You can always install more applications later.

27. 如果你想安装更多软件，被询问是否浏览程序集合时回答 Yes。从图 13.15 所示的屏幕中安装任何对你有用的程序，或稍后再说。你随时可以稍后安装更多应用程序。

![](img/b2b6702758c230ce537468351fc8af15_281_1.png)

If you are inclined to work with Samba networking, be sure to install the Samba package from the net hierarchy of software.

如果你倾向于使用 Samba 网络，请务必从软件的 net 层级中安装 Samba 包。

28. When the software packages are finished, enter at least one user's login account information in the standard user editor, shown in Figure 13.16, when prompted.

28. 软件包完成后，被提示时在图 13.16 所示的标准用户编辑器中输入至少一个用户的登录账户信息。

29. All that remains is some cleanup work. Set the root password when asked, and then ask to return to the installation menu. If you plan to use FreeBSD for any serious graphical work, you might want to use the Configure option on the installation menu to call up Desktop Settings and install either GNOME or KDE.

29. 剩下的只是一些清理工作。被询问时设置 root 密码，然后请求返回安装菜单。如果你计划将 FreeBSD 用于任何严肃的图形工作，你可能想使用安装菜单上的 Configure 选项调出桌面设置并安装 GNOME 或 KDE。

![](img/b2b6702758c230ce537468351fc8af15_281_2.png)

Figure 13.15 FreeBSD, like Linux, offers a wide range of freely distributed software that can be installed during the OS setup.

图 13.15 FreeBSD 与 Linux 一样，提供大量可自由分发的软件，可在操作系统设置期间安装。

![](img/b2b6702758c230ce537468351fc8af15_282_0.png)

Figure 13.16 Add at least one non-root user.

图 13.16 添加至少一个非 root 用户。

30. When you are satisfied with your installation, select Exit Install on the main menu. Remove the FreeBSD CD-ROM and let the computer restart. FreeBSD starts to boot, as pictured in Figure 13.17.

30. 当你对安装满意时，在主菜单上选择 Exit Install。取出 FreeBSD CD-ROM 并让计算机重新启动。FreeBSD 开始启动，如图 13.17 所示。

31. You can log in to FreeBSD. Figure 13.18 proves it.

31. 你可以登录到 FreeBSD。图 13.18 证明了这一点。

![](img/b2b6702758c230ce537468351fc8af15_282_1.png)

Figure 13.17 FreeBSD bootstraps itself on the virtual machine.

图 13.17 FreeBSD 在虚拟机上自行引导。

However you choose to get the archive onto the FreeBSD virtual disk, here's what you do next:

无论你选择如何将归档文件放到 FreeBSD 虚拟磁盘上，下一步操作如下：

- 1. From a shell-only login (don't start XWindows yet), cd to the directory containing the FreeBSD toolkit (I suggest you put it somewhere like /usr/vmware), and type tar xzf tools-for-freebsd-xxx.tar.gz, replacing the xxx with the appropriate number in the filename.

- 1. 从仅 shell 登录（暂时不要启动 XWindows），cd 到包含 FreeBSD 工具包的目录（我建议你将其放在像 /usr/vmware 这样的位置），并输入 tar xzf tools-for-freebsd-xxx.tar.gz，将 xxx 替换为文件名中的适当数字。

- 2. Step 1 creates a new subdirectory, vmware-freebsd-tools. Type cd vmware-freebsd-tools.

- 2. 第 1 步会创建一个新的子目录 vmware-freebsd-tools。输入 cd vmware-freebsd-tools。

- 3. Become root using the su command. (You might simply want to log in as root before performing this procedure; normally people recommend against it, but it's a fresh new installation of the OS. If something does go terribly wrong, there's no big loss.)

- 3. 使用 su 命令成为 root。 （你可能只想在执行此过程之前以 root 身份登录；通常人们不建议这样做，但这是一个全新的操作系统安装。如果出现严重错误，也没有太大损失。）

- 4. Type ./install.pl to start the installation.

- 4. 输入 ./install.pl 开始安装。

- 5. You should be able to simply answer with the defaults when the tools installer asks for the paths to various pieces of software.

- 5. 当工具安装程序询问各种软件的路径时，你应该只需使用默认值回答即可。

- 6. When the installation is complete (see Figure 13.19), reboot the FreeBSD virtual machine. (Just type reboot.)

- 6. 当安装完成后（参见图 13.19），重新启动 FreeBSD 虚拟机。 （只需输入 reboot。）

- 7. Before you can run X, you need to adjust the XF86Config file, usually found in /etc on FreeBSD systems. Edit the file /etc/XF86Config.

- 7. 在你能够运行 X 之前，需要调整 XF86Config 文件，通常在 FreeBSD 系统的 /etc 中找到。编辑文件 /etc/XF86Config。

- 8. Scroll down to the heading labeled Section "Monitor" and ensure that there is a listing for the screen resolution you want to use. (The format is ModeLine "resolution," where resolution should ideally match the screen size you use in Linux.) Make a note of the name in quotes after Identifier because you need it in Step 10.

- 8. 向下滚动到标题为 Section "Monitor" 的位置，并确保列出了你想要使用的屏幕分辨率。 （格式为 ModeLine "resolution"，其中 resolution 理想情况下应与你在 Linux 中使用的屏幕尺寸相匹配。）记下 Identifier 之后引号中的名称，因为你在第 10 步需要它。

![](img/b2b6702758c230ce537468351fc8af15_284_0.png)

Figure 13.19 When the VMware Tools installation is complete, as shown here, type reboot.

图 13.19 当 VMware Tools 安装完成后，如图所示，输入 reboot。

