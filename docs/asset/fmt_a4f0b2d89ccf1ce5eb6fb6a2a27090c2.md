
`/usr/dt/bin/dtconfig -e`

登录服务器将在系统重启后自动启动。

# 停止登录服务器

若要在下次系统启动时禁用 CDE 登录服务器，请输入以下内容：

```
/usr/dt/bin/dtconfig -d
```

此命令告诉系统在下次重启时不启动登录服务器。

您可以通过杀死其进程来立即停止登录服务器。输入以下内容：

```
/usr/dt/bin/dtconfig -kill
```

这将发出 `kill` 命令 `<login_server_ID>`。

这些自定义中的每一个都可以针对所有显示器进行，也可以针对单个显示器进行。由于这些自定义内容不在考试范围内，我没有在本章中介绍它们。如果您对学习更多关于自定义 CDE 内容感兴趣，我建议您参考 Solaris CDE 高级用户和系统指南。

# 启动登录服务器

登录服务器在系统启动时通过 `/etc/rc2.S99dtlogin` 脚本启动环境。它也可以从命令行启动。例如，要从命令行启动登录服务器，请输入：

```
/etc/init.d/dtlogin start
```

或者

```
/usr/dt/bin/dtconfig -daemon; exit
```

要停止登录服务器，请输入：

```
/etc/init.d/dtlogin stop
```

> 如果杀死登录服务器时用户已登录桌面，会话将立即终止。

# 附录 B CDE 的管理与配置 881

# 在本地显示上显示登录界面

启动时，登录服务器检查 `Xservers` 文件以确定是否需要启动 X 服务器以及如何在本地或网络显示器上显示。以下是 `Xservers` 文件中行的格式：

```
<login_name> <display_class> <display_type> \
X_server_command
```

`Xservers` 文件中的默认行类似于：
`local console /usr/bin/X11:0`

`Xservers` 文件中的每个字段见表 B.1。

要修改 `Xservers` 文件，请从 `/usr/dt/config/etc/xdt/config` 复制。`etc/xdt/` 目录包含特定工作站的配置文件。如果 `/etc` 不存在，您需要创建它。系统管理员可以通过创建 `/etc/xdt/config/` 来修改系统默认资源。在您的目录中，可以创建配置文件来覆盖默认资源或为所有桌面用户指定额外的资源。这在会话启动期间合并到桌面默认设置。此文件中指定的资源优于桌面文件中指定的资源。修改 `/etc/xdt/config/Xservers` 后，输入以下内容让登录服务器重启 X：

| 字段 | 描述 |
| :--- | :--- |
| display_name | 登录服务器在连接到 X 服务器时使用的名称（例如为 :0）。星号“ ”的值将展开为主机名:0。Xserver_command 中指定的数字与连接号匹配。 |
| display_class | 为此显示器指定资源（例如为 Local）。 |
| display_type | 告诉登录服务器此显示器是本地的或如何管理登录服务器上的命令行选项（例如为 local@console）。 |
| X_server_command | 指定登录服务器用于启动 X 服务器时使用的命令编号和其他其他选项（例如为 /usr/bin/X11/X）。指定的连接号必须与 display_name 字段中指定的数字匹配。 |

```
/usr/dt/bin/dtconfig -reset -HUP
login_process_ID.
```

# 附录 B CDE 管理与配置

会话管理器（Session Manager）负责启动桌面并自动保存和恢复应用程序、颜色、字体、鼠标行为、音量和键盘点击。使用会话管理器，你可以执行以下操作：

## 源 `$HOME/.dtprofile` 脚本

- 为所有桌面用户自定义初始化设置。
- 为所有桌面用户自定义环境和资源。
- 更改会话启动消息。
- 更改会话启动工具和守护的参数。
- 为所有用户自定义桌面颜色用法。

在启动时，`Xsession` 脚本会源用户的 `$HOME/.dtprofile` 脚本——这是一个 `/bin/sh` 或 `/bin/ksh` 脚本，用于为他们的会话设置环境变量。`.dtprofile` 只接受 sh 或 ksh。桌面的默认值为 `/usr/dt/config/sys.dtprofile`。如果 `$HOME/.dtprofile` 不存在（例如，当用户首次登录时），`Xsession` 会将默认的 `sys.dtprofile` 复制到 `$HOME`。

会话管理器通过 `/usr/dt/bin/Xsession` 启动。当用户登录时，登录管理器（Login Manager）默认启动。当会话管理器启动时，它将通过以下步骤启动用户的会话：

你可以通过从 `/usr/dt/config` 复制到 `/etc/dt/config` 并编辑新文件来自定义 `sys.dtprofile` 脚本。你也可以在 `$HOME/.dtprofile` 中设置个人环境变量。例如，`export VARIABLE="value"` 会在下次登录时在用户的环境中设置变量 `VARIABLE`。

1. 源 `.dtprofile` 脚本。
2. 源 `Xsession.d` 脚本。
3. 显示欢迎消息。
4. 设置桌面搜索路径。
5. 收集可用的应用程序。
6. 可选源 `$HOME/.profile` 或 `$HOME/.login`。
7. 启动 ToolTalk 消息守护。
8. 加载会话资源。
9. 启动颜色服务器。
10. 启动空间管理器（Workspace Manager）。
11. 启动会话应用程序。

要设置系统级变量，请在 `/etc/dt/config/Xsession.d` 目录下创建一个设置并导出该变量的文件。例如，如果你创建一个可执行的 ksh 脚本 `/etc/dt/config/Xsession.sitevars`，其内容包含 `export SITEVARIABLE='value'`，则该变量将在每个用户下次登录时设置到其环境中。

> 虽然会话管理器不会自动读取 `.profile` 或 `.login` 文件，但它可以配置为使用这些文件。要让 `Xsession` 源配置或登录脚本，请在 `$HOME/.dtprofile` 中将变量 `SOURCEPROFILE` 设置为 true

## 源 Xsession.d 脚本

在源 `$HOME/.dtprofile` 脚本后，`Xsession` 会源 `Xsession.d` 脚本以设置额外的环境变量并为用户的会话启动可选的守护进程。

要关闭欢迎消息，请设置 `dtstart_hello[]=""`。

## 设置桌面搜索路径

桌面使用登录时创建的搜索路径来定位应用程序及其相关的桌面文件。桌面提供了四个搜索路径，如表 B.2 所示。

> 任何启动文件中的错误都可能导致用户无法登录。要排除启动问题，请检查文件 `$HOME/.dtstart`。会话管理器在该文件中记录每个用户的会话启动进度。

## 表 B.2

| 搜索路径 | 描述 |
| :--- | :--- |
| Applications (应用程序) | 用于定位应用程序。管理器在用户登录时使用 Applications 搜索路径动态填充其顶层结构。 |
| Database (数据库) | 用于指定操作和数据类型文件 (*dtfiles) 以及前面板文件 (*fp files) 的额外位置。 |
| Icons (图标) | 用于指定图标的额外位置。 |
| Help data (帮助数据) | 用于指定桌面帮助数据的额外位置。 |

## 自定义欢迎消息

在源 `/etc/dt/config/sys.dtprofile`（如果存在）、`$HOME/.dtprofile` 和 `Xsession.d` 脚本后，`Xsession` 会显示一条覆盖屏幕的欢迎消息。你可以自定义欢迎消息或将其关闭。

使用 `dthello` 用于显示欢迎消息。要更改消息，请更改 `dthello` 变量。通过设置 `dtstart_hello[]`，在 `/usr/dt/config/Xsession.d` 脚本中创建一个设置新值的脚本。例如，若要为所有用户显示今日消息信息（message of the day），请创建一个名为 `/usr/dt/config/Xsession.d/myvars` 的可执行 sh 脚本，并如下设置 `dtstart_hello[]`：

```
dtstart_hello[]="/usr/dt/bin/dthello -file / /etc/motd &"
```

用户还可以通过在 `$HOME/.dtprofile` 中设置 `dtstart_hello[]` 来更改其会话的欢迎消息。

## 修改搜索路径

### 逐步操作

### B.1 修改搜索路径

要修改特定用户的搜索路径，请按照以下步骤操作：

1. 打开 `$HOME/.dtprofile` 进行编辑。
2. 添加或编辑定义并导出个人输入变量的行。

例如，以下行向用户的个人应用程序搜索路径添加了一个位置：

```
export DTSOURCE_HOSTS=$~/projects1/editors
```
