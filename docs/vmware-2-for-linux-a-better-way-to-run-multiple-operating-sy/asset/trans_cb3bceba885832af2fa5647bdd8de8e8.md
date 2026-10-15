

在所有现代版本的 Windows 中，微软都贴心地包含了一个命令行 FTP 程序，几乎与 Linux 中的 ftp 命令完全相同。你可以通过打开 MS-DOS 窗口（或根据你的 Windows 版本打开命令提示符）并输入 ftp IP_address_of_host 来访问主机计算机的 FTP 服务器。如果你的 Windows 虚拟机仅运行主机专用或桥接网络，而不两者兼有，请务必使用合适的宿主机 IP。

如果你希望 FTP 成为在 Linux 与 Windows 客户机之间共享文件的主要方法，可能需要更强大的工具。来自 Ipswitch, Inc. 的 WS_FTP（http://www.ipswitch.com）是领先的图形化、易于使用的 FTP 程序之一。你也可以考虑 LeechFTP，这是一款免费的、面向“高级用户”的 FTP 客户端。图 9.1 显示了在 Windows 98 虚拟机上运行的 LeechFTP。

> LeechFTP 可从 http://linux.fh-heilbronn.de/~debis/leechftp 获取。

如果你担心在桌面上开放 FTP 服务器的安全问题，可以改为在虚拟机上运行 FTP 服务器。虽然在客户机 VM 上运行服务器软件效率不高，但更安全（因为很少有人知道 VM 的存在，而且它可能并非全天候运行）。为了增加保护，你可以让服务器运行在仅主机网络的 VM 上，这使其对世界其他地方实际上不可访问。

![](img/b2b6702758c230ce537468351fc8af15_172_0.png)

图 9.1 FTP 客户端是向虚拟机传输和接收文件的有效方式。

> 许多 Windows 服务器程序会在桥接和主机专用网络上同时响应请求，因此如果 Windows 虚拟机上同时安装了这两种网络类型，外网 LAN 将能够访问服务器软件。

Windows NT 和 2000 Server 具有专门的服务器级 FTP 服务器，如果你需要测试生产环境，可以进行调查。但对于一般的、文件交换、轻量级使用，诸如 Dragon Server 之类的共享软件服务器对于任何 32 位版本的 Windows 都完全适用。

以下是让 Dragon Server 运行起来的方法：

> 你需要一个处理 zip 文件归档的程序，例如 WinZip 或适用于 Windows 的 PKZip 来安装 Dragon Server。你可以从 http://www.hotfiles.com 或 http://www.download.com 等共享软件站点下载一个。

- 1. 如果尚未启动，请启动你的 Windows VMware 会话。
- 2. 将附带的 CD 插入驱动器。
- 3. 使用我的电脑或 Windows 资源管理器打开 CD 并浏览到 Extras/Windows 目录。
- 4. 双击 drgnsrvr.zip 归档文件以打开文件（见图 9.2）。
- 5. 将内容复制到临时安装文件夹。
- 6. 双击 Setup 图标开始安装。会显示 Dragon Server 许可协议。阅读后关闭即可继续。
- 7. 如需更改安装目录，请更改，然后在图 9.3 所示的提供的框中输入你的姓名和电子邮件地址，然后单击继续。

![](img/b2b6702758c230ce537468351fc8af15_173_0.png)

图 9.2 Dragon Server 包含在一个小型的 ZIP 归档中。

![](img/b2b6702758c230ce537468351fc8af15_174_0.png)

图 9.3 安装 Dragon Server 需要一个简短的注册步骤。

8. 下一个窗口是服务器配置（见图 9.4）。你可以保留服务器主目录不变，但务必单击 FTP 旁边的框以启用 FTP 服务，并将 Max Users 设置为大于 0 的值。如果不做这两个更改，你将无法连接到 FTP 服务器！

![](img/b2b6702758c230ce537468351fc8af15_174_1.png)

图 9.4 务必启用 FTP 访问并允许超过零个用户登录。

9. 找到 Dragon Server 程序组（它应位于 Windows 开始菜单的程序下自己的组中）并启动服务器。

10. 在你能够通过 FTP 进入 Windows 虚拟机之前，需要设置至少一个登录名。单击工具栏中的 Users，并选择 Options 以打开图 9.5 所示的用户设置窗口。

![](img/b2b6702758c230ce537468351fc8af15_174_2.png)

图 9.5

