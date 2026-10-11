
`daemon:x:2:2:daemon:/sbin:/sbin/nologin`

`adm:x:3:4:adm:/var/adm:/sbin/nologin`

`lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin`

### 按 IP 地址对 `/etc/hosts` 文件进行排序

```
$ sort -t . -k 1,1n -k 2,2n -k 3,3n -k 4,4n /etc/hosts
```

`127.0.0.1 localhost.localdomain localhost`

`192.168.100.101 dev-db.thegeekstuff.com dev-db`

`192.168.100.102 prod-db.thegeekstuff.com prod-db`

`192.168.101.20 dev-web.thegeekstuff.com dev-web`

`192.168.101.21 prod-web.thegeekstuff.com prod-web`

### 将 `sort` 与其他命令结合使用

- `ps -ef | sort` : 对进程列表的输出进行排序

- `ls -al | sort +4n` : 按文件大小升序列出文件。 即按第 5 个字段排序并先显示最小的文件。

- `ls -al | sort +4nr` : 按文件大小降序列出文件。 即按第 5 个字段排序并先显示最大的文件。

### Hack 24. `uniq` 命令

`uniq` 命令通常与 `sort` 命令结合使用，因为 `uniq` 仅从已排序的文件中删除重复项。 即为了使 `uniq` 正常工作，所有重复条目都应位于相邻行。 以下是一些常见示例。

1. 当你有一个包含重复条目的员工文件时，可以执行以下操作来删除重复项。

```
$ sort namesd.txt | uniq
```

```
$ sort -u namesd.txt
```

2. 如果你想知道有多少行是重复的，请执行以下操作。 以下示例中的第一个字段表示为该特定行找到的重复次数。 因此，在此示例中，以 `Alex` 和 `Emma` 开头的行在 `namesd.txt` 文件中出现了两次。

```
$ sort namesd.txt | uniq -c
```

`2`

`2`

`1`

`1`

`1`

`Alex Jason:200:Sales`

`Emma Thomas:100:Marketing`

`Madison Randy:300:Product Development`

`Nisha Singh:500:Sales`

`Sanjay Gupta:400:Support`

3. 以下仅显示重复的条目。

```
$ sort namesd.txt | uniq -cd
```

`2 Alex Jason:200:Sales`

`2 Emma Thomas:100:Marketing`

### Hack 25. `cut` 命令

`cut` 命令可用于仅显示文本文件或其他命令输出的特定列。

以下是一些示例。

### 从冒号分隔的文件中显示第 1 个字段（员工姓名）

```
$ cut -d: -f 1 names.txt
```

`Emma Thomas`

`Alex Jason`

`Madison Randy`

`Sanjay Gupta`

`Nisha Singh`

### 从冒号分隔的文件中显示第 1 和第 3 个字段

```
$ cut -d: -f 1,3 names.txt
```

`Emma Thomas:Marketing`

`Alex Jason:Sales`

`Madison Randy:Product Development`

`Sanjay Gupta:Support`

`Nisha Singh:Sales`

### 仅显示文件中每行的前 8 个字符

```
$ cut -c 1-8 names.txt
```

`Emma Tho`

`Alex Jas`

`Madison`

`Sanjay G`

`Nisha Si`

### 其他 `cut` 命令示例

- `cut -d: -f1 /etc/passwd` 显示系统中所有用户的 `unix` 登录名。

- `free | tr -s ' ' | sed '/^Mem/!d' | cut -d" " -f2` 显示系统上可用的总内存。

### Hack 26. `stat` 命令

`stat` 命令可用于检查单个文件或文件系统的状态/属性。

显示文件或目录的统计信息。

```
$ stat /etc/my.cnf
```

```
File:
Size:
Device:
Access:
(0/
Access:
Modify:
Change:
`/etc/my.cnf’
346 Blocks: 16 IO Block: 4096regular file
801h/2049dInode: 279856Links: 1
(0644/-rw-r--r--) Uid: (0/root)Gid:
  root)
2009-01-01 02:58:30.000000000 -0800
2006-06-01 20:42:27.000000000 -0700
2007-02-02 14:17:27.000000000 -0800
```

```
$ stat /home/ramesh
```

`File:` `/home/ramesh’`

`Size:` `4096` `Blocks:` `8` `IO Block:`

`4096` `directory`

`Device:` `803h/2051d` `Inode:` `5521409` `Links:` `7`

`Access:` `(0755/drw xr-xr-x)` `Uid:` `( 401/ramesh)` `Gid:` `( `

`401/ramesh)`

`Access:` `2009-01-01 12:17:42.000000000 -0800`

`Modify:` `2009-01-01 12:07:33.000000000 -0800`

`Change:` `2009-01-01 12:07:33.000000000 -0800`

### 使用选项 `-f` 显示文件系统的状态

```
$ stat -f /
```

`File:`

`ID:`

`Blocks:`

`1876998`

`Inodes:`

`"/"`

`0` `Namelen:` `255` `Type:` `ext2/ext3`

`Total:` `2579457` `Free:` `2008027` `Available:`

`  Size:` `4096`

`Total:` `1310720` `Free:` `1215892`

### Hack 27. `diff` 命令

`diff` 命令比较两个不同的文件并报告差异。 输出非常晦涩，不易直接阅读。

语法：`diff [options] file1 file2`

与旧文件相比，我的新文件中修改了什么？

`diff` 命令中的选项 `-w` 将在执行比较时忽略空白。

在以下 `diff` 输出中：

- 行上方 `–`，表示 `diff` 命令中第一个文件（即 `name_list.txt`）发生的更改。

- 行下方 `–`，表示 `diff` 命令中第二个文件（即 `name_list_new.txt`）发生的更改。 属于第一个文件的行以 `<` 开头，第二个文件的行以 `>` 开头。

```
# diff -w name_list.txt name_list_new.txt
```

`2c2,3`

`< John Doe`

`–`

`> John M Doe`

`> Jason Bourne`

### Hack 28. 显示用户的总连接时间

`ac` 命令将显示有关用户连接时间的统计信息。

### 当前登录用户的连接时间

使用选项 `-d`，它将按天分解输出。 在此示例中，我今天已登录系统超过 6 小时。

`12` 月 `1` 日，我登录了大约 `1` 小时。

```
$ ac -d
```

```
Dec 1
Dec 2
Dec 3
Dec 4
Today
total
total
total
total
total
1.08
0.99
3.39
4.50
6.10
```

### 所有用户的连接时间

要显示所有用户的连接时间，请使用 `-p`，如下所示。 请注意，这表示各个用户的累计连接时间。

```
$ ac -p
```

`john`

`madison`

`sanjay`

`nisha`

`  3.64`

`0.06`

`  88.17`

` 105.92`

`45`

`ramesh`

`total 309.21`

`111.42`

### 特定用户的连接时间

要获取特定用户的连接时间报告，请执行以下操作：

```
$ ac -d sanjay
```

`Jul 2`

`Aug 25`

`Sep 3`

`Sep 4`

`Dec 24`

`Dec 29`

`Today`

`total`

`total`

`total`

`total`

`total`

`total`

`total`

`12.85`

`5.05`

`1.03`

`5.37`

`8.15`

`1.42`

`2.95`

## 第 5 章：`PS1`、`PS2`、`PS3`、`PS4` 和 `PROMPT_COMMAND`

### Hack 29. `PS1` - 默认交互提示

如下所示，可以修改 Linux 上的默认交互提示，使其更有用且更具信息性。 在以下示例中，默认的 `PS1` 为 `"\s-\v\$"`，它显示 shell 名称和版本号。 让我们更改此默认行为，以显示用户名、主机名和当前工作目录名称，如下所示。
