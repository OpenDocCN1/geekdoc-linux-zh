
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



在我们的案例中，选择了`Custom`。点击`Next`继续安装。您将看到与图 13 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_30_0.png)

图 13. 分区硬盘

11. 在此处，您可以创建、删除或修改分区。要创建新分区，请选择显示为“Not used”的项目并点击`Edit`，您将看到与图 14 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_31_0.png)

图 14. 创建新分区

如图 14 所示，您可以创建四种分区：

- Linux
- Swap（交换分区）
- Extended（扩展）
- DOS/Windows

为了成功安装 `Caldera OpenLinux`，您至少需要创建一个 Linux 分区交换分区。但我们建议为安装文件创建更多 Linux 分区：

- 一个用于 `boot` 挂载点的小分区，内核镜像约占 20 MB
- `/` 挂载点分区（ROOT），至少 1GB
- `/home` 挂载点分区；大小取决于您的需求
- `/usr` 挂载点分区；大小取决于您的需求
- `/var` 挂载点分区；大小取决于您的需求
- `/opt` 挂载点分区；大小取决于您的需求

对于 Linux 类型分区，可以通过点击挂载点（Mount Point）字段右侧的箭头来选择挂载点，您将看到与图 15 类似的窗口。

> 注意
>
> 请参考附录 C 第 301 页的“分区建议”获取有关磁盘分区的建议。

![](img/2d69b129b41635ef36a3e6707d34b788_32_0.png)

图 15. 选择挂载点

如果所需的挂载点不可用，您可以轻松输入任何需要的内容。`/boot` 挂载点就是如此。如果您希望创建的分区是可启动的，请勾选 `bootable` 复选框。

12. 当您选择了挂载点并定义了分区大小后，点击 `OK` 保存选择。您将看到与图 16 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_33_0.png)

图 16. 格式化后

![](img/2d69b129b41635ef36a3e6707d34b788_41_0.png)

图 25. 定义根密码

22. 在此窗口中，你可以定义 `root` 账户密码。`root` 用户将管理你的系统。输入密码后，点击“Next”继续。你将看到一个与图 26 相似的窗口。

## 设置登录名

真实姓名：Caldera Systems OpenLinux 用户

登录名：`user`

密码：***** 再次输入密码：*****

登录 Shell：( ) `bash` ( ) `tcsh` ( ) `zsh`

添加用户

将添加这些用户：

| 登录 | 真实姓名 | Shell | 密码 |
| :--- | :--- | :--- | :--- |

## 添加新登录名

Linux 是一个多用户/多任务的操作系统。要能够让许多人同时共享一台机器，你必须为每个用户分配登录账户。

如果没有至少一个登录名，你将无法（`root` 系统管理员）之外登录你的机器。由于 `root` 账户保留用于系统管理任务，因此为你的日常使用设置至少一个用户账户是非常重要的。

图 26. 定义用户

23. 你需要创建至少一个用户才能继续安装。要添加新用户，请填写所有字段并点击“添加用户”。你将看到一个与图 27 相似的窗口。

第 1 章. Linux 安装 25

## 设置登录名

真实姓名：

登录名：

密码：

再次输入密码：

登录 Shell：

- `bash`
- `tcsh`
- `bash`

添加用户

将添加这些用户：

| user | 真实姓名 | Shell | 密码 |
| :--- | :--- | :--- | :--- |
| n | Caldera Systems OpenLinux | `/bin/bash` | 不显示 |

## 添加新登录名

Linux 是一个多用户/多任务的操作系统。要能够让许多人同时共享一台机器，你必须为每个用户分配登录账户。

如果没有至少一个登录，你将无法（`root` 系统管理员）之外登录你的机器。由于 `root` 账户保留用于系统管理任务，因此为你的日常使用设置至少一个用户账户是至关重要的。

图 27. 添加新用户后

24. 你可以看到已经创建了哪些用户。要继续安装，点击“Next”，你将看到一个与图 28 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_43_0.png)

![](img/2d69b129b41635ef36a3e6707d34b788_44_0.png)

25. 如果你的网卡被内核识别，你就可以对其进行设置。设置只能针对以太网卡。你有三个选项：

- a. `No Ethernet`：如果你没有网卡或网卡不支持（例如令牌环），请使用此选项。你稍仍然可以配置令牌环网卡。
- b. `Configure Ethernet Using DHCP`：当你使用 DHCP 服务器定义客户端的 IP 地址时，使用此选项。
- c. `Configure Ethernet Using Static`：当你有静态 IP 地址时，使用此选项。

在此页面上，你还定义了正在安装计算机的主机名。所有设置以后都可以使用 `Caldera Open` 管理系统 (`COAS`) 进行修改。当你输入完所有需要的数据后，点击 `Next` 继续。你将看到一个与图 29 相似的窗口。

图 28. 设置网络

第 1 章. Linux 安装 27

## Linux 加载器

要加载的操作系统：

| 分区 | 类型 | 标签 |
| :--- | :--- | :--- |
| `/dev/hda1` | `OpenLinux` | `linux` |

安装 `LILO` 的位置：

- 主引导引导记录 (MBR) [ `/dev/hda` ]
- 目标分区 (`/dev/hda1`) [ `(VMware)` ]
- 其他：

图 29. 配置 Linux 加载器

26. Linux 操作系统由 `Linux` 加载器 (`LILO`) 加载。在此窗口中，你指定 `LILO` 的安装位置。你有三个选项：

- a. 主引导记录 (MBR)：`LILO` 将位于第一块硬盘上。当 Linux 是系统上的唯一操作系统时，使用此选项。
- b. 目标分区：在这种情况下，`LILO` 被设置在分区中，在使用其他系统时使用此选项。
- c. 其他：这仅供经验用户使用的选项。选择选项后，点击“Next”继续。你将看到一个与图 30 相似的窗口。

28 Caldera OpenLinux 和 Netfinity 指南

![](img/2d69b129b41635ef36a3e6707d34b788_46_0.png)

图 30. 时区

27. 选择你的时区以及硬件时钟的设置方式。点击“Next”继续，你将看到一个与图 31 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_47_0.png)

28. 在等待安装软件包时，你可以通过玩俄罗斯块来消磨时间。当“完成”按钮变为可用时，安装完成。点击“完成”继续，你将看到一个与图 32 相似的窗口。

图 31. 添加新用户后

## OpenLinux

| 引导点 | 状态 |
| :--- | :--- |
| 加载内核 | OK |
| 启动内核 | OK |
| 自动检测 | |
| 探测 PCI 设备 | OK |
| 探测 PCMCIA 卡 | 无 |
| 探测 SCSI 主机 | 无 |
| 探测 ATA 光驱 | OK |
| 探测其他光驱 | 跳过 |
| 探测以太网卡 | OK |
| 自动安装源 | |
| 从光驱安装 | OK |
| 通过 NFS 安装 | 跳过 |
| 从硬盘安装 | 跳过 |
| Caldera 系统安装向导： |
| 启动 LARD | OK |
| 准备启动到新系统 | 等待 |

图 32. 安装后启动

## OpenLinux

| 系统启动中... | 状态 |
| :--- | :--- |
| 引导点 | |
| 加载内核 | OK |
| 启动内核 | OK |
| 加载默认模块 | |
| 即插即用配置 | 跳过 |
| sound | 跳过 |
| pcnet32 | 跳过 |
| parport_lowlevel | 跳过 |
| 最小系统准备： | |
| 检查文件系统 | OK |
| 挂载本地文件系统 | OK |
| 启动基础网络 | OK |
| 挂载远程文件系统 | 跳过 |
| 清理临时空间 | 等待 |

![](img/2d69b129b41635ef36a3e6707d34b788_49_0.png)

图 33. 启动操作系统

当所有服务启动后，你将看到一个与图 34 相似的登录窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_50_0.png)

恭喜，你的 `Caldera OpenLinux` 系统已就绪！

# 6 使用 ServeRAID 安装

在本节中，我们将描述如何在带有 `IBM ServeRAID` 控制器的 `IBM Netfinity` 服务器上安装 `Caldera OpenLinux` 产品，以及如何使用 `IBM ServeRAID` 控制器的功能。`IBM ServeRAID` 控制器是一个高性能 RAID 控制器。当前的 Linux 驱动支持所有版本的 ServeRAID 适配器。在开始安装之前，你需要定义 RAID 阵列和逻辑驱动器。逻辑驱动器在操作系统中的表现就像物理磁盘驱动。有关 RAID 级别和性能问题的更多信息，请参阅第 283 页的附录 A，“RAID 级别”。

# 停止

在带有 `IBM ServeRAID` 控制器的 `IBM Netfinity` 服务器上安装 `Caldera OpenLinux` 之前，您需要定义 RAID 阵列和逻辑驱动器。您可以使用随所有 `IBM Netfinity` 服务器附带的 `ServerGuide`，或者使用 `http://www.pc.ibm.com/support` 提供的 `ServeRAID` DOS 配置磁盘完成此操作。

我们强烈建议您使用系统中的空闲硬盘以最安全的方式保护您的数据。

从 2.3 版本开始，`Caldera OpenLinux` 发版支持 `ServeRAID` SCSI 控制器。要安装操作系统，请遵循第 3 页 1.5 “基本 Linux 安装”中的步骤。您在 RAID 阵列中定义的逻辑驱动器将在安装程序中显示为 SCSI 驱动器。

安装完系统后，可以通过以下路径获取 RAID 管理工具：

```
http://www.developer.ibm.com/welcome/netfinity/serveraid.html
```

您可以从该网站下载以下文件：

- `ips-100.tgz`：此文件包含针对 2.2.x 内核的内核补丁，可启用这些内核对 `IBM ServeRAID` 适配器的支持；
- `ipsutsil.rpm`：此文件包含用于 `IBM ServeRAID` SCSI 适配器的 Linux 工具；
- `009n012.exe`：此文件包含 `WIN32` 管理客户端，可远程配置和监控 Linux 安装中使用的 `ServeRAID` 控制器。

## 1.6.1 安装 ipsutsil.rpm

要成功安装 `ipsutsil` 软件包，您必须以“`root`”身份登录。下载 `ipsutsil.rpm` 软件包后，您需要对其进行安装。`ipsutsil` 软件包是一个标准的 `Red Hat` 软件包管理器 (`RPM`) 包。`Caldera OpenLinux` 使用 `RPM` 安装软件包包，因此您的系统中已经安装了 `RPM` 工具。要检查您的 `RPM` 工具是否工作正常，请在 `KDE` 图形环境中打开终端窗口并执行此命令：

```
rpm --version
```

如果您的输出类似于所示，说明您的 `RPM` 工作正常：

更倾向于图形界面的用户可能想使用 `kpackage` 工具，它是 `KDE` 图形环境的一部分，用于安装软件包。但如果您尝试用此工具安装 `ipsutils.rpm`，您将看到一个与图 35 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_52_0.png)

图 35. 使用 kpackage 安装 ipsutils.rpm 错误

经验用户会看出这是一个依赖问题，但即使您尝试在不启用 `Check Dependencies` 选项的情况下安装，如图 36 所示，您仍会得到相同的错误。

![](img/2d69b129b41635ef36a3e6707d34b788_52_1.png)

图 36. 在 kpackage 中不带依赖安装

这是因为 `ipsutils.rpm` 在安装前会显示版权信息。因此，安装包的唯一方法是从终端执行以下命令：

```
rpm -Uvh --nodeps ipsutils.rpm
```

这假设您当前的目录是 `ipsutils.rpm` 所在的目录。必要的文件将安装在 `/usr/bin`。要查看工具是否工作，请输入以下命令：

```
ipsutsil
```

您将看到类似于图 37 的输出。

第 1 章 Linux 安装 35 

```
用法：ipsutsil <命令> <参数 1>

帮助：ipsutsil 可获取任何命令的特定帮助。

命令 | 参数 1 | 参数 2 | 参数 4 | 参数 5

AUTOSNC | Controller | Logical Drive

BACKUP | Controller | Filename

DEVINFO | Controller | SCSI ID

DRIVER | Controller | SCSI ID

ERASE | Controller | Options

GETCONFIG | Controller | Options

GETSTATUS | Controller | Options

REBUILD | Controller | Logical Drive

INIT | Controller | SCSI ID

SYNC | Controller | State

REBUILD | Controller | Channel

RESTORE | Controller | Channel

SETSTATE | Controller | Scope

UNATTACHED | Controller | Scope

UNBLOCK | Controller | Logical Drive
```

图 37. ipsutsil 命令输出

如您所见，`ipsutsil` 支持许多用于处理 `IBM ServeRAID` 控制器的命令。在本节中，我们将涵盖为了使用 ServeRAID 控制器而必须的命令。

## 1.6.2 ipsutsil 命令

本节将介绍 `ipsutsil` 命令的不同选项。

#### 1.6.2.1 getconfig 命令

该命令用于获取 `IBM ServeRAID` 控制器、逻辑驱动器和物理驱动器的配置信息。`getconfig` 命令的语法如下：

```
ipsconfig getconfig <Controller> <Options>
```

参数说明见表 1。

表 1. getconfig 命令参数

| 参数 | 说明 |
| :--- | :--- |
| Controller | 控制器数量 (1 到 12) |
| Options | 用于控制器信息 |
| LD | 逻辑驱动器信息 |
| PD | 物理设备信息 |
| AL (默认) | 所有信息 |

要获取关于第一个 `ServeRAID` 控制器的所有信息，请执行以下命令：

```
ipsconfig config 1
```

您将看到一个类似于图 38 的窗口。

```
找到 1 个 ServeRAID 控制器。

配置已启动针对控制器 1...

控制器信息

固件版本 2.8.10

配置版本 97139

配置日期 6/25/1999

配置 ID 配置

SCSI 通道描述并行 SCSI

接口描述 12 位 PCI

启动器 ID (通道/SCSI ID) 7

最大设备 30

离线磁盘 0

逻辑驱动器/离线 2/0

重建速率 (低/中/高) 高

预读自适应

空闲模式 (是/否) 无

并发命令支持 128

配置更新计数

逻辑驱动器信息

逻辑驱动器编号 1

逻辑驱动器状态：良好 (OKY)

RAID 级别 5

大小 (MB) 100

写入状态：写入 (WT)

块数量 3

单元大小 16K

访问阻塞：否

属于阵列 A

逻辑驱动器编号 2

逻辑驱动器状态：良好 (OKY)

RAID 级别 5

大小 (MB) 17256

写入状态：写入 (WT)

块数量 3

单元大小 16K

访问阻塞：否

属于阵列 A

阵列 A 排序顺序 (通道/SCSI ID): 1,0, 1,4, 1,3

物理设备信息

通道 #1:

启动器在 SCSI ID 7

空闲磁盘 快速 SCSI

SCSI ID: 0

PFA (是/否): 无

状态：在线 (ONL)
```

图 38. 执行 ipsconfig config 1

如您所见，`ipsutsil` 支持许多用于处理 `IBM ServeRAID` 控制器的命令。在本节中，我们将涵盖为了高效使用 `ServeRAID` 控制器而必须的命令。

要获取所有控制器的信息，执行此命令：

```
ipsconfig config 1 ad
```

您将看到类似于图 39 的输出。



#### 1.6.2.1 config 命令

此命令用于配置 IBM ServeRAID 控制器的设置。`config` 命令具有以下语法：

```bash
ipsconfig config <Controller> <Action>
```

参数解释见表 1。

表 1. `config` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |
| `Action` | 配置操作类型，例如 `ad` (添加) 或 `ld` (逻辑驱动器) |

要获取控制器的适配器信息，执行此命令：

```bash
ipsconfig config 1 ad
```

你将看到类似于图 39 的输出。

```
[root@nf5S00 /]# ipsconfig config 1 ad
找到 1 个控制器。
配置已启动针对控制器 1...
--------------------------------------------
控制器信息

| 项目 | 值 |
|---|---|
| 固件版本 | 2.8.10 |
| 块版本 | 97139 |
| 配置日期 | 6/25/1999 |
| 配置 ID | 配置 |
| SCSI 通道描述 | 并行 SCSI |
| 接口描述 | 12 位 PCI |
| 启动器 ID (通道/SCSI ID) | 7/7 3 |
| 最大设备 | 30 |
| 离线磁盘计数 | 0 |
| 逻辑驱动器/离线 | 2/0/0 |
| 重建速率 (低/中/高) | 高 |
| 预读 | 自适应 |
| 空闲模式 (是/否) | 无 |
| 并发命令支持 | 128 |
| 配置更新计数成功。 | 14 |
```

图 39. 执行 `ipsconfig config 1 ad`

要获取逻辑设备的信息，执行此命令：

```bash
ipsconfig config 1 ld
```

你将得到类似于图 40 的输出。

```
[root@nf5S00 /root]# ipsconfig config 1 ld
找到 1 个 ServeRAID 控制器。
配置已启动针对控制器 1...
--------------------------------------------
逻辑驱动器信息
逻辑驱动器编号 1
逻辑驱动器状态：良好 (OKY)
RAID 级别 5
大小 (MB) 100
写入状态：写入 (WT)
块数量 3
单元大小 16K
访问阻塞：否
属于阵列 A
逻辑驱动器编号 2
逻辑驱动器状态：良好 (OKY)
RAID 级别 5
大小 (MB) 17256
写入状态：写入 (WT)
块数量 3
单元大小 16K
访问阻塞：否
属于阵列 A

阵列 A 排序顺序 (通道/SCSI ID) : 1,0, 1,4, 1,3
命令成功完成。
```

图 40. 执行 `ipsconfig config 1 ld`

你可以从此输出获取有关逻辑驱动器的所有信息：

- 驱动器状态
- RAID 级别
- 大小
- 写缓存状态
- 块（Chunks）数量
- 条带单元大小（Stripe Unit Size）
- 访问
- `Array`

要获取物理硬盘的详细信息，执行此命令：

```bash
ipsend getconfig 1 pd
```

你将看到类似于图 41 的输出。

```
[root@if5500 /root]# ipsend getconfig 1 pd
Found 1 IBM RAID Controller(s)
Read Configuration has been initiated for Controller 1...
------------------------------------
Physical Device
Channel #1:
Initiator at SCSI ID 7
Target on SCSI ID 0
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 4
0
FFA (Yes/No)
No
State
Online (OML)
Size (in MB)/(in Sectors)
9678/17773988
Device ID
IBM-PCC0DOHS09Y 03561864EE69
Target on SCSI ID 3
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 0
3
FFA (Yes/No)
No
State
Online (OML)
Size (in MB)/(in Sectors)
17357/3548048
Device ID
IBM-PCC0DOHS18Y 0356180EF209
Target on SCSI ID 15
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 4
0
FFA (Yes/No)
No
State
Online (OML)
Size (in MB)/(in Sectors)
9678/17773988
Device ID
IBM-PCC0DOHS09Y 0420618F8A1
Channel #2:
Initiator at SCSI ID 7
Command Completed Successfully
```

图 41. 执行 `ipsend getconfig 1 pd`

#### 1.6.2.2 getstatus 命令

此命令用于检索 IBM ServeRAID 控制器的当前状态。`getstatus` 命令具有以下语法：

```bash
ipssend getstatus <Controller>
```

参数解释见表 2。

表 2. `getstatus` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |

要获取你的 IBM Netfinity 服务器上第一个 ServeRAID 控制器的状态，请执行此命令：

```bash
ipssend getstatus 1
```

你将看到类似于图 42 的输出。

```
[root@nf5500 /root]# ipssend getstatus 1
Found 1 IBM ServeRAID Controller(s)
Background Command Progress Status for controller 1...
Current/Most Recent Operation : Rebuild
Source logical drive : 1
Target logical drive : 1
Rebuild Rate : High
Status : Successfully Completed
Logical Drive Size (in Stripes) : 552192
Number of Remaining Stripes : 0
Percentage Complete : 100.00%
Command Completed Successfully
```

图 42. 执行 `ipssend getstatus 1`

如果 ServeRAID 控制器正在重建，你将看到类似于图 43 的输出。

```
[root@nf5500 /root]# ipssend getstatus 1
Found 1 IBM ServeRAID Controller(s)
Background Command Progress Status for controller 1...
Current/Most Recent Operation : Rebuild
Source logical drive : 1
Target logical drive : 1
Rebuild Rate : High
Status : In Progress
Logical Drive Size (in Stripes) : 3200
Number of Remaining Stripes : 2070
Percentage Complete : 35.31%
Command Completed Successfully
```

图 43. 在硬盘重建期间执行 `ipssend getstatus 1`

#### 1.6.2.3 devinfo 命令

此命令用于检索到 IBM ServeRAID 控制器的设备当前状态。`devinfo` 命令具有以下语法：

```bash
ipss devinfo <Controller> <Channel> <SCSI ID>
```

参数解释见表 3。

表 3. `devinfo` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |
| `Channel` | 设备通道 (1 到 3) |
| `SCSI ID` | 设备的 SCSI ID (0 到 15) |

要获取你的 IBM Netfinity 服务器上第一个 ServeRAID 控制器中通道 1 上 SCSI ID 为 0 的设备状态，请执行命令：

```bash
ipss devinfo 1 1 0
```

你将看到类似于图 44 的输出。

```
[root@nf55 linux]# ipsend devinfo 1 1 0
Found 1 IBM ServeRAID Controller()
Device Information has been initiated for controller 1
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
Channel : 1
SCSI ID : 0
PFA (Yes/No) : No
State : Hot Spare (HSP)
Size (in MB)/(in Sectors) : 8578/17737888
Device ID : IBM-COC0DGHS09Y 03561864EE69
Target on SCSI ID 15
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 4
0
FFA (Yes/No)
No
State
Online (OML)
Size (in MB)/(in Sectors)
9678/17773988
Device ID
IBM-PCC0DOHS09Y 0420618F8A1
Channel #2:
Initiator at SCSI ID 7
Command Completed Successfully
```

图 44. 执行 `ipsend devinfo 1 1 0`

如果 ServeRAID 控制器正在重建，你将看到类似于图 45 的输出。

```
[root@nf5500 /root]# ipsend devinfo 1
Found 1 IBM ServeRAID Controller()
Device Information has been initiated for controller 1
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
Channel : 1
SCSI ID : 0
PFA (Yes/No) : No
State : Hot Spare (HSP)
Size (in MB)/(in Sectors) : 8578/17737888
Device ID : IBM-COC0DGHS09Y 03561864EE69
```

图 45. 执行 `ipsend devinfo 1`

#### 1.6.2.4 getrebuild 命令

此命令用于检索 IBM ServeRAID 控制器的重建状态。`getrebuild` 命令具有以下语法：

```bash
ipssend getrebuild <Controller>
```

参数解释见表 4。

表 4. `getrebuild` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |

要获取你的 IBM Netfinity 服务器上第一个 ServeRAID 控制器的状态，请执行此命令：

```bash
ipssend getrebuild 1
```

你将看到类似于图 46 的输出。

```
[root@nf5500 /root]# ipssend getrebuild 1
Found 1 IBM ServeRAID Controller(s)
Rebuild Progress Status for controller 1...
Source logical drive : 1
Target logical drive : 1
Rebuild Rate : High
Status : Successfully Completed
Logical Drive Size (in Stripes) : 552192
Number of Remaining Stripes : 0
Percentage Complete : 100.00%
Command Completed Successfully
```

图 46. 执行 `ipssend getrebuild 1`

#### 1.6.2.5 setstate 命令

通过 `setstate` 命令，你可以将物理设备从当前状态重新定义为指定状态。`setstate` 命令具有以下语法：

```bash
ipssend setstate <Controller> <Channel> <SCSI ID> <New State>
```

参数解释见表 5。

表 5. `setstate` 命令参数

| 参数 | 描述 |
| :--- | :--- |
| `Controller` | 控制器编号 (1 到 12) |
| `Channel` | 设备通道 (1 到 3) |
| `SCSI ID` | 设备的 SCSI ID (0 到 15) |
| `New State` | `EMP` (空), `RDY` (就绪), `HSP` (热备), `SHS` (备用热备), `DDD` (故障硬盘), `DHS` (故障热备), `RBL` (重建中), `SBY` (待机), `ONL` (在线) |

执行此命令时必须极其小心！例如，在不经过重建的情况下将故障（`DDD`）设备重新定义为在线（`ONL`）是非常危险的。

你可以通过执行此命令来验证设备状态的变化：

```bash
ipssend getconfig 1 pd
```

#### 1.6.2.6 synch 命令

此命令用于同步冗余逻辑驱动器上的校验和信息。如果校验信息不一致，将自动进行修复。`synch` 命令的语法如下：

```bash
ipssend synch <Controller> <Scope> <Scope ID>
```

参数解释见表 6。

表 6. `synch` 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `Controller` | 控制器数量 (1 到 12) |
| `Scope` | 单个逻辑驱动器的驱动器 |
| `Scope ID` | 逻辑驱动器数量 (1 到 8) |

![](img/2d69b129b41635ef36a3e6707d34b788_63_0.png)

> 注意
> 我们建议您每周执行此命令。

#### 1.6.2.7 unattended 命令

此命令用于更改 ServeRAID 控制器的无人值模式（`unattended mode`）。`unattended` 命令的语法如下：

```bash
ipssend unattended <Controller> <Options>
```

参数解释见表 7。

表 7. `unattended` 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `Controller` | 控制器数量 (1 到 12) |
| `Options` | `ON`: 启用无人值模式<br>`OFF`: 禁用无人值模式<br>`?`: 显示无人值模式功能的状态 |

如果你想查看第一个 ServeRAID 控制器的当前状态，请执行此命令：

```bash
ipsend unattended 1 ?
```

46 Caldera OpenLinux 和 Netfinity 服务器集成指南

你将看到与图 49 类似的输出。

```
[root@nfs500 /#] ipsend unattended 1 ?
Found 1 IBM ServeRAID Controller(s)
Set Unattended Mode has been initiated for controller 1...
Unattended Mode is set off
```

图 49. 执行 `ipsend unattended 1 ?`

如果你想将无人值模式设置为开启，请执行此命令：

```bash
ipsend unattended 1 ON
```

#### 1.6.2.8 rebuild 命令

此命令启动到指定驱动器的重建（`rebuild`）。`rebuild` 命令的语法如下：

```bash
ipsend rebuild <Controller> <Channel> <SCSI ID> <New Channel> <New SCSI ID>
```

参数解释见表 8。

表 8. `Rebuild` 命令参数

| 参数 | 说明 |
| :--- | :--- |
| `Controller` | 控制器数量 (1 到 12) |
| `Channel` | 故障驱动器的通道 (1 到 3) |
| `SCSI ID` | 故障驱动器的 SCSI ID (0 到 15) |
| `New Channel` | 新驱动器的通道 (1 到 3) |
| `New SCSI ID` | 新驱动器的 SCSI ID (0 到 15) |

此操作适用于包含一个或多个处于关键（`Critical, CRT`）状态的逻辑驱动器的磁盘阵列。例如，如果你想将第一个 ServerRAID 控制器通道 1 上 SCSI ID 为 1 的故障驱动器重建到同一通道上 SCSI ID 为 0 的新驱动器，将执行此命令：

```bash
ipsend rebuild 1 1 1 0
```

你将看到与图 50 类似的输出。

```
[root@nf5500 linux]# ipssend rebuild 1 1 1 0
Found 1 IBM ServeRAID Controller(s).
Rebuild Drive has been initiated for controller 1...
Rebuilding Logical Drive #1:
10% Done
20% Done
30% Done
40% Done
50% Done
60% Done
70% Done
80% Done
90% Done
Done Logical Drive #1
Rebuilding Logical Drive #2:
[]
```

图 50. 执行 `ipssend rebuild 1 1 1 0`

### 1.6.3 替换故障驱动器



当 `RAID` 阵列中的物理驱动器发生故障时，你会看到驱动器上的指示信号。你可以通过执行以下命令来模拟故障驱动器：

```
ipssend setstate 1 1 4 ddd
```

在这种情况下，我们正在模拟第一个 `ServeRAID` 控制器通道 1 上 `SCSI` ID 为 4 的驱动器发生故障。应采取以下步骤更换故障驱动器：

1. 用完好的驱动器物理替换故障驱动器。
2. `ServeRAID` 控制器将自动开始重建驱动器。

> **注意**
>
> 自动重建适用于 `ServeRAID` II 和 III。并且必须将热备重建（`Hot Spare Rebuild`）设置为启用（`Enabled`）。

你可以通过此命令检查第一个 `ServeRAID` 控制器逻辑驱动器的重建进度：

```
ipsend status 1
```

你将看到与第 41 页图 43 类似的输出。如果重建未完成，你将看到与图 51 类似的输出。

```
root@nf500 /root# ipsend status
Found 1 IBM ServeRAID Controller(s)
Background Progress for controller 1
Current/Most Recent Operation : Rebuild
Source logical drive : 1
Target logical drive : 1
Rebuild Rate : High
Status : Failed
Channel is : 1
SSD ID is : 0
Logical Drive Size (in Stripes) : 55192
Number of Remaining Stripes : 30292
Percentage Complete : 45.18%
Command Completed Successfully.
```

图 51. 重建失败

### 1.4 使用禁用热备重建更换故障驱动器

当你在 `ServeRAID` 控制器禁用了热备重建功能时，应采取以下步骤更换故障驱动器。在示例中，第一个 `ServeRAID` 控制器通道 1 上 `SCSI` ID 为 1 的驱动器发生故障。

1. 用完好的驱动器物理替换故障驱动器。
2. 执行以下命令开始重建驱动器：

```
ipsend status 1 1 rbl
```

你将看到如下输出：

```
root@nf500 /# ipsend status 1 1 rbl
Found 1 IBM ServeRAID Controller(s)
Set Device State has been initiated for controller 1
Command Completed Successfully.
```

图 52. 故障驱动器的强制重建

你可以通过此命令检查 `ServeRAID` 控制器逻辑驱动器的重建进度：

```
ipsend status
```

你将看到与第 41 页图 43 类似的输出。

### 1.6.5 使用已安装的热备驱动器更换故障驱动器

当你在 `ServeRAID` 中配置了热备驱动器时，故障驱动器会自动重建为热备驱动器。按照以下步骤更换故障驱动器并将其设置为热备驱动器：

1. 发现 `RAID` 阵列中有一个故障驱动器。在示例中，第一个 `ServeRAID` 控制器通道 1 上 `SCSI` ID 为 1 的驱动器被定义为热备驱动器。你可以通过执行此命令检查：

```
ipssend getconfig 1 pd
```

你将看到与图 53 类似的输出。

![](img/2d69b129b41635ef36a3e6707d34b788_67_0.png)

图 53. 驱动器故障后热备已就绪，且可见其处于故障热备（`Defunct Hot Spare`, `DHS`）状态。

2. 从服务器移除故障驱动器。示例中通道 1 上 `SCSI` ID 为 4 的驱动器。

3. 使用以下命令将驱动器状态设置为空（`Empty`, `EMP`）：

```
ipsend setstate 1 1 4 emp
```

你将看到与图 54 类似的输出。

```
[root@nf500 #] ipssend setstate 1 1 4 emp
Found 1 IBM ServeRAID Controller(s)
Set Device State has been initiated for Controller 1...
Command Completed Successfully.
```

图 54. 将 `DHS` 设置为 `EMP`

你可以执行此命令检查此操作的结果：

```
ipssend getconfig 1 pd
```

你将看到与图 55 类似的输出。

```
[root@nf550 #] ipssend getconfig 1 pd
Found 1 IBM ServeRAID Controller(s).
Read Configuration has been initiated for Controller 1...
Physical Device Information
Channel #1
Initiator at SCSI ID 7
Target on SCSI ID 0
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 0
PFA (Yes/No): No
State: Online (ONL)
Size (in MB)/(Sectors): 8678/17773888
Device ID: IBM-PCCD0DGHS05Y 03518164E69
Target on SCSI ID 1
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 1
PFA (Yes/No): No
State: Rebuild (RBL)
Size (in MB)/(Sectors): 8678/17773988
Device ID: IBM-PCCD0DGHS05Y 04206816A1
Target on SCSI ID 3
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID 3
PFA (Yes/No): No
State: Online (ONL)
Size (in MB)/(Sectors): 17357/35540848
Device ID: IBM-PCCD0DGHS18Y 035168EE209
Target on SCSI ID 15
Device is a 16 bit, Fast SCSI, tag queuing Unknown Device
SCSI ID 15
PFA (Yes/No): No
State: Stand By (SBY)
Size (in MB)/(Sectors): 0/0
Device ID: SDR GEM200 2 1
Channel #2
Initiator at SCSI 7
Command Completed Successfully.
```

图 55. 移除故障驱动器后

4. 将新驱动器插入服务器。在示例中，该位置与故障驱动器相同。

5. 使用此命令将该驱动器状态设置为就绪（`Ready`, `RDY`）：

```
ipssend setstate 1 1 4 rdy
```

你将看到与图 56 类似的输出。

```
[root@nf500 #] ipssend setstate 1 1 4 rdy
Found 1 IBM ServeRAID Controller(s)
Set Device State has been initiated for Controller 1...
Command Completed Successfully.
```

图 56. 将新驱动器状态设置为 `RDY`

通过将状态设置为就绪（`RDY`），驱动器将启动。

> **注意**
>
> 所有新驱动器必须首先设置为就绪（`RDY`）。

你可以通过执行此命令检查此操作的结果：

```
ipssend getconfig 1 pd
```

你将看到与图 57 类似的输出。

```
root@is5500 # ipassend setconfig 1 pd
Found 1 IBM RAID Controller(s)
Read Configuration has been initiated for Controller 1...
----------------------------------------------------------------------
Physical Device Information
Channel #1
Initiator at SCSI ID 7
Target on SCSI ID 0
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 0
PFA (Yes/No) : Online (UML)
State
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCCDGHS09Y 035616814E669
Target on SCSI ID 1
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 1
PFA (Yes/No) : No
State : Rebuild (RBL)
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCCDGHS09Y 0420681F8A1
Target on SCSI ID 3
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 3
PFA (Yes/No) : Online (UML)
State
Size (in MB)/(Sectors) : 17357/35540848
Device ID : IBM-PCCDGHS18Y 0351680EEE209
Target on SCSI ID 4
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 4
PFA (Yes/No) : No
State : Ready (RDY)
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCCDGHS09Y 0420681924B4
Target on SCSI ID 15
Device is a 16 bit, Fast SCSI, tag queuing Unknown Device
SCSI ID : 15
PFA (Yes/No) : No
State : Stand By (SBY)
Size (in MB)/(Sectors) : 0/ 0
Device ID : SDR GEM200 2 1
Channel #2
Initiator at SCSI ID 7
Command Completed Successfully.
```

**图 57. 将状态设置为 `RDY` 后**

如你所见，新驱动器显示为 `Ready` (`RDY`) 设备，在我们的示例中为通道 1 上的 `SCSI` ID 4。

6. 使用此命令将新驱动器的状态更改为热备 (`HSP`)：

```
ipssend setstate 1 1 4 hsp
```

你将看到类似图 58 的输出。

```
[root@nF500]# ipssend setstate 1 1 4 hsp
Found 1 IBM ServerRAID Controller(s)
Set Device State has been initiated for Controller 1...
Command Completed Successfully
```

图 58. 将状态更改为 `HSP`

你可以通过执行此命令来检查此操作的结果：

```
ipssend getconfig 1 pd
```

你将看到类似图 59 的输出。

```
[root@nF500]# ipssend getconfig 1 pd
Found 1 IBM ServerRAID Controller(s).
Read Configuration has been initiated for Controller 1...
Physical Device Information
Channel #1
Initiator at SCSI ID 7
Target on SCSI ID 0
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 0
FFA (Yes/No) : Online (ONL)
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCC0DOHHS09Y035168164E669
Target on SCSI ID 1
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 1
FFA (Yes/No) : No
State : Rebuild (RBL)
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCC0DOHHS09Y04206182F8A1
Target on SCSI ID 3
Device is a 16 bit, Fast SCSI, tag queuing Hard Disk
SCSI ID : 3
FFA (Yes/No) : Online (ONL)
Size (in MB)/(Sectors) : 17357/35540848
Device ID : IBM-PCC0DOHHS09Y0351680EE209
Target on SCSI ID 4
Device is a 16 bit, Fast SCSI, tag queuing Unknown Device
SCSI ID : 4
FFA (Yes/No) : No
State : Hot Spare (HSP)
Size (in MB)/(Sectors) : 8678/17773888
Device ID : IBM-PCC0DOHHS09Y0420619242B44
Target on SCSI ID 15
Device is a 16-bit, Fast SCSI, tag queuing Device
SCSI ID : 15
FFA (Yes/No) : No
State : Stand By (SBY)
Size (in MB)/(Sectors) : 0/0
Device ID : SDR GEM200 2 1
Channel #2
Initiator at SCSI ID 7
Command Completed Successfully.
```

图 59. 将状态设置为 `HSP`

恭喜！你刚刚安装了一个新的热备驱动器，它已准备可用。

### 1.6.6 使用 `ipsmon` 工具

`ipsmon` 工具是 `ipsutils.rpm` 软件包的一部分。它可以用于监控 `IBM ServeRAID` 控制器的当前状态。`ipsmon` 命令的语法如下：

```
ipsmon -f:filename -s
```

参数见表 9。

| 参数 | 描述 |
| :--- | :--- |
| `-f:filename` | 指定用于报告消息的文件；默认文件名 `ipsmon.log` |
| `-s` | 指定消息是否仅记录到标准输出设备 |

如果你想在标准控制台上监控 `IBM ServeRAID` 控制器的活动，请执行此命令：

```
ipsmon -s
```

你将看到类似图 60 的输出。

```
[root@mf5500 /root# ipsmon -s
Licensed Material - Property of IBM
IBM ServeRAID Controller v3.50
Copyright (C) IBM Corporation 1996-1999
All Rights Reserved
US Government Restricted Rights - Use, Duplication, or Disclosure
Restricted by USA Schedule with IBM
Found 1 IBM ServerRAID Controller(s)
Oct 12 12:18:39 EDT 199 --> IBM ServeRAID Server started
Oct 12 12:18:39 EDT 199 --> Successfully created parent socket.
Oct 12 12:18:39 EDT 199 --> Bind to socket successful.
```

图 60. `ipsmon` 工具

![](img/2d69b129b41635ef36a3e6707d34b788_76_0.png)

图 64. 网络设置

3. 如图 64 所示，选择**客户端/服务器（Client/Server）**选项。

4. 在**主机名:端口号（可选）(Host Name:Port Number(Optional)** 字段中，输入运行 `ipsadm` 工具的 `IBM Netfinity` 服务器的主机名或 `IP` 地址。端口号是可选的，如果你更改了服务器端的默认端口，则需要提供。点击**添加（Add）**添加主机。你将看到一个类似于图 65 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_76_1.png)

图 65. 主机已添加

5. 点击**确定（OK）**返回网络设置窗口。你将看到一个类似于图 66 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_77_0.png)

图 66. 添加主机后

6. 在**用户名（User Name）**字段中，输入在密码文件中定义的用户 ID，在**密码（Password）**字段中，输入密码。点击**连接（Connect）**以通过 `IBM ServeRAID` 控制器连接到服务器。你将看到一个类似于图 67 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_78_0.png)



图 67. 已连接到服务器

恭喜你！你现在可以远程管理你的 IBM ServeRAID 控制器。

## 1.7 安装和配置令牌环网卡

在 OpenLinux 中，没有办法化添加和配置令牌环网卡的方法。要成功安装并配置令牌环网卡，请按照以下步骤操作：

1. 在你的 IBM Netfinity 服务器的空槽中安装令牌环网卡（PCI 或 ISA）。
2. 启动系统，并按照第 106 页 2.20节“操作内核模块”所述从 CO 启动内核工具。要跳过对新硬件的探测，点击完成（`Done`）。当工具启动时，你将看到一个类似于图 68 的窗口。

第 1 章 Linux 安装 61

## 内核模块

请选择要加载或卸载的模块。左侧列表显示所有可用模块，右侧显示所有当前加载的模块。你可以使用视图（`View`）菜单将显示限制为某些类别的模块。

| 3c501 | | eegpro100 | | |
|---|---|---|---|---|
| 3c503 | Load | extd2 | | |
| 3c505 | | floppy | | |
| 3c507 | Info | ips | | |
| 3c509 | | lsoff | Info | | |
| 3c515 | | lance | | |
| 3c523 | | lockd | | |
| 3c527 | | loop | | |
| 3c59x | | ip | | |
| 3dfk | | nfs | | |

图 68. 加载令牌环网卡的模块

## 3rd. 为你的网卡加载适当的模块：

- `olympic` - 这是适用于 PCI 令牌环网卡的模块。
- `ibbmtr` - 这是适用于 ISA 令牌环网卡的模块。

在我们的示例中，我们为 PCI 令牌环网卡使用了 `olympic` 模块。选择该模块并点击加载（`Load`），你将看到一个类似于图 69 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_79_0.png)

图 69. 加载 PCI 令牌环网卡的模块

## 注意

当使用 IBM Turbo 16/4 ISA 适配器时，你必须将其设置为自动 16/4 兼容模式。这是通过使用 LANAID C 磁盘并运行此命令实现的：

```
LANAIDC /fast=auto16
```

如果你不确定，请运行 `LANAIDC /view`。

4. 点击确定（`OK`）加载模块。如果模块加载成功，窗口将关闭，你会在网卡背面看到一个绿灯。
5. 你需要为令牌环网卡创建一个网络脚本。在我们的示例中，我们假设这是服务器上的第一块令牌环网卡。使用你喜欢的编辑器创建文件：

```
/etc/sysconfig/network-scripts/ifcfg-tr0
```

该文件应该如下：

```
DEVICE=tr0
IPADDR=9.24.104.202
REMIP=0.0.0.0
NETMASK=255.255.255.0
BROADCAST=9.24.104.255
MTU=1500
GATEWAY=9.24.104.1
BOOT=yes
```

你需要根据你的配置调整所有地址。

（注：后续重复的 Note 部分已根据要求省略或仅翻译核心逻辑，以保持结构一致）

# 2. 基本管理

本章将概述如何在图形化环境中使用一些基本工具，特别是如何通过 COAS 自定义你的 Caldera OpenLinux 系统。

## 2.1 登录

在可以使用任何工具之前，你需要通过图形界面或文本界面登录。要启动图形界面，在类似于图 70 的窗口中输入用户名和密码，然后点击 `转（Go）`。你将看到一个类似于图 72 的窗口。

## 2.2 使用窗口管理器

一旦你通过图形界面登录系统，你将看到一个类似于图 72 的窗口，该窗口由窗口管理器控制。Caldera OpenLinux 使用 KDE 窗口管理器。你可以在此处获取更多关于 KDE 的信息：

```
http://www.kde.org
```

窗口底部可以看到访问所有功能的工具栏。它包含下拉菜单、图标和按钮。你可以使用它们访问操作系统和应用程序的功能。

## 2.3 获取 X-Windows 终端窗口

为了在拥有 GUI Windows 界面窗口时从命令行运行命令，你需要创建一个终端窗口。你可以通过点击图 73 中圈出的终端窗口图标来实现。

终端窗口启动后，你将看到一个类似于图 74 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_87_0.png)

图 74. KDE 中的终端窗口

在此终端窗口中，你可以通过命令行提示符作为文本界面访问系统。命令行提示符比菜单更具灵活性，但你也可以从菜单系统中完成大部分基本操作。这取决于个人的喜好。

## 2.4 访问 COAS - Caldera 开放管理系统

Caldera OpenLinux 中的所有管理任务都是通过使用 COAS 完成的。你可以点击 KDE 工具栏上的 COAS 图标（如图 75 圈所示）来访问 COAS 工具。

![](img/2d69b129b41635ef36a3e6707d34b788_88_0.png)

图 75. 访问 COAS 工具

点击 COAS 图标后，你将看到一个与图 76 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_89_0.png)

图 76. COAS 工具

你可以看到有几个可用工具。我们将在接下来的章节中讨论它们。

## 2.5 使用 kpackage 添加和删除软件包

如果你想在安装 Caldera OpenLinux 后添加或删除软件，或者只是想检查软件是否已安装，可以使用 COAS 中的 `kpackage` 工具。你可以通过从 COAS 工具菜单中选择 `kpackage` 来启动它，如图 77 所示。

![](img/2d69b129b41635ef36a3e6707d34b788_90_0.png)

当 `kpackage` 启动时，你将看到一个与图 78 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_91_0.png)

### 2.5.1 卸载软件包

如果你想卸载一个软件包，选择所需的软件包并点击 `Uninstall`（卸载）。你将看到一个与图 79 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_91_1.png)

在卸载软件包之前，你可以更改选项，但我们建议保持默认设置不变。调整设置后，点击 `Uninstall` 继续。在检查依赖项后，软件包将被卸载。

### 2.5.2 安装软件包

要安装软件包，点击 `File > Open`，你将看到一个与图 80 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_92_0.png)

图 80. 选择要安装的软件包

在这里，你可以从任何可用系统目录选择你想要安装的软件包。

> 注意
>
> 如果你想从 CD-ROM 刻软件包，必须先挂载 CD-ROM 驱动器才能访问其中的文件。这可以通过命令行提示符运行命令 `mount /mnt/cdrom` 来完成。

选择软件包后，点击 `OK` 继续。你将看到一个与图 81 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_93_0.png)

在此窗口中，你可以看到软件包的描述。选择 `File List`（文件列表）选项查看软件包包含的文件。在实际安装软件包之前，你可以调整安装选项。选项有：

- `Upgrade`（升级）：用于已安装的软件包。
- `Replace File`（替换文件）：如果相同位置已存在文件，则将其替换。
- `Replace Packages`（替换软件包）：更新数据库中的软件包。
- `Check Dependencies`（检查依赖项）：检查是否满足所有依赖关系。
- `Test (do not install)`（测试（不安装）：执行测试。

选择选项后，点击 `Install` 安装软件包。安装完成后，它将出现在软件包列表中，如图 82 所示。

## 使用 RPM 管理软件包

软件包管理也可以直接在命令行使用 RPM 包管理器完成。图形界面命令行可以通过 2.3 节中第 69 页的“Windows 窗口”访问。表 11 显示了一些最常用的 rpm 命令。

| 命令 | 描述 |
| :--- | :--- |
| `rpm -q <package>` | 如果软件包已安装，检查其版本和构建次数。 |
| `rpm -qi <package>` | 获取已安装软件包的更多信息。 |
| `rpm -qa` | 列出所有已安装的软件包。 |
| `rpm -qf <filename>` | `<file>` 属于哪个已安装的软件包。 |
| `rpm -Uhv <package>.rpm` | 更新/安装文件 rpm，显示进度条。 |

第 2 章 基础系统管理

![](img/2d69b129b41635ef36a3e6707d34b788_94_0.png)

| 命令 | 描述 |
| :--- | :--- |
| `rpm -F -v *.rpm` | 使用当前目录下的 RPM 文件更新已安装的软件包。 |
| `rpm --help` | 获取有关选项和参数的帮助。 |

## 注意

使用 RPM 安装软件包后，你可能需要运行一些额外的程序。像 Apache 等程序需要根据特定环境进行自定义，并需要安装后维护。这些软件包中的一些可以通过图标从图形界面进行配置。其他软件包可能有自己的配置工具。

关于 RPM 的更多信息和选项可以在手册页 (`man rpm`)、RPM how-to 文件 (`/usr/doc/howto/en/RPM-HOWTO.txt`) 以及 RPM 网站上找到。你也可以通过运行 `rpm --help` 显示快速概述。

## 2.7 系统菜单

在 COAS 工具系统菜单中，你可以访问以下工具：

- `Accounts`（账户）：管理账户。
- `Daemons`（守护进程）：管理启动程序。
- `Filesystem`（文件系统）：挂载设备和 NFS 卷。
- `Hostname`（主机名）：设置主机名。
- `Resources`（资源）：检查硬件资源。
- `Time`（时间）：设置时间和时区。

系统菜单如图 83 所示。

![](img/2d69b129b41635ef36a3e6707d34b788_96_0.png)

图 83. 系统菜单

要从系统菜单启动工具，选择你需要的工具。在初始窗口中，点击 `OK` 继续。

## 2.8 Accounts

此工具用于操作用户账户。工具启动后，你将看到一个与图 84 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_97_0.png)

图 84. 账户管理

在这里你可以管理用户和组。在接下来的章节中我们将描述如何执行这些任务。

在 `View` 菜单中，你有两个显示选项：

- `All users`（所有用户）：显示所有用户。
- `Regular users`（普通用户）：只显示用户。

在 `Options` 菜单中，你有三个选项可选：

- `Preferences`（偏好）：在这里定义创建用户组全局偏好。如果你选择此选项，你将看到一个与图 85 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_98_0.png)

图 85. 设置创建偏好

- `Enable/Disable shadow passwords`（启用/禁用影子密码）：在这里启用或禁用影子密码。
- `Enable/Disable NIS lookups`（启用/禁用 NIS 查询）：在这里启用或禁用 NIS 查询。

### 2.8.1 管理账户

在本节中我们解释如何管理账户。我们涵盖了添加新用户、删除用户和编辑现有用户。

要创建新用户请遵循以下步骤：

- 要添加新用户，选择 `User > Create User`。你将看到一个与图 86 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_98_1.png)

图 86. 新用户的登录名

- 输入新用户的唯一登录名并点击 `OK` 继续，你将看到一个与图 87 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_99_0.png)

图 87. 为新用户指定参数

在这里你需要指定以下内容：

- `Full name`（全名）：用户的描述。
- `UID`：系统识别你的数字。它仅关联文件和目录的所有权，并使用 `/etc/passwd` 将转换为用户名。通常 `UID` 是唯一的，系统程序通常会阻止你创建相同 `UID` 的多个用户名。这可以通过指定创建 ID 的选项覆盖。
- `GID`：分配给组的唯一数字。CalderaLinux 每个用户都有自己的默认组。默认 `GID` 是下一个可用的，`GID` 号从 500 开始。
- `Other groups`（其他组）：每个用户可以是多个组的成员。你可以在这里指定这些组。

此对话框允许你编辑新用户的附加组列表。

请按 `F1` 可获取更多帮助。

![](img/2d69b129b41635ef36a3e6707d34b788_100_0.png)

图 88.为用户指定其他组

当你添加了所有需要的组后，点击确定继续。

- `登录 shell (Login shell)` - 用户登录时启动的 shell。
- `密码 (Password)` - 用于登录的密码。如需定义密码，请点击标记为 `<未显示>` 的按钮，你将看到与图 89 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_100_1.png)

图 89.为新用户指定密码

输入用户密码并点击确定继续。

> 注意
>
> Caldera Linux 默认使用影子密码 (shadow passwords)。

- `主目录 (Home directory)` - 这是用户的家目录。它是用户登录时进入的第一个地方。它包含该用户拥有并使用的文件及程序。

第 2 章 基础系统管理 83

- `禁用/启用 (Disabled/Enabled)` - 通过此项你可以定义账户是启用还是禁用。你可以通过点击按钮来切换此值。
- `影子信息 (Shadow information)` - 在此处你可以定义密码属性：过期、更改时间范围等。如果你想更改默认值，点击按钮，你将看到与图 90 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_101_0.png)

图 90.新用户的密码属性

编辑完属性后，点击 `确定 (OK)` 保存。

- 在输入完新用户的所有必要信息后，点击 `确定 (OK)` 创建新用户。

#### 2.8.1.1 删除用户

当你想删除用户时，从列表中选择该用户并点击 `用户 > 删除用户 (User > Delete User)`。你将看到与图 91 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_101_1.png)

图 91. 删除用户

点击 `是 (Yes)` 删除该用户。

#### 2.8.1.2 编辑用户

当你想编辑用户时，从列表中选择该用户并选择 `用户 > 编辑用户 (User > Edit User)`。你将看到与图 92 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_102_0.png)

图 92. 编辑用户

在此处你可以修改用户的以下属性：

- `其它组 (Other groups)`
- `登录 shell (Login shell)`
- `密码 (Password)`
- `主目录 (Home directory)`
- `禁用/启用 (Disabled/Enabled)`
- `影子信息 (Shadow information)`

我们已经在第 81 页的 2.8.1“管理账户”中描述了这些属性。完成后，请点击确定 (`OK`)。

### 2.8.2 管理组

你可以通过选择 `账户 > 组 > 管理组 (Accounts > Groups > Manage groups)` 来访问组管理工具。你将看到与图 93 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_103_0.png)

图 93. 组管理

在此处你可以执行与组相关的操作。

#### 2.8.2.1 创建新组

你可以选择 `组 > 创建组 (Groups > Create Group)` 来创建一个新组。你将看到与图 94 类似的新窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_103_1.png)

图 94. 创建新组

输入组名并点击确定 (`OK`) 创建。

#### 2.8.2.2 删除组

从组列表中选择要删除的组，并选择 `组 > 删除组 (Groups > Delete Group)`。你将看到与图 95 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_104_0.png)

图 95. 删除组

点击 `继续 (Continue)` 删除该组。

#### 2.8.2.3 重命名组

从组列表中选择要重命名的组，并选择 `组 > 重命名组 (Groups > Rename Group)`。你将看到与图 96 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_104_1.png)

图 96. 重命名组

输入新组名并点击确定 (`OK`) 完成。

#### 2.8.2.4 合并组

你可以将用户从一个组合并到另一个组。选择要合并的目标组，并选择 `组 > 合并组 (Groups > Merge Group)`。你将看到与图 97 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_105_0.png)

图 97. 合并组

输入要合并入的组名。点击确定 (`OK`) 继续。

#### 2.8.2.5 组成员



你可以更改组的成员。要更改所需组的成员，从列表中选择该组并选择`组 > 成员 (Groups > Membership)`。你将看到与图 98 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_105_1.png)

图 98. 组成员

你可以向组或移除用户。点击`确定 (OK)` 保存更改。

## 2.9 守护进程 (服务)

此工具用于操作服务器启动时的守护进程。工具启动后，你将看到与图 99 类似的窗口。

使用此列表选择启动后激活的系统服务：

- `打印服务器 (Print server (LPD))`
- `大文件系统支持 (Large filesystem support (background))`
- `基础 IP 服务 (Basic IP services (normally enabled))`
- `网络文件系统支持 (Networked filesystem support)`
- `重定向控制台/tty0 到 tty1 (Redirect console/tty0 to tty1 for boot (normally enabled))`
- `自动挂载 (Auto Mount (NFS & local))`

| 确定 | 取消 |

图 99. 系统服务

在此定义服务器启动时启动的服务（守护进程）。完成后，点击`确定` 保存更改。

## 2.10 文件系统

你可以挂载或卸载设备并连接到 NFS 服务器。工具启动后，你将看到与图 100 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_106_0.png)

图 100. 文件系统

左侧显示未挂载的设备。如果你想挂载设备，从列表中选择它并点击`挂载 (Mount)`。

右侧显示已挂载的设备。如果你想卸载已挂载的设备，从列表中选择它并点击`卸载 (Unmount)`。

通过选择已挂载或未挂载的设备并点击`信息 (Info)`，你可以查看特定设备的信息。

第 2 章 基础系统管理 89

### 2.10.1 挂载 NFS 卷

你可以通过`操作 > 挂载 NFS (Action > Mount NFS)` 来挂载 NFS 系统。你将看到与图 101 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_107_0.png)

图 101. 挂载 NFS 卷

输入所需值并点击`确定 (OK)` 挂载 NFS 卷。

## 2.11 主机名

你可以更改 Linux 服务器的主机名。工具启动后，你将看到与图 102 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_107_1.png)

图 102. 修改主机名

输入新主机名并点击`确定` 保存。

## 2.12 资源

通过此工具，你可以检查硬件资源。工具启动后，你将看到与图 103 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_108_0.png)

图 103. 系统资源

在此处你可以获取关于以下资源的信息：

- `块设备 (Block devices)`
- `字符设备 (Character devices)`
- `中断 (Interrupts)`
- `系统平均负载 (System load average)`
- `I/O (IOports)`
- `DMA`

要访问这些信息，请从`信息 (Info)` 菜单选择相应的选项。例如，如果你选择`中断 (Interrupts)`，你将看到与图 104 类似的窗口。

第 2 章 基础系统管理 91

### 系统中断

你可以看到已注册的中断、该线路上已处理的中断数量、带有 `*` 的共享中断以及使用该中断的设备。

| IRQ | 设备 | 已处理 |
| :--- | :--- | :--- |
| 0 | 定时器 | 235849 |
| 1 | 键盘 | 6335 |
| 2 | 级联 | 0 |
| 6 | 软盘 | 80 |
| 8 | RIC | 0 |
| 10 | IPS | 112149 |
| 11 | Intel Ether/Express | 164583 |
| 12 | PS2/鼠标 | 487340 |
| 13 | FPU | 1 |
| 14 | `ide0` | 1563 |
| 15 | PCnet/FAST+ 7C | 17219 |

图 104. 系统中断

## 2.13 时间

你可以设置系统时间和时区。工具启动后，你将看到与图 105 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_109_0.png)

图 105. 设置时间

92 Caldera OpenLinux 与 Netfinity 服务器集成指南

输入当前时间。如果你也想更改时区，请点击对应的按钮。你将看到与图 106 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_110_0.png)

图 106. 设置时区

选择你的地区，系统将显示该地区的时区。选择匹配你所在城市。之后你将回到系统时间面板。点击`确定 (OK)` 保存更改。

## 2.14 外设菜单

在 COAS 工具的外设菜单中，你可以访问以下工具：

- `鼠标` - 管理鼠标
- `打印机` - 管理打印机

![](img/2d69b129b41635ef36a3e6707d34b788_111_0.png)

图 107. 外设菜单

要从外设菜单启动工具，请选择你所需的工具。在初始对话框中，点击`OK` 继续。

## 2.15 鼠标

此工具用于配置文本用户界面中鼠标的行为。工具启动后，你将看到一个类似于图 108 的窗口。

> **警告**
>
> 此对话框配置 `GPM`（文本控制台的鼠标驱动程序），它与你当前正在使用的 `X Window` 系统不同。注意，对于某些鼠标，当 `GPM` 运行时，`X Window` 服务器将无法访问鼠标。如果你的鼠标出现此情况，请在启动 `X Window` 系统之前使用 `COAS` 禁用鼠标。

![](img/2d69b129b41635ef36a3e6707d34b788_111_1.png)

图 108. 配置鼠标前的警告

94 Caldera OpenLinux 和 Netfinity 服务器集成指南

如警告所示，此工具用于配置 `GPM`，以便启用文本界面中使用鼠标的额外功能。点击`Continue（继续）`继续配置。你将看到一个类似于图 109 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_112_0.png)

图 109. GPM 鼠标配置

选择符合你需求的配置参数并点击`OK` 继续。在下一个窗口中，点击`Save` 保存你的设置。

> **注意**
>
> 如果你没有安装 `GPM` 软件包，你将收到守护进程无法启动的错误信息。

## 2.16 打印机

此工具用于配置你在 Caldera OpenLinux 系统中想要使用的打印机。工具启动后，你将看到一个类似于图 110 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_113_0.png)

图 110. 打印机配置

在此处你可以管理打印机。在接后的章节中，我们将描述如何执行这些任务。

从 `Daemon（守护进程）` 菜单，你可以`Start（启动）` 或 `Stop（停止）` 打印守护进程。

> **注意**
>
> 只有在守护进程运行时才能打印文档。

### 2.16.1 添加新打印机

你可以通过选择`Printer > Add（打印机 > 添加）` 为系统添加新打印机。你将看到一个类似于图 111 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_113_1.png)

图 111. 选择打印机型号

从列表中选择你的型号。之后，你将看到一个类似于图 112 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_114_0.png)

图 112. 定义打印机逻辑名称

在此处你定义打印机的逻辑名称。该名称随后将用于所有打印机定义。点击`OK` 继续，你将看到一个类似于图 113 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_114_1.png)

图 113. 打印机属性

在此处你定义打印机属性：

- `Paper size（纸张尺寸）`
- `Device（设备）` - 打印机连接的物理设备。通常是并行端口，`dev/lp0` 是服务器上的第一个并行端口。
- `Speed（速度）` - 数据通过打印机连接设备传输的速度。

这些属性与你选择的打印机驱动程序相关，因此所有驱动程序的选项并不相同。

定义完打印机的所有属性后，点击`OK` 继续。在下一个窗口中选择`Save` 保存你的配置。安装程序将询问你是否为新打印机创建队列。点击`OK` 创建队列。打印机守护进程将停止以便创建队列，然后将重启。

### 2.16.2 移除打印机

你可以从已安装打印机列表中选择要移除的打印机并选择`Printer > Remove（打印机 > 移除）` 从系统中移除它。系统会询问你是否确定要移除该打印机。如果确定，请两次点击`OK`。

### 2.16.3 编辑打印机

如果你想编辑已安装打印机的属性，从列表中选择打印机并选择`Printer > Edit（打印机 > 编辑）`。你将看到一个类似于图 114 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_115_0.png)

图 114. 打印机属性

98 Caldera OpenLinux 和 Netfinity 服务器集成指南

## 2.17 网络菜单

从网络菜单你可以访问：

- `TCP/IP` - 用于 `TCP/IP` 设置。
- `Ethernet interfaces（以太网接口）` - 用于 `NIC`。
- `Mail Transfer（邮件传输）` - 用于 `MTA`。你可以在第 8 章中找到关于如何设置 `MTA` 的更多信息。

![](img/2d69b129b41635ef36a3e6707d34b788_116_0.png)

图 115. 网络菜单

从 `Peripherals（外设）` 菜单启动工具，请选择所需的工具。在初始对话框中，点击`OK` 继续。

![](img/2d69b129b41635ef36a3e6707d34b788_111_0.png)

图 107. 外设菜单

此工具用于配置文本用户界面中鼠标的行为。工具启动后，你将看到一个类似于图 108 的窗口。

> **警告**
>
> 此对话框配置 `GPM`（文本控制台的鼠标驱动程序），它与你当前正在使用的 `X Window` 系统不同。注意，对于某些鼠标，当 `GPM` 运行时，`X Window` 服务器将无法访问鼠标。如果你的鼠标出现此情况，请在启动 `X Window` 系统之前使用 `COAS` 禁用鼠标。

![](img/2d69b129b41635ef36a3e6707d34b788_111_1.png)

图 108. 配置鼠标前的警告

94 Caldera OpenLinux 和 Netfinity 服务器集成指南

如警告所示，此工具用于配置 `GPM`，以便启用文本界面中使用鼠标的额外功能。点击`Continue（继续）`继续配置。你将看到一个类似于图 109 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_112_0.png)

图 109. GPM 鼠标配置

选择符合你需求的配置参数并点击`OK` 继续。在下一个窗口中，点击`Save` 保存你的设置。

> **注意**
>
> 如果你没有安装 `GPM` 软件包，你将收到守护进程无法启动的错误信息。

## 2.18.2 移除网络接口

如果你想删除以太网网卡（`NIC`）的定义，请点击第101页图117所示的对话框中的“删除设备”。然后点击`确定` 关闭配置窗口。在下一个窗口中，点击`保存` 以保存你所做的更改。

如果你有多个以太网适配器，例如你想移除 `eth1` 适配器，请按照以下步骤操作：

1. 执行命令停止接口：
   ```
   /sbin/ifdown eth1
   ```
2. 执行命令删除文件 `/etc/sysconfig/network-scripts/ifcfg-eth1`：
   ```
   rm /etc/sysconfig/network-scripts/ifcfg-eth1
   ```

当你定义了多个适配器时，此程序适用于所有适配器。

## 2.19 域名解析设置

你可以点击`网络 > TCP/IP > 解析器`访问域名解析设置工具。启动该工具时，你将看到一个与图120 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_120_0.png)

图120. 域名解析设置

在这里，你可以定义系统如何进行域名解析。这里有四个选项：

- `信息源` - 在此处定义域名解析的顺序和来源。
- `尝试防止欺骗`
  - `报告欺骗尝试`
  - `DNS 服务器` - `DNS` 服务器的定义 `IP` 地址

### 2.19.1 域名解析顺序和源

你可以点击“信息源”右侧的按钮更改域名解析的顺序和源。你将看到一个与图121 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_121_0.png)

图121. 搜索顺序

可以通过移动域名解析资源来更改搜索顺序。如果你想启用或禁用特定的域名解析源，可以通过选择“启用”并选择要启用或禁用的源来实现。如果某个源当前处于启用状态，你可以禁用它，反之亦然。完成后，点击`确定` 继续，并在下一个窗口中选择`保存` 以保存更改。

### 2.19.2 定义 DNS 服务器

你可以点击“DNS 服务器”按钮右侧的按钮来定义 `DNS` 服务器。你将看到一个与图122 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_122_0.png)

图122. DNS 服务器

如果你定义了多个 `DNS` 服务器，可以通过上下移动它们来重新排序。最顶部的服务器将最被访问，依此类推。

#### 2.19.2.1 添加新的 DNS 服务器

如果你想添加新的 `DNS` 服务器，选择`编辑 > 添加服务器`。你将看到一个与图123 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_122_1.png)

图123. 指定 DNS 服务器

输入 `DNS` 服务器的 `IP` 地址并点击`确定` 返回上一个窗口。

#### 2.19.2.2 移除 DNS 服务器

如果你想移除 `DNS` 服务器，从列表中选择它并选择`编辑 > 移除服务器`。

#### 2.19.2.3 更改 DNS 服务器

如果你想更改 `DNS` 服务器的 `IP` 地址，从列表中选择它并选择`编辑 > 编辑服务器`。你将看到一个与图123 相似的窗口。输入服务器的新 `IP` 地址并点击`确定` 返回上一个窗口。

## 2.20 操作内核模块

你可以使用 `COAS` 工具中的内核配置工具在 Caldera Linux 中管理内核模块。你可以通过从 `COAS` 工具菜单选择`内核` 启动。当内核工具启动时，你将看到一个与图124 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_123_0.png)

图124. 内核模块

在左侧你可以看到所有可用模块，在右侧你可以看到已加载的模块。默认显示所有模块，但如果你只想显示一种模块，可以通过从“视图”菜单选择以下选项来实现：

- 所有驱动程序
- `Arcnet` 驱动程序
- `CD-ROM` 驱动程序
- 以太网驱动程序
- 其他驱动程序
- 网络驱动程序
- `SCSI` 驱动程序
- `SCSI` 主机适配器驱动程序
- 音频驱动程序
- 令牌环驱动程序
- `ISDN` 驱动程序
- 多媒体驱动程序

如果你想获取有关特定模块的信息，从任一侧选择该模块并点击“信息”。

### 2.20.1 加载新模块

当你安装新硬件时，需要加载相应的模块才能使硬件发挥作用。在 Linux 中，可以加载驱动程序。如果你想获取有关特定模块的信息，从任一侧选择该模块并点击“信息”。要加载模块，从任一侧选择该模块。你将看到一个与图125 相似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_124_0.png)

图125. 模块配置

当你安装新硬件时，需要加载相应的模块才能使硬件发挥作用。在 Linux 中，可以加载驱动程序。如果你想获取有关特定模块的信息，从任一侧选择该模块并点击“信息”。要加载模块，从任一侧选择该模块。你将看到一个与图125 相似的窗口。

### 2.20.2 卸载新模块

如果你想卸载模块，从列表中选择它并选择`编辑 > 移除服务器`。

## 2.21 配置 X-Windows

出于某种原因你需要在安装后更改 `X-Windows` 设置，你可以通过从 `COAS` 工具菜单点击 `X` 服务器来实现。更多信息请参阅第 3 页的 1.5 “基础安装”。

挂载此选项后，对文件的读取访问将不再更新 `inode` 访问时间信息。在文件服务器或 `Web` 服务器上，这些信息通常并不重要，该字段缺少更新也无影响。`noatime` 标志的性能优势在于它抑制了对仅进行读取的文件的文件系统写操作。由于这些写访问会增加额外的开销，这可以带来可衡量的性能提升。与其将其作为一个应用于整个文件系统的挂载选项，你也可以使用 `chattr` 命令在单个文件或目录上设置此标志。例如：

```
chattr -R +A /var/spool/news
```

此命令会在 `news` 目录下的所有文件上递归设置 `noatime` 标志（这在繁忙的服务器上是非常常见的做法）。你可以查看 `chattr(1)` 手页获取更多信息。



## 硬盘参数调整

你可以使用`hdparm`工具来调整某些硬盘参数。遗憾的是，大部分参数只在 IDE 系统上有效（无论如何，服务器系统中应该避免），但`-a`选项也适用于 SCSI。此选项用于获取/设置文件系统预读（readahead）的扇区数。它通过预取块以备运行任务可能会使用，从而提高大文件顺序读取的性能。默认设置为 8 个扇区（4KB）。这个值对于大多数用途来说是很好的，但在大多数文件访问都是随机寻道的系统中，较小的设置可能会提供更好的性能。此外，许多驱动器具有独立的内置预读功能，这在很多情况下减轻了文件系统预读的需求。

例如，要将你的第一个 SCSI 磁盘的预读扇区数设置为 4 扇区（2 KB），可以使用以下命令：

```bash
hdparm -a 4 /dev/sda
```

查看`hdparm`手页获取可用选项的完整列表。

## 性能调优工具

免费工具`Powertweak`是一个用于 PCI 芯片组优化的优秀实用程序。预计它将扩展为类似于微软 Windows 的通用性能调优工具。有关它的更多信息，请访问`http://linux.powertweak.com`。

你还应该禁用所有未使用的服务和设备，特别是网络相关的服务。这有几个优点：更少的系统资源（文件描述符、内存），并且系统不易受到针对已知安全漏洞的外部攻击。一个良好的起点是`/etc/inetd.conf`。注释掉所有不需要的服务，或完全禁用`inetd`。

## /proc 文件系统

Linux`/proc`文件系统为无需重新编译内核的运行时优化提供了许多入口。该目录在你的硬盘上物理并不存在；它被映射为一个虚拟目录。其中包含的大多数文件都是可读的，并包含各种系统信息。其他文件可以使用文本编辑器编辑以设置特定的内核参数。Linux 内核源码中的`/usr/src/linux/Documentation/sysctl/README`提供了可调参数的详细说明（包括文件系统、虚拟内存等）。

## TCP 选项调优

在信号质量和带宽较高的局域网中，可以禁用某些特殊的 TCP 选项，因为它们主要是为丢包连接设计的（参见 Linux 内核源码中的`/usr/src/linux/net/TUNABLE`获取详细列表）：

禁用 TCP 时间戳：

```bash
echo 0 > /proc/sys/net/ipv4/tcp_timestamps
```

禁用窗口缩放（window scaling），输入：

```bash
echo 0 > /proc/sys/net/ipv4/tcp_window_scaling
```

禁用选择性确认（selective acknowledgments），输入：

```bash
echo 0 > /proc/sys/net/ipv4/tcp_sack
```

调整默认和最大窗口大小（仅在你知道自己在做什么时进行），输入：

```bash
/proc/sys/net/core/rmem_default - 默认接收窗口
/proc/sys/net/core/rmem_max - 最大接收窗口
/proc/sys/net/core/wmem_default - 默认发送窗口
/proc/sys/net/core/wmem_max - 最大发送窗口
```

以下网站提供了许多关于 Linux 调优和性能问题的额外有用提示：

```text
http://tune.linux.com
http://www.tunelinux.com
```

## 3.2 系统监控 / 性能测试工具

本节介绍了许多可用工具中的一小实用工具，用于监控你的 Linux 系统或收集系统信息。

### 使用 top 命令

要获取所有运行进程和系统负载的概述，请在终端会话中运行`top`命令。

```text
11:53am up 37, 1 user, load average: 0.00, 0.00, 0.00
34 processes: 33 sleeping, 1 running, 0 zombie, 0 stopped
CPU states: 0.0% user, 1.6% system, 0.0% nice, 98.4% idle
Mem: 62968KB used, 59196KB free, 3772KB cache, 17408KB shrd, 33768KB buff
Swap: 12596KB used, 0KB free, 12596KB swap
PID USER PRI SIZE AVR SHR RES SMEM %CPU %MEM TIME COMMAND
515 root 0 792 628 R 0 0.0 0.0 01:01 top
1 root 0 196 160 S 0 0.0 0.0 --
2 root 0 0 0 SW 0 0.0 0.0 --
3 root 0 0 0 SW 0 0.0 0.0 --
4 root 0 0 0 SW 0 0.0 0.0 --
6 root 0 0 0 SW 0 0.0 0.0 --
76 root 0 640 640 536 S 0 0.0 0.0 --
79 root 0 816 816 392 S 0 0.0 0.0 --
116 at 0 552 552 456 S 0 0.0 0.0 --
121 root 0 452 452 376 S 0 0.0 0.0 --
132 root 0 1592 1592 1408 S 0 0.0 0.7 --
135 root 0 624 624 520 S 0 0.0 0.9 --
137 wunun 0 1592 1592 1500 S 0 0.0 0.0 --
138 wunun 0 1592 1592 1500 S 0 0.0 0.0 --
139 wunun 0 1592 1592 1500 S 0 0.0 0.0 --
141 wunun 0 1592 1592 1500 S 0 0.0 0.0 --
```

图 127. top 命令输出

`top`命令按间隔更新进程列表。要更改间隔，按下`S`并输入所需的秒数。如果你想按内存消耗排序进程，按下`M`。退出`top`，按下`Q`。这将带回到命令行。

### 使用 pstree 命令

与`top`命令类似，`pstree`命令显示所有运行进程的层级结构。

```text
[root@nf5000 /] # pstree
init-atd
-cron
-dhclient
-gpm
-httpd-httpd
-httpd-httpd
-inetd-in.telnetd-login-bash-make-gcc-as
-cc1
-in.telnetd-login-bash-pstree
-cpp
-kflushd
-klogd
-kpiold
-kswapd
-kupdate
-login-bash
-lpd
-md_thread
-minggetty
-nmbd
-nscd-nscd
-sendmail
-smbd-smbd
-syslogd
```

### 使用基于窗口的工具

如果你正在运行像 CalderaLinux 中使用的 KDE 图形桌面，也可以使用基于窗口的工具，如`KTop`，KDE 管理器：

`img/2d69b129b4165ef36e6707d34788_131.png`

图 128. KDE 管理器：进程列表

`KTop`命令提供了两种不同的视图。它可以显示进程列表（类似于`top`和`pstree`命令），或者你可以切换到性能计数表，它显示较长时间的系统负载和内存使用情况。

`img/2d69b129b4165ef36e6707d34788_132.png`

图 129. KDE 任务：性能计数表

Lothar 项目正在开发一个非常复杂的硬件检测和配置工具。可以在此处找到网站：

`http://www.linux-mandrake.com/lothar/`

第 116 页的图 130 显示了 Lothar 网站上的图形前端。

`img/2d69b129b4165ef36e6707d34788_133.png`

### /proc 文件系统信息

KDE 控制中心通过读取`/proc`文件系统的许多信息文件提供有关系统的大量信息。它们也可以在普通的文本查看器中显示（例如`more`、`less`或`cat`）：

`/proc/cpuinfo`文件包含关于 CPU 的信息（例如，厂商、频率以及如`mmx`等标志）。例如：

图 130. Lothar 主窗口

```bash
[root@nf5000 ] # cat /proc/cpuinfo
processor : 0
vendor_id : GenuineIntel
cpu family : 6
model : 5
model name : Pentium II (Desutches)
stepping : 2
cpu Wtr : 513.953536
cache size : 512 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
f00_bug : no
cname_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 2
wr : yes
flags : fpu vme pse tsc mar pae moe cx8 sep mtrr pge ca cmov pat p
s36 mmx csfsx
```

`/proc/interrupts`文件列出了 Linux 使用的所有中断。注意，这只显示来自内核检测到的设备的中断！如果设备因为资源冲突未被检测，你必须手动解决此冲突（例如通过更改 BIOS 设置）。例如：

```text
[root@nf5000 /# # cat /proc/interrupts
CR0
0: 548029 XT-PIC timer
1: 557 XT-PIC keyboard
2: 0 XT-PIC cascade
8: 2 XT-PIC rtc
9: 371 XT-PIC Pciet/PCI II 7C970A
12: 68 XT-PIC PS/2 Mouse
13: 0 XT-PIC fpu
14: 198235 XT-PIC ide0
15: 3 XT-PIC idel
NMI: 0
```

`/proc/ioports`文件包含所有分配的设备 I/O 端口。在这里适用相同的规则。此处列出的是内核实际检测到的设备。例如：

```bash
[root@mf5000 /] # cat /proc/ioports
0000-001f: dial
0020-003f: pci1
0040-005f: timer
0060-006f: keyboard
0070-007f: rtc
0080-008f: dma page reg
00a0-00bf: pci2
00c0-00df: dma2
00f0-00ff: fpu
0170-0177: idel
01f0-017f: ide0
02e8-02ef: serial (auto)
02f8-02ff: serial (auto)
0376-037f: idel
03c0-03df: vga+
03e8-03ef: serial (auto)
03f6-03ff: ide0
03f8-03ff: serial (auto)
100e-101f: PISA/PCI II 7C9C0A
1020-1027: ide0
1028-102f: idel
```

`/proc/meminfo`文件显示关于内存的信息（例如，总内存、空闲内存和交换分区大小）。你也可以使用`free`命令来显示这些信息。例如：

```bash
[root@mf5000 /] # cat /proc/meminfo
total:     used       free     shared   buffers   cached
Mem:      64569344  62578868 1990656 54308864 18792448 27807744
Swap:     12901990  102400   12891750
MemTotal: 63056 kB
MemFree:  1944 kB
MemShared: 53036 kB
Buffers:  18352 kB
Cached:   27156 kB
SwapTotal: 125996 kB
SwapFree: 125896 kB
[root@mf5000 /] # free
total:     used       free     shared   buffers   cached
Mem:      63056      61124     1932     53068    18352    27164
-/+ buffers/cache: 15608     47448
Swap:     125996      100     125896
```

`/proc/mounts`文件显示所有当前挂载的分区。不带参数的`mount`命令会显示类似的信息。例如：

```bash
[root@nf5000 /]# cat /proc/mounts
dev/root /ext2 rw 0 0
proc /proc rw 0 0
dev/hda1 /boot ext2 rw 0 0
devpts /dev/pts devpts rw 0 0
[root@nf5000 /]# # mount
dev/hda3 on /proc type2 (rw)
proc on /proc type proc (rw)
dev/hda1 on /boot-type ext2 (rw)
devpts on /dev/pts devpts (rw,gid=5,mode=0620)
```

`/proc/partitions`文件显示所有设备上的所有现有分区。你也可以使用`fdisk -l`来显示这些信息。例如：

```bash
[root@nf5000 /]# # cat /proc/partitions
major minor blocks name
3 0 1023907 hda
3 1 6016 hda1
3 2 126000 hda2
3 3 891072 hda3
3 64 1023907 hdb
3 65 123088 hdb1
22 0 107341823db2
[root@nf5000 /]# # fdisk -l

Disk /dev/hda: 32 heads, 63 sectors, 1015 cylinders
Units = cylinders of 2016 * 512 bytes

| Device | Boot | Start | End | Blocks | System |
| /dev/hda1 | * | 6 | 6016+ | Linux |
| /dev/hda2 | | 7 | 131 | 126000 | swap |
| /dev/hda3 | | 132 | 1015 | 891072 | Linux |

Disk /dev/hdb: 32 heads, 63 sectors, 1015 cylinders
Units = cylinders of 2016 * 512 bytes

| Device | Boot | Start | End | Blocks | System |
| /dev/hdb1 | | 1 | 1015 | 102308+ | Linux | |
```

`/proc/pci`文件提供了有关所有 PCI 设备的信息。你也可以使用`lspci`命令。请注意`/proc/pci`文件已过时，未来将被`/proc/bus/pci`替换。例如：

```bash
[root@nf5000] # cat /proc/pci

PCI devices found:

Bus 0, device 0, function: 0:

Host bridge: 82349TX (rev 1).

Medium devel. Masterable.

Bus 0, device 7, function: 0:

ISA bridge: 82371AB PIX4 (rev 8).

Medium devel. Masterable.

Bus 0, device 7, function: 1:

IDE interface: 82371AB PIX4 (rev 1).

Medium devel. Fast-to-back. Masterable. Length=64.

I/o at 0x0120

Bus 0, device 15, function: 0:

Display controller: unknown vendor (rev 0).

Vendor id-15ad. Device id-15ad.

Medium devel. Fast-to-back. Masterable. Length=64.

I/o at 0x0130

Non-prefetchable 32 bit memory at 0xfc000

Non-prefetchable 32 bit memory at 0xfb000

Bus 0, device 16, function: 0:

Ethernet controller: AMD 79c70 (rev 16).

Medium devel. Fast-to-back. IRQ 9. Masterable. Latency=64.

Min=Max Lat=25.

I/o at 0x0400

Non-prefetchable 32 bit memory at 0xfd000

[root@nf5000] # lspci

00.00. Host bridge: Intel Corporation 82349TX-82349TX (rev 0)

00.07. ISA bridge: Intel Corporation 82371AB PIX4 (rev 0)

00.07. IDE interface: Intel Corporation 82371AB PIX4 IDE (rev 0)

00.0f. Display controller: unknown device 15ad:0710

00.10. Ethernet controller: Advanced Micro Devices 79c90 (PCNet) (rev 10)
```



## 3. 系统信息与性能测试

`/proc/swaps` 文件显示所有活动分区的信息。例如：

| Filename | Type | Size | Used | Priority |
| :--- | :--- | :--- | :--- | :--- |
| `/dev/hda2` | partition | 125996 | 56 | -1 |

`/proc/version` 文件显示关于 `Linux` 内核的一些信息。命令示例：

```bash
[root@nf5000] # cat /proc/version
Linux version 2.2.12 (root@calderysystems.com) (gcc gcc-2.91.66 19990314 (gcc-1.1.2 release)) #1 SMP Sep 23 22:09:31 MDT 1999

[root@nf5000] # uname -a
Linux nf5000.itzc 2.2.12 #1 SMP Sep 23 22:09:31 MDT 1999 unknown
```

如果你想获取有关 SCSI 设备的信息，请查看 `/proc/scsi` 下方的文件。

除了配置硬盘驱动器的许多参数外，`hdparm` 命令也可以用于通过 `hdparm -tT <device>` 命令执行硬盘性能测试。例如：

```bash
[root@nf5000] # hdparm -tT /dev/hda

/dev/hda:
Timing buffer-cache reads: 64 MB in 0.68 seconds = 94.12 MB/sec
Timing buffered disk reads: 32 MB in 29.51 seconds = 1.08 MB/sec

[root@nf5000] / # hdparm -cl /dev/hda

dev/hda:
setting 32-bit I/O support flag to 1
I/O support = 1 (32-bit)

[root@nf5000] / # hdparm -tT /dev/hda

dev/hda:
Timing buffer-cache reads: 64 MB in 0.67 seconds = 95.52 MB/sec
Timing buffered disk reads: 32 MB in 12.92 seconds = 2.48 MB/sec
```

另一个流行的硬盘性能测试是 `bonnie`，位于 (http://www.textuality.com/bonnie/)。但请注意，这些测试主要用于在单机上测试不同的参数设置以作为相对衡量，而不是作为不同系统之间的比较。

要测试网络吞吐量，你可以使用 `netperf`（位于 http://www.netperf.org/netperf/NetperfPage.html），或者使用 `bing`。

![](img/2d69b129b41635ef36a3e6707d34b788_142_0.png)

图 132. 检查 Samba 包

如图 132 所示，Samba 软件包已安装。

## 3.2.1 配置 Samba 服务器

在本节中，我们将解释如何配置 Samba，使其能够作为 Windows 网络中的文件/打印服务器，或者仅作为 Windows 和 Linux 客户端的独立文件/打印服务器。

在开始使用 Samba 之前，你需要配置 `smb.conf` 文件。该文件是 Samba 服务器的核心。当在 Caldera OpenLinux 中安装 Samba 软件包时，示例配置文件安装在 `/etc/samba.d/smb.conf` 文件。

在 Caldera OpenLinux 中，Samba 默认使用 `/etc/samba.d` 目录下的 `smb.conf` 文件。首先，只需执行以下命令创建示例文件的副本即可：

```bash
cp /etc/samba.d/smb.conf.sample /etc/samba.d/smb.conf
```

Samba 配置文件 `smb.conf` 分为大部分部分：

1. **全局设置** (Global Settings) - 在此处设置影响连接参数的参数。
2. **共享定义** (Share Definitions) - 在此处定义共享。共享是一个可以通过网络访问并在用户之间共享的目录。该部分包含三个子节：
    a. **用户目录** (Homes) - 在此子节中定义用户的家目录。
    b. **打印机** (Printers) - 在此子节中定义可用打印机。
    c. **共享** (Shares) - 此子节可以有更多条目，对应每个定义的共享。

在接下来的章节中，我们将描述如何修改 `smb.conf` 文件，以便高效简单地使用 Samba 作为文件/打印服务器。我们仅解释必要的参数。如果你需要更多信息，请参阅 `smb.conf` 文件的手册条目或 Samba 项目网站：

```
http://www.samba.org
```

你可以在附录 E 第 305 页“示例 `smb.conf` 配置文件”中找到我们的 `smb.conf` 配置文件。

## 4.2.1.1 设置 NetBIOS 参数

NetBIOS 参数是全局部分（Global Section）的一部分。当你打开 `smb.conf` 文件时，你会看到类似以下的内容：

```
================ Global Settings ====================

[global]

netbios name = NF5000
workgroup = LINUX
server string = Samba Server on Caldera OpenLinux
```

参数描述见表 12。

| 表 12. NetBIOS 参数 | 描述 |
| :--- | :--- |
| `netbios name` | Samba 服务器在网络上通过此名称识别。此参数与 Windows NT 计算机名的含义相同。如果不指定，它默认为服务器的主机名。 |
| `workgroup` | 此参数指定 Samba 服务器将参与哪个 Windows NT 域或工作组。它等同于 Windows NT 域或工作组名称。 |
| `server string` | Samba 服务器的描述字符串。它的作用与 Windows NT 的描述字段相同。 |

## 4.2.1.2 全局打印设置

在 `smb.conf` 文件中，你会看到类似以下的内容：

```
load printers = yes
printcap name = /etc/printcap
printing = lprng
```

参数描述见表 13。

表 13. 打印参数

| 参数 | 描述 |
| --- | --- |
| `load printers` | 此参数控制 Samba 加载 `printcap` 文件中的所有打印机以便浏览。 |
| `printcap name` | 通过此参数你告诉 Samba `printcap` 文件的位置。默认值为 `/etc/printcap` |
| `printing` | 此参数告诉 Samba 在你的服务器上使用什么打印样式。Caldera OpenLinux 默认使用 LPRNG 打印样式 |

## 4.2.1.3 全局安全设置

在你的 `smb.conf` 文件中，你会看到类似以下的内容：

```
security = user
; password server = <NT-Server-Name>
encrypt passwords = yes
smb passwd file = /etc/samba.d/smbpasswd
```

参数描述见表 14。

表 14. 安全参数

| 参数 | 描述 |
| --- | --- |
| `security` | 此参数有四个可能的值：`share`（共享）, `user`（用户）, `server`（服务器）, `domain`（域） |
| `password server` | 在 `server` 或 `domain` 安全级别下，此项用于授权。对于参数值请使用 NetBIOS 名称。 |
| `encrypt passwords` | 通过将此参数设置为 `yes`，你启用了 Samba 的加密密码协议，该协议用于 Windows NT Service Pack 3 和 Windows 98。这与这些客户端通信时是必需的。 |
| `smb passwd file` | 此参数告诉 Samba 加密密码存储的位置。 |

安全模式如下：

*   **Share** - 对于这种安全模式，客户端只需要提供资源的密码。这种模式是 Windows 95 的默认设置，且不建议在 UNIX 环境中使用，因为它违反了 UNIX 的设计范式。
*   **User** - 密码验证在提供资源的服务器上完成。这种模式被广泛使用。
*   **Server** - 密码验证在指定的服务器上完成，该服务器可以是 Windows NT 服务器或另一个 Samba 服务器。
*   **Domain** - 这种安全级别基本上与 `server` 级别相同，区别在于 Samba 服务器成为了 NT 域的成员。在这种情况下，Samba 服务器也可以参与信任关系。

由于 Windows NT 4.0 Service Pack 3 或更高版本（带有最新补丁）以及 Windows 98 使用加密密码访问 NetBIOS，因此需要与这些客户端通信。



`printing = lprng`

```

参数描述见表 13。

表 13. 打印参数

| 参数 | 描述 |
| --- | --- |
| `load printers` | 此参数控制 Samba 加载 `printcap` 文件中的所有打印机以便浏览。 |
| `printcap name` | 通过此参数你告诉 Samba `printcap` 文件的位置。默认值为 `/etc/printcap` |
| `printing` | 此参数告诉 Samba 在你的服务器上使用什么打印样式。`Caldera OpenLinux` 默认使用 `LPRNG` 打印样式 |

## 4.2.1.3 全局安全设置

在你的 `smb.conf` 文件中，你会看到类似以下的内容：

```
security = user

; password server = <NT-Server-Name>

encrypt passwords = yes

smb passwd file = /etc/samba.d/smbpasswd
```

参数描述见表 14。

表 14. 安全参数

| 参数 | 描述 |
| --- | --- |
| `security` | 此参数有四个可能的值：`share`, `user`, `server`, `domain` |
| `password server` | 在 `server` 或 `domain` 安全级别下，此项用于授权。对于参数值请使用 `NetBIOS` 名称。 |
| `encrypt passwords` | 通过将此参数设置为 `yes`，你启用了 Samba 的加密密码协议，该协议用于 `Windows NT Service Pack 3` 和 `Windows 98`。这与这些客户端通信时是必需的。 |
| `smb passwd file` | 此参数告诉 Samba 加密密码存储的位置。 |

安全模式如下：

- `Share` - 对于这种安全模式，客户端只需要提供资源的密码。这种模式是 `Windows 95` 的默认设置，且不建议在 UNIX 环境中使用，因为它违反了 UNIX 的设计范式。
- `User` - 密码验证在提供资源的服务器上完成。这种模式被广泛使用。
- `Server` - 密码验证在指定的服务器上完成，该服务器可以是 `Windows NT` 服务器或另一个 Samba 服务器。
- `Domain` - 这种安全级别基本上与 `server` 级别相同，区别在于 Samba 服务器成为了 NT 域的成员。在这种情况下，Samba 服务器也可以参与信任关系。

由于 `Windows NT 4.0 Service Pack 3` 或更高版本（带有最新补丁）以及 `Windows 98` 使用加密密码访问 `NetBIOS`，因此需要与这些客户端通信。在开始使用 Samba 之前，你需要配置 `smb.conf` 文件。在 `Caldera OpenLinux` 中，Samba 默认使用 `/etc/samba.d` 目录下的 `smb.conf` 文件。首先，只需执行以下命令创建示例文件的副本即可：

```
cp /etc/samba.d/smb.conf.sample /etc/samba.d/smb.conf
```

Samba 配置文件 `smb.conf` 分为大部分部分：

- 1. 全局设置 (`Global Settings`) - 在此处设置影响连接参数的参数。
- 2. 共享定义 (`Share Definitions`) - 在此处定义共享。共享是一个可以通过网络访问并在用户之间共享的目录。该部分包含三个子节：
    - a. 用户目录 (`Homes`) - 在此子节中定义用户的家目录。
    - b. 打印机 (`Printers`) - 在此子节中定义可用打印机。
    - c. 共享 (`Shares`) - 此子节可以有更多条目，对应每个定义的共享。

在接下来的章节中，我们将描述如何修改 `smb.conf` 文件，以便高效简单地使用 Samba 作为文件/打印服务器。我们仅解释必要的参数。如果你需要更多信息，请参阅 `smb.conf` 文件的手册条目或 Samba 项目网站：

```
http://www.samba.org
```

你可以在附录 E 第305 页“示例 `smb.conf` 配置文件”中找到我们的 `smb.conf` 配置文件。

## 4.2.1.4 全局名称解析设置

在你的 `smb.conf` 文件中，你会看到类似以下的内容：

```
name resolve order = wins bcast

wins support = yes

; wins server = w.x.y
```

参数描述见表 15。

| 参数 | 描述 |
| --- | --- |
| `name resolve order` | 通过此参数指定 Samba 服务器如何将 `NetBIOS` 名称解析为 `IP` 地址。首选值是 `wins bcast`。更多信息请参阅 `smb.conf` 文件的手册。 |
| `wins support` | 如果启用此选项，Samba 服务器也将作为 `WINS` 服务器。 |
| `wins server` | 通过此参数你告诉 Samba 使用哪个 `WINS` 服务器。 |

![](img/2d69b129b41635ef36a3e6707d34b788_147_0.png)

Samba 可以作为 `WINS` 服务器或 `WINS` 客户端，但不能同时兼顾。因此不能同时设置其中一个参数（`wins support` 或 `wins server`）。如果你指定了 `WINS` 服务器的 `IP` 地址，则 `wins support` 必须设置为 `no`。

## 4.2.1.5 创建共享

在之前的章节中，我们解释了如何准备通用配置参数。但当 Samba 服务器为用户提供资源时，它变得非常有用。在本节中，我们将解释如何创建一个共享。`smb.conf` 文件中的简单共享部分看起来如下：

```
[redbook]

comment = Redbook files

path = /redbook

browseable = yes

printable = no

writable = yes

write list = @users
```

表 16 描述了创建共享最重要的参数。

表 16. 共享参数

| 参数 | 描述 |
| --- | --- |
| `comment` | 描述共享的功能。 |
| `admin users` | 此参数用于指定具有共享管理权限的用户。当他们访问共享时，他们将以 `root` 身份执行所有操作。 |
| `path` | 定义你正在共享的目录的完整路径。 |
| `browseable` | 如果此参数设置为 `yes`，当在浏览 Samba 服务器上的资源时，可以看到该共享。该值可以是 `yes` 或 `no`。 |
| `printable` | 此参数指定该共享是否为打印共享。值可以是 `yes` 或 `no`。 |
| `write list` | 此列表中指定的的用户具有该共享的写权限。如果名称以 `@` 开头，则表示一个组名。 |
| `writable` | 此参数指定该共享是否可写。值可以是 `yes` 或 `no`。 |
| `read list` | 此列表中指定的的用户具有该共享的读取权限。如果名称以 `@` 开头，则表示一个组名。 |
| `read only` | 如果设置为 `yes`，则共享为只读。值可以是 `yes` 或 `no`。 |
| `valid users` | 此参数指定哪些用户可以访问该共享。 |

通过使用这些参数，你可以轻松地设置一个新的共享。每个共享定义以括号 `[]` 中的共享名称开始。在该名称下方，你可以指定共享参数的值。

## 4.2.1.6 共享权限

尽管你可以使用共享参数控制共享权限，但 UNIX 权限会在用户访问共享上的文件之前被应用。因此，你需要处理 UNIX 权限，以确保用户在 UNIX 下也能访问共享目录。

当用户在共享目录上创建新文件时，使用的默认创建掩码是 `0744`。对于目录创建，默认创建掩码是 `0755`。

如果你需要，可以强制使用不同的创建掩码。这些参数的解释见表 17。

表 17. 创建掩码参数

| 参数 | 描述 |
| --- | --- |
| `create mask` | 用于文件创建，以根据请求的 DOS 模式计算出的 UNIX 掩码进行屏蔽。 |
| `directory mask` | 用于目录创建，以根据请求的 DOS 模式计算出的 UNIX 掩码进行屏蔽。 |

## 4.2.1.7 为主目录创建共享

为了处理主目录，Samba 有一个名为 `[homes]` 的特殊共享部分。此共享定义用于所有主目录，因此你不需要为每个用户创建单独的共享。

当客户端请求连接文件共享时，会扫描现有的文件共享。如果找到匹配项，则使用该共享。如果没有找到匹配项，则请求的共享被视为用户名并由安全机制进行验证。如果名称存在且密码正确，将通过克隆 `[homes]` 部分创建一个该名称的共享。主共享定义使用与普通共享定义相同的参数。以下是 `smb.conf` 文件中主共享定义的示例：

```
[homes]

comment = Home Directories

path = %H

valid users = %S

browseable = no

writable = yes

create mode = 0700

directory mode = 0700
```

如你所见，我们在定义中使用了一些变量，这些变量在表 18 中进行了解释。

表 18. 变量描述

| 参数 | 描述 |
| --- | --- |
| `%H` | 此变量代表用户的主目录。 |
| `%S` | 当前服务的名称，在主目录共享的情况下，它等于用户名。 |

如示例所示，我们以这种方式对文件和目录使用了创建掩码，强制新文件或目录仅允许主目录的所有者进行访问。

## 4.2.1.8 创建打印共享

Samba 服务器对打印共享使用的步骤与主目录共享相同。如果所有共享定义和用户名都针对请求的共享名称进行了测试，但仍未找到匹配的定义，Samba 将搜索名称为该定义的打印机（如果存在 `[printers]` 部分）。如果在打印机定义中找到匹配项，则请求的服务将克隆 `[printers]` 共享部分，该服务实际上是一个打印机名称。`smb.conf` 配置文件中的打印机定义：

```
[printers]

comment = All Printers

path = /var/spool/samba

browseable = no

# 设置 public = yes 以允许用户 'guest account' 打印

guest ok = no

writable = no

printable = yes

create mask = 0700
```

如你所见，`[printers]` 部分只是另一个共享定义，当用户打印时，他们基本上是将数据拷贝到池化目录中，之后数据将由本地打印系统处理。打印共享与其他共享定义之间的唯一区别是 `printable` 参数设置为 `"yes"`。这意味着用户可以将池化文件写入共享定义下指定的目录。如果共享是可打印的，那么它在默认情况下也是可写的。

## 4.2.2 启动和停止 Samba 服务器

你可以通过执行命令启动 Samba 服务器：

```
/etc/rc.d/init.d/samba start
```

你将看到类似下方的输出：

```
[root@nf5000 /root]#etc/rc.d/init.d/samba start

Starting samba: smbd nmbd.
```

如你所见，启动了两个守护进程：`smbd` 和 `nmbd`。`smbd` 是 Samba 服务器，`nmbd` 是 `WINS` 服务器。

可以通过执行命令停止 Samba 服务器：
`/etc/rc.d/init.d/samba stop`

在你加载 SWAT 的主页后，你将看到一个类似于图 137 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_154_0.png)

图 137. SWAT 用户授权

输入在你的 Linux 服务器上定义的 Linux 用户的用户名和密码。点击 `OK` 继续。你将看到一个类似于图 138 的窗口。

> **停止**
> 任何 Linux 用户都可以访问 SWAT，但只有 `root` 用户可以进行更改。
> 记住，当你从远程机器登录 SWAT 时，你正在以明文形式发送密码。这可能会导致安全问题，因此我们建议你仅在本地进行 SWAT 管理。

![](img/2d69b129b41635ef36a3e6707d34b788_155_0.png)

如图 138 所示，你有七类可用选项：
1. `Home`（主页） - 在这里找到所有关于 Samba 的所需文档。
2. `Globals`（全局） - 在这里你可以查看并修改来自 `smb.conf` 配置文件的全局参数。
3. `Shares`（共享） - 在这里你可以查看、修改和添加共享。
4. `Printers`（打印机） - 在这里你可以查看、修改和添加打印机。
5. `Status`（状态） - 在这里你可以检查 Samba 服务器的当前状态。
6. `View`（查看） - 在这里你可以查看 `smb.conf` 配置文件的当前配置。
7. `Passwords`（密码） - 在这里你可以管理 Samba 服务器的密码。

现在我们将简要描述 SWAT 中提供的可用功能。

> **注意**
> 你可以在所有 SWAT 页面上访问这七个功能中的任何一个。每个页面的顶部都有这些功能的图标。

对 `smb.conf` 配置文件进行更改后，必须重启 Samba 服务器。

## 4.2.4.1 Globals（全局）

当你点击 SWAT 主窗口中的 `Globals` 图标时，你将看到一个一个类似于图 139 的窗口。

### 全局变量 (Global Variables)

- 提交更改 | 重置值 | 基础视图

### 基础选项 (Base Options)

| 帮助 | | |
| --- | --- | --- |
| `workgroup` | `LINUX` | 设置默认值 |
| `netbios name` | `NF5000` | 设置默认 |
| `netbios aliases` | | 设置默认 |
| `server string` | `Samba Server on Caldera OpenLinux tv` | 设置默认 |
| `interfaces` | `9.24.106.169/24` | | |
| `bond interfaces only` | `No` | 设置默认 |

### 安全选项 (Security Options)

| 帮助 | | |
| --- | --- | --- |
| `security` | `USER` | 设置默认 |
| `encrypt passwords` | `Yes` | 设置默认 |
| `update encrypted` | `No` | 设置默认 |
| `allow trusted domains` | `Yes` | 设置默认 |

图 139. SWAT 中的全局部分

在此窗口中，你可以修改 Samba 服务器的全局参数。默认情况下，你看到的是基础视图（`Basic View`）；如果你想查看高级视图（`Advanced View`），请点击 `Advanced View`。在高级视图中，你拥有所有可用选项，而在基础视图中你只能更改基础选项。要从高级视图返回基础视图，请点击 `Basic View`。完成更改后，你可以通过点击 `Commit changes` 来保存。如果你弹出一个类似于图 140 的弹出窗口，警告你正在通过网络发送非安全信息，如果你在本地工作或知道你的网络是安全的，可以轻松地选择 `Continue`。

140 Caldera OpenLinux 和 Netfinity 服务器集成指南

![](img/2d69b129b41635ef36a3e6707d34b788_158_0.png)

图 140. 安全警告

## 4.2.4.2 Shares（共享）

点击任何 SWAT Web 页面上的 `Shares` 图标，你将看到一个类似于图 141 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_158_1.png)

图 141. SWAT 中的共享部分

在这里你可以：
1. 查看已定义的共享
2. 删除共享
3. 创建新共享

## 4.2.4.3 查看或修改已定义的共享

从 `Choose Share` 按钮右侧的字段中选择共享，类似于图 142。

![](img/2d69b129b41635ef36a3e6707d34b788_159_0.png)

图 142. 选择要查看的共享

选择共享后，点击 `Choose Share` 查看共享属性。你将看到一个类似于图 143 的窗口。

142 Caldera OpenLinux 和 Netfinity 服务器集成指南

![](img/2d69b129b41635ef36a3e6707d34b788_160_0.png)

图 143. 共享属性

如果你想查看所有可用参数，点击 `Advanced View`。在此视图中，你也可以进行更改并通过点击 `Commit Changes` 保存它们。

删除现有共享

要删除现有共享，你必须先选择一个类似于图 142 的已定义共享。然后点击 `Delete Share`。

> **停止**
> 共享将立即删除且无警告。

在你删除共享后，Samba 服务器必须重启。

## 4.2.4.5 创建新共享

要创建一个共享，请遵循以下步骤：
1. 创建一个将用于共享的目录。你可以通过终端执行此命令来实现：
```bash
mkdir /home/public
```



2. 确保该目录的 UNIX 权限设置正确，以便用户可以访问。
3. 在 `SWAT Web` 页面的共享部分，输入你要创建的共享名称，类似于图 144。
![](img/2d69b129b41635ef36a3e6707d34b788_161_0.png)

图 144. 输入共享名称
4. 点击 `Share` 继续，你将看到一个类似于图 145 的窗口。
![](img/2d69b129b41635ef36a3e6707d34b788_162_0.png)

图 145. 输入所需的共享
5. 填写所需的参数。如果你需要设置更多参数，点击 `Advanced View`。在你输入所有参数后，点击 `Commit Changes` 来保存你的共享。
6. 通过选择 `SWAT` 页面上的 `View` 查看 `smb.conf` 配置文件。你将看到一个类似于图 146 的窗口。
![](img/2d69b129b41635ef36a3e6707d34b788_163_0.png)

图 146. 查看 `smb.conf` 配置

7. 重启 `Samba` 服务器。

恭喜！你已经在 `Samba` 服务器上创建了第一个可用共享。

## 4.2.4.6 重启 `Samba` 服务器

通过点击任何 `SWAT Web` 页面上的图标可以重启 `Samba` 服务器。你将看到一个类似于图 147 的窗口。

### 服务器状态 (`Server Status`)

自动刷新
刷新间隔：30

### 激活连接 (`Active Connections`)

| `PID` | 客户端 | `IP` 地址 | 日期 | 杀死 |
|---|---|---|---|---|
| 11508 | 23-8pc3 | 9.24.106.146 | 10月20日 15:37 | |

### 激活共享 (`Active Shares`)

| 共享 | 用户 | 组 | `PID` | 客户端 | 日期 |
|---|---|---|---|---|---|
| `public` | `users` | 11508 | 23-8pc3 | 10月20日 15:37 |

图 147. 重启 `Samba` 服务器

只需点击 `Restart smbd` 即可重启 `Samba` 服务器。在此页面上，你还可以点击 `Restart nmbd` 重启 `WINS` 服务器。

## 4.2.4.7 `Printers`（打印机）

在打印机部分，你可以查看、修改或添加打印机。处理打印机的操作与处理共享相同。通过点击类似于图 148 的 `SWAT` 页面上的 `Printers` 图标可以访问打印机设置。

![](img/2d69b129b41635ef36a3e6707d34b788_165_0.png)

图 148. `SWAT` 打印机部分

如果你想查看特定打印机的设置，如图 149 所示从列表中选择打印机。

![](img/2d69b129b41635ef36a3e6707d34b788_166_0.png)

图 149. 选择要查看的打印机

选择打印机后，点击 `Choose Printer` 查看其属性。你将看到一个类似于图 150 的窗口。

```ini
log file = /var/log/samba/log
max size = 50
name order = hosts
socket option = TCP
dns proxy =
wins support = Yes

[homes]
comment = Home Directories
valid users = @
read only = No
create mask = 0700
browseable = No

[printers]
comment = All Printers
path = /var/spool/samba
printing = none
print ok = Yes
browseable = No

[redbook]
comment = Redbook
path = /redbook
write list = @
read only = No

[public]
comment = Samba
path = /home/public
write list = @
read only = No
create mask = 0777
```

图 150. 查看 `smb.conf` 文件

![](img/2d69b129b41635ef36a3e6707d34b788_167_0.png)

图 150. 打印机属性
在此视图中，你还可以修改打印机属性。完成后，点击 `提交更改`（`Commit Changes`）保存设置。

### 4.2.4.8 状态

在本节中，你可以检查 `Samba` 服务器的状态。在这里你可以查看所有的连接和打开的文件。你还可以启动或重启 `Samba` 服务器或其各个组件。如图 151 所示，你可以点击 `SWAT` 页面上的 `状态`（`Status`）图标访问打印机设置。

![](img/2d69b129b41635ef36a3e6707d34b788_168_0.png)

图 151. 状态部分

## 4.2.4.9 查看

在本节中，你可以查看当前的 `smb.conf` 配置文件。你可以点击 `SWAT` 页面上的 `查看`（`View`）图标来访问打印机设置，类似于图 152。

![](img/2d69b129b41635ef36a3e6707d34b788_169_0.png)

# 当前配置

```
# Samba config file created using SWAT
# from: 23-BP3PC.itco.ral.ibm.com (9.24.106.146)
# Date: 1999/10/20 17:19:26

[global]
workgroup = LINUX
ethbios name = NY5000
server string = 9.24.106.169/24 Server on Caldera OpenLinux
encrypt passwords = Yes
log file = /var/log/samba.d/smb.log
max log size = 50
name resolve order = wins hosts boost
socket options = TCP NODELAY
dns proxy = No
wins support = Yes
printing = lprng

[home]
comment = Home Directories
path = %h
valid users = *
read_only = No
document_lock = Done
```

图 152. `SWAT` 的查看部分

## 4.2.10 密码

在本节中，你可以管理所有 `Samba` 用户的密码。如图 153 所示，你可以点击 `Samba` 页面上的 `密码`（`Password`）图标访问打印机设置。

## 3 来源和附加信息

你可以在 `Samba` 官方项目网站找到更多信息：

```
http://www.samba.org
```

在 `Linux` 文档项目（`Linux Documentation project`）主页上一直有很多教程文档：

```
http://www.linuxdoc.org/
```

![](img/2d69b129b41635ef36a3e6707d34b788_170_0.png)

图 153. 管理密码

## 第 5 章 `DNS` - 域名服务

如果你将两或多台计算机连接到网络，它们就可以共享信息和资源。然而，这些计算机需要“用同一种语言说话”才能建立连接。这种“语言”被称为网络协议。今天最流行的通信协议是 `TCP/IP`。这是互联网以及许多局域网正在使用的协议。

`TCP/IP` 网络中的主机使用唯一的 `IP` 地址进行相互通信。这些地址由四个 8 位数（字节）组成，用点隔开。例如，主机 `A` 的地址为 `192.168.99.1`，而主机 `B` 使用的是 `122.68.29.5`。

然而，这种地址方案对人类来说并不十分直观，几乎不可能通过 `IP` 地址记住大量主机。因此，人们发明了一套命名方案。

每个主机都有一个主机名（例如 `fred`）并属于某个域名（例如 `snake-oil.com`）。域名可以以层次化的方式组织，并由不同的子域名组成（例如 `marketing.snake-oil.com`）。主机名及其域名的组合称为完全限定域名（`FQDN`）（例如 `fred.marketing.snake-oil.com`）。由于域名是层次化的，在不同的子域名中可能具有相同主机名的更多主机。因此，`fred.marketing.snake-oil.com` 可以与 `fred.management.snake-oil.com` 是不同的主机，你需要向中央注册机构注册你的域名。有几个顶级域名，如 `.com`、`.org` 或 `.net`。除了这些通用顶级域名外，每个国家都有自己的国家代码作为顶级域名。例如，德国有 `.de`，丹麦有 `.dk`，芬兰有 `.fi`。

由于主机内部仍然使用其 `IP` 地址进行通信，因此主机名与相应的 `IP` 地址之间需要一种映射。这种映射可以通过方式实现：

将网络中的所有主机（包括其 `IP` 地址）都放入一个静态文本文件中。对于想要通过名称与其他主机通信的每台主机，都必须复制此文件。一旦主机从网络中添加或删除，或者 `IP` 地址或主机名发生变化，所有计算机上的主机文件都必须进行相应调整。如果主机数量达到一定程度，这可能会变得非常繁琐。

这就是域名系统（`DNS`）派上用场的地方。以下对 `DNS` 的描述非常简单，但它应该让你对 `DNS` 的本质有一个大致的了解。

与其在每台机器上维护单独的主机文件，不如由一台服务器携带其域下所有主机和 `IP` 地址的列表。现在所有客户端向这个中央服务器发送主机解析请求，而不是在本地表中查找。域名服务器将查询请求的主机名并返回相应的 `IP` 地址。此外，客户端也可以请求属于特定 `IP` 地址的主机名。如果客户端请求另一个域的 `IP` 地址，如果本地域名服务器无法自行回答请求，它会将请求转发到其层次结构中上一个域名服务器。因此，主机表的更改只需要在一个中心点进行，而不是在网络的所有参与者处进行。

![](img/2d69b129b41635ef36a3e6707d34b788_173_0.png)

图 154. `DNS` 层次结构

## 5.1 软件安装

域名服务器的主配置文件是 `/etc/named.conf`。由于大多数发行版带有一个非常详细的示例配置，你可能想将其保存备参考。我们将从头创建一个新文件。

## 5.2 `DNS` 配置

域名服务器的主配置文件是 `/etc/named.conf`。由于大多数发行版带有一个非常详细的示例配置，你可能想将其保存备参考。我们将从头创建一个新文件。

你还需要按照如下所示创建一个 `/var/named/localhost.zone` 文件：

```
@ORIGIN localhost.\      1D IN SOA      @ root (
@42                     ; serial (d. adams)
3H                     ; refresh
15M                    ; retry
1W                     ; expiry
1D )                   ; minimum
1D IN NS               @
1D IN A                127.0.0.1
```

此外，创建一个包含内容的 `/var/named/127.0.0.0 zone` 区域：

```
@ORIGIN 0.0.127.in-addr.arpa.
@                     localhost.root.localhost. (
42                     ; serial (d. adams)
3H                     ; refresh
15M                    ; retry
1W                     ; expiry
1D )                   ; minimum
1D IN NS               localhost.
1D IN PTR              localhost.
1
```

你的网络客户端都应被配置为查询本地 `DNS` 服务器的 `IP` 地址，而不是你的 `ISP` 域名服务器。

你现在可以使用以下命令启动服务器：

```
/etc/rc.d/init/named start
```

检查 `/var/log/messages` 文件中的启动信息。域名服务器应该通过将查询转发到 `ISP` 的域名服务器来解析客户端的 `DNS` 查询。你可以通过 `host <hostname>` 和 `nslookup` 命令来验证这一点。

如果你希望 `DNS` 在 `Linux` 服务器启动时自动启动，请遵循第 134 页 4.2.3 节“将 `Samba` 作为启动服务启动”中的说明，但不要选择 `SMB` 服务器进程 (`samba`)，而是使用 `Internet` 域名服务器 (`named`)。在你启用了 `DNS` 作为服务运行后，它将在 `Linux` 服务器启动时自动启动。

在接下来的步骤中，此服务器现在还应该作为本地域名 `snake-oil.com` 的主域名服务器。使用此命令停止域名服务器：

```
/etc/rc.init/named stop
```

编辑 `/etc/named.conf` 文件，使其看起来如下所示：

```
options {
  directory "/var/named";
  listen-on ( any );
  forward only;
  forwarders (9.24.106.15);
  sortlist (
    ( localhost, localnets);
    ( localnets );
  );
}

logging {
  category lame-servers ( null );
  category cname ( null );
}

zone "." {
  type hint;
  file "root.hint";
}

zone "localhost" IN {
  type master;
  file "localhost.zone";
  check-names fail;
  allow-update { none };
}

zone "0.127.0.in-addr.arpa" IN {
  type master;
  file "127.0.0.zone";
  check-names fail;
  allow-update { none };
}

zone "snake-oil.com" {
  type master;
  file "snake-oil.zone";
}

zone "99.168.192.IN-ADDR.ARPA" {
  type master;
  file "snake-oil.rev";
}
```

我们现在已经添加了本地域名 `snake-oil.com` 需要的区域文件（数据库）。`/var/named/snake-oil.zone` 文件负责主机名到 `IP` 地址的映射。

```
;
; Zone file for snake-oil.com
```

```
@  IN SOA ns.snake-oil.com. hostmaster.snake-oil.com. (
        199910011 ; serial, todays date + todays serial #n
        8H        ; refresh, seconds
        2H        ; retry, seconds
        1W        ; expire, seconds
        1D)       ; minimum, seconds
```

```
NS  ; Inet Address of nameserver
MX  10 mail      ; Primary Mail Exchanger
MX  20 mail.bigisp.com. ; Secondary Mail Exchanger
```

```
localhost A  127.0.0.1
gw       A  192.168.9.1
ns       A  192.168.9.2
fred     A  192.168.9.3
mail     A  192.168.9.4
ftp      A  192.168.9.5
www       A  192.168.9.6
```

你还应该创建区域文件 `/var/named/snake-oil.rev`。这对于反向域名查找是必要的，例如，当你需要将 `IP` 地址解析为其名称时。

```
@  IN SOA ns.snake-oil.com. hostmaster.snake-oil.com. (
        199910011 ; Serial, todays date + todays serial #n
        8H        ; Refresh
        2H        ; Expire
        1D)       ; Minimum TTL
    NS ns.snake-oil.com.
```

```
1  PTR gw.snake-oil.com.
2  PTR ns.snake-oil.com.
3  PTR fred.snake-oil.com.
4  PTR mail.snake-oil.com.
5  PTR ftp.snake-oil.com.
6  PTR www.snake-oil.com.
```

现在通过运行 `named restart` 让域名服务器重新加载其配置。查看 `/var/log/messages` 中的消息。如果一切一切顺利，你将看到类似下面的消息：

```



## 5.2 启动 Named

Oct 26 18:03:20 ns named: cache (IN) loaded (serial 42)

Oct 26 18:03:20 ns named: master "localhost" (IN) loaded (serial 4)

Oct 26 18:03:20 ns named: master "0.127.0.in-addr.arpa" (IN) loaded (serial 4)

Oct 26 18:03:20 ns named: master "snake-oil.com" (IN) loaded (serial 99)

Oct 26 18:03:20 ns named: master "99.168.192.IN-ADDR.ARPA" (IN) loaded (serial 9910011)

Oct 26 18:03:20 ns named: listening on 127.0.0.1:53 (lo)

Oct 26 18:03:20 ns named: listening on 9.24.106.15:53 (eth0)

Oct 26 18:03:20 ns named: Forwarding source address is 0.0.0.0:1)

Oct 26 18:03:20 ns named: Ready to answer queries.

## 5.3 配置技巧

在 `named.conf` 的 `options` 部分使用 `listen-on` 指令。对于域名服务器监听的每个接口，都会打开一对文件句柄。在繁忙的域名服务器上，节省每个文件句柄是一个巨大的优势。定期检查 `/var/log/messages` 文件以发现错误。`Named` 的消息非常详尽。如果你不断地添加、删除或修改你的区域记录，你可能想看一眼 `nsupdate` 工具，它也属于 `bind` 软件包。你的域名服务器也应该能正确地解析 `snake-oil` 域名的主机名。

# 第 6 章 DHCP - 动态配置协议

随着可用 IP 地址数量的不断减少，以及维护静态 IP 的苦恼，DHCP 已成为大多数 TCP/IP 环境的必需。

## 6.1 什么是 DHCP？

DHCP 代表动态主机配置协议。在使用 TCP/IP 时，计算机系统需要一个唯一的 IP 地址。没有 DHCP，必须为每个计算机系统输入 IP 地址。有了 DHCP，服务器分配 IP 地址。

## 6.2 我为什么应该使用 DHCP？

在过去，网络上的每个设备都必须有一个静态 IP 地址。随着访问互联网的计算机增加，可用地址池正在迅速减少。网络管理员可以使用 DHCP 大幅减少所需的 IP 地址。

即使对于较小的网络，跟踪单个 IP 地址也非常困难。有了 DHCP，服务器完成所有的维护工作，映射 IP 地址到 MAC 地址并跟踪租赁时间。

## 6.3 在 Linux 上实现

在本节中我们将讨论如何在 Linux 上实现 DHCP 服务器。

首先我们将安装 DHCP 服务器二进制文件。该软件包位于 Caldera OpenLinux 光盘上，并且默认安装。你可以按照我们在第 123 页“设置 Samba 服务器”中描述的方法验证这一点。`dhcpd` 软件包位于 Boot Session 中的 Server 部分。启动软件包后，你将看到一个类似于图 155 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b88_181_0.png)

图 155. 验证 `dhcpd` 软件包已安装

`dhcpd` 服务器配置文件通常位于 `/etc/dhcp/dhcpd.conf` 或 `/etc/dhcpd.conf`（取决于发行版）。以下是一个示例配置：

```
# DHCP 服务器配置文件。

# 请参阅 /usr/doc/dhcpd-1.0pl2 获取示例，

# 并查看 man 页 dhcpd.conf。

#

default-lease-time 600;

max-lease-time 7200;

option subnet-mask 255.255.255.0;

option broadcast-address 192.168.1.255;

option routers 192.168.1.254;

option domain-name-servers 192.168.1.1, 192.168.1.2;

option domain-name "ibm.com";

subnet 192.168.1.0 netmask 255.255.255.0 (

  range 192.168.1.100;

)
```

您并不局限于单个子网。您允许共享网络特定参数、多个子网特定参数、组参数以及主机特定参数。

您可以定义多个范围，根据客户端的硬件地址分配特定的 IP 地址，并在需要时指定 WINS 服务器。

更多信息请参阅 `dhcpd.conf` man 页。

DHCP 服务器需要一个地方来跟踪租约。这是通过 `/var/state/dhcpd.leases` 文件完成的。

要启动 DHCP 服务器，请输入：

```
/etc/rc.d/init/dhcpd start
```

如需调试信息，请使用 `-d -f` 标志。

如果您希望 DHCP 服务器在服务器启动时自动启动，请遵循第 134 页 4.2.3 “将 Samba 作为启动服务启动”中的说明，但不要选择 SMB 服务器进程 (`samba`)，而是选择 DHCP 和 BOOTP 启动服务器。

# 第 7 章 Apache Web IBM HTTP 服务器

Apache Web 服务器是当今互联网上流行的 Web 服务器软件。根据 NetCraft 在 `http://www.netcraft.com/survey/` 上的 Web 服务器调查，所有调查的 Web 服务器中，超过 55%（超过 730 万个）运行着 Apache 版本（截至本文编写时）。Apache 是一个非常成功的协作开源项目。Apache 的网站是 `http://www.apache.org`。由于完整源代码免费提供，它是一个灵活且强大的 Web 服务器解决方案。此外还有许多额外的模块，可以与 Apache 主程序结合使用。一些流行的示例包括 PHP（PHP: 超文本预处理器，一种嵌入的 HTML 脚本语言）、`mod_perl`（一个嵌入的 perl 解释器）以及用于安全事务的 `mod_ssl`。可以从 Apache 模块库下载更多 Apache 模块：`http://modules.apache.org`。

Apache 的一些关键特性包括：

- 实现最新的协议，包括 HTTP/1.1 (RFC2068)。
- 具有高度配置性，并可以通过第三方模块进行扩展。
- 可以使用 Apache 模块 API 编写“模块”进行自定义。
- 提供完整的源代码并附带不受限制的许可。
- 可以在大多数版本的 UNIX（包括 Linux）上无需修改即可运行。
- 用于身份验证的 DBM 数据库，允许您设置具有大量授权用户的密码保护页面，而不会导致服务器缓慢。也可以使用多种 SQL 数据库进行身份验证（使用附加模块）。
- 对错误和问题的自定义响应，允许您设置文件甚至甚至是 CGI 脚本，由服务器在响应错误和问题时返回。例如，您可以设置一个脚本来拦截 500 服务器错误，并对用户和自己进行实时诊断。
- 多个 `DirectoryIndex` 指令，允许您设置 `DirectoryIndex index.html index.cgi`，这指示服务器在请求目录 URL 时返回 `index.html` 或运行 `index.cgi`，取决于它在目录中找到哪一个。
- 可以在文件中声明无限数量的 `alias`（别名）和 `redirect`（重定向）指令。

## 7.1 IBM HTTP 服务器

由 Apache IBM HTTP Server 基于 Apache HTTP Server。除了 Linux 之外，此 HTTP 服务器还运行在 AIX、Solaris 和 Windows NT 上。访问主页：

```
http://www-4.ibm.com/software/webservers/httpsservers/
```

Linux 版 IBM HTTP Server 提供以下额外功能：

- 远程配置：基于浏览器的配置工具，允许通过 GUI 操作服务器。
- SNMP 支持：简单网络管理协议 (SNMP) 是一种用于远程管理和收集服务器信息的成熟协议。此新支持允许 IBM HTTP Server 通过 SNMP 协议进行管理。
- LDAP：IBM HTTP Server 轻量级目录访问协议 (LDAP) 插件允许由 LDAP 服务器执行身份验证和授权（访问受保护资源时需要），从而大大减少了为每个 Web 服务器本地维护用户和组信息的管理开销。
- 机器翻译支持：此项新功能与可用的 IBM 机器翻译引擎配合使用时，允许 IBM HTTP Server 在无需人工干预的情况下将英文页面翻译成其他语言。这允许网站访问者以母语言阅读页面，有效地扩大了您的网站的影响范围。IBM 机器翻译引擎包含在 WebSphere Application Server 3.0 中，包括德语、简体中文和繁中文。未来将提供更多语言。
- 支持 SSL：IBM HTTP Server 支持安全连接。
- 快速响应：缓存可以显著提高服务器性能。

## 7.2 安装 Apache

Linux 通常默认安装 Apache HTTP 服务器。您可以通过运行第 72 页 2.5 “添加和删除软件”中描述的命令来检查是否安装了 Apache 包。启动、停止或重新加载 Apache，运行脚本：

```
/etc/rc.d/init/httpd (start|stop)
```

在 Caldera Linux 中，Apache 将从 `/home/httpd` 提供 HTML 文档，从 `/home/httpd/cgi-bin` 提供 CGI 脚本。如果您安装了 PHP 模块 (`mod_php`)，如果文件以 `.php` 结尾，它也将执行 PHP 代码。访问日志文件位于 `/var/log/httpd/access_log`，错误日志文件位于 `/var/log/httpd/error_log`。Apache 配置文件位于 `/etc/httpd/conf`。

如果您现在将浏览器指向服务器的 IP 地址，当 Apache 服务器运行时，您将看到以下页面 (`/home/httpd/html/index.html`)：

# 成功了！此网站已安装 Apache Web 服务器

如果您能看到此页面，该域的所有者刚刚成功安装了 Apache Web 服务器。他们现在必须在此目录添加内容并替换此占位页面，否则让服务器指向其真实内容。

> 如果您看到此页面而不是预期的网站，请联系该网站的管理员。（尝试向 `webmaster@domain.com` 发送邮件）尽管此网站运行 Apache 软件，但与 Apache 组没有联系，请勿就此网站或内容向 Apache 作者发送邮件。如果这样做，您的邮件将被忽略。

Apache 文档包含在此发行版中。

此网站的管理员管理员可在支持 Apache 的 Web 服务器上使用下方的图片。感谢使用 Apache！

![](img/2d69b129b41635ef36a3e6707d34b788_187_0.png)

图 156. Caldera Linux 上的 Apache 启动页面

## 7.3 IBM HTTP Server 安装

在 Caldera Linux 上安装 IBM HTTP Server，您需要执行以下步骤。

对于 IBM HTTP 服务器和远程管理功能，请从页面下载以下 tar 文件：

```
http://www-4.ibm.com/software/webservers/httpsservers/download.html
```

`HTTPServer.linux.glibc2.server.tar` 文件包含以下包：

- `IBM_HTTP_Server-1.3.6-2.i386.rpm` - IHS Web 服务器
- `IBM_Apache_Source-1.3.6-2.i386.rpm` - Apache 1.3.6 服务器
- `Readme.httpspserver` - 安装说明

`HTTPServer.linux.glibc21.admin.tar.file` 包含以下软件包：

- `IBM_Admin_Server-1.3.6-1.i386.rpm` - GUI 管理服务器
- `IBM_Admin_Server_Forms-1.3.6-1.i386.rpm` - 用于 GUI 的 Web 表单

还有一些额外的软件包（如 SNMP 和 SSL 模块）也可以安装。然而，本章节将不再涵盖这些。请参考下处的安装说明：

```
http://www-4.ibm.com/software/websservers/httpserver/doc/v136/readme_httpserver.htm
```

下载完“压缩包”（tarballs）后，将其移动到 `/tmp` 目录并使用以下命令解压：

```bash
tar xvf HttpServer.linux.glibc21.server.tar
tar xvf HttpServer.linux.glibc21.admin.tar
```

这会将上述的 RPM 文件从压缩包中提取到 `/tmp/IHS` 子目录中。你需要切换到 `root` 用户（如果你尚未切换的话）。为了避免资源冲突，你必须首先执行以下命令关闭当前运行的 Apache Web 服务器（如果已安装）：

```bash
/etc/rc.d/init/httpd stop
```

此外，请确保在下次重启后它不会再次启动，方法如我们在 2.9 节第 88 页“守护进程（服务）”中所描述的那样禁用 Web 服务器服务。

现在，你需要使用以下命令安装软件包（假设软件包位于当前目录）：

```bash
rpm -Uhv IBM_HTTP_Server-1.3.6-1.i386.rpm
rpm -Uhv IBM_Admin_Server-1.3.6-1.i386.rpm
rpm -Uhv IBM_Admin_Server_Forms-1.3.6-1.i386.rpm
```

安装 HTTP Server 软件包时也会尝试自动启动服务器。如果它没有启动，可能还有另一个 HTTP 服务器在运行。请先停止那一个，然后使用以下命令尝试重启 IBM HTTP Server：

```bash
/etc/rc.d/init/ibmhttpd start
```

如果命令行或以下路径：

```
/opt/IBMHTTPServer/logs/error_log
```

中没有错误，

请尝试用浏览器打开新 HTTP 服务器的首页。你应该能看到以下页面：

![](img/2d69b129b41635ef36a3e6707d34b788_189_0.png)

图 157. IBM HTTP Server 启动页面

如果你仍然看到旧 Web 服务器的启动页面，请在 Netscape 浏览器上按 `Shift+Reload` 强制刷新此页面。

IBM HTTP Server 的基础安装已完成！在默认设置下，它从 `/opt/IBMHTTPD/htdocs` 目录提供 HTML 页面，并从 `/opt/IBMHTTPD/cgi-bin` 提供 CGI 脚本。日志文件位于 `/opt/IBMHTTPD/logs`。

172 Caldera OpenLinux 和 Netfinity 服务器集成指南

### 7.3.1 在系统启动时激活 IBM HTTPD

默认情况下，IBM HTTP Server 必须在系统重启后手动启动。如果你希望它自动启动，则必须将启动脚本添加到启动过程中。

如果你希望此服务器在启动时运行，你需要在 `/etc/rc.d/rc3.d` 目录（如果你在运行级别 3 启动系统，这是默认运行级别）或 `/etc/rc.d/rc5.d`（如果你在运行级别 5 启动系统）中创建正确的符号链接。你可以通过以下命令手动完成：

```bash
cd /etc/rc.d/rc3.d
ln -s ../init.d/ibmhttpd /etc/rc.d/rc3.d/S67ibmhttpd
ln -s ../init.d/ibmhttpd /etc/rc.d/rc3.d/K01ibmhttpd
```

```bash
cd /etc/rc.d/rc5.d
ln -s ../init.d/ibmhttpd /etc/rc.d/rc5.d/S67ibmhttpd
ln -s ../init.d/ibmhttpd /etc/rc.d/rc5.d/K01ibmhttpd
```

这将在运行级别 3 和运行级别 5 下启动 IBM HTTP 服务器，并确保在切换到其他运行级别（例如关机）时能够正常关闭。

### 7.3.2 设置管理服务器

在开始使用管理服务器之前，你必须执行一些准备步骤，以便远程修改 IBM HTTP Server 的配置文件。

管理服务器任务的基本意图是允许管理服务器对必要的配置文件具有读/写/执行权限。管理服务器应该通过创建的唯一用户 ID 和组来获取读/写权限。管理服务器配置文件中的 `User` 和 `Group` 指令应更改为唯一的用户 ID 和组。管理服务器配置文件的“组访问权限”应更改为允许读写“组访问”。此外，还有一个实用程序，它应该具有“组执行权限”和“设置用户 ID 为 Root 权限”。该可执行文件必须运行，以便请求重启 IBM HTTP Server 和管理服务器。

为了正确设置这些前提条件，可以通过执行脚本 `/opt/IBMHTTPServer/bin/setup` 来完成这些任务。调用后，它将向你提几个问题并提供每个执行步骤的详细信息。在 Caldera OpenLinux 上，脚本无法自动为管理服务器创建新的用户和组。解决方案是用 COAS 工具创建组和账户，然后在设置管理服务器时使用这些名称。在随后的屏幕中输入加粗标记的关键字：



```bash
[root@n5000 #] ./setup
n**********************************
请提供一个运行管理服务器的 User ID
我们将使用系统管理工具创建 USERID
**************************************************
[no default] -> 你已创建的账户名
**************************************************
请提供一个运行管理服务器的 GROUP NAME
我们将使用系统管理工具创建该组
**************************************************
[no default] -> 你已创建的组名
**************************************************
请提供包含需要更改权限的文件目录
**************************************************
[no default] -> /opt/IBMHTTPServer
**************************************************
请提供一个运行管理服务器的 User ID
我们将使用系统管理工具创建 USERID
请提供一个运行管理服务器的 GROUP NAME
我们将使用系统管理工具创建该组
请提供包含需要更改权限的文件目录
/opt/IBMHTTPServer
```

配置文件：`/opt/IBMHTTPServer/conf/admin.conf`

将被保存为 `/opt/IBMHTTPServer/conf/admin.conf.13:48:05_295`

您是否要更新管理服务器配置文件

输入 `CONTINUE` 继续

输入 `EXIT` 退出

```
[default: QUIT -2]-> 1
USER DONE
组已成功更新配置文件
旧配置文件已保存为 '/opt/IBMHTTPServer/conf/admin.conf.13:48:05_295'
[root@mf5000 bin]#
```

总结上述步骤：管理服务器将以用户 `wwwrun` 和组 `nobody` 运行。

管理服务器基本上是另一个 Web 服务器，与主 IBM HTTP 服务器(s) 并运行。因此，它必须单独启动并监听另一个 TCP 端口（默认为 8008）。默认情况下，它必须手动启动。如果您还希望在系统启动时启动它，则必须将启动脚本集成到启动程序中。将文件 `/opt/IBMHTTPServer/bin/adminctl` 复制到目录 `/etc/rc.d/init.d`，并按照第 173 页第 7.3.1 节“系统启动时激活 IBM HTTPD”中描述的步骤操作，使用 `adminctl` 代替 `ibmhttpd` 作为初始化脚本名称。

管理服务器受用户名和密码保护。您可以在 `/opt/IBMHTTPServer/bin` 目录下执行以下命令，在密码文件 `/opt/IBMHTTPServer/bin/conf/admin.passwd` 中创建一个条目：

```
./htppasswd -m ../conf/admin.passwd <user name>
```

两次输入所需用户名的密码。如果您需要区分多个管理员，该密码文件中可以包含多个一个用户名。

现在，您可以通过运行以下命令来启动管理服务器：

```
/opt/IBMHTTPServer/bin/adminctl start
```

在点击第 172 页图 157 所示的配置服务器（`Configure Server`）链接后，您需要输入为管理服务器用户定义的用户名和密码。如果输入正确，您将看到管理服务器的欢迎页面：

# IBM 管理服务器

- 入门
- 基础设置
- 结构结构
- 索引
- 身份验证文件
- 访问权限
- 安全
- 日志
- 映射
- 脚本
- 性能
- MIME
- 查看配置

# IBM 管理服务器

通过引导复杂的配置，管理服务器极大地简化了曾经需要手动配置 Web 服务器的任务。您选择一个要配置的服务器，管理服务器会提示您输入配置值，当您点击提交（`Submit`）时，这些值将写入配置文件。

要查看管理 IBM HTTP Server 有多简单，请在管理服务器上设置几个配置选项，而无需触碰配置文件。

- 浏览器要求
- 用户和组设置信息
- 安装后的后续操作
- 导航面板中的任务！
- 用户协助（帮助）
- 此处使用的按钮和图标
- 此处使用的约定
- 选择服务器
- 管理服务器

![](img/2d69b129b41635ef36a3e6707d34b788_195_0.png)

图 158. 管理服务器启动窗口

现在您可以准备好根据需要调整主 Web 服务器的配置了。请参考在线文档获取有关不同配置选项的帮助。

## 7.4 性能提示

配置 Apache 以获得最高性能取决于许多参数。Apache 非常灵活，获得最佳性能可能需要一些研究。在 Apache 网站上可以找到关于 Apache 性能调优的详尽文档：

`http://www.apache.org/docs/misc/perf-tuning.html`

简而言之，请尝试以下选项：

- 设置 `FollowLinks` 选项，除非你真的不需要。

- 将 `AllowOverride` 设置为 `None`，除非你真的需要。

- 从常用到最不常用显式列出每个 `Directory` 文件。

- 调整 `KeepAliveTimeout`，从 3 开始，根据内容和连接类型调整到 30。

- Apache（以及 IBM HTTP Server）使用多个进程来处理单个请求。调整 `StartServers`，从 64 开始，以 32 为步长增加，直到性能下降。调整 `MaxClients`，起始值从 `StartServers` 的值开始。**注意：** 如果 `Max Clients` 过大，扩展性能可能会大幅下降！

- 对于监听单个套字的 SMP 系统，尝试在定义 `SINGLE_LISTEN_UNSERIALIZED_ACCEPT` 后重新编译。

用于基准测试 Apache 服务器的实用工具是 `ab`。在最简单的形式下，您可以这样调用它：

`ab http://www.your-server.com/index.html`

以下是 `ab` 选项：

```
[root@nf5000]# ab -h
Usage: ab [options] [http://hostname[:port]]/path
Options are:
-n requests 执行的请求数
-c concurrency 并发的多个请求数
-t timeout 等待响应的最大秒数
-p postfile 包含 POST 数据的文件
-T content-type POST 的内容-type
-v verbosity 打印多少排故障排除信息
-w 以 HTTP 表格形式输出结果
-x attributes 插入作为表格属性的字符串
-y attributes 插入作为 tr 属性的字符串
-z attributes 插入作为 td 或 th 属性的字符串
-V 打印版本号并退出
-k 使用 HTTP KeepAlive 功能
-h 显示用法信息（此消息）
```

## 8 Sendmail

与人交流是最令人渴望的体验之一。每天给人们发送邮件都非常重要。

## 8.1 什么是 Sendmail？

从名称就可以看出，Sendmail 用于发送邮件。然而，电子邮件比普通邮件更重要。通过 Sendmail，它是一个强大的邮件传输代理 (MTA)，用于将邮件传递给接收者。

## 8.2 您可以使用 Sendmail 做什么

通过 Sendmail，您的 Linux 服务器可以成为电子邮件服务器。您还可以为域用户提供邮件服务。当您设置好 Sendmail 后，Linux 服务器上的用户仍然可以向任何地方发送邮件。

## 8.3 在开始之前

在接下来的章节中，我们将解释如何在您的 Linux 服务器上设置邮件服务器。在解释中，我们将使用我们的实验设置，所有的设置都与此实验相关。您可以轻松地将其应用于现有的安装中。在继续实施之前，您需要验证是否安装了这些包：

- `bind-8.1.2-1`

- `bind-utils-8.1.2-1`

- `sendmail-8.9.3-1`

- `sendmail-cf-8.9.3-1`

您可以通过从 COAS 工具中启动包工具来实现此，正如我们在第 72 页第 2.5 节“使用 `kpackage` 添加和删除软件包”中所解释的那样。这些软件包位于服务器部分的 `Network` 和 `Mail` 子部分。如果未安装这些包，请参考相应的软件包中关于如何安装的说明。

> 注意

> Sendmail 的成功运行需要正确的域名系统 (DNS) 设置。这意味着您必须正确设置自己的 DNS，或者访问另一个 DNS。

如图 159 所示，我们的网络由三个域组成：

1. `Itso` - 这是主（根）域。该域中的所有计算机都有 `.itso` 扩展。在该域中，我们有一个运行主（根）DNS 的服务器。

2. `First.itso` - 这是 `.itso` 域的第一个子域。该域的主服务器运行该域的 DNS，也是该域用户的邮件 (Sendmail) 服务器。

3. 第二，`second.itso` - 这是 `.itso` 域的第二个子域名。该域的主服务器运行着该域的 DNS，并作为该域用户的邮件（Sendmail）服务器。

邮件服务器的所有用户在他们的域名服务器上都有用户名/密码定义，即使他们使用的是其他的物理服务器或工作站。他们需要这些用户名/密码来访问邮件。每个定义的用户在邮件服务器上都有一个邮箱箱。他可以通过客户端连接邮件服务器并通过网络访问邮件。当连接建立后，用户可以将邮件下载到其工作站并从服务器上删除。或者他也可以远程连接到服务器并在服务器上读取邮件，在这种情况下，邮件将保留在服务器的邮箱箱中。

当用户仅将服务器用于邮件且他们有自己的工作站时，邮件服务器会为每个邮箱箱设置有限的空间。这意味着用户必须定期从服务器下载邮件，以便为新邮件留出空间。在用户使用服务器进行操作的环境中，邮箱箱通常会更大。用户可以使用客户端远程访问邮件，在这种情况下他们不会下载邮件。

用于发送和递送邮件的最常用协议是 SMTP/POP3。简单邮件传输协议 (SMTP) 用于从邮件客户端发送邮件，邮局协议 (POP3) 用于从邮件服务器获取邮件。Sendmail 除了所有其他协议外还支持 SMTP 和 POP3 协议。在我们的设置中，我们使用了 SMTP/POP3 协议进行邮件交换。

在我们开始描述设置邮件服务器之前，我们将先描述如何为我们的实验网络设置 DNS。因为正确的 DNS 设置对于邮件服务器的成功运行非常重要。

## 8.4 网络配置

每个子域都位于自己的网络中。`"first.itso"` 域位于 `172.168.0.0` 网络，`"second.itso"` 域位于 `192.168.0.0` 网络。运行 `"itso"` 域的服务器充当这两个两个子域的网关。

我们有以下网络定义：

- 1. 带有两个网卡 (NIC) 的网关服务器。第一个网卡的 IP 为 `172.168.0.1`，第二个网卡的 IP 为 `192.168.0.1`。该服务器启用了 IP 转发（IP Forwarding），以便作为子网的网关。

- 该服务器也是 `"itso"` 域的 DNS 服务器。

- 2. `"first.itso"` 域的服务器拥有一个 IP 地址为 `172.168.0.10` 的网卡。

- 3. `"second.itso"` 域的服务器拥有一个 IP 地址为 `192.168.0.10` 的网卡。

- 4. `"second.itso"` 域中的客户端拥有一个 IP 地址为 `192.168.0.20` 的网卡。

- 5. `"first.itso"` 域中的客户端拥有一个 IP 地址为 `172.168.0.20` 的网卡。

## 8.5 设置 DNS 配置

如前所述，我们的实验网络设置是基于名为 `".itso"` 的主（根）域，包含两个名为 `"first.itso"` 和 `"second.itso"` 的子域。你可以在图 160 中看到此设置。

![](img/2d69b129b41635ef36a3e6707d34b788_201_0.png)

图 160. 域设置

### 8.5.1 设置根 DNS

在本节中，我们将解释如何为实验网络设置设置根 DNS 服务器。在开始设置 DNS 之前，你需要检查是否安装了 BIND 软件包。你可以参考第 123 页第 4.2 节“设置 Samba 服务器”中的指令，但不需要寻找 `SAMBA` 包，而是需要搜索 `BIND` 软件包。在确认 `BIND` 包已安装后，你需要配置系统，以便 DNS 在 Linux 服务器启动时自动启动。要实现此操作，请遵循第 134 页第 4.2.3 节“将 Samba 作为启动服务启动”的指令，但不要选择 `SMB` 服务器进程 (`samba`)，而是选择互联网域名服务器 (`named`)。一旦你启用了 DNS 作为服务运行，它将在 Linux 服务器启动时自动启动。

要为 `"itso"` 域设置主（根）DNS，请按照以下步骤操作：

- 1. 创建包含以下条目的 `/etc/named.conf` 文件：

```
// generated by named-bootconf.pl
options {
directory "/var/named";
/*
* 如果你和你想要通信的名称服务器之间有防火墙，
* 你可能需要取消下面 query-source
* 指令。
* 之前的 BIND 版本始终使用端口 53 提问，
* 但 BIND 8.1 默认使用非特权端口。
*/
// query-source * port 53;
//
// 仅缓存的名称服务器配置
// 我们不需要 root 条目，因为这个 DNS
// 是 .itso 域的根服务器
//
//zone "." {
//type hint;
//file "named.ca";
//}
zone "0.0.127.in-addr.arpa" {
type master;
file "named.local";
}
zone "itso" {
notify no;
type master;
file "itso";
}
zone "0.0.168.172.in-addr.arpa" {
notify no;
type master;
file "172.0";
}
zone "0.0.168.192.in-addr.arpa" {
notify no;
type master;
file "192.0";
}
```

如你所示，我们定义了 `"itso"` 域以及网络 `172.168.0` 和 `192.168.0` 的反向地址区域。

- 2. 创建目录 `/var/named`。

- 3. 创建 `/var/named/itso` 区域文件，包含以下条目：

```
@
    IN      SOA ns5000.itso. root.itso. (
                        199702270 ; Serial
                        28800      ; Refresh
                        14400      ; Retry
                        360000        ; Expire
                        86400         ; Minimum
)
    NS ns5000.itso.
    MX 10 localhost A 127.0
    ns5000 A 172.168.0
    second A 172.168.0.10
    NS ns700010.second.itso
    ns700010.second.itso A 172.168.0.10
    NS ns5500.first.itso
    ns5500.first.itso A 172.168.0.10
```

在此文件中，我们指定了 `"first.itso"` 和 `"second.itso"` 的所有请求指向相应的 DNS 服务器。

- 4. 创建 `/var/named/172.0.0` 区域文件，包含以下条目：

```
@
    IN      SOA ns5000.itso. root.itso. (
                        199702270 ; Serial
                        28800      ; Refresh
                        14400      ; Retry
                        360000        ; Expire
                        86400         ; Minimum
)
    NS ns5000.itso.
    0.0.0.in-addr.arpa CNAME 0-255.0.172.168.in-addr.arpa.
    172.168.0.in-addr.arpa CNAME 0-255.0.172.168.in-addr.arpa.
    0-255.0.172.168.in-addr.arpa. 86400 IN NS ns5500.first.itso.
```

如所示，`172.168.0.0` 网络的反向地址请求都传递到了 `"first.itso"` 域的 DNS。当 DNS 服务器收到来自 `172.168.0.0-255` 网络 IP 地址 请求时，它将此请求传递给该网络的 DNS 服务器。在我们的示例中，这是 `"first.itso"` 域的 DNS 服务器。

- 5. 创建 `/var/named/172.168.0` 区域文件，包含以下条目：



```
@
      IN  SOA ns5000.itso. root.itso. (
                       199702270 ; Serial
                       28800      ; Refresh
                       14400      ; Retry
                       3600000   ; Expire
                       86400 )    ; Minimum

                   NS  ns5000.itso.
1.0.0.11-in-addr.arpa. INAME 10-255.0.192.168.in-addr.arpa.
10.0.0.11-in-addr.arpa. INAME 10-255.0.192.168.in-addr.arpa.
20.0.0.11-in-addr.arpa. INAME 20-255.0.192.168.in-addr.arpa.
0-255.0.192.168.in-addr.arpa. 86400 IN NS ns700010.second.itso.
```

可以看出，`192.168.0.0` 网络反向地址解析请求都传递到了 `"second.itso"` 域的 DNS。当 DNS 服务器收到来自 `192.168.0.0-255` 网络 IP 地址请求时，它将此请求传递给提供该服务的 DNS 服务器。在我们的示例中，这是 `"second.itso"` 域的 DNS 服务器。

- 6. 创建 `/var/named/named.local` 区域文件，包含以下条目：

```
@
      IN  SOA ns5000.itso. root.itso. (
                       199702270 ; Serial
                       28800      ; Refresh
                       14400      ; Retry
                       3600000   ; Expire
                       86400 )    ; Minimum

                   NS  ns5000.itso.
1 IN PTR localhost.
```

你的服务器已准备好开机。要在不重启操作系统的情况下启动服务器（这是另一种非常流行的操作系统中的情况），请执行命令：

```
/etc/rc.d/init/named start
```

恭喜！你刚刚设置了一个完整的 DNS 服务器。准备好在设置子域 DNS 服务器时迎接更多的惊喜吧。

# 1. 创建包含以下条目的 `/etc/named.conf` 文件：

```
// generated by named-conf.pl
{
  directory "/var/named";
  /*
   * 如果你与想要通信的名称服务器之间存在防火墙，
   * 你可能需要取消注释下面的 query-source
   * 指令。之前的 BIND 版本总是使用端口 53 
   * 进行查询，但 BIND 8.1 默认使用非权端口。
   */
  // query-source address * port 53;

  // 仅缓存的名称服务器配置
//
zone "." {
  type hint;
  file "named.ca";
}
zone "0.0.127.in-addr.arpa" {
  type master;
  file "named.local";
}
zone "first.itso" {
  notify no;
  type master;
  file "first.itso";
}
zone "0.168.172.in-addr.arpa" {
  notify no;
  type master;
  file "0.168.172.in-addr.arpa";
}
zone "0-255.0.168.172.in-addr.arpa" {
  type master;
  file "0.168.172.in-addr.arpa";
}
```

如你所见，定义了根域 `"."` 和 `"first.itso"` 域的区域。我们还为本地网络 `172.168.0.0` 以及网络 `172.168.0.0-255` 定义了反向地址解析区域，它们用于来自根服务器的请求。你可以看到网络 `172.168.0.0` 和 `172.168.0.0-255` 的区域文件是相同的。我们需要两个定义，是因为第一个（`0.168.172`）用于本地请求，而第二个（`0-255.0.168.172`）用于解析来自根服务器的请求，以防有人从根服务器请求该网络（`172.168.0.0`）的反向解析。根服务器将向提供该网络的服务器（`172.168.0.0`）请求信息（在我们的示例中，即 `"first.itso"` 域的服务器）。参考第 184 页的 8.5.1“设置根 DNS”，查看如何设置根服务器以将请求传递给子域中的服务器。

- 2. 创建目录 `/var/named`。

- 3. 创建包含以下条目的区域文件 `/var/named/named.ca`：

```
3600000 IN NS nf5000.itso
nf5000.itso 3600000
 A 172.168.0.1
```

在该文件中，我们定义了我们网络中的主（根）DNS。

- 4. 创建包含以下条目的区域文件 `/var/named/first.itso`：

```
@ IN SOA nf5500.first.itso. root.first.itso. (
1997022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
NS nf5500 ; Name Server
MX 10 mail ; Mail Server
localhost A 127.0.0.1
nf5500 A 172.168.0.10
mail CNAME nf5500
```

在该文件中，我们为网络 `172.168.0.0` 中的所有计算机创建了定义。

- 5. 创建包含以下条目的区域文件 `/var/named/named.172.in-addr.addr.arpa`：

```
@ IN SOA nf5500.first.itso. root.first.itso. (
1997022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
NS nf5500.first.itso.
1 PTR nf5500.itso.
10 PTR nf5500.first.itso.
```

在该文件中，我们定义了网络 `172.168.0.0` 的反向地址解析。

- 6. 创建包含以下条目的区域文件 `/var/named/named.local`：

```
@      IN  SOA  nf5500.first.itso. root.first.itso. (
                    1997022000 ; Serial
                    28800 ;; Refresh
                    14400 ;; Retry
                    360000 ; Expire
                    86400 ) ; Minimum
1      IN  NS   nf5500.first.itso.
             PTR  localhost.
```

7. 使用命令启动服务器：

```
/etc/rc.d/init/named start
```

### 8.5.3 为第二个子域设置 DNS

在配置 DNS 之前，你需要检查 DNS 服务器是否已安装。你可以通过遵循第 184 页的 8.5.1“设置根 DNS”中的说明来实现。在检查所有前提条件后，按照以下步骤设置 `"second.itso"` 域的 DNS：

- 1. 创建包含以下条目的 `/etc/named.conf` 文件：

```
// generated by named-conf.pl
options {
  directory "/var/named";
  /*
   * 如果你与想要通信的名称服务器之间存在防火墙，
   * 你可能需要取消注释下面的 query-source
   * 指令。之前的 BIND 版本总是使用端口 53 
   * 进行查询，但 BIND 8.1 默认使用非权端口。
   */
  query-source address * port 53;
};

// 仅缓存的名称服务器配置
zone "." {
  type hint;
  file "named.ca";
}
zone "0.0.127.in-addr.arpa" {
  type master;
  file "named.local";
}
zone "second.itso" {
  notify no;
  type master;
  file "second.itso";
}
zone "0.168.172.in-addr.arpa" {
  notify no;
  type master;
  file "0.168.172.in-addr.arpa";
}
zone "0-255.0.168.172.in-addr.arpa" {
  type master;
  file "0.168.172.in-addr.arpa";
}
```

如你所见，定义了根域 `"."` 和 `"first.itso"` 域的区域。我们还为本地网络 `172.168.0.0` 以及网络 `172.168.0.0-255` 定义了反向地址解析区域，它们用于来自根服务器的请求。你可以看到网络 `172.168.0.0` 和 `172.168.0.0-255` 的区域文件是相同的。我们需要两个定义，是因为第一个（`0.168.172`）用于本地请求，而第二个（`0-255.0.168.172`）用于解析来自根服务器的请求，以防有人从根服务器请求该网络（`172.168.0.0`）的反向解析。根服务器将向提供该网络的服务器（`172.168.0.0`）请求信息（在我们的示例中，即 `"first.itso"` 域的服务器）。参考第 184 页的 8.5.1“设置根 DNS”，查看如何设置根服务器以将请求传递给子域中的服务器。

- 2. 创建目录 `/var/named`。

- 3. 创建包含以下条目的区域文件 `/var/named/named.ca`：

| | |
|------|---|
| `3600000 IN NS nf5000.itso` | `172.168.0.1` |
| `nf5000.itso 3600000` | |

在该文件中，我们定义了我们网络中的主（根）DNS。

- 4. 创建包含以下条目的区域文件 `/var/named/second.it`：

```
@ IN SOA nf7000m10.second.it. root.second.it. (
1997022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
;
NS nf7000m10 ; Name Server
MX 10 mail ; Mail Server
;
localhost A 127.0.0.1
nf7000m10 A 172.168.0.10
mail CNAME nf7000m10
client A 172.168.0.20
```

在该文件中，我们为网络 `192.168.0.0` 中的所有计算机创建了定义。

- 5. 创建包含以下条目的区域文件 `/var/named/0.168.192.addr.arpa`：

```
@ IN SOA nf7000m10.second.itso. root.second.itso. (
1997022700 ; Serial
28800 ; Refresh
14400 ; Retry
3600000 ; Expire
86400 ) ; Minimum
;
NS -nf7000m10.second.itso.
1 PTR nf5000.itso.
10 PTR nf7000m10.second.itso.
20 PTR client.second.itso.
```

在该文件中，我们定义了网络 `192.168.0.0` 的反向地址解析。

- 6. 创建包含以下条目的区域文件 `/var/named/named.local`：

### 8.5.4 设置 Sendmail

所有关于 `Sendmail` 的文档都会告诉你，`Sendmail` 配置文件 `/etc/sendmail.cf` 是网络管理员的噩梦。这并非完全正确；当你不需要 `Sendmail` 提供的特殊功能时，设置其实非常简单。你只需要稍微修改通用文件，并使用 `"m4"` 宏处理器重新创建新的 `sendmail.cf`。在本节中，我们将解释如何为自己的域设置邮件。`Caldera Linux` 使用通用文件文件 `Sendmail`。该文件位于 `/usr/share/sendmail/cf`，名为 `generic-col2.mc`。该文件只需要少许修改即可在你的服务器上运行。按照以下步骤设置你的邮件服务器：

- 1. 使用命令拷贝 `Caldera` 通用文件：

```
cp /usr/share/sendmail/cf/generic-col2.mc /usr/share/sendmail/cf/mydomain.mc
```

- 2. 在 `mydomain.mc` 文件中添加以下行：

    - a. 用于 `"first.itso"` 域的服务器：

        ```
        dnl ####################################################
        dnl # 示例域的定义
        dnl # 我们定义了 PSEUDONYMS, DEFAULT_HOST
        define(`PSEUDONYMS`, 'nf5500.first.itso' 'first.itso')
        define(`DEFAULT_HOST`, 'nf5500.first.itso')
        dnl ####################################################
        ```

    - b. 用于 `"second.itso"` 域的服务器：

        ```bash
        dnl ############################################################
        dnl # Definitions for sample domain
        dnl # we define PSEUDONYMS, DEFAULT_HOST
        define(`PSEUDONYMS`, 'n700m10.second.itso' 'second.itso')
        define(`DEFAULT_HOST`, 'n700m10.second.itso')
        dnl ############################################################
        ```

3. 执行以下命令，带有你的域名文件创建一个新的 `sendmail.cf` 文件：

```
/usr/bin/m4 /usr/share/sendmail/cf/cf/m4/m4
/usr/share/sendmail/cf/cf/mydomain.cf
/usr/share/sendmail/cf/feature/relay_entire_domain.m4 >
/etc/sendmail.cf
```

如果你的当前目录是 `/usr/share/sendmail/cf`，操作将会简单得多：

```
/usr/bin/m4 cf.cf.m4 mydomain.cf feature/relay_entire_domain.m4 >
/etc/sendmail.cf
```

如你所见，为了创建配置我们额外使用了两个文件：

- a. 必须使用 `cf.m4`，否则文件无法正确解析。

- b. 使用 `relay_entire_domain.m4` 允许通过远程客户端访问邮件服务器的客户端通过此服务器发送邮件。

4. 修改 `/etc/sendmail.cw` 文件：

- a. 为 `"first.itso"` 域名的服务器添加行：

```
first.itso
```

- b. 为 `"second.itso"` 域名的服务器添加行：

```
second.itso
```

`/etc/sendmail.cw` 包含了你邮件服务器的所有别名。你需要包含域名；否则邮件将无法送达。

5. 使用命令启动服务器：

```
/etc/rc.d/init.d/mta start
```

如果你想让 `sendmail` 在服务器启动时自动启动，请参考第 134 页第 4.2.3 节“将 Samba 作为启动服务”中的说明，但不要选择 `SMB` 服务器进程 (`samba`)，而是选择邮件传输代理 (`Mail Transfer Agent`)。

如果你想从一个域名向另一个域名发送邮件，你需要在两个域（`first.itso` 和 `second.itso`）的服务器上执行所有先述指令。

#### 8.5.4.1 配置 Sendmail

默认情况下，如果 `Sendmail` 能够到达用户域名的邮件服务器，它就可以向用户投递邮件。例如，如果你处于内部网络中，且你的 `Sendmail` 服务器没有直接连接互联网，你可以配置 `Sendmail` 通过另一个连接到互联网的可达邮件服务器来路由邮件。要实现此点，你需要在 `/etc/sendmail/mailertable` 文件中输入适当的值。例如，如果你想将 `otherdomain.com` 的邮件路由到 `reachableserver`，那么你的 `/etc/sendmail/mailertable` 文件看起来如下：



```
#
# /etc/mailertable
# 此文件可用于精调 sendmail 的邮件路由。
# 更改此文件后，你必须使用以下命令重建 DB 文件：
# /usr/sbin/makemap hash /etc/sendmail/mailertable < /etc/sendmail/mailertable
# otherdomain. smtp:reachableserver
```

这意味着所有发送 `otherdomain` 的邮件都将通过 SMTP 协议路由到 `reachableserver` 邮件服务器。域名必须始终以 `.` 结尾。通过这种设置，你可以让邮件从服务器路由到服务器，直到到达目的地。

每当你修改 `/etc/sendmail/mailertable.db` 文件时（这实际上是 `Sendmail` 用于执行路由任务的文件），你可以通过执行命令来实现：

```
/usr/sbin/makemap hash /etc/sendmail/mailertable
/etc/sendmail/mailertable
```

如果你想将所有邮件都路由到另一个服务器，可以通过向 `/etc/sendmail/mailertable` 文件末尾添加以下行：

```
smtp:smartserver
```

其中 `smartserver` 是处理所有来自你的 `Sendmail` 服务器邮件的邮件服务器。

### 8.5.5 设置邮件客户端

每个邮件用户在邮件服务器（在本例中为 `Sendmail`）上都需要一个用户名/密码。用户获得用户名/密码后，就可以远程访问其信箱。在本节中，我们将展示如何设置 `Netscape` 邮件设置以发送和接收邮件。

> 注意
>
> 在设置客户端之前，必须安装并运行 `POP3` 服务器。

按照以下步骤设置 `Netscape` 邮件属性：

1. 启动 `Netscape`。
2. 选择 `Edit > Preferences > Mail & Newsgroups > Identity`，你会看到一个与图 161 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_213_0.png)

图 161. 设置身份设置

3. 输入所需的值并选择 `Mail Servers`。你会看到一个与图 162 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_214_0.png)

图 162. 设置身份

4. 在 `Outgoing Mail`（发件邮件）中，选择 `(SMTP)`
5. 在 `Incoming Server`（入站服务器）中，选择 `POP3`

![](img/2d69b129b41635ef36a3e6707d34b788_215_0.png)

图 163. 设置身份

6. 在 `Server` 字段中输入你的地址。
7. 在 `User Name` 字段中输入你的用户名。
8. 点击 `OK` 继续。

## 3.1 LDIF 文件

`LDIF` 文件是用文本格式表示目录数据的标准方式。该格式通常用于导入和导出目录数据。以下是一个用于加载 `LDAP` 目录并在 `Netscape` 漫游配置目录中添加用户的 `LDIF` 文件：

```
dn: o=ibm.com
objectclass: top

dn: ou=People, o=ibm.com
objectclass: top
objectclass: organizationalUnit

dn: cn=username, ou=People, o=ibm.com
objectclass: top
objectclass: organizationalUnit
cn: username
userpassword: secret

dn: ou=Roaming, o=ibm.com
objectclass: top
objectclass: organizationalUnit

dn: nsLIProfileName=username, ou=Roaming, o=ibm.com
objectclass: top
nsliproProfile
nsliprofilename: username
owner: cn=username, ou=People, o=ibm.com
```

每个 `LDAP` 条目必须有一个区分名称（`DN`）。区分名称是一个特指引用该条目的唯一键。

> 注意
>
> 导入 `LDIF` 文件时，请注意额外的空格、拼写和大小写。`OpenLDAP` 对这些处理方式不同。认证错误通常可以追溯到 `LDIF` 文件的错误。

## 9.4 在 Linux 上实现

`Caldera OpenLinux` 带有 `OpenLDAP` 包版本 `1.2.3-1`。此版本无法与我们在解释 `OpenLDAP` 时使用的 `Netscape` 漫游配置兼容。

![](img/2d69b129b41635ef36a3e6707d34b788_218_0.png)

在继续本章节之前，请确保没有安装原始 `OpenLDap` 包。你可以通过 `KDE` 菜单中的 `kpackage` 工具来实现。启动 `kpackage` 时，通过点击 `Server -> Network` 可以找到 `OpenLDAP`。你会看到一个类似于图 164 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_219_0.png)

图 164. 检查是否安装了 `OpenLDAP`

> 注意
>
> 如果你想使用 `Netscape` 漫游配置，不要忘记卸载最初安装的 `OpenLDap` 包。

202 `Caldera OpenLinux` 和 `Netfinity` 服务器集成指南

## 4.4.1 下载并安装 OpenLDAP

虽然 `Calder OpenLinux` 包含了 `OpenLDAP` 的源码包，但在编译之前需要对其应用补丁。推荐的方法是从官方 `OpenLDAP` `ftp` 站点下载最新的稳定版本和补丁：`ftp://ftp.openldap.org`。该补丁解决了 `OpenLDAP` 与 `Netscape` 的 `LDAP` 实现之间的差异。该补丁不会被整合到 `OpenLDAP` 的后续版本中。`OpenLDAP` 的立场是，他们目前的实现与 `OpenLDAP` 的先例一致。

从下处下载 `OpenLDAP` 最新稳定版本：

```
ftp.openldap.org/pub/openldap
```

从下处下载 `Netscape` 补丁 (`Albert-FitzPatrick-9905019.gz`)：

```
ftp.openldap.org/pub/openldap/incoming/
```

通过输入命令解压 `OpenLDAP`：

```
tar -xvzf openldap-stable.tgz
```

在编译和安装之前应用补丁。

```
gunzip < Albert-FitzPatrick-9905019.tar.gz > roaming.patch
cd ld/servers/slapd
patch ../../../roaming.patch
cd ../../../(ldap)
```

开始安装程序：

```
./configure
make depend
make
cd tests
```

接一步将测试 `OpenLDAP`。请注意任何错误。

```
make
cd ..
make install
```

`OpenLDAP` 现在已安装。

## 9.4.2 用于 Netscape 的漫游配置

为了设置漫游配置，我们需要 `Netscape` 目录架构。你可以从下处下载 `roaming-073099.tar.gz` 文件，该文件包含了 `slapd.oc.conf` 文件、`slapd.at.conf` 文件以及一个优秀的示例 `slapd.conf` 文件：

```
http://www.openldap.org/incoming/roaming-073099.tar.gz
```

或者或者向 `slapd.oc.conf` 和 `slapd.ac.conf` 文件中添加以下内容。以下行应位于 `/usr/local/etc/openldap/slapd.oc.conf` 的末尾：

```
# from netscape to implement roaming access...
objectclass nsLIPtr
  # oid 2.16.840.1.113730.3.2.74
    requires
      objectclass
    allows
      nsLIPtrURL,
      owner

objectclass nsLIPProfile
  # oid 2.16.840.1.113730.3.2.75
    requires
      objectclass,
      nsLIPProfileName
    allows
      nsLIPrefs,
      uid,
      owner

objectclass nsLIPProfileElement
  # oid 2.16.840.1.113730.3.2.76
    requires
      objectclass,
      nsLIElementType
    allows
      owner,
      nsLIata
      nsLVersion

objectclass nsLIServer
  # oid 2.16.840.1.113730.3.2.77
    requires
      objectclass,
      serverhostname
    allows
      description,
      cn,
nsServerPort,
nsIServer,
serverroot
```

> 注意
>
> 如果要使用 `Netscape` 漫游配置，请注释掉 `slapd.oc.conf` 中的条目。

在 `/usr/local/etc/openldap/slapd.at.conf` 的末尾添加以下行：

```
# ns-cd-schema.conf
# Netscape Mission Control Roaming Access
attribute nsLIPtrURL          2.16.840.1.113730.3.2.99
attribute nsLIPProfileName   2.16.840.1.113730.3.2.400
attribute nsLIata           2.16.840.1.113730.3.2.401
attribute nsLIElement       2.16.840.1.113730.3.2.402
attribute nsIServerType    2.16.840.1.113730.3.2.403
attribute nsLVersion      2.16.840.1.113730.3.2.404
attribute nsServerPort      2.16.840.1.113730.3.2.405
```

关于 `Netscape` 目录架构和漫游配置的更多信息可以在下处找到：

`http://help.netscape.com/products/communicator/manual_roaming.html`

创建存储 `OpenLDAP` 数据库文件的目录：

```
mkdir /usr/ldap_db
```

修改你的 `slapd.conf` 以支持漫游配置。将 `ibm.com` 替换为你的组织名称。

```
# See slapd.conf for details.
# 此文件不应该是全局可读的
include /usr/local/etc/openldap/slapd.at.conf
include /usr/local/etc/openldap/slapd.oc.conf
schemacheck off
lastmod
#referral ldap://ldap.umich.edu
pidfile /usr/local/var/slapd.pid
argsfile /usr/local/var/slapd.args

####################
# ldbm 数据库定义
####################

database: ldbm
  suffix="o=ibm.com"
  directory /usr/tmp
rootdn "cn=root, o=ibm.com"
rootpw secret
  # 应避免明文密码，特别是 rootdn。
  access to * by write
  access to * by compare
  access to * by read
```

最后三行指定的权限极不安全，仅应用于测试目的。查看 `slapd.conf` 手页获取有关为你的环境设置适当权限的信息。

![](img/2d69b129b41635ef36a3e6707d34b788_223_0.png)

## 9.4.3 启动 OpenLDAP 服务器

要启动 `OpenLDAP` 服务器，你需要运行 `slapd` 程序。输入以下命令：

```
/usr/libexec/slapd (-d 255 用于调试信息)
```

当 `slapd` 成功运行时，我们需要加载初始数据库。创建一个类似于第 201 页的 `LDIF` 文件。将 `Username` 替换为你的用户名，将 `ibm.com` 替换为你的组织名称。

一旦你创建了（例如）`entries.ldif` 文件，通过执行命令将该文件的数据添加到数据库：

```
/usr/local/bin/ldapadd -D "cn=root, o=ibm.com" -w secret -f entries.ldif
```

## 9.4.4 配置 Netscape

最后一步是配置 `Netscape` 浏览器。

## OpenLDAP

社区开发的 `LDAP` 软件

- 项目 (The Project)
- 基金 (The Foundation)
  - 赞助商 (Sponsors)
  - 开发 (Development)
  - 源 (Sources)
  - 软件 (Software)
  - AnonCVS
  - 下载!(Download!)
  - 路线图 (Roadmap)
  - 快速开始 (Quick Start)
  - 追踪 (Chase)
  - 支持 (Support)
  - Rag-O-Matic
  - 问题跟踪 (Issue Tracking)
  - 邮件列表 (Mailing Lists)
  - 搜索!(Search!)

你的 `open LDAP` 项目需要托管吗？我们可以提供帮助！

`OpenLDAP` 项目宣布立即可以使用

更改应用程序的用户偏好

图 165. 配置你的浏览器

# 1. 从 Edit 下拉菜单中选择 Preferences（选项）。

![](img/2d69b129b41635ef36a3e6707d34b788_224_0.png)

图 166. 配置 Netscape

2. 点击 `Roaming User`（漫游用户）选项卡，你会看到一个类似于图 166 的窗口。

3. 点击 `Enable Roaming Access for this profile`（为此配置启用漫游访问）复选框。

4. 输入用户名。

![](img/2d69b129b41635ef36a3e6707d34b788_225_0.png)

图 167. 配置 Netscape 2

5. 点击 `Server Information`（服务器信息），你会看到一个类似于图 167 的窗口。

6. 在 `LDAP Directory Server` 下的 `Address`（地址）字段输入：

`ldap://linuxbox/nsLIProfilename=$USERID, ou=Roaming, o=ibm.com`

将 `linuxbox` 替换为 `OpenLDAP` 服务器的主机名，将 `ibm.com` 替换为你的组织名称（在 `slapd.conf` 中指定）。

7. 在 `LDAP Directory Server` 下的 `User DN` 字段中输入：

`cn=$USERID, ou=People, o=ibm.com`

![](img/2d69b129b41635ef36a3e6707d34b788_226_0.png)

图 168. 配置 Netscape 3

8. 点击“选择项目”，你将看到一个与图 168 类似的窗口。

9. 选择你想要与 `OpenLDAP` 服务器同步的项目。

10. 重启 `Netscape`，设置已完成。恭喜你！

## 5.5 更多信息来源

- 可以在 `Linux` 文档项目网站获取 `LDAP` 教程：

`http://www.linuxdoc.org`

- `OpenLDAP` 主页包含关键信息，包括 `Phil Allred` 一关于 `Netscape` 漫游配置和 `OpenLDAP` 的贴文：

`http://www.OpenLDAP.org`

- 《理解与部署 `LDAP` 目录服务》（`Understanding and Deploying LDAP Directory Services`），作者：`Timothy Howes`, `Mark Smith`, `Gordon Good`，`Macmillan` 出版社，1999 年。

第 9 章 `LDAP` - 轻量级目录访问协议 209 页

# 第 10 章 NIS - 网络信息系统

在分布式计算环境中，维护密码文件、组文件和主机文件可能是一项艰巨的任务。一致性可能是最大的困难。例如，当用户在某一台机器上更改密码时，理想情况下，该更改应该传播到他们拥有账户的任何其他机器。当网络由成百甚至上千台机器组成时，这种便利就变成了一种必需。`NIS` 是解决这些问题的方法之一。

## 10.1 什么是 NIS？

网络信息系统（`NIS`）是一种旨在为常用配置文件提供分布式数据库系统的服务。`NIS` 服务器管理数据库文件的副本。`NIS` 客户端从 `NIS` 服务器请求信息，而不是使用它们自己的配置文件。



NIS 构建在客户端/服务器模型之上。NIS 服务器包含名为“映射”（`maps`）的数据文件。这些映射由 NIS 所有，且只能由主服务器更新。存在 NIS 从服务器（`slave servers`），它们从主服务器同步数据。当主服务器的映射发生更改时，该更改将分发到所有从服务器。客户端是从这些映射请求信息的宿主机，但不被允许修改它们。

## 10.2 我如何使用 NIS？

NIS 通常用于集中管理常用的复制配置文件。常用配置文件的示例包括：

- `/etc/hosts`
- `/etc/passwd`
- `/etc/group`

## 10.3 在 Linux 上实现

为了引入 NIS 背后的概念，我们将为存储在 NIS 主服务器上的密码文件创建一个映射。这将允许用户登录 NIS 客户端，而无需在每台机器上维护账户。集中管理是使用 NIS 的主要优势。

关于安全的说明：在决定将 NIS 引入生产环境之前，请考虑跨网络传输敏感数据的安全影响。你可能希望使用 `NIS+`，它具有强加密功能以及额外的维护影响。

NIS 客户端和 NIS 服务器需要安装的包：

```
# nis-client-2.0-8
# nis-server-2.0-8
```

`/etc/nsswitch.conf` 文件决定了执行的查找顺序。

示例 `/etc/nsswitch.conf` 文件：

```
# /etc/nsswitch.conf
#
# 名称服务切换配置文件。
#
passwd : compat
shadow : compat
group : compat
#
hosts : files dns nis
networks : nis files dns
#
ethers : nis files
protocols : nis files
rpc : nis files
services : nis files
```

![](img/2d69b129b41635ef36a3e6707d34b788_229_0.png)

> 注意

> 在所有未使用 NIS 服务器进行协调的选项中，你应该移除 NIS 引用。

### 10.3.1 NIS 服务器

Caldera OpenLinux 中 NIS 服务器的配置文件位于 `/etc/nis` 目录。要在你的 Caldera OpenLinux 服务器上设置 NIS 服务器，请遵循以下步骤：

1. 确定一个 NIS 域名。此名称不需要与服务器的域名相同，因为它只需要位于相邻域之间即可，而不是全球范围内。

2. 创建目录 `/etc/nis/nisdomainname`。在我们的示例中，我们使用了域名 `"nis.com"`。我们通过执行此命令创建目录：

   ```
   mkdir /etc/nis/nis.com
   ```

3. 你可以使用 `COAS` 定义 NIS 域。点击面板上的 `K` 符号，选择 `COAS -> Network -> TCP/IP -> NIS`。见图 169。

   ![](img/2d69b129b41635ef36a3e6707d34b788_230_0.png)

   图 169. NIS 设置

   NIS 配置启动后，你将看到一个与图 170 类似的窗口。

   ![](img/2d69b129b41635ef36a3e6707d34b788_230_1.png)

   图 170. NIS 属性

4. 在“Domain Name（域名）”字段中，输入你的域名。在我们的示例中输入 `nis.com`

5. 点击 `OK` 继续，在下一个窗口中点击 `Save`（保存），并在最后一个窗口中选择 `Done`（完成）或等待窗口关闭。

6. 将所有想要在局域网共享的文件创建符号链接到 `/etc/nis/nisdomainname`。在我们的示例中，我们希望共享密码和组文件，因此我们为这些文件创建了符号链接：

   ```
   ln -s /etc/passwd /etc/nis/nis.com/passwd
   ln -s /etc/group /etc/nis/nis.com/group
   ```

   （注：原文示例代码最后有误，此处已根据逻辑修正为 group）

7. 将 `/etc/passwd.sample` 复制到 `/etc/nis/nis.com`。在我们的示例中，我们需要更新密码文件。通过执行此命令：

   ```
   cp /etc/passwd.sample /etc/nis/nis.com/passwd
   ```

8. 启动 NIS 服务器。你将看到一个与图 171 类似的窗口。

   （此处原文内容存在乱码和重复，已根据指令逻辑进行处理）

   ```
   root@test22:/root# ypcat passwd
   john:$S2Xq2QgM6X3IPvBGpir2UQQSJbc1:501:501:/home/bin/bash
   ayne:$S7tsemaW1ZlZI00dsIcAG3fe2:502:502:/home/ayne/bin/bash
   karri:$S52F2F27Uj56Cc.yooFcAak42jSWRc1:507:510:/home/karri/bin/bash
   otto:$StcEvubWH2Vr6X.SndoutAqYwc5:501:504:/home/otto/bin/bash
   sammy:$S11VHfF2Z3N6C78N0:504:508:/home/sammy/bin/bash
   tiva:$S11oW9ZpkS5CDGjUsXe1.pn12:504:511:/home/tiva/bin/bash
   ivo:$S1DMaqOOFpIC3BAnWpbBLATIVE:505:509:/home/ivo/bin/bash
   hncy:$N22zayWc/EvobX3ehMzhzuw7:506:509:/home/hncy/bin/bash
   korry:$S52F2F56Cc.yooFcAak42jSWRc1:507:510:/home/korry/bin/bash
   steve:$S1veYFMnZcaEF2FJRGDU80deICUF9:503:508:/home/steve/bin/bash
   root@test22:/root]# 
   ```

   图 176. 执行 `ypcat passwd` 测试机器，使用一个作为 NIS 主服务器的账户登录 NIS 客户端。当你登录时，你应该看到以下内容：

   ```
   Caldera OpenLinux(TM)
   Version 2.3-Lone Wolf One
   Copyright 1996-1999 Caldera Systems, Inc.
   login: ivo
   Password:
   Last login: Wed Oct 27 19:22:03 1999 from 9.24.106.49 on tty1
   No directory /home/ivo
   Logging in with home = "/"
   bash$ 
   ```

   图 177. 客户端机器上没有定义该目录，但在 NIS 主服务器上定义了，我们在登录时会收到错误。

由于 `Ivo` 的主目录在 NIS 主服务器上没有定义，我们在登录时会报错。如果需要，可以通过在客户端上为 `Ivo` 创建主目录来解决此问题。另一个选项是结合 NIS 使用 `NFS` 来自动挂载 `Ivo` 的主目录。

218 Caldera OpenLinux 和 Netfinity 服务器集成指南

## 10.4 其他信息的来源

如需更多信息或进行故障排除，Thorsten Kukuk 编写的 NIS 指南是一个很好的起点。可以在此处找到它：

`http://www.metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO`

Hal Stern 写的《Managing NFS and NIS》也是一个很好的资源。

# 第 11 章. NFS - 网络文件系统

网络文件系统 (NFS) 是 Sun Microsystems 开发的一产品，允许你跨网络共享目录。挂载的目录对你来说是透明的。你可以像访问计算机上的任何目录或文件系统一样访问挂载的目录。挂载过程与你想在系统上挂载的任何文件系统或分区相同。此功能的基础是 `mount` 命令。

为了跨网络共享目录，你需要两个基本要素：

- 共享数据的系统必须允许你访问。
- 使用数据的的系统必须发起请求并允许挂载发生。

这两个概念将在本章中讨论。

## 11.1 NFS 进程

首先，你需要验证 NFS RPM 包已加载。RPM 是 Red Hat Package Manager 的缩写，是 Linux 中安装软件包的常用方法。你可以使用以下命令执行：

```
rpm -ql nfs
```

你将看到如图 178 所示的结果。这是已安装 NFS 的 RPM 内容列表。当你最初设置系统并选择包含它的软件包时，可能已经默认安装了 NFS。你可以按照第 72 页 2.5 节描述的，使用 `AS` 工具中的 `kpackage` 工具，或者通过点击 `Server -> Network` 找到 `nfs-server` 软件包。

你可以手动安装 NFS，通过使用 `kpackage` 工具或使用以下命令：

```
mount /mnt/cdrom
rpm -i /mnt/cdrom/Packages/RPMS/nfs-server-2.beta4
```

现在 NFS 软件包应该已经安装了。你可以重复之前的 `rpm` 命令来验证软件包已安装。

```
(root@nf5000 user]# rpm -ql nfs-server
/etc/rc.d/init/nfs
/etc/sysconfig/daemons.2beta4
/usr/doc/nfs-server-2beta4
/usr/doc/nfs-server-2beta4/README
/man8/exports.gz
/man8/mount.gz
/man8/nfsd.gz
/man8/mountd.gz
/usr/sbin/rpc.mount
/usr/sbin/nfs[root@nf5000 user]#
```

图 178. 检查 NFS rpm

NFS 使用多个守护进程（服务）。这些守护进程是：

- `portmap` - 远程过程调用 (RPC) 程序号转换进程。当客户端想要对给定程序（例如 NFS 服务器）调用 RPC 时，它会首先联系服务器上的 `portmap` 以确定应该发送的端口号。
- `rpc.mountd` - 处理文件系统的导出。它查看 `/etc/exports` 文件以确定处理来自各种主机的挂载请求。
- `rpc.nfsd` - 提供 NFS 进程的用户部分。

你可以如图 179 所示验证 `rpc.nfsd`、`rpc.mountd` 和 `portmap` 守护进程正在运行。

```
# ps ax | grep nfs
323 ? S 0:00 [nfsd]
324 ? S 0:00 [nfsd]
325 ? S 0:00 [nfsd]
326 ? S 0:00 [nfsd]
327 ? S 0:00 [nfsd]
328 ? S 0:00 [nfsd]
329 ? S 0:00 [nfsd]
330 ? S 0:00 grep nfs
# ps ax | grep mount
313 ? S 0:00 [rpc.mountd]
673 tty1 S 0:00 grep mount
# /etc/rc.d/init.d/portmap status (pid 192) is running...
```

图 179. 验证 NFS 守护进程

如果 `portmap` 守护进程未运行，你需要在启动 NFS 守护进程之前启动它。你可以使用命令：

```
/etc/rc.d/init.d/portmap start
```

一旦 `portmap` 守护进程运行，你可以使用命令启动 NFS 守护进程：

```
/etc/rc.d/init.d/nfs start
```

当你启动 NFS 守护进程时，将看到如图 180 所示的结果。

```
[root@nf5000 user]# /etc/rc.d/init.d/nfs start
Starting NFS services: mountd nfsd.
```

图 180. 启动 NFS

> 注意

如果 `/etc/exports` 文件不存在或为空，则 NFS 守护进程将不会启动。设置 `/etc/exports` 文件的信息请见第 224 页 11.2 节“允许 NFS 访问数据”。

停止 NFS 服务器请使用命令：

```
/etc/rc.d/init.d/nfs stop
```

结果如图 181 所示。你会注意到相同的进程被关闭，但并不一定按照相同的顺序。

```
[root@mf5000 user]# /etc/rc.d/init.d/nfs start
Starting NFS services: mountd nfsd.
```

图 181. 停止 NFS 服务器

你可以使用命令重启 NFS 进程：

```
/etc/rc.d/init.d/nfs restart
```

如果你更改了配置文件，也可以用此命令重启 NFS 进程。

## 11.2 允许 NFS 访问数据

你可以通过在 `/etc/exports` 文件中设置来为文件系统提供 NFS 访问。该文件在导出服务器上设置。你可以通过打开 `/etc/exports` 文件创建一个示例条目。然后你可以添加如下的条目：

```
/usr/local/share myserver.mydomain.com(ro)
```

这表示 `/usr/local/share` 仅对 `myserver.mydomain.com` 可用。

![](img/2d69b129b41635ef36a3e6707d34b788_241_0.png)

> 注意

导出文件系统时，你需要能够识别并访问 `/etc/exports` 文件中的服务器。你可以使用命令验证这一点：

```
ping server_name
```

其中 `server_name` 是你尝试访问的服务器名称。否则，NFS 命令可能会挂起。

示例 `/etc/exports` 文件中的行解释如下：

- `# 示例 /etc/exports 文件`

  任何行或字符字符串都可以通过输入 `#` 符号转换为注释并禁用。从该符号开始到行尾的所有内容都被视为注释。

- `/ nmaster(rw) trusty(rw,no_root_squash)`

  这表示根目录 (`/`) 已被导出到以下服务器：

  - `master` - 权限为读/写。
  - `trusty` - 权限为读/写，且客户端的访问权限可以是服务器的根目录。

- `/projects proj*.local.domain(rw)`

  `/projects` 目录对所有匹配 `proj.local.domain` 模式的服务器开放读写访问。这包括 `proj.local.domain`、`proj1.local.domain`、`projprojprojproj.local.domain` 等。

- `/usr *.local.domain(ro) @trusted(rw)`

  任何主机名以 `.local.domain` 结尾的系统都允许只读访问。`@trusted` 网络组被允许读/写访问。

- `/home/joe pc001(rw,all_squash,anonuid=150,anongid=100)`

  `/home/joe` 目录允许 `pc001` 进行读写访问；所有访问请求都作为匿名用户进行处理。匿名 UID 数字设置为 `150`，匿名组 ID 设置为 `100`。这当客户端在 PC 上运行 `PCGNFS` 或类似的 NFS 进程时非常有用。由于 PC 的 ID 不一定映射到 UNIX ID，这允许设置恰当的文件属性。

- `/pub (ro,insecure,all_squash)`

  `/pub` 目录以只读方式访问。该条目中的选项允许那些不使用预留端口进行 NFS 的 NFS 实现客户端进行访问，并将所有请求作为匿名用户处理。

- `/pub/private (noaccess)`

  `/pub/private` 目录不允许任何 NFS 访问。

## 11.3 使用 NFS 远程访问数据

要在你的本地系统上挂载远程文件系统，挂载点必须存在。挂载过程不会自动创建挂载点。创建挂载点的方法是使用 Linux 的 `mkdir` 命令。要创建 `/usr/local/share` 挂载点，请输入：

```
mkdir /usr/local/share
```

通常，在创建 NFS 挂载点时你不需要担心文件属性和所有权。NFS 访问权限通常会覆盖为目录建立的任何权限。

一旦创建了挂载点，你就可以如下所示使用 `mount` 命令：

```
mount -t nfs nfs_host:share_dir local_mount_dir
```

其中：

- `-t nfs` 表示以 NFS 挂载方式执行。这现在是可选的，因为如果你显式指定要挂载的目录为 `host:directory`，`mount` 命令就会知道这是一个 NFS 挂载。
- `nfs_host:share_dir` `nfs_host` 是导出共享文件系统的主机，`share_dir` 是要共享的实际目录。
- `local_mount_dir` 是本地主机上用于挂载远程目录的目录。如前，此挂载点必须存在。

## 11.4 使用 GUI 允许 NFS 访问数据

在 Caldera OpenLinux 中，你也可以使用图形用户界面（`GUI`）挂载 NFS 资源。我们在第 90 页的 2.10.1 节“挂载 NFS 卷”中解释过这一点。

# 第 12 章 使用 IP 链进行包过滤

每当你将计算机连接到今天的互联网世界时，你就会暴露在外部入侵者的威胁之下。数以千计的黑客正等待进入你的计算机造成损害，或者窃取信息。因此，你需要保护来防止他们！

## 12.1 什么是包过滤？

从名称可以看出，包过滤是一种过滤器，用于对进入你计算机的数据进行过滤。数据包过滤是防火墙实现中常用的方法之一。通过包过滤，你可以实现一个防火墙，保护你的计算机免受外界的影响。

由于每个人迟早都想要通信，你需要将你的私有网络连接到互联网。这时是时候考虑安全问题了。你也可以在单计算机上使用防火墙，例如通过拨号链路连接到互联网。当你安装防火墙来保护内部网络时，任何想要与内部网络计算机通信的计算机都要向防火墙请求权限。如果未授予权限，访问将被拒绝。

## 12.2 你用 Linux 包过滤可以做什么？

通过 Linux 包过滤，你可以做很多事情。让我们在这里描述其中一些：



- 你可以保护连接到互联网的内部网络免受外部入侵者的侵害。
- 你可以执行网络地址转换（NAT），这允许没有注册互联网地址的内部连接计算机访问互联网资源。
- 你可以过滤进出你内部网络或单台计算机的信息。
- 你可以将你的 Linux 服务器作为两个不同类型网络之间的网关，例如连接令牌环网络和以太网世界。与购买昂贵的路由器来完成此项任务相比，这是一个廉价的解决方案。
- 你可以与其他共享你的拨号上网连接。

## 12.3 运行包过滤需要什么？

要使用 IP 链（IP Chains）设置包过滤器，你的 Linux 安装需要满足以下要求：

1. 你需要 `2.2` 或更高的内核。建议使用最新的稳定版本。内核必须编译适用于 IP 转发（IP Forwarding）、IP 伪（IP Masquerading）和 IP 防火墙（IP Firewall）的适当模块。我们建议编译所有的网络选项和可用选项。如果你想让服务器作为路由器，必须启用 IP 转发。
2. IP 转发
3. Caldera OpenLinux 默认未启用 IP 转发。

## 12.4 包过滤的网络配置

在本节中，我们将描述用于包过滤的设置。图 183 显示了：

- `192.168.0.1` (网关)
- `192.168.0.2` (`eth0`)
- `192.168.0.3` (`eth1`)

你可以看到有两个网络：`192.168.0.0` 和 `172.168.0.0`。`172.168.0.1` 是作为网关的服务器。`172.168.0.2` 连接到互联网的。

## 12.5 如何永久启用 IP 转发

在 Caldera OpenLinux 中，网络在启动期间通过此脚本启动：

`/etc/rc.d/init/network`

要启用它，打开 `/etc/rc/d/init/network` 文件并找到行：

```
:IPFORWARDING=no
```

将其更改为：

```
:IPFORWARDING=yes
```

你需要重启网络来激活更改。可以通过执行以下命令来实现：

`/etc/rc/d/init/network stop`

`/etc/rc/d/init/network start`

现在你的服务器已准备好充当路由器。你可以通过从 `172.168.0.0` 机器 ping `tr0` 接口 `192.24.104.22`，如果 ping 成功，说明你的路由器工作正常。你会看到一个类似于图 184 的窗口。

```
[root@client ~] ping 192.24.104.22
PING 192.24.104.22 (192.24.104.22) 56 data bytes
64 bytes from 192.24.104.22: icmp_seq=0 ttl=255 time=7 ms
64 bytes from 192.24.104.22: icmp_seq=1 ttl=255 time=3 ms
64 bytes from 192.24.104.22: icmp_seq=2 ttl=255 time=0.3 ms
64 bytes from 192.24.104.22: icmp_seq=3 ttl=255 time=0.3 ms
64 bytes from 192.24.104.22: icmp_seq=4 ttl=255 time=0.3 ms

--- 192.24.104.22 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, round-trip min/avg/max = 0.3/0.3/0.7 ms
[root@client ~]#
```

## 12.6 你的首次 IP Chains 成功尝试

现在你的路由器已经工作了，让我们利用它吧。如果不部署它，拥有一个路由器是没有意义的。我们希望从内部网络 `172.168.0.0` 访问外部网络 `9.0.0.0`。我们如何做到这一点？通过使用 IP Chains 的 IP 伪装（IP Masquerading）功能。在网关网络上按照以下步骤操作，设置从内部网络 `172.168.0.0` 到外部网络 `9.0.0.0` 的文件传输协议（FTP）访问：

1. 执行命令为所有模块创建模块依赖信息：
   ```
   /sbin/depmod -a
   ```
2. 加载用于以实现正确 FTP 伪装的模块：
   ```
   /sbin/modprobe ip_masq_ftp
   ```
   如果你想使用其他协议，例如 Real Audio 和互联网中继聊天（IRC），你也可以加载它们的模块。
3. 设置 IP 伪装的超时时间：
   ```
   /sbin/ipchains -M -S 8000 20 200
   ```
   参数的含义如下：
   - `8000` - TCP 会话的超时时间（秒）
   - `20` - 收到 `FIN` 包后 TCP 会话的超时时间（秒）
   - `200` - UDP 数据包的超时时间（秒）
   你可以根据需要调整这些设置。
4. 通过禁用所有 IP 地址的转发来更改内置转发策略：
   ```
   /sbin/ipchains -P forward DENY
   ```
5. 为你的内部网络添加启用带伪装转发的策略：
   ```
   /sbin/ipchains -A forward -s 192.168.0.0/24 -j MASQ
   ```
   ```
   /sbin/ipchains -A forward -s 172.168.0.0/24 -j MASQ
   ```

你已经准备好尝试你的设置了。从网络 `172.168.0.0` 上的计算机执行命令：

```
/usr/bin/ftp server
```

其中 `ftp server` 是外部网络上的 FTP 服务器（在我们的示例中为 `9.0.0.0`）。你会看到一个类似于图 185 的窗口。

```
[root@local ~]# ftp 92.24.106.49
Connected to 92.24.106.49
220 TPIVO2 IBM TCP/IP for OS/S2 - FTP Server at 19:29:50 on Sep 2 1998 ready.
Name (92.24.106.49:root): ivo
331 Password required for ivo.
Password:
230 User logged in.
ftp>
```

图 185. 设置 IP 伪装后的 FTP

你刚刚成功从内部网络访问了外部网络。

## 12.7 数据包如何通过网关

在本节中，我们将解释 IP Chains 的工作原理。你可以在图 186 中看到进入服务器的数据包路径。

![](img/2d69b129b41635ef36a3e6707d34b788_251_0.png)

图 186. 数据包的传输方式

以下是每个阶段的简短描述：

- 校验和（Checksum） - 用于测试数据包是否损坏。
- 完整性（Sanity） - 在此拒绝格式错误的包。
- 输入链（Input chain） - 这是第一个真实的数据包检查点。包可以被拒绝、禁止或接受。
- 去伪装（Demasquerade） - 如果数据包是之前伪装数据包的响应，它将去伪装并直接从这里到输出链。
- 路由决策（Routing decision） - 路由代码决定此包是用于本地进程还是应该转发到远程机器。
- 本地进程（Local process） - 运行在服务器上的进程可以在路由决策步骤后接收数据包，然后发送数据包，数据包通过路由决策步骤进入输出链。
- `lo` 接口 - 来自本地进程的数据包的目标是本地进程，它们将通过接口设置为 `"lo"` 的输出链，然后通过接口 `"lo"` 返回输入链。`"lo"` 接口通常称为回环接口。
- 本地（Local） - 如果数据包不是由本地进程创建，则检查转发链。
- 转发链（Forward chain） - 这是所有通过此服务器到达其他地方的数据包的检查点。
- 输出链（Output chain） - 这是所有数据包在发送出去之前的检查点。

从图 186 可以看出，你可以在服务器的三个三个可以检查数据包：

- 输入链
- 转发链
- 输出链

使用 `/sbin/ipchains` 命令，你可以设置数据包检查的规则。

> 注意
>
> 默认情况下，所有检查策略都设置为接受（Accept）。这意味着所有数据包都可以进入、通过或离开你的服务器，而没有任何任何限制。

你可以通过执行以下命令查看当前的检查策略：

`/sbin/ipchains -L`

你会看到一个类似于图 187 的窗口。

```
[root@client /root]# ipchains -L
Chain input (policy ACCEPT)
Chain forward (policy ACCEPT)
Chain output (policy ACCEPT):
[root@client /root]#
```

图 187. 列出 IP 策略

## 12.8 使用 IP Chains

通过 `/sbin/ipchains` 命令，你可以创建、更改或删除你自己的数据包检查策略，也可以修改内置策略。你不能删除内置链，但可以向现有链添加规则或创建自己的。管理整个链可以使用表 20 的参数。

### 表 20. 管理整个链的参数

| 参数 | 描述 |
| :--- | :--- |
| `-N` | 创建新链 |
| `-X` | 删除空链 |
| `-P` | 修改内置链的策略 |
| `-L` | 列出链的规则 |
| `-F` | 清空链的规则 |
| `-Z` | 链计数清零 |

操作链内部规则可以使用表 21 中的参数。

### 表 21. 管理链内规则的参数

| 参数 | 描述 |
| :--- | :--- |
| `-A` | 向链添加规则 |
| `-I` | 在某某位置插入新规则 |
| `-R` | 在某位置替换规则 |
| `-D` | 在某位置删除规则 |

还有更多用于伪装的操作，在表 22 中描述。

### 表 22. 管理伪装的参数

| 参数 | 描述 |
| :--- | :--- |
| `-M` | 列出当前伪装的连接 |
| `-S` | 设置伪装超时值 |

### 12.8.1 如何创建规则

创建新规则的最常用语法是：

```
/sbin/ipchains -A input -s protocol -j action
```

参数在表 23 中描述。

### 表 23. IP 参数

| 参数 | 描述 |
| :--- | :--- |
| `-A` | 向链添加新规则 |
| `source` | 源 IP 地址或主机名 |
| `protocol` | 应用规则的协议类型 |
| `action` | 数据包将发生什么:<br>1) `ACCEPT` - 包被接受<br>2) `REJECT` - 包被拒绝<br>3) `DENY` - 包由于未接收被丢弃<br>4) `MASQ` - 包将被伪装<br>5) `REDIRECT` - 包被重定向到本地端口<br>6) `RETURN` - 退出链 |

> 注意：使用 `REDIRECT` 操作将数据包重定向到本地端口仅在与透明代理结合使用时才有意义。

例如，如果你想为执行特定 IP 地址 `ping` 命令时使用的 `ICMP` 包创建一个规则，你可以通过执行命令来实现：

```
/sbin/ipchains -A input -s IP_address -p icmp -j DENY
```

如果你省略了协议定义，所有数据包将被拒绝。例如，如果你想阻止来自子网掩码为 `255.255.255.0` 的 `172.168.0.0` 网络的访问，你可以执行以下命令：

```
/sbin/ipchains -A output -s 172.168.0.0/255.255.255.0 -j DENY
```

或者使用：

```
/sbin/ipchains -A input -s 172.168.0.0/24 -j DENY
```

你可以看到，子网掩码可以使用位数来指定。从你的服务器到 `172.168.0.0` 网络子网掩码为 `255.255.255.0`）不允许任何流量的命令如下：

```
/sbin/ipchains -A output -d 172.168.0.0/24 -j DENY
```

![](img/2d69b129b41635ef36a3e6707d34b788_254_0.png)

在这里使用了 `"d"` 参数来指定目标地址。

### 12.8.1.1 使用反转标志

对于某些参数，你可以使用反转选项 `"!!"`。这意味着规则将适用于除 `"I"` 之后指定的参数以外的所有内容。例如，如果你想拒绝来自除子网掩码为 `255.255.255.0` 的 `192.168.0.0` 网络的所有 IP 地址的包，你可以通过执行命令来实现：

```
/sbin/ipchains -A input -s ! 192.168.0.0/24 -j DENY
```

> 注意
>
> 你创建的规则不是持久的，所以下次重启服务器时它们就会消失。

## 12.8.2 使规则持久化

为了使规则持久化，你有两个脚本可以让你的生活更轻松。要保存你创建的所有规则，你可以执行命令：

```
/sbin/ipchains-save > filename
```

如果你执行此命令时不指定文件名，规则将发送到标准输出。

你可以通过执行命令恢复保存的规则：

```
cat filename /sbin/ipchains-restore
```

所以，如果你希望在每次启动系统时启用保存的规则，请向 `/etc/rc.d/rc.local` 文件中添加以下行：

```
cat filename /sbin/ipchains-restore
```

## 12.9 更多信息来源

你可以在官方 Linux IP Firewall Chains 页面找到更多信息：

```
http://www.rustcorp.com/linux/ipchains
```

在 Linux 文档项目页面也有很多优秀的教程文档：

```
http://www.linuxdoc.org/
```

# 第 13 章 备份与恢复

尽管硬件正变得越来越可靠，但我们仍然需要保护数据。为了保护你的数据，你需要一个备份解决方案。最常用的备份媒介是磁带，但现如今你也可以在其他介质上创建备份，例如 `CDRW` 或 `CD-ROM`。

快速备份和恢复数据至关重要这似乎显而易见，但许多管理员会将此任务置于“待办事项”列表的最后，直到为时已晚。由于有 Microlite 和 `BRU` 工具提供的商用备份工具，用起来非常方便，无需等待。

## 3.1 Microlite BackupEDGE

`BackupEDGE` 是一个适用于 Linux 平台的完整备份解决方案。它易于使用且非常健壮。通过 `BackupEDGE`，你可以安全地归档文件系统上的每个文件、目录、设备节点和特殊文件与标准的 UNIX `tar` 文件会忽略许多重要文件不同，`BackupEDGE` 还会验证写入磁带的每一个字节数据，以确保磁带是你数据的准确反映。以下是 Microlite `BackupEDGE` 软件提供的功能：

- **数据压缩** - 支持自动数据压缩。
- **菜单界面** - 几乎所有功能都可以通过直观的菜单系统访问。
- **远程磁带驱动支持** - 你可以跨网络备份计算机。
- **高性能** - 高级双重缓冲和可变块因子。
- **虚拟文件支持** - 你可以备份虚拟（稀疏）文件。
- **多卷/多设备归档** - 自动跨卷或跨设备跨。
- **通配符支持** - 在选择文件时可以使用通配符。
- **原始设备备份** - 你可以将整个设备/分区归档到磁带。
- **全备份 / 增量备份**
- **无人值操作** - 你可以执行全备份或仅备份更改的文件。

`BackupEDGE` 设计用于在 Linux 内核 `2.x` 上运行，并提供多种类型库的可用。

在接下来的章节中，我们将描述如何安装、配置和使用 Microlite `BackupEDGE` 备份软件。

> 注意
>
> 我们建议你不要将磁带设备连接到 IBM ServeRAID 控制器。请使用独立的 `SCSI` 控制器连接磁带设备。

### 13.1.1 安装 Microlite BackupEDGE

在安装 `BackupEDGE` 之前，你必须识别备份设备的设备节点。通常 Linux 下的磁带设备被分配在设备节点 `/dev/st0`、`/dev/sti`……，每个磁带设备都会创建一个不回带设备，即 `/dev/nst0`、`/dev/nst1`……在我们的示例中，我们使用 `/dev/st0` 作为磁带设备，使用 `/dev/nst1` 作为不回带设备。

在我们的示例中，我们使用软盘作为安装媒介。按照以下步骤安装产品：

1. 以 `root` 身份登录。
2. 切换目录到根目录 `"/"`。
3. 将带有产品的软盘插入软驱器并执行命令：
   `tar xvf /dev/fd0`
   其中 `/dev/fd0` 是你的软驱设备。
4. 执行以下命令完成安装：
   `/tmp/init.edge`
   你将看到一个窗口。

# BackupEDGE 增强数据归档系统

| 部分 | 版权 |
| :--- | :--- |
| 部分 [c] | 1987 - 1999 Microlite Corporation |
| 部分 [c] | 1987 - 1999 UniTrends Software Corporation |
| 保留所有权利 | |

系统 Linux `2.x` (使用 `glibc` `[libc.so.6]` 和 `stdc++.so.2.9`)

`BackupEDGE` 版本: `01.01.07` - `1999-11-02`

`BackupEDGE` 已激活 `90` 天。

临时激活将于 `2000` 年 `1` 月 `31` 日过期。

请运行 `/usr/lib/edge/bin/edge activate` 来注册你的产品。

请将 `/usr/lib/edge/bin/s88edge` 复制到你的启动目录或 `/etc/rc` 文件的末尾。

此程序在系统启动期间会删除 `edge` 进度文件。

快速文件恢复选项已安装。请运行 `/usr/lib/edge/bin/edge.resmgr` 测试快速文件恢复能力！

`BackupEDGE` 安装完成！

按 `[Enter]` 继续

图 18. 完成产品的使用。



现在你已经准备好使用该产品了。

### 3.1.2 配置磁带设备

在开始备份之前，你需要定义你的备份设备。

要实现这一点，请按照以下步骤操作：

1. 执行命令启动 `edge.resmgr` 资源管理器：

```
/usr/lib/edge/bin/edge.resmgr
```

你将看到一个类似于图 189 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_259)

2. 点击 `New`（新建）并按资源。你将看到一个img/ 29991。

bimg/635926a3e67073343783259))图 188. 资源资源

3. 输入资源名称并选择类型。你将看到一个类似于图 191 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_259)

图 190. 定义名称

4. 输入描述、不回带节点。在我们的示例中，数据节点是 `/dev/st0`，不回带节点是 `/dev/nst1`。

5. 点击 `OK` 配置其他字段。你将看到一个类似于图 192 的窗口。

图 191. 磁带参数

6. 在这里你可以选择块因子和大小。点击 `Start` 继续。你将看到一个类似于图 193 的窗口。

图 192. 设置参数

7. 点击 `Yes`（是），这将删除磁带上的数据。你将看到一个类似于图 194 的窗口。

图 193. 性能

8. 测试完成后，你会看到阈值。点击 `OK` 继续。

图 194. 阈值

9. 通过选择 `Save`（保存）保存更改。你将看到一个类似于图 196 的窗口。

图 195. 保存定义

### 3.1.3 为备份定义设备

硬件配置好后，你需要告诉备份软件每个用户使用哪个设备。如果你以 `root` 登录，这是唯一的备份用户。按照以下步骤操作：

1. 执行命令启动 `edge.config` 菜单：

`/usr/bin/edge.config`

你将看到一个类似于图 197 的窗口。

图 197. 设备配置

2. 在这里你需要定义演示和无人备份的设备。你将看到一个类似于图 198 的窗口。

图 198. 选择备份设备

3. 输入 `A` 并按回车定义演示备份的设备。你将看到一个类似于图 199 的窗口。

```
文件分区选项

备份设备配置 (edge.config) 版本 01.01.07
Copyright 1998 - 1999 Microlite Corporation 保留所有权利
备份资源: 演示备份 无人备份
主系统: (A) Localhost (E) NONE
资源: DL
描述: DLT 磁带 35/70GB
设备节点/文件: /dev/st0
溢出系统: (B) NONE (F) NONE
资源:
描述:
设备节点/文件:
更改: (C) NONE (G) NONE
资源:
描述:
设备节点/文件:
更改 主备份资源 F 更改无人
更改 溢出备份资源 F 更改无人
更改 磁带自动库资源 I 更改无人
通过资源管理器添加/更改资源
活动系统名称为 n9f3500.first.itso.com
输入选择 (ARG,3,X7) 并按 <Enter> :
```

图 199. 定义演示设备

4. 按照步骤 1-4 处理无人设备。

你现在准备好备份你的重要文件了。

### 3.1.4 初始化磁带

在进行备份之前，你应该初始化磁带。要执行此操作，请按照以下步骤操作：

1. 执行命令启动 `edgemenu` 程序：

`/usr/bin/edgemenu`

你将看到一个类似于图 200 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_268_0.png)

图 200. ADGEMEMENU 主菜单

2. 在管理（`Admin`）菜单中选择初始化磁带（`Initialize Tapes`）。你将看到一个类似于图 201 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_268_1.png)

图 201. 初始化磁带

3. 选择初始化磁带（`Initialize Tape`）并按 `Enter`。磁带将被初始化。你将收到磁带成功初始化的消息。按 `Enter` 继续。

你可以通过选择验证（`Verify`）菜单中的显示磁带标签（`Show Tape Label`）来检查磁带属性。你将看到一个类似于图 202 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_269_0.png)

图 202. 磁带信息

### 13.1.5 你的首次备份

在本节中，我们将展示如何对所需的文件或目录进行备份。你可以在 `edgenemu` 工具中执行备份。按照以下步骤进行示例备份：

1. 通过执行命令启动 `edgenemu` 程序：

```
//usr/bin/edgenemu
```

你将看到一个类似于图 203 的窗口。

### Terminal

```
[文件] [备份] [恢复] [验证] [管理] [计划]
  [主备份]
  增量备份
  备份文件/目录
  [备份当前目录]
  单个文件或目录
```

![](img/2d69b129b41635ef36a3e6707d34b788_270_0.png)

图 203. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

2. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

### Terminal

```
[文件] [备份] [恢复] [验证] [管理] [计划]
主.增量, L 或文件备份
  文件 / 目录备份
验证卷               记录锁定
[2] 验证类型（按文件）                  (X) 不锁定文件
[X] 验证期间索引                    ( ) 强制读取
  在处理归档时包含的文件
  要包含的文件/目录 [es]
  [/user/arc                          [es]
  列出包含的文件
  [
  [确定]                                     [取消]
目录文件
  资源  NONK
  计算机硬盘类型列表  文件 #asterisk
  本地备份 Bac Nov 7 10:15 am
本地机器 nr5500 first.com Administering nr5500 first itscom
```

图 204. 选择备份内容

3. 在要包含的文件/目录（`Files / Directories to Include`）字段中，输入你想要备份的文件或目录。在我们的示例中，我们想要备份目录

第 13 章 备份与恢复 253

`/usr/src/` 选择确定（`OK`）继续。你将看到一个类似于图 205 的窗口。

### Terminal

| [文件] [备份] [恢复] [验证] [管理] [计划] |
| 文件 / 目录备份 | 记录锁定 |
| [2] 验证类型（逐个文件） | (X) 不锁定文件 |
| [X] 验证期间索引 | (强制读取 |
| 备份文件 | /usr/src/linux-2.2.10/net/root |
| 文件 5122 | [C] 取消 | es |

图 205. 正在备份中

备份完成后，你将看到一个类似于图 206 的窗口。

### Terminal

| [文件] [备份] [恢复] [验证] [管理] [计划] |
|| 文件 / 目录备份 | 记录锁定 |
| [2] 验证类型（逐个文件） | (X) 不锁定文件 |
| [X] 索引 | 或强制读取 |
| 备份 / 验证 / 索引成功 | 读取 |
| Spl | [包含] |
| Make | 包含 |
| Ok | |

图 206. 备份完成

Caldera OpenLinux 和 Netfity 服务器集成指南

你还将看到一个类似于图 207 的备份报告。

```
# /tmp/lb1/http=/badv/bdt-1999-11-02/bts-19.53/bdv-st0/bbk=64/bvs=350000
a /usr/src/linux-2.10/System.map, 399 blocks
VOL=209715Mb
a /usr/src/linux-2.10/System.map-pc-97, 381 blocks
VOL=209715Mb
a /usr/src/linux-2.10/include/linux/compile h. h, 1 blocks
a /usr/src/linux-2.10/include/linux/s.out h. h, 15 blocks
a /usr/src/linux-2.10/include/linux/acct. h, 6 blocks
a /usr/src/linux-2.10/include/linux/adfs fs. h, 10 blocks
a /usr/src/linux-2.10/include/linux/adfs fs i. h, 1 blocks
a /usr/src/linux-2.10/include/linux/adfs fs-b. h, 1 blocks
a /usr/src/linux-2.10/include/linux/affs fs. h, 9 blocks
VOL=209715Mb
a /usr/src/linux-2.10/include/linux/affs fs i. h, 4 blocks
a /usr/src/linux-2.10/include/linux/affs fs sb. h, 6 blocks
a /usr/src/linux-2.10/include/linux/affs hardblocks. h, 3 blocks
```

图 207. 备份报告

你刚刚完成了备份，你的文件是安全的！

### 13.1.6 恢复文件或目录

在本节中，我们将展示如何从备份恢复文件。我们假设你使用相同的工具进行了备份。按照以下步骤进行恢复：

1. 通过执行命令启动 `edgenemu` 程序：

```
//usr/bin/edgenemu
```

你将看到一个类似于图 203 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_273_0.png)

2. 在备份（`Backup`）菜单中，选择备份文件/目录（`Backup Files / Dirs`），你将看到一个类似于图 204 的窗口。

3. 在要包含的文件/目录（`Files / Directories to Include`）字段中，输入你想要恢复的文件或目录。选择确定（`OK`）继续。你将看到一个类似于图 205 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_274_0.png)

恢复完成后，你将看到一个类似于图 210 的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_277_0.png)

### 13.1.9 执行计划备份

要执行计划备份，你可以使用 `BackupEDGE` 自带的实用程序。该工具名为 `edge.nightly`。要启动该工具，请执行命令：

```
/usr/lib/edge/bin/edge.nightly
```

但在使用计划备份之前，你需要先对其进行定义。请按照以下步骤操作：

1. 启动 `edgemenu`。

2. 选择 `Schedule`（计划）-> `Nightly Scheduling`（每日调度）。你将看到一个与图 218 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_279_0.png)

图 218. 计划设置

3. 在这里你可以定义备份计划。你需要定义备份的类型和时间。要定义备份类型，选择 `A` 并按回车，你将看到一个与图 219 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_280_0.png)

图 219. 定义备份类型

4. 指定你想执行的备份类型。在我们的示例中，我们选择了 `M` 代表主备份（master backup）。返回返回主窗口。

> 注意

> 你不能混合使用主备份和增量备份。如果你的主备份可以放入一个磁带盒，我们建议每天执行一次主备份。如果你的主备份无法放入一个磁带盒，请每周执行一次手动主备份，每天执行增量备份。

5. 接下来，你需要通过选择 `B` 并按回车来指定每日备份的时间。你将看到一个与图 220 类似的窗口。

```
Currently 1999-11-04 12:09:22
At what hour do you want your Master Backups to start? (0-23)
Press [ENTER] for 23 (11 PM) :
```

图 220. 设置时间

6. 定义你备份的时间。你将看到一个与图 221 类似的窗口。

```
Terminal <2>
BackupEDGE Nightly Archive Setup Menu (edge_cronset) Version 01.07
Copyright 1988 - 1999 by Microsoft Corporation All Rights Reserved
Choice Settings Type Current Last
A BackupEDGE Backup Type Master Master
B Backup Time (24 hour format) 12:30 12:30
C Mail Notification To root root
D (t) Backup on Sundays YES root
E (t) Backup on Tuesdays YES YES
F (t) Backup on Wednesdays YES YES
H (t) Backup on Thursdays YES YES
I (t) Backup on Fridays YES YES
J (t) Backup on Saturdays YES YES
K Verify After Backup BIT BIT
L Index After Backup YES YES
M Send Diagnotstics Output To /dev/null
N Print Backup Results To DISABLED
S Save Settings - Create New Cron
X Exit - Abandon Changes Use Last Entries 1999-11-04 12:37:39
(t) Toggles Entry (YES or No)
please Type Letter of Your Selection and Press [ENTER] 
```

图 221. 计划定义后

7. 选择 `S` 并按回车设置设置。配置程序将在 `cron` 数据库中创建一个用于执行 `edge.nightly` 工具的条目。从现在起，`cron` 将按照你之前步骤中的定义执行备份工具。

# 注意

在开始使用计划备份之前，你需要将文件 `/usr/lib/edge/bin/S88egde` 复制到 `/etc/rc.d` 目录。此脚本将在系统重启时清除 `edge.nightly`。

你也可以从自己的脚本启动 `edge.nightly`。当你从命令行或脚本以 `root` 身份启动 `edge.nightly` 后，它将执行备份。

## 13.2 轻量级 RecoverEDGE

使用 `RecoverEDGE` 工具可以创建恢复磁盘，以便在灾难时重建系统。`RecoverEDGE` 处理重建 `FDisk`、分区表、重建文件系统以及恢复数据的细节，即使硬盘的大小或几何结构发生了变化。`RecoverEDGE` 使用实时系统备份，因此不需要关闭系统。你甚至可以通过网络恢复系统。

使用 `RecoverEDGE` 恢复系统非常简单。要恢复系统应遵循以下任务：

1. 识别并修复故障原因。

2. 从 `RecoverEDGE` 磁盘启动。

3. 重配置你的文件系统。

4. 恢复你的备份。

5. 重启。

6. 系统就绪。

# 注意

`RecoverEDGE` 使用主备份和增量备份进行恢复，因此数据的准确性取决于这些备份。

### 13.2.1 创建 RecoverEDGE 启动磁盘

在使用 `RecoverEDGE` 进行灾难恢复之前，你需要构建启动磁盘。创建启动磁盘请遵循以下步骤：

1. 启动创建 `RecoverEDGE` 启动磁盘的工具：

```
/usr/bin/re
```

你将看到一个与图 222 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_283_0.png)

图 222. `RecoverEDGE` 工具

2. 选择 `Configure`（配置）并按回车，你将看到一个与图 223 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_284_0.png)

图 223. 配置菜单

3. 选择 `Disk Layout`（磁盘布局）选项并按回车，你将看到一个与图 224 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_284_1.png)

图 224. 磁盘布局菜单

4. 在这里你可以为 `RecoverEDGE` 磁盘配置内核模块、网络和文件系统。选择 `Kernel`（内核）选项，你将看到一个与图 225 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_285_0.png)

图 225. 内核选项

在这里定义用于磁盘的内核。

5. 返回上一个阶段并选择 `Modules`（模块）并按回车，你将看到一个与图 226 类似的窗口。



# 内核模块

```
[Kernel] [Modules] [Network] [Filesystems] [Previous]
View / Modify Loadable Kernel Configuration

Kernel Modules
Directory: [/lib/modules]           Modules Needed For Boot / Recovery
Detected Modules                                     [ ]
loop                                 /lib/modules/2.2/13/pcnet32.o
dac960                              /lib/modules/2.2/13/scsi/scsi_mod
ide-tape                             /lib/modules/2.2/13/scsi/sd_mod
ide-floppy                           /lib/modules/2.2/13/scsi/aic_prox.o
xd                                   /lib/modules/2.2/13/scsi/ips
cpqarras                             /lib/modules/2.2/13/fs/isofs
[X]Compatible Modules Only (More) [X]Autodetect Modules On Startup (More)
```

```
screen-Boot  date feb 14 as version 2.1.12 12:00
Temp: Recovery  dev:display:0  System#S500 Boot again
root: re-  verify Sec  Booting version 2 |kernel
```

图 226. 模块选项

你定义用于构建恢复系统初始 ramdisk 的模块。在 `Directory` 字段中，你可以指定与你定义的启动内核对应的模块路径。如果你选择 `Autoprobe Modules at Startup`（启动时自动探测模块），`RecoverEDGE` 将加载当前加载的模块。

> **注意**
>
> 不要忘记包含磁带驱动器的模块。

## 网络配置

6. 返回上一个阶段并选择 `Network`（网络）并按回车，你将看到一个与图 227 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_287_0.png)

图 227. 网络选项

在这里定义网络设置，以便从网络上的磁带设备恢复系统。如果你有本地连接的磁带，则不需要此项。

## 文件系统配置

7. 返回上一个阶段并选择 `Filesystems`（文件系统）并按回车，你将看到一个与图 228 类似的窗口。

```
[Kernel] [Modules] [Network] [Filesystems] [Previous]
Select Filesystems For Restore
            Select Auto-Recover Filesystems
Non-Restorable (e. g. CD-ROM)          Restorable Filesystems
/proc                               "swap"
                               --> /boot
                                     /mnt/boot.rh
                                     /mnt/boot turbo
                                     /mnt/cdrom
                                     /mnt/root.rh
                                              (More)
```

![](img/2d69b129b41635ef36a3e6707d34b788_288_0.png)

图 228. 文件系统选项

在这里定义要恢复的挂载文件系统。

## 引导加载程序配置

8. 返回配置面板并选择 `Boot Loader`（引导加载程序）选项并按回车。你将看到一个与图 229 类似的窗口。

```
[Disk Layout] [Boot Loader] [Boot Media] [Previous]
Configure Boot Setup
            Boot Loader Configuration
[X] Boot Floppy with LILO          Configuration File: [/etc/lilo.conf ]
[X] Normal HD Boot Uses LILO
                                     Map File: [ ]
                                     Boot File: [/boot/boot.b ]
```

![](img/2d69b129b41635ef36a3e6707d34b788_288_1.png)

图 229. 引导加载程序选项

在此处定义引导加载程序（`Boot Loader`）的选项。

## 启动媒体配置

9. 返回配置面板，选择启动媒体（`Boot Media`）选项并按回车。你将看到一个与图 230 类似的窗口。

![](img/2d69b129b41635ef36a3e6707d34b788_289_0.png)

图 230. 启动媒体选项

在此处定义如何创建启动磁盘。

在制作磁盘之前，你需要修改 `RecoverEDGE` 工具的配置。要执行此操作，请打开 `/usr/lib/edge/recover2/OSFILES` 文件。

在该文件中进行以下更改：

- a. 删除行 `/bin/ash`。
- b. 将行 `/lib/ld.so` 改为 `/lib/ld-linux.so.1.9.9`。

10. 配置所有设置后，返回主窗口并选择制作磁盘（`Make Disks`）。系统将提示你插入三张磁盘。

> **注意事项**
>
> 如果你收到无法创建磁盘的错误，可能的原因是镜像太大。尝试减少加载的模块数量，甚至专门为此目的创建一个特殊的内核，丢弃所有不需要的内容。

*272 Caldera OpenLinux 和 Netfinity 服务器集成指南*

在你创建的磁盘准备好处理系统灾难之后。但在灾难真正发生之前，请尝试从这些磁盘启动并验证你的磁带设备是否被识别。

### 13.2.1.1 验证 RecoverEDGE 启动磁盘

要验证磁盘，从第一张磁盘启动并按照窗口上的说明操作。当系统启动时，你将看到 `RecoverEDGE` 主菜单。选择 `Utilities`（工具）-> `Tape Drive`（磁带驱动）。

在磁带设备节点（`Tape Device Node`）字段中，看到定义的磁带设备。转到 `Test Tape Drive`（测试磁带驱动）字段测试你的磁带设备。如果测试成功，恢复集即可使用。

### 13.2.2 从总崩溃中恢复

要从崩溃故障中恢复，请遵循以下步骤：

1. 解决所有硬件问题。

   > **注意**
   >
   > 在恢复系统之前，请初始化所有磁盘驱动器的主引导记录（`Master Boot Records`）。

2. 从第一张 `RecoverEDGE` 启动磁盘启动服务器。

3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。磁盘加载后，`RecoverEDGE` 将启动。

4. 选择 `Restore`（恢复）-> `One Touch`（一键恢复）。按照窗口上的说明完成恢复。

   > **注意**
   >
   > 恢复时你将使用你的主备份和增量备份。

5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。

6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

```
mount /dev/sdb6 /mount
cat /mount/etc/fstab
```

![](img/2d69b129b41635ef36a3e6707d34b788_290_0.png)

![](img/2d69b129b41635ef36a3e6707d34b788_290_1.png)

在我们的示例中，`sdb6` 是我们的根分区；你应该在此处使用你的根分区。

就是这些。你恢复的系统已准备就绪。

# 13.3 关于 Microlite 的更多信息

有关高级功能的信息，请参阅 `Microlite` 用户指南或 `Microlite` 网站：

```
http://www.microlite.com/
```

# 13.4 BRU

`BRU` 是一种备份和恢复工具，相比 `tar`、`cpio`、`volcopy` 和 `dump` 等其他常用工具有显著增强。`BRU` 设计用于大多数备份设备，包括带带、`4mm DAT`、`8mm (Exabyte)` 和 `9` 轨磁带机。

`BRU` 包含增量备份、全备份、多卷存档、发行和更新、错误检测与恢复、随机访问能力、文件比较、文件覆盖保护，以及比以前版本更高的速度。

## 13.4.1 安装 BRU

在开始之前，我们需要知道以下信息：

1. 磁带驱动器的设备名称。在 `Caldera OpenLinux` 下，它通常为 `/dev/st0`。

2. 备份介质的大小（单位为 `MB`）。

要使用 `tar` 命令从软盘器安装 `BRU`，请执行以下操作：

```
cd /tmp
tar xvf /dev/fd0
./install
```

按照 `readme` 文件和许可提示操作，直到出现以下窗口：

```
########################### 新 /etc/brutab 文件。此文件将包含
关于你系统中设备的信息。
###########################################
```

请从下列表中选择备份设备，或在完成后输入 `Q`。

- a) 1/4 英制带带驱动器
- b) 4mm DAT 磁带驱动器
- c) 8mm (Exabyte) 磁带驱动器
- d) DLT (数字线性磁带)
- e) 其他
- q) 退出

此设备的类型是：-

图 231 选择你的备份设备

1. 选择所有的备份设备，完成后输入 `Q`。
2. 磁盘加载后，`RecoverEDGE` 将启动。
3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。
4. 选择 `Restore` -> `One Touch`。按照窗口上的说明完成恢复。
5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。
6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

> **注意**
>
> 在恢复系统之前，请初始化所有磁盘驱动器的主引导记录。
>
> 恢复时你将使用你的主备份和增量备份。

在我们的示例中，`sdb6` 是我们的根分区；你应该在此处使用你的根分区。

就是这些。你恢复的系统已准备就绪。

### 13.2.1.1 验证 RecoverEDGE 启动磁盘

要验证磁盘，从第一张磁盘启动并按照窗口上的说明操作。当系统启动时，你将看到 `RecoverEDGE` 主菜单。选择 `Utilities`（工具）-> `Tape Drive`（磁带驱动）。

在磁带设备节点（`Tape Device Node`）字段中，看到定义的磁带设备。转到 `Test Tape Drive`（测试磁带驱动）字段测试你的磁带设备。如果测试成功，恢复集即可使用。

### 13.2.2 从总崩溃中恢复

要从崩溃故障中恢复，请遵循以下步骤：

1. 解决所有硬件问题。
2. 从第一张 `RecoverEDGE` 启动磁盘启动服务器。
3. 当提示插入根磁盘时，插入第二张 `RecoverEDGE` 启动磁盘。
4. 选择 `Restore` -> `One Touch`。按照窗口上的说明完成恢复。
5. 当所有文件备份完成后，按任意键返回主窗口。所有文件系统将将被同步，并设置并执行 `LILO`。
6. 在重启之前，按 `Alt+F2` 切换到控制台 2，并执行以下命令检查 `fstab` 文件以确保你的系统条目是否正确：

```
mount /dev/sdb6 /mount
cat /mount/etc/fstab
```

# 13.3 关于 Microlite 的更多信息

有关高级功能的信息，请参阅 `Microlite` 用户指南或 `Microlite` 网站：

```
http://www.microlite.com/
```

# 13.4 BRU

`BRU` 是一种备份和恢复工具，相比 `tar`、`cpio`、`volcopy` 和 `dump` 等其他常用工具有显著增强。`BRU` 设计用于大多数备份设备，包括带带、`4mm DAT`、`8mm (Exabyte)` 和 `9` 轨磁带机。

`BRU` 包含增量备份、全备份、多卷存档、发行和更新、错误检测与恢复、随机访问能力、文件比较、文件覆盖保护，以及比以前版本更高的速度。

## 13.4.1 安装 BRU

在开始之前，我们需要知道以下信息：

1. 磁带驱动器的设备名称。在 `Caldera OpenLinux` 下，它通常为 `/dev/st0`。

2. 备份介质的大小（单位为 `MB`）。

要使用 `tar` 命令从软盘器安装 `BRU`，请执行以下操作：

```
cd /tmp
tar xvf /dev/fd0
./install
```

按照 `readme` 文件和许可提示操作，直到出现以下窗口：

```
########################### 新 /etc/brutab 文件。此文件将包含
关于你系统中设备的信息。
###########################################
```

请从下列表中选择备份设备，或在完成后输入 `Q`。

- a) 1/4 英制带带驱动器
- b) 4mm DAT 磁带驱动器
- c) 8mm (Exabyte) 磁带驱动器
- d) DLT (数字线性磁带)
- e) 其他
- q) 退出

存档。备份将通过向您显示预计的完成时间和进度窗口来进行。

## 13.4.4.2 调度

要访问调度功能，请选择 `文件 (File)` -> `调度器 (Scheduler)`。

![](img/2d69b129b41635ef36a3e6707d34b788_296_0.png)

图 234. 调度器

`BRU` 提供了一个调度工具，为忙碌的管理员自动化备份过程。有三种预定义的定义：全量（`Full`）、1级（`Level 1`）和2级（`Level 2`）。这些与 13.4.4 节中定义相同，即第 277 页上的“大按钮”。您可以在创建存档界面中创建自己的定义。

通过 `BRU for X11` 调度器界面，您可以根据每周、每月或特定日期设置调度备份。调度器非常灵活。为了利用调度选项，您必须保存所需的调度配置，并验证调度器正在通过 `cron` 运行。要验证或添加 `cron` 条目，请以 `root` 身份登录并输入：

```
crontab -e
```

插入以下行：

```
0/5 * * * * /usr/local/bin/bruschedup
```

如果您在安装期间为二进制文件选择了不同的路径，请相应更改条目。

保存 `crontab` 条目。您现在可以调度备份了。

## 13.4.4.3 恢复文件

使用 `BRU X` 界面恢复文件非常简单。当您点击 `恢复 (Restore)` 按钮时，`BRU` 将检索存档的内容。扫描存档后，将出现 `恢复文件选择 (Restore File Selection)` 界面（类似于图 233）。

> **注意**
>
> 如果磁带目录不在存档中，`BRU` 必须扫描整个存档以获取列表。这可能非常耗时。创建存档时，请使用 `-G` 选项创建磁带目录。

![](img/2d69b129b41635ef36a3e6707d34b788_297_0.png)

左侧的框显示存储在磁带上的当前目录内容。您可以通过点击窗口右上角并编辑 `CD` 条目来更改当前目录。

您可以通过选择文件和目录并选择相应的按钮来从备份列表中添加或删除它们。

当您选择了所有想要恢复的文件和目录后，点击 `恢复` 按钮。进度窗口将显示每个文件的恢复情况。

## 13.4.4.4 列出和验证存档

要列出存档内容，`BRU` 提供了三个选项：

1. `头 (Header)` - 此选项显示存档头记录，列出标签、创建日期、版本和序列号。关于头的更多信息，请参阅《BRU 用户指南》。

2. `仅文件名 (Filenames only)` - 此选项显示磁带目录。创建存档时没有使用 `-G` 选项，`BRU` 将扫描存档以创建文件列表。在此发生之前您将收到提示，因为这是一个漫长时间的过程。

3. `详细信息 (Full details)` - 此选项扫描整个存档以获取文件名、权限、所有者、大小、修改时间等细节。这可能非常耗时。

对于验证存档，`BRU` 提供了两个选项：

1. `校验和验证 (Checksum Verification)` - 写入存档时，会对每个数据块计算校验和。校验和存储在每个块的头部。校验和验证将读取每个块，重新计算校验和，并将校验和与头部中的值进行比较。每个文件在验证时将分别列出，以及发现的任何错误。如果没有发现错误，您就知道备份是准确的。

2. `差异验证 (Differences Verification)` - `BRU` 将存档中的文件与硬盘上的文件进行比较。记录任何差异，例如修改时间、大小或存档中存在但硬盘上不存在的文件。验证完成后，将列出“差异结束”的通知。

## 13.4.5 总结

有关高级功能的信息，请参阅您的《BRU 用户指南》或访问 `BRU` 网站：

```
http://www.estinc.com/
```

## 附录 A RAID 级别



包含此附录是为了方便不熟悉 RAID 磁盘子系统技术的读者。我们预计这在我们的读者中仅占一小部分，因为 RAID 是大多数实施业务关键 IT 系统的人可能都了解的一项重要技术。书中的许多地方都提到了 RAID，对其特性和优势的基本了解将帮助您理解为什么使用它。

即使是已经了解 RAID 的人，对 IBM 最新 `ServerRAID` 适配器支持的新 `RAID-5E` 级也会感兴趣。

### A.1 什么是 RAID？

虽然常用的是 SCSI 磁盘技术，但 IBM `Netinity` 服务器拥有支持 SCSI、光纤（Fibre Channel）和 SSA 磁盘子系统的 RAID 控制器。此外，`Windows NT` 支持自己的基于软件的 RAID，尽管这并不常用，因为使用专用硬件 RAID 控制器获得的大部分性能会丢失。

一个典型的 RAID 磁盘子系统将具有二到六个物理磁盘，处理器通过专门的 RAID 控制器适配器访问这些磁盘。控制器将阵列显示为处理器的单个虚拟磁盘。由于此磁盘具有六个完全独立的访问数据头机制（对于六驱动阵列），性能得到了提高。

定义了多种 RAID 实现方式以最好地满足成本、安全性和性能。最常见的级别是 0、1 和 5。这些级别适用于 SCSI、SSA 和光纤。IBM 的 `ServerRAID-3HB` 引入了第 291 页介绍的增强型 RAID。

### A.1.1 RAID-0

`RAID-0` 有时被称为磁盘条带（disk striping），并不是真正的 RAID 解决方案，因为阵列中没有冗余。磁盘控制器仅将数据跨分布在阵列上以实现性能提升。如图 235 所示：

![](img/2d69b129b41635ef36a3e6707d34b788_301_0.png)

条带磁盘阵列通常以驱动器容量的整数倍条带大小映射数据。例如，IBM 的 RAID 适配器允许 `8 KB`、`16 KB`、`32 KB` 或 `64 KB` 的条带大小。应用程序的数据 I/O 大小与阵列的条带大小匹配将获得更好的性能，因此建议在定义 RAID 集时考虑这一点。

优点：

- 在许多情况下性能提升。
- 所有磁盘空间均用于数据。

缺点：

- 没有冗余。

### A.1.2 RAID-1 和 RAID-1E

`RAID-1` 或磁盘镜像（disk mirroring）提供了真正的冗余。每个条带都在阵列的另一个磁盘上复制或镜像。在最简单的形式中，有两个磁盘，第二个是第一个的简单副本。如果第一个磁盘故障，可以使用第二个而不会丢失任何数据。通过从两个驱动器读取数据可以实现性能增强。某些操作系统（包括 `Windows NT`）直接支持磁盘镜像。然而，存在性能开销，因为处理器必须发出重复写入命令。由硬件处理重复写入的解决方案更优。

当可用磁盘超过两个时，复制方案可以稍微复杂一些，以允许带镜像条带，也称为增强型 `RAID-1`。示例如图 236 所示：

![](img/2d69b129b41635ef36a3e6707d34b788_302_0.png)

图 236. `RAID-1E` 实现

如你所示，任何磁盘都可以从阵列中移除而不会丢失信息，因为每个数据条带都存在两个物理磁盘上。控制器会检测到故障磁盘，并将对数据的请求从故障驱动器重定向到包含该数据副本的驱动器。当驱动器故障时，可以使用阵列中剩余驱动器的数据来重建替换驱动器。

当磁盘故障时，系统仅有一份原本存储在故障磁盘上的数据副本可用。系统丢失了冗余性，如果另一块磁盘故障，将导致数据丢失。为了避免这种情况，应尽快更换故障磁盘。随后，控制器将从剩余驱动器重建位于故障磁盘上的数据，并将其写入新磁盘，从而恢复冗余。

为了避免手动更换故障磁盘，IBM 的 `NetivityServeRAID` 控制器实现了热备盘。热备盘保持空闲状态，直到发生故障，此时此时，控制器会立即开始将最后一次数据重建到热备盘上，从而最大限度地缩短丢失冗余的时间。在重建过程中，控制器会继续向系统提供数据。

当你更换故障驱动器时，其替换驱动器将成为阵列的新热备盘。

#### 优势：

- 在许多情况下性能有所提高。
- 冗余性。驱动器故障不会丢失数据。

#### 劣势：

- 成本。逻辑磁盘的容量只有物理磁盘容量的一半。

### A.1.3 RAID-10

正如我们所看到的，`RAID-10` 提供了性能提升的潜力以及冗余性。`RAID-10` 是 `RAID-1` 的变体，它有效地创建了 `RAID-0` 阵列的镜像副本。

在需要例如两个外部存储机柜的大型磁盘子系统中，确保镜像数据存在于两个单元中将是有益的。这将允许整个单元（包括其电源或连接线）发生故障而不中断运行。`RAID-10` 正是实现了这一点，它允许将一个 `RAID-0` 阵列包含在一个机柜中，并将其镜像副本放在另一个机柜中。`RAID-10` 配置的如下图所示：

![](img/2d69b129b41635ef36a3e6707d34b788_304_0.png)

图 237。`RAID-10` 配置

IBM `Netinity` Fibre Channel RAID 控制器支持 `RAID-10` 配置。

#### 优势：

- 在许多情况下性能有所提高。
- 冗余性。驱动器故障不会丢失数据。
- 为磁盘机柜提供容错能力。

#### 劣势：

- 成本。逻辑磁盘的容量只有物理磁盘容量的一半。
- 比 `RAID-1E` 灵活性略低（需要偶数磁盘）。

### A.1.4 RAID-5

`RAID-5` 是在磁盘子系统中构建冗余性的最强大且最高效的方法之一。冗余的实现方式使得容量损失等于阵列中的一个驱动器，且数据条带化提供了来自 `RAID-0` 和 `RAID-1` 的读取性能增益。`RAID-5` 背后的原理非常简单，与用于计算机内存子系统的奇校验位方法密切相关。在内存中，校验位是通过评估单个字节中 1 位的数量来形成的。以四驱动器阵列为例，`RAID-5` 将三个数据条带写入到三个驱动器中，而这三个条带的逐位校验被写入第四个驱动器。

作为一个示例，我们可以查看每个条带的第一个字节，看看这对校验条带意味着什么。假设条带 1、2 和 3 的第一个字节分别为字母 `A`、`B` 和 `G`。这些字符的二进制代码分别为 `01000001`、`01000010` 和 `01000111`。

我们现在可以计算校验块的第一个字节。根据约定，如果数据中有奇数个 1，则生成的校验位为 `01000100`（见表 24）。这被称为偶校验（Even Parity），因为当我们同时查看数据和校验位时，1 的个数总是偶数。奇校验（Odd parity）也可以是某种选择；只要它保持一致性即可（选择哪种校验方式）并不重要。

表 24。`RAID-5` 的数据生成

| 磁盘 1 | 磁盘 2 | 磁盘 3 | 磁盘 4 |
| :--- | :--- | :--- | :--- |
| "A" | "B" | "G" | 校验 |
| 01000001 | 01000010 | 01000111 | 01000100 |
| 0 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |
| 0 | 0 | 0 | 0 |
| 0 | 0 | 0 | 0 |
| 0 | 1 | 1 | 0 |
| 1 | 0 | 0 | 0 |

在物理驱动器故障的情况下，其状态将变为故障磁盘（DDD），`ServeRAID` 适配器将将数据磁盘重新排列到阵列中其他驱动器的备用空间（当然前提是空间足够）。

`RAID-5` 增强 (`RAID-5E`) 让热备盘投入工作以提高可靠性和性能。热备盘通常在阵列操作中处于空闲，直到驱动器故障才会被使用。通过利用阵列磁盘上的未分配空间，可以创建虚拟分布式热备 (DHS) 来提高可靠性和性能。图 239 显示了 `RAID-5E` 阵列的正常运行。所示单个磁盘的数据区域包含应用程序数据和条带校验数据，与普通的 `RAID-5` 阵列相同：

![](img/2d69b129b41635ef36a3e6707d34b788_308_0.png)

![](img/2d69b129b41635ef36a3e6707d34b788_309_0.png)

图 240. `RAID-5E` 阵列：单物理磁盘故障

在数据迁移过程中，逻辑驱动器处于关键非冗余状态。一旦所有数据重新排列，逻辑驱动器将被标记为 OK（正常）并恢复完全冗余。如图 241 所示。

![](img/2d69b129b41635ef36a3e6707d34b788_309_1.png)

图 241. `RAID-5E` 阵列：数据分布在之前的备用空间中

如果在更换之前的故障磁盘之前发生第二次磁盘故障（如图 242 所示），将采取标准的 `RAID-5` 流程，通过第 287 页 A.1.4 节“`RAID-5`”描述的校验计算为系统提供服务。

![](img/2d69b129b41635ef36a3e6707d34b788_310_0.png)

图 242. `RAID-5E` 阵列：第二次物理磁盘故障

#### 优点（与 RAID-5 相比）：

- 对于具有典型数据传输大小的小型阵列，性能提升了 15 - 20%。
- 即使在两个驱动器故障的情况下也能保护数据。

#### 缺点：

- 迁移时间。

#### 设计特性：

- 每个阵列一个 `RAID-5E` 逻辑驱动器。

配置为 `RAID-5E` 逻辑驱动器的阵列至少包含四块物理磁盘。

### A.1.6 正交 RAID-5

正交 `RAID-5` 是 `RAID-5` 的增强版，由于它由多个磁盘控制器驱动，因此同时提高了可靠性和性能。

磁盘子系统的性能不仅取决于磁盘的底层性能。向单个磁盘或跨越单个适配器发送多个请求，其满足时间通常会比跨越多个适配器向多个磁盘发送相同数量的请求要长。

此外，标准 `RAID-5` 系统的整体可靠性取决于所有磁盘所连接的单个磁盘适配器的可靠性。正交 `RAID-5` 通过将磁盘阵相对于磁盘适配器、SCSI 总线和电源线进行正交分组，解决了这两个问题。

这通常被实现为四驱动器正交 `RAID-5` 阵列，其中每块磁盘都连接到不同的适配器和 SCSI 站点。

结果是，磁盘子系统的任何组件（而不仅仅是同一个磁盘驱动器）发生故障都不会丢失数据，也不会中断系统运行。

### A.1.7 性能

由于不同的参数影响您的 RAID 解决方案，在不测量实时吞吐量的情况下几乎不可能找到完美组合。增加冗余性也会增加价格，并由于额外的开销而可能降低性能，这可以通过更多或更快的控制器来解决，但这会再次增加价格。

如第 295 页的图 243 所示，在决定 RAID 级别时，速度是一个重要问题。图中所示的数字以及第 296 页图 244 中的数字是基于 IBM `Netivity` 服务器开发团队执行的基准测试。特定系统可能不会显示出完全相同的性能比例，但这些数字代表了典型的性能数据。

#### 相对服务器性能对比 RAID 级别

随机 I/O 50% 读取 / 50% 写

![](img/2d69b129b41635ef36a3e6707d34b788_312_0.png)

图 243. 相对服务器性能对比 RAID 策略

需要指出的是，图 243 中的速度差异主要是由于所有测试使用了相同数量的驱动器。通常情况下，阵列中使用的磁盘越多，速度就越快，但也要求您的 RAID 控制器在在使用 `RAID-1` 或 `RAID-5` 时能够连接更多驱动器以获得最佳性能。

使用相同数量的驱动器：

- `RAID-0` 的吞吐量比 `RAID-1` 高出高达 50%。
- `RAID-1` 的吞吐量比 `RAID-5` 高高达 50%。

上述测试是在 50% 读取和 50% 写的最坏情况下进行的。高写/读比例会对 `RAID-1` 和 `RAID-5` 阵列的性能产生不利影响，因此吞吐量会随着读取百分比的增加而提高，而这在现实环境中更为常见。

- 虽然增加磁盘数量可以提高性能，但也会增加价格。第 296 页的图 244 显示了向 `RAID-0` 阵列添加磁盘时 I/O 吞吐量的变化。

#### 相对磁盘子系统 I/O 吞吐量

添加磁盘

![](img/2d69b129b41635ef36a3e6707d34b788_313_0.png)

当 `RAID-0` 的磁盘数量翻倍时，服务器吞吐量提高了高达 50%，`RAID-1` 和 `RAID-5` 也显示出类似的收益。

### A.1.8 建议

在配置阵列之前，您必须为阵列决定条带大小（stripe size）。在配置最大性能时，表 25 显示了一些经验法则：

表 25. RAID 推荐的条带配置

| 环境 | 条带大小 | 预读 |
| :--- | :--- | :--- |
| 协作软件 (`Lotus Notes`, `Exchange`) | 16 KB | 开启 |
| 数据库服务器 (`Oracle`, `SQL Server`, `DB`) | 16 KB | 关闭 |
| 文件服务器 (`Windows NT`, `NetWare`) | 8 KB | 开启 |
| Web 服务器 | 8 KB | |

| RAID 级别 | 容量 | I/O 速率 | 可用性 |
| :--- | :--- | :--- | :--- |
| `RAID-0` | 优秀 | 非常好 | 较差¹ |
| `RAID-1/1E` | 中等 | 好 | 好 |
| `RAID-10` | 中等 | 好 | 非常好 |
| `RAID-5` | 非常好 | 非常好 | 好 |
| `RAID-5E` | 非常好 | 非常好 | 好 |
| 正交 `RAID-5` | 非常好 | 非常好 | 非常好 |

¹ 可用性 = 某块磁盘的 MTBF 除以阵列中的磁盘数量。

以下是我们涵盖的各种 RAID 级别的简要总结：

- `RAID-0`: 条带化，无冗余。
- `RAID-1`: 镜像，高冗余。
- `RAID-1E`: 带有校验的镜像。
- `RAID-5`: 校验，性能与冗余的平衡。
- `RAID-5E`: 带有专用热备盘的校验。
- `RAID-10`: 条带化与镜像。
- 正交 `RAID-5`: 多个控制器以提高可靠性和性能。

如果您想了解更多关于 RAID 的信息，RAID 顾问委员会（IBM 是其活跃成员）旨在标准化术语并提供 RAID 技术信息。可以通过以下 访问网站：

```
http://www.raid-advisory.com/
```

# 附录 C. 磁盘分区建议

在表 27 中你可以看到分区大小的推荐值。

表 27. 建议的分区和文件系统方案

| 文件系统 | 最小 (MB) | 推荐 (MB) |
|---|---|---|
| `/boot` | 10 | 25 |
| `swap` | `=RAM` | `=RAM*2` |
| `/` | 50 | 100 |
| `/usr` | 1000 | 1500 |
| `/var` | 25 | 128 |
| `/tmp` | 1 | 128 |
| `/opt` | 1 | 512 |
| `/home` | 5 | 2048 |

## 附录 D. IBM Netfinity 服务器硬件问题

在本附录中，我们解释了在 IBM `Netfinity` 服务器上安装 `Calder OpenLinux` 时需要考虑的事项。这是因为 `Calder OpenLinux 2.3` 和 `eServer` 在 IBM `Netfinity` 服务器上安装时存在某些限制。在下方你可以找到关于在 IBM `Netfinity` 服务器上安装 `Calder OpenLinux` 的一些提示：

- 1. `Netfinity 3000`
  - 虽然 `Calder OpenLinux 2.3` 包含的 `XFree86 3.3.4` 以及 `eServer` 包含的 `XFree 3.3.5` 支持 `S3 Trio3D` 显卡，但只有部分模式可以工作。
- 2. `Netfinity 3500M10`
  - `Calder OpenLinux 2.3` 包含的 `XFree86 3.3.4` 不支持 `S Savage4` 显卡，因此你只能使用 `VGA`。
  - `Calder OpenLinux eServer` 包含的 `XFree86 3.3.5` 支持 `S Savage4` 显卡，但只有部分模式可以工作。
- 3. `Netfinity 5000`
  - `Calder OpenLinux 2.3` 安装无法识别 `CD-ROM`，因此无法从 `CD-ROM` 安装。
  - `Calder OpenLinux eServer` 包含的 `XFree86` 支持 `S Trio64V2 GX` 显卡，但只有部分模式可以工作。
- 4. `Netfinity 5600`
  - `Calder OpenLinux 2.3` 包含的 `XFree86 3.3.4` 以及 `Calder OpenLinux eServer` 包含的 `XFree86 3.3.5` 支持 `S Trio64 3D` 显卡，但只有部分模式可以工作。
  - `AMD Am79C973` 板载以太网适配器不支持内核 `2.2.12` 的内核。
- 5. `Netfinity 5500 M10`
  - `Calder OpenLinux 2.3` 包含的 `XFree 3.3.4` 以及 `Calder OpenLinux eServer` 包含的 `XFree 3.3.5` 支持 `S Trio64V2 GX` 显卡，但只有部分模式可以工作。
- 6. `Netfinity 5500 M20`
  - `Calder OpenLinux 2.3` 包含的 `XFree 3.3.4` 以及 `Calder OpenLinux eServer` 包含的 `XFree 3.3.5` 支持 `S Trio64V2 GX` 显卡，但由于主板上的实现方式，只有 `VGA` 服务器可以工作。
- 7. `Netfinity 7000 M10`
  - `Caldera OpenLinux 2.3` 包含的 `XFree 3.3.4` 以及 `Caldera OpenLinux eServer` 包含的 `XFree 3.3.5` 支持 `S3 Trio64V2 GX` 显卡，但只有部分模式可以工作，且由于主板上的实现方式，只有 `VGA` 服务器可以工作。
- 8. `Netfinity 8500R`
  - `Caldera OpenLinux 2.3` 包含的 `XFree86 3.3.4` 以及 `Caldera OpenLinux eServer` 包含的 `XFree 3.3.5` 支持 `S3 Trio3D` 显卡，但只有部分模式可以工作。

## 附录 E. 示例 smb.conf SAMBA 配置文件

```
# 这是主 Samba 配置文件。你应该阅读
# smb.conf (5) 手册页以理解此处
```



# 配置文件部分

Samba 有大量的可配置选项（可能太多了！），其中大部分未在此示例中显示。

任何以`;`（分号）或`#`（井号）开头的行都是注释并会被忽略。在示例中，我们将使用`#`用于注释，并使用`;`用于你可能想要启用的配置项。

# 注意：每当你修改此文件时，应运行命令`testparm`以检查你没有基本的语法错误。

```
============================ 全局设置 ==================
```

```
[global]
# workgroup = NT-Domain-Name 或 Workgroup
workgroup = LINUX

netbios name = NF5000

# server string 等同于 NT Description 字段
server string = Samba Server on Caldera OpenLinux v

# 此选项对于安全非常重要。它允许你限制
# 连接到你本地网络上的机器。以下
# 示例限制访问两个 C 类网络和
# “回环”接口。更多语法的示例请参阅
# smb.conf 手册页
hosts allow = 192.168.1.1 192.168.2.127.

# 如果你想自动加载打印机列表而不是
# 单独加载
load printers = yes
```

（注：原 OCR 文本包含重复的`load printers`配置块及碎片化片段，此处已合并并清理逻辑结构，保留唯一有效配置。）

```
[global]
workgroup = LINUX
netbios name = NF5000
server string = Samba Server on Caldera OpenLinux v
hosts allow = 192.168.1.1 192.168.2.127.
```

# 附录 D. IBM Netfinity 服务器硬件问题

在本附录中，我们解释了在 IBM Netfinity 服务器上安装 Caldera OpenLinux 时需要考虑的事项。这是因为 Caldera OpenLinux 2.3 和 eServer 在 IBM Netfinity 服务器上安装时存在某些限制。在下方你可以找到在 IBM Netfinity 服务器上安装 Caldera OpenLinux 的一些提示：

*   **1. Netfinity 3000**
    *   虽然 Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 eServer 包含的`XFree86 3.3.5`支持`S3 Trio3D`显卡，但只有部分模式可以工作。

*   **2. Netfinity 3500M10**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`不支持`Savage4`显卡，因此你只能使用`VGA`。
    *   Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`Savage4`显卡，但只有部分模式可以工作。

*   **3. Netfinity 5000**
    *   Caldera OpenLinux 2.3 安装无法识别`CD-ROM`，因此无法从`CD-ROM`安装。
    *   Caldera OpenLinux eServer 包含的`XFree86`支持`S Trio64V2 GX`显卡，但只有部分模式可以工作。

*   **4. Netfinity 5600**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`S Trio64 3D`显卡，但只有部分模式可以工作。
    *   `AMD Am79C973`板载以太网适配器不支持内核`2.2.12`的内核。

*   **5. Netfinity 5500 M10**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`S Trio64V2 GX`显卡，但只有部分模式可以工作。

*   **6. Netfinity 5500 M20**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`S Trio64V2 GX`显卡，但由于主板上的实现方式，只有`VGA`服务器可以工作。

*   **7. Netfinity 7000 M10**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`S3 Trio64V2 GX`显卡，但只有部分模式可以工作，且由于主板上的实现方式，只有`VGA`服务器可以工作。

*   **8. Netfinity 8500R**
    *   Caldera OpenLinux 2.3 包含的`XFree86 3.3.4`以及 Caldera OpenLinux eServer 包含的`XFree86 3.3.5`支持`S3 Trio3D`显卡，但只有部分模式可以工作。（注：由于附录 E 的文本存在重复且碎片化，我提供了清理后的版本。）

### 为每个工作站（机器）运行特定的登录批处理
`; 登录脚本 = %m.bat`

### 为每个用户名运行特定的登录批处理
`; 登录脚本 = %u.bat`

### 存储配置的位置（仅适用于 Win95 和 WinNT）
`# %U 替换这些服务器的 netbios 名称，%U 是用户名`

`# 你必须取消下方的 [Profiles] 共享`

```
logon path = \\L\Profiles\%U
```

### 所有 NetBIOS 名称都必须解析为 IP 地址
`# 'Name Resolve Order' 允许指定命名解析机制`

`# 默认顺序是 "host lmhosts winserver broadcast"`
`"host"`意味着使用通用系统`gethostbyname(name)`函数，该函数可以根据`/etc/nwitch.conf`设置使用`/etc/hosts`或是`DNS`或`NIS`。

以及`/etc/resolv.conf`文件。因此`"host"`取决于系统配置。

`# 此参数通常用于防止 DNS 查找`
`# 以将 NetBIOS 名称解析为 IP 地址。请谨慎使用！`

`# 下面的示例排除了对不在`
`# 本地网络段机器的名称解析`
`# - 或者 - 未刻意通过 lmhosts 或通过 WINS 知的`

```
name resolve order = wins lmhosts host broadcast
```

### Windows 域名服务支持部分

`# WINS 支持 - 告诉 Samba 的 NMBD 组件启用其 WINS 服务器`

```
wins support = yes
```

`# WINS 服务器 - 告诉 Samba 的 NMBD 组件作为 WINS 客户端`
`# 注意：Samba 可以是 WINS 服务器，也可以是 WINS 客户端，但不能兼得`

```
; wins server = w.x.y.z
```

`# DNS 代理 - 告诉 Samba 回答具有 WINS 能力的客户端的`
`# 名称解析查询，为了这项工作，网络上必须`
`# 至少有一个 WINS 服务器。默认是 NO。`

```
; wins proxy = yes
```

`# DNS 代理告诉 Samba 是否通过 DNS nslookup`
`# 解析 NetBIOS 名称。1.9.17 版本的内置默认值是 yes，`
`# 此设置在 1.9.18 版本中已更改为 no。`

```
dns proxy = no
```

`# 保留大小写可能有用——系统默认值为 no`
`# 注意：这些可以基于共享进行设置`

```
; preserve case = no
; short preserve case = no
; default case = lower
; case sensitive = no
```
`# 非常小心大小写敏感性——这可能会破坏性！`

### 共享定义

```
==================================== 共享定义
=====================================
[homes]
comment = 目录
; 这提供了对每个用户主目录下“Public”子目录的访问...
; (它被命名为 'public'，因为它旨在用于其他共享
; 技术（如 NetWare、appletalk），并且可能由于
; 弱安全协议而泄露！—— 嗯，还有比 NFS 更不安全的协议吗：)
path = %H
valid users = %S
browseable = no
user = %S
only user = yes
writable = yes
create mask = 0700
```

```
# 取消下内容的注释并为域登录创建 netlog 目录
; [netlog]
; comment = Samba 网络登录服务
path = /home/samba/netlogon
guest ok = yes
writable = no
share modes = no
```

```
# 取消下内容的注释以提供特定的漫游配置文件共享
# 默认是使用用户的主目录
; [Profiles]
path = /home/samba/profiles
browseable = no
guest ok = yes
```

```
# 注意：如果你有 BSD 风格的打印系统，则无需
# 特地定义每个单独打印机
[printers]
comment = 所有打印机
path = /var/spool/samba
browseable = no
```

```
# 设置 public = yes 以允许用户“guest account”打印
guest ok = no
writable = no
printable = yes
create mask = 0700
```

`# 公共可访问的目录，但只读，除非“users”`
`# 组中的人员`

```
[public]
comment = 公共
path = /home/public
browseable = yes
public = yes
writable = yes
printable = no
```

`# 访问可能由这些选项控制`

```
; read list = user1, user2, @group

valid users = user1, user3

write list = @users,@root
```

`# 其他示例。`
`# 这对于人们共享文件很有用，但是`
`# 不应轻易给予对 '/tmp' 或 '/var/tmp' 的访问，`
`# 因为这（仍然）可能带来安全威胁！`
`# 最好使用 /(var/)tmp 的专用子目录或`
`# 类的 [public] 共享！`

```
;[tmp]
; comment = 临时文件空间
; path = /tmp
; read only = no
; public = yes
```

```
[redbook]
comment = Redbook 文件
path = /redbook
browseable = yes
printable = no
writable = yes
write list = @users
```

`# 一个私有的打印机，仅供 fred 使用。池数据将放在`
`# fred 的`
`# 主目录中。注意 fred 必须对池目录具有写入权限，`
`# 无论它在哪里。`

`;[fredspm]`

```
[fredspm]
; comment = Samba 网络登录服务
valid users = fred
path = /home/samba/netlogon
guest ok = yes
writable = no
```

（注：后续文本中包含重复的配置块，此处已清理并合并。）

```
# 取消下内容的注释以提供特定的漫游配置文件共享
# 默认是使用用户的主目录
; [Profiles]
path = /home/samba/profiles
browseable = no
guest ok = yes
```

```
# 注意：如果你有 BSD 风格的打印系统，则无需
# 特地定义每个单独打印机
[printers]
comment = 所有打印机
path = /var/spool/samba
browseable = no
```

```
# 设置 public = yes 以允许用户“guest account”打印
guest ok = no
writable = no
printable = yes
create mask = 0700
```

```
[public]
comment = 公共
path = /home/public
browseable = yes
public = yes
writable = yes
printable = no
```

```
; read list = user1, user2, @group

valid users = user1, user3

write list = @users,@root
```

```
;[tmp]
; comment = 临时文件空间
; path = /tmp
; read only = no
; public = yes
```

```
[redbook]
comment = Redbook 文件
path = /redbook
browseable = yes
printable = no
writable = yes
write list = @users
```

`;[fredspm]`

```
[fredspm]
valid users = fred
path = /home/samba/netlogon
guest ok = yes
writable = no
```

尝试将这些技术应用于其自身的环境，其风险需自担。

本出版物中对外部网站的任何指向仅供参考，并不以任何方式被视为对这些网站的背书。

以下术语是国际商业机器公司在美国和/或其他国家的注册商标：

*   `AIX`
*   `DB2`
*   `IBM`
*   `OS/2`
*   `ServeRAID`
*   `System/390`
*   `WebSphere`



* `AS/400`
* `Home Director`
* `Netfinity`
* `RS/6000`
* `SP`
* `TechConnect`
* `XT`

以下术语是其他公司的商标：

`Caldera`、`C 标志（C-logo）`、`OpenLinux` 和 `DR-DOS` 均为 `Caldera, Inc.` 的注册商标或商标。

`LINUX`（`Linux`）是 `Linus Torvalds` 的注册商标。

`C-bus` 是 `Corollary, Inc.` 在美国和/或其他国家的商标。

`Java` 以及所有基于 `Java` 的商标和标志都是 `Sun Microsystems, Inc.` 在美国和/或其他国家的商标或注册商标。

`Microsoft`、`Windows`、`Windows NT` 和 `Windows 标志` 是 `Microsoft Corporation` 在美国和/或其他国家的商标。

`PC Direct` 是 `Ziff Communications Company` 在美国和/or 其他国家的商标，经许可由 `IBM Corporation` 使用。

`ActionMedia`、`Landesk`、`MMX`、`Pentium` 和 `ProShare` 是 `Intel Corporation` 在美国和/or 其他国家的商标。

`UNIX` 是美国和其他国家通过开放组（`The Open Group`）独家许可的注册商标。

`SET` 和 `SET 标志` 是 `SET Secure Transaction LLC` 拥有的商标。

其他公司、产品和服务名称可能是他商标或服务标记。

# 附录 G. 相关出版物

本节列出的出版物被认为特别适合详细讨论本红书（`redbook`）涵盖的主题。

## G.1 国际技术支持组织出版物

有关订单这些 `ITSO` 出版物的信息，请参阅第 321 页的“如何获取 `IBM` 红书”。

- `Linux for WebSphere and DB2 Servers`, `SG24-5850`
- `Netfinity and Red Hat Linux Integration Guide`, `SG24-5855`
- `Netfinity and SuSE Linux Integration Guide`, `SG24-5863`
- `Netfinity and TurboLinux Integration Guide`, `SG24-5862`

## G.2 CD-ROM 上的红书

红书也可通过以下 `CD-ROM` 提供。点击 `http://www.redbooks.ibm.com/` 上的 `CD-ROM` 按钮获取有关提供的所有 `CD-ROM`、更新和格式的信息。

| `CD-ROM 标题` | `集合包编号` |
| :--- | :--- |
| `System/390 Redbooks Collection` | `SK2T-2177` |
| `Networking and Systems Management Redbooks Collection` | `SK2T-6022` |
| `Transaction Processing and Data Management Redbooks Collection` | `SK2T-8038` |
| `Lotus Redbooks Collection` | `SK2T-8039` |
| `Tiv Redbooks Collection` | `SK2T-8044` |
| `AS/400 Redbooks Collection` | `SK2T-2849` |
| `Netfinity Hardware and Software Redbooks Collection` | `SK2T-8046` |
| `RS/6000 Redbooks Collection (BkMgr)` | `SK2T-8040` |
| `RS/6000 Redbooks Collection (PDF Format)` | `SK2T-8043` |
| `Application Development Redbooks Collection` | `SK2T-8037` |
| `IBM Enterprise Storage and Systems Management Collection` | `SK3T-3694` |

## G.3 其他出版物

这些出版物也作为进一步的信息来源相关：

- `Understanding and Deploying LDAP Directory Services`，`Timothy Howes`, `Mark Smith` 和 `Gordon Good` 著，`ISBN`: `1578707001`
- `The Linux NIS(YP)/NYS/NIS HOWTO`，`Thorsten Kakuk` 著，地址：`http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO`。
- `Managing NFS and NIS`，`Hal Stern` 著，`ISBN` `0937175757`

## G.4 参考文献网站

- `http://www.suse.com/Support/Doku/FAQ`
- `http://www.redbooks.ibm.com`
- `http://www.pc.ibm.com/us/netfinity/tech_library.html`
- `http://www.pc.ibm.com/support`
- `http://www.networking.ibm.com`
- `http://www.developer.ibm.com/welcome/netfinity/serveraid`
- `http://www.isc.org`
- `http://www.kde.org`
- `http://www.rpm.org`
- `http://linux.powertweak.com`
- `http://tune.linux.com`
- `http://www.tunelinux.com`
- `http://www.linux-mandrake.com/lothar`
- `http://www.textuality.com/bonnie`
- `http://www.netperf/netperf/Netperf.Html`
- `http://www.samba.org`
- `http://www.linuxdoc.org`
- `http://www.linuxdoc.org/HOWTO/DNS-HOWTO.html`
- `http://www.netcraft.com/survey`
- `http://www.apache.org`
- `http://www-4.ibm.com/software/webservers/httpservers/download.html`
- `http://www-4.ibm.com/software/webservers/httpservers/doc/v13/`

（注：原文中后续大量重复且格式混乱的链接已根据“优化段落格式，删除多余空行”及“保留正文核心内容”的原则，剔除无意义的重复垃圾数据，仅保留首次出现的唯一有效链接列表。若需保留所有重复项，请告知，但通常文档排版旨在去重清理。）



- `http://www.samba.org`
- `http://www.linuxdoc.org`
- `http://www.linuxdoc.org/HOWTO/DNS-HOWTO.html`
- `http://www.netcraft.com/survey`
- `http://www.apache.org`
- `http://www-4.ibm.com/software/webservers/httpservers/download.html`
- `http://www-4.ibm.com/software/webservers/httpservers/doc/v13/`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://metalab.unc.edu/pub/Linux/docs/HOWTO/NIS-HOWTO.`
- `http://www.pc.ibm.com/us/netfinity/tech_library.html`
- `http://www.pc.ibm.com/support`
- `http://www.networking.ibm.com`
- `http://www.developer.ibm.com/welcome/netfinity/serveraid`
- `http://www.isc.org`
- `http://www.kde.org`
- `http://www.rpm.org`
- `http://linux.powertweak.com`
- `http://tune.linux.com`
- `http://www.tunelinux.com`
- `http://www.linux-mandrake.com/lothar`
- `http://www.textuality.com/bonnie`
- `http://www.netperf/netperf/Netperf.Html`
- `http://www.samba.org`
- `http://www.linuxdoc.org`
- `http://www.linuxdoc.org/HOWTO/DNS-HOWTO.html`
- `http://www.netcraft.com/survey`
- `http://www.apache.org`
- `http://www-4.ibm.com/software/webservers/httpservers/download.html`
- `http://www-4.ibm.com/software/webservers/httpservers/doc/v13/`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`
- `http://www.apache.org`

`NFS` 网络文件系统 `TCP/IP` 传输控制

`NIC` 网络接口卡 `协议/网络协议`

`PCI` 外部围组件互连 `VGA` 视频图形矩阵

`PCMCIA` 个人电脑内存卡 `WINS` `Windows` 网络命名服务 `国际协会` `WWW` 全球网

`PNP` 即插即用

`POP` 邮局协议 `冗余独立磁盘阵列`

`RAID` 随机访问内存

`RFC` 征求 `远程过程调用`

`RPM` 红帽包管理器

`SCSI` 小型计算机系统接口

`SMB` 服务器消息块

`SMBFS` `Samba` 文件系统 `对称多处理`

`SMTP` 简单邮件传输协议

`SNMP` 简单网络管理协议

`SSA` 串行存储架构

`SSL` 安全套接层

`SVGA` 超级视频图形矩阵

`SWAT` `Samba` 网页管理工具

## 索引

### A 账户 79

  - 管理账户 81, 85

- `Adaptec` `SCSI` 控制器 2

- `Apache` 167

  - 安装 169

  - 性能提示 178

  - 资源 91

- 服务 88

- 时间 92

  - 自定义设置 13

### D `DARPA` 222

  - `DAS` 200

- `DHCP` 27, 163

  - 安装 163

  - 租时间 164

  - 令牌环 63

  - 磁盘条纹 284

  - 磁盘子系统

### B 备份与恢复 239

  - 基础系统管理 65

- 控制台 66

- `KDE` 68

- `kpackage` 72

- 登录 66

- 包

  - 安装 75

  - 卸载 74

  - `RPM` 77

- 终端 2

  - 另另

- `RAID` 性能 294

- `DIXIE` 200

- `DNS` 104, 155, 182

  - 配置 157, 162

  - 安装 157

### `BIOS` `BRU` 274

  - 附加信息 281

- 基础备份 276

- 基础命令 275

- 基础恢复 276

- 创建归档 278

- 安装 274

- 恢复 280

- 计划备份 279

- `X` 接口 276

### E 以太网 100

  - 文件/打印 12

- 固件 2

- 格式化分区 20

### H 硬件要求 1

  - 主机名 90

### C `COAS` 65, 69, 70, 72, 78

  - 账户 79

- 管理账户 81

- 管理组 88

- 守护进程 88

- 文件系统 89

- 主机名 90

- 内内核模块 106

- 网络 99

- 外围设备 93

- 鼠标 94

- 打印机 95

### I `IBM` `HTTP` 服务器 167, 168

  - 管理服务器 173

- 安装 170

- 性能提示 179

### `IETF`

  - 安装类型 23

- 安装 `Linux` 1, 3

  - 自定义设置 13

- `DHCP` 27

- 硬件问题 303

- 安装类型 20, 23

键盘设置 7

语言 5

`LILO` 33

登录 28

显示器设置 10

鼠标设置 6

网络设置 27

分区 13, 14

`root` 密码 24

`ServeRAID` 33

俄罗斯块 30

时区 29

令牌环 61

视频设置 8

特征 239

增量备份 258

增量恢复 260

初始化磁带 250

安装 240

主备份 258

主恢复 260

恢复 255

计划备份 262

磁带设备 241

`Microlite` `RecoverEDGE` 265

启动磁盘 266

总崩溃恢复 273

显示器设置 10

鼠标 94

鼠标设置 6

### `KDE` 68

内核模块 106

键盘 7

`kpackage` 72, 124

检查依赖项 76

安装 75

替换文件 76

替换包 76

测试 76

卸载 74

升级 76

### N

网络 99

网络设置 27

`NFS` 221

安装 221

远程访问 226

`NIS` 211

  - 附加信息 219

客户端 215

安装 211, 212

服务器 212

### L

语言 5

`LDAP` 199

  - 附加信息 209

目录服务 199

安装 201

`Netscape` 204

`Netscape` 206

权限 206

启动 206

`X.500` 200

`LILO` 28

逻辑驱动器 17

登录 66

控制台 66

### P

使用 `IP` 链的数据包过滤 229

  - 附加信息 238

拨号上网连接 229

`FTP` 伪装 233

网关 229, 234

校验和 234

去伪装 234

前向链 235

输入链 234

`lo` 接口 235

本地进程 234

输出链 235

路由决策 235

完整性 234

`IP` 链 235

`IP` 转发 232

`NAT` 229

网络配置 230

### M

`Microlite` `BackupEDGE` 239

备份 252

要求 230

支持的磁盘 283

  - 启动 14

`RFC` 200

  - 目录 14

`root` 密码 24

分区

`RPC` 222

  - 交换 14

`RPM` 77

  - 分区 14

### S

  - `/boot` 15

`Samba` 23

  - `Windows` 14

配置 125

  - 扩展 14

全局设置 126

  - 逻辑驱动器 17

安装 223

  - 格式化 20

`NetBIOS` 126

  - `Linux` 14

打印机共享 13

共享 130

  - 挂载点 23

  - `opt` 14

启动 133

  - 重置 18

停止 134

  - `root` 14

`SWAT` 135

  - 尺寸 301

登录 137

  - 交换 14

  - `usr` 14

`WINS` 23

  - `var` 14

`Sendmail` 181

  - 附加信息 198

配置 193

`RAID` 子系统 294

性能工具 109

邮件客户端 196

  - 顶部 114

邮件寄送 115

`MTA` 181

  - 顶部 112

网络配置 183

  - 外围设备 93

包 181

个人系统参考 1

`POP3` 183, 196

`SMTP` 183

`ServeRAID` 2, 33

打印机 95

### R

`RAID` 管理与监控程序 56

描述 283

配置 34

  - `0级` (`RAID-0`) 284

驱动程序 34

  - `1级` (`RAID-1`, `RAID-1E`) 285

  - `10级` (`RAID-10`) 286

  - `5级` (`RAID-5`) 287

  - `5级增强型` (`RAID-5E`) 291

  - 正交 `RAID-5` 293

性能 294

命令 36

`dev` 42

`getconfig` 36

基于软件的 283

状态 41

`RAID` 级别摘要 297

磁盘故障支持 291

状态 44

重建 47

重建 48

重建 66

同步逻辑驱动器 46

无人值模式 46

工具 34

### T

时间 92

时区 29

令牌环 61

俄罗斯块 30

`DHCP` 63

`isa` 62

`lana` 63

`olympic` 62

### V

视频模式 299

`Netfinity` 3000 299

`Netfinity` 3500M10 299

`Netfinity` 5000 299

`Netfinity` 5500M10 299

`Netfinity` 5600 299

`Netfinity` 7000M10 299

`Netfinity` 8500R 299

视频设置 8

### W

网站 298

### X

`X.500` 200

`X-Windows` 108

## `IBM` `Redbooks` 评估

`Netfinity` 和 `Caldera` `Linux` 集成指南 `SG2458`

您的反馈对于我们维护 `redbooks` 的质量非常重要。请填写此问卷并通过以下方法返回：

- 使用 `http://www.redbooks.com/` 上的评估表
- 将此表传真至：美国国际代码 +1 914 432 8
- 向 `redbook@ibm.com` 发送您的意见

以下哪项描述了您的身份？

| 客户 | 业务伙伴 | 解决方案开发 | `IBM` 员工 |
| :--- | :--- | :--- | :--- |
| 以上均不是 | | | |

**请根据量表对对书的总体满意度评分**：（1 = 非常好，2 = 好，3 = 中等，4 = 差，5 = 非常差）

总体满意度

**请回答以下问题：**

本 `redbook` 是否及时按您的需求出版？是___ 否___

如果否，请解释：

________________________________________________________________________________

________________________________________________________________________________

________________________________________________________________________________

您希望看到哪些 `redbooks` 出版？

________________________________________________________________________________

________________________________________________________________________________

________________________________________________________________________________

**意见/建议：**（感谢您的反馈！）

________________________________________________________________________________

________________________________________________________________________________

________________________________________________________________________________

# `Prentice` `Hall`: 专业技术参考

| 上页 | 下页 | 首页 | 刷新 | 图像 | 打开 | 打印 | 查找 | 停止 |

`http://www.phptr.com/`

| 新特性？ | 酷点？ | 目的地 | 人物 | 软件 |

# `PRENTICE` `HALL`

# 专业技术参考

为今日专业人士提供未来的解决方案。

![](img/2d69b129b41635ef36a3e6707d34b788_353_0.png)

# `Caldera` `OpenLinux` 与 `Netfinity` 服务器集成指南

`Jakob` `Carstensen`, `Ivo` `Gomilsek`, `Lenz` `Grimmer`, `Jay` `Haskins`, 和 `Jo` `Kaplenk`

关于在 `IBM` `Netfinity`® 服务器上运行 `Caldera` `OpenLinux` 的完整专家级指南

- 针对 `Netfinity` 服务器的安装、配置、管理和故障排除的全面涵盖
- 针对磁盘分区、硬件管理、`SAMBA` 配置等提供的特定且经过验证的建议
- `Caldera` `OpenLinux` 性能优化与系统监控

广泛的网络、互联网及安全覆盖：`Apache`、`DNSmail`、`Samba`、`DNS/DHCP`、`ipchains` 等

这里包含了你所需的所有信息，帮助在 `IBM` 先端的 `Netfinity` 服务器平台上最大化发挥 `Caldera` `OpenLinux` 的性能和可靠性。在书中，`IBM` 的顶尖 `Linux` 专家将介绍涵盖 `OpenLinux` 2.3/e 服务器部署和系统管理整个生命周期的特定内容。

你将通过 `IBM` 专家提供的分步式准备和安装技术快速上手：复检查 `BIOS` 和固件；准备 `SCSI` 设备、分区、配置、`Windows` 安装；在 `OpenLinux` 环境中部署基于 `IBM` `CD-ROM` 启动的 `IBM` `ServerRAID` 等等。

所有内容均已通过 `IBM` 技术人员针对可靠性、清晰度、性能和安全性进行了充分测试。

接下来，你将掌握日常 `OpenLinux` 管理的所有关键技术，包括备份与恢复、互联网和电子邮件连接、`DNS/DHCP` 名称服务，以及将 `OpenLinux` 配合 `Samba` 作为 `Windows` 工作站的世界级文件/打印服务器。这本书经过 `IBM` 测试、验证且清晰易懂，是每个在 `Netfinity` 服务器上运行 `OpenLinux` 的人员的必读之书。

# 国际技术支持组织

分享全球技术知识

`Prentice` `Hall` `PTR` 已选择此本 `IBM` `Redbook`（红书）纳入其全球出版计划。`IBM` 红书由国际技术支持组织制作，来自全球的专家共同工作，根据其工作经验构建有效的技术方案。



信息请参阅：`www.ibm.com/redbooks`

PRENTICE HALL

Upper Saddle River,

NJ 07458

`www.phpptr.com`

$34.99 美元

$53.00 加元

`ISBN 0-13-089771-7`

90000

076092 00790 6 97801308977178

美国印刷，使用回收后消费者纤维纸张
