
[/miff24 /psmono /alc8500 /lp2563 /pbrusraw /stp /iw1q /pbm /md1x1mono /epson /bjc600 /bp1310 /coslwp /cdjcolor /bj10v /cdj1600 /djet500 /xl1rg16x /atx23 /xl1gray4 /st800 /jpeggray /neclp /psgray /alc2000 /lp8000 /pksm /lrm3200 /jetp3852 /pbmrw /DJ630 /epsonc /bjc800 /ibp320 /coslxl /cdjmono /bj10vh /cdj500 /laserjet /xl1rg32x /atx24 /xl1mono /stcolor /pdfwrite /oce9050 /psrgb /cup5 /iq850 /pkstmax /lx5000 /la50 /pgm /DJ6xx /escp /faxg3 /lips2p /cps0 /cdj550 /mag16 /cdj670 /ijetplus /ijet4pi1 /atx38 /bmpmono /sunhmno /pswrite /okii82 /bit /c1jet5 /lxm5700m /tifffcrle /lex7000 /la70 /pgmraw /DJ6xxF /fs600 /faxg32d /bjc880j /declj250 /pj /mag56 /cdj850 /lj1jet2p /l14dithp /bmpa16 /bmpgray /t4693d2 /epswrite /okiihm /bitrbg /cljet5c /m8510 /tiffg3 /lex5700 /la75 ...*]

此示例中并未列出所有设备。

> **ALADDIN 还是 GNU？**
>
> Linux 至少有两个版本的 Ghostscript 可供选择。一个版本名为 AFPL Ghostscript，formerly 称为 Aladdin Ghostscript。该版本根据 Aladdin Free Public License 授权，此许可证禁止商业分发。另一个版本称为 GNU Ghostscript，根据 GNU 通用公共许可证分发。有关不同版本的详细信息或关于授权问题的答案，请参阅 Ghostscript 主页 [http://www.cs.wisc.edu/ghost/](http://www.cs.wisc.edu/ghost/)。

## 创建和配置本地打印机

为你的 Fedora 系统创建本地打印机可以通过六个简单的步骤完成。你必须有 root 权限才能使用 `system-config-printer` 客户端。在开始之前，`cupsd` 守护进程也应当正在运行（手动启动守护进程，如本章前面所示，或者使用 `ntsysv`、`chkconfig` 或 `system-config-services` 命令确保 `cupsd` 在启动时自动运行）。

要启动 `system-config-printer`，请从 GNOME 或 KDE 桌面面板的 System Settings 菜单中选择 Printing 菜单项，或者在 X 终端窗口中使用命令行，如下所示：

```bash
# system-config-printer &
```

## 创建打印队列

Fedora 的 `system-config-printer` 工具会引导您完成创建新打印队列的流程，这实际上是在您的系统上定义了一台新打印机。要开始配置本地（连接）打印机，请单击 `system-config-printer` 主窗口工具栏中的 **New**（新建）按钮。随后会出现“添加新打印队列”配置对话框，如图 12.1 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_343_0.png)

**图 12.1** 单击工具栏中的 **New**（新建）按钮以开始为您的系统配置新打印机；当向导对话框出现时，单击 **Forward**（前进）按钮开始。

单击 **Forward**（前进）按钮：将出现“队列名称”对话框。为新的打印机输入一个期望的名称（例如 `lp`），输入简短的描述，然后单击 **Forward**（前进）按钮。“队列类型”对话框将出现，如图 12.2 所示。单击队列类型下拉菜单以选择您要添加的打印机类型。您可以配置受通用 UNIX 打印系统（CUPS）支持的本地或网络打印机、远程服务器上的 `lpd` 守护进程、SMB（会话消息块）服务器、Novell 的 NetWare 核心协议或 JetDirect 接口。要配置连接到您计算机的打印机，请选择“本地连接”队列类型，单击选择打印机设备（可能是 `/dev/lp0` 或 `/dev/usb/lp0`），然后单击 **Forward**（前进）。您也可以使用“自定义设备”按钮来输入不同的端口，例如串行打印机的 `/dev/ttyS0`。

![](img/2045828cf45e5632bf056f9ca99d6755_343_1.png)

**图 12.2** 单击下拉菜单以选择本地连接的打印机队列类型。

**图 12.3** 中所示的“打印机型号”对话框提供了一个下拉菜单，您可以使用它来选择打印机的制造商，或者只需选择一种通用类型的连接打印机。

![](img/2045828cf45e5632bf056f9ca99d6755_344_0.png)

**图 12.3** 单击下拉菜单以选择打印机的制造商或打印机类型。

请注意，即使打印机未连接到您的计算机，您也可以为 Fedora 配置该打印机。选择打印机制造商后，将出现该制造商的打印机列表（例如 HP，如图 12.4 所示）。从列表中选择您的打印机，然后单击 **Forward**（前进）按钮。

![](img/2045828cf45e5632bf056f9ca99d6755_344_1.png)

**图 12.4** 从列表中选择您的打印机，然后单击 **Forward**（前进）按钮以完成本地连接打印机的配置。

如果在列表中看不到您的打印机，请不要担心。您可以选择一个相关但不同的打印机型号，仍然可以正常打印。例如，许多 HP 打印机可以通过选择 Deskjet 500（黑白）或 500C（彩色）型号来使用。

**注意**

您还可以浏览 [http://www.linuxprinting.org/](http://www.linuxprinting.org/) 以查找适用于您的打印机的驱动程序，或者查看每个驱动程序支持的打印机交叉引用列表。您也可以在市场上最新的打印机上找到新的和改进的驱动程序。

如果其型号未列出，您可以尝试不同的选择，看看哪种打印机选择最适合您的打印机。您可能无法使用打印机的所有功能，但可以设置打印服务。做出选择后，单击 **Forward**（前进）。

“完成并创建新打印队列”对话框将显示打印机类型、打印机设备和所选打印机，以便您可以确认信息是否正确（参见图 12.5）。如果需要更改选项，请单击 **Back**（后退）返回之前的对话框。要创建新的打印队列，请单击 **Finish**（完成）。

![](img/2045828cf45e5632bf056f9ca99d6755_345_0.png)

**图 12.5** 在 `/etc/printcap` 中提交创建新的打印机条目之前，请再次检查您的设置；当设置正确时，单击 **Finish**（完成）以创建新的打印队列。

当打印队列创建完成后，系统会询问您是否要打印测试页。单击 **Yes**（是）以保存新的打印机设置并打印测试页。如果单击 **No**（否），则不会打印测试页，您必须在退出 `system-config-printer` 之前删除新的打印机条目，或者保存或取消您的更改。

您可以在 `system-config-printer` 主窗口中看到新定义的打印机，如图 12.6 所示。

**提示**

您还可以为同一打印机配置多个打印队列。使用此技术可以通过相同的打印机测试不同的打印驱动程序来打印。创建一个新的队列，给它一个特定的名称（例如 `testpc13`），然后选择不同的打印机。完成配置并打印测试页，与其他条目比较结果，以找到最佳输出。您还可以使用此技术为同一打印机定义黑白或彩色打印机条目，或者为不同类型的介质（例如普通纸或照片纸）使用不同的驱动程序。

![](img/2045828cf45e5632bf056f9ca99d6755_346_0.png)

**图 12.6** 在 `/etc/printcap` 中创建的新打印机条目将显示在 `system-config-printer` 的主窗口中。

## 编辑打印机设置

您也使用 `system-config-printer` 工具来编辑新定义的打印机。要编辑打印机设置，请在“打印机配置”对话框中突出显示打印机的列表项，然后单击工具栏上的 **Edit**（编辑）按钮。将显示“编辑打印队列”对话框，如图 12.7 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_346_1.png)
