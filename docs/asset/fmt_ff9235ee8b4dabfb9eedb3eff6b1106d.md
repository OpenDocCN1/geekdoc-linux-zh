
## 查看目录内容

`ls` 命令用于列出文件和目录。使用 `-l` 选项以长格式显示详细信息，使用 `-R` 选项递归列出子目录内容。

```bash
$ ls -lR Music/
Music/:
total 4
drwxr-xr-x. 2 jason jason 4096 Feb 22 12:40 jazz
Music/jazz:
total 20932
-rw-r--r--. 1 jason jason       79496 Feb 22 12:40 giant-steps.mp3
-rw-r--r--. 1 jason jason 21267371 Feb 16 11:12 jazz-album-1.mp3
-rw-r--r--. 1 jason jason       79496 Feb  3 18:13 john-coletrene.mp3

$ find Music/ -type f -ls
397966 20772 -rw-r--r--   1 jason jason 21267371 Feb 16 11:12 Music/jazz/jazz-album-1.mp3
396787    80 -rw-r--r--   1 jason jason    79496 Feb 22 12:40 Music/jazz/giant-steps.mp3
132464    80 -rw-r--r--   1 jason jason    79496 Feb  3 18:13 Music/jazz/john-coletrene.mp3
```

## 以树状格式查看文件和目录

`tree` 命令以树状格式显示文件和目录。如果你只想查看目录结构，请使用 `-d` 选项。要限制树的深度，请使用 `-L` 选项并跟随一个数字。

```bash
$ tree Music/
Music/
└── jazz
    ├── giant-steps.mp3
    │
    ├── jazz-album-1.mp3
    │
    └── john-coletrene.mp3

1 directory, 3 files

$ tree -d Music/
Music/
└── jazz

1 directory

$ tree -d /var | head
/var
├── account
├── cache
│
└── fontconfig
    |
    └── gdm
        |
        ├── adminuser
        |
        └── jason

$ tree -dL 1 /var
/var
├── account
├── cache
├── crash
├── db
├── empty
├── ftp
├── games
├── gd
├── lib
├── local
├── lock
├── log
├── mail -> spool/mail
├── nis
├── opt
├── preserve
├── run
├── spool
├── tmp
├── www
└── yp
$
```

## 在多个文件中替换字符串

如果你有一些嵌入在多个文件中的信息需要修改，请结合使用 `find` 命令和 `sed`。`sed` 的 `-i` 选项表示执行就地编辑。你可以为 `-i` 指定一个扩展名，以便在编辑前创建文件的备份。传递给 `sed` 的命令指示它全局将“replacement”替换为“string”。全局替换会在所有位置执行替换。普通替换仅替换行中的第一个出现位置。

在这个例子中，托管软件仓库的服务器正在被替换。使用以下单行命令，所有“thor”的出现位置都被替换为“loki”。

```bash
$ grep -r thor .
./deploy-il.sh:REPO_SERVER="thor.company.com"
./deploy-ca.sh:REPO_SERVER="thor.company.com"
./deploy-fl.sh:REPO_SERVER="thor.company.com"
./deploy-ny.sh:REPO_SERVER="thor.company.com"

$ find . -type f -exec sed -i.bak 's/thor/loki/g' { } \;

$ grep -r thor .
./deploy-fl.sh.bak:REPO_SERVER="thor.company.com"
./deploy-il.sh.bak:REPO_SERVER="thor.company.com"
./deploy-ny.sh.bak:REPO_SERVER="thor.company.com"
./deploy-ca.sh.bak:REPO_SERVER="thor.company.com"

$ grep -r loki .
./deploy-il.sh:REPO_SERVER="loki.company.com"
./deploy-ca.sh:REPO_SERVER="loki.company.com"
./deploy-fl.sh:REPO_SERVER="loki.company.com"
./deploy-ny.sh:REPO_SERVER="loki.company.com"
$
```

## 从文件中提取第 N 行

要从文件中提取特定行，请告诉 `awk` 打印匹配行号的行。当你遇到脚本中的错误时，这会很有用。要查看脚本在该行具体做了什么，请使用 `awk`。

```bash
$ ./deploy.sh
./deploy.sh: line 74: /usr/local/bin/patch: No such file or directory

$ awk 'NR==74' deploy.sh
/usr/local/bin/patch $NEW_HOST
$
```

## 将文本文件从 Windows 格式转换为 Linux 格式，反之亦然

迟早你会收到或下载一个使用 CR（回车）和 LF（换行）字符对来终止行结束的文件。这类文件是 Windows/DOS 格式的。类 Unix 操作系统仅使用 LF 字符来终止行。有时这会导致问题。要将文件转换为类 Unix 格式，请使用 `dos2unix`。要检查行终止字符，请使用 `cat -A` 或 `file` 命令。

```bash
$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl^M$
print "This is a cross-platform perl script!\n"^M$

$ ./from-my-windows-buddy.pl
-bash: ./from-my-windows-buddy.pl: /usr/bin/perl^M: bad interpreter: No such file or directory

$ dos2unix from-my-windows-buddy.pl
dos2unix: converting file from-my-windows-buddy.pl to UNIX format ...

$ cat -A from-my-windows-buddy.pl
#!/usr/bin/perl$
print "This is a cross-platform perl script!\n"$

$ ./from-my-windows-buddy.pl
This is a cross-platform perl script!

$ file other-file.txt
other-file.txt: ASCII text, with CRLF line terminators

$ dos2unix other-file.txt
dos2unix: converting file other-file.txt to UNIX format ...

$ file other-file.txt
other-file.txt: ASCII text
```

另一方面，如果你将 Linux 主机上创建的文件发送给某人在 Windows 上用记事本打开，他们只会看到一行很长的文本。使用 `unix2dos` 命令将文件转换为 Windows/DOS 格式。

```bash
$ file report-for-ceo.txt
report-for-ceo.txt: ASCII text

$ unix2dos report-for-ceo.txt
unix2dos: converting file report-for-ceo.txt to DOS format ...

$ file report-for-ceo.txt
report-for-ceo.txt: ASCII text, with CRLF line terminators
$
```

## 杂项

### 返回前一个工作目录

如果你想返回到上一个工作目录，请使用 `cd -`。环境变量 `OLDPWD` 保存了你最近一个目录位置的路径。`cd -` 等同于 `cd $OLDPWD`。

```bash
$ cd /etc/httpd/conf.d
$ grep ^SSLCert ssl.conf
SSLCertificateFile /etc/pki/tls/certs/localhost.crt
SSLCertificateKeyFile /etc/pki/tls/private/localhost.key

$ cd /etc/pki/tls/certs/
$ ls
ca-bundle.crt ca-bundle.trust.crt localhost.crt
make-dummy-cert Makefile renew-dummy-cert

$ cd -
/etc/httpd/conf.d
```

### 在命令行中搜索维基百科

如果你需要快速查找某个主题的信息，可以使用 DNS 搜索维基百科。该名称服务器会以 TXT 记录的形式返回维基百科文章的摘要。

```bash
$ dig +short txt <string>.wp.dg.cx
$ host -t txt <string>.wp.dg.cx
```

```bash
$ dig +short txt linux.wp.dg.cx
"Linux is a Unix-like computer operating system
assembled under the model of free and open source
software development and distribution. The defining
component of Linux is the Linux kernel, an operating
system kernel first released 5 October 1991 by Linus
Torvalds. http://en.wikipedia.org/wiki/Linux"
$ host -t txt bash_shell.wp.dg.cx
bash_shell.wp.dg.cx descriptive text "Bash is a Unix
shell written by Brian Fox for the GNU Project as a free software replacement for the Bourne shell (sh). Bash is a command processor, typically run in a text window, allowing the user to type commands which cause actions. Bash can also read commands from a file, called a script. Like all Unix shells, it supports filename wildcarding, piping, here documents...
http://en.wikipedia.org/wiki/Bash_(Unix_shell)"
```

你可以创建一个小型 shell 脚本，以免每次都需要输入完整的 DNS 查询语句。

```bash
$ echo -e '#!/bin/bash\ndig +short txt ${1}.wp.dg.cx' > wikidig

$ chmod 755 !$
chmod 755 wikidig

$ ./wikidig ubuntu_operating_system
"Ubuntu As of 2012, according to online surveys, Ubuntu is the most popular Linux distribution on desktop/laptop personal computers, and most Ubuntu coverage focuses on its use in that market. However, it is also popular on servers and for cloud computing.
http://en.wikipedia.org/wiki/Ubuntu_(operating_system)"
```

或者，你可以创建一个函数并将其添加到你的点文件（dot files）中。

```bash
$ echo 'wikidig(){ dig +short txt ${1}.wp.dg.cx; }' >> .bash_profile
$ . ./.bash_profile
```

```bash
$ wikidig jazz
"Jazz is a musical style that originated at the beginning of the 20th century in black communities in the Southern United States. It was born out of a mix of African and European music traditions. Its African pedigree is evident in its use of blue notes, improvisation, polyrhythms, syncopation and the swung note. From its early development until the present day jazz has also…
http://en.wikipedia.org/wiki/Jazz"
```

### 让非交互式 Shell 会话表现出与交互式会话相同的行为

在 `~/bashrc` 中进行任何自定义设置。`~/bash_profile` 的内容如下：

```bash
if [ -f ~/.bashrc ]; then
source ~/.bashrc
fi
```

当你通过交互式方式登录与仅仅连接以运行单个命令时，Shell 的行为略有不同。`.profile` 或 `.bash_profile` 的内容仅会在交互式会话中执行。如果你没有意识到这种细微差异，可能会导致你困惑于为什么某事在你登录并执行命令时完美工作，而在你仅仅通过 `ssh` 连接运行相同命令时却不工作。你可以通过让交互式和非交互式会话表现一致来省去一些麻烦。为此，请配置 `.bash_profile` 以引用 `.bashrc`，并将所有配置放在 `.bashrc` 中。

下面是一个示例，以便更好地说明交互式和交互式 shell 之间的区别。例如，如果你在 `~/bash_profile` 中为 `ll` 定义了一个别名，它在交互式会话期间会有效，但在非交互式会话期间则不可用。

#### 交互式

```bash
mac:~ jason $ ssh linuxserver
jason@linuxserver:~$ uptime
    11:49:16 up  97 days,  2:59,   5 users,  load average:
    0.15, 0.25, 0.31
jason@linuxserver:~$ ll
-rw-r--r-- 1 jason jason 221 Nov 13 11:30 file.txt
jason@linuxserver:~$ exit
logout
Connection to 10.0.1.9 closed.
mac:~ jason $
```

#### 非交互式

```bash
mac:~ jason$ ssh linuxserver uptime
    11:49:16 up 97 days, 2:59, 5 users, load average:
    0.15, 0.25, 0.31
mac:~ jason$ ssh linuxserver ll
bash: ll: command not found
mac:~ jason$
```

```bash
$ cat .bash_profile
# Put our settings in .bashrc so we have the same
environment for login and non-login shells.
if [ -f ~/.bashrc ]; then
    source ~/.bashrc
fi
```

```bash
$ cat .bashrc
alias ll='ls -l'
HISTFILESIZE=5000
export HISTFILESIZE
```

### 让你的计算机与你对话

```bash
$ espeak -f file
$ echo text | espeak
```

`Espeak` 将文本转换为语音。你可以向 `espeak` 提供一个文件或通过管道输入文本让它朗读。如果你有长时间运行的任务，可以让你的计算机在完成时告知你，如下例所示。

```bash
$ for VIDEO in $(ls *.mp4 | sed 's/\.mp4//')
> do
>         avconv -v quiet -i $VIDEO.mp4 $VIDEO.mp3
> done; echo "File conversions complete." | espeak
```

### 显示不同时区的当前日期和时间

```bash
$ TZ=<TIMEZONE> date
```

`TZ` 环境变量指定时区。如果你想知道特定时区的时间，请在 `date` 命令前加上环境变量和时区。
