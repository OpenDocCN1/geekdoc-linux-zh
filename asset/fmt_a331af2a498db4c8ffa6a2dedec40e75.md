
CMS 命令中实用的`help`命令提供了有关许多标准系统任务的信息。它还提供了所有 CMS 和 CP 命令的语法和功能，以及可能报告给用户的错误消息的含义。

如果您记不起命令的格式，或者正在寻找有关命令功能的信息，请使用`help`命令。输出显示的信息与 IBM 文档中包含的信息相同。

易于使用的`help`命令类似于 Linux 系统上的`man`命令。如果您单独输入`help`，将显示选项及其描述的列表。

本章接下来的几个部分解释了如何更直接地访问`help`命令。要从菜单中选择一个条目，将光标放在适当的单词上并按 Enter。另一个帮助窗口打开，例如任务菜单或命令菜单。

**z/OS 类比：** `help`命令类似于`TSO HELP`或 ISPF 中的 HELP 面板。

#### 任务菜单

任务菜单是帮助系统的部分，它提供了您可以执行的任务的索引和描述，包括创建、修改或更改文件，或自定义 CMS 安装。任务菜单提供有关特定操作的详细信息，而无需您事先知道命令的名称。

当您导航到（向下钻取到）特定主题的最低级别时，您会找到命令的描述和正确格式。

要查看可用的任务和组件列表，请键入以下不区分大小写的命令：

```
help task
```

图 2-5 显示了`help task`命令的输出。

```
HELP TASK                  Task Help Information                  line 1 of 39
(c) Copyright IBM Corporation 1990, 2004

z/VM Help, main panel

This panel lists other Help panels that provide information about
various z/VM functions, topics, and tasks.
To view a Help panel, move the cursor to any character of the name
and press the ENTER key or the PF1 key.

HELPINFO  - HELP Facility topics
MENUS     - z/VM Help menus
TASKS     - Basic z/VM tasks - good choice for beginners
COMMANDS  - z/VM commands available to general users
CMS       - CMS commands
CP        - CP commands
QUERYSET  - QUERY and SET commands and subcommands
TCP/IP    - TCP/IP commands
PF1= Help   2= Top      3= Quit     4= Return    5= Locate   6= ?
PF7= Backward 8= Forward 9= PFkeys 10=           11=          12= Cursor

====> _

Macro-read 1 File
40 a                                                       23/007
```

图 2-5 `help task`命令的输出

#### 组件菜单

组件菜单列出了特定 HELP 组件可用的所有命令 HELP 文件的名称。

要显示 CMS 可用的所有命令 HELP 文件，请从图 2-5 中所示的任务帮助信息窗口（HELP TASK 菜单）开始。将光标定位在 CMS 单词下的任何位置，然后按 Enter。

菜单帮助信息窗口显示如下图 2-6 所示。窗口显示了 CMS 可用的所有命令 HELP 文件。

```
CMS MENU                      Menu Help Information                     line 1 of 42
(c) Copyright IBM Corporation 1990, 2004

Help for CMS commands

To view a Help panel, move the cursor to any character of the name
and press the ENTER key or the PF1 key.
An asterisk (*) preceding the name indicates a MENU panel.
A colon (:) preceding the name indicates a TASK panel.

*BORDER   CMDCALL   DSERV    GLOBALV   NETLCNVT   RT       SYNMSGS
*CMSQUERY CMSBATCH Edit     GRAnt     NOTE       RTNDrop  SYNonym
*CMSSET   COMPARE  ERASE    HB        NUCDROP    RTNLoad  SYSWATCH
*CMSUTIL  CONWAIT  ESERV    Help      NUCXLOAD   RTNMap   TAPE
*EDIT     COPYFILE ESTATE   HELPCONV  NUCXMAP    RTNState TAPEMAC
*FILESERV CP       ESTATEW  HI        OPNNMSSG   RUN      TAPPDS
*OPENVM   CReate   ETRACE   HO        Option     SAD T    TE
*OS HELP  CSLGEN   Exec     HT        OSRUN      SAMGEN   TELL
PF1= Help   2= Top    3= Quit    4= Return    5= Locate   6= ?
PF7= Backward 8= Forward 9= PFkeys 10=          11=        12= Cursor

====> _

Macro-read 2 Files

a
23/007
```

图 2-6 CMS 组件菜单

#### 命令菜单

除了帮助系统中提供的任务菜单外，还提供了几个 VM 组件的单独命令菜单，包括 CP 和 CMS 信息的菜单。例如，如果您从初始帮助菜单中选择 CMS 的命令菜单，将显示一个面板，其中列出了可用的 CMS 命令。

菜单导航与任务菜单类似；要选择一个命令，将光标放在其上并按 Enter 或单击 PF1。

#### 2.5.2 帮助（级别）层级

帮助系统提供了多种获取命令信息的方式，具体取决于您的专业水平以及对特定任务所需详细程度。每条命令都可以显示简要、详细或相关层级的帮助。

要显示三种可用层级中的任何一种，请指定以下层级选项之一：`BRIEF`、`DETAIL`或`RELATED`。您一次只能指定一个层级选项。但是，在您对指定命令请求了一层帮助后，您可以切换（在该命令可用的其他层级之间切换）。

`BRIEF`是默认选项，这意味着如果您未指定选项，则会显示简要层级的帮助（如果可用）。如果某条命令没有简要帮助，则会显示 DETAIL HELP。以下各节提供了有关三种命令帮助层级的更多信息。

#### BRIEF

`BRIEF`是帮助的第一层。它适用于许多命令。简要帮助显示所请求命令的简短描述、命令的基本语法（不带选项的命令）、示例，以及如果适用，告知您是否有更多或相关信息可用的消息。

如果您处于全屏 CMS 中并请求 `BRIEF` HELP，您的窗口会显示您输入的帮助命令，并在其下方，在您的窗口上显示一个窗口，其中显示 `BRIEF` HELP 信息。如果您未处于全屏 CMS 中，则会显示 Brief Help Information 窗口。

以下示例请求`SENDFILE`命令的简要帮助：

```
help cms sendfile (brief)
```

如果您未处于全屏 CMS 中，则该命令的输出将显示在 Brief Help Information 窗口中，如第 40 页的图 2-7 所示。

图 2-7 请求`sendfile`命令简要帮助的输出

#### DETAIL

`DETAIL`层提供命令的完整描述、命令格式、对参数和选项的解释、用法说明以及错误信息。有关 `DETAIL` 帮助的更多信息，请参阅 z/VM: CMS Commands and Utilities Reference, SC24-6073。

该帮助层有七个子集选项：`DESCRIPT`、`FORMAT`、`PARMS`、`OPTIONS`、`NOTES`、`ERRORS`和`ALL`。通过指定子集选项，您可以显示详细帮助的一个或多个特定部分。
