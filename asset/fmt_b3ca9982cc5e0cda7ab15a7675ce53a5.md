
# Caldera OpenLinux 与 Netfinity 服务器集成指南

您在其他任何地方都找不到的 Netfinity 服务器特定内容——包括 `ServeRAID` 配置！

分步骤规划、配置和安装关键服务：`Samba`、`Apache`、`Sendmail`、`DNS`、`DHCP`、`LDAP` 等。

Jakob Carstensen, Ivo Gomilsek, Lenz Grimmer, Jay Haskins 和 Joe Kaplenk

Jakob Carstensen, Ivo Gomilsek, Lenz Grimmer, Jay Haskins, 和 Joe Kaplenk

国际技术支持组织 (ITSO)

JAKOB CARSTENSEN ■ IVO GOMILSEK ■ LENZ GRIMMER ■ JAY HASKINS ■ JOE KAPLENK

![](img/2d69b129b41635ef36a3e6707d34b788_6_0.png)

本版适用于准备或安装 Caldera OpenLinux 2.3 或 Caldera OpenLinux eServer。

意见请邮寄至：

IBM Corporation, International Technical Support Organization

Dept. HZ8 Building 678

P.O. Box 12195

Research Triangle Park, NJ 27709-2195

当您向 IBM 咨询时，即授予 IBM 非排占性，允许其以认为适当的方式使用或分发信息，而无需对您承担任何义务。

由 Prentice-Hall PTR 出版

Prentice-Hall, Inc.

Upper Saddle River, NJ 07458

Prentice-Hall 图书被公司和政府机构广泛用于培训、营销和

批量订购本书时，出版商提供折扣。更多信息请联系

企业销售部，电话 800-382-3419；传真：201-236-7141；电子邮件：`corpsales@prenhall.com`；

Prentice-Hall PTR

企业销售部

One Street

Upper Saddle River, NJ

> 注意：在使用本信息及其支持的产品之前，请务必阅读附录 F 第 313 页的“注意事项”。

在美国打印

Prentice-Hall International (英国) 有限公司，伦敦

Prentice-Hall 澳大利亚有限公司，悉得尼

Prentice-Hall 加拿大公司，多伦多

Prentice-Hall 西班牙 S.A., 墨西哥城

Prentice-Hall 印度有限公司，新德里

Prentice-Hall 日本公司，东京

Pearson Education Asia 亚洲有限公司

Prentice-Hall 巴西公司 Ltda., 里地雅内卢

### 目录摘录

- 2.14 外设设备菜单 ................................................................... 93
- 9.4.1 下载并安装 `OpenLDAP` ....................................... 203
- 12.7 数据包如何通过网关传输 . . . . . . . . . . . 234
- 12.8 使用 `IP Chains` . . . . . . . . . . . . . . . . . . . . . . . 235
    - 12.8.1 如何创建规则 . . . . . . . . . . . . . . . . . . . . . . . . 236
    - 12.8.2 使规则持久化 . . . . . . . . . . . . . . . . . . . . . 238
- 12.9 附加信息来源 . . . . . . . . . . . . . . . . . . . . . . . . 238
- 13.1.4 初始化磁带 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 250
- 附录 A. RAID 级别 . . . . . . . . . . . . . . . . . . . . . 283
    - A.1 什么是 RAID? . . . . . . . . . . . . . . . . . . . . . . . . . . . 283
- 附录 D. IBM Netfinity 服务的硬件问题 .......................... 303
- 附录 E. 示例 `smb.conf`  .......................... 305
- 附录 F. 特别说明 ................................................... 313
- 附录 G. 相关出版物 ...................................................

感谢来自国际技术支持组织（Raleigh Center）的以下人员：

- Gail Christensen
- Shawn Walsh
- Linda Robinson
- David Watts
- Rufus Credle
- Margaret Ticknor
- Mike Haley

感谢以下 IBM 员工：

- Egan Ford，高级技术支持部
- Karl Schultz，`NetfinityServerProven`
- Julie Briddon，营销传播部
- Bo Brun，PC学院

## 欢迎反馈

您的意见对我们至关重要！

我们希望我们的红书（`redbooks`）能够尽可能提供帮助。请通过以下方式之一向我们发送关于本版或其他红书的意见：

- 将第 329 页“IBM Redbooks evaluation”中的评估表传真至表单上显示的传真号码。
- 使用位于 `http://www.redbooks.ibm.com/` 上的在线评估表。
- 通过电子便签将您的意见发送至 `redbook@us.ibm.com`

# 第 1 章 Linux 安装

本章详细描述了在 IBM Netfinity 服务器上安装和运行 Caldera OpenLinux 2.3 以及 Caldera OpenLinux eServer 测试版所需的各种安装步骤。我们还展示了在安装之前需要执行的步骤，以避免安装过程中出现问题。

## 1.1 了解您的硬件

在安装 Caldera OpenLinux 之前，您应该熟悉计算机中的硬件。您至少需要了解计算机以下组件的信息：

- 硬盘 - 接口类型（`SCSI` 或 `IDE`）和容量
- CD-ROM - 接口类型（`SCSI` 或 `IDE`）和制造商
- `SCSI` 适配器 - 制造商和型号数字
- 显示适配器 - 制造商和型号
- 鼠标 - 鼠标类型和连接器类型
- 网卡 - 制造商和型号
- `RAM` - 系统中的内存容量
- 显示器 - 制造商和型号

对于显示器，了解所有的技术规格是最好的。

对于 IBM Netfinity 服务器和其他 IBM 产品（包括显示器和 `SCSI` 适配器），所有信息的最终来源是：

```
ftp://ftp.ibm.com/pcircse/psref
```

在这里您可以找到所有当前及已淘汰的 IBM PC 产品的 `PSREF`（个人系统参考）表。您也可以通过以下网络资源找到许多有用信息：

```
http://www.pc.ibm.com/support
http://www.pc.ibm.com/us/netfinity/tech_library.html
```

## 1.2 硬件考虑

在本节中，我们描述了在安装 Caldera OpenLinux 时如何处理 IBM Netfinity 服务器中的硬件。

### 1.2.1 Adaptec SCSI 控制器

IBM Netfinity 服务器使用的所有版本 `Adaptec` `SCSI` 控制器均支持内核 2.2.10 及以上，这些内核用于 Caldera OpenLinux 2.3 和 Caldera OpenLinux eServer。

### 1.2.2 IBM ServeRAID 控制器

IBM Netfinity 服务器使用的所有版本 `IBM` `ServeRAID` 控制器都支持 Caldera OpenLinux 2.3 和 Caldera OpenLinux eServer。

### 1.2.3 IBM 令牌环网络适配器

`IBM` `ISA`、`PCMCIA` 和 `PCI` 令牌环网络适配器支持内核 2.2.10 及以上，这些内核用于 Caldera OpenLinux 2.3 和 Caldera OpenLinux eServer。

## 1.3 更新 BIOS 和 ServeRAID 控制器固件

在开始安装之前，确保您的所有硬件组件都具有最新版本的微代码至关重要。您可以从以下地址下载适用于您的 IBM Netfinity 服务器的最新 `BIOS`、诊断更新和 `ServeRAID` 控制器固件：

```
http://www.pc.ibm.com/support
```

对于网络产品，您可以在 `http://www.networking.ibm.com` 找到所有可用代码。

> **注意**
>
> 在安装之前，务必将 IBM Netfinity 服务器的 `BIOS` 更新到最新版本，并使用最新固件更新所有适配器。

![](img/2d69b129b41635ef36a3e670d34788_19_png)

## 1.4 使 CD-ROM 可启动

如果您想使用 `CD-ROM` 启动系统以开始安装，请确保 `CD-ROM` 位于启动序列之前。您可以在 IBM Netfinity 服务器 `BIOS` 中进行此操作。步骤如下：

- 开启服务器。
- 当看到 `IBM Logo` 时，按 `F1` 进入设置程序。
- 在设置程序中选择 `Start Options > Startup Sequence`。
- 确保 `CD-ROM` 位于第一个硬盘设备之前。
- 按 `Esc` 直到进入设置主窗口并选择 `Save Settings`（保存设置）。
- 按 `Enter` 确认当前设置。
- 退出设置程序。

> **注意**
>
> 也可以通过从设置程序加载默认设置使 `CD-ROM` 可启动，但请注意其他设置将是默认值。

## 1.5 Linux 安装

在本节中我们将描述如何在 IBM Netfinity 服务器上安装 Caldera OpenLinux 2.3 和 Caldera OpenLinux eServer。要成功完成安装，请遵循以下步骤：

1. 将 Caldera OpenLinux 2.3 或 Caldera OpenLinux eServer 插入 Netfinity 服务器的 `CD-ROM` 驱动器。当 `CD` 启动时，您将看到类似图 1 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_20_png)

加载初始 `ramdisk` 和内核后，您将看到类似图 2 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_21_png)

**硬件检测**

当检测到所有硬件时，您将看到类似图 3 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_22_png)

**语言选择**

选择一种语言并点击 `Next`（下一步）。您将看到类似图 4 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_23_png)

**鼠标设置**

2. 在此处您选择您的鼠标类型和设置。完成后，点击 `Next` 继续。您将看到类似图 5 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_24_png)

**键盘设置**

3. 在此窗口中，您选择键盘类型和布局。点击 `Next` 继续。您将看到类似图 6 的窗口。

## 选择显卡

| 显卡类型 (`Card Type`) | 通用 `SVGA` 兼容 |
| :--- | :--- |
| 您的显卡未被识别。尝试从列表中选择您的显卡。如果不在列表中，探测可能会找到所需信息，但在这种情况下也可能导致系统死机，请从列表中选择 `VGA` 兼容。 | 硬件详情： |
| 显存 (`Video RAM`) [ 1024 ] `KB` | |
| 频率 (`Mode clocks`) [ 可调至 (`MHz`): ] [ 170 ] 固定 (`MHz`): ] | |
| 探测 (`Probe`) 您可以在此处输入显卡详情，也可以进行探测。注意探测可能会导致系统死机。 | |

![](img/2d69b129b41635ef36a3e670d34788_25_png)

4. 在此处您选择用于显卡的 `XFree` 服务器。在选择 `XFree` 视频之前，请检查 299 页的附录 B，“IBM Netfinity 服务器的工作视频模式”。定义显卡类型时，安装程序会自动选取支持该显卡的 `XFree` 服务器。最好的方法是从 `Card Type` 滚动框选择支持您正在使用的显卡的 `XFree` 服务器。选择好 `XFree` 服务器后，您需要指定显存大小和频率。如果您不知道确切值，可以点击 `Probe` 来搜索显卡详情。

> **注意**
>
> 在成功探测显卡之前，您需要为显卡指定正确的 `XFree` 服务器。

如果您点击 `Probe`，将看到类似图 7 的窗口。如果选择 `VGA XFree` 服务器，安装程序将将从第 11 步继续。

![](img/2d69b129b41635ef36a3e670d34788_26_0.png)

图7 探测显卡之前

5. 点击 `Probe` 开始探测。窗口将短暂变为黑色。探测完成后，您将看到类似图 8 的窗口。

![](img/2d69b129b41635ef36a3e670d34788_26_1.png)

图8 成功探测显卡后

6. 如果由于某些原因无法正确识别显卡，您需要手动输入设置。如果您不知道正确设置，请选择 `VGA XFree` 服务器，并可以在安装完成后微调 `XFree`。点击 `OK` 返回显卡设置窗口。点击 `Next` 继续。您将看到类似图 9 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_27_0.png)

图 9. 选择显示器

7. 选择您正在使用的显示器类型。如果没有完全匹配您的显示器型号，请选择“典型显示器”（`Typical Monitors`）之一。选择与您正在使用的显示器最接近的一个。点击“下一步”（`Next`）继续，您将看到与图 10 类似的窗口。

## 选择视频模式

| 分辨率 | 深度 | 可用 | 水平同步 | 模式频率 |
|---|---|---|---|---|
| 1152*864 | 60 Hz | 8 `bpp` | 53.5 `kHz` | 89.8 `MHz` |
| 1152*864 | 69 Hz | 8 `bpp` | 44 `kHz` | 85 `MHz` |
| 1024*768 | 76 Hz | 8 `bpp` | 62.5 `kHz` | 85 `MHz` |
| 1024*768 | 70 Hz | 8 `bpp` | 56.5 `kHz` | 65 `MHz` |
| 1024*768 | 60 Hz | 8 `bpp` | 48.4 `kHz` | 65 `MHz` |
| 1024*768 | 87 Hz | 8 `bpp` | 35.5 `kHz` | 44.9 `MHz` |
| 800*600 | 65 Hz | 8 `bpp` | 55.4 `kHz` | 60.7 `MHz` |
| 800*600 | 75 Hz | 8 `bpp` | 40 `kHz` | 50 `MHz` |
| 800*600 | 60 Hz | 8 `bpp` | 37.5 `kHz` | 36 `MHz` |
| 640*480 | 65 Hz | 8 `bpp` | 43.2 `kHz` | 36 `MHz` |
| 640*480 | 75 Hz | 8 `bpp` | 37.5 `kHz` | 31.5 `MHz` |
| 640*480 | 70 Hz | 8 `bpp` | 36.5 `kHz` | 31.5 `MHz` |

![](img/2d69b129b41635ef36a3e6707d34b788_28_0.png)

图 10. 选择视频模式

在此窗口中，您可以选择喜好的视频模式、色彩深度和虚拟桌面大小。您可以在附录 B 第 29 页的“Netfinity 服务器工作视频模式”中找到 IBM Netfinity 服务器的可用模式。根据显卡内存的大小、色彩深度和分辨率，您可以拥有虚拟桌面。这是 Netfinity 服务器的一个功能。默认情况下，只显示与所选视频颜色和显示器兼容的模式。如果您是高级用户，可以勾选 `显示所有模式`（`Show all modes`）查看所有可用模式。可以通过点击 `测试此模式`（`Test this mode`）来选择视频模式。您将看到与图 11 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_29_0.png)

图 11. 测试视频模式

8. 点击 `确定`（`OK`）开始测试。如果您为硬件选择了工作模式，将获得一个清晰的图像以及关于如何返回安装界面的消息。如果您不进行任何操作，此图像将在 10 秒后消失。成功测试视频模式后，您将回到与图 10 类似的窗口。点击 `下一步`（`Next`）继续安装。您将看到与图 12 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_29_1.png)

图 12. 选择安装目标

12 Caldera OpenLinux 和 Netfinity 集成指南

9. 此时，您可以选择想要使用的分区类型。您有三个选项：

- `整个硬盘`（`Entire hard disk`）：如果系统中没有找到之前的 Linux 安装，则默认勾选此选项。这意味着整个磁盘将用于 Caldera OpenLinux 的安装。
- `已准备的分区`（`Prepared partition(s)`）：只有在硬盘上找到之前的 Linux 安装时才启用此选项。如果您选择此选项，安装过程将使用现有的分区。
- `自定义（仅限专家！）`（`Custom (expert only!)`）：如果您想创建自己的分区方案，请使用此选项。
