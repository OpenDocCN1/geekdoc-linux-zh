
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
  if [ -n "$LINE2" ] #Print two lines
  then
    echo $LINE1
    echo -e $LINE2 \c"
  else
    echo -e $LINE1 \c" #Print one line
  fi
#
  read -t 60 ANSWER
done
unset LINE1
unset LINE2
}
```

询问用户要删除什么时，脚本已经有了所需的所有结构。此脚本中还有几个问题要问用户，仅仅问这一个问题就需要大量的代码！因此，让我们把这段代码转换为函数（见第 17 章），以便在你的 `Delete_user.sh` 脚本的多个位置使用。

# 获取正确的账户的函数

（注：此处由于原文文本存在重复，已按逻辑整合翻译）

# 获取正确的账户

询问用户要删除什么时，脚本已经有了所需的所有结构。此脚本中还有几个问题要问用户，仅仅问这一个问题就需要大量的代码！因此，让我们把这段代码转换为函数（见第 17 章），以便在你的 `Delete_user.sh` 脚本的多个位置使用。

# 获取正确的账户的函数

（注：此处由于原文文本存在重复，已按逻辑整合翻译）

# 获取正确的账户

询问用户要删除什么时，脚本已经有了所需的所有结构。此脚本中还有几个问题要问用户，仅仅问这一个问题就需要大量的代码！，，，，翻译翻译翻译翻译翻译：

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

现在脚本拥有了询问用户要删除什么的所有结构。此脚本中还有几个问题要问用户，仅仅问这一个问题就需要大量的代码！因此，让我们把这段代码转换为函数（见第 17 章），以便在你的 `Delete_user.sh` 脚本的多个位置使用。

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
```
