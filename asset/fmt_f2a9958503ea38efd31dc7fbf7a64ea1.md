
Resulting archive file is: `/archive/archive140828.tar.gz`
```
$ ls /archive
archive140828.tar.gz Files_To_Backup
$
```

你可以看到脚本捕获到目录不存在，`/home/Does_not_exist`。它让你这在配置文件的某一行，并继续构建列表进行存档。你的数据现在已安全地存档在 tar 包中。

# 创建小时存档脚本

如果你处于文件变化频繁的高容量生产环境，每日存档可能不够。如果你想将存档频率增加到每小时，你需要考虑另一个项目。

当每小时备份文件并尝试使用 `date` 命令为每个 tar 包设置时间戳时，情况可能会变得糟糕。处理如下所示 tar 包目录是繁琐的：

`archive010211023.tar.gz`

与其将所有文件放在同一个文件夹中，不如为你的存档文件创建一个层级结构。图 24.1 演示了这一点。

![](img/f4b0da3f699eed06c5e37a566e1b4a6756_0.png)

**图 24.1** 创建存档目录

存档目录包含每个月的目录，使用月份数字作为目录名称。每个月的目录又包含每天的文件夹（使用日期数值作为目录名称）。这允许你为每个 tar 包设置时间戳，并将它们放在相应的日期目录中。

首先，必须创建 `/archive/hourly` 目录，并对其设置适当权限。记得在本章早期，Archivers 组已被授予在该区域创建存档的权限。因此，新创建的目录必须更改其主组和组权限：

```bash
$ sudo mkdir /archive/hourly

[sudo] password for Christine:

$

$ sudo chgrp Archivers /archive/hourly

$

$ ls -ld /archive/hourly/

drwxr-xr-x. 2 root 4096 Sep 2 09:24 /archive/hourly/

$

$ sudo chmod 775 /archive/hourly

$

$ ls -ld /archive/hourly/

drwxrwxr-x. 2 root 4096 Sep 2 09:24 /archive/hourly/
```

设置好目录后，用于小时存档的 `Files_To_Backup` 配置可以移动到新目录：

```bash
$ cat Files_To_Backup
/usr/local/Production/Machine_Errors

/home/Development/Simulation_Logs

$

$ mv Files_To_Backup /archive/hourly
```

等等，我注意到提示提供的 OCR 文本在关于小时脚本的部分有些杂乱。我将根据提供的文本片段重构逻辑。（自我修正：提示要求处理提供的 OCR 文本。末尾关于小时脚本的提供的 OCR 文本实际上是碎片化/重复的我会将清理提供的文本，修复如 `techo` 为 `echo` 以及 `drxr` 为 `drwxr` 等明显错误。）

实际上，查看提供的源码：
- `techo` -> `echo`
- `drxr` -> `drwxr`
- `$Files_To_Backup` -> `Files_To_Backup`（上下文暗示变量或路径）

让我们提供所提供文本的清理版本。

# 备注

如果你在白天运行 `Hourly-Archive.sh` 脚本，当小时数为单位数时，你的存档文件名为将只有三个数字。例如，如果你在凌晨 1:15 运行脚本，存档文件的名称为 `archive115.tar.gz`。如果你希望存档文件名始终为四位数字，请修改脚本行 `TIME=$(date +%k%M)`，在 `%k` 之后添加一个零 `0`，任何单位数的小时都会通过前导零补齐为两位。这样，`archive115.tar.gz` 将被重命名为 `archive0115.tar.gz`。

为了测试，脚本被第二次运行，以查看它与现有目录 `/archive/hourly/09/02` 是否存在问题：

```
$ date +%k%M

1017

$ ./Hourly_Archive.sh

Starting archive...

Archive completed

Resulting archive file is: /archive/hourly/09/02/archive1017.tar.gz

$ ls /archive/hourly/09/02/

archive1011.tar.gz archive1017.tar.gz

$
```

与现有目录没有问题！脚本再次运行良好并创建了存档文件。它现在准备好用于 cron 定时任务表了。

# 管理用户账户

管理用户账户不仅仅是添加、修改和删除账户。你必须考虑安全问题、保留工作的需求以及对账户的准确管理。这可能是一项耗时的任务。这里是编写脚本实用工具真正节省时间的另一个实例！

# 获取所需的函数

删除账户是比较复杂的账户管理任务。删除账户时，至少需要执行四个独立的动作：

- 1. 获取要删除的正确用户用户名。
- 2. 杀死系统上当前运行的属于该账户的所有进程。
- 3. 确定系统中属于该账户的所有文件。
- 4. 移除用户账户。

很容易漏掉某一步。本节中的 shell 脚本工具可以帮助你避免此类错误。

# 获取正确的账户名

账户删除过程的第一步是最重要的：获取要删除的正确用户用户名。由于这是一个交互式脚本，你可以使用 `read` 命令（见第 14 章）来获取账户名。如果脚本用户离开并让问题悬挂，你可以使用 `read` 命令的 `-t` 选项，在给脚本 60 秒时间回答问题后超时：

```
echo "Please enter the username of the user "
echo -e "account you wish to delete from system: \c"
read -t 60 ANSWER
```

```
while [ -z "$ANSWER" ]
do
.....
echo "Please enter the username of the user"
echo -e "account you wish to delete from system: \c"
read -t 60 ANSWER
done
```

当第一个问题超时时，需要一种与脚本用户通信的方法，当还有一个问题需要回答时，`case` 语句（见第 12 章）是此处完美工作的结构化命令。通过使用增加的 `ASK_COUNT` 变量，可以设置不同的消息与脚本用户通信。该部分的代码如下：

```
case $ASK_COUNT in
2)
  echo
  echo "Please answer the question."
  echo

3)
  echo
  echo "One last try...please answer the question."
  echo

4)
  echo
  echo "Since you refuse to answer the question..."
  echo "exiting program."
  echo
  #
  exit
esac
#
```

现在脚本拥有了询问用户要删除什么的所有结构。此脚本中还有几个问题要问用户，仅仅问这一个问题就需要大量的代码！因此，让我们把这段代码转换为函数（见第 17 章），以便在你的 `Delete_user.sh` 脚本的多个位置使用它。

# 创建获取正确账户的函数

你需要做的第一件事是声明函数名 `get_answer`。接下来，使用 `unset` 命令清除脚本之前给出的任何问题的答案（见第 6 章）。执行这两项的代码如下：

```
function get_answer {
#
unset ANSWER
```

你需要更改的另一个原始代码项是给脚本用户的提。创建两个新变量 `LINE1` 和 `LINE2` 来处理问题：

```
echo $LINE1
echo -e $LINE2 \c"
```

然而，并不是每个问题都有两行显示。有些只有一行。`if` 语句（见第 12 章）可以帮助解决这个问题。函数测试 `LINE2` 是否为空，如果为空则仅使用 `LINE1`：

```
if [ -n $LINE2 ]
then
  echo $LINE1
  echo -e $LINE2 \c"
else
  echo -e $LINE1 \c"
fi
```

最后，函数需要通过清除 `LINE1` 和 `LINE2` 变量来完成清理工作。因此，函数现在看起来如下：

```
function get_answer {
#
unset ANSWER
ASK_COUNT=0
#
while [ -z "$ANSWER" ]
do
  ASK_COUNT=$[ ASK_COUNT + 1 ]
#
  case $ASK_COUNT in
    echo
    2)
esac
#
  echo
```
