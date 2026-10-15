

```
2 $ echo $PATH

/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:.

3 $ su

password:

4 $ echo $PATH

/usr/local/bin:/usr/bin:/bin:/usr/X11R6/bin:.

5 # cd /tmp

6 # ls -l useradd

-rwxr-xr-x 1 ellie group 65 Feb 12 11:56 useradd

7 # ls -l /usr/sbin/useradd

-rwxr-xr-x 1 root root 57348 Mar 17 2003

/usr/sbin/useradd

8 # useradd newguy

this is the useradd script in the /tmp directory

9 # tail -1 /etc/passwd

ellie:x:501:100::/home/ellie:/bin/bash

# exit

10 $ su -

password:

11 # useradd newguy

12 # tail -1 /etc/passwd

newguy:x:502:100::/home/newguy:/bin/bash

13 # exit
```

### EXPLANATION

- 1 运行`id`命令，显示此 shell 由用户 ellie 拥有，这是一个非超级用户账户。
- 2 显示`PATH`变量，显示它确实包含`.`目录，但不包含`/usr/sbin`目录。
- 3 运行`su`命令，启动一个由 root 拥有的新 shell。
- 4 显示`PATH`变量，显示它没有改变。
- 5 运行`cd`命令，将`/tmp`设为当前目录。
- 6 `ls`命令显示当前目录中存在一个名为`useradd`的程序，该目录为`/tmp`目录。此程序几乎肯定不存在于你的系统上。此程序恰好位于该特定系统的`/tmp`目录中。

### EXPLANATION (CONTINUED)

- 7 此`ls`命令显示`/usr/sbin`目录中也存在`useradd`程序。`/usr/sbin`中的版本是管理员用于创建新账户的正常`useradd`命令。
- 8 运行`useradd`命令。由于`PATH`中存在`.`（点），shell 运行了当前目录中的`useradd`副本。这并非本意；本应运行`/usr/sbin`目录中的`useradd`命令。由此错误导致 newguy 账户从未被添加。
- 9 使用`exit`命令终止当前的 root 拥有 shell。
- 10 再次运行`su`命令，这次使用连字符选项。`su`命令在创建新 shell 时将使用 root 的`PATH`而不是非特权账户的`PATH`（`su`命令创建的 shell）。
- 11 再次执行`useradd`命令。shell 将使用 root 的`PATH`来查找命令，并执行`/usr/sbin`目录中的`useradd`。`useradd`命令将在`/etc/passwd`文件末尾添加一行以创建此账户。
- 12 使用`tail`命令显示`/etc/passwd`文件的最后一行。你可以看到 newguy 账户已被添加。
- 13 退出 root 拥有 shell。这是一个良好的做法——当超级用户完成需要 root 访问的命令后，应终止 root shell。如果超级用户忘记退出 root shell，它将对使用该账户的任何人开放。不是一个好主意！

## 16.3.1 Running Scripts As Root

以 root 账户（超级用户）运行脚本所需的技巧与以普通用户运行脚本略有不同。传统上，root 账户的`PATH`变量值与非特权账户不同。root 的`PATH`通常由包含系统命令的目录组成。例如，`/usr/sbin`目录通常是 root `PATH`的一部分，但不是非 root 账户`PATH`的一部分。为了防止 root 意外运行当前目录中的程序，root 的`PATH`变量通常不包含当前目录，称为点目录，用`.`表示。

### Running a Script in the Current Directory.

由于`.`（点）不是 root 的`PATH`的一部分，因此脚本在以正常方式通过在命令行单独输入脚本名称调用时不会运行。当你以 root 身份运行脚本时，应在脚本前加上调用 shell 的名称。

#### 示例 16.4

```
1  # cat myscript

#! /bin/sh

echo this is my script

2  # echo $PATH

/usr/sbin:/bin:/usr/bin:/sbin:/usr/X11R6/bin

3  # myscript

bash: myscript: command not found

4  # /bin/sh myscript
```

#### 解释

1. `shell`脚本`myscript`的内容被显示出来。该脚本的第一行表明它为`/bin/sh`程序编写，该程序是 Bourne shell。
2. `PATH`变量的值被显示出来。注意`PATH`中不包含点（`.`）目录。
3. 该命令失败，因为`PATH`不包含`.`（点）目录。
4. 该命令成功，因为脚本名称作为参数传递给了 shell `/bin/sh`。通过这种方式调用 shell，`PATH`变量不会被用来定位脚本；相反，shell 会检查当前工作目录以查看脚本是否在那里。

执行当前工作目录中的脚本或任何其他命令的另一种方法是，在程序前加上`./`以表示该程序位于当前工作目录中。

#### 示例 16.3

```
1  # cd /usr/local/bin

2  # myprog

-bash: myprog: command not found

3  # ./myprog

this is my program
```

#### 解释

1. 当前目录被更改为`/usr/local/bin`。
2. 该目录包含一个名为`myprog`的程序。尝试运行该程序`myprog`并未成功。在`PATH`中没有`.`的情况下，shell 无法定位该程序。
3. 在指定了`myprog`的位置（`.`目录）之后，命令成功运行。

## 16.3.2 以 root 身份运行的脚本（setuid 程序）

谁运行 setuid 程序，谁就会暂时成为该程序的所有者，并拥有与所有者相同的权限。虽然大多数 setuid 程序设置为 root，但它们可以设置为任何用户。如果 setuid 程序设置为 root，当一个无特权用户运行此类程序时，他或她会暂时成为 root。这有点像灰姑娘的故事，因为当程序退出时，用户会回到他或她卑微的生活地位并失去所有 root 权限。`passwd`程序是 setuid 程序的一个很好的例子。当你更改密码时，你会暂时成为 root，但仅在`passwd`程序执行期间。这就是为什么你能够在不求助于系统管理员帮助的情况下更改密码。如果不能以 root 身份运行，你将不被允许访问`/etc/passwd`（或`/etc/shadow`）文件，该文件通常对普通用户禁止访问。要识别 setuid 程序，请使用`ls -l`命令。如果程序是 setuid 程序，则`x`（执行）权限将被`s`替换。

#### 示例 16.6

```
1 $ ls -l /bin/passwd

-r-sr-sr-x 1 root sys 21964 Apr 6 2002 /bin/passwd

2 $ ls -l /etc/shadow

-r-------- 1 root sys 4775 May 5 13:33 /etc/shadow
```

#### 解释

1. `ls -l`的输出显示此 setuid 程序将以 root 身份运行。权限字段中用字母`s`替换了`x`（执行位）。
2. `/etc/shadow`文件，即密码存储位置（Solaris），显示这是一个 root 所拥有的文件，只有 root 可以读取它。

Shell 程序可以写成 setuid 程序，如果不由系统管理员监控，则会构成严重的安全威胁。如果 shell 脚本是 setuid 程序（对 root），则生成的 shell 是 root 所拥有的 shell，并且从脚本中执行的命令将以 root 身份运行。为什么 shell 脚本需要是 setuid 程序？如果某个文件，例如数据库或日志文件，包含不应让普通用户访问的信息，则该文件上的权限应对除所有者之外的所有人关闭。如果脚本需要访问该文件，并且由非特权用户执行，则会显示`Permission denied`错误并且脚本将失败。如果脚本是 setuid 脚本，运行脚本的人可以采用文件所有者的身份并访问文件中的数据。并非所有 shell 都允许脚本设置为 root 权限，即使 shell 允许，操作系统也可能不允许。例如，`Bash`不支持 setuid 脚本，而`Korn shell`有一个特权模式（`-p`）用于在操作系统允许的情况下运行 setuid 脚本。以下步骤为`C/TC shell`脚本设置 setuid 程序。

1. 在脚本中，第一行是

```
#!/bin/csh -feb
```

