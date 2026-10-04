

534 第 10 章 加固 IIS

- **键**: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters
- **类型**: REG_DWORD
- **推荐值**: 取决于服务器角色
- **EnableSvcLoc**: 此设置允许或阻止微软管理控制台 (MMC) 查看 IIS 服务器。

- **键**: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W3SVC\Parameters
- **类型**: REG_DWORD
- **推荐值**: 取决于服务器角色

# 加固默认网站和管理网站

当首次安装 IIS 时，会创建两个 Web 站点：一个默认网站和一个管理站点。这两个站点都可能存在安全风险，应该被禁用。如图 10.10 所示，默认网站包含许多默认虚拟目录，其中许多目录映射到系统驱动器，这被认为是一种不良的做法。这些虚拟目录中的某些可能会可能会许多许多网站不会使用的危险功能，而某些仅仅是示例，在生产环境服务器上并没有用武之地。如果默认网站中出现任何以下虚拟目录，请删除它们，除非你对它们有特定的用途。如果你保留了其中任何一个，请确保限制谁可以访问它们：

- Scripts
- IISHelp
- IISSamples
- Printers
- IISAdmin
- IISAdmpwd
- MSADC
- PBSServer
- PBSData
- RPC
- CertSrv
- CertControl
- CertEnroll

# 图 10.10 默认网站

![](img/729efc56f204a2ebffb8295c3a2dfdfb_559_0.png)

作为进一步的预防措施，你应该从文件系统中完全删除这些目录：

- C:\netpub\scripts
- C:\winnt\help\iis\iis
- C:\netpub\iisamples
- C:\winnt\web\printers
- C:\winnt\system32\inetsrv\iisadmin
- C:\winnt\system32\iisadmpwd

你应该通过设置 IP 限制以拒绝所有外部访问并最终停止该站点来禁用默认网站。加固站点可以采取的其他措施包括将端口更改为 80 以外的端口、将主机标头设置为 LocalHost，以及禁用对站点的匿名访问。

管理网站提供了敏感的基于 HTML 的 IIS 管理功能。虽然默认情况下对站点的访问限制在 LocalHost，但如果你不使用基于 HTML 的管理，你应该完全删除此站点。如果你正在使用基于 HTML 的管理，请采取措施通过更严格的 IIS 和 NTFS 权限来进一步加固它。

# 地下室备记……

# 禁用默认网站

既然可以直接删除它，为什么还要费劲去禁用默认站点呢？虽然删除站点似乎是一个更好的策略，但保持站点完整性也有充分的理由。首先，许多安装虚拟目录的第三方 Web 应用程序默认会在第一个网站 (W3SCV1) 上进行操作，这可能会暴露不安全的和/或示例应用程序。其次，当你在 IIS 中删除默认网站且没有配置其他站点时，该站点在重启后再次会出现。此外，如果你删除了站点并创建一个新站点，新站点在某些情况下会继承旧站点的所有设置。因此，你最好将站点留那里，将其禁用，并从 W3SVC2 开始创建你自己的 Web 站点。尽管默认网站是不安全的，但通过禁用它至少可以控制暴露范围。

# 禁用 Internet 打印

基于 Web 的打印允许内网用户通过 IIS 访问服务器打印机的功能。虽然这方便，但它为生产 Web 服务器增加了不必要的暴露。删除默认网站上的 Printers 目录可以禁用 Web 打印，但一旦重启，Printers 虚拟目录就会替换。要完全禁用 Web 打印，必须设置组策略来禁用 Web 打印。要实现此，从**运行**菜单输入 **mmc.exe** 打开 Web 服务器的本地组策略。这将提供一个空白控制台，你可以在其中添加组策略组件。从**控制台菜单**选择**添加/删除单元**并点击**添加**以显示可用组件列表。从列表中选择**组策略**，在出现提示时，点击**完成**以接受本地计算机作为组策略对象。回到 MMC 控制台，浏览到 Local Computer\Configuration\Administrative Templates\Printers，并将 Web 打印策略设置为**禁用**（参见图 10.11）。

请注意，如果你不想使用组策略，可以通过将注册表 HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\WindowsNT\Printers\DisableWebPrinting 设置为 **1** 来直接设置此值。

# 图 10.11 通过组策略禁用 IIS

![](img/729efc56f204a2ebffb8295c3a2dfdfb_561_0.png)

# 禁用或加固 FrontPage 服务器扩展

FrontPage 服务器扩展 (FPSES) 方便的远程 Web 授权功能，但它们因不安全而声誉不好。从历史上来看，大多数 FrontPage 问题更多是配置不当而非其他任何问题。尽管它们增加了攻击面，但你应该清楚具体的风险。

安装 FPSSE 的风险是：

- 它们暴露了有关 Web 服务器的信息
- 它们提供了身份验证
- 它们需要具有执行权限的虚拟目录
- 它们安装在单独分区上
- 日志文件有时缺少详细信息
- FPSSE 在进程 (inetinfo.exe) 中运行，并在 SYSTEM 账户下运行

另一个风险是 FPSSE 安全模型是 IIS 安全之上的另一层，可能会有些令人困惑。如果你使用 FPSES，最好识别出一组特定的互联网 (IP) 地址用于编写和管理站点。如果你能做到这一点，请在 _yti 虚拟目录上设置 IP 限制以限制未经授权的访问。你还应该启用授权操作日志，并定期检查和存档位于 _yti_log 目录下的日志文件。

将 FrontPage 二进制文件移动到不同的分区有点困难。要这样做，你必须将 C:\Program Files\Common Shared\web server extensions\40（如果你使用 FPSSE 2002，则为 C:\Program Files\Common Shared\web server extensions\50）的内容移动到新位置。然后，你必须打开 Regedit 并搜索旧路径的所有实例，将其替换为新路径。你需要使用 metaedit.exe（可在 http://download.microsoft.com/download/iis50/Utility/5.0/NT45/EN-US/Medt22.exe）替换数据库中的所有路径。重启服务器，过程即可完成。记住，每次安装补丁或服务包时，都必须在新位置手动更新这些文件。

想要完全删除 FPSES，必须打开 Internet 服务管理器并右键点击每个网站，选择“所有任务”，然后选择“删除服务器扩展”。接下来，删除任何网站中的任何 _yti 或 _private 目录。最后，你应该从主网站属性的 ISAPI 扩展选项卡中删除 FPED.dll 文件。

一个需要记住的重要点是，永远不要在分配表 (FAT) 分区上安装 FPSSE。任何人都可以编写和管理 FrontPage Web 站点而无需密码。

# 配置 URLScan

URLScan 作为 IIS Lockdown 工具的一部分安装的，但也可以单独更新。你可以从 http://download.microsoft.com/download/iis50/Update/2.5/NT45/EN-US/URLSCAN.EXE 下载最新版本的 URLScan。运行安装文件以更新 URLScan。

