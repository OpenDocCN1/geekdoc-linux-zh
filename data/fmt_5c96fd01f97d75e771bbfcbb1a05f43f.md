
```bash
#!/bin/bash

# 定义源目录和目录
SRC_DIR="/home/user/data"
DEST_DIR="/backups/$(date +%Y%m%d_%H%M%S)"

# 创建目标目录
if [ ! -d "${DEST_DIR}" ]; then
    mkdir -p "${DEST_DIR}"
fi

# 使用 rsync 执行备份
rsync -av --delete "${SRC_DIR}/" "${DEST_DIR}/"

# 检查 rsync 是否成功
if [ $? -eq 0 ]; then
    echo "Backup completed successfully."
else
    echo "Backup failed." >&2
    exit 1
fi
```

此脚本利用了一个常用于备份的快速且多功能的文件复制工具。`-a` 选项确保 `rsync` 以“归档”模式运行，保留符号链接、文件权限和其他属性。`--delete` 选项会将源目录的删除同步到备份目录，从而保持完全镜像。

在目标路径中使用 `date` 命令确保了每次备份都有时间戳，防止覆盖之前的备份。错误处理通过检查 `rsync` 命令的退出状态来实现，为备份操作的成功或失败提供反馈。

对于目录恢复，相应的脚本可能如下：

```bash
#!/bin/bash

# 定义备份目录和恢复目标
BACKUP_DIR="/backups/20230101_123456"
RESTORE_DIR="/home/user/data"

# 确保备份目录存在
if [ ! -d "${BACKUP_DIR}" ]; then
    echo "Backup directory not found" >&2
    exit 1
fi

# 使用 rsync 执行恢复
rsync -av "${BACKUP_DIR}/" "${RESTORE_DIR}/"

# 检查 rsync 是否成功
if [ $? -eq 0 ]; then
    echo "Restoration completed successfully"
else
    echo "Restoration failed." >&2
    exit 1
fi
```

此脚本同样使用 `rsync` 将文件从备份位置复制到恢复目录。它包含一个在尝试恢复之前确保备份目录存在的检查，减少了错误风险。

虽然 `rsync` 适用于许多场景，但可能存在需要 `tar` 等归档格式的用法。以下示例演示了一个创建一个目录压缩归档的脚本：

```bash
#!/bin/bash

# 定义源目录和存档文件
SRC_DIR="/home/user/data"
ARCHIVE_FILE="/backups/data_backup_$(date +%Y%m%d_%H%M%S).tar.gz"

# 创建压缩 tar 归档
tar -czf "${ARCHIVE_FILE}" -C "${SRC_DIR}" .

# 检查 tar 是否成功
if [ $? -eq 0 ]; then
    echo "Archive created successfully: ${ARCHIVE_FILE}"
else
    echo "Failed to create archive." >&2
    exit 1
fi
```

`tar` 命令配合 `-c` 选项创建归档，`-z` 将其进行压缩，`-f` 指定输出文件。`-C` 选项切换到 `SRC_DIR` 目录，确保归档存储的是相对路径而非绝对路径。对于从 `tar` 归档恢复，脚本可能是：

```bash
#!/bin/bash

# 定义存档文件和恢复目标
ARCHIVE_FILE="/backups/data_backup_20230101_123456.tar.gz"
RESTORE_DIR="/home/user/data"

# 确保存档文件存在
if [ ! -f "${ARCHIVE_FILE}" ]; then
    echo "Archive file not found" >&2
    exit 1
fi

# 提取 tar 归档
tar -xzf "${ARCHIVE_FILE}" -C "${RESTORE_DIR}"

# 检查 tar 是否成功
if [ $? -eq 0 ]; then
    echo "Restoration from archive completed successfully"
else
    echo "Failed to restore from archive." >&2
    exit 1
fi
```

在此脚本中，`tar` 命令配合 `-x` 选项进行提取，`-z` 进行过滤，`-f` 指定存档文件。提取的文件存储在 `RESTORE_DIR` 中。这些示例为开发健壮的备份和恢复脚本提供了基础。通过引入错误检查并确保备份始终带有时间戳，可以实现可靠的备份流程。

## 日志文件分析与管理

日志文件对于理解系统行为至关重要。有效的日志分析有助于管理员检测异常、规划容量并确保安全。本节将深入探讨分析和管理日志文件的实用 `shell` 脚本。

首先，我们关注从日志中提取特定模式。考虑一种场景：你需要在位于以下位置的系统日志中找到所有出现“ERROR”术的地方

```bash
#!/bin/bash
grep "ERROR" /var/log/syslog
```

这使用 `grep` 命令在指定的日志文件中搜索字符串 "ERROR"。输出直接显示在终端上。对于更复杂的搜索，可以使用正则表达式。例如，如果我们想搜索包含 "ERROR" 或 "WARNING" 消息的行，可以使用以下脚本：

```bash
#!/bin/bash
grep -E "ERROR|WARNING" /var/log/syslog
```

`-E` 标志启用扩展正则表达式，允许使用 `|` 运算符匹配多个模式。

排序和计数是日志分析中的常见需求。使用之前的示例，如果你想统计 "ERROR" 消息的数量，可以将 `grep` 与 `wc` 命令结合：

```bash
#!/bin/bash
grep "ERROR" /var/log/syslog | wc -l
```

`wc -l` 命令计算输出行数。分析日志可能涉及更高级的任务，例如按日期汇总日志条目。以下脚本从每个日志条目提取日期并按日期统计“ERROR”消息的次数：

```bash
#!/bin/bash
grep "ERROR" /var/log/syslog | awk '{ print $1 } | sort | uniq -c
```

在此脚本中，我们总结步骤如下：

- `grep "ERROR" /var/log/syslog` 提取包含 "ERROR" 的行。
- `awk '{ print $1 }'` 提取日期（假设日期是每个日志条目的第一个字段）。
- `sort` 对日期进行排序。
- `uniq -c` 统计每个日期的唯一次数。

对于持续监控，可以使用 `tail` 实时查看日志。以下脚本监控 `syslog` 新写入的 "ERROR" 消息：

```bash
#!/bin/bash
tail -F /var/log/syslog | grep --line-buffered "ERROR"
```

`tail` 的 `-F` 选项跟踪日志文件，`grep` 的 `--line-buffered` 确保匹配行的立即输出。

日志轮转是一项必要的管理任务，防止日志占用过多磁盘空间。`logrotate` 工具通常用于此目的。针对 `/var/log/syslog` 的基础 `logrotate` 配置如下：

```
/var/log/syslog {
    daily
    rotate 7
    compress
}
```

- `daily` 指令 `logrotate` 每天轮转日志文件。
- `rotate 7` 保留最后七份轮后的日志。
- `compress` 对轮后的日志进行压缩以节省空间。

`missingok` 忽略缺失的文件。

`notifempty` 如果日志文件为空，则跳过旋转。

`postrotate` 和 `endscript` 定义了一个旋转后运行的脚本；在这种情况下，它会向 `rsyslog` 服务发送信号。

若要对自定义日志进行旋转而不使用以下脚本，可以手动旋转 `/var/log/custom.log`：

```bash
#!/bin/bash

LOGFILE="/var/log/custom.log"
BACKUPDIR="/var/log/backup"

if [ -f $LOGFILE ];
then
    TIMESTAMP=$(date +%Y%m%d%H%M%S)
    mv $LOGFILE "$BACKUPDIR/custom.log.$TIMESTAMP"
    gzip "$BACKUPDIR/custom.log.$TIMESTAMP"
    touch $LOGFILE
fi
```

此脚本执行以下任务：

- 检查 `/var/log/custom.log` 是否存在。
