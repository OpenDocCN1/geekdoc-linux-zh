
`mkcdsl`命令的设计目的不仅仅是创建 CDSL，而是创建可维护的 CDSL。正如我们之前所说，CDSL 是一个符号链接。当然，它是一个特殊的符号链接，其中路径中夹入了`"{memb}"`变量，但它仍然是一个符号链接。换句话说，你可以使用`ln`命令配合`"-s"`开关来创建 CDSL，如上一节所述，但我们尚未告诉你的原因是为什么使用`ln`命令是个坏主意。简单来说，`ln`命令不会记录 CDSL 是否曾经被创建。因此，如果你为应用程序创建了一个 CDSL，以便每个成员都可以写入其自己的

```shell
# mkcdsl -i $C && grep $C /var/adm/cdsl_admin.inv
0                 34              00000             0              120777    2/26/01 010
./myFirstCDSL     cluster/members/(member)/myFirstCDSL
```

## 6.4.3 CDSL 和 mv(1) 命令

在使用`mv`命令时，如果涉及 CDSL，则需要特别小心。`mv`命令不会跟随链接，因此会用文件替换链接。在独立配置中，这可能无关紧要，也可能很重要（当然，`cdslinvchk`会返回错误）；然而，在集群中，这将产生不可预测的（并且可能不太愉快）结果。

为说明此问题，创建一个文件（我们称之为 `"mover"`）并将其移动到上一节中创建的链接。

```shell
# cat > mover
la dee da
sweedledeae
sweedledum
^D
```

```shell
# ls -lid mover myFirstCDSL | awk '{ print $1,$10,$11,$12 }'
2112 myFirstCDSL -> cluster/members/(member)/myFirstCDSL
2894 mover
```

```shell
# mv mover myFirstCDSL; ls -lid myFirstCDSL | awk '{ print $1,$10,$11,$12 }'
2894 myFirstCDSL
```

你可以通过序列号看出该文件是同一个文件，但更重要的是，CDSL 不见了！建议在涉及 CDSLs 时使用`cp(1)`命令而不是`mv`命令。如果你不小心删除了 CDSL，不用担心，只需使用`mkcdsl`命令重新创建即可。

## 6.4.4 CDSL 和 Shells

Korn shell ’88 (`ksh`) 和 Korn shell ’93 (`dtksh`) 不会像 Bourne shell (`sh`) 或 C shell (`csh`) 那样显示符号链接。Korn shell 会在可能的情况下在输出中隐藏符号链接，而其他 shell 则显示实际所在的路径。表 6-5

## Shell 对 CDSLs 的响应

| sh (`/sbin/sh`, `/usr/bin/sh`) | csh (`/usr/bin/csh`) | ksh (posix) (`/usr/bin/ksh`, `/usr/bin/posix/sh`) | dtksh (ksh93) (`/usr/dt/bin/dtksh`) | tcsh (`/usr/local/bin/tcsh`) | bash (`/usr/local/bin/bash`) | zsh (`/usr/local/bin/zsh`) |
|---|---|---|---|---|---|---|
| `# cd /.local..`<br>`# pwd`<br>`/cluster/members/member0` | `# cd /.local..`<br>`# pwd`<br>`/cluster/members/member0` | `# cd /.local..`<br>`# pwd`<br>`/.local..` | `# cd /.local..`<br>`# pwd`<br>`/.local..` | `# cd /.local..`<br>`# pwd`<br>`/cluster/members/member0` | `# cd /.local..`<br>`# pwd`<br>`/.local..` | `# cd /.local..`<br>`# pwd`<br>`/.local..` |

**表 6-5：Shell 对符号链接的响应** 说明了每个 shell 在使用 CDSL 作为目录更改当前工作目录时的响应。表中还显示了来自 Tru64 UNIX 开源 CD 的另外三种替代 shell。

请注意，`bash`和`zsh` shell 与`ksh`类似，而`tcsh`与`csh`相似。

另外，你也可以使用`/usr/bin`目录中的`pwd`命令。

## 6.5 扩展进程 ID

你可能会想，“扩展进程 ID 与 CDSLs 和文件系统层次结构有什么关系？” 其实没有什么关系，但我们认为你可能会对这条信息感兴趣，因此选择在这里提供。

进程 ID 从 Tru64 UNIX 版本 5.0 开始扩展为 32 位整数（尽管最大值为 2147483647，实际上是 31 位）。在独立环境中，你不会看到任何明显差异；例如 PID 0 仍然是 `[kernel_idle]`，PID 1 仍然是`init`守护进程。在 TruCluster 环境中，PID 结构被定义为提供一组唯一的进程 ID（524288 PIDs/成员），定义如下：

1. 进程 ID（19 位）
2. 成员 ID（8 位）
3. 序列号（4 位） – 目前未使用。
4. 符号位（1 位） – 此位保留供将来使用。

PID 结构定义在`/usr/include/sys/types.h`中。每个成员的初始 PID 如表 6-6 所示。

让我们更仔细地查看集群上`init`守护进程的 PID，以探索集群中的 PID 结构如何影响 PID。在`member1`上，`init`的 PID 将为 524289。

```
# sysconfig -q generic memberid
generic:
memberid = 1
```

```
# ps -eo pid,command | grep "/sbin/init*" | grep -v grep
524289 /sbin/init -a
```

### 按 Member ID 的 PID 范围

`memberid × 2^19`

| Member ID | PID | Member ID | PID | Member ID | PID |
|---|---|---|---|---|---|
| 1 | 524288 | 22 | 11534336 | 43 | 22544384 |
| 2 | 1048576 | 23 | 12058624 | 44 | 23068672 |
| 3 | 1572864 | 24 | 12582912 | 45 | 23592960 |
| 4 | 2097152 | 25 | 13107200 | 46 | 24117248 |
| 5 | 2621440 | 26 | 13631488 | 47 | 24641536 |
| 6 | 3145728 | 27 | 14155776 | 48 | 25165824 |
| 7 | 3670016 | 28 | 14680064 | 49 | 25690112 |
| 8 | 4194304 | 29 | 15204352 | 50 | 26214400 |
| 9 | 4718592 | 30 | 15728640 | 51 | 26738688 |
| 10 | 5242880 | 31 | 16252928 | 52 | 27262976 |
| 11 | 5767168 | 32 | 16777216 | 53 | 27787264 |
| 12 | 6291456 | 33 | 17301504 | 54 | 28311552 |
| 13 | 6815744 | 34 | 17825792 | 55 | 28835840 |
| 14 | 7340032 | 35 | 18350080 | 56 | 29360128 |
| 15 | 7864320 | 36 | 18874368 | 57 | 29884416 |
| 16 | 8388608 | 37 | 19398656 | 58 | 30408704 |
| 17 | 8912896 | 38 | 19922944 | 59 | 30932992 |
| 18 | 9437184 | 39 | 20447232 | 60 | 31457280 |
| 19 | 9961472 | 40 | 20971520 | 61 | 31981568 |
| 20 | 10485760 | 41 | 21495808 | 62 | 32505856 |
| 21 | 11010048 | 42 | 22020096 | 63 | 33030144 |

**表 6-6：按成员的 PID 范围**

![](img/a0df85c2e542a8d6c913113908553aa4_165_0.png)

**图 6-6：PID 结构图示**
