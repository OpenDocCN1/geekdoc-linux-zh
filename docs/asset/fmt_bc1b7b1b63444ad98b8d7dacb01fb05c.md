
> 如果你不使用 `elm` 读邮件但想完成此练习，你可以用你的邮件读取器名称替换 `elm`，或者完成练习并在 `elm` 询问是否应该创建文件夹时回答“否”。这样运行 `elm` 不会对你的配置产生永久影响。如果你使用基于 XWindow 的邮件读取器，请选择窗口类型为 `Graphical`（图形化）。

在图 6.5 所示的“创建动作”对话框中，你只需要指定一个动作名称；在顶部的框中使用 `Read Mail`，在运行命令中使用 `elm`。此外，选择窗口类型为 `Terminal (Auto-Close)`（终端（自动关闭））。填写这些字段后，从“文件”中选择“保存”。

### 图 6.5.

创建动作对话框。

| 创建动作 (Create Action) |

| :--- |

| 文件 选项 帮助 |

| 动作名称 (图标标签): |

| 1 |

| 动作图标: |

| | 查找 设置... 编辑图标... |

| 动作打开时执行命令 (双击): |

| | 动作图标文本: |

| | 窗口类型: Graphical (图形化) |

| | 高级 |

你现在在应用程序管理器中有一个名为 `Read Mail` 的图标。如果你想，可以将此图标放在 `/etc/dt/types` 目录树中。你可以在主目录 `$HOME/.dt/types` 中创建一个名为 Mail 的配置文件。由于你在个人配置中指定了 Mail 控件，覆盖了默认控件。

## 创建控件

通过这个新动作，你可以创建一个新的控件：

```
CONTROL MyMail
{
  TYPE              icon
  CONTAINER_NAME   Top
  CONTAINER_TYPE    BOX
  POSITION_HINTS    5
  ICON             DtMail
  LABEL            Mail
  ALTERNATE_ICON   DtMew
  MONITOR_TYPE      mail
  PUSH_ACTION       DtMail
  PUSH_RECALL       true
}
```

这创建了一个名为 `Games` 的子面板，并将其放置在 `Calendar` 控件上方，由工作管理器自动创建。

现在使用应用程序管理器中的“创建动作”工具创建一个名为 `Spider` 的动作。然后在 `$HOME/.dt/types` 中创建一个 `Spider.fp` 文件，其包含以下内容：

```
CONTROL Spider
{
  CONTAINER_NAME   Games
  CONTAINER_TYPE   SUBPANEL
  LABEL            Spider
  ICON             redhat_footer
  PUSH_ACTION       Spider
  PUSH_RECALL       true
}
```

当桌面重启时，`Games` 子面板中会出现一个红帽图标。点击它时，将启动蜘蛛应用程序。

## 修改控件

现在你已经成功创建了控件，可以使用简单的方法。将 `myownmail.fp` 移动为 `mymail.fp`。修改包含此内容的文件：

```
CONTROL Mail
{
  TYPE           icon
  CONTAINER_NAME Top
  CONTAINER_TYPE BOX
  POSITION_HINTS 5
  ICON           DtMail
  LABEL          Mail
  ALTERNATE_ICON DtMew
  MONITOR_TYPE   mail
  PUSH_ACTION    DtMail
  PUSH_RECALL    true
}
```

当桌面重启时，前面板保持不变。因为你在个人配置中指定了 Mail 控件，该配置先读取，覆盖了默认控件。

## 创建和修改子面板

之前你使用鼠标创建新的子面板并向其添加图标。当你通过这种方式更改时，它们会被添加到 `$HOME/.dt/types` 的 `fp_dynamic` 子目录下。不要通过编辑这些文件来对子面板进行更改和添加。

## 创建子面板

`SUBPANEL` 定义看起来与 `CONTROL` 非常相似：

```
SUBPANEL Games
{
  CONTAINER_NAME    Date
  TITLE             Games
}
```

## 修改子面板

与默认控件一样，默认子面板是可以修改的。

要移除安装控件，添加

```
CONTROL_INSTALL False
```

要向子面板添加，指定子面板为容器。例如，将以下内容放在 `$HOME/.dt/types` 目录下的 `.fp` 文件中，将为帮助子面板添加一个方便的帮助页控件。

## 常用桌面环境 (CDE)

第 6 章

```
{
TYPE file
CONTAINER_TYPE SUBPANEL
CONTAINER_NAME HelpSubpanel
POSITION_HINTS last
ICON Dhover
FILE_NAME /usr/dt/appconfig/appmanager/C/Desktop_Apps/Dtmanpageview
HELP_STRING The Page Viewer (Dtmanpageview) action displays a man in Quick Help window.
}
```

当将页面查看器（Page viewer）拖入文件时，安装图标（Install Icons）会向文件中插入上述内容。两个重要的指令是 `CONTAINER_TYPE` 和 `CONTAINER_NAME`，它们指定了容器类型（即子面板，`SUBPANEL`）及其名称。

如果可能，使用安装图标可能是最好的机制，因为可以避免错误和多余的细节（例如前一个示例所示的帮助信息）。

## 子面板行为

当你点击子面板上的控件时，它们的默认行为是关闭。你可以覆盖此行为，但要这样做，必须修改默认的 `PANEL` 定义。

在 `HOME/.dt/types` 下创建一个名为 `main.fp` 的文件。将 `/usr/dt/appconfig/types/C/dtwm.fp` 中找到的默认 `PANEL` 定义复制到 `main.fp` 中（大约从第18 行开始）。

```
PANEL FrontPanel
DISPLAY_HANDLES True
DISPLAY_MENU True
DISPLAY_MINIMIZE True
CONTROL_BEHAVIOR single_click
DISPLAY_CONTROL_LABELS False
HELP_TOPIC FPButtonItemPanel
HELP_VOLUME FP
```

添加以下指令：

```
SUBPANEL_UNPOST False
```

这是一个利用每次初始化 CDE 时如何构建前面板（Front Panel）方式的良好示例。系统管理员可以将此修改添加到 `/etc/dt/appconfig/types/C` 区域。

## 出错时恢复会话

工作区管理器（Workspace Manager）在保存新会话时总是保存上次会话的备份。如果出现问题，可以激活此备份会话以恢复登录正常。

## 配置其他服务器

第二部分

使用安全模式（Fail-safe）或命令行登录（CommandLine Login），或切换到任意虚拟终端登录。

切换到 `$HOME/.dt/sessions` 目录。旧会话在 `current.old` 目录中。将其复制到当前目录——例如：

```
cd current.old; find . | cpio -pdw ../current
```

## 登录时执行应用程序和命令

当用户首次登录桌面时，会执行 `/usr/dt/config/language/` 下的 `sys.session` 脚本。它会启动几个桌面应用程序，包括帮助查看器（Help Viewer）。

随默认 CDE 包一起的大的文件（如 `sys.session`）不应被修改。相反，用户应该在 `/etc/dt/config/language/` 中放置一个副本并对其进行修改。在用户首次注销后，他或她将有一个用于恢复桌面的目录或会话，该脚本不会再次运行。

你可能想在登录时执行一些无法通过 CDE 设置的命令，例如作为守护进程，或者通过 `xv` 或 `xsetroot` 运行应用程序以设置备用的根窗口背景。要这样做，请在 `$HOME/.dt/sessions` 目录下创建一个名为 `sessionetc` 的脚本。

例如，以下脚本将在登录时将 `companylogo.jpg` 文件设置为背景：
