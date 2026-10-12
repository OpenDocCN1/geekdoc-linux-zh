
`C:\WINDOWS\System32\eventcreate.exe` -edit `backup.bat`

File Edit View Options Help

`C:\Documents\New folder\backup.bat`

`copy R:\> C:\backup.bat *`

```
帮助线：行12:列32
```

# EventCreate 命令

`EventCreate` 命令允许你创建一个并添加到 Windows 事件日志中的事件。如果你想记录某些发生的异常情况，这将非常有用。它通常用于批处理文件，以标记任务（如每夜备份）的开始或完成。

以下是基本语法：

```
eventcreate [options]
eventcreate /T type /D "description" /ID eventide
[/L logname] [/SO sourcename] [/S system]
[/U username [/P password]]
```

## EventCreate 命令 605

以下是选项说明：

- `/T`: 指定类型。选项有 Information（信息）、Warning（警告）或 Error（错误）。
- `/D`: 提供保存在日志中的描述性消息。如果消息包含多个单词，请使用引号。
- `/ID`: 1 到 1000 之间的数字。
- `/L`: 写入事件的日志名称。默认是 Application（应用程序）。
- `/SO`: 代表事件源的字符串。默认是 EventCreate。如果你指定此项，必须也指定 `/L` 选项。
- `/S`: 应该记录事件的系统名称。
- `/U`: 记录事件时使用的用户账户。只有在指定 `/S` 的情况下才能指定此选项。
- `/P`: 密码。只有在也指定 `/U` 的情况下才能指定此选项。

以下是一个向 Application 日志写入信息性消息的示例：

```
eventcreate /t informational /id 100 "Nightly processing completed" /L Application /SO Nightly
```

图 9-3 显示了该命令创建的事件。

![](img/2cf73c243032d4689a17a526d04b44a0_637_0.png)

图 9-3：
由 EventCreate 命令创建的事件。

# Net 命令 606

对于网络管理员来说，更有用的命令是 Net 服务命令。这些命令都是以 Net 开头的双单词命令，例如 `Net Use` 和 `Net Start`。在接下来的章节中，我将按字母顺序介绍每个 Net 命令，以便方便参考。首先，我想指出关于 Net 命令的几个细节：

- 你可以在命令提示符中输入 `net ?` 来快速获取可用 Net 命令的列表。
- 你可以通过输入 `net help [command]` 来获取任何命令的简要帮助。例如，要显示 Net Use 命令，请输入 `net help use`。（是的，我们可以使用一些帮助。）
- 许多 Net 命令会提示你完成某操作。对于这些命令，你可以指定 `/Y` 或 `/N` 来跳过确认提示。如果你在无人值运行的批处理文件中使用这些命令，你最好这样做。请注意，即使某个 Net 命令没有提示你确认，你也可以任何 Net 命令上使用 `/Y` 或 `/N`。我建议在打算无人值运行的批处理文件中，对每个 Net 命令都加上 `/Y`。

## Net Accounts 命令

此命令更新用户账户关于密码要求的策略。以下是命令语法：

```
net accounts [/forcelogoff:minutes | no]
 [/maxpage:{days | unlimited}]
 [/minpwlen:length]
 [/minpage:days]
[/uniquew:password]
[/domain]
```

以下段落描述了 Net Accounts 命令的参数：

- `Forcelogoff`: 指定在用户登录时间过期后强制用户注销系统之前等待多久。默认值 `no` 可防止用户被强制注销。如果你指定一个数字，用户将在被强制注销前几分钟收到警告。
- `Minpwlen`: 指定用户密码的最小长度。数字可以是从 0 到 127 之间的任何值。默认是 6。
- `Maxpwlen`: 指定用户密码被认为有效的天数。`Unlimited` 意味着密码永不过期。天数可以从 1 到 [缺失]。

# Net 命令 607

（注：此处内容为原文重复，保持翻译一致）

- `Forcelogoff`: 指定在用户登录时间过期后强制用户注销系统之前等待多久。默认值 `no` 可防止用户被强制注销。如果你指定一个数字，用户将在被强制注销前几分钟收到警告。
- `Minpwlen`: 指定用户密码的最小长度。数字可以是从 0 到 127 之间的任何值。默认是 6。
- `Maxpwlen`: 指定用户密码被认为有效的天数。`Unlimited` 意味着密码永不过期。天数可以从 1 到 [缺失]。

## Net Accounts 命令

（注：此处内容为原文重复）

此命令更新用户账户关于密码要求的策略。以下是命令语法：

```
net accounts [/forcelogoff:minutes | no]
 [/maxpage:{days | unlimited}]
 [/minpwlen:length]
 [/minpage:days]
[/uniquew:password]
[/domain]
```

以下段落描述了 Net Accounts 命令的参数：

- `Forcelogoff`: 指定在用户登录时间过期后强制用户注销系统之前等待多久。默认值 `no` 可防止用户被强制注销。如果你指定一个数字，用户将在被强制注销前几分钟收到警告。
- `Minpwlen`: 指定用户密码的最小长度。数字可以是从 0 到 127 之间的任何值。默认是 6。
- `Maxpwlen`: 指定用户密码被认为有效的天数。`Unlimited` 意味着密码永不过期。天数可以从 1 到 [缺失]。

## Net Accounts 命令

（注：此处内容为原文重复）

此命令更新用户账户关于密码要求的策略。以下是命令语法：

```
net accounts [/forcelogoff:minutes | no]
 [/maxpage:{days | unlimited}]
 [/minpwlen:length]
 [/minpage:days]
[/uniquew:password]
[/domain]
```

以下段落描述了 Net Accounts 命令的参数：

- `Forcelogoff`: 指定在用户登录时间过期后强制用户注销系统之前等待多久。默认值 `no` 可防止用户被强制注销。如果你指定一个数字，用户将在被强制注销前几分钟收到警告。
- `Minpwlen`: 指定用户密码的最小长度。数字可以是从 0 到 127 之间的任何值。默认是 6。
- `Maxpwlen`: 指定用户密码被认为有效的天数。`Unlimited` 意味着密码永不过期。天数可以从 1 到 [缺失]。

# Net 命令

（注：此处包含大量 OCR 错误和重复，已根据指令要求翻译核心逻辑）

（注：原文 OCR 文本包含大量重复和碎片，我已根据你的要求提取并翻译了唯一的逻辑内容。）

## Computer 命令

此命令创建或删除计算机账户。以下是语法：

```
net computername {add | del}
```

以下段落描述了 Net Computer 命令的参数：

- `Computerename`: 添加或删除的计算机名称。
- `Add`: 创建计算机账户。
- `Del`: 删除指定的计算机。

以下是一个添加名为 the 的计算机的示例：

```
net computer add
```

## Net Config 命令

此命令允许你查看或配置各种服务。以下是语法：

```
net config {server|workstation}
```

要配置服务器设置，使用此语法：

```
net config server [/autodisconnect:time] [/srvconnect:"text"] [/hidden:{yes} no]
```
