

## 命令行功夫

默认情况下，只会替换 `<string1>` 的第一次出现。若要替换所有出现，请附加 `&`。除非使用 `&`，否则可以省略结尾的脱字符符号。

```
$ grpe json /etc/passwd
-bash: grpe: command not found
$ ^pe^ep
$ grep root /etc/passwd
$ ^y
grep root /etc/passwd
root:x:0:0:root:/root:/bin/bash
operator:x:11:0:operator:/root/sbin/nologin
$ grep cannon /etc/passwd ; ls -ld /home/cannon
ls: cannot access /home/cannon: No such file or directory
$ ^cannon~cannon~^&
grep cannon /etc/passwd ; ls -ld /home/cannon
cannon:x:1001:1001::/home/cannon:/bin/sh
drwxr-xr-x 2 cannon ball 4096 Apr  7 00:22 /home/cannon
```

### 引用当前命令中的某个词并重新使用它

```
$ !#:N
```

`!#` 事件指示符代表当前命令行，而 `:N` 词指示符代表命令行上的一个词。词引用是基于零的，因此第一个词（几乎总是命令）是 `:0`，第二个词（或命令的第一个参数）是 `:1`，等等。

```
$ mv Working-with-Files.pdf Chapter-18-!:1
mv Working-with-Files.pdf Chapter-18-Working-with-Files.pdf
```

### 保存你的命令行会话副本

```
$ script
```

如果你想记录屏幕上看到的内容，请使用 `script` 命令。`script` 命令会捕获打印在终端上的所有内容，并将其保存到一个文件中。你可以为 `script` 提供文件名作为参数，或者让它创建名为 `typescript` 的默认文件。

```
$ script
Script started, file is typescript
$ cd /usr/local/bin
$ sudo ./upgradedb.sh
sudo password for jason:
Starting database upgrade.
...
Database upgrade complete.
$ exit
exit
Script done, file is typescript
$ cat typescript
Script started on Wed 09 Apr 2014 06:30:58 PM EDT
$ cd /usr/local/bin
$ sudo ./upgradedb.sh
sudo password for jason:
Starting database upgrade.
...
Database upgrade complete.
$ exit
exit
Script done on Wed 09 Apr 2014 06:31:44 PM EDT
$
```

### 找出你最常使用的命令

```
$ history | awk '{print $2}' | sort | uniq -c | sort -rn | head
```

要获取 shell 历史记录中使用最频繁的前十个命令列表，请使用以下命令。

```
$ history | awk '{print $2}' | sort | uniq -c | sort -rn | head
      61 ls
      45 cd
      40 cat
      31 vi
      24 ip
      22 sudo
      22 ssh
      22 ll
      19 rm
      17 find
$
```

### 清除你的 Shell 历史记录

```
$ history -c
```

要清除你的 shell 历史记录，请使用 `history` 命令的 `-c` 选项。

```
$ history | tail -5
    966  ls -lR Music/
    967  find Music/ -type f -is
    968  dstat
    969  sudo vi /etc/motd
    970  cd ..
    971  sudo du -s /home/* | sort -n
$ history -c
$ history
            1  history
$  
```

## 文本处理和操作

### 去除注释和空行

```
$ grep -E -v "^#|^$" file
```

要从配置文件中去除所有噪音，请去掉注释和空行。这两个正则表达式（regular expressions）可以做到。`"^#"` 匹配以 `"#"` 开头的所有行。`"^$"` 匹配所有空行。`grep` 的 `-E` 选项允许我们使用正则表达式，而 `-v` 选项反转匹配结果。

```
[jason@www conf]$ grep -E -v '^#|^$' httpd.conf | head
ServerTokens OS
ServerRoot "/etc/httpd"
PidFile run/httpd.pid
Timeout 60
KeepAlive Off
MaxKeepAliveRequests 100
KeepAliveTimeout 15
<IfModule prefork.c>
StartServers          8
MinSpareServers      5
[jason@www conf]$ 
```

### 使用 Vim 通过网络编辑文件

```
$ vim scp://remote-host//path/to/file
$ vim scp://remote-user@remote-host//path/to/file
```

如果你想通过 SSH 使用 `vim` 编辑文件，可以让它完成来回复制文件的繁重工作。

```
$ vim scp://linuxserver//home/jason/notes.txt
```

### 以表格形式显示输出

```
$ alias ct='column -t'
$ command | ct
```

使用 `column` 命令将文本格式化为多列。通过使用 `-t` 选项，`column` 会计算输入包含的列数，并创建一个具有该列数的表格。这确实可以使许多命令的输出更易读。我发现自己如此频繁地使用它，以至于我为该命令创建了一个别名。

```
$ alias ct='column -t'
$ echo -e 'one two\nthree four'
one two
three four
$ echo -e 'one two\nthree four' | ct
one    two
three four
$ mount -t ext4
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$ mount -t ext4 / ct
/dev/vda2 on / type ext4 (rw)
/dev/vda1 on /boot type ext4 (rw)
$
```

### 获取输出行中的最后一个单词

```
$ awk '{print $NF}' file
$ cat file | awk '{print $NF}'
```

你可以使用 `$FIELD_NUMBER` 表示法让 `awk` 打印字段。要打印第一个字段，使用 `$1`；要打印第二个，使用 `$2`，等等。但是，如果你不知道字段的数量，或者不想去计算它们，请使用 `$NF`，它代表字段的总数。`awk` 以空格分隔字段，但你可以使用 `-F` 参数来改变这种行为。以下是如何打印系统中正在使用的所有 shell。使用冒号作为字段分隔符，然后打印最后一个字段。

```
$ awk -F: '{print $NF}' /etc/passwd | sort -u
```

如果你想显示系统中每个用户的 shell，可以这样做。

```
$ awk -F: '{print $1,$NF}' /etc/passwd | sort | column -t
adm /sbin/nologin
apache /sbin/nologin
avahi-autoipd /sbin/nologin
bin /sbin/nologin
bob /bin/bash
...
```

### 使用 Less 查看彩色输出

```
$ ls --color=always | less -R
$ grep --color=always file | less -R
```

一些 Linux 发行版为 `ls` 和 `grep` 创建带有 `--color=auto` 选项的别名。这导致仅当输出发送到终端时才使用颜色。当你将 `ls` 或 `grep` 的输出通过管道传输时，不会发出颜色代码。你可以使用 `--color=always` 强制 `ls` 或 `grep` 始终显示颜色。要让 `less` 命令显示产生颜色的原始控制字符，请使用 `-R` 选项。

```
$ grep --color=always -l bob /etc/passwd | less -R
$ ls -l --color=always /etc | less -R
```

### 在管道传输到 Grep 时保留颜色

```
$ ls -l --color=always | grep --color=never string
```

如果你将有颜色的输入通过管道传输到 `grep`，并且 `grep` 是带有 `--color=auto` 选项的别名，`grep` 将丢弃输入中的颜色并突出显示被 grep 的字符串。为了保留有颜色的输入，使用 `--color=never` 选项强制 `grep` 不使用颜色。

```
$ ls -l --color=always *.mp3 | grep --color=never jazz
-rw-r--r--- 1 jason jason 21267371 Feb 16 11:12 jazz-album-1.mp3
```

### 使用 Sudo 将文本追加到文件

```
$ echo text | sudo tee -a file
```

如果你曾尝试在 `"sudo echo"` 命令后使用重定向将文本追加到文件，你会很快发现这不起作用。发生的情况是 `echo` 语句以 root 身份执行，但重定向以你自己身份发生。

```
$ sudo echo "PRODUCTION Environment" >> /etc/motd
bash: /etc/motd: Permission denied
```

幸运的是，你可以将 `sudo` 与 `tee` 命令结合使用来将文本追加到文件。

```
$ echo "PRODUCTION Environment" | sudo tee -a /etc/motd
PRODUCTION Environment
```

### 更改字符串的大小写

```
$ tr [:upper:][:lower:]
$ tr [:lower:][:upper:]
```

当你需要更改字符串的大小写时，请使用 `tr` 命令。你可以为 `tr` 提供范围，如 `"tr a-z A-Z"`，或者使用 `"tr [:lower:][:upper:]"`。

```
$ ENVIRONMENT=PRODUCTION
$ DIRECTORY=$(echo $ENVIRONMENT | tr [:upper:][:lower:])
$ echo $ENVIRONMENT | sudo tee -a /etc/motd
$ tail -1 /etc/motd
PRODUCTION
$ sudo mkdir /var/www/$DIRECTORY
$ sudo tar zxf wwwfiles.tgz -C /var/www/$DIRECTORY
```

### 以人类可读格式显示你的命令搜索路径

```
$ echo $PATH | tr ':' '\n'
```

读取冒号分隔的项目列表对我们人类来说不像对计算机那样容易。要用换行符替换冒号，请使用 `tr` 命令。

```
$ echo $PATH
/usr/bin:/bin:/usr/local/bin:/bin:/usr/bin:/usr/local/sbin:/usr/sbin:/sbin

$ echo $PATH | tr ':' '\n'
/usr/bin
/bin
/usr/local/bin
/bin
/usr/bin
/usr/local/sbin
/usr/sbin
/sbin
```

### 在没有 ... 的情况下从命令行创建文本文件

