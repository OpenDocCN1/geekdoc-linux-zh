

注意：虽然我们创建了一个指向某处的 CDSL，但该处指向无处。

```sh
# wc -l myFirstCDSL
wc: myFirstCDSL : No such file or directory
```

这不是一个错误，而是符号链接的特性。你可以通过简单地将一个文件复制到 /myFirstCDSL 来解决这种情况。

```sh
# cp .profile myFirstCDSL && wc -l myFirstCDSL
       74 myFirstCDSL
```

接下来，让我们在根目录（/）下创建一个目录，以演示使用 “-c” 选项的 mkcdsl 命令。“-c” 选项会将文件（或在这种情况下的目录）从其位置复制到成员特定的位置，同时在文件的位置留下 CDSL。

```sh
# CcdlDir && mkdir $C && mkcdsl -c $C && fin $C
cluDir -> cluster/members/(memb)/cluDir
```

你可以使用 “-n” 选项查看 mkcdsl 将会做什么（而不实际执行）。

```sh
# mkcdsl -n anotherCDSL
mkcdsl would: ln -s cluster/members/(memb)/anotherCDSL /anotherCDSL
```

## 6.4.2   维护 CDSLs

有两条命令可用于在系统上维护 CDSLs：

- `cdslinvchk(8)`
- `mkcdsl(8)`

### 6.4.2.1   使用 cdslinvchk (8) 命令

cdslinvchk 命令通过搜索位于 /usr/.smdb/ 中的子集清单文件（*.inv 文件）和 /var/adm/cdsl_admin.inv 文件来验证系统中安装的所有 CDSLs 是否存在。如果命令检测到任何错误，它会将它们写入位于 /var/adm 中的 cdsl_check_list 文件。cdslinvchk 命令仅检查缺失的 CDSLs；它不会重新创建缺失的链接。要重新创建缺失的 CDSL，请使用 mkcdsl 命令。

```sh
# cdslinvchk
Successful CDSL inventory check
```

让我们删除一个 CDSL 来演示错误情况。

```
# mv /etc/rc.config /etc/rc.config.cdsl
```

重新运行 CDSL 清单检查程序。

```
# cdslinvchk
Failed CDSL inventory check. See details in /var/adm/cdsl_check_list
```

检查错误日志的内容。

```
# cat /var/adm/cdsl_check_list
Expected CDSL: ./etc/rc.config -> ../cluster/members/{memb}/etc/rc.config
An administrator or application has removed this CDSL.
```

该如何纠正？使用本章前面讨论过的 mkcdsl 命令。

```
# mkcdsl /etc/rc.config
```

重新运行 cdslinvchk 程序以确保我们已正确地将所有内容重新组合。

```
# cdslinvchk
Successful CDSL inventory check
```

不要忘记删除保存的链接。

```
# rm /etc/rc.config.cdsl
```

### 6.4.2.2 使用 mkcdsl(8) 命令

mkcdsl 命令的设计目的不仅仅是创建 CDSL，而是创建可维护的 CDSL。正如我们之前所说，CDSL 是一个符号链接。当然，它是一个特殊的符号链接，其中路径中夹入了 "{memb}" 变量，但它仍然是一个符号链接。换句话说，你可以使用 ln 命令配合 "-s" 开关来创建 CDSL，如上一节所述，但我们尚未告诉你的原因是为什么使用 ln 命令是个坏主意。简单来说，ln 命令不会记录 CDSL 是否曾经被创建。因此，如果你为应用程序创建了一个 CDSL，以便每个成员都可以写入其自己的

```shell
# mkcdsl -i $C && grep $C /var/adm/cdsl_admin.inv
0                 34              00000             0              120777    2/26/01 010
./myFirstCDSL     cluster/members/(member)/myFirstCDSL
```

## 6.4.3  CDSL 和 mv(1) 命令

在使用 mv 命令时，如果涉及 CDSL，则需要特别小心。mv 命令不会跟随链接，因此会用文件替换链接。在独立配置中，这可能无关紧要，也可能很重要（当然，cdslinvchk 会返回错误）；然而，在集群中，这将产生不可预测的（并且可能不太愉快）结果。

为说明此问题，创建一个文件（我们称之为 “mover”）并将其移动到上一节中创建的链接。

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

你可以通过序列号看出该文件是同一个文件，但更重要的是，CDSL 不见了！建议在涉及 CDSLs 时使用 cp(1) 命令而不是 mv 命令。如果你不小心删除了 CDSL，不用担心，只需使用 mkcdsl 命令重新创建即可。

## 6.4.4  CDSL 和 Shells

Korn shell ’88 (ksh) 和 Korn shell ’93 (dtksh) 不会像 Bourne shell (sh) 或 C shell (csh) 那样显示符号链接。Korn shell 会在可能的情况下在输出中隐藏符号链接，而其他 shell 则显示实际所在的路径。表 6-5

