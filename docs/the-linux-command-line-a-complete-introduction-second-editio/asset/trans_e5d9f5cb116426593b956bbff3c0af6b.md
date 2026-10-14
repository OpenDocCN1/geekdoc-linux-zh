
使用关联数组。这个名为 array-2 的脚本，当给定一个目录名时，会打印该目录中文件的列表，同时显示每个文件的所有者和组所有者。在列表末尾，脚本会打印属于每个所有者和组的文件数量统计。以下是脚本给定目录 `/usr/bin` 时的结果（为简洁起见已缩减）：

```
[me@linuxbox ~]$ array-2 /usr/bin
/usr/bin/2to3-2.6          root    root
/usr/bin/2to3             root    root
/usr/bin/a2p              root    root
/usr/bin/abrowser         root    root
/usr/bin/aconnect         root    root
/usr/bin/acpi_fake_key    root    root
/usr/bin/acpi_listen      root    root
/usr/bin/add-apt-repository root root
-- snip --
/usr/bin/zipgrep          root    root
/usr/bin/zipinfo          root    root
/usr/bin/zipnote          root    root
/usr/bin/zip              root    root
/usr/bin/zipsplit         root    root
/usr/bin/zsdecode         root    root
/usr/bin/zsoelim          root    root

File owners:
daemon  :   1 file(s)
root    : 1394 file(s)

File group owners:
crontab :   1 file(s)
daemon  :   1 file(s)
lpadmin :   1 file(s)
mail    :   4 file(s)
mlocate :   1 file(s)
root    : 1380 file(s)
shadow  :   2 file(s)
ssh     :   1 file(s)
tty     :   2 file(s)
utmp    :   2 file(s)
```

以下是该脚本的列表（带行号）：

```
1   #!/bin/bash
2
3   # array-2: Use arrays to tally file owners
4
5 declare -A files file_group file_owner groups owners
6
7 if [[ ! -d "$1" ]]; then
8     echo "Usage: array-2 dir" >&2
9     exit 1
10 fi
11
12 for i in "$1/*"; do
13     owner="$(stat -c %U "$i")"
14     group="$(stat -c %G "$i")"
15     files["$i"]="$i"
16     file_owner["$i"]="$owner"
17     file_group["$i"]="$group"
18     ((++owners[$owner]))
19     ((++groups[$group]))
20 done
21
22 # List the collected files
23 { for i in "${files[@]}"; do
24     printf "%-40s %-10s %-10s\n" \
25         "$i" "${file_owner["$i"]}" "${file_group["$i"]}"
26 done } | sort
27 echo
28
29 # List owners
30 echo "File owners:"
31 { for i in "${!owners[@]}"; do
32     printf "%-10s: %5d file(s)\n" "$i" "${owners["$i"]}"
33 done } | sort
34 echo
35
36 # List groups
37 echo "File group owners:"
38 { for i in "${!groups[@]}"; do
39     printf "%-10s: %5d file(s)\n" "$i" "${groups["$i"]}"
40 done } | sort
```

让我们看一下这个脚本的机制。

第 5 行：关联数组必须使用带 `-A` 选项的 `declare` 命令创建。在本脚本中，我们创建了如下五个数组：

- `files` 包含目录中的文件名，以文件名为索引。
- `file_group` 包含每个文件的组所有者，以文件名为索引。
- `file_owner` 包含每个文件的所有者，以文件名为索引。
- `groups` 包含属于该索引组的文件数量。
- `owners` 包含属于该索引所有者的文件数量。

**第 7–10 行：** 这些行检查是否传入了有效的目录名作为位置参数。如果没有，则显示一条用法消息，并以退出状态 1 退出脚本。

**第 12–20 行：** 这些行循环遍历目录中的文件。使用 `stat` 命令，第 13 和 14 行提取文件所有者和组所有者的名称，并使用文件名作为数组索引，将这些值赋给对应的数组（第 16 和 17 行）。同样，文件名本身也被赋给 `files` 数组（第 15 行）。

**第 18–19 行：** 属于文件所有者和组所有者的文件计数各增加一。

**第 22–27 行：** 输出文件列表。这是通过 `"${array[@]}"` 参数展开实现的，它将展开为整个数组元素列表，每个元素被视为一个单独的词。这样文件名即使包含嵌入空格也能处理。还要注意，整个循环被括在大括号内，构成一个组命令。这允许将循环的全部输出通过管道传给 `sort` 命令。这是必要的，因为数组元素展开后并未排序。

**第 29–40 行：** 这两个循环与文件列表循环类似，不同之处在于它们使用 `"${!array[@]}"` 展开，该展开扩展为数组索引列表，而不是数组元素列表。

## 进程替换

虽然它们看起来相似，并且都可以用于组合重定向流，但组命令和子 shell 之间有一个重要区别。组命令在当前 shell 中执行其所有命令，而子 shell（顾名思义）在当前 shell 的子副本中执行其命令。这意味着环境被复制并交给一个新的 shell 实例。当子 shell 退出时，环境的副本会丢失，因此任何更改
