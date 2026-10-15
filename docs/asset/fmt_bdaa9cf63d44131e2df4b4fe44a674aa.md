
```
martyp $ history fc
110    fc -l
111    history
112    alias history="fc -l"
113    history
114    alias history="fc -l"
115    history
116    history 128
117    history 128 | more
118    history 200
119    alias
120    history 1
121    inv
122    env
123    env | more
124    history 1
125    more .profile
126    env | grep HIS
127    exit
128    env
129    env | grep HIS
130    more .profile
131    history
132    history 0
133    history
134    history -n
135    history 100
136    history -20
137    history -1 -20
138    history -20 -1
139    history
140    history grep
141    history env
142    history
143    history fc
martyp $
```

你还可以使用 `-r` 选项将此列表反转，如下面的示例所示：

```
martyp $ history -r fc
144    history -r fc
143    history fc
142    history
141    history env
140    history grep
139    history
138    history -20 -1
137    history -1 -20
136    history -20
135    history 100
134    history -n
133    history
132    history 0
131    history
130    more .profile
129    env | grep HIS
128    env
127    exit
126    env | grep HIS
125    more .profile
124    history 1
123    env | more
122    env
121    inv
120    history 1
119    alias
118    history 200
117    history 128 | more
116    history 128
115    history
114    alias history="fc -l"
113    history
112    alias history="fc -l"
111    history
110    fc -l
martyp $
```

能够访问此历史记录列表是 Korn-Shell 的一个很棒的功能。你可以查看你发出的所有命令，包括你的输入错误，格式任选。在下一节中，我们将开始使用历史记录列表中的命令来调用它们。

### 使用 `r` 重新执行命令

你可以使用 `r` 命令重新发出命令。要重新发出上一条命令，只需键入 `r` 即可。在下面的示例中，我发出命令 `history 5` 以查看历史记录列表中的最后五条命令。然后我键入 `r` 以重新发出上一条命令，再次列出最后五条命令：

```
martyp $ history -5
301    whoami
302    pwd
303    more /etc/passwd
304    ps -ef
305    cat .profile
306    history -5
martyp $ r
    history -5
    302 pwd
    303 more /etc/passwd
    304 ps -ef
    305 cat .profile
    306 history -5
    307 history -5
martyp $
```

你可以通过键入 `r`、一个空格以及你想重新发出的命令编号来重新发出特定编号的命令。在下面的示例中，我发出编号为 302 的 `history` 命令：

```
martyp $ history
294    history -5
295    whoami
296    pwd
297    more /etc/passwd
298    ps -ef
299    cat /etc/profile
300    history 5
301    whoami
302    pwd
303    more /etc/passwd
304    ps -ef
305    cat .profile
306    history -5
307    history -5
308    history -5
309    history
martyp $ r 302
    pwd
/home/martyp
martyp $
```

你还可以给出你要重新发出的命令的名称。假设你想重新发出最后一个 `fc` 命令。你只需在 `r` 命令旁给出字母 "f"，即可重新发出以 **f** 开头的最后一个命令，如下面的示例所示：

```
martyp $ history
308    history -5
309    history
310    pwd
311    whoami
312    pwd
313    cat /etc/profile
314    ls
315    fc -l
316    env
317    who
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
martyp $ r f
fc -l
309    history
310    pwd
311    whoami
312    pwd
313    cat /etc/profile
314    ls
315    fc -l
316    env
317    who
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
324    fc -l
martyp $
```

![](img/75f39fc91296b889c0653851accdfd46_332_0.png)

你还可以使用 `r` 命令执行一些替换。如果你早先发出了 `vi` 命令，现在想重新运行 `vi` 但指定不同的文件名进行编辑，你可以替换新的文件名。下面的示例展示了重新发出早先的 `vi` 命令，但现在我们要将编辑过的原始文件名 `.profile` 替换为我们想要编辑的新文件名 `.kshrc`。在这个示例中，我们首先运行 `history` 命令，然后重新发出 `vi` 命令以编辑 `.kshrc`，接着再次运行 `history` 命令以查看我们修改后的 `vi` 命令：

![](img/75f39fc91296b889c0653851accdfd46_333_0.png)

```
martyp $ history
316    env
317    who
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
324    fc -l
325    vi .profile
326    set
327    ls -al
328    env
329    who
330    more /etc/passwd | grep marty
331    history
martyp $ r vi .profile=.kshrc
martyp $ history
318    cat /etc/passwd
319    ls -al
320    history
321    more .profile
322    set
323    history
324    fc -l
325    vi .profile
326    set
327    ls -al
328    env
329    who
330    more /etc/passwd | grep marty
331    history
332    vi .kshrc
333    history
martyp $
```

该命令在命令行上用 `.kshrc` 替换 `.profile`。

这引导我们进入更高级的命令行编辑。你可能想要召回早先发出的命令并使用 `vi` 编辑器命令编辑命令行。下一节涵盖命令行编辑。
