

Re01759
Re13201
Sting/
VR001187
VR002540
VR002678

现在我将使用 pr 来构建双列输出：
% pr -m src.listing tmp.listing | head -15

Dec 9 13:53 1993    Page 1

calc-help
calc-c
fixit.c
info.c
info.o
message.c

Erik/
Giri/
Garry/
MmsAlive
Re01759
Re13201
Sting/
VR001187
VR002540

管道断开

+ 4. 如果我能自动关闭每个列表页顶部自动包含的空行，那将更有帮助，这是 -f 标志的工作（或者如果你的 pr 版本中 -f 表示分页符，则使用 -t）：
% pr -f
pr -m src.listing tmp.listing | head -15
Dec 9 13:53 1993    Page 1

calc-help
calc-c
fixit.c
info.c
info.o
message.c

Erik/
Giri/
Garry/
MmsAlive
Re01759
Re13201
Sting/
VR001187
VR002540
VR002678
VR002477

管道断开

+ 5. 看起来不错。现在是时候通过将 pr 命令管道到 lpr 命令来执行打印了：
% lpr | lpr
pr -f -m src.listing tmp.listing | head -15 | lpr

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_398_0.png)

# 在 UNIX 环境下打印

`pr` 命令可以用来确保你的打印输出始终整洁且易读。再次，这是一个创建别名的绝佳位置：alias 'pr' | 'lpr' 或 alias 'pr' | 'lprq'。即使不使用任何标志，pr 也会自动在每页顶部添加页码。

## 第 18.4 节：使用打印队列

在个人系统中，打印机直接连接到系统可能会有所帮助，这样使用 PRT（在 DOS 上）或 File|Print（在 Mac 上）打印的任何内容立即打印。遗憾的是，UNIX 并没有拥有私人打印机的奢侈。相反，它在打印队列中处理打印请求，这是一个待打印文件的管理列表。当你将文件发送到打印机时，它会被添加到等待打印的文件队列中。你的请求将位于列表底部，任何随后的打印请求将排在下方。你的打印请求会逐渐移动到列表顶部并打印，而不会中断你之前的打印请求。

有时等待打印输出可能会令人沮丧。然而，与简单允许用户共享一个打印机相比，使用队列系统有一些优点。最大的优点可以使用 `lpr` 命令改变主意，并在浪费纸之前从队列中移除打印请求。`pr` 命令与作业名称配合，你可以通过使用 `ipq` 打印队列来了解它。`lpr` 和 `ipq` 都可以使用 DEFAULT 设置，或者通过 -Pprinter 指定打印机。`ipq` 命令还可以通过通过在命令中添加账户名称来限制输出。

如果你的系统没有 `lpr`，请使用 `cancel` 命令从打印队列中删除项目。`ipstat` 命令是 System V 对 `ipq` 命令的替代，尽管许多站点设置了 `ipq = ipstat` 以让生活方便一点。

要取消，你需要指定打印机名称和作业 ID，如 `ipstat` 输出所示。如果我在硬拷贝打印机上有 37 号请求，可以使用 `cancel -37` 取消该打印。

+ 扫一眼 mathw 队列显示有很多文件等待打印：
  * ipq

```
mathw@server.utech.edu: 驱动未激活
打印已禁用。
```

| Pos | User | Bin | Jobname |
| --- | --- | --- | --- |
| 1 | KOSHHWE | 0104 | 008 KOSHHWE0104 |
| 2 | KOSHHWE | 0104 | 008 KOSHHWE0104 |
| 3 | KOSHHWE | 0104 | 008 KOSHHWE0104 |
| 4 | kleimanj | 0317 | 032 kleimanj0317 |
| 5 | zeta | 0042 | 008 zeta0042 |
| 6 | jharger | 0167 | 008 jarger0167 |
| 7 | jharger | 0167 | 008 jarger0167 |
| 8 | ssinfo | 0353 | 000 ssinfo0353 |
| 9 | fueling | 0216 | 024 fueling0216 |
| 10 | zeta | 0042 | 152 zeta0042 |
| 11 | Hajred | 0142 | 012 hajared0142 |
| 12 | SUJATHA | 0043 | 016 SUJATHA043 |
| 13 | SUJATHA | 0043 | 024 SUJATHA043 |
| 14 | SUJATHA | 0043 | 044 SUJATHA043 |
| 15 | bee | 0785 | 012 bee0785 |
| 16 | bee | 0785 | 026 bee0785 |
| 17 | bee | 0785 | 028 bee0785 |
| 18 | info | 0353 | 004 info0353 |
| 19 | info | 0353 | 000 info0353 |
| 20 | info | 0353 | 000 info0353 |
| 21 | info | 0353 | 004 info0353 |
| 22 | stacysm | 0321 | 000 stacysm0321 |
| 23 | info | 0353 | 000 info0353 |
| 24 | taylor | 0889 | 000 taylor089a |

```
mathlw: 正在传输到 server.utech.edu.
```

队列是空的。我的作业是 24 号，作业名为 taylor09a。图 18.1 解释了队列中的不同字段。

# 图 18.1. lpq 输出格式。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_400_0.png)

打印机已关闭。你可以在 lpq 输出顶部看到驱动未激活打印已禁用。显然，如果打印机被禁用，等待超时是徒劳的。

+ 2. 为了将输出限制为仅我的作业，我指定了我的账户
% lpq taylor
mathlw@server.utech.edu: 驱动未激活
打印已禁用。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_400_1.png)

# 在 UNIX 环境下打印

| Pos | User | Bin | Size | Jobname |
| --- | --- | --- | --- | --- |
| 1 | taylor | 0889 | 004 | taylor089a |

```
mathlw: 正在传输到 server.utech.edu
```

队列是空的。

+ 3. 为了检查另一个打印机的状态，可以使用 -P 标志指定打印机：
% lpq -P2801l
```
b2801l@franklin.utech.edu:
驱动未激活
```

队列是空的。

```
b2801l: 正在传输到 franklin.utech.edu
```

队列是空的。这样好多了。

+ 4. 为了从 mathlw 打印队列中移除我的作业，我只需指定 lpq 输出中的打印作业名称：
% lpr taylor089a
UNIX 执行了我的命令而没有给我已完成的确认，用 lpq 快速检查即可看到情况：
% lpq taylor

```
mathlw@server.utech.edu: 驱动未激活
打印已禁用。
```

队列是空的。

```
mathlw: 正在传输到 server.utech.edu
```

队列是空的。

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_401.png)

我希望 lpq 默认只显示我的作业，否则 lpq 应该报告更有用的信息，比如队列中有其他打印作业。

+ 5. 现在我重新提交我的打印请求，这次到 b2801l：
% pr -f -m src.listing tmp.listing | head -15 | lpr -P2801l

哦，我不想要 -15 截断打印信息。

% lpq -P2801l
b2801l@franklin.utech.edu:
驱动激活；无作业打印

| Pos | User | Bin | Size | Jobname |
| --- | --- | --- | --- | --- |
| 1 | nfsuser | 0058 | 008 nfsuser0058 |
| 2 | nfsuser | 0054 | 008 nfsuser0054 |
| 3 | nfsuser | 0054 | 008 nfsuser0054 |
| 4 | kleimanj | 0317 | 032 kleimanj0317 |
| 5 | zeta | 0042 | 008 zeta0042 |
| 6 | jharger | 0167 | 008 jarger0167 |
| 7 | jharger | 0167 | 008 jarger0167 |
| 8 | ssinfo | 0353 | 000 ssinfo0353 |
| 9 | fueling | 0216 | 024 fueling0216 |
| 10 | zeta | 0042 | 152 zeta0042 |
| 11 | Hajred | 0142 | 012 hajared0142 |
| 12 | SUJATHA | 0043 | 016 SUJATHA043 |
| 13 | SUJATHA | 0043 | 024 SUJATHA043 |
| 14 | SUJATHA | 0043 | 044 SUJATHA043 |
| 15 | bee | 0785 | 012 bee0785 |
| 16 | bee | 0785 | 026 bee0785 |
| 17 | bee | 0785 | 028 bee0785 |
| 18 | info | 0353 | 004 info0353 |
| 19 | info | 0353 | 000 info0353 |
| 20 | info | 0353 | 000 info0353 |
| 21 | info | 0353 | 004 info0353 |
| 22 | stacysm | 0321 | 000 stacysm0321 |
| 23 | info | 0353 | 000 info0353 |
| 24 | taylor | 0889 | 000 taylor089a |

b2801l: 正在传输到 franklin.utech.edu.

队列是空的。为了移除我的打印请求，我使用 iprm：
% iprm taylor89a
"taylor89a" - 未找到。

我犯了一个严重的错误！我需要指定打印机。

% iprm -P2801l taylor89a
现在我可以修复原始命令并正确打印文件：
% pr -f -m src.listing tmp.listing | head -15 | lpr -P2801l

UNIX 提供的打印功能你可能不习惯，特别是那种在接触纸之前停止打印作业的能力。你可以看到将 PRINTER 环境变量设置为你喜欢的打印机是一个好主意，这样可以避免每次打印文件都要输入奇怪的名字。

# 总结

合理定义的别名在未来可以节省你很多烦恼。选择你喜欢的打印机，定义 PRINTER 环境变量以打印到该打印机，并为你创建一个包含你喜欢的所有默认选项的打印别名。你可能会考虑使用别名 pq 来显示在你喜欢的打印机上的打印请求。（这很容易实现）。使用 alias pq 'lpq $LOGNAME*' 或 alias pq 'lpstat -u $LOGNAME*'。你可以通过在命令中加入 grep 来只显示你的打印请求（如果有）：alias pq 'lpq | grep $LOGNAME'。

# 工作坊

工作坊总结了你学习的关键术语，并对本章介绍的内容提出了问题。它还预告了你将在下小时内将学习的内容。

