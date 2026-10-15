
```
#report_url=stderr

#NOT IMPLEMENTED report_url=mailto:root@foo.com

#report_url=file:/tmp/some_file.txt

#NOT IMPLEMENTED report_url=syslog:LOG_AUTH

report_url=stdout

# Here are all the things we can check - these are the default rules

#

#p:  permissions

#i:  inode

#n:  number of links

#u:  user

#g:  group

#s:  size

#b:  block count

#m:  mtime

#a:  atime

#c:  ctime

#S:  check for growing size

#md5: md5 checksum

#sha1: sha1 checksum

#rmd160: rmd160 checksum

#tiger: tiger checksum

#R:  p+i+n+u+g+s+m+c+md5

#L:  p+i+n+u+g

#E:  Empty group

#?:  Growing logfile p+u+g+l+n+S

# You can also create custom rules - my home made rule definition

# goes like this

#

MyRule = p+i+n+u+g+s+b+m+c+md5+sha1

# Next decide what directories/files you want in the database

/etc p+i+u+g      #check only permissions, inode, user and group for etc

/bin MyRule       # apply the custom rule to the files in bin

/sbin MyRule      # apply the same custom rule to the files in sbin

/var MyRule

!/var/log/*       # ignore the log dir it changes too often

!/var/spool/*     # ignore spool dirs as they change too often

!/var/adm/wtmp$     # ignore the file /var/adm/wtmp

!/var/cron/log/*   #ignore /var/cron/log

/opt/sfw MyRule    # Solaris specific

/usr/openwin/bin MyRule  # Solaris specific

/usr/dt/bin MyRule  # Solaris specific

/usr/ccs/bin MyRule  # Solaris specific

/usr/ucb MyRule     # Solaris specific

#EOF
```

您可以使用 `/usr/local/doc/aide/aide.conf` 中的示例作为起点，但提到的文件不应直接用作配置文件。它只是一个示例。您可以使用清单 7.7 中的示例作为需要更改内容的指南，但应谨慎使用，因为并非所有修改都适用于所有系统。这意味着并非所有修改在所有系统上都有意义。清单 7.7 中配置中的一些条目以粗体显示；这些需要进一步解释。条目 `@define TOPDIR /HO/aid` 定义了 `aide` 的基本目录。条目 `database=file:@{TOPDIR}/aide.db` 和 `database_out=file:@{TOPDIR}/aide.db.new` 分别搜索现有数据库并在指定目录中创建新数据库。条目 `MyRule = p+i+n+u+g+s+b+m+c+md5+sha1` 是一个定义的规则，可能有点偏执。它运行以下测试：检查权限；`i` 指向相关文件的 inode；`n` 链接数；`u` 文件的所有者，`g` 文件所属的组；`s` 文件的大小；`b` 文件占用的块数；`m` 文件最后修改的日期；`c` 文件最后修改的时间；`md5` 创建 md5 校验和；`sha1` 创建 sha1 校验和。没有绝对的控制，但此规则应涵盖几乎所有情况。条目 `!/var/log/*` 指示程序忽略 `/var` 中的 log 子目录。

您只需将 `aide` 可执行文件和修改后的配置文件 `aide.conf` 存储在 `TOPDIR` 指向的位置。然后您需要使用程序的 `--init` 选项创建初始数据库，如清单 7.8 所示。

### LISTING 7.8 Creating the Initial Database

```
# ls

aide aide.conf bu

# ./aide --init -c aide.conf

# ls -l

total 2443

-rwxr-xr-x 1 root other 1093216 Sep 16 2003 aide

-rw-r--r-- 1 root other 2048 Sep 17 2003 aide.conf

-rw------- 1 root other 1380792 Aug 31 20:06 aide.db.new

#
```

`-c` 选项指向当前目录中的配置文件。程序根据名为 `aide.db.new` 的配置文件中的条目创建了一个新的数据库。数据库中存储的信息是检查所指示目录的所有检查的基础。你需要将此数据库的名称更改为 `aide.db`，如配置文件中所示。

如果你想对配置文件中指示的目录运行检查，则使用如 7.9 节所示的 `--check` 选项。

## 7.9 节 检查目录是否发生变化

```
# ./aide --check -c aide.conf

AIDE found differences between database and filesystem!!

Start timestamp: 2004-08-31 22:04:24

Summary:

Total number of files=3804, added files=1, removed files=0, changed files=1

Added files:

added:/opt/sfw/bin/test_whoami

Changed files:

changed:/opt/sfw/bin

Detailed information about changes:

Directory: /opt/sfw/bin

Mtime  : 2004-08-20 15:35:29        , 2004-08-31 22:03:24

Ctime  : 2004-08-20 15:35:29        , 2004-08-31 22:03:24
```

7.9 节中的输出表明在 `/opt/sfw/bin` 中发现了一个名为 `test_whoami` 的新文件，并报告了修改发生的时间和日期。

如果你应该对该系统应用补丁或更新，或者应该安装了新软件，那么你也需要使用 `-update` 选项更新数据库。如果使用此选项更新数据库，`aide` 会报告自上次运行以来更改的所有文件和目录，如 7.10 节所示。

## 7.10 节 更新 aide 数据库

```
# ./aide --update -c aide.conf

AIDE found differences between database and filesystem!!

Start timestamp: 2004-08-31 22:12:08

Summary:

Total number of files=3804, added files=1, removed files=0, changed files=1
```

```
Added files:

added:/opt/sfw/bin/test_whoami

Changed files:

changed:/opt/sfw/bin

Detailed information about changes:

Directory: /opt/sfw/bin

Mtime  : 2004-08-20 15:35:29      , 2004-08-31 22:03:24

Ctime  : 2004-08-20 15:35:29      , 2004-08-31 22:03:24

# ./aide --check -c aide.conf

#
```
