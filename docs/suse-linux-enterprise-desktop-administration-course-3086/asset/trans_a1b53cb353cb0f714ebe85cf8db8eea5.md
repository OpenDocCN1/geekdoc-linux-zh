

随后会引导你进入一系列对话框，在其中可以为连接类型添加详细信息并选择打印机型号，如图 12-6 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_432_0.png)

**Figure 12-6**

选择 Next。出现的对话框中，你可以根据需要修改此型号的配置（与图 12-4 中显示的对话框相同）。

**Network Printers**  要配置网络打印机，请在 Printer Type 对话框中选择 Network Printers（图 12-3）。

你可以指定多种协议，如图 12-7 所示。

![](img/9129877170834ca9d5fdac5319bf5f12_433_0.png)

Figure 12-7

CUPS 支持 IPP、LPD、SMB、IPX 和 socket 协议。这些协议在下面进行描述：

- *IPP (Internet Printing Protocol)*—IPP 是一种相对较新的协议（自 1999 年起），基于 HTTP 协议。与其他协议相比，IPP 可以传输更多与作业相关的数据。

CUPS 使用 IPP 进行内部数据传输。这是 CUPS 服务器之间转发队列的首选协议。

IPP 的端口号为 631。

可以使用设备 URI（Uniform Resource Identifier）来指定打印机。设备 URI 用于某些 CUPS 命令行工具中，例如 **lpadmin**。

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

- Print via CUPS Network Server
- Print Directly to a Network Printer
- Print to an SMB Printer

## ***Print via CUPS Network Server***

如果选择 Print via CUPS Network Server，将出现图 12-8 所示的对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_435_0.png)

**Figure 12-8**

选项在左侧的帮助文本中进行了描述。

- *CUPS Client Only*—仅允许你访问单台服务器上的打印队列。本地不运行打印机守护进程。见图 12-9。

![](img/9129877170834ca9d5fdac5319bf5f12_435_1.png)

**Figure 12-9**

在警告消息之后，下一个对话框允许你输入打印服务器的 IP 地址或完全限定域名（FQDN），并指定要使用的队列。见图 12-10。

![](img/9129877170834ca9d5fdac5319bf5f12_436_0.png)

将要使用的 CUPS 服务器添加到 /etc/cups/client.conf 文件中。

```
# /etc/cups/client.conf
ServerName 10.0.0.2
```

如果整个网络只有一台打印服务器，这种设置是一个不错的选择。

- **CUPS Using Broadcasting**—在本地网络中可能是最佳选择。CUPS 在本地运行，你可以在本地连接的打印机以及网络中其他服务器广播的打印机上打印。网络中广播的新打印机会自动出现并可供用户使用。见图 12-11。

![](img/9129877170834ca9d5fdac5319bf5f12_437_0.png)

有关如何使本地打印机可供他人使用或限制对本地打印机的网络访问的详细信息，请参阅 *SUSE Linux Enterprise Server 10 Administration*（课程 3072）。使用 CUPS Using Broadcasting 时，你可以修改防火墙设置（如果防火墙处于活动状态），并指定接受广播的地址。见图 12-12。

![](img/9129877170834ca9d5fdac5319bf5f12_437_1.png)

选择 OK 返回到 Printer Configuration 对话框。

- *Remote IPP Queue*—访问特定服务器上的特定队列。见图 12-13。

![](img/9129877170834ca9d5fdac5319bf5f12_438_0.png)

**Figure 12-13**

与仅客户端配置不同，本地 CUPS 服务器正在运行，并且本地连接的打印机仍然可访问。

## **Print Directly to a Network Printer**

对于配备网络卡的打印机，应选择 Print Directly to a Network Printer。对于此类打印机，请在图 12-14 所示的对话框中选择 Direct TCP Port Printing。

![](img/9129877170834ca9d5fdac5319bf5f12_439_0.png)

Figure 12-14

Remote LPD Queue 选项会打开对话框以输入打印服务器的主机名和队列名称，并选择打印机型号。最后会显示远程 LPD 队列的配置，如图 12-14 所示。**Remote IPP Queue** 可用于可能通过 YaST 无法配置的未来 CUPS 队列。

选择 **Direct TCP Port Printing** 并选择 **Next** 后，输入打印服务器的 *hostname* 或 *IP address*。然后选择 **Next**。见图 12-15。

![](img/9129877170834ca9d5fdac5319bf5f12_440_0.png)

图 12-16 所示的对话框会出现。在此对话框中，你可以为打印队列命名，并添加有关打印机及其位置的信息。

![](img/9129877170834ca9d5fdac5319bf5f12_441_0.png)

**Figure 12-16**

当你选择 Next 时，先前在图 12-4 和 12-6 中介绍过的对话框将打开；然后你将被返回到 Printer Configuration 对话框（图 12-2）。

如果你想编辑打印机配置，请在 Printer Configuration 对话框中选择打印机条目并选择 Edit。如果你想删除打印队列，请选择它并选择 Delete。

**Print to an SMB Printer.** 当你的打印机连接到 Windows 或 Samba 服务器时，选择 Print via SMB Network Server 选项。图 12-17 所示的对话框会出现。

![](img/9129877170834ca9d5fdac5319bf5f12_442_0.png)

**Figure 12-17**

在此对话框中，你可以输入工作组、打印服务器的主机名、打印机队列名称以及任何需要的身份验证信息。选择 Next 以打开与之前介绍过的类似的对话框，在其中输入本地队列的名称并选择打印机型号。

## Add and Remove Printers with the GNOME Printers Dialog

GNOME Printers 对话框可用于添加打印机或管理现有队列。要访问该对话框，请选择 Computer > Control Center > Printers。见图 12-18。

![](img/9129877170834ca9d5fdac5319bf5f12_443_0.png)

Figure 12-18

要添加打印机，请选择 New Printer。输入 root 密码后，将出现图 12-19 所示的对话框。

![](img/9129877170834ca9d5fdac5319bf5f12_443_1.png)

Figure 12-19

在这种情况下，检测到一台打印机。选择 Forward 后，另一个对话框，如图 12-20 所示，会出现。选择打印机的制造商和型号。

![](img/9129877170834ca9d5fdac5319bf5f12_444_0.png)

Figure 12-20

选择 **Apply** 以打开 Properties 对话框，该对话框允许你设置不同的打印机参数，例如其位置和使用的纸张尺寸，或更改之前对话框中输入的值。见图 12-21。

![](img/9129877170834ca9d5fdac5319bf5f12_444_1.png)

Figure 12-21

