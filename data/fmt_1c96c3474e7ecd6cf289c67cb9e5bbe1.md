
```
$ sort +0 -1 sortfile ...仅按第一个字段排序。
Feb End chapter 1 14
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
may End chapter 7 17th
```

## 排序文件：`sort`

Apr End Chapter 5 1

Jan Start chapter 1 30th

Mar Start chapter 7 27

jan Start chapter 3 10th

$

注意，前导空格被计入第一个字段的一部分，这导致了奇怪的排序序列。此外，我更希望月份按正确的顺序排序，例如 `Jan` 在 `Feb` 之前。`-b` 选项忽略了前导空白，而 `-M` 选项根据月份顺序排序字段。这里有一个更好的示例：

```
$ sort +0 -1 -bM sortfile ...按第一个月份排序。
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
Jan Start chapter 1 30th
jan Start chapter 3 10th
Feb End chapter 1 14
Mar Start chapter 7 27
Apr End chapter 5 1
may End chapter 7 17th
$
```

示例文件已按月份正确排序，但日期仍然是乱序的。你可以在命令行上指定多个排序字段来解决这个问题。`sort` 工具首先根据第一个排序规范对所有行进行排序，然后使用第二个排序规范对第一个规范结果相同的行进行排序。因此，要按月份和日期对示例文件进行排序，必须先按第一个字段排序，再按第五个字段。此外，第五个字段必须使用 `-n` 选项按数字排序。

```
$ sort +0 -1 -bM +4 -nn
jan Start chapter 3 10th
Jan End chapter 3 23rd
Jan Start chapter 5 23rd
Jan Start chapter 1 30th
Feb End chapter 1 14
Mar Start chapter 7 27
Apr End chapter 5 1
may End chapter 7 17th
$
```

除了空格以外的字符经常用于分隔字段。例如，`etc/passwd` 文件包含存储在冒号分隔字段中的用户信息。你可以使用 `-t` 选项指定备用字段分隔符。在下面的示例中，我根据由冒号分隔的字段对文件进行了排序。

```
$ cat sortfile2 ...查看测试文件。
jan:Start chapter 3:10th
Jan:Start chapter 1:30th
Jan:Start chapter 5:23rd
Jan:End chapter 3:23rd
Mar:Start chapter 7:27
may:End chapter 7:17th
Apr:End chapter 5:1
Feb:End chapter 1:14
$ sort -t: +0 -1 -bM +2 -n sortfile2 ...冒号分隔符。
jan:Start chapter 3:10th
Jan:End chapter 3:23rd
Jan:Start chapter 5:23rd
Jan:Start chapter 1:30th
Feb:End chapter 1:14
Mar:Start chapter 7:27
Apr:End chapter 5:1
may:End chapter 7:17th
$
```

除了空格以外的字符经常充当字段分隔符。例如，`etc/passwd` 文件包含存储在冒号分隔字段中的用户信息。你可以使用 `-t` 选项指定备用字段分隔符。在下面的示例中，我根据由冒号分隔的字段对文件进行了排序。

```
$ cat sortfile2 ...查看测试文件。
jan:Start chapter 3:10th
Jan:Start chapter 1:30th
Jan:Start chapter 5:23rd
Jan:End chapter 3:23rd
Mar:Start chapter 7:27
may:End chapter 7:17th
Apr:End chapter 5:1
Feb:End chapter 1:14
$ sort -t: +0 -1 -bM +2 -n sortfile2 ...冒号分隔符。
jan:Start chapter 3:10th
Jan:End chapter 3:23rd
Jan:Start chapter 5:23rd
Jan:Start chapter 1:30th
Feb:End chapter 1:14
Mar:Start chapter 7:27
Apr:End chapter 5:1
may:End chapter 7:17th
$
```
