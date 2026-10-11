
`-xr-xr-x 3 root sys 1948 Jan 1970 r03`

`-xr-xr-x 3 root sys 2689 Jan 1970 r04`

`-xr-xr-x 3 root sys 257444 Sep 1998 r05`

`-xr-xr-x 2 root bin 9412 Jan 1998 r06`

`-xr-xr-x 1 root root 195300 Sep 1998 sh`

`lrw-rw-rw- 1 root root 13 Nov 27 14:40 su /usr/bin/su`

`-xr-xr-x 1 root bin 478308 Sep 1998 us_static`

`-xr-xr-x 1 root bin 288544 Sep 1998 sulogin`

`-xr-xr-x 1 root bin 3138 Jan 1970 swadmin`

`-xr-xr-x 1 root bin 29716 Jan 1970 swapadded`

`-xr-xr-x 1 root bin 435004 Jan 1998 uadmin`

`-xr-xr-x 1 root bin 213408 Sep 1998 umount`

`-xr-xr-x 1 root sys 3292 Jan 1970 umountall`

`-xr-xr-x 1 root bin 193152 Sep 1998 uname`

`martyp ls -r`

`typed escape* to get seven files`

`rc0 rc1 rc2 rc3 rc5 rc6 rc8`

`typed escape3_ to get third word`

1) `rc0`

2) `rc1`

3) `rc2`

4) `rc3`

5) `rc5`

```
```

因为上一个命令包含了 `ls` 命令，所以第三个单词不是 `rc2` 而是 `rc1`，它是上一个命令中的第一个条目。

表 22-1 总结了示例中使用的命令和匹配模式：

## 表 22-1 ksh 中的命令和路径补全

| 单词或命令（在每个单词前输入 escape） | 结果 |
|---|---|
| `wordescape=` | 显示以该单词开头的文件名编号列表。 |
| `wordescape*` | 将单词替换为所有匹配的文件。 |
| `wordescape\` | 将单词替换为以该单词开头的第一个文件名。 |
| `command wordescape=` | 显示以该单词开头的文件名编号列表。 |
| `command wordescape*` | 将单词替换为所有匹配的文件。 |
| `command wordescape_` | 在光标位置插入上一个命令的最后一个单词。 |
| `command wordescape_3` | 在光标位置插入上一个命令的第三个单词。 |

## 文件名扩展

在 `ksh` 的日常操作中，你必须执行许多与文件名相关的工作，包括编写处理文件名的 shell 脚本。对文件名扩展进行概述将有助于你在编写 shell 脚本之前熟悉这一主题。

表 22-2 列出了一些常见的文件名扩展和模式匹配：

![](img/6969df54e516231f8e64fd1177ac1127_1456_0.png)

## 表 22-2 文件名扩展和模式匹配

| 字符 | 示例 | 描述 |
|---|---|---|
| `*` | 1) `*.c` | 匹配零或多个字符 |
| `?` | 2) `conf.?` | 匹配任意单个字符 |
| `[list]` | 3) `conf[list]` | 匹配列表中的任意字符 |
| `[lower-upper]` | 4) `file[5-6]` | 匹配范围内的任意字符 |
| `{str1,str2,str3}` | 5) `ux*{700,300}` | 扩展带有这些内容的 str |
| `~` | 6) `-a ~` | 家目录 |
| `~username` | 7) `-a ~` | 用户的家目录 |

以下是表 22-2 中示例的更详细描述：

- 1. 列出目录下所有以 ".c" 结尾的文件：
`$ ls *.c`
`conf.c`

- 2. 查找名为 "conf" 的目录下所有扩展为一个字符的文件：
`$ ls conf.?`
`conf.c conf.o`

- 3. 列出名为 "conf" 的目录下所有扩展为 "c" 或 "o" 的文件：
`$ ls conf.{c,o}`
`conf.c conf.o`

![](img/6969df54e516231f8e64fd1177ac1127_1457_0.png)

## KornShell 简介

- 4. 列出名称相似但字段覆盖范围的文件：
`$ ls file[5-6]`
`file5.txt file6.txt`

![](img/8e64fd1177ac1127_1458_0.png)

- 5. 列出所有以 "ux" 开头且扩展为 "700" 的文件：
`$ ux*,{700,300}`
`uxfile700 uxfile300`

- 6. 列出家目录下的文件，可以使用 `~`：
`$ ls -a ~`
`.cshrc .login .shrc .exrc .profile .rc.org`

- 7. 列出用户家目录下的文件，可以：
`$ ls -a ~username`
`.history under.des .login trail.txt xtra.part .chshrc .login.org .cshrc.org .profile Mail .exrc .shrc.org opt`

在操作 `ksh` 和编写 shell 脚本时，这些技术都非常有用，因此你需要熟悉文件名扩展。

![](img/1458_1.png)

## 重定向（I/O 重定向）

UNIX 的设置使得命令通常从键盘获取输入（通常称为标准输入），并将输出发送到屏幕（通常称为标准输出）。命令还将错误信息发送到屏幕。你并不总是希望标准输入、输出和错误都进入标准输出。你有许多控制权可以覆盖这些默认。这被称为重定向。表 22-3 显示了许多常见的重定向形式。

如 22-3 所示，要将命令的输出从标准输出重定向到文件，使用 `>`。这在几乎所有情况下都有效。如果你设置了一个名为 `noblober` 的环境变量，那么重定向到现有文件将不起（我们稍后会介绍环境变量）。`noblober` 不允许重定向重写现有文件。如果你像下面所示尝试重写现有文件 `/tmp/processes`，你会收到文件已存在的消息：

```
# ps -ef > /tmp/processes

/tmp/processes: File exists
```
