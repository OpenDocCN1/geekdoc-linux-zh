

如果使用 su 命令获取 root 权限，则应使用连字符 (-) 选项来获得 root 环境，特别是 root 的 PATH。下面的示例展示了 su 命令在有和没有连字符选项时的运行情况。请注意，如果没有连字符，就会运行错误的 useradd 命令。

## EXAMPLE 16.3

```
1 $ id
uid=501(ellie) gid=100(users) groups=100(users)
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

## EXPLANATION

- 1 运行 id 命令，显示此 shell 由用户 ellie 拥有，这是一个非超级用户账户。
- 2 显示 PATH 变量，显示它确实包含 . 目录，但不包含 /usr/sbin 目录。
- 3 运行 su 命令，启动一个由 root 拥有的新 shell。
- 4 显示 PATH 变量，显示它没有改变。
- 5 运行 cd 命令，将 /tmp 设为当前目录。
- 6 ls 命令显示当前目录中存在一个名为 useradd 的程序，该目录为 /tmp 目录。此程序几乎肯定不存在于你的系统上。此程序恰好位于该特定系统的 /tmp 目录中。

### EXPLANATION (CONTINUED)

- 7 此 ls 命令显示 /usr/sbin 目录中也存在 useradd 程序。/usr/sbin 中的版本是管理员用于创建新账户的正常 useradd 命令。
- 8 运行 useradd 命令。由于 PATH 中存在 .（点），shell 运行了当前目录中的 useradd 副本。这并非本意；本应运行 /usr/sbin 目录中的 useradd 命令。由此错误导致 newguy 账户从未被添加。
- 9 使用 exit 命令终止当前的 root 拥有 shell。
- 10 再次运行 su 命令，这次使用连字符选项。su 命令在创建新 shell 时将使用 root 的 PATH 而不是非特权账户的 PATH（su 命令创建的 shell）。
- 11 再次执行 useradd 命令。shell 将使用 root 的 PATH 来查找命令，并执行 /usr/sbin 目录中的 useradd。useradd 命令将在 /etc/passwd 文件末尾添加一行以创建此账户。
- 12 使用 tail 命令显示 /etc/passwd 文件的最后一行。你可以看到 newguy 账户已被添加。
- 13 退出 root 拥有 shell。这是一个良好的做法——当超级用户完成需要 root 访问的命令后，应终止 root shell。如果超级用户忘记退出 root shell，它将对使用该账户的任何人开放。不是一个好主意！

## 16.3.1 Running Scripts As Root

以 root 账户（超级用户）运行脚本所需的技巧与以普通用户运行脚本略有不同。传统上，root 账户的 PATH 变量值与非特权账户不同。root 的 PATH 通常由包含系统命令的目录组成。例如，/usr/sbin 目录通常是 root PATH 的一部分，但不是非 root 账户 PATH 的一部分。为了防止 root 意外运行当前目录中的程序，root 的 PATH 变量通常不包含当前目录，称为点目录，用句点表示。

### Running a Script in the Current Directory.

由于 .（点）不是 root PATH 的一部分，因此脚本在以正常方式通过在命令行单独输入脚本名称调用时不会运行。当你以 root 身份运行脚本时，应在脚本前加上调用 shell 的名称。

