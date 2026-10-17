
# LAB 177

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_186_0.png)

图 4：点击编辑按钮

出现网络适配器配置对话框（图 5）。

如果您的系统中安装了两个以上的以太网卡，您可以为您的以太网卡分配不同的设备名称。

- 6. 点击设备（Device）选项旁边的箭头按钮。会出现一个下拉列表（图 5）。
- 7. 为您的以太网卡选择设备名称。在我们的案例中，我们选择了 `eth1` 作为所选以太网卡的设备名称（图 6）。
- 8. 点击确定（OK）按钮，关闭网络适配器配置对话框（图 6）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_186_1.png)

图 5：网络适配器配置对话框

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_186_2.png)

图 6：输入设备名称

网络配置窗口再次出现（图 8）。出现一个下拉菜单。

- 9. 从菜单中选择文件（File）菜单。
- 10. 从文件菜单中选择保存（Save）按钮以保存网络配置窗口中的更改，如图 8 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_186_3.png)
![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_186_4.png)

图 7：打开文件菜单

图 8：选择保存选项

当您从文件菜单选择保存选项时，会出现一个对话框，通知您您的更改已保存，并建议您重启电脑（图 9）。

- 11. 点击确定（OK）按钮（图 9）。
- 12. 网络配置窗口再次出现（图 10）。
- 13. 从网络配置窗口菜单栏中选择文件（File）菜单。出现一个下拉列表（图 10）。
- 14. 点击下拉列表中的退出（Quit）选项以退出网络配置窗口（图 10）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_187_0.png)
![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_187_1.png)

**图 9：** 显示消息的对话框，网络配置窗口随之关闭。

**图 10：** 选择退出（Quit）选项

# LAB-6：使用 FTP 服务器

目标：

- 安装、配置并访问 FTP 服务器。

要求：

- 一台网络计算机
- Linux 操作系统
- FTP 服务器配置文件
- 一台客户端计算机

## 安装 FTP 服务器

执行以下步骤安装 FTP 服务器：

- 1. 打开终端（Terminal）窗口并进入 root 模式。
- 2. 在终端窗口中输入 `yum install vsftpd` 命令（图 1）。
- 3. 按 `ENTER` 键设置 FTP 服务器安装过程（图 1）。
- 4. 按 `y` 键确认下载 FTP 软件包。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_188_0.png)

▲ 图 1：yum 命令

▲ 图 2：下载 FTP 软件包

FTP 服务器只需几分钟即可安装完成，如图 3 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_188_1.png)

▲ 图 3：已安装的 FTP 服务器

安装 FTP 服务器后，让我们学习如何配置 FTP 服务器。

## 配置 FTP 服务器

配置 FTP 服务器时，会使用 `vsftpd` 配置文件。FTP 服务器配置文件存储在 `/etc` 目录下。您需要使用文本编辑器（如 `vi`）编辑此 `/etc` 文件来配置服务器。

执行以下步骤配置 FTP 服务器：

- 1. 在终端窗口中输入 `/etc/vsftpd.conf` 命令（图 4）。
- 2. 按 `ENTER` 键（图 5）。

`vsftpd` 配置文件包含：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_189_0.png)

> 图 4：配置 FTP 服务器

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_189_1.png)

> 图 5：vsftpd 配置文件

- 3. 按键盘上的 Insert（插入）键进入插入模式（图 AT-2.46）。
- 4. 在 `allow_wrappers=Yes` 文本后输入 `pasv_max_port=1024`（图 6）。
- 5. 在 `pasv_max_port=1024` 语法后输入 `local_root=/home/kgoment/download`（图 6）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_189_2.png)

> 图 6：插入模式

- 6. 按 `ESC` 键。
- 7. 按冒号（:`）组合键并输入 `wq` 保存（图 7）。

一旦您在编辑器中输入 `wq`，配置文件就会被保存。
- 8. 在终端中输入 `/etc/init.d/vsftpd restart`（图 8）。
- 9. 按 `ENTER` 键（图 8）。

FTP 服务器已重启。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_193_0.png)

图 2：Samba 服务器配置窗口

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_193_1.png)

图 3：创建 Samba 共享窗口

+ 出现“选择目录”对话框（图 4）。
选择您想要共享的目录。在我们的示例中，我们选择了 `/tmp` 目录（图 4）。
点击 `OK` 按钮，如图 4 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_193_2.png)

图 4：选择目录对话框

+ 重新出现“创建 Samba 共享”窗口（图 5）。
勾选可写（Writable）和可见（Visible）复选框（图 5）。
在“创建 Samba 共享”窗口中选择访问（Access）选项卡，如图 5 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_193_3.png)

图 5：基本选项卡

打开访问选项卡（图 6）。

10. 选择“允许所有人访问”（Allow access to everyone）单选框（图 7）。
11. 点击 `OK` 按钮（图 7）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_194_0.png)

▲ 图 6：访问选项卡

重新出现 Samba 服务器配置窗口，显示已目录现在已共享（图 8）。

12. 点击 Samba 服务器配置窗口标题栏上的“关闭窗口”按钮，现在窗口如图 8 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_194_1.png)

▲ 图 7：OK 按钮

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_194_2.png)

图 8：关闭窗口

与 Samba 服务器共享文件后，现在让我们学习如何从 Windows 访问 Samba。

## 从 Windows 访问 Samba 共享

在 Samba 服务器中，您可以访问 Microsoft Windows（如 Windows Vista/XP）上的共享文件夹或目录。您还可以访问您已共享的文件或文件夹的内容。

执行以下步骤从 Windows Vista 访问 Samba 共享：

+ 1. 点击按钮。出现开始菜单（图 9）。
2. 从开始菜单中选择“网络”（Network）选项。
出现网络窗口（图 10）。
3. 在网络窗口的地址栏中输入 `192.168.1.36`（图 10）。
4. 按下回 键。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_195_0.png)

▲ 图 9：开始菜单

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_195_1.png)

▲ 图 10：访问网络

出现“连接到 192.168.1.36”对话框（图 11）。

+ 5. 在“用户名”（User name）框中输入用户名。在我们的示例中，我们已经输入了（图 12）。
+ 6. 在“密码”（Password）文本框中输入密码。
+ 7. 点击 `OK` 按钮（图 12）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_195_2.png)

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_195_3.png)

▲ 图 11：连接到 192.168.1.36 对话框

▲ 图 12：输入凭据

打开 `192.168.1.36` 电脑的共享目录，如图 13 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_195_4.png)

▲ 图 13：共享目录

你可以看到 `192.168.1.36` 电脑的 `tmp` 目录，你可以从 Windows Vista 访问。

### 实验 8：使用 Apache Web 服务器

目标：
安装 Apache Web 服务器并使用它托管网页。

要求：

- Fedora 11 操作系统
- 一台联网计算机

### 安装 Apache Web 服务器

您需要安装 Apache Web 服务器以便在 Linux 中创建自己的网页。让我们执行以下步骤安装 Apache Web 服务器：

+ 1. 在终端中输入 `sudo yum install httpd` 以在 Linux 中安装 Web 服务器（图 1）。
2. 按下回 键。包管理器检查软件包依赖项并升级软件包（图 2）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_196_0.png)

▲ 图 1：sudo 命令

▲ 图 2：已升级的软件包

+ 3. 在询问确认安装 Web 服务器时，按下键盘上的 `y` 键（图 3）。
4. 按下回 键。
Web 服务器的安装继续，剩余的软件包和更新正在下载中：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_196_1.png)

▲ 图 3：Web 服务器安装

几分钟后，安装完成。
安装 Apache 服务器后，让我们学习如何使用 Apache 服务器托管网页。

### 通过 Apache 服务器托管网页

您不需要在 Web 浏览器的地址栏再次输入网页地址。Apache 服务器的默认位置为 `/var/www/html`。

执行以下步骤使用 Apache 服务器托管网页：

+ 1. 点击 GNOME 桌面上的“应用程序”（Applications）菜单。出现下拉列表（图 4）。
2. 从下拉菜单中选择“附件”（Accessories）选项。出现子菜单（图 4）。
3. 从子菜单中选择“文本编辑器”（Text Editor）选项，如图 4 所示：

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_197_0.png)

图 4：启动 gedit 文本编辑器

+ 4. 在文本编辑器窗口中输入你想显示在网页上的文本。在我们的示例中，我们输入了 Welcome to the world。
5. 点击“保存”（Save）按钮，所示：

+ 7. 从“位置”（Places）侧边栏中选择位置。在我们的示例中，我们选择了（图 6）。
出现“另存为”（Save as）对话框（图 6）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_198_0.png)

▲ 图 5：另存为

+ 8. 从“文件系统”（File System）中选择位置（图 7）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_198_1.png)

▲ 图 6：另存为框

+ 8. 从“文件系统”（File System）中选择位置（图 7）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_198_2.png)

▲ 图 7：文件系统

+ 9. 从“文件系统”（File System）中选择位置（图 8）。

▲ 图 8：文件系统

+ 10. 从“文件系统”（File System）中选择位置（图 9）。

▲ 图 9：文件系统

+ 11. 点击 `OK` 按钮（图 11）。
12. 点击 `OK` 按钮（图 12）。
13. 点击 `OK` 按钮（图 13）。

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_200_0.png)

▲ 图 10：OK 按钮

![](img/5cfda308a5eba7fcc04c6aeafbe7fe3f_200_1.png)

▲ 图 11：OK 按钮

3. 启动你的 NFS 服务器：
```
