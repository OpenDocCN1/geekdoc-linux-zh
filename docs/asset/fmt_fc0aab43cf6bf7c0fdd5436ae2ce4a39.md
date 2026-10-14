
`echo -e "\n \$@ :";  print_params $@`

`echo -e "\n \"$@\" :"; print_params "$@"`

}

`pass_params "word" "words with spaces"`

```
在这个相当复杂的程序中，我们创建了两个参数：`word` 和 `words with spaces`，并将它们传递给 `pass_params` 函数。该函数随后使用特殊参数 `$*` 和 `$@` 可用的四种方法，将它们传递给 `print_params` 函数。执行时，脚本揭示了这些差异：
```

```
[me@linuxbox ~]$ posit-params3

$* :

$1 = word

$2 = words

$3 = with

$4 = spaces

"$*" :

$1 = word words with spaces

$2 =

$3 =

$4 =

$@ :

$1 = word

$2 = words

$3 = with

$4 = spaces

"$@" :

$1 = word

$2 = words with spaces

$3 =

$4 =
```

使用我们的参数，`$*` 和 `$@` 都产生四个词的结果：`word`、`words`、`with` 和 `spaces`。`"$*"` 产生一个词的结果：`word words with spaces`。`"$@"` 产生两个词的结果：`word` 和 `words with spaces`。

这符合我们的实际意图。从中可以学到的教训是，尽管 shell 提供了四种不同的方式来获取位置参数列表，但在大多数情况下，`"$@"` 显然是最有用的，因为它保留了每个位置参数的完整性。

## 一个更完整的应用

在长时间的中断之后，我们将继续 `sys_info_page` 程序的工作。下一步将为程序添加几个命令行选项，如下所示：

- **输出文件。** 我们将添加一个选项，用于指定一个文件名来保存程序的输出。该选项可通过 `-f file` 或 `--file file` 指定。
- **交互模式。** 此选项会提示用户输入输出文件名，并判断指定文件是否已存在。如果已存在，在覆盖现有文件之前将提示用户。该选项可通过 `-i` 或 `--interactive` 指定。
- **帮助。** 可以指定 `-h` 或 `--help`，使程序输出一条信息丰富的用法消息。

以下是实现命令行处理所需的代码：

```
usage () {
    echo "$PROGNAME: usage: $PROGNAME [-f file | -i]"
    return
}
```

```
# process command line options
interactive=
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

首先，我们添加一个名为 `usage` 的 shell 函数，用于在调用帮助选项或尝试未知选项时显示消息。

接下来，我们开始处理循环。只要位置参数 `$1` 不为空，此循环就会继续。在循环底部，我们有一条 `shift` 命令来推进位置参数，以确保循环最终能够终止。

在循环内部，我们有一个 `case` 语句，检查当前的位置参数，看它是否与任何受支持的选项匹配。如果找到受支持的参数，则执行相应操作；如果没有，则显示 `usage` 消息，脚本将以错误终止。

`-f` 参数的处理方式很有趣。当检测到它时，会额外执行一次 `shift`，将位置参数 `$1` 推进到通过 `-f` 选项提供的文件名参数。

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

如果 `interactive` 变量不为空，则会启动一个无限循环，其中包含文件名提示和后续的现有文件处理代码。如果期望的输出文件已存在，则会提示用户覆盖、选择另一个文件名或退出程序。如果用户选择覆盖现有文件，则会执行 `break` 以终止循环。请注意，`case` 语句仅检测用户是否选择覆盖或退出。任何其他选择都会导致循环继续并再次提示用户。

为了实现输出文件名功能，我们必须首先将现有的页面写入代码转换为 shell 函数，原因稍后会变得清楚：

```
write_html_page () {
    cat << _EOF_
    <HTML>
        <HEAD>        <TITLE>$TITLE</TITLE>
        </HEAD>
        <BODY>
            <H1>$TITLE</H1>
            <P>$TIME_STAMP</P>
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
    if touch $filename && [[ -f $filename ]]; then
        write_html_page > $filename
    else
        echo "$PROGNAME: Cannot write file "$filename"" >&2
        exit 1
    fi
else
    write_html_page
fi
```

上述列表末尾的代码处理了 `-f` 选项的逻辑。在其中，我们测试 `filename` 的存在性，如果找到文件名，则会进行测试以查看文件是否确实可写。为此，会执行 `touch`，然后测试以确定生成的是否为常规文件。这两个测试可以处理输入无效路径名的情况（`touch` 将失败），并且如果文件已存在，则确保它是一个常规文件。

正如我们所见，`write_html_page` 函数被调用以执行页面的实际生成。其输出要么被定向到标准输出（如果变量 `filename` 为空），要么被重定向到指定的文件。

## 最终说明

通过添加位置参数，我们现在可以编写功能相当完善的脚本。对于简单、重复的任务，位置参数使得可以编写非常有用的 shell 函数，这些函数可以放置在用户的 `.bashrc` 文件中。

我们的 `sys_info_page` 程序在复杂性和精妙程度上有所增长。以下是完整列表，其中最新更改已突出显示：

```
#!/bin/bash
# sys_info_page: program to output a system information page
PROGNAME=$(basename $0)
TITLE="System Information Report for $HOSTNAME"
CURRENT_TIME=$(date '+%x %r %Z')
TIME_STAMP="Generated $CURRENT_TIME, by $USER"
report_uptime () {
  cat <<_EOF_
