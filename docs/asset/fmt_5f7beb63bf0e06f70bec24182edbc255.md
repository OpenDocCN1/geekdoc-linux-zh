
有多个打印条目来定义处理指向同一物理打印机数据的不同方式是可以的。例如，物理打印机可能支持 PostScript 和 HP LaserJet 数据格式，通过设置发送到打印机的某些序列。如果你指定 `/dev/null` 为设备，所有处理都将正确执行，但最终数据将进入“比特桶”——也就是说，通向无处。除了测试配置外，打印到无处很少有用。当你正在设置远程打印机时（即你指定了 `rm` 和 `rp`），请指定 `:ip=`。

除非使用远程打印机，否则不要让该字段为空。如果没有指定设备，打印守护进程会报错。

`If` 字段你指定的任何文件应该已经存在，否则不会记录日志。

`If` 字段输入过滤器是从标准输入接收打印数据并在标准输出生成输出程序。输入过滤器的典型用法是检测 ASCII 文本并转换为 PostScript——也就是说，原始文本是它的输入，PostScript 是它的输出。

当你使用输入过滤器时，打印守护进程不会将溢出数据发送到指定的设备。相反，它运行输入过滤器，并将溢出数据作为标准输入，打印设备作为标准输出。

# 理解 /etc/printcap 中的字段

`printcap` 有许多字段需要描述；后续章节将详细介绍。字段有三种类型：字符串、布尔和数值。表 21.4 描述了最重要的。

表 21.4 `/etc/printcap` 字段
| 字段 | 类型 | 描述 |
|---|---|---|
| `1p` | 字符串 | 指定打印到的设备 |
| `sd` | 字符串 | 指定溢出目录名称 |
| `1f` | 字符串 | 指定输入过滤器名称 |
| `rm` | 字符串 | 指定远程主机名称 |
| `rp` | 字符串 | 指定远程打印机名称 |
| `sh` | 布尔 | 指定此字段以抑制页眉（横页） |
| `sf` | 布尔 | 指定此字段以抑制作业结束换页 |
| `mx` | 数值 | 指定最大打印作业大小（以块为单位） |

# 创建一个测试 printcap 条目

## `mx` 字段
`mx` 字段允许你限制要缓存的打印数据的大小。你指定的数字单位是 `BUSIZE` 块（在 Linux 下为 1K）。如果你指定为零，则取消限制，允许打印作业仅受可用磁盘空间的限制。

注意：该限制是针对溢存数据的大小的，而不是发送到物理打印机的数据量。

如果用户尝试超过此限制，文件将被截断。用户会看到一条消息说 `lpr-fname: copy file is too large`。

对于非 PostScript 打印机，如果你有用户或程序可能会刻意或无意中创建过大的输出，这个限制是很有用的。对于 PostScript 打印机，这个限制完全没用，因为极小的溢存 PostScript 数据就可以产生大量的输出页面。

# 设置 PRINTER 环境变量

你可能想在你的登录脚本中——甚至是默认用户登录脚本中——添加一行来设置 `PRINTER` 环境变量。在 `bash` shell 环境下，一行适当的命令是 `export PRINTER=myprinter`。这可以防止人们在每次提交打印作业时都指定 `-Pprinter`。

要添加更多打印机，只需使用不同的打印机名称重复此过程。记住，你可以有多个 `printcap` 条目，它们都使用同一个物理设备。这样，你可以根据在提交打印作业时对其调用的名称，对同一设备进行不同的处理。

# 创建一个测试 printcap 条目

以下脚本是一个非常简单的输入过滤器——只需在适当的横幅后，将你的输入连接到文件 `/tmp/` 的末尾。在 `printcap` 条目中使用此过滤器，并将 `/dev/null` 指定为打印设备。打印设备永远不会被实际使用，但你必须将其设置为某个值；否则打印守护进程会报错。

```sh
#/bin/sh

# 此文件应该放在打印机的队列目录中，

# 并命名为 input_filter。它应该属于 root 用户，daemon 组，

# 并具有可执行权限 (-rwxr-xr-x)。

echo >> /tmp/
date >> /tmp/
echo >> /tmp/
cat >> /tmp/
```

在下面的 `printcap` 条目中，注意其相当可读的格式以及在所有最后一行使用了续行符 `\`：

```
myprinter:myprinter: \
ip=/dev/null: \
sd=/usr/spool/lp/myprinter: \
lf=/usr/spool/lp/myprinter/errors: \
*
```

# 第 21 章 打印

```
if=/usr/lpd/myprinter/input_filter: \
:mx#$: \
:sh: \
:sf:
```

# 将前面的内容整合在一起

为了将前面的部分整合在一起，以下步骤将指导你如何在 `/dev/lp0` 上设置单台打印机。然后你可以将其扩展到其他打印机。（顺便说一下，执行所有这些操作需要 root 权限。）

- 检查 `lpr`, `lrm`, `lpc`, `lpq` 和 `lpd` 的权限和位置。在本章前面的部分，目录和打印机表 21.2 都列出了正确的设置和目录。

- 为你的打印机创建队列目录（现在命名为 `myprinter`）。确保目录和打印机都属于 root 用户、`daemon` 组，并且对用户和组可写写，对其他人只读 `-rw-rx-x`。使用以下命令：

```
mkdir /usr/spool/lpd
mkdir /usr/spool/lpd/myprinter
chown root.daemon /usr/spool/lpd /usr/spool/lpd/myprinter
chmod ug=rx,ro=/usr/spool/lpd /usr/spool/lpd/myprinter
```

- 在 `/usr/spool/lpd` 目录中创建必要的文件并赋予它们正确的权限和所有者。使用以下命令：

```
cd /usr/spool/lpd/myprinter
touch .seq errs status lock
chown root.daemon .seq errs status lock
chmod ug=rx,ro=.seq errs status lock
```

- 在 `/usr/spool/lpd/myprinter` 目录下创建 shell 输入 `input_filter`。使用之前在“创建一个测试公平条目”节节提供的输入过滤器。确保该文件属于 root 用户、`daemon` 组，并且对任何人可执行。使用以下命令：

```
cd /usr/spool/lpd/myprinter
chmod ug=rx,ro=input_filter
```

- 如果 `/etc/printcap` 文件不存在，则创建它。移除其中所有的条目，并添加之前在“创建一个测试公平条目”节中提供的测试条目。确保该文件属于 root 用户并对其他所有人只读。你可以使用 `chmod` 设置文件权限：`-rw-r--` 或 `644`（八进制）。

- 编辑 `/etc/local` 文件（你可以使用任何 ASCII 编辑器，如 `vi` 或 `emacs`）。在末尾添加行 `/etc/lpd`，这会在每次系统启动时运行打印守护进程。不过现在不需要重启；只需通过 `lpd` 命令运行它即可。

> "通过使用现有文件启动 vi，” 第 395 页

- 执行测试打印

```
ls -l | lpr -myprinter
```

# 整合在一起

8. 使用 `ls` 命令查看 `/tmp`，查找一个名为 `testlp.out` 的文件。它应该包含你的输出。如果没有，检查错误日志。

9. 如果你可以使用 `ls` 命令，编辑 `/etc/printcap` 文件，查找名为 `testlp.out` 的文件。它应该包含你的输出。如果没有，检查错误日志。

10. 使用 `shut -r now` 命令重启系统。

11. 执行测试打印

```
ls -l | lpr myprinter
```
