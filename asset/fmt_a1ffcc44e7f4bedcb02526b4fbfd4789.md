
# END function "Determine_total_number_of_BYTES_transferred_to_each_host"

################################################################################

```bash
################################################################################
function Print_Report
################################################################################
# 开始报告
print "处理的 Web 日志文件总数: $num_web_logs_processed"
print "分析的 Web 记录总数: $counter_input_recs"
print "符合 CLFF 标准格式的 Web 记录："
print "无效记录: $counter_invalid_recs"
print "成功的 html 请求: $counter_html_recs"
print "成功的 jpeg 请求: $counter_jpeg_recs"
print "成功的 gif 事务: $counter_gif_recs"

print "\n按主机访问次数排序的前10名："
print "主机"
print "访问次数"
total_number_of_hosts=$(sort -u $HOSTS | wc -l)
# -k1 表示唯一（无重复）
print "主机总数（无重复）: $total_number_of_hosts"
head -10 $HOSTS_AND_NUMBER_OF_ACCESSES_sorted

print "\n按文件访问次数排序的前10名："
print "文件"
print "访问次数"
head -10 $FILES_AND_NUMBER_OF_REQUESTS_sorted

print "\n按主机传输字节数排序的前10名："
print "主机"
print "传输字节数"
head -10 $HOSTS_and_BYTECOUNT_TOTALS_sorted

} # 函数 "Print_Report"
```

```bash
if [ $ -eq 0 ];
then num_web_logs_processed=$default_WEBLOG_file_name
List_of_Filenames=
else num_web_logs_processed=$$
List_of_Filenames=-*
fi
```

```bash
print "Patience, please!"
print "\nTHE FOLLOWING FILE(S) WILL BE PROCESSED:\nn$List_of_Filenames"

# Process each web log file that each host accessed on the command line:
Process_all_files_on_command_line
```

```bash
# Determine how many times each host accessed our webserver:
Determine_number_of_times_each_HOST_accessed_our_webserver # Execute function
```

```bash
# Determine how many times each FILE was requested:
Determine_number_of_times_each_FILE_requested # Execute function
```

```bash
# Determine the total number of bytes transferred to each host:
Determine_total_number_of_BYTES_transferred_to_each_host # Execute function
```

```bash
# Execute the function that will display the report on the user's screen:
Print_Report
```

```bash
# Remove/ temporary files:
rm $HOSTS 2>/dev/null
rm $HOSTS_sorted 2>/dev/null
rm $HOSTS_no_duplicates 2>/dev/null
rm $FILES 2>/dev/null
rm $FILES_sorted 2>/dev/null
rm $FILES_no_duplicates 2>/dev/null
rm $HOSTS_AND_BYTECOUNT_sorted 2>/dev/null
rm $HOSTS_AND_BYTECOUNT_TOTALS 2>/dev/null
rm $HOSTS_AND_BYTECOUNT_TOTALS_sorted 2>/dev/null
rm $HOSTS_AND_NUMBER_OF_ACCESSES 2>/dev/null
rm $FILES_AND_NUMBER_OF_ACCESSES_sorted 2>/dev/null
rm $FILES_AND_NUMBER_OF_REQUESTS 2>/dev/null
rm $FILES_AND_NUMBER_OF_REQUESTS_requested 2>/dev/null
```

```bash
print "\nDONE. Script: $0"
exit
# END MAIN_LOGIC.
```

## 释义：元字符的模式，请参阅 "`metacharacters_wildcards.txt`"

# （关于...详情）`web_log_rec=^[A-Za-z0-9]*\.*\*\*\\].*\\].*"[0-9]{3}-[0-9]*$`

`pattern_of_web_log_rec=1234567890123456789012345678901234567890123456789012345678901`

### 示例输入记录：

`[15/05/2007 08:51:23-0500] GET /kim/img.htm HTTP/1.1 200 144`

# 当读入每条 web 日志记录时，以下代码行

# 执行快速检查，以验证该记录是否具有有效格式：

`if [ $(grep "$pattern_of_web_log_rec") -eq 0 ]; then`

该语句的意思是：“如果 web 日志记录具有有效格式，

则处理它，否则拒绝它。”

`grep` 命令（“扩展 grep”）有一个 `-c` 选项，允许我们使用

“计数”（count）来判断是否在记录中找到了该模式。

# 如果计数为 0，则表示没有匹配到模式。

# 如果计数为 1，则表示记录格式正确。

# 我们示例输入中模式开头的前 15 个字符

# `input_record`：'svr7.aol.com'

# 记录中的数据必须开头的字符 (`^`)

# '[a-zA-Z0-9]*' 表示一个或多个字母或数字（大小写均可）

# 或者一个或多个数字后跟一个空格。svr7.aol.com

# web 记录的开头通常像这样：999.42.255.1

# 但看起来像这样（IP 地址）：

# 接下来的字段 UserID 和 AuthID 在大多数 web

# 日志记录中是不可见的，你会在 UserID 和 AuthID 看到 '-'

# 这在我们的日志记录中也是如此。

# 而主机名 (svr7.aol.com)，你只需说 '-'

# 在我们的模式中，第 16-18 位和第 21 位是 '*'。

# 这意味着任何跟随空格的字符

# 都会匹配该模式。

# web 日志记录中的时间戳以 '[' 开始以 ']' 结束；

# 例如：[2011/Apr/07/08:51:23-0500]

# 模式中的第 22-26 位是 '[.*'。

# '\[' 表示我们在此处期望一个左括号。

# ']' 表示我们在此处期望一个右括号。

# （如果没有反斜杠，] 将被解释为元字符）。

# '*' 意味着左右括号之间的任何字符

# 都是接受的；更详细的验证可以...

# web 日志记录中的 "Request" 信息以

# 双引号开头："GET /index.html HTTP/1.1"

# 模式匹配字面双引号

# 例如中，`$code` 是 '200'；

# 模式匹配 code 为 '[0-9]{3}'

请注意

# 有时 `$bytes` 字段仅包含一个连字符。

# 在其他情况下，寻找数字 `[0-9]+` 或 `[0-9]*`

# 模式末尾的 `$` 符号表示“数据的结束”。

# 另一个注释：

# '+' 表示“一个或多个数字”

# 理解 '[0-9]*'

# 与 '[0-9]+' 是不同的
