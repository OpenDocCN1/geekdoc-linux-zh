
- `page-number` 字段包含页数（在此示例中为 1）。
- `num-pages` 字段包含副本数（在此示例中为 1）。对于无法自行产生副本的打印机，`num-pages` 字段始终为 1。
- `job-billing` 字段包含随 IPP `create-job` 或 `print-job` 请求提供的 `job-billing` 属性的副本——或（如果未提供）。
- `hostname` 字段包含产生打印作业的主机的名称（在此示例中为 `localhost`）。

## Configuration File

CUPS 的配置文件是 `/etc/cups/cupsd.conf`。它的格式与 Apache Web 服务器的配置文件相似。

各种选项用于配置服务器本身，以及配置过滤、网络、浏览和访问。

服务器配置的详细信息在 SUSE Linux Enterprise Server 10 Administration（课程 3072）中介绍。

## Objective 2—Configure Printers and Queues

YaST 提供打印机安装和配置功能。要配置打印机，您需要了解以下内容：

- When to Configure a Printer
- Required Printing Software
- Add a Printer
- Manage Print Queues with the GNOME Printers Dialog

### When to Configure a Printer

您可以在以下时间配置打印机：

- *During installation*—如果您在安装期间处于硬件配置对话框中，并且自动检测不正确，请选择 Printers 链接或使用 Change 下拉列表。请注意，在安装期间，仅自动检测并列出在 Printers 下的本地连接打印机。
- *After installation*—您可以从 YaST 控制中心通过选择 **Hardware > Printer** 来更改打印机配置设置。您也可以作为 root，从终端窗口直接使用 `yast2 printer` 命令启动 YaST 打印机配置模块。

### Required Printing Software

表 12-1 显示了设置打印服务器所需的软件包。

| Package | Content |
|---|---|
| `cups` | 提供 `cupsd` 打印机守护进程。 |
| `cups-client` | 提供命令行打印工具。 |
| `cups-libs` | 应始终安装，因为许多程序（如 Samba）都链接到 CUPS 库。 |
| `cups-drivers` `cups-drivers-stp` | 提供打印队列的 PPD 文件。 |
| `cups-SUSE-ppds-dat` | 提供预生成的 `/etc/cups/ppds.dat` 文件。 |

**Table 12-1**

如果使用 YaST 进行打印机配置，这些文件将自动安装。YaST 还会在运行级别目录中创建符号链接，以确保在启动时自动启动 CUPS 守护进程。

打印系统所需的其他软件包，例如 `ghostscript-library`，会在标准安装期间自动选择。

### Add a Printer

有几种方法可以添加打印机：

- Add a Printer with YaST
- Add and Remove Printers with the GNOME Printers Dialog

#### Add a Printer with YaST

用于配置打印机的打印机配置对话框在安装期间和安装后是相同的。参见图 12-2。

![](img/9129877170834ca9d5fdac5319bf5f12_428_0.png)

Figure 12-2

打印机配置对话框的上部列出了已配置的打印机和任何自动检测到的打印机。

打印机列在上部，对话框的下部显示上部中选定打印机的详细信息。

要添加在对话框上部未显示的打印机，请选择 Add。图 12-3 所示的对话框会出现。

![](img/9129877170834ca9d5fdac5319bf5f12_429_0.png)

**Figure 12-3**

根据您选择的打印机类型，下一个对话框提供更具体的选择。以下打印机类型可用：

- New Queue for Existing Printer
- Directly Connected Printers
- Network Printers

**New Queue for Existing Printer** 此选项仅在已配置打印机时出现。如果您想通过打印到不同的队列来使用不同的分辨率或打印质量，为现有打印机添加队列很有用。选择 New Queue for Existing Printer > Next 以打开一个对话框，您可以在其中选择要添加队列的打印机。再次选择 Next。

在图 12-4 所示的配置对话框中，选择一个条目然后选择 Edit。

![](img/9129877170834ca9d5fdac5319bf5f12_430_0.png)

**Figure 12-4**

对该队列进行所需的任何更改。您可以通过选择 Test 来测试打印机配置。选择 OK 以创建队列并返回到打印机配置对话框。

**Directly Connected Printers** 大多数直接连接的打印机会自动检测到。如果没有，请在图 12-3 所示的 **Printer Type** 对话框中选择 **Directly Connected Printers**。图 12-5 所示的对话框会出现。

![](img/9129877170834ca9d5fdac5319bf5f12_431_0.png)

Figure 12-5

从列表中选择连接类型并选择 **Next**。

随后会引导你进入一系列对话框，在其中可以为连接类型添加详细信息并选择打印机型号，如图 12-6 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_432_0.png)

**Figure 12-6**

选择 Next。出现的对话框中，你可以根据需要修改此型号的配置（与图 12-4 中显示的对话框相同）。

**Network Printers** 要配置网络打印机，请在 Printer Type 对话框中选择 Network Printers（图 12-3）。

你可以指定多种协议，如图 12-7 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_433_0.png)

Figure 12-7

CUPS 支持 IPP、LPD、SMB、IPX 和 socket 协议。这些协议在下面进行描述：

- *IPP (Internet Printing Protocol)*—IPP 是一种相对较新的协议（自 1999 年起），基于 HTTP 协议。与其他协议相比，IPP 可以传输更多与作业相关的数据。

CUPS 使用 IPP 进行内部数据传输。这是 CUPS 服务器之间转发队列的首选协议。

IPP 的端口号为 631。

可以使用设备 URI（Uniform Resource Identifier）来指定打印机。设备 URI 用于某些 CUPS 命令行工具中，例如 `lpadmin`。

IPP 协议的设备 URI 可能如下所示：

`ipp://cputserver/printers/printqueue`

- **LPD (Line Printer Daemon)**—LPD 协议在 RFC 1179 中有描述（可在 http://www.ietf.org/rfc.html 找到请求评论）。

由于在实际打印数据之前会发送一些与作业相关的数据，例如打印机队列，在为数据传输配置 LPD 协议时必须指定打印机队列。

大多数打印机厂商的实现足够灵活，可以接受任何名称作为打印机队列。打印机手册可能会指出应使用哪个名称（例如 LPT、LPT1 或 LP1）。

也可以在网络中使用 CUPS 系统的另一台 Linux 或 UNIX 主机上配置 LPD 队列。LPD 服务的端口号为 515。

设备 URI 示例：`lpd://host-printer/LPT1`。

- **SMB (Server Message Block)**—CUPS 支持在连接到 Windows 共享的打印机上打印。此目的所使用的协议是 SMB。

SMB 使用端口号 137、138 和 139。

设备 URI 示例：

`smb://user:password@workgroup/server/printer`

`smb://user:password@host/printer`

`smb://server/printer`

- **IPX**—该协议用于通过 Novell NetWare Server 打印。
- **socket**—该协议用于连接到配备网络端口的打印机，例如 HP 的 JetDirect。常用的一些 socket 端口号为 9100 或 35。

设备 URI 示例：`socket://host-printer:9100/`。

接下来出现的对话框取决于你的选择。我们在此介绍其中三种：
