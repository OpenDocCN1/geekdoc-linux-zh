
- 7. 启动 ToolTalk 消息守护进程。
- 8. 加载会话资源。
- 9. 启动颜色服务器。
- 10. 启动工作区管理器。
- 11. 启动会话应用程序。

## 载入 .dtprofile 脚本

会话启动时，xsession 脚本载入用户 HomeDirectory/.dtprofile 脚本——一个用于使用户能够为其会话设置环境变量的 /bin/sh 或 /bin/ksh 脚本。.dtprofile 仅接受 sh 或 ksh 语法。桌面默认文件为 /usr/dt/config/sys.dtprofile。如果 HomeDirectory/.dtprofile 脚本不存在（例如用户首次登录时），xsession 会将桌面默认的 sys.dtprofile 复制到 HomeDirectory/.dtprofile。

您可以通过将其从 /usr/dt/config 复制到 /etc/dt/config 并编辑新文件来自定义 sys.dtprofile 脚本。您可以在 HomeDirectory/.dtprofile 中设置个人环境变量。例如，

```
export MYVARIABLE="value"
```

在下次登录时设置用户环境中的变量 MYVARIABLE。

要设置系统范围的环境变量，请在 /etc/dt/config/Xsession.d 目录中创建一个设置并导出该变量的文件。例如，如果您创建一个可执行 ksh 脚本 /etc/dt/config/Xsession.d/sitevars，其中包含

```
export SITEVARIABLE="value"
```

该变量 SITEVARIABLE 将在下次登录时设置在每个用户的环境中。

> 注意。虽然会话管理器不会自动读取 .profile 或 .login 文件，但可以配置为使用这些文件。要指示 xsession 载入 .profile 或 .login 脚本，请在 HomeDirectory/.dtprofile 中将变量 DTSOURCEPROFILE 设置为 True。

## 载入 Xsession.d 脚本

载入 HomeDirectory/.dtprofile 脚本后，xsession 脚本载入 xsession.d 脚本。这些脚本设置额外的环境变量并为用户会话启动可选守护进程。

**CAUTION!** 任何会话启动文件中的错误都可能阻止用户登录。要排查会话启动问题，请检查文件 HomeDirectory/.dt/startlog。会话管理器在此文件中记录每个用户的会话启动进度。

## 欢迎消息

载入 HomeDirectory/.dtprofile 和 Xsession.d 脚本后，Xsession 会显示覆盖屏幕的欢迎消息。您可以自定义欢迎消息或完全关闭该消息。

使用 dtHello 客户端显示欢迎消息。要更改消息文本，请通过修改 dtstart_hello[] 变量来更改 dtHello 选项。要更改 dtstart_hello[]，请创建一个设置新值的 /usr/dt/config/Xsession.d 脚本。例如，要为所有用户显示每日消息，请创建一个名为 /usr/dt/config/Xsession.d/myvars 的可执行 sh 或 ksh 脚本并按如下方式设置 dtstart_hello[]：

```
dtstart_hello[]="/usr/dt/bin/dthello -file /etc/motd &"
```

用户还可以通过在 HomeDirectory/.dtprofile 中设置 dtstart_hello[] 来更改其会话的欢迎消息。要关闭欢迎消息，请将 dtstart_hello[]=" "。

## 设置桌面搜索路径

桌面使用在登录时创建的搜索路径来定位应用程序及其关联的桌面文件。桌面提供四个搜索路径，见表 7-2。

### 表 7-2 桌面搜索路径

| Search Path | Description |
|---|---|
| Applications | 用于定位应用程序。应用程序管理器使用应用程序搜索路径在用户登录时动态填充其顶层。 |
| Database | 用于指定操作和数据类型定义文件 (*.dt 文件) 以及前置面板文件 (*.fp 文件) 的额外位置。 |
| Icons | 用于指定图标的额外位置。 |
| Help data | 用于指定桌面帮助数据的额外位置。 |

## 修改搜索路径

要为特定用户修改搜索路径，请按以下步骤操作：

- 1. 打开 HomeDirectory/.dtprofile 进行编辑。
- 2. 添加或编辑定义并导出个人输入变量的行。
  例如，以下行将位置添加到用户的个人应用程序搜索路径：
  `export DTSUSERAPPPATHS=:/projects1/editors`
- 3. 要使更改生效，请注销然后重新登录。

## 收集可用应用程序

设置桌面搜索路径后，下一步是通过使用 dtappgather 收集可用应用程序。这些是将在应用程序管理器窗口中显示的应用程序。dtappgather 实用程序收集应用程序文件以供应用程序管理器展示，并负责创建和刷新用户的应用程序管理器子目录。

要更改 dtappgather 的命令行选项，请在所有用户的 /etc/dt/config/Xsession.d/sitevars 文件中或单个用户的 HomeDirectory/.dtprofile 中修改 dtstart_appgather 变量。按如下方式设置 dtstart_appgather：

```
dtstart_appgather="/usr/dt/bin/dtappgather &"
```

## 载入用户 .profile 或 .login 文件

Xsession 能够载入用户的传统 $HOME/.profile 或 $HOME/.login 脚本，但默认情况下此功能被禁用。要指示 Xsession 载入 .profile 或 .login 脚本，请在 $HOME/.dtprofile 中将 DTSOURCEPROFILE 设置为 true。

## 启动 ToolTalk 消息守护进程

Xsession 的下一个任务是启动 ToolTalk 消息守护进程。ToolTalk 服务使独立的应用程序能够在彼此之间没有直接了解的情况下进行通信。应用程序创建并发送 ToolTalk 消息以相互通信。ToolTalk 服务接收这些消息，确定接收者，然后将消息传递给适当的应用程序。用户可以通过按如下方式在 $HOME/.dtprofile 中设置 dtstart_ttsession 变量来更改其会话的 tt 会话选项：

```
dtstart_ttsession="/usr/dt/bin/ttsession -s"
```

## 加载会话资源

资源用于应用程序设置某些外观和行为方面。例如，样式管理器 (dtstyle) 提供资源，使您能够指定系统查找包含调色板信息的文件的位置：

```
dtstyle*paletteDirectories: /usr/dt/palettes/C \ HomeDirectory/.dt/palettes
```

资源在会话启动时由会话管理器加载。桌面默认资源可在 /usr/dt/config/language/sys.resources 中找到。这些资源通过 RESOURCE_MANAGER 属性提供给每个用户的会话。此文件不应被编辑，因为在后续桌面安装中会被覆盖。系统管理员可以通过创建 /etc/dt/config/language/sys.resources 来修改系统默认资源。在此文件中，您可以覆盖默认资源或为所有桌面用户指定额外资源。

用户可以通过其 HOME/.Xdefaults 文件修改桌面默认和系统范围的资源。此文件中指定的资源优先于桌面默认或系统管理员资源文件中指定的资源。

## 启动颜色服务器

您可以使用样式管理器（如图 7-1 所示）或通过自定义样式管理器用于控制桌面颜色使用的颜色资源来为显示器选择各种颜色。

Figure 7-1
The Style Manager.

![](img/85737305a4c9aeecbcadd9986d604c02_143_0.png)

通过创建 /etc/dt/config/language/sys.resources 并在该文件中指定颜色服务器资源，为所有用户设置颜色服务器资源。用户也可以通过在 $HOME/.Xdefaults 中指定颜色服务器资源来为其会话设置颜色服务器资源。

## 启动工作区管理器

会话管理器负责启动工作区管理器。默认情况下，会启动 /usr/dt/bin/dtwm。工作区管理器是桌面提供的窗口管理器，控制

- 窗口框架组件的外观
- 窗口的行为，包括其堆叠顺序和焦点行为
- 键绑定和按钮绑定
- 最小化窗口的外观
- 工作区和窗口菜单

此外，工作区管理器控制表 7–3 中概述的桌面组件。

### 表 7–3 桌面组件

| Component | Description |
|---|---|
| Workspaces | 工作区管理器控制工作区的数量并跟踪每个工作区中打开的窗口。 |
| Workspace backdrops | 用户可以使用样式管理器更改背景图像。然而，背景管理是工作区管理器的功能。 |
| The Front Panel | 尽管前置面板使用自己的配置文件，但它由工作区管理器创建和管理。 |

可以对工作区管理器进行的额外修改包括更改工作区的数量并提供系统范围的工作区名称。

## 在系统范围内更改工作区数量

默认桌面配置提供四个工作区。用户可以使用与工作区切换关联的弹出菜单添加和删除工作区。

在 /usr/dt/app-defaults/C/Dtwm 文件中，workspaceCount 资源被设置为以下默认工作区数量：

```
Dtwm*0*workspaceCount: 4
Dtwm*workspaceCount: 1
```

在屏幕 0 上指定多个工作区；在任何其他屏幕上指定单个工作区。您可以创建（或如果存在则修改）/etc/dt/config/C/sys.resources 文件，以更改工作站上所有新用户的默认工作区数量。

使用 0*workspaceCount 资源在主屏幕上设置系统范围的默认值：

```
Dtwm*0*workspaceCount: number
```

例如，以下资源将主屏幕上系统范围的工作区数量设置为六：

```
Dtwm*0*workspaceCount: 6
```
