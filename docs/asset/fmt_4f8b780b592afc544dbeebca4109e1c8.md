
## 方法 20: `function while_LINE_line_FD_IN`

代码列表 2-30（续）

# 第二章 逐行处理文件的 24 方法 121

| real | 8m3.41s |
| user | 0m.41s |
| sys | 8m16.23s |

## 方法 21: `function while_LINE_line_cmdsub2_FD_IN`

| real | 8m35.62s |
| user | 0m14.46s |
| sys | 8m17.71s |

## 方法 22: `function while_read_LINE_FD_IN_AND_OUT`

| real | 0m.31s |
| user | 0m.29s |
| sys | 0m.00s |

## 方法 23: `function while_LINE_line_FD_IN_AND_OUT`

| real | 8m27.93s |
| user | 0m14.03s |
| sys | 8m11.04s |

## 方法 24: `function while_LINE_line_cmdsub2_FD_IN_AND_OUT`

| real | 8m27.55s |
| user | 0m14.04s |
| sys | 8m10.56s |

**代码列表 2-30（续）**

你可以看到，文件处理循环是平等的。有两个方法并列第一。方法 12 和 22 处理 1 MB 文件所需的时间均为 0.30 秒和 0.31 秒。方法 16 位居第二，耗时 0.45 秒。其余方法从不到 1 秒到超过 8 分钟不等。实际时间的排序输出显示在列表 2-31 中。

| real | 0m.30s 方法 12: |
| real | 0m.31s 方法 22: |
| real | 0m.45s 方法 16: |
| real | 0m.47s 方法 15: |

**列表 2-31** 按方法排序的时间数据

| real | 0m.61s 方法 2: |
| real | 0m.62s 方法 10: |
| real | 0m.74s 方法 7: |
| real | 0m.75s 方法 8: |
| real | 0m.36s 方法 5: |
| real | 0m.37s 方法 3: |
| real | 0m.31s 方法 6: |
| real | 0m.24s 方法 4: |
| real | 0m.75s 方法 11: |
| real | 0m.31s 方法 1: |
| real | 4m.16s 方法 18: *失败* |
| real | 4m.67s 方法 19: *失败* |
| real | 4m.21s 方法 9: *失败* |
| real | 2m.22s 方法 17: *失败* |
| real | 2m.25s 方法 24: |
| real | 8m.29s 方法 23: |
| real | 2m.52s 方法 14: |
| real | 3m.41s 方法 20: |
| real | 3m.44s 方法 13: |
| real | 8m.52s 方法 21: |

**列表 2-31（续）**

注意，前几个方法都在不到一秒内处理了这个 1 MB 文件。然后注意，最后六个方法都花了超过 8 分钟！现在希望你明白为什么处理文件的方式如此重要。最快方法和最慢方法之间的百分比差异是惊人的 177,773.333%！

让我们来看看前四种技术的代码。出现的顺序是方法 12、22、16、15 和 2。为了争论起见，我们就说方法 12 和 22 并列第一。列表 2-32 显示了方法 12。

```bash
function while_READ_LINE_bottom_FD_OUT
{
  # 方法 12
  # 清空 $OUTFILE
  >$OUTFILE
  # 将标准输出关联文件描述符 4
  # 并将标准输出重定向到 $OUTFILE
  exec 4<&1
  exec 1 >$OUTFILE
  while read LINE
  do
    echo "$LINE"
    :
  done < $INFILE
  # 恢复标准输出并关闭文件
  # 描述符 4
  exec 1<&4
  exec 4>&-
}
```

**列表 2-32** — 并列第一

列表 2-32 中的方法并列第一。该方法对输入和输出使用了文件描述符，如列表 2-33 所示。

```bash
function while_read_LINE_FD_IN_AND_OUT
{
  # 方法 22
  # 清空 $OUTFILE
  >$OUTFILE
  # 将标准输入关联文件描述符 3
  # 并将标准输入重定向到 $INFILE
  exec 3<&0
  exec 0<$INFILE
  # 将标准输出关联文件描述符 4
  # 并将标准输出重定向到 $OUTFILE
  exec 4<&1
  exec 1>$OUTFILE
  while read LINE
  do
    echo "$LINE"
    :
  done
  # 恢复标准输出并关闭文件
  # 描述符 4
  exec 1<&4
  exec 4>&-
  # 恢复标准输入并关闭文件
  # 描述符 3
  exec 0<&3
  exec 3>&-
}
```

**列表 2-33**

我编写 Shell 脚本时倾向于使用这种方法，因为维护代码生命周期可能会困难。如果用户不熟悉文件描述符，那么使用这种方法的脚本将难以理解。列表 2-32 中的方法产生了相同的计时结果，而且更容易理解。列表 2-34 显示了排名第二的循环方法。

```bash
for_LINE_cat_FILE_cmdsub2_FD_OUT ()
{
  # 方法 16
  # 清空 OUTFILE
  >$OUTFILE
  # 将标准输出关联文件描述符 4
  # 并将标准输出重定向到 $OUTFILE
  exec 4<&1
  exec 1>$OUTFILE
  for LINE in $(cat $INFILE)
  do
    echo "$LINE"
    :
  done
  # 恢复标准输出并关闭文件
  # 描述符 4
  exec 1<&4
  exec 4>&-
}
```

# 列表 2-34 方法 16 – 计时测试中的第二

列表 2-34 显示的方法是另一个惊喜：一种使用文件描述符输出重定向替换的 for 循环。我们在列表 2-35 中尝试了这种 for 循环，仅更改了命令替换的方法。

```bash
for_LINE_cat_FILE_FD_OUT () {
  # 方法 15
  # 清空 $OUTFILE
  >$OUTFILE
  # 将标准输出关联到文件描述符 4
  # 并标准输出重定向到 $OUTFILE
  exec 4<&1
  exec 1> $OUTFILE
  for LINE in `cat $FILE`
  do
    echo "$LINE"
  done
  # 恢复标准输出并关闭文件
  # 描述符 4
  exec 1<&4
  exec 4>&-
}
```

**列表 2-35** 方法 15 —— 计时测试第三名

如列表 2-36 所示，方法 15 和方法 16 之间的唯一区别是用于命令替换的技术。

## 第一部分 Shell 脚本基础

```text
Method 15:
function for_LINE_cat_FILE_FD_OUT
real      0m.47s
user      0m.38s
sys       0m.06s

Method 16:
function for_LINE_cat_FILE_cmdsub2_FD_OUT
real      0m.45s
user      0m.38s
sys       0m.05s
```

**列表 2-36** 方法 15 和方法 16 之间的计时差异

计时结果显示，两种命令替换方法之间的系统时间（或系统/内核时间）为 10 ms，总执行时间为 20 ms。列表 2-37 中的方法是不使用文件描述符逐行处理文件的最快方法。

```bash
function while_read_LINE_bottom
{
  # 方法 2
  # 清空 $OUTFILE
  >$OUTFILE
  while read LINE
  do
    echo "$LINE" >> $OUTFILE
    ;
  done < $INFILE
}
```
