

3. 运行 make_novell-client-conf_rpm 脚本，使用 /add-on/novell-client-conf 目录中包含的所有 .conf 文件创建一个 novell-client-conf-version_number.platform.rpm 文件（例如，novell-client-conf-1.0.0-0.i586.rpm）。

- a. 确保你是以 root 用户身份登录。
- b. 在终端中输入以下内容：

```
hash make_novell-client-conf_rpm
```

4. 使用以下任一方法安装 novell-client-conf-version_number platform.rpm 中包含的预配置设置：

- *在终端中手动安装*—从终端提示符输入以下内容（全部在一行中）：
  `rpm -i novell-client-conf-version_number.platform.rpm`
- *使用 ncl_install 脚本安装*—当你启动 ncl_install 脚本（位于 /opt/novell/ncl/bin 或你解压 Client 下载文件所在的目录中）时，它会在 /add-on/novell-client-conf 目录中查找 novell-client-conf-version_number.platform.rpm 并将其添加到作为 Client 安装的一部分所安装的 RPM 列表中。
- *使用 YaST 安装 Novell Client*—将新创建的 novell-client-conf-version_number.platform.rpm 的位置添加到 YaST 安装源列表中（在安装源选项中添加一个本地目录并将其指向包含 novell-client-conf-version_number.platform.rpm 的目录）。当 YaST 安装运行时，novell-client-conf-version_number.platform.rpm 将被添加为 Novell Client 选择中的 RPM 之一。

![](img/9129877170834ca9d5fdac5319bf5f12_528_0.png)

工作站上的 Novell Client 配置设置可随时使用 YaST 方法进行更新。

RPM 中包含的 .conf 文件会被复制到 /etc/opt/novell/ncl 目录，覆盖已存在于该处的同名文件。安装后还会将 slp.conf 文件复制到 /etc 目录，覆盖该文件。

![](img/9129877170834ca9d5fdac5319bf5f12_528_1.png)

现有文件的备份副本会保存在同一目录中，以便在需要时可以恢复到旧文件。

![](img/9129877170834ca9d5fdac5319bf5f12_529_0.png)

## Exercise 13-5: Install and Configure the Novell Client for Linux

在本练习中，你将安装和配置适用于 Linux 的 Novell Client。
练习的第一部分，安装适用于 Linux 的 Novell Client。从 3086 Student DVD2 复制安装文件到你的主目录，并使用 YaST 将文件集成作为附加产品。然后安装适用于 Linux 的 Novell Client。
第二部分，使用适用于 Linux 的 Novell Client 登录到 eDirectory 网络，更改你的 eDirectory 密码，并映射网络目录。
第三部分，配置适用于 Linux 的 Novell Client 以满足你的需求。

### Detailed Steps to Complete This Exercise

- Part I: Install the Novell Client for Linux Packages
- Part II: Use the Novell Client Tray Application
- Part III: Configure the Novell Client

### Part I: Install the Novell Client for Linux Packages

1. 在你的 daxx SLED 10 工作站上，插入 3086 Course DVD2。
2. 使用 Nautilus 浏览到 /home/geeko/。
3. 选择 File > Create Folder。
4. 输入文件夹名称 install_files。
5. 使用 Nautilus 浏览到并选择 /media/3086_CourseDVD2/exercises/3086_13/Novell-Client-Linux/。
6. 将 NCL_Disk 目录（及其所有内容）复制到你刚创建的 install_files 目录中。
7. 关闭 Nautilus。
8. 通过选择 Computer > More Applications > System > YaST 启动 YaST 控制中心。
9. 提示时，输入 root 密码 n0v311；然后选择 Continue。
10. 从左侧面板选择 Software；然后从右侧面板选择 Add-on Product。
11. 选择 Local Directory；然后选择 Next。
12. 在 Path to Directory or ISO image 字段中，输入或浏览并选择以下内容：
```
/home/geeko/install_files/NCL_disk/
```
13. 选择 OK。
14. （条件）如果出现 No Checksum Found 消息，选择 Yes。（可能需要重复多次。）
15. 当 Software Installation 对话框出现时，在 Search 字段中输入 novell；然后选择 Search。
16. 从右侧列表中，确保 novell-client 和 novell-client-script 包已选中（可能还有其他包也被选中）。
17. 选择 Accept。
出现 Changed Packages 对话框。
18. 选择 Continue。
等待包安装完成（可能需要几分钟）。
19. 当出现询问是否要安装或删除更多包的对话框时，选择 No。
20. 通过选择 Computer > Shutdown > Restart 重启计算机。
21. 当登录屏幕出现时，以 geeko 身份登录，密码为 novell。
你应该在系统托盘中看到 Novell Client 图标。如果由于某种原因托盘中没有出现红色 N 图标，请选择 Computer > More Applications > Novell Tray。

### Part II: Use the Novell Client Tray Application

你可以自定义 Novell Client 选项，例如 Novell Client Tray 应用程序在桌面或应用程序托盘中的位置。这可以通过 Novell Client Tray 应用程序完成。

你可以使用 Novell Client Tray 应用程序访问适用于 Linux 的 Novell Client 的许多功能。只需选择托盘中位于的红色 N 图标即可。

在本练习的这一部分，你将使用 Novell Client Tray 应用程序执行以下操作：

- Part A: Log In to an eDirectory Network
- Part B: Change Your eDirectory Password
- Part C: Map a Network Directory
- Part D: Disconnect from a Mapped Directory

#### Part A: Log In to an eDirectory Network

要登录到 DA-TREE eDirectory 树，请执行以下操作：

1. 从 DA1 SLES 10 主机，确保 DA-OES 虚拟机已开机并且你已以 admin 身份登录，密码为 novell。
注意：在课堂环境中，这将由讲师完成。
2. 从你的 DAxx SLED 10 工作站，通过选择系统托盘中的 Novell Client 图标（红色 N）打开 Novell Login 对话框。
3. 选择 Novell Login。
4. 选择 Advanced。图 13-29 显示了出现的内容。

![](img/9129877170834ca9d5fdac5319bf5f12_531_0.png)

Figure 13-29

5. 输入以下信息：
- User Name—geeko
- Password—novell
- Tree—DA-TREE
- Context—digitalairlines
- Server—10.0.0.252
6. 选择 OK。等待登录到 eDirectory 树。
7. 登录过程完成后，选择 Novell Client 图标；然后选择 Novell Connections。

图 13-30 显示了出现的内容。

![](img/9129877170834ca9d5fdac5319bf5f12_532_0.png)

Figure 13-30

8. 确保你看到连接到 DA-TREE 上的 DA-OES。
9. 选择 Close。

#### Part B: Change Your eDirectory Password

要更改你的 eDirectory 密码，请执行以下操作：

1. 选择 Novell Client 图标；然后选择 Change Password。
2. 在 Old password 字段中输入 novell。
3. 在 New password 字段中输入 11evon。
4. 在 Confirm 字段中再次输入 11evon。
5. 通过选择 OK 保存更改并退出。

#### Part C: Map a Network Directory

要映射网络目录，请执行以下操作：

1. 选择 Novell Client 图标；然后选择 Novell Map Directory。
图 13-31 显示了出现的内容。

![](img/9129877170834ca9d5fdac5319bf5f12_533_0.png)

Figure 13-31

2. 输入以下内容：
- Enter the location where the link will reside: /home/gecko/Documents
- Enter the name of the link or select a drive letter: DA-Shared
- Enter the server name and path to the directory you want to map: \\DA-OES\SYS:PUBLIC\

![](img/9129877170834ca9d5fdac5319bf5f12_533_1.png)

你也可以选择 Browse 按钮并找到你想要映射的目录。
3. 选择 Map。
出现一条消息，指示映射目录已创建。
4. 选择 OK。
映射的驱动器会出现在你的主目录（默认）中或你在第 2 步指定的目录中。

#### Part D: Disconnect from a Mapped Directory

要断开映射的目录，请执行以下操作：

1. 选择 Novell Client 图标；然后选择 Disconnect Novell Mapped Directory。
出现 Disconnect Novell Mapped Directory 对话框。
2. 选择 DA-OES\SYS:PUBLIC 目录；然后选择 Disconnect。
3. 选择 Close。

### Part III: Configure the Novell Client

要配置 Novell Client，请运行 Novell Client Configuration Wizard。它允许你配置文件浏览器、协议、登录、托盘应用程序和 OpenSLP 设置。

1. 从系统托盘中选择 Novell Client 图标（ ）；然后选择 System Settings。
2. 提示时，输入 root 密码 n0v311；然后选择 OK。
出现 Novell Client Configuration Wizard 对话框。
3. 选择 Start Wizard。
出现 Login Settings 页面。
4. 确保以下选项已选中：
- NMAS Authentication
- Advanced Button
- Integrated Login
- Display Integrated Login Results
5. 在 Login Defaults 部分，输入以下内容：
- Default Tree: DA-TREE
- Default Context: users.digitalairlines
6. 选择 Next。
7. 从 Map Settings 页面，接受默认设置；然后选择 Next。
8. 从 Protocol Settings 页面，接受默认设置；然后选择 Next。
9. 从 Tray Application Settings 页面，接受默认设置；然后选择 Next。
10. 从 File Browser Settings 页面，接受默认设置；然后选择 Next。
11. 从 Service Location Protocol (OpenSLP) Settings 页面，接受默认设置；然后选择 Next。
你将被返回到 Novell Client Configuration Wizard 页面。

