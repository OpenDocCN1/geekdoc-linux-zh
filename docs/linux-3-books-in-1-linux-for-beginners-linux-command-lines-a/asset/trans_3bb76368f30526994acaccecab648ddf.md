

在当前工作目录中。相反，我们需要首先检查是否存在名为 `$dir` 的文件夹，如果不存在，我们可以创建一个。以下是其实现方法：

```bash
#!/bin/bash
echo -n "Enter the directory name ->"
read dir
if [ -d "$dir" ]
then
    echo "The directory exists"
else
    mkdir $dir
    echo "Directory created"
fi
```

如果你想提升你的 bash 脚本编写技能，请使用 `eval` 来编写上述程序。

## 如何读取文件

Bash 脚本提供了一种读取文件的有效方式。下面的示例演示了如何使用 shell 脚本来读取文件。首先创建一个新文件并将其命名为 `editors.txt`，使其可执行，并添加以下内容：

- 1. Vim
- 2. Emacs
- 3. ed
- 4. nano
- 5. Code

这段代码的结果是这五行会显示在你的屏幕上。

```bash
#!/bin/bash
file='editors.txt'
while read line; do
    echo $line
done < $file
```

## 如何删除文件

在下一个程序中，我们将查看如何在 shell 脚本中删除文件。首先，程序以文件名形式要求用户输入。如果文件存在，它将被删除。在这个例子中，使用 `rm` 命令进行删除：

```bash
#!/bin/bash
echo -n "Enter the filename ->"
read name
rm -i $name
```

当要求输入文件名时，请输入 `editors.txt`，并在询问确认时按 Y 键。文件应该被删除。

## 如何向文件追加内容

下一个 shell 示例向你展示了如何使用 bash 脚本向文件系统中的一个文件追加数据。这将向 `editors.txt` 文件中添加一行额外的内容：

```bash
#!/bin/bash
echo "Before you append the file"
cat editors.txt
echo "6. NotePad++" >> editors.txt
echo "After you append the file"
cat editors.txt
```

至此，你应该已经注意到 bash 脚本正在使用标准终端命令。

## 如何测试文件是否存在

在下一个示例中，我们可以看到如何使用 bash 程序来查找文件是否存在：

```bash
#!/bin/bash
filename=$1
if [ -f "$filename" ]; then
    echo "File exists"
else
    echo "File does not exist"
fi
```

参数是文件名，它直接从命令行传递。

## 如何从 Shell 脚本发送邮件

从 bash 脚本发送邮件非常简单。在下面的示例中，你可以看到执行此操作的一种方法：

```bash
#!/bin/bash
recipient="admin@example.com"
subject="Greetings"
message="Welcome to UbuntuPit"
mail -s $subject $recipient <<< $message
```

这将向指定的收件人发送电子邮件，并包含指定的主题行和消息。

## 如何解析日期和时间

在下一个脚本示例中，你可以看到如何使用脚本来处理时间和日期。我们使用 `date` 命令获取所需信息，脚本将进行必要的解析：

```bash
#!/bin/bash
year=`date +%Y`
month=`date +%m`
day=`date +%d`
hour=`date +%H`
minute=`date +%M`
second=`date +%S`
echo `date`
echo "Current Date is: $day-$month-$year"
echo "Current Time is: $hour:$minute:$second"
```

保存并运行该程序以查看其工作原理，并且也请从你自己的终端运行 `date` 命令。

运行此程序以查看其工作原理。此外，尝试从你的终端运行 `date` 命令。

## 如何使用 Sleep 命令

你可以使用 `sleep` 命令让 shell 脚本在每条指令之间暂停。这对许多事情都有用，包括当你想要执行系统级任务时。在下一个示例中，可以看到 `sleep` 命令在 shell 脚本中的工作方式：

```bash
#!/bin/bash
echo "How long should you wait?"
read time
sleep $time
echo "Waited for $time seconds!"
```

程序停止最后一条指令的执行，持续时间由用户指定。

## 如何使用 Wait 命令

我们可以使用 `wait` 命令来暂停 bash 脚本系统进程。下面的示例详细演示了这在 bash 脚本中是如何工作的：

```bash
#!/bin/bash
echo "Testing the wait command"
sleep 5 &
pid=$!
kill $pid
wait $pid
echo $pid was terminated.
```

保存并运行程序，亲自查看其工作原理。

## 如何显示最近更新的文件

有时，你可能需要定位最近更新的文件 – 这在特定操作中可能需要。下方你可以看到一个简单的程序，展示如何在 bash 中使用 `awk` 命令来执行此操作。它将列出当前工作目录中最近更新或最近创建的文件之一。

```bash
#!/bin/bash
ls -lrt | grep ^- | awk 'END{print $NF}'
```

将此代码复制到文件中并运行它，以查看其工作原理。

## 如何添加批量扩展名

在下面的程序中，我们为指定目录内的每个文件应用了一个自定义扩展名。为了演示目的，请创建一个全新的目录并在其中放入几个文件。在我的文件夹中，我有五个文件。每个文件名都是 `test` 后跟 0 到 4 之间的数字。为了演示，脚本将在每个文件末尾添加 `.UP` – 你可以添加任何想要的扩展名，只需确保相应地修改脚本。

```bash
#!/bin/bash
dir=$1
for file in `ls $1/*`
do
    mv $file $file.UP
done
```

一个重要提示 – 你不应该尝试从常规目录运行此脚本，只能从测试目录运行。你还必须提供一个包含文件目录名的命令行参数 – 当前工作目录应使用点（.）表示。

## 如何打印文件或目录的数量

下面的脚本将使用 Linux 提供的 `find` 命令来查找指定目录中有多少文件夹或文件。你要查找文件的目录名称应从命令行传递。

```bash
#!/bin/bash
if [ -d "$@" ]; then
    echo "Files found: $(find "$@" -type f | wc -l)"
    echo "Folders found: $(find "$@" -type d | wc -l)"
else
    echo "[ERROR] Please retry with another folder:"
    exit 1
fi
```

如果你指定的目录不可用，系统将要求你尝试使用其他目录。如果你没有权限访问指定目录，也会出现相同的消息。

## 如何清理日志文件

在下一个演示中，你可以看到 shell 脚本如何在实际生活中轻松使用。我们将删除存储在名为 `/var/log` 的目录中的所有日志文件。如果你想清理不同的日志，只需更改持有目录的变量：

```bash
#!/bin/bash
LOG_DIR=/var/log
cd $LOG_DIR

cat /dev/null > messages
cat /dev/null > wtmp
echo "Logs cleaned up."
```

重要提示 – 此 shell 脚本必须以 root 身份运行。

## 使用 Bash 备份你的脚本

Shell 脚本提供了一种强大且有效的目录和文件备份方式。在下一个示例中，你可以看到如何备份过去 24 小时内修改过的所有文件和目录。Linux 的 `find` 命令用于此目的。

```bash
#!/bin/bash

BACKUPFILE=backup-$(date +%m-%d-%Y)
archive=${1:-$BACKUPFILE}

find . -mtime -1 -type f -print0 | xargs -0 tar rvf "$archive.tar"
echo "Directory $PWD backed up in archive file \"$archive.tar.gz\"."
exit 0
```

备份成功完成后，文件名和目录名将被打印出来。

## 如何查看用户是否为 Root

在下一个示例中，你可以看到如何使用 bash 脚本来查看用户是否为 root：

```bash
#!/bin/bash
ROOT_UID=0
if [ "$UID" -eq "$ROOT_UID" ]
then
    echo "You are root."
else
    echo "You are not root"
fi
exit 0
```

输出完全取决于运行脚本的用户。Root 用户通过 `$UID` 进行匹配。

## 如何从文件中移除重复行

处理文件可能需要大量时间，并且可能会严重降低管理效率。最耗时的任务之一是在文件中查找重复行，但一个简短、简单的 shell 脚本可以解决问题：

```sh
#!/bin/sh

echo -n "Enter the Filename-> "
read filename
if [ -f "$filename" ]; then
    sort $filename | uniq | tee sorted.txt
else
    echo "No $filename in $PWD...try again"
fi
exit 0
```

此脚本将检查指定文件的每一行，并删除任何重复项。然后这些行被放入一个新文件中，保留原始文件不变。

## 如何进行系统维护

如果你想让生活更轻松一些，你可以使用一个小 shell 脚本来升级你的系统，而不是全部手动操作。以下是执行此操作的一个示例：

```bash
#!/bin/bash
```

