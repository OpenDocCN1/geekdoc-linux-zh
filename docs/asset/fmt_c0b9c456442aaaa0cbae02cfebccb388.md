
![](img/9129877170834ca9d5fdac5319bf5f12_446_2.png)

## 练习 12-1：更改您的打印机配置

![](img/9129877170834ca9d5fdac5319bf5f12_446_3.png)

在本练习中，您添加一台本地打印机并打印到远程队列。该练习分为两部分。

在第一部分中，使用 `YaST` 添加打印机到您的打印机配置中。配置一台并行打印机型号 `HP LaserJet 4`，打印队列名为 `hplj4`。出于本练习的目的，不必将打印机连接到您的计算机。配置打印机以在一张纸上打印两页，并将默认纸张尺寸从 `A4` 改为 `US Letter`。

在第二部分中，配置一台使用主机 `da1` 上可用打印机的计算机队列。如果此打印机不存在，出于本练习此部分的目的，您可以使用运行在您自己的机器上的 `CUPS` 服务器。

### 完成此练习的详细步骤

- Part I: Add a Printer
- Part II: Print to a Remote CUPS Printer

## Part I: Add a Printer

要添加打印机，请执行以下操作：

1. 启动 `YaST Control Center` 并选择 **Hardware > Printer**。  
   `Printer Configuration` 对话框出现。
2. 通过选择 **Add** 为打印机添加一个新队列。
3. 对于打印机类型，确保选择了 **Directly Connected Printers**，然后选择 **Next**。
4. 对于打印机类型，确保选择了 **Parallel Printer**；然后选择 **Next**。
5. 通过选择 **Next** 接受 **First Parallel Port (/dev/lp0)** 作为打印机设备。
6. 输入以下内容：
   - Name for printing: `hplj4`
   - Description of Printer: `LaserJet 4 on daxx`（其中 `xx` 为您的主机号）
   - Location of Printer: `daxx computer`
   确保选择了 **Do Local Filtering**；然后选择 **Next**。  
   `Printer Model` 对话框出现，其中列出制造商和型号。
7. 从制造商列表中选择 **HP**；从型号列表中选择 **LaserJet 4**。
8. 完成后，选择 **Next**。  
   `Configuration` 对话框出现。
9. 通过选择 **Filter Settings**；然后选择 **Edit** 来更改打印过滤器的设置。  
   屏幕顶部出现一个选项列表，屏幕底部出现每个选项的值列表。
   a. 通过选择 **Pages per Sheet** 来更改每张纸应打印的页数。
   b. 在 Values 列表中，选择 **2**。
   c. 滚动选项列表并选择 **Page Size**。  
      注意纸张尺寸的设置。
   d. 通过选择 **Letter** 将纸张尺寸更改为 `US Letter`。
10. 完成后，选择 **Next**。
11. 通过选择 **OK** 返回到主 `Printer Configuration` 对话框。  
    通过选择 **Finish** 完成配置；然后关闭 `YaST Control Center`。

## Part II: Print to a Remote CUPS Printer

要打印到远程 `CUPS` 打印机，请执行以下操作：

1. 从 `YaST Control Center`，选择 **Hardware > Printer**。  
   `Printer Configuration` 对话框出现。
2. 通过选择 **Add** 添加一个新的 `CUPS` 打印机。
3. 选择 **Network Printers**；然后选择 **Next**。
4. 选择 **Print via CUPS Network Server**；然后选择 **Next**。
5. 选择 **Remote IPP Queue**；然后选择 **Next**。
6. 在 **Hostname of Print Server** 字段旁边，选择 **Lookup**；然后选择 **Scan for IPP Servers**。
7. 从下拉列表中选择 `da1.digitalairlines.com`。
   - *(Conditional)* 如果 `da1.digitalairlines.com` 未出现在下拉列表中，请在字段中输入 `da1.digitalairlines.com`。
8. 在 **Remote Queue Name** 字段旁边，选择 **Lookup** 以选择 `da1` 上的默认队列。
9. 通过选择 **Test Remote IPP Access** 测试对打印机服务器的连接性。
10. 当成功消息出现时，选择 **OK**。
11. 选择 **Next**。
    - 出现 `Queue Name` 对话框。
    - 注意 **Do Local Filtering** 未被选中，因为过滤是在远程 `CUPS` 打印机服务器上完成的。
12. 从 **Name for Printing** 字段中，记录讲师服务器上打印机队列的名称。
13. 通过选择 **Next** 接受默认设置。
14. 通过选择 **Finish** 保存配置更改。
15. 关闭所有窗口。

## Objective 3—Understand Novell iPrint

`Novell iPrint` 可安全地在多个网络和操作系统之间扩展打印服务。要在 `SUSE Linux Enterprise Desktop 10` 上有效使用 `Novell iPrint`，您需要了解以下内容：

- Describe the Purpose and Architecture of Novell iPrint
- Configure Novell iPrint
- Install the Novell iPrint client

### Describe the Purpose and Architecture of Novell iPrint

要描述 `Novell iPrint` 的目的和架构，您需要知道以下内容：

- What Novell iPrint Is
- Novell iPrint Components on Linux
- Novell iPrint Port Usage

#### What Novell iPrint Is

`Novell iPrint` 允许移动员工、业务合作伙伴和客户使用现有的 Internet 连接从各种远程位置访问打印机。

![](img/9129877170834ca9d5fdac5319bf5f12_448_0.png)

无论用户是在办公楼工作、从家中远程办公，还是在另一个国家的销售会议中，`Novell iPrint` 都确保他们可以快速、轻松、可靠地打印文档。

用户可以使用 Web 浏览器指向显示可供安装打印机的 Web 页面。

当用户选择打印机时，`Novell iPrint` 客户端将被安装（如果之前未安装），打印机的驱动程序将被下载，并且在用户的 workstation 上创建一台打印机，使用户能够从桌面上的任何应用程序向打印机发送文档。

图 12-24 说明了此过程。

![](img/9129877170834ca9d5fdac5319bf5f12_449_0.png)

Figure 12-24

使用 `Novell iPrint`，移动用户不再需要联系忙碌的网络管理员以查找打印机的名称和上下文以及所需的打印机驱动程序。相反，移动用户在熟悉的 Web 浏览器中工作，使用 `Novell iPrint Printer List` Web 页面或管理员创建的地图来查找附近的打印机。

公司还可以通过减少在办公室之间传真文档的需求来降低通信成本；相反，公司可以使用现有的 Internet 连接将文档打印到远程打印机。

`Novell iPrint` 使用 Internet Printing Protocol（`IPP`），一种行业标准，以消除通过 Internet 打印的复杂性并使基于位置的打印成为现实。

`IPP` 的好处包括以下内容：

- 使用 IP 协议
- 提供广泛的厂商支持
- 可在本地网络和 Internet 上工作
- 提供打印数据加密（`SSL`、`TLS`）
- 为所有平台提供标准打印协议（如 Linux、Macintosh 和 Windows）

![](img/9129877170834ca9d5fdac5319bf5f12_450_0.png)

有关 `IPP` 的更多信息，请参阅 Printer Working Group 网站上提供的文档，网址为 *http://www.pwg.org/ipp/index.html*。
