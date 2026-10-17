
```
[student@krosum ~]$ ls
Desktop Downloads p1.c process.log Templates
Documents Music Pictures Public Videos
[student@krosum ~]$ ls Desktop
DEM02 ModuleA ModuleB
[student@krosum ~]$ ls -l Desktop
total 0
drwxwxr-x. 2 student student 6 Mar 20 00:08 DEM02
drwxwxrxr-x. 5 student student 33 Mar 20 00:42 ModuleA
drwxwxrxr-x. 5 student student 33 Mar 19 23:54 ModuleB
[student@krosum ~]$
[student@krosum ~]$ ls -d Desktop
drwx-xr-x. 5 student student 46 Mar 20 00:42 Desktop
[student@krosum ~]$ _
```

```
[student@krosum ~]$ ls
ab.sh Desktop Downloads p1.c Pictures Public Videos
chat Documents Music p2.c process.log Templates
[student@krosum ~]$ ls -F
ab.sh* Desktop/ Downloads/ p1.c Pictures/ Public/ Videos/
chat/ Documents/ Music/ p2.c@ process.log Templates/
[student@krosum ~]$ _
```

### 8. `ls -F`

`-F` 选项显示文件列表，并指示它们的文件类型。

参考下表表有关文件类型指示的更多详细信息。

| * | 可执行文件 |
| :--- | :--- |
| | 命名管道（或）FIFO 文件 |
| / | 目录 |
| @ | 符号文件 |

### 9. `ls -i`

`-i` 选项显示带有相应文件索引号的文件列表。

如何以长列表格式列出最近创建的文件？

```
[student@krosum ~]$ ls -lt
total 12
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-xr-x. 1 student student 1 Mar 20 18:25 ab.sh
-rw-rw-r-- 1 student student 0 Mar 20 18:23 chat
-rw-rw-xr-x. 1 student student 4 Mar 20 18:13 p2.c -> p1.c
-rw-rw-r-- 1 student student 168 Mar 20 18:13 p1.c
-drwxr-xr-x. 2 student student 46 Mar 23 00:42 Desktop
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Documents
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Music
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Pictures
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Public
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Templates
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Videos
-drwxr-xr-x. 2 student student 6 Sep 23 2017 Downloads
[student@krosum ~]$
```

- 我们可以使用这两个 -- 选项，无论它们的顺序如何。

`ls -lt` 和 `ls -tls` 的效果相同。

```
[student@krosum~]$ ls
ab.sh Desktop Downloads p1.c Pictures Public Videos
chat Documents Music p2.c process.log Templates
[student@krosum ~]$ -$
[student@krosum ~]$ ls -i
180 ab.sh 4235394 Downloads 6291588 Pictures 141 Videos
178 chat 4235395 Music 146 process.log
2097282 Desktop 173 p1.c 140 Public
2097283 Documents 176 p2.c 6291587 Templates
[student@krosum ~]$ |
```

### 如何查看？

以下是查看文件列表的几种方法。

- 递归顺序的文件长列表。

`ls -lR` (or) `ls -Rl`

- 以递归顺序的长列表格式列出最近创建的文件。

`ls -ltR` (or) `ls -tRL` (or) `ls -lRt`

- 按降序（从大到小尺寸）排列的文件列表（长列表）。

文件大小

```
[student@krosum ~]$ ls -ls 168 Mar 20 18:13 p1.c
total 12
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-r-- 1 student student 46 Mar 20 00:42 Desktop
drwxr-xr-xr-x. 5 student student 6 Sep 23 2017 Documents
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Downloads
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Music
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Pictures
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Public
drwxr-xr-xr-x. 2 student student 6 Sep 23 2017 Templates
-rw-rw-r-x. 1 student student 4 Mar 20 18:23 p2.c -> p1.c
-rw-rw-r-x. 1 student student 1 Mar 20 18:25 ab.sh
rw-rw-r-- 1 student student 0 Mar 20 18:23 chat
[student@krosum ~]$
```

`ls -S`

按升序（从小到大尺寸）排列的文件列表（长列表）

文件大小。

```
$student@krosum ~ ~/ ls -l
total 12
-rw-rw-r-- 1 student student 6 Mar 20 18:23 chat
-rwxr-xr-x. 1 student student 1 Mar 20 18:25 ab.sh
-rwxr-xr-x. 1 student student 4 Mar 20 18:13 p2.c -> p1.c
drwxr-xr-x. 2 student student 6 Sep 23 2017 videos
drwxr-xr-x. 2 student student 6 Sep 23 2017 Templates
drwxr-xr-x. 2 student student 6 Sep 23 2017 Public
drwxr-xr-x. 2 student student 6 Sep 23 2017 Pictures
drwxr-xr-x. 2 student student 6 Sep 23 2017 Music
drwxr-xr-x. 2 student student 6 Sep 23 2017 Downloads
drwxr-xr-x. 2 student student 46 Mar 20 00:42 Desktop
-rw-rw-r-- 1 student student 84 Mar 20 18:31 process.log
-rw-rw-r-- 1 student student 168 Mar 20 18:13 p1.c
[student@krosum ~]$
```

`ls -Sr`（反序顺序）

| 选项 | 用法 |
| :--- | :--- |
| `-a` | 列出所有文件，包括以 . 开头的隐藏文件 |
| `-d` | 列出目录项 |
| `-F` | 文件类型 |
| `-l` | 长列表 |
| `-t` | 修改时间 |
| `-h` | 人类可读格式 |
| `-i` | 索引号 |
| `-r` | 反序 |
| `-R` | 递归顺序 |
| `-S` | 排序顺序 |
| `-s` | 块大小 |
