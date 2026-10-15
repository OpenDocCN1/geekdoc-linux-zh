
在 `level1` 子目录中创建一个名为 `letter1` 的零长度文件：

```
$ touch level1/letter1<Enter>
```

切换到 `level1` 子目录：

```
$ cd level1<Enter>
```

在 `level1` 下创建一个名为 `level2` 的子目录：

```
$ mkdir level2<Enter>
```

在 `level2` 子目录中创建一个名为 `letter2` 的零长度文件：

```
$ touch level2/letter2<Enter>
```

切换到你的主目录：

```
$ cd<Enter>
```

在你的主目录中，执行列出所有以字母 1 开头的文件的命令。记录显示的名称：

```
$ ls 1*<Enter>
```

在你的主目录中，执行查找仅以字母 1 开头的文件的命令：

```
$ find . -name '1\*' -type f<Enter>
```

最后，记录显示的名称。

#### 7. 在 `/etc/passwd` 文件中查找所有用户名以 team 开头的行：

```
$ grep team /etc/passwd<Enter>
```

#### 8. 在 `/etc/passwd` 文件中查找所有以字母 t 开头的行：

```
$ grep '^t' /etc/passwd<Enter>
```

#### 9. 在 `/etc/passwd` 中查找所有包含 0 到 9 之间数字的行：

```
$ grep [0-9] /etc/passwd<Enter>
```

#### 10. 重复前一步的搜索，但这次只显示包含该模式的行数：

```
$ grep -c [0-9] /etc/passwd<Enter>
```

#### 11. 使用 `ps` 和 `grep` 命令显示由除你自己以外的用户启动的进程：

```
$ ps ua | grep -v username<Enter>
```

#### 12. 按字母顺序显示 `/etc/passwd` 文件的内容：

```
$ sort /etc/passwd<Enter>
```

#### 13. 以相反的顺序显示同一文件的内容：

```
$ sort -r /etc/passwd<Enter>
```

#### 14. 显示 `/etc/passwd` 的前十行：

```
$ head /etc/passwd<Enter>
```

#### 15. 显示 `/etc/passwd` 的前五行：

```
$ head -5 /etc/passwd<Enter>
```

#### 16. 显示 `/etc/passwd` 的最后十行：

```
$ tail /etc/passwd<Enter>
```

#### 17. `tail` 命令对于剥离命令输出的头部信息也很方便。首先，列出你的系统上当前运行的所有进程。注意标题：

```
$ ps ua | less<Enter>
```

#### 18. 接下来，显示你的系统上运行的所有进程，排除头部信息：

```
$ ps ua | tail +2 | less<Enter>
```

参见附录 B 获取答案。

## 测验

- 1. 你会使用哪个命令来定位系统中所有以文本字符串 `mis` 开头的文件？

- 2. 解释以下命令：

```
$ ps ua | grep -w root | grep -w /sbin*<Enter>
```

- 3. 解释以下命令：

```
$ ls -l /home/teamok | egrep 'un$|isc$|yc$' | sort -r +5 | tail +2 | head -7<Enter>
```

参见附录 C 获取答案。

##### 第 9 章

## 高级 Linux 实用工具

在第 8 章“基础 Linux 实用工具”中，我们讨论了一些基础的 Linux 实用工具。本章继续该讨论并扩展你执行文件系统管理的能力。在本章的几个部分和示例中，我们再次引用桑丘的文件结构。

### 最大化每条命令的工作量：`xargs`

为了高效执行，`xargs` 是 Linux/UNIX 提供的最佳命令之一。`xargs` 有两个非常有价值的功能，我们将在这里讨论。

#### `xargs`：对“智能”命令的最优执行

一些 Linux/UNIX 命令足够“智能”，可以接受来自参数行的输入并执行它。此外，如果参数行为空，命令又足够“智能”以从 `stdin`（通常是一个管道）获取输入。`xargs` 是一个非常高效的命令，它可以逐行从 stdin 读取多个参数，然后将尽可能多的参数组装成单个命令行，直到它确定已达到其容量。“达到容量”意味着如果添加更多参数，`xargs` 将无法执行。此外，`xargs` 的参数通常本身就是命令或程序，正如你将在示例 9.1 中看到的那样。

因此，一旦 `xargs` 以这种方式将其输入填充至容量，所有命令将被执行。如果源中仍有更多参数，`xargs` 会将更多参数组装成另一个单个命令行，直到它也被填充至容量，然后这些命令将被执行。`xargs` 命令持续执行此任务，直到耗尽给定的参数/命令供应。

`xargs` 的语法如下：

```
$ command [options] | xargs [options] [arguments]<Enter>
```

我们建议在执行 `xargs` 时，应包含 `-t` 选项（它启动详细模式）——至少在你熟悉 `xargs` 并且它正做着你想要的事情之前如此。当你习惯了 `xargs` 并且信任它时，你很可能不会再选择使用 `-t` 选项。

#### 示例 9.1 使用“智能”命令与 `xargs`

在示例 9.1 中，我们将展示 `xargs` 的两个相当简单的应用程序。但首先，让我们看看图 9.1 中堂吉诃德在 RFI 目录结构部分最新版本。他正忙着为下一次“高尚事迹部门”之旅做准备。他扩展了他的文件结构，以便他可以为每个条目专门分配一个文件。

堂吉诃德此时有两个目标：

- 打印他新的 `/home/quixote/provisions` 子目录中的大量文件名

- 更改现有文件的名称，以便他以后可以添加具有相似名称的新文件

以下是他如何使用 `xargs` 和其他命令来打印文件名的方法：

```
$ cd /home/quixote/provisions<Enter>
$ ls > prov_list<Enter>
```

![](img/cae5c706c216875d12d4b7d28144cc71_282_0.png)

**图 9.1** 堂吉诃德的 RFI 目录结构部分。

```
$ cat prov_list<Enter>
accom_inns
bills
buckler
cell_ph
.
.
travcl_H2O
withr_fcsts
$ xargs -t lpr < prov_list
lpr accom_inns bills buckler ... insurance
lpr lance maps medical ... withr_fcsts
```

在这个第一步中，堂吉诃德演示了一次打印多个文件名。他移动到 `provisions` 子目录，然后在那里创建一个名为 `prov_list` 的文件，该文件由子目录中所有文件的名称组成。这些是他想要打印的名称。他使用 `cat` 检查新文件列表中的文件名。

在此步骤中，堂吉诃德使用了组合的 `xargs` 和 `lpr` 命令及其结果。来自 shell 的反馈表明，在第一次执行 `lpr` 之前，`xargs` 能够用从 `accom_inns` 到 `insurance` 的参数填充命令行。然后，`xargs` 有能力将剩余的文件（从 `lance` 到 `wthr_fests`）传递给 `lpr` 进行第二次执行。注意，堂吉诃德使用 `-t` 选项以确保 `xargs` 已将输入传递给 `lpr`，且 `lpr` 确实执行了。

由于现有文件大多与他三月的前一次旅程有关，他选择更改它们的文件名以反映该日期。以下是他一次性更改所有文件名的方法：

```
$ ls | xargs -t -i mv {} {.}.mar01<Enter>
mv accom_inns accom_inns.mar01
mv bills bills.mar01
mv buckler buckler.mar01
mv cell_ph cell_ph.mar01
.
.
.
mv travel_H2O travel_H2O.mar01
mv wthr_fests wthr_fests.mar01
```
