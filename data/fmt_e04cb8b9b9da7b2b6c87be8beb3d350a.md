
# Shell 比较示例

```bash
#!/bin/sh
number1=5
number2=10
number3=5

if [ $number1 -eq $number3 ]; then
    echo "number1 is equal to number3"
else
    echo "number1 is not equal to number3"
fi

if [ $number1 -ne $number2 ]; then
    echo "number1 is not equal to number2"
else
    echo "number1 is equal to number2"
fi

if [ $number1 -gt $number2 ]; then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
fi

if [ $number1 -ge $number3 ]; then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
fi

if [ $number1 -lt $number2 ]; then
    echo "number1 is less than number2"
else
    echo 'number1 is not less than number2'
fi
```

```bash
if [ $number1 -le $number3 ]; then
    echo 'number1 is less than or equal to number3'
else
    echo 'number1 is not less than or equal to number3'
fi
```

执行上述 shell 程序后，将得到以下结果：

`number1` 等于 `number3`

`number1` 不等于 `number2`

`number1` 不大于 `number2`

`number1` 大于或等于 `number3`

`number1` 小于 `number2`

`number1` 小于或等于 `number3`

## 文件运算符

以下运算符可用作文件比较运算符：

- `-d`——用于确定文件是否为目录
- `-f`——用于确定文件是否为常规文件
- `-r`——用于确定文件是否设置了读权限
- `-s`——用于确定文件是否存在且长度大于零
- `-w`——用于确定文件是否设置了写权限
- `-x`——用于确定文件是否设置了执行权限

假设当前目录下有一个名为 `compare3` 的 shell 程序，并且还有一个名为 `file1` 的文件和一个名为 `dir1` 的子目录。假设 `file1` 的权限为 `r-x`（读和执行权限），`dir1` 的权限为 `rwx`（读、写和执行权限）。该 shell 程序的代码如下所示：

```bash
#!/bin/sh
if [ -d $dir1 ]; then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
fi
```

```bash
if [ -f $dir1 ]; then
    echo "dir1 is a regular file"
```

```
else
echo "string1 not equal to string2"
endif

if (string2 != string1) then
echo "string2 not equal to string1"
else
echo "string2 equal to string1"
endif
```

如果执行 `compare1`，将得到以下结果：

```
string1 not equal to string2
string2 not equal to string1
```

## 数字比较

这些运算符可用于比较两个数字：

- `>=` 用于比较一个数字是否大于或等于另一个数字
- `<=` 用于比较一个数字是否小于或等于另一个数字
- `>` 用于比较一个数字是否大于另一个数字
- `<` 用于比较一个数字是否小于另一个数字

下面的示例在名为 `compare2` 的 shell 程序中比较两个数字 `number1` 和 `number2`：

```bash
#!/bin/tcsh
set number1=5
set number2=10
set number3=5

if ($number1 > $number2) then
    echo "number1 is greater than number2"
else
    echo "number1 is not greater than number2"
endif

if ($number1 >= $number3) then
    echo "number1 is greater than or equal to number3"
else
    echo "number1 is not greater than or equal to number3"
endif

if ($number1 < $number2) then
    echo "number1 is less than number2"
```

else

echo "number1 is not less than number2"

endif

if ($number1 <= $number3) then

echo "number1 is less than or equal to number3"

else

echo "number1 is not less than or equal to number3"

endif
```

执行 shell 程序 `compare2` 时，你会得到以下结果：

- `number1 is not greater than number2`
- `number1 is greater than or equal to number3`
- `number1 is less than number2`
- `number1 is less than or equal to number3`

## 文件运算符

这些运算符可以用作文件比较运算符：

- `-d` — 确定一个文件是否为目录
- `-e` — 确定一个文件是否存在
- `-f` — 确定一个文件是否为普通文件
- `-o` — 确定用户是否为文件的拥有者
- `-r` — 确定文件是否设置了读权限
- `-w` — 确定文件是否设置了写权限
- `-x` — 确定文件是否设置了执行权限
- `-z` — 确定文件大小是否为零

以下示例基于一个名为 `compare3` 的 shell 程序，该程序位于当前目录下，与一个名为 `file1` 的文件和一个名为 `dir1` 的子目录同目录。假设 `file1` 的权限为 `r-x`（读和执行权限），`dir1` 的权限为 `rwx`（读、写和执行权限）。

以下是 `compare3` shell 程序的代码：

```bash
#!/bin/tcsh
if (-d dir1) then
    echo "dir1 is a directory"
else
    echo "dir1 is not a directory"
endif
```

此名为 `logic` 的示例使用了前面 `compare3` 示例中提到过的文件和目录。

```bash
#!/bin/tcsh
if ( -x file1 && -x dir1 ) then
    echo file1 and dir1 are executable
else
    echo at least one of file1 or dir1 are not executable
endif

if ( -w file1 || -w dir1 ) then
    echo file1 or dir1 are writable
else
    echo neither file1 or dir1 are executable
endif

if ( ! -w file1 ) then
    echo file1 is not writable
else
    echo file1 is writable
endif
```

如果执行 `logic`，它将产生以下结果：

```
file1 and dir1 are executable
file1 or dir1 are writable
file1 is not writable
```

## for 语句

`for` 语句用于在指定条件为真时每次执行一组命令。`for` 语句有多种格式。`pdksh` 和 `bash` 使用的第一种格式如下：

```bash
for curvar in list
do
    statements
done
```
