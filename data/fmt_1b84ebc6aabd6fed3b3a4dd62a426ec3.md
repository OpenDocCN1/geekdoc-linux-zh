
```
[root@krosum Temp]#
[root@krosum Temp]# ps -L
PID LWP TTY TIME CMD
1195 1195 pts/0 00:00:00 bash
25704 25704 pts/0 00:00:00 ps
root@krosum Temp]# 
```

![](img/398fde7fc51cbef611658dfbb1fe2.png)

# 第 14 章 - 过滤器 (FILTERS)

在 Unix/Linux 中，过滤器是指从标准输入获取数据、对输入进行处理并将结果发送到标准输出的任何命令。某些过滤器可以直接从文件接收数据。

## 常用过滤器

| 命令 | 说明 |
|---|---|
| `cut` | 传递指定的列 |
| `paste` | 合并列 |
| `cmp` | 比较两个文件 |
| `comm` | 识别两个文件的共同行 |
| `diff` | 识别两个文件或两个目录间共同文件的差异 |
| `head` | 传递数据开头指定的行 |
| `tail` | 传递数据末尾指定的行 |
| `sort` | 排序 |
| `tr` | 翻译字符 |
| `uniq` | 去除重复行 |
| `grep` | 搜索模式 |
| `find` | 搜索文件 |

## 过滤器与管道

在 Unix/Linux 中，过滤器依赖标准输入。一个命令的输出可以使用管道 (`|`) 用作另一个命令的输入。

## cut 命令

虽然列规范在数据围绕固定列组织时效果良好，但在其他情况下并不适用。例如查看下面的快照。`file.csv` 的字段由逗号 (`,`) 分隔。在这里，如果我们想根据第 1 个字段（员工 ID）进行过滤，请使用 `-d` 选项。

## 字段规范

当数据由 `,` 或任何特殊字符分隔时，使用字段从文件中提取数据更为简单。要指定字段，我们使用字段选项 (`-f`)。字段从行首开始编号，第一个字段为字段 1。与字符选项一样，多个字段用逗号分隔，且逗号后没有空格。连续的字段可以使用范围来指定。

```bash
[student@krosum~]$ cat -n emp.csv
1 101,kumar,sales,pune,1000
2 203,arun,prod,bglore,1245
3 432,vijay,sales,chennai,3500
4 323,xerox,HR,mumbai,5490
5 894,vijay,prod,delhi,4590
6 245,theeba,hr,hyd,9000
7 456,ram,sales,pune,8905
8 399,karthik,prod,bglore,5904
```

```bash
[student@krosum~]$ cut -d, -f 1 emp.csv
101
203
432
323
894
245
456
399
```

```bash
[student@krosum~]$ cut -d, -f 2,4 emp.csv
kumar,pune
arun,bglore
vijay,chennai
xerox,mumbai
vijay,delhi
theeba,hyd
ram,pune
karthik,bglore
```

如何过滤员工姓名和员工工作城市？

如何从 `emp.csv` 文件提取第 2 字段到第 4 字段（范围）？

```bash
[student@krosum ~]$ cut -d, -f 2,4 emp.csv
kumar,pune
arun,bglore
vijay,chennai
xerox,mumbai
vijay,delhi
theeba,hyd
ram,pune
karthik,bglore
[student@krosum ~]$ cut -d, -f 2-4 emp.csv
kumar,sales,pune
arun,prod,bglore
vijay,sales,chennai
xerox,HR,mumbai
vijay,prod,delhi
theeba,hr,hyd
ram,sales,pune
karthik,prod,bglore
```

## paste 命令

`paste` 命令将行合并在一起。它从两个或多个文件中获取输入。

### 语法

```
paste filename1 filename2 .. filename
[student@krosum ~]$ cat -n p1.log 
[student@krosum ~]$ cat -n p2.log
  1 data1                 1 DATA1
  2 data2                 2 DATA2
  3 data3                 3
  4                       4
  5 data5                 5
  6                       6
  7 data7                 7 DATA-END
[student@krosum ~]$ paste p1.log p2.log
data1                   DATA1
data2                   DATA2
data3

data5

data7                 DATA-END
[student@krosum ~]$
```

使用 `paste` 命令我们可以合并多个文件。

`paste` 命令将每个文件视为一列。如果文件超过两个，则会将每个文件中对应的行（用制表符分隔）写入输出流。上面的输入文件 `p1.log` 包含 7 行，包括 2 个空行（第 4 行和第 6 行）。输入文件 `p1.log p2.log` 包含 7 行，包括 5 个空行。因此，我们将 `p1.log` 和 `p2.log` 合并时，输入文件 `p1.log` 变成第 1 列，文件 `p2.log` 变成第 2 列。

注意：`cat` 和 `paste` 命令在合并多个文件方面相似。但 `cat` 命令按垂直（行）合并文件，而 `paste` 命令按水平（列）合并文件。

```bash
$student@krosum-$ cat p1.log p2.log
[student@krosum-$]$ paste p1.log p2.log
data1 DATA1
data2 DATA2
data3 DATA3
data5
data7 DATA-END
[student@krosum-$]
```

```bash
$student@krosum ~]$ cat -n IP1
1 data1
2 data2
3 data3
4 data4
5 data5
[student@krosum ~]$ cat -n IP2
1 DATA1
2 DATA2
[student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
data5
[student@krosum ~]$
```

如果文件内容不一致，如果每个文件包含的行数不同，所有数据仍会带有分隔符写入输出中。例如，如果第一个文件比第二个文件长，`paste` 将带有分隔符（如制表符）写入第一个文件的额外数据。

如果第一个文件比第二个文件短，`paste` 将一个分隔符后跟来自第二个文件的额外数据写入输出流。下面的示例显示了输入文件 `IP2` 和 `IP1` 的合并情况。请查看上述情况的高亮框。

```bash
[student@krosum ~]$ cat -n IP1
1 data1
2 data2
3 data3
4 data4
5 data5
[student@krosum ~]$ cat -n IP2
1 DATA1
2 DATA2
[student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
data5
[student@krosum ~]$ $student@krosum ~]$ paste IP2 IP1
DATA1 data1
DATA2 data2
data3
data4
data5
[student@krosum ~]$ $student@krosum ~]$ paste IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
[student@krosum ~]$ $student@krosum ~]$ paste -d IP1 IP2
data1 DATA1
data2 DATA2
data3
data4
[student@krosum ~]$
```

可以使用 `-d` 选项指定分隔符。`-s` 选项将每个文件转换为单行。输入文件 1 放在第 1 行，输入文件 2 放在第 2 行。

```bash
[student@krosum ~]$ paste IP1 IP2

data1 DATA1

data2 DATA2

data3

data4

[student@krosum ~]$ paste -s IP1 IP2

data1 DATA1data2 DATA2data3data45
