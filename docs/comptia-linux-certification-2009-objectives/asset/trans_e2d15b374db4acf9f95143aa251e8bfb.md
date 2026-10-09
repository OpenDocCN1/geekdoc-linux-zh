
## printers.conf 文件

存储在 /etc/cups 目录中的 printers.conf 文件，将网络上的本地打印机集合定义为共享资源。打印机列表由 cupsd 守护进程自动生成。可以对其进行配置，使其仅允许显式公布的打印机。该文件包含一组指令，用于定义被共享打印机的功能。

## 如何配置远程打印

### 程序参考：安装 Samba

要安装 Samba：

- 1. 在图形界面中以 root 身份登录。
- 2. 挂载包含最新版本 samba 软件包的 Linux 安装光盘。
- 3. 导航至 /media/[媒体名称]/Server 文件夹。
- 4. 选择 samba {软件包版本}.rpm 和 perl - Convert - ASN1 - {软件包版本}.rpm 文件。
- 5. 右键单击并选择**使用软件安装程序打开**。
- 6. 在**正在安装软件包**窗口中，验证这两个软件包已列出，并单击**应用**开始安装软件包。
- 7. 如有必要，在**无法验证 {软件包名称}**消息框中，单击**仍要安装**以安装这两个软件包。
- 8. 在**软件安装成功**消息框中，单击**确定**以完成安装。

### 程序参考：使用 Samba 共享打印机

要使用 Samba 共享打印机：

- 1. 打开 /etc/samba/smb.conf 文件。
- 2. 为打印机定义共享。
    - 在方括号内指定共享名称。
      - [共享名称]
    - 定义 spool 文件的路径。
      - path = {spool 文件的路径}
    - 指定打印机名称。
      - printer = {打印机名称}
    - 指定是否允许来宾用户打印。
      - public = {是 | 否}
    - 指定用户的打印访问权限。
      - printable = {是 | 否}
    - 如有必要，包括描述共享打印机的注释。
      - comment = {打印机描述}
- 3. 保存并关闭文件。
- 4. 输入 `testparm /etc/samba/smb.conf` 以验证 smb.conf 文件是否格式正确。
- 5. 输入 `chkconfig smb on` 以在系统启动时启动该服务。
- 6. 输入 `service smb restart` 以重启 Samba 服务。
- 7. 输入 `ifconfig` 以查看连接打印机的系统的 IP 地址。
- 8. 验证您创建的打印机共享是否可以从其他 Linux 系统访问。

## 活动 6-5
### 配置远程打印机

**开始之前：**

- 1. 在 *srvA* 上，您已在图形界面中以 *root* 身份登录。
- 2. 双击桌面上的**计算机**图标。
- 3. 导航至 */rhelsource/Server* 文件夹。
- 4. 在 *Server* 窗口中，导航并选择 *perl - Convert - ASN1 - 0.20 - 1.1.noarch.rpm* 和 *samba - 3.0.33 - 3.7.el5.i386.rpm* 文件。
- 5. 右键单击并选择**使用**“*软件安装程序*”。
- 6. 在 *正在安装软件包* 窗口中，验证这两个软件包已列出，并单击 **应用** 开始安装软件包。
- 7. 在 *无法验证 samba - 3.0.33 - 3.7.el5.i386* 消息框中，单击 **仍要安装** 以安装 *samba - 3.0.33 - 3.7.el5.i386* 软件包。
- 8. 在 *无法验证 perl - Convert - ASN1 - 0.20 - 1.1.noarch* 消息框中，单击 **仍要安装** 以安装 *perl - Convert - ASN1 - 0.20 - 1.1.noarch* 软件包。
- 9. 在 *软件安装成功* 消息框中，单击 **确定** 以完成安装过程。
- 10. 关闭 *Server - File Browser* 窗口。
- 11. 选择 *系统→系统管理→打印* 以显示 *打印机配置 - localhost* 窗口。
- 12. 在左侧窗格中，选择 *服务器设置*。
- 13. 在右侧窗格的 *基本服务器设置* 部分中，勾选 *共享连接到此系统的已公布打印机* 复选框。
- 14. 单击 **应用**。
- 15. 关闭 *打印机配置 - localhost* 窗口。
- 16. 选择 *应用程序→附件→终端* 以在图形界面中启动终端窗口。

**场景：**

您在 Linux 系统上配置了一台本地打印机。由于您需要从其他 Linux 系统打印大量文档，您决定将该打印机设为共享打印机，并启用远程访问权限，同时授予 *jsmith* 用户账户权限。

## 执行内容

| 执行内容 | 操作方法 |
| :--- | :--- |
| 1. 修改 smb.conf 文件以共享打印机。 | a. 在终端窗口中，输入 `vi /etc/samba/smb.conf` 在文本编辑器中打开 smb.conf 文件。<br>b. 导航至 **Share Definitions**（共享定义）部分。<br>c. 导航至 **printers** 部分中包含 *browseable* 变量的行的开头。<br>d. 按 I 键切换到插入模式。按 **Enter** 键在当前行之前插入新行，然后按 **Tab** 键。<br>e. 按 **上箭头** 键，然后按 **Tab** 键移动到上一行。<br>f. 输入 **printer name = printer**。<br>g. 按 **下箭头** 键，然后按两次 **Backspace** 键。<br>h. 输入 **yes** 使其可浏览，然后按 **下箭头** 键。按两次 **Backspace** 键。<br>i. 输入 **yes** 以允许来宾账户访问打印机共享。<br>j. 按 **Esc** 键返回命令模式。保存文件并退出编辑器。 |
| 2. 添加新的 smb 用户并重启 smb 服务。 | a. 输入 `smbpasswd -a jsmith` 将 jsmith 添加到 smb 用户列表。<br>b. 按两次 **Enter** 键以设置空密码。<br>c. 输入 `ifconfig` 以查看 Linux 系统的 IP 地址。<br>d. 记录该系统的 IP 地址。<br>e. 输入 `service smb restart` 以重启 samba 服务器。 |
| 3. 访问远程打印机。 | a. 在 srvB 上，以 **root** 身份在图形界面中登录。<br>b. 选择 **系统→系统管理→打印**。<br>c. 在 **打印机配置 - localhost** 对话框中，单击 **新打印机** 以添加打印机。<br>d. 在 **新打印机** 对话框中，在 **打印机名称** 文本框中，输入 *printer1* 并按 **Tab** 键。<br>e. 在 **描述** 文本框中，输入 *Remote Printer* 并按 **Tab** 键。<br>f. 在 **位置** 文本框中，输入 *Printer on srvA* 并单击 **前进**。<br>g. 在 **设备** 列表框中，观察到 **LPT #1** 被选中。<br>h. 选择 **Windows Printer via SAMBA** 选项并单击 **前进**。<br>i. 在右侧窗格中，观察到 **MYGROUP** 共享已显示。<br>j. 双击 **MYGROUP** 共享。<br>k. 在右侧窗格中，观察到 **SRVA** 已显示。<br>l. 双击 **SRVA** 共享。<br>m. 在右侧窗格中，观察到打印机已显示。<br>n. 选择该打印机。<br>o. 观察到在 smb 部分，打印机路径已填入文本框。单击 **前进**。 |
| 4. 选择打印机驱动程序并将远程打印机设置为默认打印机。 | a. 在 **制造商** 列表框中，确保选中 **Generic** 并单击 **前进**。<br>b. 在 **型号** 列表框中，向下滚动并选择 **PostScript Printer**。<br>c. 在 **驱动程序** 列表框中，选择 **foomatic: Generic - Postscript.ppd (推荐)** 选项并单击 **前进**。<br>d. 在确认页面中，观察到显示消息“Going to create a new printer printer at smb://MYGROUP/SRVA/printer.”。<br>e. 单击 **应用** 以添加打印机。<br>f. 观察到在 **远程打印机** 部分，添加了新打印机，**printer@srva**。<br>g. 在右侧窗格中，单击 **设为默认打印机** 以将该打印机设为默认打印机。<br>h. 关闭 **打印机配置 - localhost** 窗口。 |
| 5. 在远程打印机上打印 install.log 文件。 | a. 在桌面上，双击 **root's Home** 文件夹。<br>b. 在 **root - File Browser** 窗口中，双击 install.log 文件。<br>c. 选择 **文件→打印** 以打印文件。<br>d. 在 **打印机** 对话框中，观察到远程打印机 printer@srvA 已被选中。单击 **打印**。<br>e. 切换到 srvA。<br>f. 在任务栏中，单击 **Web 浏览器** 图标以启动 Firefox 网络浏览器。<br>g. 在地址栏中，选择现有地址并输入 http://localhost:631/jobs 以查看打印队列中的作业。<br>h. 单击 **显示已完成作业**。<br>i. 观察到 install.log 文件显示在打印队列中。<br>j. 关闭 **Jobs CUPS 1.3.7 - Mozilla Firefox** 窗口和终端窗口。<br>k. 切换到 srvB。<br>l. 关闭 **gedit** 窗口和 **File Browser** 窗口。 |

