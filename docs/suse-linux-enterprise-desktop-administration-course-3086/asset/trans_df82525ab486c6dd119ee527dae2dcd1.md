

## 使用分发软件交付客户端

你可以使用客户端分发软件（如 Novell ZENworks）将 Novell iPrint 客户端，以及可能还有打印机，交付到你的客户端工作站。

![](img/9129877170834ca9d5fdac5319bf5f12_465_0.png)

## 练习 12-2：使用 Novell iPrint 客户端进行打印

在本练习中，你将安装并使用 Novell iPrint 客户端。

尽管 Novell iPrint 已在 DA-OES Linux 服务器上配置好，供 Digital Airlines 员工访问，但你尚未在自己的 SUSE Linux Enterprise Desktop 10 工作站上安装 Novell iPrint 打印机。

你决定安装并使用 HP DeskJet 打印机。

执行以下操作：

- 1. 从你的 DAx SLED 10 工作站，打开 Firefox Web 浏览器；然后通过输入以下 URL 访问 DA-OES 服务器上的 Novell iPrint 页面：
  
  *http://da-oes.digitalairlines.com/ipp*
  
  服务器 DA-OES 上的 Novell iPrint 打印机列表出现，如图 12-32 所示，其中列出了 HP-DJ 打印机（HP DeskJet）。

![](img/9129877170834ca9d5fdac5319bf5f12_465_1.png)

图 12-32

- 2. 选择 HP-DJ 链接。  
  一个 Novell iPrint 对话框出现，提示 Novell iPrint 客户端未安装。

![](img/9129877170834ca9d5fdac5319bf5f12_466_0.png)

- 3. 通过执行以下操作在 SLED 10 工作站上安装 Novell iPrint 客户端：

- a. 从 Novell iPrint 客户端安装问题对话框中，通过选择 OK 安装 Novell iPrint 客户端。

Novell iPrint 客户端安装页面出现，如图 12-33 所示，其中包含有关如何安装客户端的说明。

![](img/9129877170834ca9d5fdac5319bf5f12_466_1.png)

图 12-33

- b. 在步骤 1 下，选择 Install the iPrint client 链接。  
  一个 Opening novell-iprint-client.i586.rpm 对话框出现。

- c. 通过选择 Save to disk；然后选择 OK，将 novell-iprint-client.i586.rpm 安装程序保存到桌面。

Firefox 下载对话框出现，提示下载已成功完成。

- d. 关闭下载对话框；然后关闭 Firefox。
  
  从 SLED 10 桌面，通过双击 `novell-iprint-client.i586.rpm` 图标启动 Novell iPrint 安装程序。

- e. 在提示时，输入 root 密码 `n0v311`；然后选择 Continue。
  
  软件安装程序对话框出现，如图 12-34 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_467_0.png)

**图 12-34**

- f. 确保 novell-iprint-xclient-sl 软件包已选中；然后通过选择 **Install** 开始 Novell iPrint 客户端安装。
  
  一个 Change Summary 对话框出现。

- g. 接受更改并选择 **Apply**。

- h. *（条件）* 如果提示提供 SLED 10 安装介质，请插入 SLED *10 SP1 Installation DVD*。

安装完成后，一个对话框出现，提示 Novell iPrint 客户端已成功安装。

- i. 通过选择 **Close** 关闭对话框。

### 4. 安装 HP-DJ Novell iPrint 打印机：

在安装了 Novell iPrint 客户端后，你就可以安装 HP-DJ Novell iPrint 打印机了。

执行以下操作：

- a. 从 SLED 10 工作站桌面，重新启动 Firefox；然后输入以下 URL 以访问 Novell iPrint 页面：
  
  `http://da-oes.digitalairlines.com/ipp`

- b. 从 Novell iPrint 打印机列表中，选择 HP-DJ。
  
  一个 Novell iPrint 对话框出现，如图 12-35 所示，提示打印机未安装。

![](img/9129877170834ca9d5fdac5319bf5f12_468_0.png)

**图 12-35**

- c. 选择 **Set printer as default** 选项。

- d. 通过选择 **Yes** 在 SLED 10 工作站上安装打印机。
  
  安装过程开始。
  
  经过片刻后，一个消息出现，提示 HP-DJ 打印机已成功安装。

- e. 通过选择 **OK** 关闭消息。

- f. 最小化 Firefox 浏览器窗口。

### 5. 验证打印机是否已安装：

- a. 从 SLED 10 桌面，选择 **Computer > Control Center**。

- b. 从控制中心，选择 **Hardware > Printers**。
  
  一个 Printers 对话框出现。

请注意，HP-DJ 打印机已列出并被选为默认打印机，如图 12-36 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_469_0.png)

图 12-36

- c. 关闭 Printers 对话框。

- d. 从桌面，选择 **Computer > OpenOffice.org Writer**。
  
  一个空的 OpenOffice.org Writer 文档窗口出现。

- e. 输入以下内容：
  
  This is a test of the HP-DJ printer.

- f. 从 OpenOffice.org Writer 菜单栏，选择 **File > Print**。
  
  经过片刻后，一个 Print 对话框出现。

- g. 通过选择 **OK** 将文档发送到 HP-DJ 打印机。

![](img/9129877170834ca9d5fdac5319bf5f12_469_1.png)

即使没有物理 HP-DJ 打印机连接到网络，打印机也被 Novell iPrint 视为有效打印机，因为它已被配置为“虚拟打印机”。

- h. 通过选择 **File > Exit** 关闭 OpenOffice.org Writer；当提示保存文件时，选择 **Discard**。

- 6. 关闭所有打开的窗口。

## 摘要

- SUSE Linux 默认使用 CUPS 打印系统。
- CUPS 使用 IPP，但可以支持 socket、LPD、IPX 和 SMB 打印协议。
- 你可以在安装期间配置 CUPS 打印机，或在安装后使用 YaST、GNOME Printers 对话框，或通过编辑 `/etc/cups` 目录中的适当配置文件并重启 CUPS 守护进程来进行配置。

- CUPS 打印作业在发送到打印机本身之前会发送到队列目录（`/var/spool/cups`）。CUPS 打印队列使用 `/etc/cups/printers.conf` 文件中的条目进行配置。
- CUPS 守护进程将日志信息写入 `/var/log/cups/error_log`、`/var/log/cups/access_log` 和 `/var/log/cups/page_log` 文件。你可以通过编辑 `/etc/cups/cupsd.conf` 文件来控制日志级别。
- Novell iPrint 可用于通过 Web 浏览器从各种客户端操作系统远程安装、访问和管理 IPP 打印机。每个客户端必须下载 Novell iPrint 客户端才能使用 Novell iPrint。
- 在将打印机添加到 Novell iPrint 之前，你必须先创建 Driver Store 以及配置具有 Printer Agents 的 Print Manager。

## 关键术语

- **/etc/cups/client.conf** — 列出 SUSE Linux 系统上远程 CUPS 服务器的文件。
- **/etc/cups/cupsd.conf** — CUPS 主配置文件。
- **/etc/cups/ppd** — 存储特定打印机所使用的活动配置文件目录。
- **/etc/cups/printcap** — 用于存储 CUPS 客户端配置信息的文件。
- **/etc/cups/printers.conf** — 包含 CUPS 打印机定义的文件。
- **/etc/cups/printcap** — 指向 `/etc/cups/printcap` 文件的符号链接。
- **/var/log/cups/access_log** — 存储网络打印请求信息的 CUPS 日志文件。
- **/var/log/cups/error_log** — 存储 CUPS 守护进程信息的 CUPS 日志文件。
- **/var/log/cups/page_log** — 存储发送到打印机每页信息的 CUPS 日志文件。
- **/var/spool/cups** — SUSE Linux 中的默认打印队列目录。
- **accept command** — 允许打印作业进入打印队列的命令。
- **Apache** — 大多数 Linux 系统上使用的默认 Web 服务器。Apache 也被 iPrint 使用。
- **Common UNIX Printing System (CUPS)** — SLES 中的默认打印系统。
- **cupsd** — CUPS 守护进程。
- **disable command** — 阻止打印队列中的打印作业发送到打印机的命令。
- **Driver Store** — iPrint 使用的打印驱动程序存储库。
- **eDirectory** — Novell 目录服务，被 iPrint 等服务使用。
- **enable command** — 允许打印队列中的打印作业发送到打印机的命令。
- **ghostscript** — 可用于转换和管理 PostScript 格式文档的开源实用程序。
- **GNOME Printers dialog** — 用于在 SUSE Linux GNOME 桌面环境中管理打印机和打印作业的对话框。
- **gnome-cups-manager command** — 用于调用扩展的 GNOME Printers 对话框实用程序的命令。

