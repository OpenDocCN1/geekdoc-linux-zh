
```bash
$ mktemp testing.XXXXX
testing.1DRLuV
$ mktemp testing.XXXXX
testing.1VbtkW
$ mktemp testing.XXXXX
testing.PgGNGK
$ ls -1 testing*"
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.1DRLuV
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.PgGNGK
-rw-r--r-- 1 rich rich 0 Oct 17 21:30 testing.Uf113
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.1VbtkW
$
```

## 使用临时文件

`mktemp`命令将6个`X`替换为6位代码，以确保文件名在目录是唯一的。你可以创建多个临时文件并确保每一个都是：

```bash
$ mktemp testing.XXXXX
testing.1DRLuV
$ mktemp testing.XXXXX
testing.1VbtkW
$ mktemp testing.XXXXX
testing.PgGNGK
$ ls -1 testing*"
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.1DRLuV
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.PgGNGK
-rw-r--r-- 1 rich rich 0 Oct 17 21:30 testing.Uf113
-rw-r--r-- 1 rich rich 0 Oct 17 21:57 testing.1VbtkW
$
```

## 日志消息

有时，将输出同时发送到显示器和文件进行记录是有益的。与其双重重定向，可以使用特殊的`tee`命令。

`tee`命令就像管道的T型接头。它同时将数据从`STDIN`发送到两个目的地。一个目的地是`STDOUT`。另一个目的地是文件名。`mktemp`命令将6个`X`替换为6位代码，以确保文件名在目录是唯一的。你可以创建多个临时文件并确保每一个都是：

由于`tee`从标准输入（`STDIN`）重定向数据，你可以配合管道命令（pipe）使用它重定向任何命令的输出：

```
$ date | tee testfile
Sun Oct 19 18:56:21 EDT 2014
$ cat testfile
Sun Oct 19 18:56:21 EDT 2014
$
```

输出显示在标准输出（`STDOUT`）并写入指定的文件中。注意：默认情况下，`tee`命令在每次使用时都会覆盖输出文件：

```
$ who | tee testfile
rich pts/0 2014-10-17 18:41 (192.168.1.2)
$ cat testfile
rich pts/0 2014-10-17 18:41 (192.168.1.2)
$
```

如果你想向文件追加数据，必须使用`-a`选项：

```bash
$ date | tee -a testfile
Sun Oct 19 18:58:05 EDT 2014
$ cat testfile
rich pts/0 2014-10-17 18:41 (192.168.1.2)
$
```

使用这种技术，你可以将数据保存到文件中，并在显示器上为用户显示数据：

```bash
$ cat test22
#!/bin/bash
# using the tee command for logging

template=test22file

echo "This is the start of the test" | tee $testfile
echo "This is the second line of the test" | tee -a $testfile
echo "This is the end of the test" | tee -a $testfile
$ /test22
```

现在，你可以在为用户显示输出的同时，保存一份输出的永久副本。

## 实际示例

在将文件读取到脚本以及将脚本输出数据到文件时，文件重定向是非常常见的。这个示例脚本同时完成了这两项工作。它读取一个`.csv`格式的数据文件，并输出`SQL INSERT`语句，以将数据插入数据库中（参见第25章）。

该`shell`脚本使用命令行参数来定义要读取数据的`.csv`文件名。`.csv`格式用于从电子表格中导出数据，因此你可以将数据库数据放入电子表格，将电子表格存为`.csv`格式，读取文件并创建`INSERT`语句将数据插入`MySQL`数据库。

以下是该脚本的内容：

```bash
$cat test23
#!/bin/bash
# read file and create INSERT statements for MySQL

outfile=members.sql
IFS=','
while read lname fname address city state
do
  cat >> $outfile << EOF
  INSERT INTO members (lname,fname,address,city,state,zip) VALUES
  ('$lname', '$fname', '$address', '$city', '$state', '$zip');
EOF
done < ${1}
```

得益于文件重定向的操作，这个脚本非常短。脚本中发生了三次重定向操作。`while`循环使用`read`语句（在第14章中讨论过）从数据文件中读取文本。注意`done`语句中的重定向符号：

```
done < ${1}
```

`$1`代表你运行`test23`程序时的第一个命令行参数。它指定了从中读取数据的数据文件。`read`语句使用`IFS`字符解析文本，我们将其指定为逗号。

脚本中的另外两个重定向操作都出现在同一个语句中：

```bash
cat >> $outfile EOF
```

## 第 15 章：数据展示

这条语句包含一个输出追加重定向（双大于号符号）和一个输入追加重定向（双小于号符号）。输出重定向将`cat`命令的输出追加到`$outfile`变量指定的文件。`cat`命令的输入从标准输入重定向，以使用脚本内部存储的数据。`EOF`符号标记了追加到文件中数据的开始和结束分隔符：

```
INSERT INTO members (lname, fname, address, city, state, zip) VALUES
('$lname', '$fname', '$address', '$city', '$state', '$zip').
```

这段文本创建了一个`SQL INSERT`语句。注意，数据值被从`read`语句中读取的数据变量所替换。

所以基本上，`while`循环每次读取一行数据，将这些数据值插入`INSERT`模板中，然后将结果输出到输出文件。

对于这个实验，我使用了此文件作为输入：

```bash
$ cat members.csv
Blum, Richard, 123 Main St., Chicago, IL, 60601
Blum, Barbara, 123 Main St., Chicago, IL, 60601
Bresnahan, Christine, 456 Oak Ave., Columbus, OH, 43201
Bresnahan, Timothy, 456 Oak Ave., Columbus, OH, 43201
$
```

当你运行脚本时，注意显示器上的输出：

```
$ ./test23 < members.csv
$
```

当你查看`members.sql`输出文件时，你应该能看到输出数据：
