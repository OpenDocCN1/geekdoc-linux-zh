
# Damn vulnerable web app
Damn Vulnerable App (`DVWA`) 是一个基于 `PHP/MySQL` 的故意留漏洞的应用程序。它的主要目标是帮助安全研究人员加固他们的应用程序。

## 攻击者机器
对于新手来说，下载并安装一个预配置的渗透系统比从零开始构建要好得多。`Kali` 发行版（以前称为 `Backtrack`）是免费提供的，并集成了许多典型的渗透工具。

## 介绍 Kali Linux
初学者在建立渗透实验室时的常见疑问是使用 Linux 还是 Windows 作为主系统。资深渗透测试者出于许多原因选择 Linux 作为他们的主系统。第一个原因是黑客工具的可用性，特别是 Linux 操作系统的开源属性使他们选择它而不是 Windows。然而，始终建议在渗透测试中同时拥有 Windows 和 Kali 盒子，因为每个平台可能提供不同的工具和功能。`Kali Linux` 绝对是伦理黑客最好的操作系统之一，因为它包含了一组分类良好的工具。`Kali Linux` 应该作为主操作系统安装在机器上，我们本节中讨论。

## 在虚拟机中安装 Kali Linux – VMware Workstation Player
`VMware Workstation Player` 是 `VMware Workstation Pro` 的功能限制免费版本。这意味着它就像 `VMware Workstation Pro`，但功能较少。然而，可用功能对于大多数用户来说足够了。`VMware Workstation Player` 是免费提供的。

`VMware Workstation Player` 的下载页面有所有可用下载选项：`https://www.vmware.com/in/products/workstation-player.html`。你可以从上述 URL 下载 `VMware Workstation Player` 并将其安装到你的系统中。

### 第一步 – 获取 Kali Linux ISO 镜像
为了安装 `Kali Linux`，我们必须获取安装 ISO 镜像文件。你可以通过访问下载页面获取它。根据你的系统下载 64 位或 32 位镜像：
`https://www.kali.org/downloads/`

### Kali Linux 下载
我们每隔几个月会生成新的 `Kali Linux` 镜像并供下载。本页面提供了下载最新官方发布版 `Kali Linux` 的链接，以及位于 `cimageage.org/kali-weekly/` 的未测试每周发布版。

如需查看发布历史，请访问我们的 `Kali Linux` 发布页面。

#### Kali Linux 2021.1 发布日志
![](img/5cafe5b4b24a423ad005874773aac823_64_0.png)
*图 3.2：Kali Linux ISO 下载页面*

### 步骤 2 – 在磁盘中找到下载的文件
文件下载后，你应该能看到一个 ISO 镜像，如图 3.3 所示。
![](img/5cafe5b4b24a423ad005874773aac823_64_1.png)
*图 3.3：磁盘中下载的 ISO 镜像*

### 步骤 3 – 打开 VMware Player
如果桌面上 `VMware Player`，请打开它。或者，你也可以从 Windows 开始菜单打开。启动后，你将看到如图 3.4 所示的窗口：
![](img/5cafe5b4b24a423ad005874773aac823_65_0.png)
图 3.4：VMware Player 启动页

### 步骤 4 – 新虚拟机安装向导
要创建新虚拟机，点击“文件 (File) -> 新虚拟机 (New Virtual Machine)”。将弹出一个“欢迎使用新虚拟机向导”对话框。选择“典型 (Typical)”并点击“下一步 (Next)”。

### 步骤 5 – 出现欢迎新虚拟机向导对话框
新虚拟机创建向导的第一个窗口如图 3.5 所示。
![](img/5cafe5b4b24a423ad005874773aac823_66_0.png)
在此对话框中，你有一个选项可以浏览下载的 ISO 文件，并点击“下一步 (Next)”。通常情况下，`VMware Workstation` 会自动检测操作系统并启动所谓的“简易安装 (Easy Install)”。在这种情况下，你可以选择“稍后安装操作系统 (I will install the operating system later)”。

### 步骤 6 – 指定客户操作系统
在此对话框中，你将被要求选择客户操作系统。根据你下载的 `Kali Linux` 系统架构，选择客户操作系统为 `Ubuntu 64` 位或 `32` 位：
![](img/5cafe5b4b24a423ad005874773aac823_67_0.png)
图 3.6：指定客户操作系统

### 步骤 7 – 输入你的虚拟机名称
在此对话框中，你将被要求提供虚拟机的名称。你可以提供任何你喜欢的名称，也可以更改虚拟机的位置：
![](img/5cafe5b4b24a423ad005874773aac823_68_0.png)
图 3.7：你的虚拟机名称

### 步骤 8 – 指定虚拟磁盘容量
此对话框要求你指定虚拟磁盘容量，即虚拟机创建后它将利用最大磁盘空间量。你可以保持默认值，但建议将其增加到至少 `60GB`。
确保勾选了“将虚拟磁盘拆分为多个文件 (Split virtual disk into multiple files)”。尽管这是默认选项：
![](img/5cafe5b4b24a423ad005874773aac823_69_0.png)
图 3.8：指定虚拟磁盘容量

### 步骤 9 – 准备好创建虚拟机对话框
这是最后一个对话框，允许你检查之前选择的选项：
![](img/5cafe5b4b24a423ad005874773aac823_70_0.png)
**图 3.9：** 检查你的虚拟机设置
上一个对话框将允许对连接到虚拟机的硬件进行进一步自定义。一旦你点击“自定义硬件 (Customize Hardware...)”按钮，将打开一个新窗口：
![](img/5cafe5b4b24a423ad005874773aac823_71_0.png)
如果你的主机 Windows 机器上有足够的 RAM 和 CPU，建议增加 RAM 和 CPU。在点击“完成 (Finish)”之前，点击“自定义硬件 (Customize Hardware...)”来增加内存。你可以使用滑动条增加内存。

### 步骤 10 – 选择新的 CD/DVD (IDE)
现在，该告诉 `VMware Workstation Player` `Kali Linux` ISO 镜像的位置，以便它从那里加载 `Kali` 操作系统了。为此，你需要进入“新 CD/DVD (IDE) (New CD/DVD (IDE))”，并在右侧选择“使用 ISO 镜像文件 (Use ISO image file)”从下载位置选择 `Kali Linux` ISO 镜像：
![](img/5cafe5b4b24a423ad005874773aac823_72_0.png)
图 3.11：选择 Kali Linux ISO 镜像

### 步骤 11 – 运行虚拟机
![](img/5cafe5b4b24a423ad005874773aac823_73_0.png)
图 3.12：运行虚拟机

### 步骤 12 – 安装 Kali
![](img/5cafe5b4b24a423ad005874773aac823_74_0.png)
图 3.13：安装 Kali
![](img/5cafe5b4b24a423ad005874773aac823_75_0.png)
图 3.14：安装 Kali

### 步骤 13 – 启动菜单
![](img/5cafe5b4b24a423ad005874773aac823_76_0.png)
图 3.15：启动菜单

### 步骤 14 – 图形安装
![](img/5cafe5b4b24a423ad005874773aac823_77_0.png)
图 3.16：图形安装

| `touch <file>` | 创建一个空文件 |
|---|---|
| `cp -r <dir1> <dir2>` | 创建目录及其包含的所有内容的副本 |
| `cp <file1> <file2>` | 创建文件的副本 |
| `cp <file> /home/Desktop/file2` | 在不同目录创建文件副本并重命名为 `file2` |
| `mv <file> /home/Desktop` | 将文件移动到特定目录（覆盖同名文件） |
| `mv <dir> /home/Desktop` | 将目录移动到另一个位置 |
| `mv <dir1> <dir2>` | 重命名文件或目录 (`dir1` -> `dir2`) |
| `rm <file>` | 删除文件 |
| `rm -f <file>` | 强制删除文件 |
| `rm -r <dir>` | 删除目录及其内容 |
| `rm -rf <dir>` | 强制删除目录及其内容 |
