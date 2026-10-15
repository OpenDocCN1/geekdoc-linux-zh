

## sort—排序和/或合并文件

```
sort [ -cmu ] [ -o output ] [ -T directory ] [ -y kmen ] [ -dfiMnr ] [ -b tx ] [ +pos1 [ -pos2 ] ] [ filename... ]
```

sort 命令将所有命名文件中的（ASCII）行一起排序并将结果写入标准输出。比较基于从每一行输入中提取的一个或多个排序键。默认情况下，有一个排序键，即整个输入行，排序顺序按机器整理序列中的字节进行词法排序。

### EXAMPLE A.31

- 1. sort filename
- 2. sort -u filename
- 3. sort -r filename
- 4. sort +1 -2 filename
- 5. sort -2n filename
- 6. sort -t: +2n -3 filename
- 7. sort -f filename
- 8. sort -b +1 filename

### EXPLANATION

- 1. 按字母顺序排序行
- 2. 排序并删除重复项。
- 3. 反向排序。
- 4. 从第 1 个字段开始排序（字段由空白分隔并从字段 0 开始），在第 2 个字段处停止，而不是排序到行尾。
- 5. 按第三个字段数值排序。
- 6. 从第 2 个字段开始数值排序并在第 3 个字段处停止，以冒号指定为字段分隔符（-t:）。
- 7. 排序时不区分大小写字母。
- 8. 从第 1 个字段开始排序，删除前导空白。

## spell—查找拼写错误

```
spell [ -blvx ] [ -d hlist ] [ -s hstop ] [ +local_file ] [ filename ]...
```

spell 从命名文件名中收集单词并在拼写列表中查找它们。既不在拼写列表中出现也不能通过应用某些词形变化、前缀和/或后缀从拼写列表中的单词派生出来的单词将被打印到标准输出。如果未命名文件名，则单词从标准输入中收集。

## split—将文件拆分为片段

```
split [ -n ] [ filename [ name ] ]
```

split 读取 filename 并将其以 n 行片段写入一组输出文件。第一个输出文件以 aa 追加命名，依此类推，按字典顺序排列，直到 zz（最多 676 个文件）。name 的最大长度比文件系统允许的最大文件名长度少 2 个字符。参见 statvfs。如果未给出输出名称，则使用 x 作为默认值。（输出文件将称为 xaa、xab 等。）

### EXAMPLE A.32

- 1 split -500 filea
- 2 split -1000 fileb out

### EXPLANATION

- 1 将 filea 拆分为 500 行的文件。文件命名为 xaa、xab、xac，依此类推。
- 2 将 fileb 拆分为 1,000 行的文件，命名为 out.aa、out.ab，依此类推。

## strings—在对象或二进制文件中查找任何可打印字符串

```
strings [ -a ] [ -o ] [ -number ] [ filename... ]
```

strings 命令在二进制文件中查找 ASCII 字符串。字符串是四个或更多打印字符的任何序列，以换行符或空字符结尾。strings 对于识别随机对象文件和其他许多事物很有用。

### EXAMPLE A.33

```
strings /bin/nawk | head -2
```

### EXPLANATION

打印二进制可执行文件 /bin/nawk 的前两行中的任何 ASCII 文本。

## stty—设置终端的选项

```
stty [ -a ] [ -g ] [ modes ]
```

stty 为当前标准输入的设备设置某些终端 I/O 选项；不带参数时，它报告某些选项的设置。

### EXAMPLE A.34

- 1 stty erase <Press backspace key> or ^h
- 2 stty -echo; read secretword; stty echo
- 3 stty -a (AT&T) or stty -everything (BSD)

### EXPLANATION

- 1 将 Backspace 键设置为删除。
- 2 关闭回显；等待用户输入；重新打开回显。
- 3 列出 stty 的所有可能选项。

## su—成为超级用户或其他用户

```
su [ - ] [ username [ arg ... ] ]
```

su 允许在不注销的情况下成为另一个用户。默认用户名为 root（超级用户）。要使用 su，必须提供适当的密码（除非调用者已是 root）。如果密码正确，su 会创建一个新的 shell 进程，其真实和有效用户 ID、组 ID 和补充组列表设置为指定用户名的那些。新 shell 将是用户名密码文件条目 shell 字段中指定的 shell。如果未指定 shell，则使用 sh（Bourne shell）。要返回到普通用户 ID 权限，请键入 Ctrl-D 退出新 shell。- 选项指定完整登录。

## sum—为文件计算校验和

## sync—更新超级块并将更改的块发送到磁盘

## tabs—在终端上设置制表位

## tail—显示文件的尾部

```
tail +[-number [ lbc ] [ f ] ] [ filename ]
tail +[-number [ l ] [ rf ] ] [ filename ]
```

当数字前有加号时，tail 从文件开头计数显示块、字符或行。如果数字前有连字符，tail 从文件末尾计数。

### EXAMPLE A.35

- 1. tail +50 filex
- 2. tail -20 filex
- 3. tail filex

### EXPLANATION

- 1. 显示 filex 从第 50 行开始的内容。
- 2. 显示 filex 的最后 20 行。
- 3. 显示 filex 的最后 10 行。

## talk—允许你与其他用户交谈

```
talk username [ ttyname ]
```

talk 是一个视觉通信程序，将行从你的终端复制到另一用户的终端。

