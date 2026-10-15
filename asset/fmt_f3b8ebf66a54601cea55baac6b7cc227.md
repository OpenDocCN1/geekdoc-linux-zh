
在第 3 章中，我们的现场响应脚本只是显示了横幅、历史文件内容和页。如果我们希望将结果导入电子表格和/或数据库，这种格式是不可行的。为了获得便于导入的输出，我们使用 `awk`。

读者可能不熟悉 `awk`。它是由 Alfred Aho、Peter Weinberger 和 Brian Kernighan 在 20 世纪 70 年代于贝尔实验室创建的。名字来自作者姓氏的首字母。`awk` 是一种文本处理语言。`awk` 最常用的用法是打印文本行中的位置字段。

简单的 `awk` 用法最好通过示例来学习。例如，命令 `echo "one two three" | awk '{ print $1 $3 }'` 将输出 "one three"。

![](img/7abfab28a493757db3f096946a95ec01_172_0.png)

图 6.19
在 PFE 主题系统上运行此脚本的部分结果如图 6.19 所示。

## 从镜像文件中提取 bash 命令历史

一旦历史记录加载到数据库，就可以使用 `select * from histories order by recno` 轻松地显示。这将提供所有用户的历史记录。请注意，每个账户的历史记录将按照该用户的顺序呈现，但无法判断这些命令是何时执行的。显示单个用户 bash 历史的正确查询语句：`select historyCommand from histories historyFilename like '%%username%' order by recno;`

运行查询 `select historyCommand from histories where historyFilename like %.johnh* order by recno;` 的结果如图 6.20 所示。从这些历史中，我们可以看到虚拟用户 john 执行了命令查看还有谁登录以及他们执行了什么命令，输出了密码文件，并切换到了两个不应具有登录权限的用户账户。

![](img/7abfab28a493757db3f096946a95ec01_173_0.png)

图 6.20

攻击者创建的虚拟账户的 bash 命令历史。请注意正在运行的命令也十分可疑。

图 6.21 显示了 john 账户 bash 历史中的几个有趣的命令。可以看出，该用户创建了 johnnh 账户，将 `/bin/true` 复制到 `/bin/false`，为 whoopsie 和 lightdm 创建了密码，将 `/bin/bash` 复制到 `/bin/false`，编辑了 group 组文件，将 john 用户的家目录从 `/home/john` 移动到 `/home/john`（这导致目录被隐藏），编辑了密码文件，显示了 sed 的帮助页，使用 sed 修改了密码文件，并安装了 rootkit。将 `/bin/bash` 复制到 `/bin/false` 可能是为了允许系统账户登录。这可能也是不断弹出“检测到系统问题”消息的来源之一。

```python
import os
import sys
import glob
import gzip
import datetime
def get_logs(directory='/var/log'):
    logs = []
    if not os.path.exists(directory):
        print(f"Directory {directory} does not exist.")
        return logs
    for log_file in glob.glob(os.path.join(directory, '**')):
        try:
            stat = os.stat(log_file)
            mtime = datetime.datetime.fromtimestamp(stat.st_mtime)
            logs.append({
                "file": log_file,
                "modified": mtime,
                "size": stat.st_size
            })
        except Exception as e:
            continue
    return sorted(logs, key=lambda x: x['modified'], reverse=True)
if __name__ == "__main__":
    all_logs = get_logs()
    for log in all_logs:
        print(f"File: {log['file']} | Modified: {log['modified']} | Size: {log['size']} bytes")
```

图 6.21

攻击者使用 john 账户进行多次操作的证据。

## 检查系统日志

作为调查的一部分，我们可能想要查看各种系统日志文件。这些文件位于 `/var/log` 下。正如我们之前讨论过的，某些日志位于子目录中，另一些位于主 `/var/log` 目录。除了少数例外外，这些都是文本日志。某些格式为 `<base log file>.n`（其中 n 是整数）的存档，且较旧的存档可能使用 `gzip` 压缩。这导致了 `syslog`、`syslog.1`、`syslog.2.gz`、`syslog.3.gz` 等日志文件的创建。

与第 3 章中的脚本非常类似的脚本允许我们捕获日志文件进行分析。使用前面的章节中的脚本，我们只捕获当前日志。如果存档日志可能与调查有关，以后可以随时从镜像中获取。我们的脚本如下。

```bash
#!/bin/bash
### get-logfiles.sh
# 用于获取所有日志并可选
# 存储在数据库中的简单脚本。
# 警告：此脚本运行可能需要很长时间！
# 由 Phil Polstra 博士 (@ppolstra) 开发，用于
### PentesterAcademy.com。
usage() {
  echo "usage: $0 <point of root> [database name]"
  echo "Simple script to get log files and"
  echo "optionally store them to a database."
  exit 1}
if [ $# -lt 1 ]; then
  usage
fi
# 如果旧文件存在则将其删除
if [ -f /tmp/logfiles.csv ]; then
  rm /tmp/logfiles.csv
fi
# 只查找文件，排除带有数字的文件，因为它们是旧日志
# 对找到的所有文件执行 echo, cat, 和 echo
olddir=$(pwd)
cd $1/var
find log -type f -regex posix-extended \
  -regex '/[a-zA-Z.]+/([a-zA-Z.]*' \
  -exec awk '{ print :"$0' }' \
  tee -s /tmp/logfiles.csv
cd $olddir
if [ $# -gt 1 ]; then
  chown mysql:/tmp/logfiles.csv
fi
echo "Let's put that in the database"
cat << EOF | mysql $2 -u root -p
create table if not exists logs (
  logFilename varchar(2048) not null,
  logtextry varchar(2048) not null,
  recno bigint not null auto_increment,
  primary key(recno)
);
load data infile "/tmp/logfiles.csv"
into table logs
fields terminated by ';'
EOF
```

```bash
echo "and and unsuccessful logins."
echo "Results may be optionally stored in a database"
exit 1
if [[ $# -lt 1 ]]; then
  usage
fi
# use the last and lastb commands to display information
# use awk to create ; separated fields
# use sed to strip white space
echo "who-what:terminal-event;start;stop;elapsedTime;" \
  | tee /tmp/logins.csv
```
