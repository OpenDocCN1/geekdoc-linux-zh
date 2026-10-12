
```bash
#!/bin/Bash
#
## SCRIPT: generic_rsync.Bash
## AUTHOR: Randy Michael
## DATE: 1/18/2007
## REV: 1.0
## PURPOSE: 这是一个通用的 shell 脚本，使用 rsync 复制文件。
#
# set -n # 取消注释以检查脚本而不执行
# set -x # 取消注释以调试此脚本
#
# REV:
############################################################
## 定义文件和变量
############################################################

## 定义源目录和目标目录
SOURCE_FL="/scripts"
DEST_FL="yogi:/scripts"

############################################################
## 主体开始
############################################################

## 开始 rsync 复制
```

**列表 1-22 generic_rsync.Bash**

```bash
rsync -avz "$SOURCE_FL" "$DEST_FL"
## generic_rsync.Bash 结束
```

如你所见，这个脚本并没有多少内容。我们分别将源和目标目录定义为 `SOURCE_FL` 和 `DEST_FL`。我们在 `rsync` 语句中使用这些变量：

```bash
rsync "$SOURCE_FL" "$DEST_FL"
```

该 `rsync` 命令将递归地将本地 `/scripts` 目录中的所有文件和子目录（注意源路径结尾的斜杠）传输到 `yogi` 服务器的 `/scripts` 目录，并使用压缩来减少传输的数据量。注意结尾斜杠避免了在目标位置创建第二个目录。

## 捕获大于 MB 的文件列表

如果你想快速查找大文件，请使用以下语法：

```bash
## 在 $SEARCH_PATH 搜索大于 $MB_BYTES 的文件
HOLFILE=/tmp/largefiles.list
MB_BYTES=$1
SEARCH_PATH=$pwd
find $SEARCH_PATH -type f -size +"$MB_BYTES" > $HOLFILE
```

注意在命令的 `-size` 参数中，文件大小前面有一个加号 (`+`)，这种组合指定大于 `$MB_BYTES`（以字节计算）的文件，而不是按块。

## 捕获用户的按键

在大型商店中，至少偶尔需要监控用户的操作。你可能需要审计任何具有系统 root 权限的用户或其他管理类型账户（如 `oracle`）的按键。承包商可能会带来特殊风险。通常当新应用程序引入环境时，会有一两个承包商会活跃一段时间，用于安装、故障排除和对人员进行产品培训。列表 1-23 显示的代码使用了 `script` 命令来捕获所有按键。

```bash
TS=$(date +%m%d%H%M%S) # 文件时间戳
THISHOST=$(hostname|cut -f1) # 主机名
LOGDIR=/var/log # 日志目录
LOGFILE=${LOGDIR}/${THISHOST}.${TS}.log # 日志文件
## 使用 script 命令记录所有按键
script -a $LOGFILE
## 运行命令...
exit # 退出 script 模式
```

*修正：根据原文片段翻译如下：*

```bash
TS=$(date +%m%d%H%M%S) # 文件时间戳
THISHOST=$(hostname|cut -f1) # 主机名
LOGDIR=/var/log # 日志目录
LOGFILE=${LOGDIR}/${THISHOST}.${TS}.log # 日志文件
## 使用 script 命令捕获所有按键
script -a $LOGFILE
```

```bash
## 记录所有按键
```

## 脚本执行的示例

############################################################

## 获取日志

############################################################

## 查看记录的按键：

```bash
cat $LOGFILE
```

## 第 1 章 脚本快速上手与回顾 51

## 自动化 FTP 文件传输

你可以使用在此文档（here document）中编写一个 FTP 文件传输脚本。其基本思路如下：

```bash
ftp -i -v n wilma <<END_FTP

user randy mypassword

lcd /scripts/download

cd /scripts

get auto_ftp_xfer.sh

bye

END_FTP
```

## 使用 rsync 复制数据

我们使用 `rsync` 的方式与使用 `rcp` 和 `scp` 非常相似。这三种方法都需要源文件和目标文件或目录，并且有递归命令行开关，允许我们保存文件权限、链接、所有权等，还可以递归地复制目录结构。几个示例是学习如何使用 `rsync` 的最佳方法。让我们从这个 `rsync` 语句开始：

```bash
rsync myscript.Bash yogi:/scripts/
```

这将把当前目录下的文件 `myscript.Bash` 传输到 `yogi` 服务器上的 `/scripts` 目录。现在，如果 `myscript.Bash` 文件已经存在于 `yogi` 服务器的 `/scripts` 目录中，则将使用 `rsync` 远程更新协议通过仅发送源和目标文件之间的差异来更新文件：

```bash
rsync -avz yogi:/scripts/data /scripts/tmp
```

该 `rsync` 语句将递归地将 `yogi` 机器 `/scripts/data` 目录下的文件和目录传输到本地机器的 `/scripts/tmp` 目录。`-a` 选项表示归档模式，它保留权限、所有权、符号链接、属性等，并在传输过程中指定递归复制。`-z` 选项指定在传输中使用压缩，以减少传输的数据量。请注意，此示例将在本地机器上创建一个新目录 `/scripts/tmp/data`。`-v` 选项指定为详尽输出模式（verbose mode）。

```bash
rsync -avz yogi:/scripts/data/ /scripts/tmp
```

注意源路径结尾的斜杠：`yogi:/scripts/data/`

这个结尾斜杠会改变 `rsync` 的行为，消除在目标位置创建额外的目录（上一个示例产生了：`/scripts/tmp/data`）。源端的结尾斜杠让 `rsync` 复制目录的内容，而不是复制目录本身及其所有内容。

```bash
rsync -avz /scripts/data /scripts/tmp
rsync -avz /scripts/data/ /scripts/tmp
```

如你通过这两个示例所示，你可以复制本地文件也可以复制远程文件。注意，本地文件复制没有通过 `主机名:` 符号指定主机名。

## 简单的通用 rsync Shell 脚本

一个用于 `rsync` 的简单通用 shell 脚本仅包含定义指向我们想要复制的文件/目录的变量，以及单行的 `rsync` 语句。请查看列表 1-22，我们将在末尾介绍细节。

```bash
#!/bin/Bash

#
## SCRIPT: generic_rsync.Bash
## AUTHOR: Randy Michael
## DATE: 1/18/2007
## REV: 1.0
## PURPOSE: 这是一个通用的 shell 脚本，使用 rsync 复制文件。
#
# set -n # 取消注释以检查脚本而不执行
# set -x # 取消注释以调试此脚本
#
# REV:
############################################################
## 定义文件和变量
############################################################

## 定义源目录和目标目录
SOURCE_FL="/scripts"
```
