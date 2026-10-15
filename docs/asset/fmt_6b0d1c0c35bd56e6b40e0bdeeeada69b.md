
```
3     echo "$file": readable/writable/plain file

    endif

end
```

（输出）

```
3 complete: readable/writable/plain file

dirstack: readable/writable/plain file

file.sc: readable/writable/plain file

filetest: readable/writable/plain file

glob: readable/writable/plain file

modifiers: readable/writable/plain file

env: readable/writable/plain file
```

# 解释

- 1 `foreach` 循环遍历 UNIX/Linux `ls` 程序产生的 文件列表，一次一个文件，将每个文件名赋给变量 `file`。
- 2 如果文件可读、可写且为普通文件（`-rwf`），则执行第 3 行代码。在 `tcsh` 中堆叠这些文件测试选项是合法的，但在 `csh` 中不合法。
- 3 如果正在测试的文件名可读、可写且可执行，则执行此行。

## 10.6.19 filetest 内建命令（tcsh）

`tcsh` 内建的 `filetest` 命令将一个文件查询操作符应用于一个文件或文件列表，并返回一个以空格分隔的数字列表；1 表示真，0 表示假。

### 示例 10.30

```
1 > filetest -rwf dirstack file.sc xxx

1 1 0

2 > filetest -b hdd

1

3 > filetest -lrx /dev/fd

1
```

# 解释

- 1 对每个文件 `dirstack`、`file.sc` 和 `xxx` 进行测试，看它们是否可读、可写、普通文件。对前两个文件测试返回真（1 1），对最后一个文件测试返回假（0）。
- 2 `filetest` 命令如果文件 `hdd` 是块特殊设备文件则返回 1。是的。否则返回 0。
- 3 `filetest` 命令如果文件 `fd` 是符号链接且可读且可执行则返回 1。是的。否则返回 0。

## 10.6.20 附加的 TC Shell 文件测试操作符

还有一组附加的文件测试操作符（仅限 `tcsh`），如表 10.10 所示，用于返回有关文件的信息。由于返回的值不是真/假值，-1 表示失败（除 F 外，F 返回一个 ）。

### 表 10.10 附加的 tcsh 文件测试

| 操作符 | 其作用 |
|---|---|
| -A | 最后一次文件访问时间，以自纪元（1970 年 1 月 1 日）以来的秒数表示 |
| -A: | 与 A 相同，但以时间戳格式，例如 Fri. Aug. 27 16:36:10 2004 |
| -M | 最后一次文件修改时间 |
| -M: | 与 M 相同，但以时间戳格式 |
| -C | 最后一次 inode 修改时间 |
| -C: | 与 C 相同，但以时间戳格式 |
| -F | 复合文件标识符，格式为 device:inode |
| -G | 数字组 ID |

### 表 10.10 附加的 tcsh 文件测试（续）

| 操作符 | 其作用 |
|---|---|
| -G: | 组名或如果组名未知则为数字组 ID |
| -L | 符号链接指向的文件名 |
| -N | （硬）链接数 |
| -P | 权限，以八进制表示，无前导零 |
| -P: | 与 P 相同，但带前导零 |
| -Pmode | 等价于 -P file & mode；例如 -P22 file 如果文件可被组和其他用户写入则返回 22，如果仅可被组写入则返回 20，如果两者都不可则返回 0 |
| -Mode: | 与 Mode: 相同，带前导零 |
| -U | 数字用户 ID |
| -U: | 用户名，或如果用户名未知则为数字用户 ID |
| -Z | 大小，以字节为单位 |

### 示例 10.31

```
1 > date

Wed Apr 22 13:36:11 PST 2004

2 > filetest -A myfile

934407771

3 > filetest -A: myfile

Wed Apr 22 14:42:53 2004

4 > filetest -U myfile

501

5 > filetest -P: myfile

0600

> filetest -P myfile

600
```

# 解释

- 1. 打印今天的日期。
- 2. 使用 `-A` 选项，`filetest` 内建命令打印 `myfile` 最后一次被访问的日期（以纪元形式表示）。
- 3. 使用 `-A:` 选项，`filetest` 内建命令以时间戳格式打印日期。
- 4. 使用 `-U` 选项，`filetest` 内建命令打印 `myfile` 所有者的数字用户 ID。
- 5. 使用 `-P:` 选项，`filetest` 内建命令打印带前导 0 的八进制权限模式。不带冒号时，前导 0 会被移除。

# 示例 10.32

(脚本)

```
#!/bin/tcsh -f

# Scriptname: filecheck

# Usage: filecheck filename

1 alias Usage 'echo " Usage: $0 filename\n"; exit 1'

2 alias Error 'echo " Error: \n"; exit 2'

3 set file=$1

4 if ($#argv == 0 ) then

file

Usage

endif

5 if ( ! -e $file ) then

Error "$file does not exist"

endif

6 if ( -d $file ) then

echo "$file is a directory"

7 else if ( -f $file ) then

8 if ( -rx $file ) then  # nested if construct

echo "You have read and execute permission on $file"

9 endif

else

print "$file is neither a plain file nor a directory."

10 endif
```

(命令行)
```
% filecheck testing1
You have read and execute permission on file testing1.
```

# 说明

+   1 这个别名 `Usage` 可用于产生错误消息并退出程序。
+   2 这是一个名为 `Error` 的别名，它会在被调用时产生一条错误消息，并附带所传入的任何参数。
+   3 变量 `file` 被设置为从命令行传入的第一个参数 `$1`（即 `testing1`）。
+   4 如果传入的参数个数为 0，即没有提供参数，则别名 `Usage` 会在屏幕上打印其消息。
+   5 如果 `file`（在变量替换后）是一个不存在的文件（注意 NOT 操作符 `!`），那么 `then` 关键字下的别名 `Error` 会显示其消息。
+   6 如果文件是目录，则打印 "`testing1 is a directory.`"。
+   7 如果文件不是目录，`else if` 该文件是一个普通文件，那么……执行下一条语句，即另一个 `if`。
+   8 这个 `if` 嵌套在前一个 `if` 中。如果 `file` 可读且可执行，那么……这个 `if` 有它自己的 `endif`，并且通过缩进对齐来表明它所属的位置。
+   9 `endif` 终止最内层的 `if` 结构。
+   10 `endif` 终止最外层的 `if` 结构。

# 说明（续）

## 10.6.21 switch 命令

`switch` 命令是使用 `if-then-else if` 结构的替代方案。在处理多个选项时，`switch` 命令有时能让程序更清晰易读。`switch` 表达式中的值会与 `case` 关键字之后的表达式（称为标签）进行匹配。`case` 标签可以接受常量表达式和通配符。标签以冒号结尾。`default` 标签是可选的，但如果没有其他 `case` 与 `switch` 表达式匹配，则执行 `default` 标签对应的操作。`breaksw` 用于将执行转移到 `endsw`。如果省略 `breaksw` 且某个标签被匹配，则会执行该匹配标签下方的所有语句，直到遇到 `breaksw` 或 `endsw` 为止。

### 格式

```
switch (variable)

case constant:

    commands

    breaksw

case constant:

    commands

    breaksw

endsw
```

### 示例 10.33

(脚本)

```
#!/bin/csh -f

# Scriptname: colors

1  echo -n "Which color do you like? "

2  set color = $c

3  switch ("$color")

4  case bl*:
       echo I feel $color
```
