
```
filename=

while [[ -n $1 ]]; do
    case $1 in
        -f | --file)
            shift
            filename=$1
            ;;
        -i | --interactive)
            interactive=1
            ;;
        -h | --help)
            usage
            exit
            ;;
        *)
            usage >&2
            exit 1
            ;;
    esac
    shift
done
```

首先，我们添加一个名为 usage 的 shell 函数，用于在调用帮助选项或尝试未知选项时显示一条消息。

接下来，我们开始处理循环。只要位置参数 $1 不为空，该循环就会继续。在循环底部，我们有一条 shift 命令，用于推进位置参数，以确保循环最终会终止。

在循环内部，我们有一个 case 语句，用于检查当前的位置参数，看它是否与任何受支持的选项匹配。如果找到受支持的参数，则对其执行相应操作。如果没有找到，则显示 usage 消息，脚本将以错误状态终止。

-f 参数的处理方式很有趣。当检测到它时，会额外执行一次 shift，从而将位置参数 $1 推进到 -f 选项所提供的文件名参数。

接下来，我们添加实现交互模式的代码：

```
# interactive mode

if [[ -n $interactive ]]; then
    while true; do
        read -p "Enter name of output file: " filename
        if [[ -e $filename ]]; then
            read -p "$filename exists. Overwrite? [y/n/q] > "
            case $REPLY in
                Y|y) break
;;
Q|q) echo "Program terminated."
    exit
;;
*) continue
;;
esac
elif [[ -z $filename ]]; then
    continue
else
    break
fi
done
fi
```

如果 interactive 变量不为空，则启动一个无限循环，其中包含文件名提示符以及后续的现有文件处理代码。如果期望的输出文件已存在，则会提示用户选择覆盖、更换文件名或退出程序。如果用户选择覆盖现有文件，则执行 break 以终止循环。注意 case 语句仅检测用户是否选择覆盖或退出。任何其他选择都会使循环继续，并再次提示用户。

为了实现输出文件名的功能，我们必须首先将现有的页面写入代码转换为一个 shell 函数，原因稍后就会明了：

```
write_html_page () {
    cat << _EOF_
<HTML>
    <HEAD>
        <TITLE>$TITLE</TITLE>
    </HEAD>
    <BODY>
        <H1>$TITLE</H1>
        <P>$TIMESTAMP</P>
        $(report_uptime)
        $(report_disk_space)
        $(report_home_space)
    </BODY>
</HTML>
_EOF_
    return
}

# output html page

if [[ -n $filename ]]; then
```

```
if touch $filename && [[ -f $filename ]]; then
    write_html_page > $filename
else
    echo "$PROGNAME: Cannot write file '$filename'" >&2
    exit 1
fi
else
    write_html_page
fi
```

处理 `-f` 选项逻辑的代码出现在上面列表的末尾。在这段代码中，我们测试文件名是否存在；如果存在，则进一步测试该文件是否确实可写。为此，先执行 touch，然后测试生成的文件是否为常规文件。这两个测试分别处理了输入无效路径名（touch 会失败）的情况，以及文件已存在且是常规文件的情况。

正如我们所见，调用 `write_html_page` 函数来实际生成页面。其输出要么定向到标准输出（如果变量 `filename` 为空），要么重定向到指定文件。

## 总结

通过增加位置参数，我们现在可以编写功能相当完备的脚本。对于简单、重复的任务，位置参数使得编写非常有用的 shell 函数成为可能，这些函数可以放置在用户的 `.bashrc` 文件中。

我们的 `sys_info_page` 程序在复杂性和精巧性上都有所提升。以下是完整清单，最新的更改已突出显示：

```
#!/bin/bash

# sys_info_page: program to output a system information page

PROGNAME=$(basename $0)
TITLE="System Information Report For $HOSTNAME"
CURRENT_TIME=$(date +"%x %r %Z")
TIMESTAMP="Generated $CURRENT_TIME, by $USER"

report_uptime () {
    cat <<- _EOF_
        <H2>System Uptime</H2>
        <PRE>$(uptime)</PRE>
    _EOF_
    return
}
```

