
```
1314-taylorj?:760:Mary Taylor:/users/taylorj/users/local/lib/tcsh

1419-taylorj?:375:518:Dave Taylor:/users/taylorj/datayour/bin/csh

1547-taylorj?:208:James Taylor:/users/taylorj/bin/csh

1988-taylorj?:568:Taylor:/users/taylorj/bin/csh

2133-taylorj?:8692:Melanie Taylor:/users/taylorj/bin/csh

3405-taylorj?:Dave Taylor:/users/taylorj:/bin/csh
```

这是一个极好的例子，说明默认分隔符为命令输出增加了难以置信的困惑。通常，行号后面跟着冒号没有问题，但在密码文件（已经充斥着冒号）中，这会令人困惑。将此输出与指令 4 中使用 `grep` 命令获得的输出进行比较，看看发生了什么变化。

你可以看到我关于 `Taylor` 创建账户的理论是错的。如果距离密码文件的远近是账户在相似时间分配的指标，那么没有一个 `Taylor` 在同一周内创建账户。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_183_0.png)

这些关于 `grep` 基础用法的示例仅触及这一强大且复杂的命令用法的一角。尝试使用 `grep` 探索你的文件系统以搜索特定模式。

有了通配符，你现在可以尝试使用 `grep` 的 `-l` 标志，回想一下，它指示包含特定模式的文件名，而不是打印匹配模式的行。如果我进入我的电子邮件归档目录 `--Mail`，我可以轻松地使用 `grep -i chicago Mail/` 命令搜索所有包含 `Chicago` 的文件（此处原文为 Mail-）。尝试使用 `grep -l` 搜索你家目录中所有文件中的模式。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_183_1.png)
![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_183_2.png)

## 通配符与正则表达式

## 任务 9.5：对于复杂表达式，尝试 egrep

有时正则表达式无法定位你所寻找的内容。也许你正在寻找包含一个或多个模式的行。这时 `egrep` 命令就证明是有帮助的。该命令的名字来源于“expression”（表达式），它拥有的比 `grep` 更强大的表示法，见表 9.3。

egrep 表格表示法：

| 表示法 | 含义 |
| :--- | :--- |
| `\|` | a 或 b |
| `()` | 表达式 |
| `^` | 行首 |
| `$` | 行尾 |
| `.` | 任意字符 |
| `[xy]` | 集合中的任意字符 |
| `[^xy]` | 不在集合中的字符 |
| `*` | 0 次或多次 |
| `+` | 1 次或多次 |
| `?` | 0 次或 1 次 |

1. 现在我使用 `egrep` 来搜索模式，效果如下：

```bash
% grep /etc/passwd

taylorj?:2048:1375:James Taylor:/users/taylor:/bin/csh
taylorj?:760:1375:James Taylor:/users/usr/local/bin/tcsh
taylord?:375:518:Dave Taylor:/users/taylor:/usr/local/lib/msh
taylorjr?:203:1022:James Taylor:/users/taylorjr:/bin/csh
taylorrj?:668:1042:Robert Taylor:/users/taylorrj:/bin/csh
taylorm?:862:1508:Melanie Taylor:/users/taylormx:/bin/csh
taylorj?:1989:1412:Dave Taylor:/users/taylor:/bin/csh
```

## 第 9 小节

4. 我可以修改我的别名（`alias`），但要让引号正确显示简直是一场噩梦。直接编写这个简单的 shell 脚本会容易得多：

```
% cat bin/wrongs
# wrongs - 显示文件中常见误用单词的列表
cat $* | \
awk '{for (i=1;i<=NF; i++) print $i}' | \
fgrep -F ".wrongs"
```

为了让它生效，我需要使用 C shell 别名删除现有的 `wrongwords` 别名，为 shell 脚本添加执行权限，然后执行 `rehash` 以确保 C shell 在被请求时能找到该命令：

```
% alias wrongwords
% chmod +x bin/wrongwords
% rehash
```

现在已经可以使用了：

```
% wrongwords sample3
insure
afect
```

5. `fgrep` 命令还可以从列表中排除单词。如果你一直在使用 `myspell` 命令，你会很快地发现该程序对缩写词或你在写作中使用的某些其他拼写正确的单词一无所知。这时 `grep` 就能成为一个得力的爱国者了。列出一个你常用的、没有拼写错误但被报告为错误的单词列表：

```
% alias myspell '*spell\* | fgrep -v -f $HOME/.dictionary'
% cat $HOME/.dictionary
BBS:
FAX
Taylor
Utech
ygote
```

现在 `spell` 变得更有帮助了：

```
% spell newsample

FAX
illiterate
Literacy
letteracy
illiterate
Papert
pre
rithmetic
Rs
Taylor
Utech
ygote

% myspell newsample

illiterate
Literacy
```
