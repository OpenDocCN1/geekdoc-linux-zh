

![](img/415c89a1ede71e11e5040a0038b6916c_118_0.png)

## Figure 3.6

Windows 2000 启动画面。

## LOADING SYSTEM SERVICES

一旦内核初始化阶段成功完成，服务管理器（SMSS.EXE）将被加载。在此阶段，完成以下任务：

- 1. 服务管理器完成 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SessionManager\BootExecute 注册表值下指定的操作。默认情况下，BootExecute 下的唯一条目是 autocheck autochk *。Autocheck 是 chkdsk 的启动时版本，用于检查所有可用分区。
- 2. 系统分页文件根据 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\Paging-Files 中定义的条目进行设置。
- 3. 检查 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\DosDevices 注册表值并创建指定的文件系统链接。
- 4. 检查 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Subsystems\Required 值并加载所需的子系统。默认情况下，仅需要 Win32 子系统。

## STARTING THE WIN32 SUBSYSTEM

如果所有先前的阶段都已完成，则加载 Win32 子系统并执行以下任务：

- 1. 启动 WINLOGON.EXE 程序，进而启动本地安全机构（LSASS.EXE）。完成后，会显示熟悉的 Ctrl+Alt+Del 消息，表明系统已准备好供用户开始登录过程。此消息框显示在图 3.7 中。
- 2. 执行服务控制器（SCREG.EXE）并最后一次遍历注册表以查找并启动设置为自动启动的任何设备和服务。这包括启动工作站和服务器服务，这些服务对于网络访问是必需的。服务和驱动程序根据注册表中指定的依赖项加载。如果您处于网络环境中，最好不要尝试登录，直到所有服务和驱动程序都已加载（即磁盘停止读写）。

Figure 3.7
Windows 2000 登录消息。

![](img/415c89a1ede71e11e5040a0038b6916c_119_0.png)

## USER LOGON

启动过程的最后一个，也是可能最重要的阶段是用户登录阶段。在用户成功登录到 Windows 2000 系统之前，不能认为启动是成功的。用户通过按 CTRL+ALT+DEL 来开始登录过程，以显示图 3.8 所示的登录对话框。输入用户名和密码后，并选择适当的域（如适用），即可通过单击 OK 按钮开始登录。在此阶段，系统会从克隆控制集创建 LastKnownGood 控制集。此时，系统应该稳定且可用。

## DUAL-BOOT SYSTEMS

双启动和多启动系统变得越来越普遍。能够同时拥有 UNIX 和 NT 操作系统的能力具有一定的吸引力。同样，能够使用 Windows 98 或其他系统使运行某些程序变得更容易。

“Windows 2000 启动过程”部分提供了双启动系统的示例。双启动系统的选项范围很广，使得不可能在此讨论所有不同的排列组合。

## Advanced Windows 2000 Boot Options

正如我们前面所述，在显示 Starting Windows 屏幕期间按下 <F8> 键将显示高级选项菜单，如图 3.9 所示。

Figure 3.8
Windows 2000 登录对话框。

![](img/415c89a1ede71e11e5040a0038b6916c_120_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_121_0.png)

Figure 3.9
Windows 2000 高级选项菜单。

高级选项菜单为启动 Windows 2000 提供了多种恢复和故障排除选项。本节将解释这些选项以及您可能想要使用它们的情况。

## SAFE MODE

如果您在正常启动系统时遇到困难，则选择安全模式可能会有所帮助。当您选择安全模式时，Windows 2000 仅加载系统启动所需的最低限度驱动程序和服务。当您启动到安全模式时，正常的 Windows 2000 桌面将被特殊的 安全模式 桌面取代，屏幕为黑色，四角均显示 Safe Mode。如果您的系统在安全模式下仍无法启动，您将需要执行系统恢复。

安全模式有三种类型：前面讨论的标准安全模式、安全模式 with Networking 和安全模式 with Command Prompt。这三种变体基本上相同，但有细微差别。如果您选择安全模式 with Networking，Windows 2000 将尝试在标准安全模式选项下加载的驱动程序和服务之外加载网络驱动程序和服务。如果您的系统可以在标准安全模式下启动，但在安全模式 with Networking 下无法启动，则您的系统可能存在不兼容或损坏的网络驱动程序。在安全模式下删除该驱动程序应该可以让您正常启动并重新安装网络组件

