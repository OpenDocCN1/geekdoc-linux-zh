
## SELinux 管理工具

SELinux 提供了多种工具，让你能够管理 SELinux 配置和策略实施，包括使用 `semanage` 来配置策略。SELinux 的 Fedora 系统配置工具是 `system-config-selinux`。`setools` 软件包提供了 SELinux 配置和分析工具，包括 `apol`（用于域转换分析的安全策略分析工具）、用于策略差异分析的 `sediffx` 以及用于检查审计日志的 `seaudit`（参见表 17-2）。`setools` 集合还包括相应的 GUI 界面，位于 `setool-gui` 软件包中。这些将在“系统 | 管理”菜单中列为 SELinux 审计日志分析、SELinux 策略分析和 SELinux 策略差异。命令行用户管理工具 `useradd`、`usermod` 和 `userdel` 都具有可在安装 SELinux 时应用的选项。此外，`audit2allow` 工具会将 SELinux 拒绝消息转换为允许访问的策略模块。请参阅 `fedoraproject.org/wiki/SELinux/Commands` 上的完整 SELinux 命令列表。

| 命令 | 描述 |
| :--- | :--- |
| `seinfo` | 显示策略统计信息 |
| `sestatus` | 检查系统中 SELinux 的状态，包括进程和文件的上下文 |
| `sesearch` | 在策略中搜索类型强制规则 |
| `seaudit` | 检查 SELinux 日志文件 |
| `sediffx` | 检查 SELinux 策略差异 |
| `audit2allow` | 使用审计 AVC 拒绝消息为模块生成策略允许规则。 |
| `apol` | SELinux 策略分析 |
| `system-config-selinux` | Fedora SELinux GUI 配置工具 |
| `setroubleshoot` | SELinux GUI 故障排除工具 |
| `checkpolicy` | SELinux 策略编译器 |
| `fixfiles` | 检查文件系统并设置安全上下文 |
| `restorecon` | 为特定文件设置安全特性 |
| `newrole` | 新角色 |
| `setfiles` | 为文件设置安全上下文 |
| `chcon` | 更改上下文 |
| `chsid` | 更改安全 ID |

表 17-2 SELinux 工具

在 SELinux 的模块化版本中，策略管理不再通过直接编辑配置文件来处理。相反，你使用 SELinux 管理工具，如命令行工具 `semanage` 和 `system-config-selinux`（系统 | 管理 | SELinux 管理）。这些工具利用接口文件来生成修改后的策略。

### 使用 system-config-selinux 进行配置

通过 `system-config-selinux`，你可以管理和配置 SELinux 策略，但不能创建新策略（参见图 17-1）。你可以通过在“系统 | 管理”菜单中选择“SELinux 管理”条目来访问 `system-config-selinux`。

`system-config-selinux` 窗口将列出多个窗格，并带有侧边栏菜单，包括：状态、布尔值、文件标记、用户映射、SELinux 用户、翻译、网络端口和策略模块。`system-config-selinux` 将调用带有适当选项的 SELinux 管理工具（如 `sestatus` 和 `semanage`）以进行配置更改。

![](img/ab68ea377332b50bf70ef1316c8175b6_415_0.png)

图 17-1 `system-config-selinux`

状态窗格列出了用于选择策略和执行默认值的弹出菜单，以及当前的强制模式。一个在重启时重新标记的复选框允许你在重启时强制重新标记文件的安全上下文（参见图 17-1）。

布尔值窗格列出了针对 Web 服务器和 FTP 服务器、NFS 以及 Samba 等目标服务的各种选项。通过这些选项，你可以进一步修改每个服务的控制方式。有可展开的菜单用于不同的服务，如 FTP、Apache Web 服务器和 Samba。例如，FTP 条目允许你选择是否允许访问主目录或 NFS 传输。

文件标记窗格将列出你的系统目录和文件，显示它们的安全上下文和类型。你可以通过选择条目然后单击“属性”来编辑文件的属性。这会显示一个对话框，包含文件名、类型、SELinux 类型和 MLS 级别。你可以更改 SELinux 类型或 MLS 级别。对于许可策略，MLS 级别为 `$0`，允许任何人访问。你还可以添加或删除条目。

用户映射显示了用户登录名到 SELinux 用户的映射。最初将有两个映射：root 用户和默认用户。

SELinux 用户窗格显示了不同类型的 SELinux 用户。最初将有三种用户类型：root、`system_u` 和 `user_u`（参见图 17-2）。root 用户是 root 用户，具有对整个系统的完全和管理权限。`system_u` 用户允许用户在需要时获得管理访问权限。`user_u` 用户用于普通用户。每个条目列出了其 SELinux 用户、SELinux 前缀、MLS 级别、MLS 范围和 SELinux 角色。MLS 级别是访问级别（在许可策略中为 `$0`），MLS 范围是从 SystemLow 到 SystemHigh 的访问范围。给定用户具有某些可用的角色。root 用户具有 `system_r`、`sysadm_r` 和 `user_r` 角色，允许其拥有系统访问权限、管理功能和标准用户访问。同样的角色也应用于 `user_u`，如果该用户拥有 root 用户密码，则允许该用户执行系统管理。`system_u` 角色仅具有系统访问权限，不能执行系统管理。

![](img/ab68ea377332b50bf70ef1316c8175b6_416_0.png)

图 17-2 `system-config-selinux` SELinux 用户窗格

翻译窗格允许你设置 MLS 符号。最初，你将拥有 SystemHigh 和 SystemLow–SystemHigh 范围的符号。你更改映射的 MLS 级别，从而改变整个系统的安全级别访问。

网络端口窗格列出了系统中的网络协议、SELinux 类型以及端口的 MLS 安全级别。选择一个条目并单击“属性”以更改端口的 SELinux 类型或 MLS 级别。“组视图”按钮将显示 SELinux 类型以及它们适用的端口列表。此视图不显示 MLS 级别，因为这些适用于单个端口。

策略模块窗格列出了不同的 SELinux 策略模块。在这里，你将看到不同应用程序（如 Thunderbird 和 Evolution）以及设备服务（如 USB 和 HAL）的模块。还列出了如 GNOME 等桌面环境。该窗格允许你添加或删除模块。你还可以为模块启用或添加额外的审计规则以用于日志记录。

> 注意 你可以使用 `system-config-securitylevel` 来配置 SELinux 的基本设置（更多详细信息请参见第 4 章）。在这里，你可以选择是否启用 SELinux，以及如果启用，是强制执行还是使用许可选项。许可选项仅发出警告。

## SELinux 故障排除与 audit2allow

Fedora 包含 SELinux 故障排除程序，该程序会通知 SELinux 检测到的问题。每当 SELinux 拒绝访问某个文件或应用程序时，内核就会发出 AVC 通知。SELinux 故障排除程序会分析这些通知，以检测用户可能需要处理的问题。当检测到问题时，SELinux 故障排除程序的通知将显示在桌面通知区域，并附带一个故障排除程序图标。单击该图标或通知将打开 SELinux 故障排除程序窗口。你也可以随时通过“系统 | 管理 | SELinux 故障排除程序”访问它。你可以在 [hosted.fedoraproject.org/projects/setroubleshoot](https://hosted.fedoraproject.org/projects/setroubleshoot) 上了解有关 SELinux 故障排除程序的更多信息。

SELinux 故障排除程序窗口将显示通知列表，以及它们的日期、发生次数、类别和简要说明。“筛选器”条目允许你关闭此事件的后续通知。选择某个条目将显示关于该通知的详细信息，分为四个部分：摘要、详细描述、允许访问和附加信息（参见图 17-3）。

在许多情况下，问题可能很容易修复，如图 17-3 中的“允许访问”部分所示。通常，必须重命名文件的安全上下文以允许访问。你使用 `chcon` 命令来更改文件的安全上下文。在此示例中，需要向 Samba 服务器授予对 `/var/lib/samba` 目录中 `log.richard3` 文件的 rename 访问权限。SELinux 故障排除程序本身不会采取任何行动。相反，它会推荐可能的操作。在此示例中，用户只需发出以下 `chcon` 命令：

```
chcon -R -t samba_share_t log.richard3
```
