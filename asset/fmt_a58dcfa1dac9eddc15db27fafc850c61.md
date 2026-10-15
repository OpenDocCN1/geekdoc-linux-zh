
因为它可以在系统范围内执行脚本和启动客户端，所以 `Xstartup` 类似于 `sys.session`。区别在于 `Xstartup` 以 root 身份运行。因此，对 `Xstartup` 的修改应保留用于挂载文件系统之类的操作。

`Xreset` 是 `Xstartup` 的系统级伴随脚本。它以 root 身份运行，基本上撤销了 `Xstartup` 所启动的内容。

`Xfailsafe` 文件包含对标准故障安全会话的自定义。故障安全会话提供了一种纠正由登录和会话配置文件中的错误导致的错误 CDE 会话的方法。因此，`Xfailsafe` 是您的用户永远不会使用的东西，但您可以通过一些明智的自定义让生活稍微轻松一些。

`sessionetc` 文件位于用户的 `.dt/sessions` 目录中，并个性化该用户的 CDE 会话。`sessionetc` 处理启动额外的 X 客户端，如 `sys.session`，但基于每个用户，而非系统范围。虽然 `dt.session` 也基于每个用户启动客户端，但这些客户端是默认或当前会话的客户端。`dt.session` 位于 `.dt/session/current.sessionetc` 中，而后者位于 `.dt/session` 中，并且应该仅包含那些未自动恢复的客户端。通常，这些是未正确设置 `WM_COMMAND` 的客户端，因此会话管理器无法保存或恢复它们；因此需要在 `sessionetc` 中重新启动它们。

`sys.font` 文件包含系统范围、默认的会话字体配置。这些默认字体基于可用性研究，因此 `sys.font` 是一个您可能永远不会更改的文件。但是，如果您遇到需要在系统范围内使用不同字体组合的情况，这里就是您更改它们的地方。请注意，`sys.font` 中提到的字体资源和值必须与 `/usr/dt/app-defaults/C/Dtstyle` 文件中指定的默认字体资源完全匹配。

CDE 有一堆指定 CDE 操作和数据类型定义的文件。所有这些文件都以文件扩展名 `*.dt` 结尾。`*.dt`（"dt" 代表 "desk top"）包含数据类型和操作定义。默认的 `*.dt` 文件位于 `/usr/dt/appconfig/types/C`，并在系统范围内起作用。类似地，`user-prefs.dt`，其主副本也位于 `/usr/dt/appconfig/types/C`，在个人用户级别使用。

`.Xauthority` 文件是一个用户特定的配置文件，包含需要授权机制才能连接到服务器的客户端所需的授权信息。

### CDE 配置文件位置

CDE 查找特定配置文件的位置取决于配置文件的性质，主要是文件配置的内容及其影响范围有多大。表 4-3 显示了基于文件内容性质的系统和用户配置文件的位子。

对于表 4-3 中列出的每个默认系统范围文件位置，都存在一个对应的自定义系统范围配置文件位置。这些自定义文件应位于 `/etc/dt` 下的适当子目录中。基本操作是从 `/usr/dt/something` 复制您需要自定义的文件到 `/etc/dt/something`，然后在那里进行修改。例如，要更改 `Xresources` 中的默认标志，请将 `/usr/dt/config/C/Xresources` 复制到 `/etc/dt/`

在 `config/C/Xresources` 中，打开 `/etc/dt/config/C/Xresources`，并进行您的修改。

**表 4-3 CDE 系统与用户配置文件**

| 配置文件的性质 | 系统范围影响 | 用户个人影响 |
|---|---|---|
| 环境变量 | `/usr/dt/config/` | `$HOME/` |
| 外观与行为资源 | `/usr/dt/config/C` `/usr/dt/app-defaults/C` | `$HOME/.dt/` `$HOME/.dt/sessions/current/` `$HOME/.dt/sessions/home/` |
| 文件类型与操作定义 | `/usr/dt/appconfig/types/C` | `$HOME/.dt/types` |
| 登录时客户端启动 | `/usr/dt/config/` `/usr/dt/config/C` | `$HOME/.dt/session/` `$HOME/.dt/session/current/` `$HOME/.dt/session/home/` |
| 工作区管理器 | `/usr/dt/config` | `$HOME/.dt/` |

这是一个重要的要点。位于 `/usr/dt` 下的文件被视为 CDE 系统文件，并在更新期间被覆盖。因此，您在那里所做的任何自定义都会丢失。请对所有系统范围配置文件的修改在 `/etc/dt` 及其子目录中进行。

#### 配置文件如何协同工作

根据迄今所介绍的材料，您可能正确地得出结论：CDE 配置文件并不是可以在没有计划的情况下随意乱改的东西——需要一个深思熟虑的计划。您可能已经弄清楚，您想要配置的要素以及您希望它拥有的影响范围，决定了您修改哪个配置文件。

例如，如果您想设置环境变量，您有四个配置文件可供选择：`sys.dprofile`、`Xconfig`、`Xsession` 和 `.dprofile`。但如果您想设置仅影响特定用户的环境变量，您的选择立即缩小到单个文件，即 `.dprofile`。

现在，拼图中唯一剩下的部分就是理解 CDE 读取其配置文件的顺序。当某个配置要素（环境变量、资源、操作或数据类型）被指定了两次但值不同，您显然希望使用正确的值，并忽略错误的值。

以下规则适用：

- 对于环境变量，使用最后指定的值。
- 对于资源，使用最后指定的值。然而，这受具体性（specificity）的影响。因此，对于 Emacs 客户端，`*emacs*foreground` 优先于仅 `foreground`，无论资源的出现顺序如何。
- 对于操作，使用第一次指定的。
- 对于数据类型，使用第一次指定的。

表 4-4 说明了当 CDE 读取其配置文件中配置要素的多个指定时，使用哪一个指定：

**表 4-4 CDE 用于配置的内容**

| 配置要素 | 使用的要素 |
| :--- | :--- |
| 资源 | 最后遇到的或最具体的 |
| 环境 | 最后遇到的 |
| 操作 | 第一次遇到的 |
| 文件类型 | 第一次遇到的 |

用范围来说，用户配置文件覆盖系统范围的配置文件。查看仅系统范围配置文件的优先级顺序，`/etc/dt` 中的文件优先于 `/usr/dt` 中的文件，因此全局自定义配置优先于 CDE 默认配置。并且 `$HOME/.dt` 文件优先于 `/etc/dt` 中的文件。

对于资源，即用于指定 GUI 外观和行为的要素，CDE 根据以下优先级设置值：

1. **命令行** - 当您从命令行启动客户端时，命令行上列出的选项具有最高优先级。
2. `Xresources`、`.Xdefaults`、`dt.resources`、`sys.resources`， - 当 CDE 启动时，它会读取这些资源配置文件，以确定用于会话的 X 资源的值。
3. **RESOURCE MANAGER** - 属性中已有的资源 `RESOURCE_MANAGER` 可能会影响刚刚启动的应用程序。
4. `app-defaults` - 指定与内置资源值不同的“默认”资源值。
5. **内置默认值** - “硬编码”的默认资源具有最低优先级。

具体的资源指定优先于一般的资源指定。例如，假设您希望在文本输入区域中使用某种字体。您可以在个人的 `.Xdefaults` 文件中正确指定 `FontList` 资源，但可能会被 `app-defaults` 文件中的 `*XmText*FontList` 覆盖。虽然 `app-defaults` 的优先级低于 `.Xdefaults`，但在那里设置资源指定更具体，因此它优先。

对于环境变量，CDE 根据以下优先级设置值：

1. `$HOME/.dtprofile` - 用户特定的变量具有最高优先级。
2. `/etc/dt/config/C/Xsession` - 未被 X 服务器读取的自定义系统范围变量。
3. `/etc/dt/config/C/Xconfig` - 被 X 服务器读取的自定义系统范围变量。
4. `/usr/dt/config/C/Xsession` - 未被 X 服务器读取的默认系统范围变量。
5. `/usr/dt/config/C/Xconfig` - 被 X 服务器读取的默认系统范围变量。
6. `/usr/dt/bin/dtlogin` - 内置默认变量具有最低优先级。

对于数据类型和操作定义，CDE 按以下优先级查找 `.dt` 文件：

1. `$HOME/.dt/types`
2. `/etc/dt/appconfig/types/C`
3. `/usr/dt/appconfig/types/C`
