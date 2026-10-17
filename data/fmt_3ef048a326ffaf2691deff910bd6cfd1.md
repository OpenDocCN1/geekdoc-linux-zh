
Address: 432 Lombard Avenue SF California

# 列表 5.33: employees.sh

```
inputfile="employees.txt"

outputfile="employees2.txt"

echo "=> Input file:"

cat $inputfile

awk {

if($0 ~ /^Name:/) {

    x = substr($0,8) ","

    next

}

if($0 ~ /^EmpId:/) {

#跳过 EmpId 数据行
#x = x substr($0,7) ","
    next

}

if($0 ~ /^Address:/) {

    x = substr($0,9)

    print x

}

}' $inputfile > $outputfile

echo "=> Output file:"

cat $outputfile
```

运行列表 5.33 中的代码后的输出如下：

```
=> Input file:
Name: Jane Edwards
EmpId: 12345
Address: 123 Main Street Chicago Illinois

Name: John Smith
```

# 180 • GREP、SED 和 AWK 快速上手

EmpId: 23456
Address: 432 Lombard Avenue SF California

```
=> Output file:
Jane Edwards, 123 Main Street Chicago Illinois
John Smith, 432 Lombard Avenue SF California
```

现在你已经看到了了 `awk` 代码段和包含 `awk` 命令的 shell 脚本，这些代码说明了你可以在文件和数据集上执行的各种类型任务，现在你已经准备好学习一些用例了。下一节（即第一个用例）将向你展示如何将多个字段分隔符替换为单个分隔符，第二个用例将展示如何处理日期字符串。

# 多行记录 CSV 文件

本节包含一个具有多行记录的 CSV 文件，其中每个字段都在单独的一行（例如：`survived:0`），而不是每个记录使用逗号分隔的字段值。

当我们使用 `awk` 时，解决方案出奇地简单：将 `RS` 设置为分隔记录的字符串模式。在我们的情况下，我们需要将 `RS` 设置为 `\n\n`，之后 `$0` 将包含每个多行记录的内容。此外，指定 `FS='\n'` 使得每行都被视为一个字段（即 `$1`, `$2` 等）。

等 列表 5.34 显示了 CSV 文件 `multi_line_rows.csv` 的内容，列表 5.35 显示了 `multi_line_rows.sh` 的内容。

### 列表 5.34: multi_line_rows.csv

```
survived:0
pclass:3
sex:male
age:22.0

survived:1
pclass:1
sex:female
age:38.0

survived:0
pclass:3
sex:male
age:35.0

survived:1
pclass:3
sex:female
age:27.0
```

### 列表 5.35: multi_line_rows.sh

```
filename="multi_line_rows.csv"
cat $filename | awk '
BEGIN { RS="\n\n"; FS="\n\n" }
  # 名称/值对的格式如下：
  # survived:0 pclass:3 sex:male age:22.0
  split($1,arr,":"); printf("%s,\n",arr[2]);
  split($2,arr,":"); printf("%s,\n",arr[2]);
  split($3,arr,":"); printf("%s,\n",arr[2]);
  split($4,arr,":"); printf("%s\n",arr[2]);
}'
```

列表 5.35 中的核心思想已加粗显示，它将 `RS`（记录分隔符）的值指定为两个连续的换行符，并将 `FS`（字段分隔符）指定为换行符。主代码块通过冒号（":"）分隔符拆分 `$1`, `$2`, `$3` 和 `$4`，并打印第二个字段，即实际的数据值。

注意 `arr[1]` 包含字段名称（如 `survived`, `pclass`, `sex` 或 `age`），而 `arr` 包含字段的值。运行列表 5.35 中的代码，你将看到以下输出：

0,male,22.0
1,female,38.0
0,male,35.0
1,female,27.0

还有最后一个细节：列表 5.35 没有显示包含字段名称的表头。列表 5.36 展示了如何修改列表 5.34 来生成表头行。

### 列表 5.36: multi_line_rows2.sh

```
filename="multi_line_rows.csv"
cat $filename | awk '
BEGIN { RS="\n\n"; FS="\n\n"; count=0 }
  if(count == 0) {
  count += 1
  split($1,arr,":"); header = header "," arr[1]
  split($2,arr,":"); header = header "," arr[1]
  split($3,arr,":"); header = header "," arr[1]
  split($4,arr,":"); header = header "," arr[1]
  print header
}
  # 名称/值对的格式如下：
  # survived:0 pclass:3 sex:male age:22.0
  split($1,arr,":"); printf("%s,\n",arr[2]);
  split($2,arr,":"); printf("%s,\n",arr[2]);
```

# 182 • GREP、SED 和 AWK 快速上手

```
split($3,arr,":"); printf("%s,\n",arr[2]);
```

列表 5.36 将变量 `count` 初始化为值 0，紧接着是一个条件代码块，该代码块通过顺序拼接字段名称来构建变量 `header` 的内容（该变量将包含字段名称）。`header` 的内容会被打印出来，由于 `count` 的值已经增加，此代码块只会执行一次，防止了表头行重复显示。运行列表 5.36 中的代码，你将看到以下输出：

```
survived,class,age
0,male,22.0
1,female,38.0
0,male,35.0
1,female,27.0
```

上述代码的其他变体也是可能的，即更改字段的顺序。列表 5.37 以反向顺序显示字段：`age`, `sex`, `pclass` 和 `survived`。

### 列表 5.37: multi_line_rows.sh

```
filename="multi_line_rows.csv"
cat $filename | awk '
BEGIN { RS="\n\n"; FS="\n"; count=0 }
  # 字段按反序显示：
  if(count == 0) {
  count += 1
  split($4,arr,":"); header = header "," arr[1]
  split($3,arr,":"); header = header " " arr[1]
  split($2,arr,":"); header = header " " arr[1]
  split($1,arr,":"); header = header " " arr[1]
  print header
  }
  # 名称/值对的格式如下：
  # survived:0 pclass:3 sex:male age:22.0
  split($1,arr,":"); printf("%s,\n",arr[2]);
  split($2,arr,":"); printf("%s,\n",arr[2]);
```

列表 5.37 包含一个条件代码块，通过顺序拼接字段名称来构建变量 `header` 的内容。`header` 的内容会被打印出来，由于 `count` 的值已经增加，此代码块只会执行一次，防止了表头行重复显示。

核心思想是将 `RS`（记录分隔符）的值指定为两个连续的换行符，并将 `FS`（字段分隔符）指定为换行符。运行列表 5.37 中的代码，你将看到以下输出：

```
age,sex,pclass,survived
22.0,male,3,0
38.0,female,1,1
35.0,male,3,0
27.0,female,3,1
```

age,,,,,
2222,0,3,3
3
30,0,1,1
3
.0,0,3,0
27.0,female,,,,

## 处理,文件

列表 5.38, 5.39 和 5.40 分别显示了1.txt, file..txt 和...txt 的内容。

### 列表 5.38: file1.txt

```
survived:0
pclass:3
sex:male
age:22.0
```

### 列表 5.39: file2.txt

```
survived:1
pclass:1
sex:female
age:38.0
```

### 列表 5.40: file3.txt

```
survived:0
pclass:3
sex:male
age:35.0
```

# 使用 awk 处理多个文件

列表 5.41 显示了 `single-line.sh` 的内容，展示了如何打印文本文件中的单行。

### 列表 5.41: single-line.sh

```
echo "Print a single line from ONE file:"
awk 'FNR == 2 {print}' file1.txt file2.txt
```

## GREP、SED 和 AWK 快速上手

列表 5.41 包含一个 `echo` 命令来打印消息，随后跟一个 `awk` 命令，它只打印第二个输入文件（恰好是 `file2.txt`）。运行列表 5.41 中的代码，你将看到以下输出：

```
Print a single line from ONE file:
deep potato garlic file1 line
```

列表 5.42 显示了 `single-line2.sh` 的内容，展示了如何从多个文件中打印单行。

### 列表 5.42: single-line2.sh

```
echo "Print a line from MULTIPLE files:"
awk 'FNR == 2 {print}' file1.txt file2.txt
```

列表 5.43 显示了 `single-line3.sh` 的内容，它展示了如何从多个文件中打印单行，以及打印包含每个输出行的文件名。

### 列表 5.43: single-line3.sh

```
echo "Print a line from MULTIPLE files:"
awk 'FNR == 2 {print FILENAME ": " $0}' file1.txt file2.txt
```

# 使用 AWK 操作，第 3 部分 • 185

```awk
awk '
BEGIN { count = 0; token = "chicken" 
if($3 ~ token) {
count += 1
}
END { print "Token:",token,"token count:",count
}' file.txt
```

列表 5.44 包含一个显示消息的 `echo` 命令，随后 是一个包含 `BEGIN` 块的 `awk` 命令，该块将变量 `count` 和 `token` 分别初始化为 0 和 `chicken`。主执行块包含条件逻辑，检查 `$3` 的值是否匹配 `token` 的值，如果是，则 `count` 的值加1。

列表 5.44 的最后部分是一个 `END` 块，它打印 `token` 和变量 `count` 的值。运行列表 5.44 中的代码，将看到以下输出：

在多个文件中统计相同的标记：
Token: chicken token count: 7

列表 5.45 显示了 `count-tokens2.sh` 的内容，它向你展示了如何统计标记在多个文本文件的第二个字段中出现的次数，并统计处理的行数。

# 列表 5.45: count-tokens2.sh

```bash
echo "the same token in MULTIPLE files"
awk '
BEGIN { count = 0; token = "chicken" 
if($3 ~ token) {
count += 1
}
END { print "Token:",token,"token count:",count
print "Number of processed lines: \NR"
}' file.txt
```

列表 5.45 与列表 5.44 几乎相同，唯一的区别在于 `END` 块中的代码片段，它显示了已处理行数 `NR`。运行列表 5.45 中的代码，将看到以下输出：

在多个文件中统计相同的标记：
Token: chicken token count: 7
Number of processed lines: 15

# 在 awk 中两个文件的内连接

本节代码示例执行了 RDBMS 术语中称为“内连接”（inner join）的操作。列表 5.46 显示了 CSV 文件 `customers.csv` 的内容，列表 5.47 显示了 CSV 文件 `purchase_orders.csv` 的内容。

### 列表 5.46: customers.csv

```csv
1000,Jane Jones, 1234 Appian Way
2000,John Smith, 5678 Main Street
3000,Dave Stone, 3333 Birch Avenue
```

### 列表 5.47: purchase_orders.csv

```csv
1000,11100,2023/02/05,$125.00
1000,11200,2023/02/13,$480.00
2000,12100,2023/03/09,$312.00
2000,12200,2023/03/25,$567.00
```

列表 5.48 显示了 `join2.sh` 的内容，它展示了如何通过 Unix `join` 命令连接 `customers.csv` 和 `purchase_orders.csv` 的内容。

### 列表 5.48: join2.sh

```bash
# #shapeshed.com/unix-join/
file1="customers.csv"
file2="purchase_orders.csv"
echo "Joining $file1 and $file2:"
join -l 1 -l 2 -t," $file1 $file2
echo ""
```

```bash
# 使用 "o" 来指定输出字段的顺序：
echo "A different ordering of the output fields:"
join -l 1 -l 2 -t," -o 1.1,1.2,1.3,2.2,2.1 $file1 $file2
```

列表 5.48 首先初始化变量 `file1` 和 `file2` 分别引用 CSV 文件 `customers.csv` 和 `purchase_orders.csv`。下一部分代码调用 `join` 命令，根据这些文件第一个字段的内容对 `file1` 和 `file2` 执行连接。

列表 5.48 的最后部分包含另一个代码片段，它也对同一对 CSV 文件调用 `join` 命令，并指定了从 `file1` 和 `file2` 中显示的列以输出输出。运行列表 5.48 中的代码，将看到以下内容：

customers.csv and purchase_orders.csv:
1000,Jane Jones, 1234 Appian Way,11100,2023/02/05,$125.00
1000,Jane Jones 1234 Appian Way,11200,2023/02/13,$480.00
2000,John Smith 5678 Main Street,12100,2023/03/09,$312.00
2000,John Smith, 5678 Main Street,12200,2023/03/25,$367.00

输出字段的另一种排序：
1000,Jane Jones, 1234 Appian Way,11200,1000
1000,Jane Jones, 1234 Appian Way,11200,1000
2000,John Smith, 5678 Main Street,12100,2000
2000,John Smith, 5678 Main Street,12200,2000

列表 5.49 显示了 `duplicate-fields.sh` 的内容，它展示了如何打印第二和第三字段相同的行。

### 列表 5.49: duplicate-fields.sh

```awk
awk -F ',' '
  if($2 == $3) {
    print "Duplicate fields in row",NR,":1,$3
  }' datapoints.txt
```
