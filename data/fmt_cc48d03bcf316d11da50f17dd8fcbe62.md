
其他生成包含成功和错误信息的单个中心日志文件的服务器，会用 `[error]` 字段值来标记错误消息条目。在这种情况下，可以使用 `grep '[error]'` 来创建错误日志，使用 `grep -v '[error]'` 来创建访问日志。

无论你的服务器是否自动创建错误日志，还是你必须通过搜索包含 `'[error]'` 字符串的条目来创建自己的错误日志，错误日志中的几乎所有内容都与访问日志的内容不同，包括日期的指定方式。

```
$ head -1 error_log
[Mon Jun 06 08:08:35 2016] [error] [client 54.204.131.75] File does not exist: /var/www/vhosts/default/htdocs/clientaccesspolicy.xml
```

在访问日志中，日期被指定为一个紧凑的单字段值且没有空格；错误日志则使用五个字段。此外，与访问日志中单词/字符串位置在空格分隔条目中一致地标识特定字段的方案不同，错误日志中的条目具有长度不一的有意义的错误描述。对仅这些描述值的检查显示出令人惊讶的变化，如下所示：

```
$ awk '{print $9" "$10" "$11" "$12}' error_log | sort -u
File does not exist:
Invalid error redirection directive:
Premature end of script
execution failure for parameter
premature EOF in parsed
script not found or
malformed header from script
```

其中一些错误应手工检查，因为它们很难追溯到导致问题的网页。

`Listing 10-5` 中的脚本专注于最常见的问题——特别是 `File does not exist` 错误——然后生成所有其他与已知错误情况不匹配的错误日志条目的转储。

## The Code

```
#!/bin/bash
# weberrors - Scans through an Apache error_log file, reports the
# most important errors, and then lists additional entries

temp="/tmp/$(basename $0).$$"

# For this script to work best, customize the following three lines for
# your own installation.

htdocs="/usr/local/etc/httpd/htdocs/"
myhome="/usr/home/taylor/"
cgibin="/usr/local/etc/httpd/cgi-bin/"

sedstr="s!$htdocs![htdocs]!g;s!$myhome![homedir]!g"
sedstr="$sedstr;s!$cgibin![cgi-bin]!g"

screen="File not exist|Invalid error redirect|premature EOF"
screen="$screen|Premature end of script|script not found"

length=5          # Entries per category to display

checkfor()
{
  grep "$2" "$1" | awk '{print $NF}' \
  | sort | uniq -c | sort -rn | head -$length | sed "$sedstr" > $temp

  if [ $(wc -l < $temp) -gt 0 ] ; then
    echo ""
    echo "$2 errors:"
    cat $temp
  fi
}

trap "$(which rm) -f $temp" 0

if [ "$1" = "-l" ] ; then
  length=$2; shift 2
fi

if [ $# -ne 1 -o ! -r "$1" ] ; then
  echo "Usage: $(basename $0) [-l len] error_log" >&2
  exit 1
fi

echo Input file $1 has $(wc -l < "$1") entries.

start="$(grep -E '^[\[.:*]+' "$1" | head -1 \
  | awk '{print $1" "$2" "$3" "$4" "$5}')"
end="$(grep -E '^[\[.:*]+' "$1" | tail -1 \
  | awk '{print $1" "$2" "$3" "$4" "$5}')"

/bin/echo -n "Entries from $start to $end"

echo ""

### Check for various common and well-known errors:

checkfor "$1" "File does not exist"
checkfor "$1" "Invalid error redirection directive"
checkfor "$1" "Premature EOF"
checkfor "$1" "Script not found or unable to stat"
checkfor "$1" "Premature end of script headers"

① grep -vE "$screen" "$1" | grep "\[error\]" | grep "\[client " \
| sed 's/\[error\]/||/' | cut -d'|' -f2 | cut -d' ' -f4- \
② | sort | uniq -c | sort -rn | sed 's/^/  /' | head -$length > $temp

if [ $(wc -l < $temp) -gt 0 ] ; then
 echo ""
 echo "Additional error messages in log file:"
 cat $temp
fi

echo ""
echo "And non-error messages occurring in the log file:"

③ grep -vE "$screen" "$1" | grep -v "\[error\]" \
| sort | uniq -c | sort -rn \
| sed 's/^/  /' | head -$length

exit 0
```

`Listing 10-5`: The `weberrors` script

## How It Works

该脚本通过扫描错误日志中 `checkfor` 函数调用指定的五个错误，并使用 `awk` 调用提取每个错误行上的最后一个字段 `$NF`（它代表该特定输入行中的字段数）来工作。此输出随后通过 `sort | uniq -c | sort -rn` ② 传递，以便于提取该问题类别中最常出现的错误。

为了确保仅显示具有匹配项的错误类型，每个特定错误搜索都会保存到临时文件中，然后测试该文件是否不为空，然后再输出消息。所有这些都通过脚本顶部附近出现的 `checkfor()` 函数整洁地完成。

脚本的最后几行标识了脚本未另行检查但仍采用标准 Apache 错误日志格式的最常见错误。① 处的 `grep` 调用是较长管道的一部分。

然后脚本标识了脚本未另行检查但不出现在标准 Apache 错误日志格式中的最常见错误。同样，③ 处的 `grep` 调用也是较长管道的一部分。

### 运行脚本

该脚本应将其唯一的命令行参数传递给标准 Apache 格式的错误日志的路径，如清单 10-6 所示。如果使用 `-l length` 参数调用，它将显示每种错误类型匹配的长度条目数，而不是默认的每种错误类型五条条目。

### 结果
