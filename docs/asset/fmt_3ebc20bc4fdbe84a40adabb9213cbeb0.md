
```
FOO="Mixed UpEr aNd LoWeR cAsE"
echo $FOO | tr [A-Z] [a-z]
```

在下一个示例中，`tr` 命令用于一行文件名，以重命名该列表中的任何文件，使文件名中包含的空格被翻译为下划线：

```
for file in *; do
  d=`echo $file | tr '[:blank:]' '_'`
  [ "$file" != "$d" ] && mv "$file" "$d"
done
```

# 流编辑器 (sed)

`sed` 是一个简单的脚本编辑器，因此它只能执行简单的编辑，例如删除匹配特定模式的文本行、将一种字符模式替换为另一种，以及其他简单的编辑。要更深入了解 `sed` 脚本的工作原理，在线文档是不可替代的，但这里有一些常见的用法示例。

你可以使用 `sed` 命令来实现与我之前 `grep` 示例中相同的操作：在 `/etc/passwd` 文件中搜索单词 `home`。在这里，`sed` 命令搜索整个 `/etc/passwd` 文件，查找单词 `home` 并打印任何包含单词 `home` 的行。

```
sed -n '/home/p' /etc/passwd
```

在这个示例中，`sed` 搜索 `somefile.txt` 并将字符串 `Mac` 的所有实例替换为 `Linux`。输出发送到 `fixed_file.txt` 文件。

```bash
sed 's/Mac/Linux/g' somefile.txt > fixed_file.txt
```

## 第12 章：自动化系统任务

你可以通过管道获得相同的结果：

```
cat somefile.txt | sed 's/Mac/Linux/g' > fixed_file.txt
```

通过搜索模式并将其替换为空模式，你删除了原始模式。这个示例搜索 `somefile.txt` 文件的内容，查找并替换每行末尾的空格（`s/ *$`）为空内容（`//`）。结果保存到 `fixed_file.txt`。

```
cat somefile.txt | sed 's/ *//' > fixed_file.txt
```

## 尝试一些简单的 shell 脚本

有时最简单的脚本可能是最有用的。如果你反复输入相同的命令序列，那么将这些命令（只需一次！）存储在文件中是有意义的。这里有几个简单但实用的脚本。

### 一个简单的电话列表

这个想法从老旧 UNIX 技巧中代代相传。它实际上非常简单，但它运用了刚刚介绍的几个概念。

```bash
#!/bin/bash
# /ph
# 一个非常简单的电话列表
# 输入 "ph new name number" 添加到列表，或
# 只输入 "ph name" 获取电话号码

PHONELIST=~/phonelist.txt

# 如果没有命令行参数 ($)，则
# 说明有问题，所以问问他们在谈论什么。
if [ $# -lt 1 ]; then
    echo "Whose phone number did you want?"
    exit 1
fi

# 你想添加新的电话号码吗？
if [ $1 = "new" ]; then
    shift
    echo "$*" >> PHONELIST
    echo "$*" added to database
    exit 0
fi

# 不。但文件里现在已经有内容了吗？
# 毕竟，这可能是我们第一次使用它。
if [ ! -s $PHONELIST ]; then
    echo "No names in the phone list yet!"
    exit 1
else
    grep -i "$*" $PHONELIST # 静默搜索文件
    if [ $? -ne 0 ]; then # 我们找到东西了吗？
        echo "Sorry, that name was not found in the phone list"
        exit 1
    else
        grep -i "$*" $PHONELIST
    fi
fi
```

所以，如果你在当前目录下创建了 `ph` 文件，你可以从 shell 输入以下内容来尝试你的 `ph` 脚本：

```bash
$ chmod 755 ph
$ ./ph new "Mary Jones" 608-555-1212
Mary Jones 608-555-1212 added to database
$ ./ph
Mary Jones 608-555-1212
```

`chmod` 命令使 `ph` 脚本变为可执行。`./ph` 命令从当前目录带有新选项运行命令。这把 `Mary Jones` 作为姓名并将 `608-555-1212` 作为电话号码添加到数据库（phone.txt）。下一个 `ph` 命令在数据库中搜索该名称并显示 Mary 的条目。如果脚本正常工作，将其添加到目录。

### 简单的备份脚本

由于 `sed` 是一个简单的编辑器，它只能执行简单的编辑。

```bash
/bin/bash
# /ph
# 一个非常简单的电话列表
# 输入 "ph new name number" 添加到列表，或
# 只输入 "ph name" 获取电话号码

PHONELIST=~/phonelist.txt

# 如果没有命令行参数 ($)，则
# 说明有问题，所以问问他们在谈论什么。
if [ $# -lt 1 ]; then
    echo "Whose phone number did you want?"
    exit 1
fi

# 你想添加新的电话号码吗？
if [ $1 = "new" ]; then
    shift
    echo "$*" >> PHONELIST
    echo "$*" added to database
    exit 0
fi

# 不。但文件里现在已经有内容了吗？
# 毕竟，这可能是我们第一次使用它。
if [ ! -s $PHONELIST ]; then
    echo "No names in the phone list yet!"
    exit 1
else
    grep -i "$*" $PHONELIST # 静默搜索文件
    if [ $? -ne 0 ]; then # 我们找到东西了吗？
        echo "Sorry, that name was not found in the phone list"
        exit 1
    else
        grep -i "$*" $PHONELIST
    fi
fi
```

### 备份脚本

```bash
#!/bin/bash
# 备份脚本
# 备份指定目录中的文件

SOURCE_DIR="/home/user/documents"
BACK_DIR="/home/user/backups"
DATE=$(date +%Y%m%d_%H%M%S)

# 如果备份目录不存在则创建它
if [ ! -d "$BACK_DIR" ]; then
  mkdir -p "$BACK_DIR"
fi

# 创建压缩包
tar -czf "$BACK_DIR/backup_$DATE.tar.gz" "$SOURCE_DIR"

echo "备份完成：$BACK_DIR/backup_$DATE.tar.gz"
```

### 清理脚本

```bash
#!/bin/bash
# 清理脚本
# 删除 7 天前的备份文件

BACKUP_DIR="/home/user/backups"
DAYS=7

echo "正在清理 $DAYS 天前的备份..."

find "$BACKUP_DIR" -name "backup_*.tar.gz" -type f -mtime +$DAYS -exec rm {} \;

echo "清理完成。"
```

### 监控脚本

```bash
#!/bin/bash
# 监控脚本
# 检查磁盘空间并发送警报

THRESHOLD=80
USAGE=$(df / | tail -1 | awk '{print $5}' | sed 's/%//')

if [ "$USAGE" -gt "$THRESHOLD" ]; then
  echo "警告：磁盘使用率已达到 $USAGE%"
  # 在此处添加发送邮件通知的代码
  # mail -s "磁盘空间警报" admin@example.com <<< ...
else
  echo "磁盘使用率正常：$USAGE%"
fi
```

## 第 12 章：自动化系统任务

`init`（有效动作和这些动作的结果如表 12-3 所示），最后一个字段是要待执行的实际命令。

### 表 12-3：有效的 init 运行方式

| 动作 | 命令的运行方式 |
|---|---|
| once | 在进入指定的运行级别（run level）时执行一次命令。 |
| wait | 与 once 相同，但 init 会等待命令完成后再继续处理其他 inittab 条目。 |
