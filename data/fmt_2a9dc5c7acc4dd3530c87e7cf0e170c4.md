
`print "Number of words in this line: $num_words"`

`print "Number of characters in this line: $num_chars"`

```
done < "$INPUT"
```

```
561
```

### Get_HOST_TIMESTAMP_REQUEST_CODE_BYTES_from_Current_Record

Process_HOST_section_of_web_log_record

Process_TIMESTAMP_section_of_web_log_record

```
```

Process_REQUEST_section_of_web_log_record

Process_CODE_section_of_web_log_record

Process_TIMESTAMP_section_of_web_log_record

```
```

```
fi

done < $filename

else print ERROR: $filename is not a regular file OR is empty not "readable".

done # END "for filename in $list_of_filenames"

} # END function "process_all_files_on_command_line"
```

```
######################################################################
```

```
function get_HOST_TIMESTAMP_REQUEST_CODE_BYTES_from_Current_Record

######################################################################
```

```
{ START start

输入记录（web 日志记录）如下所示：

```

# SV_line -- [15/Apr/2007:08:51:23 -0500] GET /-kim/img.html HTTP/1.1" 200 1444

```

# 初始化：

Timestamp_and_rest_of_rec='

Timestamp_long='

Timestamp='

Request='

File='

Code_Bytes='

temp='

###

```

# 接下来，使用 'cut' 来“切分和处理”（解析）输入记录：

# 另另：cut AND.substring $key

```

timestamp_and_rest_of_rec=$(print "record" | cut -d ']' -f 2 2>/dev/null)

```

# 在 cut 之后，$timestamp_and_rest_of_rec 包含以下数据：
# '15/Apr/2007:08:51:23 -0500] GET /-kim/img.html HTTP/1.1" 200 1444

```

Timestamp_long=$(print "$timestamp_and_rest_of_rec" | cut -d ' ' -f 1 2>/dev/null)

Timestamp=$(print "$timestamp_long" | cut -d ' ' -f 1 2>/dev/null)

# 在 cut 之后，$timestamp 包含 '15/Apr/2007:08:51:23 -0500'

```

```

Request=$(print "record" | cut -d ' ' -f 2 2>/dev/null)

File=$(print "Request" | cut -d ' ' -f 3 2>/dev/null)

```

```

Code_Bytes=$(echo "record" | cut -d ' ' -f 3 2>/dev/null)

# 在 cut 之后，$code_and_Bytes 通常看起来像这样：200 1444

$code_and_Bytes 有时候看起来像这样：404 -

```

```

# 移除 $code_and_Bytes 前导的空格：

temp=$(echo "$code_and_Bytes" | sed 's/^[[:space:]]*//' 2>/dev/null)

Code_and_Bytes=$temp

```

```

Code=$(print "$code_and_Bytes" | cut -d ' ' -f 1 2>/dev/null)

Bytes=$(print "$code_and_Bytes" | cut -d ' ' -f 2 2>/dev/null)

```

```

# 为了调试，请取消以下 print 语句：

# print "\nbytes: $bytes"

```

```

# print Code: $code

# print "File: $file"

# print "Request: $request"

# print "Timestamp: $timestamp\n"

```

```

length=$(${timestamp})

if [ $length -eq 0 ]; then print "ERROR: Timestamp is empty";exit;

if [ $length -eq 0 ]; then print "ERROR: Request is empty";exit;

#-${file}

if [ $length -eq 0 ]; then print "ERROR: File is empty";exit;

if [ $length -eq 0 ]; then print "ERROR: Code is empty";exit;

length=${bytes}

if [ $length -eq 0 ]; then print "ERROR: Bytes is empty";exit;

```

```
######################################################################
# get_HOST_TIMESTAMP_REQUEST_CODE_BYTES_from_Current_Record 函数结束
######################################################################
```

```
######################################################################
function Process_HOST_section_of_web_log_record
######################################################################
{ START_function

Host=$(print "$record" | cut -d ' ' -f 1)

print "$HOST" >>HOST

# 对 'cut' 有疑问？参考 CUT_substring.ksh

} 函数结束
######################################################################
```

```
dd=$(print "$timestamp" | cut -d ' ' -f 1)

# 示例：15

mm=$(print "$timestamp" | cut -d ' ' -f 2)

# 示例：06

yyyy_and_rest_of_record=$(print "$timestamp" | cut -d ' ' -f 3)

# 示例：2007:06:23 -0500

ss_and_rest_of_record=$(print "$yyyy_and_rest_of_record" | cut -d ' ' -f 1)

# 示例：09

ss=$(print "$ss_and_rest_of_record" | cut -d ' ' -f 1)
```

```

# 对 'cut' 有疑问？参考 CUT_substring.ksh

} 函数结束 "Process_TIMESTAMP_section_of_web_log_record"
######################################################################
```

```
######################################################################
# function Process_REQUEST_section_of_web_log_record
