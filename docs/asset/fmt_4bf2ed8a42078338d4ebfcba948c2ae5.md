
## 用途
登录指定的主机并进入类似 `ftp` 的交互式命令模式。第二种语法允许在非交互模式下或操作后自动检索文件。第三种语法允许 `sftp` 从远程目录启动。最后一种语法允许使用批文件中的命令进行自动文件传输，而不是使用标准输入。如果 `batchfile` 为 `-`，则命令来自标准输入。

## 常用选项/功能
- `-C` 通过向 `ssh` 传递此标记来启用压缩
- `-o ssh_option` 按照 `ssh_config` 文件使用的格式将选项传递给 `ssh`

## 会话示例
以下会话显示在 `sftp` 中执行的命令。如输出所示，本地主机的命令以字母 `l`（代表 `local`）开头，如 `ls`, `lmdir`, `lpw` 和 `lumask`。或者，任何以字母 `l` 开头的 Linux shell 命令都会作为 `lpwd` 在本地主机上执行。

### 连接并获取帮助

```
$ sftp sarwar@202.147.169.195

Connecting to 202.147.169.195...

sarwar202.147.169.195:password: xxxxxxx

sftp >

```

### 可用命令
- `bye`
- `cd path`
- `chgrp path`
- `chmod path`
- `chown path`
- `df [-hl] [path]`
- `exit`
- `get [-Pr] remote [local]`
- `get remote [local]`
- `help`
- `lcd path`
- `ls [ls-options [path]]`
- `mkdir path`
- `ls [-s] oldpath`
- `pwd`
- `ls [-la] [path]`
- `umask`
- `mkdir path`
- `progress`
- `put [-Pr] local [remote]`
- `pwd`
- `quit`
- `rename oldpath new`
- `rm path`
- `rdir path`
- `symlink oldpath new`
- `version`
- `!`
- `sftp Change directory to 'path'`
- `Change group of 'path' to 'grp'`
- `Change permissions of 'path' to 'mode'`
- `Change owner of 'path' to 'own'`
- `Display statistics for current directory or filesystem containing 'path'`
- `Download file`
- `Resume remote file`
- `Display this help`
- `Change local directory to 'path'`
- `Display local listing`
- `Create local directory`
- `Link remote file (-s for symlink)`
- `Print local directory`
- `Display remote listing`
- `Set local mask to 'umask'`
- `Create remote directory`
- `Toggle display of progress`
- `Display remote directory`
- `Quit sftp`
- `Rename remote file`
- `Delete remote file`
- `Remove remote directory`
- `Symlink remote file`
- `Show SFTP version`
- `Execute 'command' in local shell`
- `Escape to local shell`
- `Synonym for help`

### 列出本地工作目录

```
sftp> lpwd

Local directory: /Users/Mansoor

sftp>

```

### 列出远程工作目录

```
sftp> pwd

Remote directory: /home/sarwar

sftp>

```

### 列出远程工作目录的文件

```
sftp> ls

Desktop Music

Pictures Servers

Videos bin courses

sorted_students

sftp>

```

### 列出本地工作目录的文件

```
sftp> ls

Desktop Movies Saved

Downloads Sites

Library Public Terminal.txt

sftp>

```

### 将名为 `alien` 的单个文件上传到远程主机

```
$ sftp> put students

Uploading students to /home/sarwar/students

students

sftp>

```

### 将多个 `.txt` 结尾的文件上传到远程主机

```
$ sftp> mput *.txt

Uploading emacs.txt to /home/bob/emacs.txt

emacs.txt

Uploading fwvm.txt to /home/bob/fwvm.txt

fwvm.txt

Uploading vi.txt to /home/bob/vi.txt

vi.txt

sftp>

```

| 传输 | 速度 | 时间 |
| :--- | :--- | :--- |
| 100 191 | 0.2KB/s | 00:00 |
| 100 458KB | 458KB/s | 00:01 |
| 100 50KB | 50KB/s | 00:00 |

### 从远程到本地系统获取（下载）单个或多个文件

```
sftp> get testfile

Fetching /home/bob/testfile to testfile

/home/bob/testfile

sftp>

```

| 传输 | 速度 | 时间 |
| :--- | :--- | :--- |
| 100 22 | 0.0KB/s | 00:00 |

### 在本地和远程机器从一个目录切换到另一个目录

远程机器：

```
sftp> cd testfile

sftp>

```

本地机器：

```
sftp> lcd Documents

sftp>

```

### 在本地和远程机器上创建新目录

远程机器：

```
sftp> mkdir test

sftp>

```

本地机器：

```
sftp> ldir Documents

sftp>

```

### 在远程机器上删除目录或文件

```
sftp> rm Report.xls

sftp> rmdir Documents

sftp>

```

注意，要从远程位置移除/删除目录，该目录必须为空。

### 退出 `sftp`

```
sftp> quit
```
