
```
[root@krosum~# ls p[0-9].py] # file name p<followed by any single digit.py
p1.py p2.py
[root@krosum~#]
[root@krosum~#] ls -l p[0-9].py # file name p<followed by any single digit.py
-rw-r--.1 root 29 May 25 7.2G 2019 p1.py
-rw-r--.2 root 146 May 25 2019 p2.py
[root@krosum~#]
[root@krosum~#] df -Th | grep "/dev/sda[1-4]" Filter only the storage device of mounted file system
/dev/sda2 9.8G 2.6G 7.2G 27% /
/dev/sda1 ext4 488M 73M 390M 16% /boot
[root@krosum~#]
```

- 或者 `ls p[abc].java` # file name p<followed by character a or b or c> java extension

### 大括号扩展 (Brace Expansion)

- 大括号 `{}` 扩展是一种生成任意字符串的机制。

- 前缀 `"a"` 会加到大括号内的每个字符串之前，然后后缀 `"e"` 会附加到每个生成的字符串之后，从左到右扩展。

```
[root@krosum ~]# echo a{b,c,d}
ace ade abe
```

- Shell 的默认元字符是在 shell 中具有特殊含义的特定字符。

| FILE DESCRIPTOR | DESCRIPTION | ABVIATION |
| :--- | :--- | :--- |
| 0 | 标准输入 | STDIN |
| 1 | 标准输出 | STDOUT |
| 2 | 标准错误 | STDERR |

- 输出重定向将命令的输出发送到文件中而不是打印到屏幕上。

文件的内容。

## 重定向标准错误 (Standard Error)

- 使用文件描述符数字 `(2)` 和大于号 `(>)` 的命令可以将任何标准错误消息重定向到 `/dev/null` 文件。

```bash
student@krosum ~$ cat r1.log
12:45:51 up 1 day, 11:12, 3 users, load average: 0.10, 0.08, 0.06
student@krosum ~$
student@krosum ~$ uptime r1.log # same as uptime r1.log
student@krosum ~$
student@krosum ~$
DOUT - 创建新文件写入命令
student@krosum ~$ cat r1.log
12:46:11 up 1 day, 11:12, 3 users, load average: 0.20, 0.11, 0.06
student@krosum ~~$
```

以下示例显示了将标准错误重定向到 `error.logfile`。

```bash
student@krosum ~$ uptimeee
bash: uptimeee: command not found
student@krosum ~$
student@krosum ~$ uptimeee >error.log
bash: uptimeee: command not found
student@krosum ~$
student@krosum ~$ uptimeee 2>error.log
student@krosum ~$ cat error.log
bash: uptimeee: command not found
student@krosum ~$ mkdir /D1 2>>error.log # appending command error
error.log file
student@krosum ~$ cat error.log
bash: uptimeee: command not found
mkdir: cannot create directory '/D1': Permission denied
student@krosum ~$
```

要将标准输出 `stdout` 和标准错误 `stderr` 都重定向到同一个文件，请使用以下语法

```bash
2>&1
```

```bash
[student@krosum]~$ uptime 1>r1.log 2>error.log
[student@krosum]~$ ###### ###### 有效命令结果(STDOUT)
[student@krosum]~$ #### 重定向到 r1.log 文件。
[student@krosum]~$$
[student@krosum]~$ uptimeee 1>r1.log 2>error.log
[student@krosum]~$ #
[student@krosum]~$ # 无效命令 - 错误消息(STDERR)
[student@krosum]~$ # 重定向到 error.log 文件。
[student@krosum]~$$
[student@krosum]~$ uptime >result.log 2>&1 将 STDOUT/STDERR 写入 result.log 文件
[student@krosum]~$ uptimeee >>result.log 2>&1
[student@krosum]~$ cat result.log
13:06:23 up 1 day, 11:33, 3 users, load average: 0.17, 0.11, 0.06
bash: uptimeee: command not found
[student@krosum]~$
```

注意：语法 `2>&1` 指示 shell 将 stderr `(2)` 重定向到接收 stdout `(1)` 的相同文件。

## 使用管道符 (Pipe Character)

- 管道符将一个命令的标准输出重定向到另一个命令的标准输入。

`Command1 | Command2`

- 例如，使用 `who` 命令的标准输出作为 `wc -l` 命令的标准输入。

```bash
who | wc -l
cat /etc/passwd|grep|wc -l
```

```bash
[student@krosum ~]$
[student@krosum ~]$ who|wc -l
[student@krosum ~]$ cat /etc/passwd|grep bash
root:x:0:0:root:/root:/bin/bash
student:x:1000:1000:appelix student:/home/student:/bin/bash
[student@krosum ~]$ cat /etc/passwd|grep bash|wc -l
[student@krosum ~]
```

通过这样我们可以使用管道连接多个命令。

## 引用字符 (Quoting Characters)

- 引用是一个指示 shell 屏蔽或忽略 shell 元字符 `meta characters` 特殊含义的过程。

- 引用字符有：

    - 单引号 `('')`：指示 shell 忽略所有包含在内的元字符。

```bash
$student@krosum ~$ echo '$0'
$student@krosum ~$ echo $0 This is special variable bash
$student@krosum ~$ echo '$#!@#$&'
$!@#$%\&
$student@krosum ~$ echo $@@#$%
bash: !@#$%: event not found
$student@krosum ~$
```

    - 反斜杠 `(\ )`：防止 shell 将 `(\ )` 之后的字符解释为元字符。

```bash
$student@krosum ~$ echo "Hello"
Hello
$student@krosum ~$ echo \"Hello"
'Hello'
```

    - 双引号 `("")`：指示 shell 执行并显示 UNIX 系统命令的输出。

    - 括号 `$(command)`：指示 shell 执行并显示括号内命令的输出。

![](img/39c8fbde7fc51cbef611f658dfbb1fe2_164_0.png)

# 第 11 章 - 文件权限 (FILE PERMISSION)

- Linux 中的所有文件和目录都有一套标准的访问权限。

- 这种访问权限控制对所有内容的访问。

## 如何查看权限

- 使用 `ls -l` 查看文件和目录的权限。

- 为了查看权限，使用 `ls -l`。

```bash
student@krosum ~$ ls -l
-rw-r--r-- 1 student 47 Mar 20 20:59 result.log
```
