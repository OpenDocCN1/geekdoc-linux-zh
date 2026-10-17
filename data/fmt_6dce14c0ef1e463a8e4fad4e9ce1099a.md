
```
sudo yum history
```

使用 CentOS `yum` 历史命令列出所有已安装的包

```
sudo yum history info 2
```

使用事务 ID `[2]` 详细检查历史记录

```
file /etc/passwd
```

显示给定文件的类型

```
[root@localhost manju]# file /etc/passwd
/etc/passwd: ASCII text
```

```
wc /etc/passwd
```

输出:
`46 91 2373 /etc/passwd`

该 `/etc/passwd` 文件包含 46 行、91 个单词和 2373 个字母

# 命令

```
grep root: /etc/passwd
```

# 说明

显示 `/etc/passwd` 中所有包含 `"root"` 字符串的行

# 命令

```
grep -n root /etc/passwd
```

# 说明

显示 `/etc/passwd` 中所有包含 `"root"` 字符串的行并带上行号

# 命令

```
grep -c false /etc/passwd
```

# 说明

显示以 `/bin/false` 为 shell 的账户数量

# 命令

```
grep ^root: /etc/passwd
```

# 说明

显示 `/etc/passwd` 中所有以字符串 `'root'` 开头接冒号的行

# 命令

```
last | head
```

# 说明

显示登录和注销系统的用户信息

（仅显示前 10 行）

`lastb`

# 显示最后失败的登录尝试

`du /etc/passwd`

# 显示 `/etc/passwd` 文件的磁盘占用

`killall proc`

# 杀死所有名为 `proc` 的进程

`wget https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm`

# 下载 RPM 文件进行安装
`sudo yum localinstall mysql80-community-release-el8-1.noarch.rpm`

# 安装 RPM 文件

```
sudo localinstall https://repo.mysql.com/mysql80-community-release-el7-1.noarch.rpm
```

# 通过 URL 安装 RPM 包

`curl --version`
# 显示 `curl` 版本

`curl -O http://website.com/myfiles.tar.gz`
# 从 URL `"http://website.com/myfiles.tar.gz"` 下载文件 (`myfiles.tar.gz`)
# 保存为 `myfiles.tar.gz`

`curl -o files.tar.gz http://website.com/myfiles.tar.gz`
# 从 URL `"http://website.com/myfiles.tar.gz"` 下载文件 (`myfiles.tar.gz`)
# 保存为 `files.tar.gz`

```
echo 'https://repo.mysql.com/mysql80-community-release-el8-1.noarch.rpm' > urls.txt
```

`xargs -n 1 curl -O < urls.txt`
# 从 `"urls.txt"` 文件中的 URL 列表下载文件

`exit 110`
# 退出终端窗口

`sudo -l`
# 了解在当前主机上允许和不允许的命令

```
命令:
echo -e "\hello\nworld"
↓
hello
world
```

```
history | grep cd | head -12
```

搜索前 12 条匹配 `cd` 单词的历史命令记录

# 开源操作系统的缺点

- 使用困难
- 兼容性问题

# 命令

```
rpm -qa | grep ftp
```

# 说明

检查所有已安装的 `ftp` 包

# 命令

```
find /home -mtime +120
```

# 说明

查找 `/home` 目录中修改于 120 天以前的文件

Samba 允许 Linux / UNIX 机器在网络中与 Windows 机器通信。

- `/etc` 目录包含 Linux 中的配置文件。
- 网络文件系统 (`NFS`) 是用于在网络上存储文件的机制。
- `"init"` 是 Linux 中内核启动的第一个进程，其进程 ID 为 1。

![](img/69fdaac95fca1cdd9f4079cb7470baa_245_0.png)

![](img/69fdaac95fca1cdd9f4079cb7470baa_245_1.png)

![](img/69fdaac95fca1cdd9f4079cb7470baa_245.png)

# 命令

```
cd ../..
```

# 返回上级目录

# 命令

```
ps -ef | grep proc
```

# 说明

列出系统中所有包含 `'proc'` 字符串的进程

```
echo -n ""
```

`echo ""`

`ls -ltr /etc`
# 按最后修改时间列出 `/etc` 中的文件

# 命令

```
ls -Rlh /var | grep M
```

# 说明

列出 `/var` 中大于 MB 小于 GB 的文件

# 命令

```
ls -lhS
```

# 说明

按大小列出文件

```
cat /etc/passwd /etc/group
```

# 显示多个文件的内容 (`/etc/passwd` 和 `/etc/group`)

```
find /tmp -name *.txt -exec rm -f {} \;
```

# 查找 `/tmp` 目录中所有 `*.txt` 文件并删除它们![](img/69fdaac95fca1cdd9f4079cb7470baa_247_0)

# 命令

```
watch -n 5 tail -n 3 /etc/passwd
```

# 每 5 秒显示一次 `/etc/passwd` 的末尾 3 行

```
watch -n 1 'ls -l | wc -l'
```

# 监控文件夹中的文件数量

```
watch -t -n 1 date
```

# 显示时间

```
find . -name "*.txt"
```

# 查找所有 `.txt` 扩展的文件

```
find . -name "*file*"
```

# 查找名称中包含 `"file"` 的文件

```
find /home -name "*file*"
```

# 查找 `/home` 中所有包含 `"file"` 的文件

```
grep -n "hello computer" ./
```

# 在当前目录搜索包含字符串 `"hello computer"` 的文件![](img/69fdaac95fca1cdd9f4079cb7470baa_248_0)img/69fdaac95fca1cdd9f4079cb7470baa_248_1)

# 命令

```
free -t -m
```

# 以 MB 显示空闲内存

# 命令

```
gnome-system-monitor
```

# 说明

显示正在运行的程序以及使用了多少、内存内存磁盘空间

# 命令

```
lsblk -m
```

# 显示设备权限和所有权

# 命令

```
lsblk -S
```

# 显示 SCSI (小型计算机接口) 设备
- `lsblk -n`: 列出无表头的设备

# 命令

```
ls -l ~
```

# 说明

检查文件和文件夹权限

# 命令

```
ls ./Documents
```

# 说明

显示 `Documents` 文件夹中的文件列表

# 命令

```
ls -R
```

# 列出所有子目录的内容

```
compgen -c
```

# 显示在命令行界面中可以使用的所有命令列表

- `pwd -L` → 打印符号路径
- `pwd -P` → 打印实际路径

```
hostnamectl
```

# 显示系统信息，包括操作系统、内核和版本

# 命令

```
find . -type f
```

# 查找文件

# 命令

```
find . -type d
```

# 查找目录

```
find . -iname "*.jpg"
```

# 忽略大小写查找扩展名为 `.jpg` 的文件（例如 `.jpg`, `.JPG`, `.Jpg`）

```
find . -type f -perm 777
```

# 按八进制权限查找文件

```
cd logs; ls -lt | head; du -sh ; df -h
```

# 使用 `";"` 运算符将上述任务合并为单行
