

正如我们所见，局部变量是通过在变量名前加上 `local` 这个词来定义的。这会创建一个仅在定义它的 shell 函数内部有效的变量。一旦离开 shell 函数，该变量就不再存在。当我们运行此脚本时，会看到以下结果：

```
[me@linuxbox ~]$ local-vars
global:  foo = 0
funct_1:  foo = 1
global:  foo = 0
funct_2:  foo = 2
global:  foo = 0
```

我们可以看到，在两个 shell 函数内部对局部变量 `foo` 的赋值，对函数外部定义的 `foo` 的值没有任何影响。

此功能允许 shell 函数被编写为彼此独立，并且与它们出现的脚本也独立。这很有价值，因为它有助于防止程序的一个部分干扰另一个部分。它还允许 shell 函数被编写为可移植的。也就是说，它们可以根据需要从一个脚本剪切并粘贴到另一个脚本中。

## 保持脚本运行

在开发程序时，保持程序处于可运行状态很有用。通过这样做并频繁测试，我们可以在开发过程的早期阶段发现错误。这将使调试问题变得容易得多。例如，如果我们运行程序，做一个小的更改，然后再次运行程序并发现问题，那么最近的更改很可能是问题的来源。通过添加空函数，在程序员术语中称为存根，我们可以在早期阶段验证程序的逻辑流程。在构建存根时，最好包含一些为程序员提供反馈的内容，以显示逻辑流程正在被执行。如果我们现在查看脚本的输出：

```
[me@linuxbox ~]$ sys_info_page
<html>
```

```
<head>
    <title>System Information Report For twin2</title>
</head>
<body>
    <h1>System Information Report For linuxbox</h1>
    <p>Generated 03/19/2018 04:02:10 PM EDT, by me</p>
</body>
</html>
```

我们可以看到在时间戳之后输出中有一些空行，但我们不能确定原因。如果我们更改函数以包含一些反馈：

```
report_uptime () {
    echo "Function report_uptime executed."
    return
}

report_disk_space () {
    echo "Function report_disk_space executed."
    return
}

report_home_space () {
    echo "Function report_home_space executed."
    return
}
```

并再次运行脚本：

```
[me@linuxbox ~]$ sys_info_page
<html>
    <head>
        <title>System Information Report For linuxbox</title>
    </head>
    <body>
        <h1>System Information Report For linuxbox</h1>
        <p>Generated 03/20/2018 05:17:26 AM EDT, by me</p>
        Function report_uptime executed.
        Function report_disk_space executed.
        Function report_home_space executed.
    </body>
</html>
```

我们现在可以看到，事实上，我们的三个函数正在被执行。

在我们的函数框架就位并正常工作后，是时候完善一些函数代码了。首先，这里是 `report_uptime` 函数：

```
report_uptime () {
    cat <<- _EOF_
        <h2>System Uptime</h2>
        <pre>$(uptime)</pre>
    _EOF_
    return
}
```

它相当直接。我们使用一个 here 文档来输出一个章节标题和 `uptime` 命令的输出，并用 `<pre>` 标签包围以保留命令的格式。`report_disk_space` 函数类似。

```
report_disk_space () {
    cat <<- _EOF_
        <h2>Disk Space Utilization</h2>
        <pre>$(df -h)</pre>
    _EOF_
    return
}
```

此函数使用 `df -h` 命令来确定磁盘空间的使用量。最后，我们将构建 `report_home_space` 函数。

```
report_home_space () {
    cat <<- _EOF_
        <h2>Home Space Utilization</h2>
        <pre>$(du -sh /home/*)</pre>
    _EOF_
    return
}
```

我们使用带有 `-sh` 选项的 `du` 命令来执行此任务。然而，这并不是解决问题的完整方案。虽然它在某些系统上有效，例如 Ubuntu，但在其他系统上则无效。原因在于许多系统将主目录的权限设置为防止其被世界可读，这是一个合理的<|message|>