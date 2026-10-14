
**目的：** `ed` 是一个简单、无修饰的文本编辑器。

**示例：** `ed`。（如需关于 `ed` 的更多信息，请查看第 7 章）。

## egrep

**目的：** `egrep` 在文件中搜索模式。当它找到指定的模式时，会打印匹配的行。

**示例：** `egrep "I am bored" myfile.txt`。这会在 `myfile.txt` 文件中搜索字符串 `I am bored`。（如需更多关于 `egrep` 和其他文本扫描工具的信息，请查看第 7 章）。

## elm

**目的：** `elm` 是流行的 UNIX 邮件客户端。

**示例：** `elm`。这会启动 `elm` 邮件读取器。（如需了解更多关于 `elm`，见第 17 章，“电子邮件”。）

## file

**目的：** `file` 报告指定文件的数据类型。

**示例：** `file *`。这里是一个 `file` 报告示例：

| Mail: | directory |

| News: | directory |

| b: | commands text |

| cig: | directory |

| dead.letter: | ascii text |

| mail: | directory |

| mytester | ascii text |

| public_html: | directory |

## find

**目的：** `find` 将目录层次结构中查找文件。

**示例：** `find . -name *gif`。这将在主目录或其下方查找所有 `.gif` 扩展的文件。这里是一个 `find` 报告示例：

```
./.public_html/assets/images/dot_clear.gif
./public_html/assets/images/link3a.gif
./public_html/assets/images/link2a.gif
./public_html/assets/images/link1a.gif
./public_html/assets/images/link5a.gif
./public_html/assets/images/link6a.gif
./public_html/assets/images/link4a.gif
./public_html/assets/images/now30_button.gif
./public_html/assets/images/Sun.gif
./public_html/assets/images/javalogo52x88.gif
```

## finger

**目的：** `finger` 将报告用户信息。

**示例：** `finger bwagner`。这会提取我上目前可用的所有信息。这里是输出：

```
Login name: bwagner              In real life: Bill Wagner
Directory: /home/bwagner        Shell: /sbin/sh
Since Aug 5 19:38:44 on pts/7 from tradersh.pacific.net
Mail read Wed Aug 5 19:39:09
```

## fsck

**目的：** `fsck` 检查文件系统。

**示例：** `fsck /dev/dsk/c0t1d0`

## ftp

**目的：** `ftp` 在主机之间传输文件。

**示例：** `ftp tradersh.pacific.net`。

## 第 7 部分

## gcc

**目的：** `gcc` 是 C 编译器。

**示例：** `gcc main.c -o program`。将 `main.c` 编译为名为 `program` 的执行文件。

## gawk

**目的：** `gawk` 是 `awk` 的 GNU 实现。

**示例：** `gawk '{print $1}' myfile.txt`。这打印文件的第一列。

## grep

**目的：** `grep` 在文件中搜索模式。

**示例：** `grep "I am bored" myfile.txt`。这会在 `myfile.txt` 文件中搜索字符串 `I am bored`。

## gzip

**目的：** `gzip` 压缩文件。

**示例：** `gzip myfile.txt`。这将 `myfile.txt` 压缩为 `myfile.txt.gz`。

## halt

**目的：** `halt` 停止系统。

**示例：** `halt`。

## head

**目的：** `head` 输出文件的几行。

**示例：** `head -n 10 myfile.txt`。这显示 `myfile.txt` 的前 10 行。

## hostname

**目的：** `hostname` 将打印机器名。

**示例：** `hostname`。

## ispell

**目的：** `ispell` 是一个交互式拼写检查器。

**示例：** `ispell myfile.txt`。

## kill

**目的：** `kill` 将终止一个进程。

**示例：** `kill 1234`。这终止进程 `1234`。

## ksh

**目的：** `ksh` 是 Korn shell。

**示例：** `ksh`。这会启动 Korn shell。

## last

**目的：** `last` 报告用户登录的日期和时间。

**示例：** `last -3`。这显示我最后登录的三次。

## mail

**目的：** `mail` 允许你发送和接收电子邮件。

**示例：** `cat myfile.txt ; mail bwagner.`。这会将 `myfile.txt` 的内容通过邮件发送给我。（`mail` 也可以通过交互模式使用，只需输入 `mail` 命令即可。要了解更多关于 `mail` 的信息，请参阅第 18 章。）

## man

**目的：** `man` 是 UNIX 参考手册的接口。这些手册通常被称为 man 页（man pages）。

**示例：** `man mail.`。这将调用 `mail` man 页。（要了解更多关于 `man` 的信息，请参阅第 15 章“帮助！”）

## mkdir

**目的：** `mkdir` 创建指定的目录。

**示例：** `mkdir bozo-mail.`。这将创建一个名为 `bozo-mail` 的目录。（要了解更多关于 `mkdir` 的信息，请参阅第 6 章。）

## more

**目的：** `more` 每次显示一屏文件内容。

**示例：** `more myfile.txt.`。这将一次屏显示 `myfile.txt` 的内容。这便于查看超过 40 行的长文件。

## mount

**目的：** `mount` 用于挂载和卸载文件系统。

**示例：** `mount /dev/fd0 /mnt/floppy.`。这将第一个软驱器挂载到 `/mnt/floppy` 目录。

## mv

**目的：** `mv` 重命名文件。

**示例：** `mv myfile.txt yourfile.txt.`。这将 `myfile.txt` 重命名为 `yourfile.txt`。（要了解更多关于 `mv` 的信息，请参阅第 6 章。）

## 录 A > 命令参考

## nroff

**目的：** `nroff` 为行打印机或终端屏幕格式化文本文件。

**示例：** `nroff myfile.txt`。这产生整洁且格式良好的输出。

## passwd

**目的：** `passwd` 可用于更改密码。

**示例：** `passwd`（系统将提示你进行更改）。

## paste

**目的：** `paste` 合并文件或输出的行。

**示例：** `who | awk '{print $1}' | paste - -`。这获取当前用户 ID 并以列格式打印它们。两个 `-` 符号指定列布局。

## perl

**目的：** `perl`（实用提取和报告语言）是一种强大的文本扫描语言。

**示例：** `perl -e 'print "Hello World\n";`。这将显示以下消息：

Hello World

`perl` 可用于编写复杂的程序。然而，这些程序通常不在命令行输入。相反，它们存储在 `perl` 脚本文件中（包含许多 `perl` 命令的文本文件）。

## pico

**目的：** `pico` 是某些 UNIX 版本（特别是 Linux）上提供的免费文本编辑器。

**示例：** `pico myfile.txt`。这启动 `pico` 来编辑 `myfile.txt`。（要了解更多关于 `pico` 的信息，请参阅第 8 章“打开、编辑和保存文件”。）

349

## 第7部分 参考

## pine

**示例：** `pine.`。这启动 `pine` 邮件阅读器。（要了解更多关于 `pine` 的信息，请参阅第 17 章。）

## ping

**目的：** `ping` 检查其他主机是否活跃。

**示例：** `ping 207.171.0.111`。这是一个来自 Sparc 的示例 `ping` 报告：

```
207.171.0.111 is alive
```

在所有其他系统上，报告可能看起来不同。这是一个示例：
