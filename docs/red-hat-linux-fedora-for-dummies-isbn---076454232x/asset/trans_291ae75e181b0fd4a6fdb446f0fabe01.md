
启动基于 Wine 的应用程序有几种方法：

- **手动操作，通过使用终端模拟器：** 以通常的方式打开一个终端模拟器窗口，然后输入此命令：`wine "C:\Program Files\WinPac 2\WinPac2.exe"`
- **通过使用 GNOME 运行实用程序：** 打开 GNOME 运行实用程序并输入此命令：`wine "C:\Program Files\WinPac 2\WinPac2.exe"`
- **通过创建并点击一个 GNOME 图标：** 该方法在下述一系列步骤中有详细说明。

我们将展示如何创建一个 GNOME 图标，以轻松使用新游戏。这些步骤描述了该过程：

1. **在 GNOME 面板上任意位置右键单击，并选择“添加到面板 → 启动器”。**
   “创建启动器”窗口将打开。
2. **在“名称”文本框中输入 WinPac2，并在“命令”文本框中输入此命令：** `wine "C:\Program Files\WinPac 2\WinPac2.exe"`
3. **单击“图标”按钮，并在打开的“浏览图标”窗口中选择一个图像。**
   例如，选择 Apple 图标。
4. **单击“确定”按钮，图标将在面板上创建。**
5. **单击新的 WinPac2 图标，游戏即启动，如**图 14-2**所示。**

## 运行 Microsoft Word（这确实很有用）

你也可以使用 Wine 运行主要应用程序。例如，你可能更喜欢使用 Microsoft Word 而不是 OpenOffice。幸运的是，Wine 提供了这种功能。

在本节中，我们将展示如何在我们的 Red Hat Linux 计算机上安装 Microsoft Word 2000。当然，你必须拥有 Word 2000 的许可证，但你不需要 Windows 2000 操作系统的许可证。Wine 提供了运行像 Word 2000 这样的应用程序所需的所有库挂钩和杂项项目。

![](img/8c094d1b36276212c03d10d898508a6e_198_0.png)

Wine 持续被修改和更新，以保持与 Microsoft 尽可能高的兼容性。然而，Wine 偶尔在运行如 Office 和 Word 等复杂应用程序时会出现问题。如果你遇到此类问题，请查阅我们的帮助页面 [www.dummies.com/go/rhlfedoraf4](https://www.dummies.com/go/rhlfedoraf4) 以查找可能的解决方案。你也可以使用商业 Wine 变体，如 CrossOver Office，来运行 Office 或 Word。

![](img/8c094d1b36276212c03d10d898508a6e_198_1.png)

![](img/8c094d1b36276212c03d10d898508a6e_198_2.png)

去找你的 Word 2000（或 Word 97、Word XP 或其他版本）光盘，准备好开始吧。这些步骤展示了如何安装和使用该文字处理器：

1. **以非 root 用户身份登录你的计算机，并将 Microsoft Word 2000 CD 插入 CD-ROM 驱动器。**

   这些步骤在 Microsoft Office 2000 CD 上应该也能良好运行。

2. **单击 GNOME 菜单，选择“系统工具 -> 终端”。**

   “运行程序”窗口将打开。

3. **在此文本窗口中输入此命令：**

   ```
   wine --dll cabinet=n /mnt/cdrom/setup.exe
   ```

   如果你有两个驱动器，可能需要将 `cdrom` 替换为 `cdrom1`。

   根据你安装的 Wine 的状态，你可能会看到一个 Microsoft Word 2000 设置窗口，通知你它找不到字体。缺失的字体通常不会影响应用程序的功能。

4. **每当出现缺失字体警告时，单击“确定”按钮。**

   安装过程在进展过程中会显示大量信息。你可以忽略这些闪过的行。它们不影响安装过程。

   Microsoft Word 2000: 欢迎 窗口将打开。

5. **在五个文本框中输入你 Microsoft Word 2000 光盘（或微软将光盘封入的物理包装中）上的产品密钥。**

   请记住，Wine 仅提供运行有效 Windows 应用程序的*平台*。它不提供应用程序本身。

6. **下一个窗口显示安装标准 Word 配置的选项，或者可选地自定义安装。**

   为了简单起见，我们建议单击“立即安装”按钮。（如果你选择“自定义”选项，我们需要留给你去导航各种额外的配置步骤。）

   安装将继续，直到提示你重新启动计算机。当然，你运行的不是 Windows 计算机，所以单击“否”按钮。安装过程似乎结束了。

7. **Wine 提供了一个 Windows 重启模拟实用程序。重复步骤 2 和 3，并输入此命令：**

   ```
   wineboot
   ```

   安装过程再次启动并完成。你已经在 Linux 计算机上安装了 Microsoft Word 2000！

8. **通过重复步骤 3–5 并在此文本窗口中输入此命令，你可以启动文字处理器：**

   ```
   wine "C:\Program\Files\Microsoft\Office\Office\winword.exe"
   ```

   ![](img/8c094d1b36276212c03d10d898508a6e_199_0.png)

   在 Linux 世界中，反斜杠 (\) 是转义字符；在 Windows 世界中，反斜杠用于分隔目录名。也就是说，它们防止 Linux（bash shell）将后面的字符按字面意思解释。如果没有反斜杠，Linux（bash）会将目录名 `Program Files` 解释为两个独立的实体 Program 和 Files，因为 bash shell 认为空格字符是分隔符，而不是目录名或文件名的一部分。因此，反斜杠和空格的组合——`Program\ Files`——允许 Linux 正确处理好目录名：Program Files。前面的命令（参见步骤 8）被 Linux 解释为 `wine C:\Program\ Files\Microsoft\Office\Office\winword.exe`。

## 介绍 CodeWeavers CrossOver Office

出色的 Wine 系统让你能够利用 Windows 世界的深厚资源。Wine 是在开源系统下开发的，志愿者为计算世界提供了无数小时的无偿服务。然而，开源社区并不限制其软件仅用于非商业用途。根据通用公共许可证（GPL）开发的软件允许商业使用，只要不限制原始 GPL 软件的使用即可。

在特定情况下，开源软件的商业使用可以提供额外的动力。为了利润而开源？确实如此。像 CodeWeavers（[www.codeweavers.com](https://www.codeweavers.com)）和 TransGaming（[www.transgaming.com](https://www.transgaming.com)）这样的公司就提供了这样的动力。这两家公司都为基本的 Wine 软件增加了功能，使安装过程更简单。CodeWeavers 专注于让 Wine 在通用桌面上更易用；该公司使安装和使用 Microsoft Office、Internet Explorer 以及各种插件变得简单。另一方面，TransGaming 的产品 WineX 则提供了一个面向游戏的系统。

本书侧重于将 Linux 用作实用的日常工作站。我们的工作倾向于使用文字处理器和类似程序。我们将使用 WineX 的实验留给你去进行。只需说明一下，我们面向游戏的同事认为 WineX 很有用。

CodeWeavers 生产两种产品：CrossOver Office 和 CrossOver Plugin。Office 作为安装实用程序具有价值，有助于安装 Windows 应用程序。Plugin 产品提供内部开发的软件，有助于使用插件。CrossOver Office 主要使用未修改的 Wine 软件，但提供了一个时尚的安装系统。CrossOver Plugin 使用其自定义库，使 Windows 插件（如 QuickTime）能够与你的 Linux 浏览器配合使用。CrossOver Office 的成本为 54.95 美元，Plugin 的成本为 24.95 美元。你可以以 69.95 美元购买两者。（这些价格是指从互联网下载产品时的价格。CD 版本的价格分别为 64.95 美元、34.95 美元和 79.95 美元。）

## 下载 CrossOver Plugin 的试用版

CodeWeavers 慷慨地为 CrossOver Plugin 和 CrossOver Office 提供 30 天的评估许可证。因此，你可以测试其产品的完整版本。这些步骤描述了如何下载 CrossOver Plugin 的试用版：

1. 以超级用户身份登录你的 Red Hat Linux 计算机。
2. 打开 Mozilla 并前往 [www.codeweavers.com/products/download_trial.php](https://www.codeweavers.com/products/download_trial.php)。
3. 单击页面顶部的 CrossOver Plugin 按钮。
4. 填写注册表单并单击“请求评估”按钮。
   “下载 CrossOver 试用版”页面将打开，通知你 CrossOver 的安装说明正在通过电子邮件发送给你。
5. 当信息通过电子邮件发送给你时，在 Mozilla 中打开此页面：[http://crossover.codeweavers.com/download/plugin-trial](http://crossover.codeweavers.com/download/plugin-trial)。
   “CrossOver 安全下载”窗口将打开。
6. 在“访问密钥”和“序列号”文本框中输入刚刚通过电子邮件发送给你的访问密钥（你的电子邮件地址）和序列号。
7. 单击“下载”按钮。
   “正在下载 install-crossover-plugin-1.2.1-demo.sh”对话框将打开。
8. 单击“确定”按钮。
   “输入要保存到的文件名称”对话框将打开。
9. 单击“保存”按钮，软件将保存到你的当前目录。

## 安装 CrossOver Plugin

在你下载了 CrossOver Plugin 安装系统之后，你的下一步是安装 CrossOver Plugin。这些步骤描述了如何使用安装系统来安装和配置软件：

1. 以（root）超级用户身份登录。
2. 打开一个 GNOME 终端窗口。
3. 输入以下命令：
   ```
   chmod +x install-crossover-plugin-1.2.1-demo.sh
   ./install-crossover-plugin-2.0.2-demo.sh
   ```
   “许可协议”对话框将打开。
4. 阅读许可证并单击“我同意”按钮。
   “CrossOver Plugin 设置”窗口显示了 Plugin 软件将安装的位置。默认目录是 /opt/cxplugin（该目录将为你创建）。
5. 单击“开始安装”按钮，CrossOver Plugin 软件将为你安装。
   当安装完成时（可能需要几分钟），“CrossOver Plugin 设置”窗口将显示消息 `Installation complete`。

