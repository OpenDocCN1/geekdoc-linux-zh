
## 示例 17-15 使用 make 安装 logcheck

```
# make linux
make[1]: Entering directory `/usr/local/src/logcheck/logcheck-1.1'
Making linux
cp -o -p .//src/logtail .//src/logtail.c
Creating temp directory /usr/local/etc/tmp
Setting temp directory permissions
chmod 700 /usr/local/etc/tmp
Copying files
cp .//systems/linux/logcheck.hacking /usr/local/etc
cp .//systems/linux/logcheck.violations /usr/local/etc
cp .//systems/linux/logcheck.violations.ignore /usr/local/etc
cp .//systems/linux/logcheck.ah /usr/local/etc
cp .//src/logtail /usr/local/bin
Setting permissions
chmod 700 /usr/local/etc/logcheck.sh
chmod 700 /usr/local/bin/logtail
chmod 600 /usr/local/etc/logcheck.violations.ignore
chmod 600 /usr/local/etc/logcheck.violations
chmod 600 /usr/local/etc/logcheck.hacking
chmod 600 /usr/local/etc/logcheck.ignore
Done. Don't forget to set your crontab.
make[1]: Leaving directory `/usr/local/src/logcheck/logcheck-1.1'
```

tion. 如您所见，如果您选择修改分发版 `logcheck.*` 配置文件，可以使用通配符 * 来匹配行中的任意模式。

**logcheck.hacking** logcheck.hacking 文件是第一个被读取的文件。此文件应包含代表实际黑客活动的模式。日志文件中匹配这些模式之一的行将报告在报告的第一个部分中，如果您看到它们，应进行调查。原始分发的 logcheck.hacking 文件如示例 17-16 所示。请注意，此文件中的关键字将以不区分大小写的方式进行搜索。

**logcheck.violations** 在报告黑客活动的模式之后，logcheck 寻找匹配 logcheck.violations 文件内容的模式。此文件中的模式通常代表负面活动，但不一定是黑客攻击的特征。匹配这些模式的日志条目（如果有的话）将在报告中以“Security Violations”为标题进行报告。分发的 logcheck.violations 文件如示例 17-17 所示。

### 示例 17-16 logcheck.hacking 模式文件

```
"wiz"
"Wiz"
"debug"
"DEBUG"
ATTACK
nested
VRFY lobs
VRFY decode
VRFY udecode
VRFY lp
VRFY demo
VRFY guest
VRFY root
VRFY uucp
VRFY oracle
VRFY sybase
VRFY games
vrfy hbs
vrfy decode
vrfy udecode
vrfy lp
vrfy demo
vrfy guest
vrfy root
vrfy uucp
vrfy oracle
vrfy sybase
vrfy games
expn decode
expn udecode
expn wheel
expn root
EXP N decode
EXP N udecode
EXP N wheel
EXP N root
LOGIN root REFUSED
rlogind.*: Connection from .* on illegal port
rshd.*: Connection from .* on illegal port
sendmail.*: user .* attempted to run daemon
uuico.*: refused connect from .*
tftp.*: refused connect from .*
login.*: *LOGIN FAILURE.* FROM *root
login.*: *LOGIN FAILURE.* FROM *guest
login.*: *LOGIN FAILURE.* FROM *bin
login.*: *LOGIN FAILURE.* FROM *uucp
login.*: *LOGIN FAILURE.* FROM *adm
login.*: *LOGIN FAILURE.* FROM *hbs
login.*: *LOGIN FAILURE.* FROM *games
login.*: *LOGIN FAILURE.* FROM *sync
login.*: *LOGIN FAILURE.* FROM *oracle
login.*: *LOGIN FAILURE.* FROM *sybase
kernel: Oversized packet received from
attacker!
```

### 示例 17-17 logcheck.violations 模式文件

```
!=
-ERR Password
ATTACK
BAD
CWD etc
DEBUG
EXP N
FAILURE
ILLEGAL
LOGIN FAILURE
LOGIN REFUSED
PERMITTED
REFUSED
RETR group
RETR passwd
RETR pwd.db
ROOT LOGIN
SITE EXEC
VRFY
"WIZ"
admin
alias database
abuse
deny
deny host
expp
failed
illegal
kernel: Oversized packet received from
nested
permitted
reject
rexec
rshd
securityalert
sender
shutwarn
smrsh
su root
su:
sucked
unapproved
vrfy
attackalert
```

与 logcheck.hacking 一样，此文件中的关键字将以不区分大小写的方式进行搜索。

**logcheck.violations.ignore** 可能会出现这样的情况：在违规部分找到的模式既出现在您希望看到的信息中，也出现在您不希望看到的信息中。logcheck.violations.ignore 模式文件提供了灵活性，可以忽略 logcheck.violations 中某些包含模式的条目。

分发的 logcheck.violations.ignore 文件中只有一个条目。它用于忽略因 logcheck.violations 而捕获的信息。如果您修改此文件，请确保忽略的模式尽可能具体，以免意外忽略其他条目。

分发的 logcheck.violations.ignore 文件包含以下行：

```
state=Deferred
```

对于此文件中的条目，大小写是重要的。

**logcheck.ignore** 这是最后检查的模式文件。如果日志条目尚未被之前的模式文件（logcheck.hacking、logcheck.violations 或 logcheck.violations.ignore）匹配，除非它匹配此文件中的模式，否则该条目将被报告。在添加要忽略的模式时，请尽可能具体，以免意外忽略您可能想查看的内容。示例 17-18 展示了分发版 logcheck.ignore 中包含的模式。此文件中的模式将区分大小写进行检查。

### 示例 17-18 logcheck.ignore 配置文件

```
authsrv.*AUTHENTICATE

cron.*CMD

cron.*RELOAD

cron.*STARTUP

ftp-gw.*: exit host

ftp-gw.*: permit host

ftpd.*ANONYMOUS FTP LOGIN

ftpd.*FTP LOGIN FROM

ftpd.*retrieved

ftpd.*screed

http-gw.*: exit host

http-gw.*: permit host

mail.local

named.*lame delegation

named.*Response from

named.*answer queries

named.*points to a CNAME

named.*reloading

named.*starting

netacl.*: exit host

netacl.*: permit host

popper.*Unable

popper: - ERR POP server at

popper: -ERR Unknown command: "uid".

qmail.*new msg

qmail.*info msg

qmail.*starting delivery

qmail.*delivery

qmail.*end msg

rlogin-gw.*: exit host

rlogin-gw.*: permit host

sendmail.*User Unknown

sendmail.*User Unknown

sendmail.*alias database.*rebuild

sendmail.*aliases.*longest

sendmail.*from=

sendmail.*lost input channel

sendmail.*message-id=

sendmail.*putcounsg

sendmail.*return to sender

sendmail.*return to sender

sendmail.*stat=

sendmail.*timeout waiting

smap.*host=

smapd.*daemon running

smqpd.*daemon running

smqpd.*delivered

smqpd.*delivered

telnetd.*utlop: peer died

tn-gw.*: exit host

tn-gw.*: permit host

x-gw.*: exit host

x-gw.*: permit host

xntpd.*Previous time adjustment didn't complete

xntpd.*time reset

root 1
```

### logcheck 输出

第一次运行 logcheck 时，它将完整读取所有日志文件（即配置要处理的文件）。`logtail` 程序将为每个日志文件在同一目录下创建一个 `logfile.offset` 文件。每个日志文件中的每个事件都将解析并与 `logcheck.` 模式文件中的模式进行比较；所有未被忽略的输出（如果有）将发送给 `logcheck.sh` 文件中 `SYSADMIN` 变量列出的用户。

在后续运行中，`logcheck` 将读取 `logfilename.offset` 文件并忽略日志文件中已处理的部分。所有新事件都将解析，如果有不应被忽略的条目，将发送报告。

`logcheck` 输出的示例如示例 17-19 所示。

### 示例 17-19 示例 logcheck 报告

```
Active System Attack Alerts
==========================
Mar 2 04:01:45 topcat sendmail[1682]: NOQUEUE: "wiz" command from roadrunner.mydomain.com (123.45.123.45) (123.45.123.45).
Security Violations
==================
Mar 2 04:01:08 topcat sshd[7589]: refused connect from 123.45.123.45
Mar 2 04:01:25 topcat sshd[7601]: refused connect from 123.45.123.45
Unusual System Events
====================
Mar 3 04:02:01 topcat syslogd 1.3:3: restart.
Mar 3 04:02:01 topcat syslogd 1.3:3: restart.
Mar 3 04:02:01 topcat syslogd 1.3:3: restart.
Mar 3 04:04:45 topcat suid:  joe : TTY=ttyp5 ; PWD=/home/joe; USER=root ; COMMAND=/usr/bin/chmod 4755 sh
Mar 3 04:08:29 topcat portmap[22220]: connect from 123.45.123.45 to callit (ypserv)
```

### 排查 logcheck 故障

如果您没有收到报告，请验证 `filenames.offset` 文件是否在与您的日志文件相同的目录中创建。如果没有，说明 `logtail` 存在问题。请确保它已安装且 `logcheck.sh` 中的路径指向正确的位置。验证事件是否实际被记录（尝试使用 `logger` 程序）。从命令行运行 `logcheck` 以验证它是否将邮件发送给正确的人员。请验证您是否记得添加一个 cron 任务来自动运行 `logcheck`。

### 总结

良好的日志文件管理是系统安全的重要组成部分。我们在本章中讨论的工具将有助于确保您的文件在需要时完整可用，并且您能及时得到问题警报。
