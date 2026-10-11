
`[student@krosum ~]$ sort -t, -k 2 emp.csv |cut -d, -f 2`

arun

karthik

kumar

ram

theeba

vijay

vijay

xerox

process 1 (`cut`)

process 2 (`sort`)

stdout to PIPE

STDIN(reading) PIPE

我们可以任何顺序组合 `cut|sort`（或 `sort|cut`）。请看下方的快照，两种可能的结果是相同的。

## uniq 命令

`uniq` 命令删除重复行，但不进行排序。它是区分大小敏感的。

```
[student@krosum ~]$ cat F1.txt

p1.c

p1.c

p1.c

p2.c

p2.c

p2.c

p3.c

p3.c

p4.c

p4.c

p4.c

[student@krosum ~]$ uniq F1.txt

p1.c

p2.c

p3.c

p4.c

[student@krosum ~]$
```

`uniq-option` 输入文件

记住所有过滤命令的输出都是运行时结果，不会修改输入文件。

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq -i IP1

html

HTML

java

C++

C++

java

java

[student@krosum ~]$
```

如果重复项是连续格式（一个接一个），`uniq` 会省略重复项；但如果重复项不是连续格式（例如相邻格式），重复项将会保留。`java` 的重复不是连续格式，因此不会被省略。在这种情况下，在省略重复行之前，我们可以先对它们进行排序，然后使用 `uniq` 命令。

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ sort IP1

C++

C++

html

HTML

java

java

[student@krosum ~]$ sort IP1|uniq -i

C++

html

java

java

C++
```

### 计算重复行 (-c) 选项

```
[student@krosum ~]$ cat IP1

html

HTML

java

C++

C++

java

[student@krosum ~]$ uniq -c IP1

1 html

1 HTML

1 java

1 C++

1 C++

1 java

[student@krosum ~]$
```

### 非重复行 (-u) 选项

```
[student@krosum ~]$ cat names.txt

kumar

kumar

arun

arun

vijay

vijay

xerox

xerox

theeba

karthik

[student@krosum ~]$ uniq -u names.txt

theeba

karthik
```

非重复行选项是 `-u`。它会抑制重复行的输出，仅列出文件中的唯一行。

## cmp 命令

Linux/UNIX 中的 `cmp` 命令用于按字节比较两个文件，帮助你判断两个文件是否相同。当使用 `cmp` 比较两个文件时，如果发现差异，它会在屏幕上报告第一个个不匹配处的位置；如果没有发现差异（即文件相同），`cmp` 不显示任何消息并直接返回。

```
[student@krosum ~]$ cat -n F1.txt

1 p1.c

2 p2.c

3 p3.c

4 p4.c

[student@krosum ~]$ cat -n F3.txt

1 p1.c

2 p2.c

3 p3.c

4 p4.c

[student@krosum ~]$ cmp F1.txt F3.txt
```

如果文件内容不是唯一的，它将显示如下消息。

### cmp 命令的选项

`-b(print-bytes)`
如果我们想让 `cmp` 将差异字节输出到终端，请使用 `-b` 选项。

```
[student@krosum ~]$ cat -n names.txt

1 arun

2 babu

3 paul

[student@krosum ~]$ cat -n names1.txt

1 arun

2 babu

3 PAUL

4 xerox

[student@krosum ~]$ cmp names.txt names1.txt

names.txt differ at line 3

[student@krosum ~]$ cmp -b names.txt names1.txt

names.txt names1.txt differ: byte 11, line 3
```

```
[student@krosum ~]$ cat -n names.txt
1 arun
2 babu
3 paul
[student@krosum ~]$ cat -n names1.txt
1 arun
2 babu
3 PAUL
4 xerox
[student@krosum ~]$ cmp names.txt names1.txt
differ: byte 11, line 3
[student@krosum ~]$ cmp -b names.txt names1.txt
differ: byte 11, line 3
```

现在，`-i` 选项在配合 `cmp` 使用时，可以跳过文件中特定数量的初始字节进行比较。这是通过将字节数作为参数来实现的。

```
[student@krosum ~]$ cat -n F1.txt
1 p1.c
2 p2.c
3 p3.c
4 p4.c
[student@krosum ~]$ cat -n F2.txt
1 p2.c
2 p3.c
3 p4.c
4 p5.c
5 p6.c
[student@krosum ~]$ diff F1.txt F2.txt
1d0
< p1.c
4a4,5
> p5.c
> p6.c
[student@krosum ~] 
```

示例：

```
[student@krosum ~]$ cp F1.txt F3.txt
[student@krosum ~]$ cat >>F3.txt
test1.c
append operation
test2.c
[student@krosum ~]$ cat -n F3.txt
1 p1.c
2 p2.c
3 p3.c
4 p4.c
5 test1.c
6 test2.c
[student@krosum ~]$ diff F1.txt F3.txt
4a5,6
> test1.c
append
> test2.c
[student@krosum ~] 
```

### 目录差异

```
[student@krosum ~]$ ls D1
p1.log p2.log
[student@krosum ~]$ ls D2
[student@krosum ~]$ diff D1 D2 Directory Differences
Only in D2: F1.txt
Only in D1: p1.log
Only in D1: p2.log
[student@krosum ~]
```

## common (comm) 命令

`comm` 命令用于两个文件中相同的行。它逐行比较文件并以三列显示结果。左列包含 file1 中特有的行；中间列包含 file2 中特有的行；右列包含两个文件中共有的行。

注意：两个输入文件（file1 和 file2）必须是经过排序的。

语法

`comm -option file1 file2`

```
[student@krosum ~]$ cat F1.txt
p1.c
p2.c
p3.c
p4.c
[student@krosum ~]$ cat F2.txt
p2.c
p5.c
p6.c
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
      p5.c
      p6.c
[student@krosum ~]$ _
```

```
[student@krosum ~]$ comm F1.txt F2.txt
p1.c
      p2.c
p3.c
p4.c
    p5.c
      p6.c
[student@krosum ~]$ comm -23 F1.txt F2.txt # 省略第 2 和第 3 列
p1.c
p3.c
p4.c
[student@krosum ~]$ █
```

**任务：** 仅过滤第一列（F1.txt 文件内容中的唯一元素）
