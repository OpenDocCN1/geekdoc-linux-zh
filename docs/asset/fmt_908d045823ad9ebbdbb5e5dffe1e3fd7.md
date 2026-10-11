
```bash
$ cat Daily_Archive.sh
#!/bin/bash
#
# Daily_Archive - 归档指定的文件和目录
############################################################
#
# 获取当前日期
#
today=$(date +%y%m%d)
#
# 设置归档文件名
#
backupFile=archive$today.tar.gz
#
# 设置配置文件和目标文件
#
config_file=/archive/Files_To_Backup
destination=/archive/$backupFile

#
######## 主脚本 ############################################
#
# 检查配置文件是否存在

if [ -f $config_file ]; # 确保配置文件存在
    # 如果存在，则继续
    echo
else
    # 如果不存在，发出错误并退出脚本
    echo "$config_file does not exist"
    echo "Backup not completed due to missing"
    echo
fi
# 构建所有待备份的文件名
file_no=1 # 从文件的第 1 行开始
exec 0<$config_file # 重定向标准输入到配置文件

while read -r file_name; do
    # 检查文件或目录是否存在
    if [ -f $file_name -o d $file_name ]; then
        # 如果存在，将其添加到列表
        file_list="$file_list $file_name"
    else
        # 如果不存在，发出错误
        echo
        echo "$file_name, does not exist."
        echo "Obviously, I will not include it in this archive."
        echo "It is listed on line $file_no of the config file."
        echo "Continuing to build archive list..."
    fi
    file_no=$[$file_no + 1]
done

# 创建归档
echo "Starting archive..."
tar -czf $destination $file_list
echo "Archive completed"
echo "Resulting archive is: $destination"
```

# 第四部分：创建和管理实用脚本

图 24.1

创建备份目录层次

![](img/f87c2c98d1a1893335a09aa9e008a15e_725_0.png)

```
$ sudo mkdir /archive/hourly
[sudo] password for christine:
$
$ sudo chgrp Archivers /archive/hourly
$
$ ls -ogd /archive/hourly/
drwx-xr-x 2 4096 Aug 7 15:56 /archive/hourly/
$
$ sudo chmod 775 /archive/hourly
$
$ ls -ogd /archive/hourly/
drwx-xr-x 2 4096 Aug 7 15:56 /archive/hourly/
$
```

设置好目录后，可以将备份的 `Files_To_Backup` 配置文件移动到新目录：

```
$ cat Files_To_Backup.txt
/usr/local/Production/Machine_Errors/
/home/Development/Simulation_Logs/
$
$ mv Files_To_Backup.txt /archive/hourly/
$
```

## 第 24 章：编写简单的脚本工具

现在，有一个新挑战需要解决。脚本必须自动创建对应的月份和日期目录。但如果这些目录已经存在且脚本尝试创建它们，就会产生错误。这并不是我们想要的结果！

如果你查看 `mkdir` 命令的命令行选项（第 3 章），你会发现 `-p` 命令行选项。该选项允许你在单条命令中创建目录和子目录。此外，额外的好处是，如果目录已经存在，它不会产生错误信息。这完美符合脚本的需求！

我们准备好创建 `Hourly_Archive.sh` 脚本了。以下是脚本的上半部分：

```
$ cat Hourly_Archive.sh
#!/bin/bash
#
# Hourly_Archive - 每小时创建一个备份
############################################
#
# 设置配置文件
#
config_file=/archive/hourly/Files_To_Backup.txt
#
# 设置备份基础位置
based=/archive/hourly
#
# 获取当前日期、月份和时间
#
day=$(date +%D)
month=$(date +%M)
time=$(date +%K)
#
# 创建备份目标目录
#
mkdir -p $based/$month/$day
#
# 构建备份目标文件
destination=$based/$month/$day/archive$time.tar.gz
#
########### 主脚本 ###########################
[...]
```

当 `Hourly_Archive.sh` 到“主脚本”部分时，其余代码与 `Daily_Archive.sh` 脚本中的内容完全相同。大部分工作已经完成了！

`Hourly_Archive.sh` 从 `date` 命令中获取日期和月份值，以及时间戳来唯一标识备份文件。然后它利用这些信息创建当天的备份目录（如果目录已存在，则静默继续）。最后，脚本使用 `tar` 命令创建备份并将其压缩为 tar 包。

### 运行小时备份脚本

与 `Daily_Archive.sh` 脚本一样，在将 `Hourly_Archive` 脚本放入 cron 表格之前，进行测试是个个好主意。首先需要修改权限。此外，在测试脚本之前，最好通过 `date` 命令获取当前的小时和分钟。拥有这些信息可以验证最终备份文件名的正确性：

```
chmod +x Hourly_Archive.sh
$ date +%kM
1610
$ ./Hourly_Archive.sh
```

开始备份...

备份已完成

生成的备份文件是：

/archive/hourly/08/07/archive1610.tar.gz

```
$ ls /archive/hourly/08/07/
/archive/hourly/08/07/archive1610.tar.gz /
```

脚本第一次运行就成功了，创建了正确的月份和日期目录，并创建了命名正确的备份文件。注意备份文件名中包含了相应的小时（16）和分钟（10），即 `archive1610.tar.gz`。

> **提示**：如果你在白天运行 `Hourly_Archive.sh` 脚本，且小时为个位数，那么你的备份文件名将只有三位数。例如，如果你在凌晨 1:15 运行，备份名为 `archive15.tar.gz`。如果你希望备份文件名为四位数，请修改脚本行 `TIME=$(date +%kM)` 为 `TIME=$(date +%k0M)`。通过在 `%k` 之后添加一个零（0），任何单位数的小时都会通过前导零补齐为两位。因此，`archive15.tar.gz` 将被命名为 `archive015.tar.gz`。

为了测试，脚本运行了第二次，看看它是否会对已存在的目录产生问题：`/archive/hourly/08/07/`。

```
$ date +%kM
1615
$
$ ./Hourly_Archive.sh
```

开始备份...

备份已完成

生成的备份文件是：

/archive/hourly/08/07/archive1615.tar.gz

```
$ ls /archive/hourly/08/07/
/archive/hourly/08/07/archive1610.tar.gz
```

脚本运行正常，创建了正确的月份和日期目录，并创建了命名正确的备份文件。

# 第四部分：创建和管理实用脚本

(续)

```
echo
[...]
esac
#
echo
if [ -n "$line2" ]
then
# 输出 2 行
echo $line1
echo -e $line2" \c"
else
# 输出 1 行
echo -e $line1" \c"
fi
#
read -t 60 answer
done
#
unset line1
unset line2
#
)#End of get_answer_function
```
