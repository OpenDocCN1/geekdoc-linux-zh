
```text
$ waitfor sandy &       Run it in the background
[1] 4392               Job number and process id
$ nroff waitfor         Do other work
    ...

sandy has logged on      Happens sometime later
```

现在你可以做其他工作，而 `waitfor` 程序会在后台持续执行，直到 sandy 登录，或者直到你退出系统。

> **注意**
>
> 默认情况下，当你退出系统时，你所有的进程都会自动被终止。
>
> 如果你想在退出登录后让某个程序继续运行，可以使用 `nohup` 命令运行它，或者使用 `at` 或 `cron` 安排它运行。更多细节请参阅你的 Unix 用户手册。

由于 `waitfor` 每分钟只检查一次用户是否登录，它在运行期间不会消耗太多系统资源（这是在后台运行程序时的一个重要考虑因素）。

遗憾的是，在指定用户登录之后，你可能会错过那一行通知消息。如果你正在使用 `vi` 之类的屏幕编辑器编辑文件，通知消息可能把你的屏幕弄得一团糟，而且你仍然可能无法看清消息！

更好的办法也许是改为把通知发送到你的邮箱。嘿，你甚至可以让用户自己选择：在程序中添加一个选项，如果选中该选项，则表示消息应该被发送到邮箱；如果没有选中，则在终端上显示消息。

在下面的 `waitfor` 版本中，为此添加了一个 `-m` 选项：

```sh
$ cat waitfor
#
# Wait until a specified user logs on -- version 2
#

if [ "$1" = -m ]
then
        mailopt=TRUE
        shift
else
        mailopt=FALSE
fi

if [ "$#" -eq 0 -o "$#" -gt 1 ]
then
        echo "Usage: waitfor [-m] user"
        echo "    -m means to be informed by mail"
        exit 1

fi

user="$1"

#
# Check every minute for user logging on
#

until who | grep "^$user " > /dev/null
do
        sleep 60
done

#
# When we reach this point, the user has logged on
#

if [ "$mailopt" = FALSE ]
then
        echo "$user has logged on"
else
        echo "$user has logged on" | mail steve
fi
$
```

第一个测试检查是否指定了 `-m` 选项。如果指定了，`mailopt` 被赋值为 `TRUE`，并执行 `shift` 以“移出”第一个参数（将要监控的用户名移到 `$1`，并递减 `$#`）。如果没有指定 `-m` 选项，`mailopt` 被设置为 `FALSE`。

随后程序的执行过程与前一版本相同，只不过这次当主代码块执行完毕后，会测试 `mailopt` 变量，以决定是通过电子邮件还是通过 `echo` 语句来输出通知。

```sh
$ waitfor sandy -m
Usage: waitfor [-m] user
             -m means to be informed by mail
$ waitfor -m sandy &
[1] 5435
```

```text
$ vi newmemo

you have mail
$ mail
From steve Wed Aug 28 17:44:46 EDT 2002
sandy has logged on

?d
$
```

*工作继续*

当然，我们本可以把 `waitfor` 写成让 `-m` 选项可以作为第一个或第二个参数出现，但这不是传统 Unix 语法的做法：所有选项都应放在命令行中其他任何类型的参数之前。

另外请注意，旧版本的 `waitfor` 也可以通过以下方式执行：

```sh
$ waitfor sandy | mail steve &
[1] 5522
$
```

来达到与添加 `-m` 选项相同的结果，但这样做远不那么优雅。

这个程序目前始终把邮件发送给 `steve`，如果有人想运行它，这就不太有用了。更好的做法是确定运行该程序的用户，然后在他们指定 `-m` 选项时，将邮件发送给该用户。但如何做到这一点呢？一种方法是执行带 `am i` 选项的 `who` 命令，获取返回的用户名。然后你可以使用 `cut` 从 `who` 的输出中提取用户名，并把该用户名作为邮件的收件人。

所有这些都可以在 `waitfor` 的最后一条 `if` 命令中完成，只要将其改为如下所示：

```sh
if [ "$mailopt" = FALSE ]
then
        echo "$user has logged on"
else
        recipient=$(who am i | cut -c1-8)
        echo "$user has logged on" | mail $recipient
fi
```

现在，任何人都可以运行这个程序，邮件通知也会被发送给正确的收件人。

## 关于循环的更多内容

### 跳出循环

有时，程序逻辑要求立即退出某个循环语句。要从循环中退出但不退出程序，可以使用 `break` 命令：

```sh
break
```

当执行 `break` 命令时，控制会立即移出循环，然后像平时一样继续执行。

这种用法常见于无限循环——即一段旨在不断循环执行相同命令、直到 `break` 将其停止的代码块。

在这些情况下，可以使用 `true` 命令来返回零退出状态。`false` 命令也可以用在相反的情况下，因为它返回非零退出状态。如果你编写

```
while true
do
        ...
done
```

那么 `while` 循环将永远执行下去，因为 `true` 总是返回零退出状态。

由于 `false` 总是返回非零退出状态，因此下面这个循环

```
until false
do
        ...
done
```

也将永远执行下去。

因此，`break` 命令通常用于在检测到错误条件或处理结束时退出这类无限循环：

```
while true
do
        cmd=$(getcmd)

        if [ "$cmd" = quit ]
        then
                break
        else
                processcmd "$cmd"
        fi
done
```

在这里，`while` 循环将继续执行 `getcmd` 和 `processcmd` 程序，直到 `cmd` 等于 `quit`。此时，将执行 `break` 命令，从而退出循环。

如果 `break` 命令以下面的形式使用

```
break n
```

那么最内层的 `n` 个循环会立即被退出，因此在

```
for file
do
    ...
    while [ "$count" -lt 10 ]
    do
        ...
        if [ -n "$error" ]
        then
            break 2
        fi
        ...
    done
    ...
done
```

中，如果 `error` 非空，`while` 和 `for` 循环都会被退出。

### 在循环中跳过剩余命令

`continue` 命令与 `break` 类似，只是它不会导致循环退出，而只是跳过当前循环迭代中的剩余命令。程序会立即进入循环的下一次迭代，并照常继续执行。与 `break` 一样，`continue` 后面可以跟一个可选数字，因此

```
continue n
```

会使最内层 `n` 个循环中的命令被跳过，之后程序照常继续执行。

```
for file
do
    if [ ! -e "$file" ]
    then
        echo "$file not found!"
        continue
    fi

    #
    # Process the file
    #

    ...
done
```

每次都会检查 `file` 的值，以确保该文件存在。如果不存在，就会打印一条消息，并跳过 `for` 循环中对该文件的进一步处理。程序继续处理列表中的下一个值。

前面的示例等同于编写
