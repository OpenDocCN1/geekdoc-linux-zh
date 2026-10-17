
# 第 8 章 使用 Expect 和 Autoexpect 自动化交互程序

```
autoexpect started, file is script.exp

Connected to yogi (192.168.1.100).

220 yogi FTP server (Version 4.1) Sat Feb 23 00:11:36 CST 2002) ready.

Name (yogi:root): prodmgr

331 Password required for prodmgr.

Password:

230 User prodmgr logged in.

Remote system type is UNIX.

Using binary mode to transfer files.

ftp> cd /scripts

250 CWD command successful.

ftp> get random_file.out

local: random_file.out remote: random_file.out

227 Entering Passive Mode (192,168,1,100,128,45)

150 Data connection opened for random_file.out (2185 bytes).

226 Transfer complete.

2185 bytes received in 0.0149 secs (1.4e+02 Kbytes/sec)

ftp> bye

221 Goodbye.

autoexpect done, file is script.exp
```

## 列表 8-7 使用 autoexpect 创建 ftp-get-file.exp Expect 脚本

```
send -- "get random_file.out\r"
expect "ftp>"
send "bye\r"
expect eof
```

## 列表 8-9（续）

在列表 8-9 中，我们移除了“多余的内容”，并仅测试或期待特定的提示符。当程序交互需要更多输入时，我们使用了这些提示符。注意，在 `ftp-get-file.exp` Expect 脚本中没有任何地方使用 `expect -exact`。如果我们最初使用 `autoexpect` 创建 Expect 脚本来保存按键，我们可以轻松地剥离输出并发送额外数据，限制对特定提示符的识别，从而节省我们尝试不同输出时的大量麻烦。新的 `ftp-get-file.exp` Expect 脚本在列表 8-10 中演示运行。

## 列表 8-10 ftp-get-file.exp shell 脚本运行

```
[root@boboo]# /ftp-get-file.exp
spawn yogi
Connected to yogi (192.168.1.100)
220 yogi ftp server (Version 4.1 Code Sat Feb 23 00:11:36 CST 2002) ready.
Name (yogi:root): prodmgr
331 Password required for prodmgr.
Password:
230 User logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd scripts
250 CMD successful.
ftp> get random_file.out
local: random_file.out
227 Entering Passive Mode (192,168,1,100,128,46)
150 Opening data connection for random_file.out (2185 bytes).
222 Transfer complete.
2185 bytes received in 0.00364 secs (5.9e+02 Kbytes/sec)
ftp> bye
222 Goodbye.
[root@boboo]#
```

在列表 8-10 中，我们有六处必须向 ftp 进程提供输入。我们首先启动到服务器 yogi 的新 ftp 会话。接下来，我们提供用户名和密码进行登录。一旦登录系统，进入 `/scripts` 目录并执行 `get random_file.out` 命令来检索远程文件。传输完成后，我们得到 `ftp>` 提示并输入 `bye` 来结束 ftp 会话。在每一步中，请注意我们如何使用特定的已知提示符作为提供更多输入的信号。

## 使用变量

我们的小型 ftp Expect 脚本可以工作，但如何让我们在命令行上指定远程主机和文件作为参数传递给 Expect 脚本呢？使用以下技术可以轻松实现。

Expect 命令 `set` 用于定义变量并赋值。例如，要将值 5 赋值给变量 `VAR`，我们使用以下语法：

```
set VAR 5
```

要访问变量，我们使用与普通 shell 脚本相同的技术——在变量名中添加 `$`（`$VAR`）。

要将命令行参数定义为 Expect 变量，我们使用以下语法：

```
set VAR [index $argv 0]
```

`set` 命令将 `VAR` 定义为指向第一个命令行参数（`$argv 0`）的指针。对于我们的 ftp shell 脚本，我们希望将第一个参数定义为远程主机 `rem_host`。第二个命令行参数被分配给包含文件的远程目录 `rem_dir`，第三个命令行参数被分配给远程文件 `rem_file` 变量。在本例中，我们使用以下声明进行这些定义：

```
set rem_host [index $argv 0]
set rem_dir [index $argv 1]
set rem_file [index $argv 2]
```

有了这些新定义，让我们修改 `ftp-get-file.exp` 脚本，以便我们创建一个更灵活的 Expect 脚本。查看列表 8-11 中的代码，我们将在末尾学习详细细节。

## 列表 8-11 ftp-get-file-cmd-line.exp 脚本

```
#!/usr/local/bin/expect -f

# SCRIPT: ftp-get-file-cmd-line.exp
#

set force_conservative 0 ;# 设置为 1 以强制进入保守模式，即使
    ;# 脚本最初没有以保守模式运行

if {$force_conservative} {
    set send_slow {1 .1}
    proc send {ignore arg} {
        sleep .1
        exp_send -s $arg
    }
}

set rem_host [index $argv 0]
set rem_dir [index $argv 1]
set rem_file [index $argv 2]

set timeout -1
spawn ftp $rem_host
match_max 100000
expect "Name *"
send -- "prodmgr\r"
expect "Password:"
send -- "Abcl234\r"
expect "ftp>"
send -- "cd $rem_dir \r"
expect "ftp>"
send -- "get $rem_file \r"
expect "ftp>"
send -- "bye\r"
expect eof
```

列表 8-9 和 8-11 之间的唯一区别是使用了命令行参数。我们不再为单一用途硬编码脚本，而是有了一个可以控制远程主机、远程目录和远程文件的灵活 Expect 脚本。在列表 8-11 中，注意我们使用 `set` 命令定义三个命令行变量：`rem_host`、`rem_dir` 和 `rem_file`。通过这些定义，我们现在启动到 `$rem_host` 的 ftp 会话，进入 `$rem_dir` 目录，然后通过定义的命令行参数获取 `$rem_file` 文件。列表 8-12 显示了 `ftp-file-cd-cmd-line.exp` 脚本的运行。

## 列表 8-12 ftp-file-cd-cmd-line.exp 脚本运行

```
@root@booooo# ./ftp-file-cd-cmd-line.exp yogi /scripts random_file.out
spawn ftp yogi
Connected to yogi (192.168.1.100).
220 yogi ftp server (Version 4.1 Code Sat Feb 23 00:11:36 CST 2002) ready.
```
