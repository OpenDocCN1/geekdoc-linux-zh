
# 第 8 章 使用 Expect 和 Autoexpect 自动化交互式程序

## 列表 8-12 ftp-file-cd-cmd-line.exp 脚本运行

```
Name (yogi:root): prodmgr
331 Password required for prodmgr.
Password:
230 User logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp /scripts
250 CMD successful.
ftp get random_file.out
local: random_file.out remote: random_file.out
227 Entering Passive Mode (192,168,1,100,128,46)
150 Opening data connection for random_file.out (2185 bytes).
222 Transfer complete.
2185 bytes received in 0.00364 secs (5.9e+02 Kbytes/sec)
ftp bye
222 Goodbye.
[root@boboo]#
```

列表 8-10 和 8-12 是相同的，因为我们通过变量赋值执行相同的命令。这些脚本唯一的缺点是用户名和密码以明文显示在脚本中。因此，你需要锁定文件以防止他人获取密码。更好的解决方案是创建一个包含用户名和密码的环境文件，在脚本开头 `source` 或执行该环境文件，甚至可以加密密码文件并在脚本在使用之前进行解密。只需记住不要忘记用户名和密码变量，否则它们会在进程表中明文显示。

## 条件测试如何？

很多时候我们期待某些值。例如，如果我们 `ssh` 到一个服务器且远程主机不在 `~/.ssh/known_hosts` 文件中，会被提示添加远程主机的公钥。在这种情况下，我们首先需要输入 `yes` 才能登录。其他时候我们会得到 `Password:` 提示。Expect 如何处理这种条件测试？一种方法是使用括号。让我们仔细观察。

## Expect 的 Case Statement

让我们看两个使用 `ssh` 登录远程服务器的示例。在第一个示例中，远程服务器不在用户的 `known_hosts` 文件中，我们得到一个额外的提示将服务器永久添加到 ssh 配置中。第二个示例显示了登录到未知主机。

### 列表 8-13 登录未知主机

```
prodmgr@wilma's:
Last login: Thu Nov 29 10:53:04 EST 2007 on ssh from yogi
Last login: Mon Dec 24 17:36:50 EST 2007 on /dev/pts/0 from fred
You are logging on to wilma
$
```

注意列表 8-13，`ssh` 并不识别 `wilma` 为已知主机，因为 `wilma` 的公钥不在本地的 `~/.ssh/known_hosts` 文件中。因此，`ssh` 提示将 `wilma` 的密钥添加到 `~/.ssh/known_hosts` 文件中，我们回答 `yes`，如下：

```text
Are you sure you want to continue connecting (yes/no)? yes
```

得到肯定回复后，我们提示输入 `prodmgr` 密码并登录。在列表 8-14 中，这次只被提示输入 `prodmgr` 密码。

### 列表 8-14 登录到已知主机

```
root@yogi~# ssh prodmgr@wilma
prodmgr@wilma's password:
Last unsuccessful login: Thu Nov 29 10:53:04 EST 2007 on ssh from yogi
Last login: Dec 27 13:44:11 EST 2007 on /dev/pts/0 from yogi
You are logging on to wilma
$
```

在列表 8-14 中，主机 `wilma` 是已知的，所以 `ssh` 不提示我们添加密钥；我们使用 `Password` 提示。使用 Expect，我们使用列表 8-15 所示的语法进行条件测试。

### 列表 8-15 Expect 条件测试示例语法

```expect
expect {
    "*re sure you want to continue connecting*"
    {
        send "yes\n"
        expect {
            "*password*"
            send "Ab1234\n"
        }
    }
    "answer"
    {
        send "Ab1234\n"
    }
}
```

列表 8-15 展示了 Expect 版本的 case statement（分支语句）。第一个 `expect` 有两种可能的响应：

- `*are you sure you want to continue connecting*`
- `answer`

注意，我们使用了通配符，因为不同版本的 SSH 和 UNIX 变体提供的响应各异。有时 A 和 P 是大写的，有时则不是。文中包含一些我们不在乎的额外文本，因此我们使用通配符来匹配那些我们不确定会变化的数据。
如果回复是 `are you sure you want to continue connecting`，我们回复 `yes` 并等待 `Password:` 提示，然后输入密码。否则，我们只得到 `answer` 提示并输入密码。这类似于 shell 脚本中的 `case` 语句。
让我们看看列表 8-16 中的 Expect 脚本来了解如何实现。`etc-hosts-copy.exp` Expect 脚本用于将位于服务器 `yogi` 上的主 `/etc/hosts` 文件复制到远程机器。请跟随脚本，并留意列表 8-16 中的加粗文本。

### 列表 8-16 etc-hosts-copy.exp Expect 脚本

```expect
#!/usr/local/bin/expect -f

# SCRIPT: etc-hosts-copy.exp

# 设置超时时间为 3 秒
set timeout 3

# 将第一个命令行参数赋值给 "host" 变量
set rem_host [index argv 0]

# 以 prodmgr 身份向 $host 启动 ssh 会话
spawn /usr/bin/ssh -l prodmgr ${rem_host}

# 当我们 ssh 到远程服务器时，有两种可能的响应：
# 1) *are you sure you want to continue connecting*，我们必须回复 "yes"
# 2) Password: 提示。接下来的 expect 语句将根据响应执行正确的操作。

expect {
    "*are you sure you want to continue connecting*"
    {
        send "yes\n"
        expect {
            "*password*"
            send "Abc1234\n"
        }
    }
    "*password*"
    {
        send "Abc1234\n"
    }
}

# 在继续之前等待 1 秒
sleep 1

# 将 prodmgr 的命令行提示符设置为井号，#
send "PS1=\\#@ \\n"

# 我们现在知道要期待命令行提示符了
expect "^#*"

# 将 yogi 上的主 /etc/hosts 文件复制到此机器。
# 首先切换到 root
send "su - \n"
expect "*password:*"
send "ABCD1234\n"
sleep 1

# 将 root 用户的命令行提示符设置为井号，#
send "PS1=\\#@ \\n"

# 现在我们知道 root 用户的命令行提示符是什么
expect "*#"

# 保存当前版本的 /etc/hosts 文件
send "cp /etc/hosts /etc/hosts$$"
expect {
    "*are you sure you want to continue connecting*"
}
```
