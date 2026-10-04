

# 第 10 章 · 安全 IIS

这假设你的答案文件位于 c:\iis.txt。命令的 /I 部分指定了应使用的主 .inf 文件。该命令将在无任何用户交互的情况下安装 IIS。Syscmgr 还支持以下选项：

- /i: <sysoc.inf 文件的位置> 指定主 sysoc.inf 的名称和路径。安装源路径从此处获取。此切换开关是必须的。
- /u: <答案文件的位置> 指定要使用的答案文件的名称和路径。
- /r 抑制重启（如果需要重启）。
- /n 强制将 sysoc.inf 视为新文件。
- /f 表明所有组件的安装状态都应该初始化，就好像它们的安装程序从未运行过一样。
- /c 不允许在最终安装阶段取消。
- /x 抑制初始化横幅。
- /q 配合 /u 使用。带有用户界面的运行无人值安装。
- /w 配合 /u 使用。在需要时提示用户重启，而不是自动重启。
- /l 多语言感知的安装。

到此时，你已经创建了一个新的网站。

## 安装热补

在服务器安装了适当组件后，你应该使用最新的热补更新 Windows 2000。除了补丁（SP）后的安全修复外，你还应该考虑其他不总是包含在服务包和热补中的更新，例如：

- FrontPage Server Extensions 2000 http://msdn.microsoft.com/library/en-us/dnserver/html/winfasp
- FrontPage Server Extensions 2002 http://msdn.microsoft.com/library/en-us/dnserver/html/fpse2win.asp
- MDAC: ADO, OLEDB, ODBC, 和 JET www.microsoft.com/data
- XML http://msdn.microsoft.com/xml
- COM+ Search 访问微软 KB 以获取最新的 COM+ 汇总包
- Windows Script Host http://msdn.microsoft.com/scripting
- Exchange Server http://www.microsoft.com/exchange
- SQL Server http://www.microsoft.com/sql
- BizTalk Server http://www.microsoft.com/biztalk/downloads/default.as
- Commerce Server http://www.microsoft.com/commerserver
- Application Center http://www.microsoft.com/applicationcenter
- Content Management Server http://www.microsoft.com/cmmserver
- SharePoint Portal Server http://www.microsoft.com/sharepoint
- ISA Server http://www.microsoft.com/isaserver

## 锁定 COM 和数据库访问

由于 Web 服务器通常提供对内部系统或敏感数据的访问，对数据库和组件对象模型 (COM) 组件进行适当锁定是非常重要的。当 COM 组件或数据库连接在特权用户账户的安全上下文中运行时，这一点尤为关重要。尽管配置良好的防火墙会消除某些这些风险，但某些项目需要额外的配置才能实现完全安全。

## 安全 ADO 和 ODBC 驱动程序

保护数据库的第一步是安装最新的驱动程序，并仅保留你特定使用的数据源名称 (DSN) 和驱动程序。驱动更新解决了许多安全问题，应在你的环境中测试后立即安装。

默认的 Windows 2000 安装包含许多默认 Open Database Connectivity (ODBC) 驱动程序，如果你不使用它们，可以安全地删除。无法从“数据源 (ODBC)”管理工具中删除 ODBC 驱动程序，你必须手动从 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI 注册表键删除未使用的驱动程序（见图 10.2）。注意，随后的驱动更新可能会恢复这些条目，因此你应该在安装更新后检查此注册表键。

![](img/729efc56f204a2ebffb8295c3a2dfdfb_547_0.png)

# 图 10.2 ODBCBST.INI 注册表键中的驱动程序

![](img/729efc56f204a2ebffb8295c3a2dfdfb_548_0.png)

## 安全 Jet

与 ODBC 类似，Jet 安装许多你可能不会使用的驱动程序。要删除它们，请删除 \HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Jet 注册表下的任何未使用的 Jet 引擎和索引顺序访问方法 (ISAM) 格式。

接下来，如果你使用 Jet，将沙箱模式（Sandbox Mode）更改为更安全的设置是重要的。沙箱模式防止用户将 Shell 等敏感命令嵌入 SQL 查询中。可能的沙箱模式如下：

- 0 沙箱模式禁用。
- 1 沙箱模式仅用于 Access 。
- 2 沙箱模式仅用于非 Access 。
- 3 沙箱模式用于所有应用程序。

你应该始终使用设置 3 以获得最大的保护。将 \HKEY_LOCAL_MACHINE\Software\Microsoft\Jet.3.5\engines\SandboxMode 和 HKEY_LOCAL_MACHINE\Software\Microsoft\Jet\4.0\engines\SandboxMode 注册表设置为三，如图 10.3 所示。

另一个问题是，默认情况下，文本 ISAM 允许你读写任何文本文件，可能允许攻击者修改敏感的系统文件或脚本。要修复此，将 \HKEY_LOCAL_MACHINE\Software\Microsoft\Jet\4.0\Text\DisabledExtensions 注册表设置为 !txt（将 txt 替换为你特定使用的任何文本扩展）。注意，此设置的默认值为 !txt,.csv,.tab,.asc,.htm,.html。

## 10.3 Jet 注册表设置

![](img/729efc56f204a2ebffb8295c3a2dfdfb_549_0.png)

更多关于保护数据库的信息，请参考第 12 章和第 13 章。

## 安全数据源

某些 Windows 应用安装用户、系统或文件 DSN 而不通知你它们已安装。如果未使用这些 DSN，你应该通过打开“数据源 (ODBC)”并对每个未使用的驱动程序点击**删除**来删除它们（见图 10.4）。注意可以通过删除 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI 中的条目来移除这些数据源。

## 10.4 未使用数据源

![](img/729efc56f204a2ebffb8295c3a2dfdfb_549_1.png)

## 禁用 RDS

远程服务 (RDS) 允许由于 Web 服务器通常提供对内部系统或敏感数据的访问，适当锁定组件是非常重要的。当 COM 组件或数据库连接在特权用户账户的安全上下文中运行时，这一点尤为重要。尽管配置良好的防火墙会消除某些这些风险，但某些项目需要额外的配置才能实现完全安全。保护数据库的第一步是安装最新的驱动程序，并仅保留你特定使用的数据源名称 (DSNs) 和驱动程序。驱动更新解决了许多安全问题，应在你的环境中测试后立即安装。

默认的 Windows 2000 安装包含许多默认 Open Database Connectivity (ODBC) 驱动程序，如果你不使用它们，可以安全地删除。无法从“数据源 (ODBC)”管理工具中删除 ODBC 驱动程序，你必须手动从 HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST.INI 注册表键删除未使用的驱动程序（见图 10.2）。注意，随后的驱动更新可能会恢复这些条目，因此你应该在安装更新后检查此注册表键。

## 安全 COM

某些组件在文件级别更容易安全，而其他根据对精确控制的程度，通过注册表更安全。表 10.1 显示了潜在危险组件及其类 ID。表 10.2 显示了组件及其相关的 DLL 或 OCX 文件。

如果你对这些对象有精确的控制，可以通过设置 HKEY_CLASSES_ROOT\CLSID 下的类 ID 来。当创建任何组件时，Windows 必须收集有关它的信息。如果特定用户无法读取注册表，则无法创建组件。默认情况下，所有用户。

例如，为了安全 FileSystemObject，收紧 HKCR\CLSID|{043FE01-F093-11CF-8940-00A0C954228} 注册表键允许管理员读取。注意这将限制使用 FileSystemObject，但 Dictionary 对象对所有用户可用。某些组件通常提供对内部系统或敏感数据的访问，对数据库和组件对象模型 (COM) 组件进行适当锁定是非常重要的。当 COM 组件或数据库连接在特权用户账户的安全上下文中运行时，这一点尤为重要。尽管配置良好的防火墙会消除某些这些风险，但某些项目需要额外的配置才能实现完全安全。（此处原文大量重复段落，已根据指令要求处理）

