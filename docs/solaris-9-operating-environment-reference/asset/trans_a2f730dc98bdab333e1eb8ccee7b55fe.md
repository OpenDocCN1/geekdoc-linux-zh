

# 1210

# SCCS

deletit [-s] [-y[comment]]

等于执行 sccs delta 然后再执行 sccs edit。deletit 子命令会提交一个 delta 并再次检出该文件，但保持该文件的当前工作副本不变。

- -s 不报告 delta 增号或统计信息。
- -y[comment] 省略 delta 注释的注释。如果省略 -y，delta 会提示输入注释。空注释将导致 delta 的注释字段为空。

delget [-s] [-y[comment]]

执行 sccs delta 然后再执行 sccs get，以提交一个 delta 并检索生成的新版本的只读副本。关于 -s 和 -y 的描述，请参阅 deletit 子命令。sccs 对参数列表中指定的所有文件执行 delta 命令，然后对所有文件执行 get。如果在执行 delta 过程中发生错误，则不执行 get。

delta [-s] [-y[comment]]

提交待处理更改。读取文件被检出期间引入的逐行更改。检出文件的人的有效用户 ID。请参阅 sccs-delta(1)。关于 -s 和 -y 的描述，请参阅 deletit 子命令。

diffs [-C] [-I] [-cdatetime] [-rsid] diff-options (/usr/ccs/bin/sccs) diffs [-C] [-I] [-cdatetime | -c date-time] [-rsid | -r sid]

diff-options [-y] 以 diff(1) 格式将已检出编辑的文件工作副本与 SCCS 历史中的某个版本进行比较。默认使用最近提交的版本。deletit 子命令接受与 diff 相同的选项。

任何 -r, -c, -i 和 -ot 选项都会传递给 get 子命令。任何 -1, -s, -e, -f, -h 和 options 都会传递给 diff 命令。-C 传递给 diff 作为 -c。-I 传递给 diff 作为 -i。

-cdate-time [/usr/ccs/bin/sccs -c date-time | -cdate-time (/usr/xpg4/bin/sccs)]

使用指定日期和时间之前提交的最新版本进行比较。date-time 的格式为 yy[mm[dd[hh[[mm][ss]]]]]。省略的单位默认为其最大可能值；例如，-c7502 等于 -c750228232959。

# SCCS 1211

```
-rsid (/usr/ccs/bin/sccs)
-r sid | -rsid (/usr/xpg4/bin/sccs)
```

使用与指定 delta 对应的版本进行比较。

检索用于编辑的文件版本。提取你可写的文件版本；在 SCCS 子目录中创建一个 p.file 作为文件历史的锁，这样其他人就无法检出该版本或检索未展开形式的 ID 关键字。edit 接受与 get 相同的选项。ID 关键字列表及其定义请参阅 sccs-get(1)。

与 create 类似，但省略了最后的 sccs get。如果你在初始化历史文件后立即执行 sccs edit，则可以使用此子命令。

```
-rsid (/usr/ccs/bin/sccs)
-r sid | (/usr/xpg4/bin/sccs)
```

修订一个（叶节点）delta。从 SCCS 历史中删除指定的 delta，在目录中保留当前版本的可写副本。此子命令用于合并不需要审计记录的部落更新，或修订 delta 注释。你必须跟上 -r 选项以指定要删除的 delta 的 sid。指定的 delta 必须是该分支中最新的（叶节点）delta。请谨慎使用，因为它不会留下差异的审计轨迹（尽管之前的副本保留在历史文件中）。

```
get {-ekmps} {-Gnewname} {-cdate-time} [-r{sid}] (/usr/ccs/bin/sccs)
get {-ekmps} [-G newname] [-c date-time] [-cdate-time] [-r sid |-rsid] (/usr/xpg4/bin/sccs)
```

从 SCCS 历史中检索一个版本。默认情况下，此副本是最新版本的只读副本；ID 关键字以展开形式存在。ID 关键字列表及其定义请参阅 sccs-get(1)。

- -e
- -G newname 使用用户名作为检索版本的名称。Solaris 9 版本中新增的功能。
- -k 检索一个用于编辑的版本。与 sccs edit 相同。
- -m 在每行前加上该行被添加的 delta sid。
- -p 将检索的版本输出到标准输出。将通常去往标准输出的报告（delta ID 和统计信息）重定向到标准错误。

# 1212

# SCCS

不报告版本号或统计信息。

```
-s
-cdate-time (/usr/ccs/bin/sccs)
-c date-time | -cdate-time (/usr/xpg4/bin/sccs)
```

检索 date-time 参数指定的日期和时间之前提交的最新版本。date-time 的格式为 yy[mm[dd mmss]]]]。如果未指定 sid，则检索指定文件的最新 sid。

```
-r[sid]
-r sid | -rsid
```

检索与指定 sid 对应的版本。

```
help-code sccs-command
```

提供有关 SCCS 诊断的更多信息。help 显示 SCCS 诊断消息所显示的错误的简要解释。如果你提供了命令名称，help 会打印用法提示。help 还可以识别关键字。请参阅 sccs-help(1)。

```
info [-b] [-username] (/usr/ccs/bin/sccs)
info [-b] [-username] (/usr/xpg4/bin/sccs)
```

显示正在编辑的文件列表，包括检出的版本号、要提交的版本、持有锁的用户名、文件检出的日期和时间。

```
-b忽略分支。
-u{username} (/usr/ccs/bin/sccs) -u | -U (/usr/xpg4/bin/sccs)
```

仅列出由...检出的文件。当你指定用户名时，仅列出该用户检出的文件。对于 /usr/xpg4/bin/sccs，-U 选项等于 -u current-user。

```
prs [-el] [-cdate-time] [-rsid] (/usr/ccs/bin/sccs)
prs [-el] [-cdate-time] [-r sid | -rsid] (/usr/xpg4/bin/sccs)
```

检索每个命名文件的完整历史。等于 sccs get -m。使用（显示）delta 表或文件的其他部分。请参阅 sccs-prs(1)。

```
-e
```

显示所有比 -r 指定的 delta 更早（如果未指定，则显示所有 delta）的 delta 表信息。

# SCCS

# 1213

- -l 显示比 -c 指定之后（包括指定的）的 delta 信息。

-cdate-time (/usr/ccs/bin/sccs)
-c date-time | -cdate-time (/usr/xpg4/bin/sccs)

指定指定的 delta 和日期-time 参数之后提交的最新 delta。date-time 的格式为 yy{dd [hb][mm[ss]]}}。

- -rsid (/usr/ccs/bin/sccs)
-r sid | -rsid (/usr/xpg4/bin/sccs)

指定指定的 sid

prt [-y] 显示 delta 表，但省略该字段（关于此字段请参阅 sccsfile(4)）。请参阅 sccs-prt(1)。

- -y 显示最新的条目。格式为每个文件单行；方便在 awk(1) 或 sed(1) 管道中使用。

rmdel -rsid (/usr/ccs/bin/sccs)
rmdel -r sid (/usr/xpg4/bin/sccs)

从历史文件中删除指定的 delta。该 delta 必须是该分支中最新的（叶节点）delta。请参阅 sccs-rmdel(1)。

sact
显示 SCCS 文件的活动状态。请参阅 sccs-sact(1)。

ccsdiff -old-sid -new-sid 使用 diff 比较指定的 sid（delta）。请参阅 sccs-ccsdiff(1)。

tell [-b] [-u username] (/usr/ccs/bin/sccs)
tell [-b] [-u username] [-U] (/usr/xpg4/bin/sccs)

显示当前检出的文件列表，每行一个。

- -b
-u[username] (/usr/ccs/bin/sccs)
-u [username] | -U (/usr/xpg4/bin/sccs)

仅列出...检出的文件。当你指定用户名时，仅列出该用户检出的文件。对于 /usr/xpg4/bin/sccs，-U 选项等于 -u current-user。

und撤销最近的编辑或 get -e，并将工作副本恢复到之前的状态。undedit 撤销自文件检出以来的所有待处理更改。

unset
与 undedit 相同。请参阅 sccs-unset(1)。

val
验证历史文件。请参阅 sccs-val(1)。

what 显示二进制（对象）或文本文件中包含的展开 ID 关键字字符串。更多信息请参阅 what(1)。

# 示例

以下示例检出一个文件，编辑它，然后再次提交。

```
castle% sccs edit program.c
1.1
new delta 1.2
14 lines
castle% vi program.c
ynyour editing session
castle% sccs delget program.c
comments? clarified cryptic diagnostic
1.2
3 inserted
2 deleted
12 unchanged
1.2
15 lines
castle%
```

以下示例定义了命令路径名的根部分。

```
castle% sccs -d/usr/src/include get stdio.h
/usr/ccs/bin/get /usr/src/include/SCCS/s.stdio.h
castle%
```

以下示例重新定义了驻留子目录。

```
castle% sccs -pprivate get include/stdio.h
/usr/ccs/bin/get include/private/s.stdio.h
castle%
```

