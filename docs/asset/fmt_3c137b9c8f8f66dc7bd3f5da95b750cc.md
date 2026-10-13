
5. 当信息通过电子邮件发送给你时，在 Mozilla 中打开此页面：[http://crossover.codeweavers.com/download/plugin-trial](http://crossover.codeweavers.com/download/plugin-trial)。

“CrossOver 安全下载”窗口将打开。

6. 在“访问密钥”和“序列号”文本框中输入刚刚通过电子邮件发送给你的访问密钥（你的电子邮件地址）和序列号。

7. 单击“下载”按钮。

“正在下载 install-crossover-plugin-1.2.1-demo.sh”对话框将打开。

8. 单击“确定”按钮。

“输入要保存到的文件名称”对话框将打开。

9. 单击“保存”按钮，软件将保存到你的当前目录。

### 安装 CrossOver Plugin

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

“CrossOver Plugin 设置”窗口显示了 Plugin 软件将安装的位置。默认目录是 `/opt/cxplugin`（该目录将为你创建）。

5. 单击“开始安装”按钮，CrossOver Plugin 软件将为你安装。

当安装完成时（可能需要几分钟），“CrossOver Plugin 设置”窗口将显示消息 `Installation complete`。

6. 单击“Configure Now”按钮。

插件设置窗口将打开。

7. 单击“Install”按钮。

安装软件窗口将打开，显示可供安装的插件列表。

8. 单击“Next”按钮。

浏览器选择窗口将打开，显示将为 Netscape 和 Mozilla 安装的插件。

9. 单击“Next”按钮。

HTTP 代理配置窗口将打开，允许您配置插件以配合 Web 代理服务器工作。代理服务器会过滤您可以浏览的位置。如果您有代理，请输入相关代理信息。

10. 单击“Finish”按钮。

CrossOver 插件设置窗口将打开，如“图14-3”所示。

![](img/8c094d1b36276212c03d10d898508a6e_202_0.png)

#### 使用 CrossOver 插件

配置过程的下一阶段允许您从众多流行的 Windows 插件中选择。当您选择要安装的插件时，系统会自动为您从互联网下载。简单快捷。

以下步骤介绍了如何选择一个 Windows 插件并自动下载它：

1. 单击“Install”按钮，随后将打开下一个 CrossOver 插件设置窗口。

“图14-4”展示了安装软件窗口。

2. 单击 QuickTime 6 插件。

3. 单击“Next”按钮。

“Express Install (Recommended)”按钮默认被选中。

![](img/8c094d1b36276212c03d10d898508a6e_203_0.png)

4. 单击“Next”按钮，QuickTime 6 插件将从互联网下载。

QuickTime 6 设置窗口将打开，如“图14-5”所示。

5. 单击“Next”按钮。

将显示一个欢迎屏幕。

6. 单击“Next”按钮以继续。

下一个窗口显示 QuickTime 许可协议。

7. 阅读该许可协议（最好是在坐满律师的房间里阅读），然后单击“Agree”按钮。

下一个窗口显示将安装 QuickTime 插件的安装位置。默认位置是模拟的 Windows 目录，实际上是您主目录中的 `.wine/c/program files` 目录。

8. 单击“Next”按钮。

选择安装类型对话框将打开。

9. 您可以选择不同复杂程度的级别。最低级别（默认级别）通常就足够了，因此只需单击“Next”按钮即可。

10. 当“Select Program Folder”打开时，单击“Next”按钮以选择默认文件夹名称：QuickTime。

深呼吸一下，因为您快要完成了。下一个窗口是输入注册信息的窗口。

11. 输入您的姓名和组织名称（如果您有的话）。（您不需要输入注册号。）单击“Next”按钮。

12. 最后一步是输入任何代理信息。如果您有代理（例如，如果贵公司网络使用代理），请获取其信息并输入。

13. 单击 `Continue` 按钮。

安装系统会思考片刻，然后在从互联网下载 QuickTime 插件时显示一个进度对话框。

![](img/8c094d1b36276212c03d10d898508a6e_204_0.png)

**图14-5：QuickTime 6 设置对话框。**

#### 配置 QuickTime

最终的 QuickTime 配置过程从 QuickTime 设置/介绍窗口打开时开始。以下步骤介绍了如何完成 QuickTime 的配置：

1. 单击 `Next` 按钮，**连接速度对话框**将打开。

连接速度对话框询问您使用哪种类型的互联网连接。

2. 从**下拉菜单**中**选择您的连接速度和类型**，然后单击 `Next` 按钮。

浏览器插件窗口将打开，询问您是否想要更改哪些 MIME 设置（如果有的话）。

3. **默认设置应该就可以了，因此单击 `Next` 按钮。**

接下来打开的文件类型关联窗口允许您选择 QuickTime 应该处理哪些类型的文件。默认选项是 QuickTime，用于处理 Mac 文件（例如 PICT 和 AIFF）。

4. 进行适合您的任何更改，然后单击 `Finish` 按钮。

5. 单击“Yes, I Want to Launch QuickTime Player”按钮，然后单击“Close”按钮。

安装报告窗口将打开，显示所有插件的信息。

6. 单击“OK”按钮，控制权返回到 CrossOver 插件设置窗口。

CrossOver 安装系统除了安装插件外，还会为 QuickTime 播放器应用程序安装链接。CrossOver 还会在 GNOME 主菜单上安装菜单项。

7. 单击 GNOME 菜单按钮，然后选择“Programs ➔ QuickTime ➔ QuickTime Player”。

QuickTime 播放器将打开，您可以在“图14-6”中看到这一点。

CrossOver 还会安装其自己的实用工具。单击 GNOME 菜单并打开 CrossOver 菜单。您将看到几个实用工具。单击“Plugin Setup”选项，插件设置窗口将打开。

![](img/8c094d1b36276212c03d10d898508a6e_205_0.png)

![](img/8c094d1b36276212c03d10d898508a6e_206_0.png)

QuickTime 插件及其支持软件安装在主目录中的 `.mozilla/plugins` 目录中。您可以通过打开 Mozilla 并选择**Help→About Plugins**来验证插件是否已安装。Mozilla 将显示所有已安装的插件。

#### VMware：一台虚拟现实机器

有时，您需要使用一个在 Linux 下根本无法运行的应用程序——即使借助 Wine 的帮助也不行。例如，我们其中一人必须使用故障单系统来解决客户的问题。问题是，该故障单应用程序在 Linux 下无法运行，无论是否使用 Wine。因此，那位作者必须在他的计算机上同时安装 Windows 和 Linux（**双启动系统**），否则就得维护一台专门用于运行该单一应用程序的独立计算机。

当然，使用双启动计算机没有什么不对。但如果只需要运行一两个应用程序，这样做有点浪费时间。双启动计算机在需要使用另一个操作系统时还必须重新启动。双启动的一种替代方案是 VMware，这是 VMware, Inc. 的一款商业产品。该程序在物理计算机内创建了一台虚拟计算机。虚拟计算机作为一个应用程序运行，就像 OpenOffice 或 Mozilla 一样。

VMware 看起来和工作起来就像一台真正的 PC。VMware 虚拟 PC 可以像任何真实计算机一样运行操作系统，例如 Linux 或 Windows。在虚拟机上运行的操作系统行为与真实操作系统完全相同。因此，它托管的任何应用程序看起来和工作起来也与真实应用程序完全一样！

![](img/8c094d1b36276212c03d10d898508a6e_206_1.png)
