
![](img/75f39fc91296b889c0653851accdfd46_334_0.png)

### 使用 vi 指令获取命令

你可以使用 `vi` 或 `emacs` 编辑器编辑历史记录列表中的条目。我将在本章中介绍 `vi` 编辑器，因为它是 UNIX 系统上使用最广泛的。然而，你可以使用 `emacs` 编辑器执行本章所示的所有相同功能。

你使用 `vi` 编辑历史记录列表的方式与使用 `vi` 编辑文件的方式相同。你按下 `escape` 键，并使用标准的 `vi` 键进行上下左右移动、插入、删除和更改文本。在本节中，我将介绍使用 `vi` 命令从历史记录列表中获取命令，然后介绍在将命令恢复到命令行后编辑该命令。当命令按你的喜好编辑好后，你按下 `enter` 键执行该命令，并将其放置在命令列表的最底部。

你的编辑器通常在你的本地 `.profile` 或 `/etc/profile` 中设置。你可以查看这些文件，看看系统管理员为你设置了哪个编辑器。当我在系统上发出 `env` 和 `set` 命令时，两者都报告 `EDITOR=vi`。这与我设置为 `vi` 编辑器的 `/etc/profile` 相对应。

让我们首先看看使用 `vi` 获取一些早先发出的命令。本节中的示例使用了 `vi` 功能，这些功能在 `vi` 章节和 `vi` 快速参考卡中都有描述。本节中的 `k`, `j`, `G` 和搜索命令在命令行上的操作方式与你使用 `vi` 编辑文件时相同。

按下 `escape` 键和某个命令允许你在 `ksh` 中执行各种功能。下面的示例展示了生成历史记录列表并发出 `escape k` 以召回上一条命令：

![](img/75f39fc91296b889c0653851accdfd46_334_1.png)

### 历史记录列表

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set |grep edit
137 set | grep vi
138 env | grep vi
139 history
140 who
martyp $ history
```

![](img/75f39fc91296b889c0653851accdfd46_335_0.png)

输入 `escape k` 会调出最后一条发出的命令，在本例中即为第 140 行的 `who` 命令。每按一次 `k`，就会获取前一条 `ksh` 命令。这等同于按下 `escape` 键和 `-` 键。你可以使用 `escape nk` 指定要在历史记录列表中回溯的命令数量，其中 `n` 是你希望回溯的命令数。以下示例展示了输入 `escape 5k` 以调取历史记录列表中倒数第五条命令：

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set |grep edit
137 set | grep vi
138 env | grep vi
139 history
140 who
martyp $ set |grep edit
```

![](img/75f39fc91296b889c0653851accdfd46_335_1.png)

输入 `escape 5k` 调出了历史记录列表中倒数第五条，即第 136 行的命令。这等同于输入 `escape 5`。

你还可以在历史记录列表中向前移动，使用 `j` 的方式与我们使用 `k` 向后移动历史记录的方式相同。让我们在历史记录列表中向后移动五条命令至第 136 行，输入 `escape 5k`，然后使用 `escape 3j` 向前移动三条命令至第 139 行，如下例所示：

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132 more .profile
133 more .profile | grep rof
134 more .profile | grep vi
135 more /etc/profile | grep vi
136 set | grep edit
137 set | grep vi
138 env | grep vi
139 history
140 history
martyp $ who
```

输入 `escape 3j` 使我们前进到第 139 行，这与输入 `escape 3` 相同。

我们还可以使用 `escape G` 回到历史记录列表中最旧的命令。你可以使用 `escape nG` 回到历史记录列表中特定的命令编号，其中 `n` 是来自历史记录文件的特定命令编号。以下示例展示了输入 `escape 126G` 从历史记录列表中回到第 126 行：

```
martyp $ history
125 man fc
126 set | more
127 exit
128 history
129 k
130 env | more
131 set | more
132     more .profile
133     more .profile | grep rof
134     more .profile | grep vi
135     more /etc/profile | grep vi
136     set |grep edit
137     set | grep vi
138     env | grep vi
139     history
140     who
martyp $ set | more
```

![](img/75f39fc91296b889c0653851accdfd46_337_0.png)

你还可以基于搜索从历史记录列表中调出行。例如，如果你想从历史记录列表中调出最近包含 `profile` 的命令，你可以输入 `/profile`，即斜杠字符后跟 `profile`，以获得以下示例中显示的结果：

```
martyp $ history
125     man fc
126     set | more
127     exit
128     history
129     k
130     env | more
131     set | more
132     more .profile
133     more .profile | grep rof
134     more .profile | grep vi
135     more /etc/profile | grep vi
136     set |grep edit
137     set | grep vi
138     env | grep vi
139     history
140     who
martyp $ more /etc/profile | grep vi
```

![](img/75f39fc91296b889c0653851accdfd46_337_1.png)

搜索最近出现的 `profile` 产生第 135 行。`vi` 中的许多其他搜索也可以在命令行中使用。`vi` 章节和 `vi` 快速参考卡片中包含更多你可能想在命令行上尝试的搜索信息。

### 使用 vi 指令在命令行上编辑

在你“调取”想要编辑的命令或输入了需要编辑的命令后，你可以使用你的 `vi` 指令在命令行上进行修改。

![](img/75f39fc91296b889c0653851accdfd46_338_0.png)

`ksh` 在从历史记录列表中调取命令后立即将你置于输入模式。这种方法是 `vi` 程序（用于编辑文件）的相反，后者默认将你置于控制模式。从历史记录列表中调取命令后，若要在 `ksh` 中使用 `vi`，你必须按下 `escape` 才能进入控制模式。

![](img/75f39fc91296b889c0653851accdfd46_338_1.png)
