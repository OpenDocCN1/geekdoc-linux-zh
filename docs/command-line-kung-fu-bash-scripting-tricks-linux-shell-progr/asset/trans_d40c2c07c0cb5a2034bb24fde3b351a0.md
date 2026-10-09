
## 删除空目录

如果你需要清理空目录，`find` 命令可以轻松完成这项任务。使用 `-type d` 选项查找所有目录，配合 `-empty` 选项仅包含空目录，最后使用 `-delete` 选项删除这些目录。

```bash
$ mkdir -p testing/{1..4}
$ ls testing/
1 2 3 4
$ find . -type d -empty -delete
$ ls testing/
ls: cannot access testing/: No such file or directory
$
```

## 打印包含指定字符串的文件列表

要获取包含特定字符串的文件列表，请在使用 `grep` 时加上 `-r`（递归）和 `-l`（列出匹配的文件）选项。

```bash
$ sudo grep -rl jim /var/log
/var/log/audit/audit.log.1
/var/log/secure-20140406
/var/log/secure
```

## 易于阅读的递归文件列表

`ls` 命令有一个递归选项，但我发现阅读 `find` 命令的输出更容易消化，尤其是当文件和目录数量很多时。使用 `find` 的优势在于它显示每个文件的完整路径，而 `ls` 则不然。

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

迟早你会收到或下载一个使用 CR（回车）和 LF（换行）字符对来终止行结束的文件。这类文件是 Windows/DOS 格式的。类 Unix 操作系统仅使用 LF 字符来终止行。有时这会导致问题。要将文件转换为类 Unix 格式，请使用 `dos2unix`。要检查行终止字符，请使用 "cat -A" 或 "file" 命令。

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

如果你想返回到上一个工作目录，请使用 "cd -"。环境变量 OLDPWD 保存了你最近一个目录位置的路径。"cd -" 等同于 "cd $OLDPWD"。

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

