
```bash
#!/bin/bash
# backup - 一个用于备份目录的程序

BACKUP_DIR="home" # 要备份的目录

STORAGE_DIR="backup" # 存储存档的目录

DATE=$(date +%b%d) # 月份/日期格式的今天日期

if [ -d /$STORAGE_DIR ] && [ -s /$STORAGE_DIR ];
then
  tar czf /$STORAGE_DIR/$DATE-$HOSTNAME-$BACKUP_DIR.tgz
else
  echo "Storage directory may not be mounted."
fi
```

如你所见，这个脚本非常直观。我们将一些参数定义为变量，用于标识受备份影响的文件和目录。我们 own使用这些变量来构建单个备份文件的命名系统。

有两个 `[ ... ]` 结构，通过逻辑与运算符 (`&&`) 连接，以确保 `/backup` 目录存在且不为空。如果目录为空，所有挂载的目录至少包含两个文件。如果 `/backup` 目录不存在或为空，脚本将返回语句 “Storage directory may not be mounted.”，你可以在运行脚本之前有机会手动挂载该目录。

变量 `DATE` 变量被定义为命令 `date +%b%d` 的输出。该命令的第二个组件是一组独立的格式化宏：`+` 表示操作系统后面将紧跟宏，而 `%b` 表示三个字母缩写的月份名称，`%d` 表示月份中的几几。这些数据从系统设置中提取，这是确保你的系统日期时间设置准确的另一个原因。

> 如果你想了解更多关于 `date` 命令的变量，可以在 shell 提示符处运行 `man date` 命令来查看 date 手页。有很多选项。

通过链用 `$DATE`、`$HOSTNAME` 和 `$BACKUP_DIR` 变量，我们为存档创建了一个单独名称，在备份文件列表中清晰地标识它。我们不需要定义 `$HOSTNAME` 变量，因为它已经在全局环境变量中定义了。所有其他变量都需要在脚本内部定义，以便执行脚本命令所需的值。

## 调整脚本以支持多个备份

尽管这个脚本目前已经很有用，但没有理由不多花一点精力。可以重写脚本以使其更灵活，包含更多目录。通过调整脚本，你就不需要为 `/home` 以外的目录编写不同的脚本了。

重写的脚本可能是这种形式：

```bash
#!/bin/bash
# backup - 一个用于备份目录的程序

STORAGE_DIR="backup" # 存储存档的目录

DATE=$(date +%bd) # 月份/日期格式的今天日期

for BACKUP_DIR in "$@"
do
    if [ -d /$STORAGE_DIR ] && [ -s /$STORAGE_DIR ]; then
        tar cfz /$STORAGE_DIR/$DATE-$HOSTNAME-$BACKUP_DIR.tgz /$BACKUP_DIR/*
    else
        echo "Storage directory may not be mounted."
    fi
done
```

此版本的脚本将接受目录列表作为参数，并为每个指定的目录创建备份存档。例如，你可以执行命令

```bash
backup etc home usr
```

脚本将为 `/etc`、`/home` 和 `/usr` 目录创建备份存档，并为每个存档命名特定的标识名称。注意，在调用脚本时不需要提供前导斜杠作为参数，因为脚本被设计为自行提供这些斜杠。在调用时使用斜杠会导致脚本失败。

## 调整脚本以提高未来的灵活性

第二个版本的脚本显然比之前的版本有用得多，因为第二个版本可以扩展为通过一个命令创建多个目录备份。然而，它仍然有点笨拙。为了让它更优雅（这既是一个风格问题，也是为了让操作系统更容易处理代码的问题），你可以再次重写它，如下所示：

```bash
#!/bin/bash
# backup - 一个用于备份目录的程序

STORAGE_DIR="backup" # 存储存档的目录

DATE=$(date +%b%d) # 月份/日期格式的今天日期

backup() {
    if [ -d /$STORAGE_DIR ] && [ -s /$STORAGE_DIR ]
    then
        tar cfz /$STORAGE_DIR/$DATE-$HOSTNAME-$BACKUP_DIR.tgz /$1/*
    else
        echo "Storage directory may not be mounted."
        exit 1
    fi
}
exit 0

for BACKUP_DIR in "$@"
do  
    dobackup $BACKUP_DIR
done
```

在这个版本的脚本中，我们将创建备份文件的命令移动到了名为 `dobackup` 的新函数中。（遍历参数列表的部分）现在根据需要调用该函数。诚然，这更多是一种编程风格而非其他，但这个版本确实比之前的版本要优雅得多。

注意，在这个版本中，我们必须将 `$BACKUP_DIR` 修改为 `$1`，因为 `$BACKUP_DIR` 的值被传递给了函数。

## 调整脚本包含日志

管理员通常负责记录他们的活动日志。如果脚本能够生成某种关于备份是否成功的消息，将非常有帮助。现在，我们可以使用：

```bash
backup etc home usr
```

脚本随后为 `/etc`、`/home` 和 `/usr` 目录创建备份存档，并为每个存档命名特定的标识名称。注意，在调用脚本时不需要提供前导斜杠作为参数，因为脚本被设计为自行提供这些斜杠。在调用时使用斜杠会导致脚本失败。

(注：由于原始文本存在大量重复和 OCR 错误，以上翻译已根据逻辑进行了整合处理)。

# 使用 cron 和 at 在 427 执行脚本

虽然节省时间是考虑自动化的重要原因，但还有另一个重要原因。许多通常由脚本执行的进程都是磁盘密集型或处理器密集型的。在许多用户需要共享系统资源的时间运行备份脚本可能会严重影响每个人的工作，因为处理器必须在极小的时间分片内来回切换，直到所有进程完成。

特别是备份任务，应该只在没有要备份的文件正在被使用时进行。例如，当你的用户都在工作并活跃使用其账户时备份 `/home` 目录，即使过程成功了，也会导致备份错误。在夜间执行备份等任务比这要好得多，因为那时几乎没有人在使用系统；在进行备份之前，你可能先将一或两个用户踢出系统，但如果有 10、20 或 100 个用户，这样做就会困难得多。

## The cron 命令

我们并不特别喜欢在凌晨 2:00 起床来做事，我们怀疑你也不喜欢。幸运的是，Unix 有一个解决方案：使用系统工具 `cron`。魔法命令是

```
crontab -e
```

`crontab` 是你用来调度 `cron` 工具自动运行进程的命令。当你执行 `crontab -e` 命令时，`crontab` 将在你通过 `EDITOR` 环境变量定义的任何编辑器中打开。一旦文件打开，添加一行类似这样的内容：

```
0 2 * * * /path/to/backup <list of directories>
```

其中 `/path/to/backup` 是你的脚本文件的完整路径——在本例中为备份脚本——而 `<list of directories>` 是你希望每次运行 cron 脚本时想要备份的目录列表。

> 提示 如果脚本文件包含在 `PATH` 环境变量列出的某个目录中，你可以在 `crontab` 中省略目录路径。

保存文件并退出编辑器。你应该会看到一条类似“安装新 crontab”的提示，尽管具体的消息会随 Unix 变体而异。这就是你需要做的一切。有了上面的条目，备份将在每天凌晨 2:00 运行，并备份 `<list of directories>` 组件中列出的目录。

## crontab 语法

要使用 Cron 自动化你的系统任务，你需要在 `crontab` 文件中为每个任务创建一个条目。`crontab` 中的条目使用特定的语法：

```
<minute> <hour> <day> <day of week> command
```

你不需要填写条目的每一个字段；如果你想在字段中包含所有可能的值，可以用 `*` 字符替换。因此，时间值 `2 * * * *` 意味着“凌晨 2 点后零分，每月的每一天，每月，每周的每一天”。时间值 `0 2 * * *` 则意味着“凌晨 2 点后零分，二月的每一天”。

由于我们在编写备份脚本时考虑了 `crontab`，因此我们可以通过在 `crontab` 中创建不同的条目来设置不同的调度。例如，我们可以设置像这样的 `crontab` 条目：

```
0 2 * * * backup home root
0 3 * * * backup etc usr/local
0 4,15 * * * backup bin s usr
```
