

格式为 `[DD/MON/YYYY:HH:MM:SS +ZZZZ]`，其中 ZZZZ 是相对于协调世界时（UTC）的时间偏移，以小时和分钟计。

- **method** 字段是使用的 HTTP 方法（如 GET、PUT 和 POST）。
- resource 字段是所请求资源的文件名。可能的资源有：
  - `/`
  - `/admin/`
  - `/printers/`
  - `/jobs/`
- version 字段是客户端使用的 HTTP 版本。对于 CUPS 客户端，这始终是 HTTP/1.1。
- status 字段包含请求的 HTTP 结果状态。通常是 200，但其他 HTTP 状态码也是可能的。例如，401 表示未授权访问。
- bytes 字段包含请求中的字节数。对于 POST 请求，bytes 字段包含从客户端接收到的字节数。

## The error_log File — The error_log file lists messages from the scheduler (such as errors and warnings):

```
I [31/Mar/2006:09:48:47 +0200] Adding start banner page "none" to job 16.
I [31/Mar/2006:09:48:47 +0200] Adding end banner page "none" to job 16.
I [31/Mar/2006:09:48:47 +0200] Job 16 queued on 'grayscale' by 'root'.
I [31/Mar/2006:09:48:47 +0200] Started filter
/usr/lib/cups/filter/texttops (PID 4088) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started filter /usr/lib/cups/filter/
pstops (PID 4089) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started filter
/usr/lib/cups/filter/fomatic-rip (PID 4090) for job 16.
I [31/Mar/2006:09:48:47 +0200] Started backend
/usr/lib/cups/backend/parallel (PID 4091) for job 16.
```

行的条目（从左到右）解释如下：

- level 字段包含消息的类型：
  - `E`—发生错误。
  - `W`—服务器无法执行操作。
  - `I`—信息性消息。
  - `D`—调试消息。
- date-time 字段包含条目的日期和时间（例如，页面开始打印时）。该字段的格式与 access_log 文件中的 date-time 字段相同。
- message 字段包含自由格式的文本消息。

使用默认日志级别 info，仅请求和状态更改会记录到文件中。如果您希望记录错误，则需要在 cupsd /etc/cups/cupsd.conf 配置文件中更改 LogLevel 选项。对于调试和故障排除，将日志级别设置为 debug2。更改配置后，通过输入 rccups restart 重启 CUPS。

## The page_log File

page_log 文件列出发送到打印机的每个页面。

```
```text
grayscale root 16 [31/Mar/2006:09:48:57 +0200] 1 1 - localhost
```
```

每行包含以下信息（从左到右）：

- printer 字段包含打印该页面的打印机名称（在此示例中为 grayscale）。如果您将作业发送到打印机类，则该字段包含分配作业的打印机名称。
- user 字段包含提交此文件进行打印的用户的名称。
- job-id 字段包含正在打印的页面的作业编号（在此示例中为 16）。
- date-time 字段包含页面开始打印的日期和时间。该字段的格式与 access_log 文件中的 date-time 字段相同。
- page-number 字段包含页数（在此示例中为 1）。
- num-pages 字段包含副本数（在此示例中为 1）。对于无法自行产生副本的打印机，num-pages 字段始终为 1。
- job-billing 字段包含随 IPP create-job 或 print-job 请求提供的 job-billing 属性的副本——或（如果未提供）。
- hostname 字段包含产生打印作业的主机的名称（在此示例中为 localhost）。

## Configuration File

CUPS 的配置文件是 /etc/cups/cupsd.conf。它的格式与 Apache Web 服务器的配置文件相似。

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
| cups | 提供 cupsd 打印机守护进程。 |
| cups-client | 提供命令行打印工具。 |
| cups-libs | 应始终安装，因为许多程序（如 Samba）都链接到 CUPS 库。 |
| cups-drivers cups-drivers-stp | 提供打印队列的 PPD 文件。 |
| cups-SUSE-ppds-dat | 提供预生成的 `/etc/cups/ppds.dat` 文件。 |

**Table 12-1**

如果使用 YaST 进行打印机配置，这些文件将自动安装。YaST 还会在运行级别目录中创建符号链接，以确保在启动时自动启动 CUPS 守护进程。

打印系统所需的其他软件包，例如 ghostscript-library，会在标准安装期间自动选择。

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

