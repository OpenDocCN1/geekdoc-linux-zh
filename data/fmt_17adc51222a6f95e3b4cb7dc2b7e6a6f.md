
`cat` 命令是 Linux 中显示、合并和格式化文件内容的强大工具。通过结合选项 `-n` 并将输出重定向到新文件，系统管理员可以简化文件管理任务。这些示例演示了在 Linux 环境下工作时清晰高效地组织内容的重要性。

# 使用 grep 命令

`grep` 命令是一个实用的实用程序，用于在文本文件中搜索模式。它扫描文件并输出匹配指定模式的行。常用选项包括：

- `-i`：忽略大小写的搜索
- `-n`：显示匹配的行号

## 搜索单词

首先，创建一个新文件并添加几行包含 `"error"` 单词的内容。然后，使用 `grep` 过滤该单词：

```bash
nano logfile.txt
grep "error"
[casarserver@RockyLinux ~]$ nano logfile.txt
[casarserver@RockyLinux ~]$ grep "error" logfile.txt
error
error
error
```

> 图 2.7：显示包含“error”的行

向现有文件添加更多行，包含一些变化，如 `"Error"` 或 `"ERROR"`。然后运行带有 `-i` 选项的 `grep` 以执行忽略大小写的搜索：

```bash
nano logfile.txt
grep "error" -i logfile.txt
```

```bash
[cesarmserver@RockyLinux ~]$ grep "error" -in logfile.txt
1:error
2:error
3:error
4:Error
5:ERROR
6:errorOR
7:ERRor
```

图 2.8：大小敏感错误信息的第一个示例

显示行号并结合忽略大小写的搜索：`grep "error" -in logfile.txt`。

```bash
[cesarmserver@RockyLinux ~]$ nano logfile.txt
[cesarmserver@RockyLinux ~]$ grep "error" -i logfile.txt
error
error
error
Error
ERROR
errorOR
ERRor
```

图 2.9：大小敏感错误信息的第二个示例

`Grep` 也可以用于管道符。例如：`cat logfile.txt | grep -i "error"`

```bash
[cesarmserver@RockyLinux ~]$ cat logfile.txt | grep -i "error"
error
error
error
Error
ERROR
errorOR
ERRor
```

图 2.10：大小敏感错误信息的第三个示例

## 使用 less 命令

高效地浏览大文件。`less` 命令允许一次一屏地查看大文件。它包含了导航工具和模式搜索。

请按照示例路径导航到新路径：

- `cd /etc/yum.repos.d`
- `ls`

```bash
[cesarmserver@RockyLinux yum.repos.d]$ cd /etc/yum.repos.d
[cesarmserver@RockyLinux yum.repos.d]$ ls
elpel-cisco-openh264.repo epel.repo rocky-devel.repo
elnel-next.repo epel-testing.repo rocky-extras.repo
elpel-next-testing.repo rocky-addons.repo rocky-repo
```

## 图 2.11：访问存储库

图 2.11 所示输出显示了访问特定目录的步骤。

查看文件：`rocky.repo`

```bash
[cesarmserver@RockyLinux yum.repos.d]$ less rocky.repo
[cesarmserver@RockyLinux yum.repos.d]$
```

## 图 2.12：验证存储库信息

`less` 命令用于在系统内导航和访问正确信息。

## 穿过内容：

- 按空格键向前滚动
- 按 `b` 向后滚动
- 使用 `/模式` 进行搜索，例如 `/important`
- 要退出文件，选择字母 `q`

## 组合命令：`ls -l /etc | less`

```bash
[cesarmserver@RockyLinux yum.repos.d]$ ls -l /etc/ | less
[cesarmserver@RockyLinux yum.repos.d]$
```

## 图 2.13：列出目录内容

图 2.13 展示了命令 `ls -l /etc | less` 的用法，该命令以长格式列出 `/etc/` 目录的内容，允许用户一次一屏地滚动查看输出。`ls -l` 部分为每个文件提供了详细信息。

## 表 2.2: 摘要

## 日志管理：查看和过滤日志

在 Rocky Linux 9 中，默认的系统日志管理工具是 `journal`（通过 `systemd`），它使用二进制日志而不是像 `/var/log/syslog` 这样的纯文本。

不要使用 `cat` 或 `less`，请使用 `journalctl` 命令来管理日志。
