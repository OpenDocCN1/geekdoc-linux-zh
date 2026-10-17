
这种方法要求在脚本上设置执行权限。它也会创建一个子壳来运行脚本。

## `script-name`

只需输入脚本名称，需要将脚本移动到你路径（`path`）中的目录，例如 `/usr/local/bin`。这是供他人使用的脚本的优选方法：

```
$ cd homeChristine/NewDir
$ sudo mv my-script.sh /usr/local/bin
[sudo] password for Christine:
$ chmod a+x /usr/local/bin/my-script.sh
$ echo $PATH
/usr/lib64/qt-3.3:bin:/usr/local/bin:bin:/usr/bin:/usr/local/sbin:/usr/bin:/sbin:homeChristine/bin
$ my-script.sh
PID PPID CMD
2821 2820 -bash
2928 2821 \ binbash /usr/local/bin/my-script.sh
2929 2928 \ ps -o pid -o pid -o cmd --forest
脚本执行完成
$
```

这种方法要求设置适当的执行权限。由于所有系统用户都会使用，因此使用 `chmod a+x` 命令向所有人授予执行权限。注意 `$PATH` 环境变量包含了 `/usr/local/bin` 目录，`my-script.sh` 正被移动到了那里。注意，当运行脚本时，这种方法会创建一个子壳。

以 `sh` 为前缀输入脚本名称与前面的 `bash` 命令几乎相同。它告诉 Linux 在当前目录运行脚本，而不是搜索当前路径：

```
$ sudo /usr/local/bin/my-script.sh homeChristine/
[sudo] password for Christine:
$ cd homeChristine
$ chmod a-x my-script.sh
$
```

```
$ sh my-script.sh
PID PPID CMD
2821 2820 -bash
2973 2821 \ bash my-script.sh
2974 2973 \ ps -o pid -o ppid -o cmd --forest
```

脚本执行完成 $

这种方法运行脚本不需要执行权限，它会创建一个子壳来运行脚本，如输出中的 `sh my-script.sh` 行所示。

```
source script-name
```

在脚本名称前输入关键字 `source` 告诉 `bash` shell 使用 `sourcing` 方法。当你 `source` 一个脚本时，不会创建子壳来运行脚本。

```
$ source my-script.sh
PID PPID CMD
2821 2820 -bash
3095 2821 \ ps -o pid -o ppid -o cmd --forest
$
```

脚本执行完成

注意没有创建新进程（子壳）来运行 `my-script.sh`。它在当前 `bash` shell (`PID` `2821`) 中运行。这种方法不需要执行权限。

- `script-name`

在脚本名称前输入一个点 `.` 然后一个空格告诉 `bash` shell 使用 `sourcing` 类型。小心，不要忘记在点和脚本名称之间包含空格：

```
$ . my-script.sh
PID PPID
2821 2820 \_ ps -o pid -o ppid -o cmd --forest
3157 2821 \_ ps -o pid -o ppid -o cmd --forest
Done with Script
$
```

这种方法也不会创建子壳。脚本在当前 `bash` shell (`PID` `2821`) 中运行。

```
exec ./script-name
```

最后一种执行脚本的方法使用 `exec` 命令。这种方法确实需要设置文件执行权限。注意，如果你在跟着书中执行脚本，你需要在脚本底部添加一个暂停。这里 `sleep 10` 命令被添加到了 `my-script.sh`，所以脚本将会暂停。

## 在 Shell 脚本中使用变量

变量可以扩展脚本的实用性。变量是脚本中的占位符，其值是在脚本运行时确定的。变量的值可以通过参数传递给脚本、在脚本内部生成或从脚本的环境中提取。

## 理解位置参数变量

传递给脚本的变量通常被称为位置参数。单个参数由美元符号 (`$`) 后跟 `0` 到 `9` 的数字表示——`$` 代表脚本名称，`$1` 是脚本的第一个参数，`$2` 是第二个参数，以此类推。

为了演示参数变量的作用，编写了一个简单的创建用户账户的脚本（有关创建用户账户的信息请参见第7章“管理系统”）。请记住，此脚本在所有发行版上都能运行，因为它使用了 `useradd` 命令，而某些发行版使用的是 `addUser`。如果你想在你的 Linux 系统上使用它，可能需要进行修改：

```
$ cat mkuser.sh
#!/binbash
#
# 创建用户账户及其密码
############################################
#
# 创建用户账户 ###
echo Account for $1 is being created...
#
useradd $1
#
# 设置用户账户密码 ###
#
echo Password for $1 is being set...
#
passwd $1
#
echo Account is ready for use.
#
############################################
$
```

注意 `mkuser.sh` 脚本中的位置参数 `$1` 不仅出现在 `useradd` 和 `passwd` 命令中，也出现在几个 `echo` 命令中。同样注意在上一个示例中，脚本的第一行，the shebang 表明 `binbash` 是该脚本的程序解释器。在第一行之后，你会看到两个井号（`#`），它们分别表示注释或实际的 `bash` 壳命令。

注意 `mkuser.sh` 脚本中的某些井号单独占一行。这为脚本提供了充足的间距，增加了其可读性。Shell 脚本应该是易读的。这在需要修改脚本时非常有帮助。

`mkuser.sh` 脚本根据作为位置参数 `$1` 传递的账户名称创建账户并更改账户密码。由于脚本完成其任务需要超级用户权限，因此在执行脚本时使用了 `sudo` 命令，如下：

```
$ chmod u+x mkuser.sh
$
$ sudo ./mkuser.sh River
Account for River is being created...
Password for River is being set...
Changing password for user River.
New password:
Retype new password:
passed: all authentication tokens updated successfully.
Account is ready for use.
$
$ tail -1 etc/passwd
River:x:506:510::/home/River:/bin/bash
$
```

注意传递给 `mkuser.sh` 脚本的位置变量的值为 `River`。因此，在脚本中每个 `$1` 变量出现的地方，现在都用 `River` 代替了。虽然非常简单，但它可以被有效地使用，例如一次创建多个用户账户。

通过对 `mkuser.sh` 脚本进行细小的修改，你可以从命令行获取位置参数并一次创建多个账户！这里有一个片段示例：

```
$ cat mkuser.sh
#!/bin/bash
#
[...]
#
passwd $1
#
echo Account is ready for use.
#
# Create user account ###
echo Account for $2 is being created...
#
useradd
#
# Set user account password ###
#
echo Password for $2 is being set...
#
passwd $2
#
echo Account is ready for use.
#
###########################################
$
```

脚本现在有了额外的代码来处理使用作为第二个位置参数 `$2` 传递的名称创建第二个用户。以下是修改后的脚本运行：

```
$ sudo ./mkuser.sh Malcolm Inara
[sudo] password for Christine:
Account for Malcolm is being created...
```
