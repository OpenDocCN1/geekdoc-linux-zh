
rsync -avz yogi:/scripts/data /scripts/tmp

此 `rsync` 语句将递归地将 yogi 机器 `/scripts/data` 目录中的所有文件和目录传输到本地机器的 `/scripts/tmp` 目录。`-a` 选项激活归档模式，该模式会保留权限、所有权、符号链接、属性等，并在传输中定义递归复制。`-z` 选项指定在传输中使用压缩，以减少传输的数据量。注意，这将在本地机器上创建一个新目录 `/scripts/tmp/data`。`-v` 选项指定详细模式。现在来看下一个 `rsync` 示例：

rsync -avz yogi:/scripts/data/ /scripts/tmp

注意源路径末尾的斜杠：`yogi:/scripts/data/`
这个末尾斜杠改变了 rsync 的行为，消除了在目标上创建额外目录的行为（上一个示例产生了：`/scripts/tmp/data`）。
源端的末尾斜杠允许 `rsync` 复制目录内容，而不是复制目录本身及其所有内容。

rsync -avz /scripts/data /scripts/tmp

rsync -avz /scripts/data/ /scripts/tmp

从这两个示例中可以看出，我们既可以在本地复制文件，也可以远程复制。注意，本地文件复制没有通过主机名表示法指定主机名。

# 通用 rsync Shell 脚本

一个简单的、通用的 rsync Shell 脚本仅包含定义一些指向我们想要复制的文件/目录的变量，以及单行的 `rsync` 语句。请查看列表 7-1，我们将在最后介绍细节。

```bash
#!/bin/Bash

#

## SCRIPT: generic_rsync.Bash

## AUTHOR: Randy Michael

# DATE: 11/18/2007

## REV: 1.0

# PURPOSE: 这是一个使用 rsync 复制文件的通用 脚本

# set -n # 取消注释以检查脚本语法而不执行

# set -x # 取消注释以调试此脚本

## REV LIST:

#

############################################################

## 在此处定义文件和变量

############################################################

# 定义源和目标文件/目录

SOURCE_FL="scripts"

DESTIN_FL="booboo/scripts"

############################################################

## 主程序开始

############################################################

## 开始 rsync 复制

rsync -avz "$SOURCE_FL" "$DESTIN_FL"

# generic_rsync.Bash结束
```

# 列表 7-1 generic_rsync.Bash 脚本

如你所见，这个 Shell 脚本并不复杂。我们分别将源和目标文件/目录定义为 `SOURCE_FL` 和 `DESTIN_FL` 变量。接下来我们在 `rsync` 语句中使用这些变量，如下：

rsync -avz "$SOURCE_FL" "$DESTIN_FL"

此 `rsync` 命令将递归地将本地 `/scripts/` 目录（注意源末尾的斜杠）中的所有文件和子目录传输到 booboo 服务器上的 `/scripts` 目录，并使用压缩来减少传输的数据量。注意末尾斜杠避免了在目标上创建第二个 `scripts` 目录：`/scripts/scripts`。

# 第二部分 程序员、测试人员和分析师的脚本

现在让我们来看一些示例脚本，分别在目录结构级和文件系统级复制数据。

# 使用 rsync 复制多个目录

你是否需要一种技术来将一个或多个目录结构复制到一个或多个远程机器？如果是的话，这一节就是你的救星！当你看到 `rsync` 远程更新协议在文件已于目标上的速度时，你会发现使用 `rsync` 复制数据高效得令人难以置信。我们已经查看了通过在后台启动每个 `rsync` 会话（由 `rsync_command &` 指定）来并行循环使用 `rsync` 多个目录结构的方法。随着 `rsync` 进程的进行，我们将在进程级别监控每个 `rsync` 会话，向用户提供详细的反馈。这种反馈对于任何带有用户交互的长运行过程或程序都是至关重要的。

对于此脚本，我们需要一个列表来存放我们要复制的每个顶层目录的名称。在本示例中，我们将此列表重命名为 `rsync_directory_list.lst`。由于我们要遍历此列表，脚本期望每行一个目录列表。示例 `rsync_directory_list.lst` 所示于列表 7-2。

```
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
# 列表 7-2 示例
# 该文件被 generic_DIR_rsync_copy.Bash 使用
# 该 shell 脚本用于定义顶层目录结构
# 使用 rsync 复制到一个或多个远程服务器。
# 脚本期望完整路径（必须以正斜杠
# 开头，例如：/directory/path。可以以正斜杠
# 结尾但不是）。
/directory/path1
/directory/path2
/directory/path3
/directory/path4
/directory/path5
```

## 第 7 章 使用 rsync 高效复制数据 225

```bash
verify_copy ()
{
# set -x
MYLOGFILE=$(WORK_DIR)/verify_rsync_copy.log
>$MYLOGFILE
ERROR=0
# 将此循环封装起来，以便通过函数底部的单一赋值
# 将输出重定向到日志文件中
{
# 为验证日志文件写入表头
echo -e "\nrsync copy verification starting $THIS_HOST 机器($s)$MACHINE_LIST\n\n" >$MYLOGFILE
for M in $MACHINE_LIST
do
  for DS in $(cat $DIR_LIST_FILE)
  do
    LS_FILES=$(find $DS -type f)
    for FL in $LS_FILES
    do
      LOC_FS=$(ls -l -1 $FL | awk '{print $5}' 2>&1)
      REM_FS=$(ssh $M ls -l $FL | awk '{print $5}' 2>&1)
      echo "Checking File: \t$LOC_FS"
      echo -e "Local $THIS_HOST size:\t$LOC_FS"
      echo -e "Remote $M size:\t$REM_FS"
      if [ "$LOC_FS" -ne "$REM_FS" ];
      then
```
