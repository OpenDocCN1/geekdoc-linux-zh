
#!/bin/ksh

#@(#) mktape2disk.sh 从磁盘上的磁带中创建文件

#这将更改名称前缀

NAME="f"

# 从文件 #i 到文件 #j

integer i=1

integer j

# 测试参数

if [ -z "${1}" ]

then

  echo "/nusage: $(basename ${0})<drive_no><#files>\n"

  echo "\t<drive_no>: 磁带驱动器号 (例如 0)"

  echo "\t<#files> : 从磁带中复制的文件数量\n"

  exit

fi

devices=/dev/rmt${1}.1

# 测试参数

if [ -z "${2}" ]

then

  echo "\nousage: $(basename ${0})<drive_no><#files>\n"

  echo "\t<drive_no>: 磁带驱动器号 (例如 0)"

  echo "\t<#files>: 从磁带中复制的文件数量\n"

  exit 1

fi

j=${2}

tctl -f ${device} rewind

if [ $? -ne 0 ]

then

  exit 1

fi

# 这将创建磁带

while [ ${i} -le ${j} ]

do

  echo "从 (${device}) 复制文件 #${i} (共 #${j}) 到磁盘作为 (${NAME}${i})"

  dd if=${device} of="${NAME}${i}" bs=200k

  i=i+1

done

tctl -f ${device} rewind

exit 0

现在你已经创建了脚本，可以如下所示运行它：

`# cd /pub/pmp3250`
`# mktape2disk.sh 0 447 (这将使它从 rmt0 读取 447 个文件)`

- **5.** 你必须创建一个新的 `.toc` 文件。

`# cd /pub/pmp3250 # inutoc . # pg .toc`

- **6.** 然后你必须在 PMP 目录下创建另一个名为 `runme.sh` 的脚本：

```bash
#!/bin/ksh

#@(#) runme.sh 用于 PMP3250

#

INSTP="/usr/sbin/installp"

LOG="/tmp/installp.log"

TEE="/usr/bin/tee"

PATCHDIR=$(pwd)

#

/usr/bin/cp /usr/lpp/info/data/ispaths /usr/lpp/info/data/ispaths.save

#

INFODIR="/usr/lpp/info/$LANG/aix"

/usr/bin/mkdir ${INFODIR} 2>/dev/null

if [ ! -w ${INFODIR} ]

then

  print "\n\tERROR\* 无法（写入）[${INFODIR}。"

  print "\n请卸载 CD 或 NFS 文件系统。\n"

  exit -1

fi
```
*(注：此处原文脚本似乎在此处截断，已按原文内容翻译/保留)*

由于原文提供的文本在结尾处似乎不完整，以下是基于您提供的最后几部分的翻译：

- **5.** 你必须创建一个新的 `.toc` 文件。

`# cd /pub/pmp3250 # inutoc . # pg .toc`

- **6.** 然后你必须在 PMP 目录下创建另一个名为 `runme.sh` 的脚本：

*(注：由于提供的原始文本在 `runme.sh` 的代码块后中断，此处翻译已至原文最后可见内容)*

### 3.2 基础版本的修复和增强级别
如果某个特定问题的修复在 3.2.5 出现之前已经构建，你可以获取旧版本。如果你的修复是在 3.2.5 子系统中首次提供的，那么该修复就是目前存在的唯一版本。

## 在 AIX 中，可以使用超过 8 个字符的密码吗？

你可以创建一个长度大于 8 个字符的密码，但第 8 个之后的所有字符都会被忽略。

如果你正在运行 NIS，你必须小心其他机器上的密码。它们都必须是 8 个字符或少以便与 AIX 兼容。

如果你正在运行 DCE，你可以为密码保存超过 8 个字符，因为 DCE 支持 kerberos，这是一种 X Windows 功能。

## 我可以获得超过 64 个限制的 pty 吗？

SMIT 只允许 64 个 pty，但你可以手动更改 ODM 文件来绕过限制。可以通过以下步骤实现：

`odmget -q"attribute=num and uniquetype=pty/pty/pty"PdAt |`
`sed "s/0-64/0-512/" |`
`odmchange -q"attribute=num and uniquetype=pty/pty/pty" -o PdAt`
`chdev -l pty0 -anum=256 -P`
`reboot`

## 有什么我应该注意的修复？

`sendmail` 和 `xterm` 中存在处理的问题。相关的补丁包指定如下：

### `sendmail`
此修复版本为 U426396

### X11R4 的 `xterm`
此修复版本为 U422575

### X11R5 的 `xterm`
此修复版本为 U425811

## 如何从 ODM 中删除不存在的物理卷？

要做到这一点，你必须使用 `reducevg` 并配合 `pvid` 而不是磁盘名称。`pvid` 实际上位于修改卷组或磁盘上逻辑卷命令时发生的错误消息中。要从数据库中删除丢失的磁盘，只需输入以下命令：

`reducevg -f <pvid>`

## 我无法用 quit、kill 或 stop 杀死进程。该如何杀死它？

你可能运气不佳。如果设备驱动程序中有待处理的 I/O 且驱动程序没有收到信号，你根本无法杀死它。你只能重启以将其从进程列表中移除。

你可以使用以下命令对进程进行跟踪（trace）：

`# echo trace -k $(expr<pid> / 256) | crash | tee stack`

你可以使用该堆栈跟踪来发现系统出了什么问题。（不过你可能需要将其发送给 IBM 系统工程师进行解码。）

## 有办法查看控制台消息吗？

你可以使用 `swcons` 命令将控制台重定向到文件，或者使用 `chcons` 命令将消息永久移动到文件中。

## 如果丢失了 root 密码我该怎么办？

你不需要采取重新加载 AIX 并从磁带恢复一切等激进的操作（最近检查过备份吗？）。只需遵循以下程序：

1. 从启动盘、磁带或 CD 启动。
2. 在 Installation/Maint 菜单中，选择项目 4，“Start a limited function maintenance shell”。
3. 在 `#` 提示下，输入命令：`getrootfs hdisk N`（其中 N 是 `rootvg` 上磁盘的编号）
4. 当返回 `#` 提示时，你将以单用户模式以 root 身份登录。
5.在此处，`cd` 到 `/etc/security` 目录并编辑 `passwd` 文件。在这里你需要删除 root 下方的三行并保存文件。
6. 现在你可以使用 `passwd` 命令为 root 给一个新密码。
7. 现在你所做的就是关机并在正常模式下重启。
8. 写下该密码并将其锁在安全的地方。只要不要忘记把它放在哪里了。

## 运行 chlv 时出现警告。LV 的前 4 KB 没吗？

在原始分区上，前 4 KB 用于存储控制块信息。某些应用程序，特别是像 Oracle 和 Sybase 这样的数据库实际上会覆盖此部分。任何调用 `getlcb` 的命令都会给出警告，但仍会成功，因为控制块信息也存在于 ODM 中。除非你真的想删除这前 4k 并将其替换为 ODM 控制块信息，否则不要运行 `synclvodm`。

## 备份

这是本章较重要的部分之一，因为备份通常等于工作安全！

## 如何进行远程备份？

有几种方法可以实现。第一种（也是目前最简单的）是 `tar` 命令：`tar -b1 -cf - | rsh REMOTEHOST "dd ibs=512 obs=1024 of=/dev/tapedevice"` 因为 `dd` 不会备份远程磁带设备，你必须创建一个脚本来满足你的需求。以下由 Frank Kramer 编写的脚本适用于远程备份：

```bash
#!/bin/ksh

#================================================

# Script : usave.sh

# Author : Frank Kramer

# Date : 92/02/19

# Update : 92/10/29

# Info : the ultimate backup script

# Example: usave.sh /dev/rmt0 - save to local tape

#          usave.sh /save/ - save to local file
```
