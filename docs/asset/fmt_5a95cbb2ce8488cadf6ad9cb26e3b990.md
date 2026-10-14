
调用脚本允许你配置异步传输模式 (`ATM`)。

## HP Insight Manager

调用用于启用和配置 `HP Insight Manager` 的工具。

你不需要使用 `System Setup` 中列出的所有选项，可以选择将任何选项推迟到以后处理。如果你选择拒绝任何配置选项并退出 `System Setup`，你需要通过 `Application Manager – System Admin` 文件夹、`SysMan` 菜单，或者通过以下命令手动从命令行调起 `System Setup`：

```
# /usr/sbin/sysman
# /usr/sbin/checklist
# /usr/sbin/setup
```

## 1.6 SysMan 菜单

`SysMan` 集成了大多数系统管理工具，并使其在多个不同的用户环境中可用。你可以通过 `SysMan` 菜单（一个层次化的、面向任务的菜单界面）访问这些工具。

`SysMan` 菜单中的所有任务都可以从支持 `X11` 的显示器、运行 `Microsoft Windows` 的个人电脑（如 `Windows NT Version 4.0`）或字符终端执行。启动 `SysMan` 菜单有多种方法：

要从 `CDE` 桌面启动 `SysMan` 菜单：

- 登录 `root` 并从 `CDE` 前置控制面板的 `SysMan Applications` 中选择 `SysMan Menu` 图标。
- 从 `Application Manager` 中的 `System Management` 组选择 `SysMan Menu` 图标。
- 从终端窗口的命令行提示启动 `SysMan` 菜单，输入以下命令：

```
# /usr/sbin/sysman
```

- 从 `SysMan Station` 启动 `SysMan` 菜单，选择视图中的图标，并在 `SysMan Tools` 菜单中选择 `SysMan_Menu`。

你可以使用菜单中的名称或其加速器（`accelerator`）从命令行启动特定任务，由于该误（原文误）加速器是 `sysman` 菜单中每个选项的唯一关键字。例如，运行调用权限分级（`DOP`）的任务，使用其加速器 `dopconfig` 并在系统提示符处输入命令：

```
# /usr/sbin/sysman dopconfig
```

使用以下命令获取可用任务及其加速器的完整列表。

```
# /usr/sbin/sysman -list
```

`SysMan` 菜单包含按层次结构（或树形结构）组织的选项文本列表。每个选项显示为树上的一个分支，通向子选项，子选项可能是进一步的分支或以任务结束。如果存在子任务，你可以折叠或展开每个选项，这由每个项目前的字符标出。加号 (`+`) 表示有更多菜单项可用；减号 (`-`) 表示该分支已完全展开。

分支末尾的任务前有一个竖线 (`|`)，表示该分支无法进一步展开，你只能选择任务来调用管理工具。

图 1-6：在 `CDE` 用户环境中调用的 `SysMan` 菜单。此菜单（原文误）的内容在你的系统上可能不同：

### 图 1-6：SysMan 菜单

![](img/6bce2e8b259cd153e89d4f71427eb696_44_0.png)

如图 1-6 所示，`Software` 分支（标签 1）已完全展开，显示了 `Installation` 分支和 `Register license data` 任务。`Installation` 分支（标签 2）包含多个任务，如 `Install software` 和 `List installed software`。当你选择一个任务时，将调用相应的工具。

你如何移动和选择菜单项或调用任务取决于你所使用的用户环境，例如 `curses` 终端或窗口环境。当使用终端时，使用方向键或 `Tab` 键在菜单中移动以展开分支或选择任务，在移动时会高亮选项和按钮。使用 `Enter` 键选择项目，这将展开分支或选择任务以调用关联工具。在窗口环境中使用鼠标时，你可以将指针移动到分支上并双击以进行选择。

`SysMan` 菜单上显示以下选项：

- 选择分支将展开或收叠它。选择任务将调用关联工具。
- `Find...`：启动搜索窗口，允许你根据关键词进行搜索并找到相关任务。
- `Help On`：对任何分支或任务提供与上下文相关的帮助。
- `Exit`：关闭 `SysMan` 菜单。
- `Options...`：为配置 `SysMan` 菜单提供选项，例如显示加速器。
- `Help`：提供 `SysMan` 菜单的通用帮助。

当你移动指针或使用 `Tab` 键移动到某个项目时，两行之间的面板中也会显示与上下文相关的帮助。

更多信息请参阅 `sysman(8)` 和在线帮助。相关工具请参阅附录 `A` 中的表。

## 1.7 使用 SysMan 命令行

`sysman-cli` 工具是 `SysMan` 菜单的命令行替代方案，允许你从命令行实现 `SysMan` 任务、查看系统数据或编写脚本来自自定义配置。当你设置系统部分内容（例如使用 `SysMan` 任务配置网络）时，你正在操作系统配置文件，如 `/etc/rc.config` 或 `/etc/hosts`。

使用 `sysman-cli` 选项需要 `root` 权限，尽管非权限用户可以使用它查看系统设置数据。有关如何使用权限分级（`DoP`）让非 `root` 用户成为 `SysMan` 任务的有权限用户，请参阅 `dop(8)`。这里介绍了 `sysman-cli` 工具许多功能的要介绍。选项和标志的完整列表请参阅 `sysman_cli(8)`。`/usr/examples/systems_management/sysman_cli` 中提供了一 `shell` 脚本示例。以下是一些命令行示例。

你可以使用 `sysman-cli` 命令显示菜单中所有可管理的组件。例如，使用以下命令列出 `SysMan` 菜单中的主要组件：

```
# sysman-cli list components
```

```
Component(s):
account_management
atm
audconfig
bindconfig
bttape
ciconfig
clschl
doprc
.
networkedSystems
```

以下命令显示 `networkedSystems` 组件包含的组：

```
# sysman-cli list group -comp networkedSystems
```

```
Component: networkedSystems
Group(s):
hostEquivalencies
hostEquivFileText
hostFileText
hostMappings
JoinMappingService
componentid
digitalmanagementmodes
```

以下命令显示 `networkedSystems` 组件中 `hostMappings` 组的当前数据值。这些数据是 `/etc/hosts` 文件的内容。

```
# sysman -cli -list values -group hostMappings /
comp networkedSystems
Component: networkedSystems
Group: hostMappings
() [] 127.0.0.1 localhost
argnot (local host) 16.140.112.139 argnot.xxx.yyy.com
jason server 16.140.112.3 jason.xxx.yyy.com
fleece [backup server] 16.140.112.28 fleece.xxx.yyy.com
() [] 150.2.3.4 newschat.pubs.com
```

对于 `SysMan` 菜单中的每个选项，`sysman -cli` 命令都允许您无需调用实用程序即可管理操作系统数据。例如，以下命令显示了如何从 `/etc/hosts` 文件中删除一个主机：

```
# sysman -cli -delete row -group hostMappings /
comp networkedSystems
```

请输入键 1 [systemName]: newschat.pubs.com

请输入键 2 [networkAddress]: 150.2.3.4

系统会提示您输入数据，以便实用程序识别 `/etc/hosts` 文件中的正确条目。由于 `SysMan` 菜单对存储在表中的数据进行操作，因此您需要标识要删除或修改的正确行。每行都有唯一的标识符，称为“键（keys）”，您必须通过 `sysman -cli` 命令选项来指定这些键。如果您没有提供键，系统会提示您输入。以下命令显示了如何确定特定表的键：

```
# sysman -cli -list keys -group hostMappings -comp /
networkedSystems
```

```
Component: networkedSystems
Group: hostMappings          Keys: systemName,networkAddress
```

您还可以使用 `sysman -cli` 命令从由 `SysMan` 更新的系统数据文件中添加或删除用户数据条目。例如，以下命令用于以交互式方式添加一个用户：
