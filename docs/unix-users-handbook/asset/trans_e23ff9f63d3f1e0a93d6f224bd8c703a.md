

创建下拉菜单很简单，并且可以通过向菜单添加子菜单轻松扩展。只需在菜单名称后加上函数 **f.menu** 即可。我们会在“Admin1’s Menu”之后添加以下内容：

```
“Work Menu” f.menu WorkMenu”

然后在 Menu AdminMenu 部分的 } 之后，添加：
Menu WorkMenu
{
.
}
```

执行这些高级功能其实并不难。最难的部分是记住将文件放入哪些目录：全局更改使用 */etc/dt*，个人更改使用 $HOME/dt。

## 创建控制按钮、操作和文件类型

操作启动一个进程，例如 shell 脚本或应用程序。操作可以连接到前面板按钮，以便在按下按钮时启动。操作可以连接到前面板投放区，以便在数据文件被投放到投放区时执行。操作可以与文件管理器窗口中的图标相关联，这样双击图标即可启动该操作。操作还可以与特定的数据类型相关联，这样双击数据文件图标即可启动操作并打开该数据文件。

除了设置前面板和默认会话以满足用户需求外，你能为依赖你的人让计算生活变得更加轻松的最重要的一件事，就是创建操作和数据类型。

CDE 操作和数据类型定义在以 **.dt** 结尾的文件中。与大多数其他 CDE 配置文件类似，*.dt* 文件有系统级版本，可以复制到用户的个人目录中并进行个性化定制。大多数系统级 *.dt* 文件位于 /usr/dt/appconfig/types/C；个人 *.dt* 文件通过从 /usr/dt/appconfig/types/C 复制 **user-prefs.dt** 到 $HOME/.dt/types 来创建。

CDE 用于查找操作和文件类型的默认搜索路径包括以下主要目录，按列出的顺序排列：

- $HOME/.dt/types
- /etc/dt/appconfig/types
- /usr/dt/appconfig/types

你可以使用 **DTDATABASESEARCHPATH** 环境变量向搜索路径添加更多目录。将此环境变量和新搜索路径插入 /etc/dt/config/Xsession 以获得系统范围的影响。将环境变量和搜索路径插入 **$HOME/.dtprofile** 以针对个人用户。

控制按钮 - 基本控制定义有六个部分：

- **CONTROL name** - 定义名称。这是定义中位于花括号外的唯一部分。
- **TYPE** - 控制的类型。存在多种类型。对于自定义前面板最有用的可能是 blank（空白）和 icon（图标）。blank 可用作占位符。icon 可以启动操作或应用程序，或者作为投放区。
- **ICON** - 在前面板上显示的位图。前面板位图位于 **/usr/dt/appconfig/icons** 目录中。
- **CONTAINER_NAME** - 容纳该控制的容器名称。这必须与 **dtwm.fp** 中列出的某个实际容器的名称相对应。
- **CONTAINER_TYPE** - 容纳该控制的容器类型。这可以是 **BOX**、**SWITCH** 或 **SUBPANEL**，但它必须与容器名称的类型一致。
- **PUSH_ACTION** - 这是按下控制按钮时发生的情况。**PUSH_ACTION** 只是几种可能的操作之一。欲了解更多信息，请参阅 **dtwm** 手册页。

要从前面板移除控制按钮，请在 CONTROL 定义行的最左列输入井号（#）。这 (#) 会将控制规范变成注释行。

通过编辑 dtwm.fp 文件来添加控制按钮：

1. 将 dtwm.fp 从 /usr/dt/appconfig/types/C 复制到 /etc/dt/appconfig/types/C。
2. 使用以下格式添加新的控制定义：

```
CONTROL NewControl
{
  TYPE                icon
  CONTAINER_NAME Top
  CONTAINER_TYPE BOX
  ICON                NewControlBitmap
  PUSH_ACTION         NewControlExecutable
}
```

操作和文件类型有其自身的特殊性，即每个都有几个部分，且每个都必须位于其自己的目录位置中。当我们创建子面板上的操作时，这种特殊性会变得清晰。以下是创建操作或文件类型定义的建议位置：

- 在 /etc/dt/appconfig/types 目录中创建一个完全新的文件。该文件具有系统范围的影响。请记住，文件必须以 .dt 扩展名结尾。
- 从 /usr/dt/appconfig/types 复制 user-prefs.dt 到 /etc/dt/appconfig/types 目录，并在那里插入定义以供系统范围内使用。
- 将 user-prefs.vf 复制到 $HOME/.dt/types，并在那里插入定义以供个人用户使用。

典型操作具有如下语法：

```
ACTION      ActionName
{
 TYPE       type
        keyword  value
        keyword  value
    }
```

例如，这是一个 FrameMaker 操作：

```
ACTION        FRAME
{
    TYPE      COMMAND
    WINDOW-TYPE NO-STDIO
    EXEC-STRING /nfs/hpcvxmk6/usr/frame/bin/maker
}
```

典型数据类型具有如下语法：

```
DATA_ATTRIBUTES    AttributesName
{
    keyword   value
    keyword   value
    ACTIONS   action, action
}
DATA_CRITERIA
{
    DATA_ATTRIBUTES AttributesName
    keyword   value
    keyword   value
}
```

注意，所有定义都具有以下通用语法：

```
    KEYWORD value
```

请注意，数据类型定义实际上分为两部分：属性部分和条件部分。数据类型定义中的属性部分指定数据类型的外观；条件部分指定数据类型的行为。

例如，这是一个使用 FRAME 操作的 FrameMaker 文件类型：

```
DATA_ATTRIBUTES FRAME_Docs
{
 DESCRIPTION This file type is for FrameMaker documents.
ICON makerIcon
ACTIONS FRAME
}
DATA_CRITERIA
{
DATA_ATTRIBUTES_NAME FRAME_Docs
NAME_PATTERN *.fm
MODE f
}
```

你可以使用这些格式从头创建操作和文件类型。然而，创建操作最简单的方法是使用 **CreateAction** 工具。**CreateAction** 位于应用程序管理器（Application Manager）中的桌面应用程序（Desktop Applications）文件夹中，它会向你展示一个填空式对话框，引导你创建包含操作定义的 *action.dt* 文件。然后你可以将此文件移动到适当的目录，以获得你希望操作具有的影响范围：系统范围的影响使用 /etc/dt/appconfig/types；个人用户使用 $HOME/.dt/types。

## 创建新图标和操作

创建图标是一项具有挑战性的任务。我们可以使用 Desktop_Apps 中的图标编辑器（Icon Editor）来创建新图标，或者我们可以找到喜欢的图片并使用它。从外部引入图片时需要注意的一件事是，为了在前面板上正确显示，图片尺寸不得超过 32x32 像素，否则只会显示图标的部分。在图标编辑器中查看图片可以显示图片的尺寸。您可能需要浏览应用程序目录以查找有用的图标，或从互联网上下载一个。

在这个完整的示例中，我将使用 HP-UX 附带的 Instant Information 软件。这是 CD 上的用户手册集。其他应用程序软件也能同样良好地工作；只需确保你的路径与你使用的软件相对应。此外，我将使用一个虚构用户的家目录：/home/admin1。

1. 从 Desktop_Apps (HP-UX)、Deskoptools (AIX) 或 Solaris 上的 Desktop_Tools，在应用程序管理器中**打开图标编辑器**。
2. 选择**文件 -> 打开**。
3. 输入路径或文件夹名称： **/opt/dynatext/data/bitmaps**。
4. 输入文件名称： **logoicon.bm**
5. 选择**打开**。

我们将看到图标，并确认它确实是 32x32。现在我们需要将图标保存到我们自己的 .dt 目录。

6. 选择**文件 -> 另存为**。
7. 输入路径或文件夹名称： **/$HOME/.dt/icons**。对于 admin1 用户，这将在 **/home/admin1/.dt/icons** 中。

如果我们要全局执行此任务，我们会将其放在 **/etc/dt/appconfig/types/C** 中。

8. 保持文件名不变。
9. **保存**。

现在我们已经有了图标，我们需要创建一个操作文件和描述文件来配合它。

1. **使用你喜欢的文本编辑器**，输入以下内容：

```
ACTION instinfo
{
    LABEL       instinfo
    TYPE        COMMAND
```

