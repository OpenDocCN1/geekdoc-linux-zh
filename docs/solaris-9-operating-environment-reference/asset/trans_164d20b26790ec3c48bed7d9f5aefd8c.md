

# stty 1355

```
saveterm="$(stty -g)    # 保存终端状态
stty (new settings)         # 设置新状态
#                             # ...
stty $saveterm               # 恢复终端状态
```

由于 -a 格式定义较为宽松，保存和恢复设置的脚本应使用 -g 选项。

# 示例
以下示例显示了在未指定选项时 stty 命令的输出。

```
castle$ stty
ispeed 89376 baud; ospeed 89360 baud; -parity cstopb hupcl loblk
rows = 37; columns = 80; ypixels = 491; xpixels = 570;
quit = <undef>; erase = #hw; switch = <undef>
-inpck -istrip icnl -ixany ixoff onlcr
echo echo echoe echochtl iexten
cast$
```

# 环境变量
请参考 environ(5) 以获取以下影响 stty 执行的环境变量的描述：LC_CTYPE、LC_MESSAGES 和 NLPATH。

# 退出状态
0 成功。
>0 发生错误。

# 属性
请参考 attributes(5) 以获取以下属性的描述：

```
/usr/bin/stty
Attribute Type    Attribute Value
Availability       SunWxcsu
```

```
/usr/xpg4/bin/stty
Attribute Type    Attribute Value
Availability       SunWxcu4
```

# 相关阅
tabs(1), ioctl(2), write(2), getwidth(3C), attributes(5), environ(5), ldterm(7), termio(7), termiox(7)

# sum — 打印文件的校验和和块计数

# 语法
```
/usr/bin/sum [-r] [file...]
/ucb/sum [file...]
```

# 描述
该命令计算并打印指定文件的 16 位校验和以及文件中 512 字节块的数量。通常用于检查传输线路中的错误。
注意 — sum 和 /ucb/sum (见 sum(1)) 返回不同的校验和。

# 选项
- -r 一种用于计算校验和的备用（依赖机器的）算法。

# 操作数
- file 文件的路径。如果没有指定文件，则使用标准输入。

# 示例
以下示例显示了文件 kookurra-1 的校验和。

```
castle% sum kookurra-1
23823 1 kookurra-1
```

# 使用
参考 largefile(5) 以了解 sum 在遇到文件大于或等于 2GB 字节时的行为。

# 环境变量
参考 environ(5) 以获取以下影响 sum 执行的环境变量描述：LC_TYPE、MESSAGES 和 NLPATH。

# 退出状态
- 0 成功。
>0 发生错误。

# 属性
参考 attributes(5) 以获取以下属性的描述：

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmesu |
| CSI | Enabled |

# 相关阅
cksum(1), sum(1), wc(1), attributes(5), environ(5), largefile(5)

# 诊断
在大多数设备上，读取错误与文件结束符无法区分；检查块计数。

# sun — 获取处理器类型真值

# 语法
/usr/bin/sun

# 描述
参考 machid(1)。

# suspend — 停止当前 shell 的内置函数

# 语法
- sh, csh, 和 ksh 

# 描述
Bourne 和 Korn Shell：停止当前 shell 的执行（如果是登录 shell 则不停止）。C Shell：停止 shell 就像发送了 ^Z 信号。此函数经常用于停止由 su 的 shell。

# 属性
参考 attributes(5) 以获取以下属性的描述：

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmesu |

# 1358

# 相关阅
```
csh(1), kill(1), ksh(1), sh(1), su(1), attributes(5)
```

# symorder — 重排符号列表

# 语法
```
/ccs/bin/symorder [-s] objectfile
```

# 描述
symorder 命令用于 SunOS 4，专门为了减少从 vunix 获取符号的开销。该命令不再适用，因为内核符号项通过 /dev/ksym 动态获取。此脚本为需要维护跨多种操作系统的脚本的开发者提供了便利。

# 退出状态
symorder 的退出状态为 0。

# 属性
参考 attributes(5) 以获取以下属性的描述：

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWtool |

# 相关阅
```
nlist(3), attributes(5), ksyms(7)
```

# sysV-make — 维护、更新和重新生成程序组

# 语法
```
/usr/lib/svr4.make [-f makefile] [-eikrst] [names]
```

# 描述
sysV-make 命令是 make 的原始版本。如果环境变量 USVR4_MAKE 被设置，则 make 命令将调用此版本的 make。该版本允许程序员维护、更新和重新生成计算机程序组（通常是程序）。源码控制 (SCCS) 文件、makefile 和 s.makefile 会按顺序尝试。如果你未指定 -f 选项，则采用标准输入。

# sysV-make
make 仅当其依赖项新于目标时才更新目标。目标的先决文件会被递归地添加到目标列表中。缺失的文件被视为过时。你可以在 makefile 中包含以下列表中的指令来扩展选项。在 makefile 中作为目标使用的指令如下：

- DEFAULT：如果必须制作文件但没有显式命令或内置规则，则使用与名称相关的命令。
- IGNORE：同于 -i 选项。
- PRECIOUS：按下退出键时不要删除 PRECIOUS 条目的依赖项。
- SILENT：同于 -s 选项。
> 注意 - 某些命令返回状态不当；使用 -i 或命令行前缀 (-) 来克服这一困难。包含冒 和 @ 字符的文件名不起。直接由 shell 执行的命令（特别是 cd(1)）在 make 的换行间无效。

# 选项
- - e：环境变量覆盖 makefile 内部赋值。
- f makefile：指定文件名。
- i：忽略调用命令返回的错误码。
- k：如果失败，放弃当前条目的工作，但继续其他不依赖于该条目的分支。
- n：打印命令但不执行它们。即使行以 @ 开头也打印。
- q：打印完整的宏定义和目标描述。
- r：不使用内置规则。
- s：不打印命令。
- t：触摸文件而不是执行命令。

# 创建 make
make 仅当其依赖项新于目标时才更新目标。目标的先决文件会被递归地添加到目标列表中。缺失的文件被视为过时。你可以在 makefile 中包含以下列表中的指令来扩展选项。在 makefile 中作为目标使用的指令如下：

