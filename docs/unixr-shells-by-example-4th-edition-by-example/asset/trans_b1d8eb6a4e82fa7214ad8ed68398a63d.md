

1    $ chmod 755 file
     $ ls -l file
     -rwxr-xr-x 1 ellie 0 Mar 7 12:52 file

2    $ chmod g+w file
     $ ls -l file
     -rwxrwxr-x 1 ellie 0 Mar 7 12:54 file

3    $ chmod go-rx file
     $ ls -l file
     -rw------- 1 ellie 0 Mar 7 12:56 file

4    $ chmod a=r file
     $ ls -l file
     -r--r--r-- 1 ellie 0 Mar 7 12:59 file

- 1. 第一个参数是八进制值 755。它为用户打开 rwx，为组打开 r 和 x，为其他用户打开文件。
- 2. 在 chmod 的符号形式中，为组添加写权限。
- 3. 在 chmod 的符号形式中，从组和其他用户中减去读和执行权限。
- 4. 在 chmod 的符号形式中，所有用户仅获得读权限。`=` 符号会导致所有权限重置为新值。

## The chown Command.
chown 命令更改文件和目录的所有者和组。如果使用 Linux，只有超级用户 root 才能更改所有权。如果使用 UNIX，文件所有者或超级用户可以更改所有权。要查看 chown 的用法和选项，请查阅手册页（UNIX）或使用 chown 命令配合 `--help`（Linux）选项，如示例 1.8 所示。示例 1.9 演示了如何使用 chown。

```
(The Command Line)
# chown --help
Usage: chown [OPTION]... OWNER[:[GROUP]] FILE...
  or:  chown [OPTION]... [OWNER]...[.][GROUP] FILE...
Change the owner and/or group of each FILE to OWNER and/or GROUP.

-c, --changes       be verbose whenever change is made
-h, --no-dereference affect symbolic links instead of any referenced file
                    (available only on systems with lchown system call)
```

### EXAMPLE 1: DOCUMENTATION

```
-f, --silent, --quiet  suppress most error messages
-R, --recursive         operate on files and directories recursively
-v, --verbose           explain what is being done
    --help              display this help and exit
    --version           output version information and exit

Owner is unchanged if missing. Group is unchanged if missing, but changed to login group
if implied by a period. A colon may replace the period.

Report bugs to fileutils-bugs@gnu.ai.mit.edu
```

### EXAMPLE 1.4

```
(The Command Line)
1   $ ls -l filetest
    -rw-rw-r--  1 ellie  ellie       0 Jan 10 12:19 filetest
2   $ chown root filetest
    chown: filetest: Operation not permitted
3   $ su root
    Password:
4   # ls -l filetest
    -rw-rw-r--  1 ellie  ellie       0 Jan 10 12:19 filetest
5   # chown root filetest
6   # ls -l filetest
    -rw-rw-r--  1 root   ellie       0 Jan 10 12:19 filetest
7   # chown root:root filetest
8   # ls -l filetest
    -rw-rw-r--  1 root   root        0 Jan 10 12:19 filetest
```

### EXPLANATION

- 1. filetest 的用户和组所有权均为 ellie。
- 2. chown 命令只有在你是超级用户，即用户 root 时才有效。
- 3. 用户使用 su 命令将身份更改为 root。
- 4. 列表显示 filetest 的用户和组均为 ellie。
- 5. 只有超级用户才能更改文件和目录的所有权。filetest 的所有权使用 chown 命令更改为 root。组所有权仍为 ellie。
- 6. ls 的输出显示 root 现在拥有 filetest。
- 7. 使用冒号（或点）表示在 root 之后将更改组所有权为 root。组名列在冒号之后。不能有空格。
- 8. filetest 的用户和组所有权现在均属于 root。

## 1.6.4 The Working Directory

登录时，你会在文件系统中获得一个工作目录，称为主目录。工作目录被继承给从此 shell 启动的进程。此 shell 的任何子进程都可以更改其自身的工作目录，但更改不会影响父 shell。

cd 命令用于更改工作目录，是 shell 内置命令。每个 shell 都有自己的 cd 副本。内置命令由 shell 作为 shell 代码的一部分直接执行；执行内置命令时，shell 不会执行 fork 和 exec 系统调用。如果从父 shell fork 出另一个 shell（脚本），并且在子 shell 中发出 cd 命令，则目录将在子 shell 中更改。当子进程退出时，父 shell 将处于子进程启动前的同一目录。

### EXAMPLE 1.10

```
1 > cd /
2 > pwd
   /
3 > bash
4 $ cd /home
5 $ pwd
   /home
6 $ exit
7 > pwd
   /
   >
```

### EXPLANATION

- 1 > 提示符是 TC shell 提示符。cd 命令将目录更改为 /。cd 命令内置于 shell 的内部代码中。
- 2 pwd 命令显示当前工作目录，/。
- 3 启动 bash shell。
- 4 cd 命令将目录更改为 /home。美元符号（$）是 Bash 提示符。
- 5 pwd 命令显示当前工作目录，/home。
- 6 退出 Bash shell，返回到 TC shell。
- 7 在 TC shell 中，当前工作目录仍为 /。每个 shell 都有自己的 cd 副本。

## 1.6.5 Variables

shell 可以定义两种类型的变量：本地变量和环境变量。变量包含用于自定义 shell 的信息，以及其他进程正常运行所需的信息。本地变量是私有变量，仅在定义它们的 shell 中

