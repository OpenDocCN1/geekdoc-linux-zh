
# Bash 示例：Linux 脚本实用指南

![](img/image_rsrcPB.jpg)

## 我是谁

Tomas Gonzalez 是一位在计算机领域拥有丰富经验的专业人士。凭借在电脑商店 5 年的工作经验，他对技术相关产品和业务积累了深厚的知识。在商店工作期间，他在客户服务、问题解决以及计算机产品选择建议方面积累了技能。

此外，Tomas 还拥有 2 年的 Web 程序员经验，专注于 `PHP` 语言和 `APIs` 的使用。作为一名 Web 程序员，他参与了多个 Web 开发项目，使用 `APIs` 将第三方功能和数据集成到他创建的应用中。他在这一领域的经验使其在 Web 开发、数据处理和技术解决方案方面具备了强大的技能。

Tomas 还涉足了教学领域，担任培训师并提供私人课程。在一年半的时间里，他向他人分享自己的知识和经验，提供个性化的培训，并指导学生学习计算机概念和编程。

总结来说，Tomas Gonzalez 是一位在计算机领域丰富的专业人士，他是计算机产品专家、拥有丰富 `PHP` 和 `APIs` 经验的高级 Web 程序员，以及一位热于分享知识的培训师。他在电脑商店的实践经验、Web 开发和教学的结合，为他应对技术领域的各种挑战提供了坚实的基础。

## 简介

欢迎阅读《实例：在做中学学》（Bash by Examples: Learning by Doing），这本书旨在手手带你开启通通 `Bash` 命令行用户的兴奋之旅。在计算机世界中，理解如何高效与 `Unix/Linux` shell 交互不仅是一项价值巨大的技能，也是从软件开发人员到系统管理员以及数据科学家等 IT 专业人士的必备技能。

本书的驱动哲学简单而强大：“在做中学学”。通过一系列精心挑选的实用示例和互动练习，本书旨在赋予你使用 `Bash` 解决实际问题所需的知识和信心。这不仅仅关乎记忆命令和选项；更关乎理解让你能够在任何命令行环境中适应并茁壮的基本原理。

从基础的文件操作到自动化复杂任务，每一章都建立在前章的基础上，允许你循序渐进地发展技能。通过重复和练习，最初看似复杂的内容将变成本能。这种实用的方法确保了你在读完这本书后，不仅能够遵循所给出的示例，还能针对新且意想不到的问题编写自己的解决方案。

书中的每个示例被入选不仅是因为它们的实用性，还因为它们说明 `Bash` 以及通用 shell 编程重要概念的能力。通过分解每个示例，我们不仅会解释“如何做”，还会解释“为什么”，从而对每个解决方案背后的基础提供深度理解。

如果你是一个深入计算机世界的学生，一个寻求扩展技能的 IT 专业人士，或者仅仅渴望学习如何充分利用 `Bash` shell 力量的技术爱好者，那么这本书就是为你准备的。无论你目前的水平如何，我们都邀请你深入研究示例，进行实验，最重要的是，在过程中享受乐趣。

让我们一起开启这段学习冒险，探索 `Bash` 庞大而强大的世界，发现我们如何通过实践和实验解锁新技能并开启新的可能性。欢迎阅读《实例：在做中学学 Bash》。是时候编写、运行和学习了！

## 任务脚本

为了在 Bash 脚本中提供一个包含说明和解决方案的示例，我将首先定义一个简单的问题，然后向你展示如何用 Bash 脚本解决它。

**创建一个执行以下任务的 Bash 脚本：**

1. 检查特定目录是否存在。要检查的目录将作为参数传递给脚本。
2. 如果目录存在，脚本应该列出其中的所有文件和目录。
3. 如果目录不存在，脚本必须创建它。

### Bash 脚本解决方案

接下来，我向你展示解决上述问题的 Bash 脚本长什么样：

```bash
#!/bin/bash

# 将第一个参数保存变量变量
directory=$1

### 检查目录是否存在
if [ -d "$directorio" ]; then
echo "The directory $directory already exists. Listing contents:"
### 列出目录内容
ls -l $directory
else
echo "The directory $directory does not exist. Creating it..."
### 创建目录
mkdir $directory
echo "Directory $directory created successfully."
be
```

### 如何使用脚本

1. 首先，你必须将脚本保存到文件中。例如，`check_directory.sh`。
2. 接下来，你必须使用命令 `chmod +x verify_directory.sh` 给文件可执行权限。
3. 最后，你可以通过传递目录名称作为参数来运行脚本。例如：`./verify_directory.sh my_directory`。

该脚本是一个基础示例，展示了如何在 Bash 脚本中处理参数、执行条件判断执行基本命令。要注意，更复杂的用例可能需要额外的检查，例如检查用户是否有创建目录的权限。

### 编写一个 Bash 脚本，在给定目录的所有 `.txt` 文件中查找并替换单词

目录和单词（搜索词和替换词）将作为参数传递给脚本。

### Bash 脚本解决方案

该脚本将使用三个参数：搜索 `.txt` 文件的目录、要查找的单词以及替换词。它将遍历给定目录中所有的 `.txt` 文件，查找目标单词并将其替换为替换词。

```bash
#!/bin/bash

### 将参数赋值给变量
directory=$1
search=$2
replace=$3

### 检查目录是否存在
if [ -d "$directorio" ]; then
echo "Searching for files in $directory to replace '$find' with '$replace'..."
### 查找所有 .txt 文件并执行替换
find $directorio -type f -name "*.txt" -print0 | while IFS= read -r -d '' archivo; do
sed -i "s/$find/$replace/g" "$file"
echo "Replaced in: $file"
done
echo "Process completed."
else
echo "The directory $directory does not exist. Please check the path."
be
```

### 如何使用脚本

1. 将脚本内容保存到文件中，例如，`replace_word.sh`。
2. 使用 `chmod +x replace_word.sh` 给文件赋予执行权限。
3. 使用三个参数运行脚本：搜索目录、要查找的单词和替换词。例如：`./replace_word.sh ./my_directory wordSearch wordReplacement`。

该脚本对于快速更改多个文本文件非常有用，尤其是需要在项目或文档中自动化文本编辑时。记住在执行批量替换操作之前备份文件，以避免意外的数据丢失。

### 创建一个 Bash 脚本，通过名称监控特定进程的 CPU 和内存使用率

如果 CPU 或内存使用超过特定阈值，脚本应发送警报（用控制台消息模拟）。CPU 和内存阈值以及进程名称将作为参数传递给脚本。

### Bash 脚本解决方案

```bash
#!/bin/bash
```

#### 将参数赋值给变量

```bash
process_name=$1
umbral_cpu=$2
memory_threshold=$3
```

#### 获取并评估进程资源使用的函数

```bash
process_monitor() {
  # 通过名称获取进程的 PID
  pid=$(pgrep -f $process_name)

  if [ -z "$pid" ]; then
    echo "未找到进程。请确保 '$process_name'正在运行。"
    exit 1
  fi

  # 获取进程的 CPU 和内存占用
  uso_cpu=$(ps -p $pid -o %cpu=)
  use_memory=$(ps -p $pid -o %mem=)

  # 将 CPU 和内存占用与阈值比较
  cpu_excedido=$(echo "$uso_cpu > $umbral_cpu" | bc)
  exceeded_memory=$(echo "$use_memory > $umbral_memory" | bc)

  if [ $cpu_excedido -eq 1 ]; then
    echo "警告：'$process_name' 的 CPU 使用率过高 (${cpu_usage}%)"
  fi

  if [ $exceeded_memory -eq 1 ]; then
    echo "警告：'$process_name' 的内存使用率过高 (${memory_usage}%)"
  fi
}
```

#### 每分钟监控一次进程的循环

```bash
while true; do
  process_monitor
  sleep 60
done
```

### 如何使用脚本

1. 将脚本内容保存到文件中，例如 `process_monitor.sh`。
2. 使用命令给文件赋予执行权限：`chmod +x monitor_process.sh`。
3. 运行脚本并提供进程名称以及 CPU 和内存阈值。例如：

```bash
./monitor_proceso.sh firefox 10 20
```

此命令将监控 Firefox 进程，如果 CPU 使用率超过 10% 或内存使用率超过 20%，将发出警报。

此脚本是一个基础示例，可能需要根据你的特定需求进行调整，特别是在具有多个相同进程实例的系统上，`pgrep` 可能需要额外的选项来选择正确的 PID。

### 开发一个 Bash 脚本来对目录进行增量备份

该脚本应将备份保存到特定目录，并用创建日期和时间标记每个备份。源目录和目标目录将作为参数传递给脚本。此外，脚本应该删除旧备份，只保留最近的 3 个。

### Bash 脚本解决方案

此 Bash 脚本将使用 `rsync` 的文件传输效率对指定目录进行增量备份。你将使用 `date` 用时间戳标记每个备份，并结合 `find` 和 `rm` 来管理仅保留最近的 3 个备份。

```bash
#!/bin/bash

### 将参数赋值给变量
source_addr=$1
dir_destination=$2

### 检查目录是否存在
if [ ! -d "$dir_origen" ]; then
  echo "源目录不存在。"
  exit 1
fi

if [ ! -d "$dir_destino" ]; then
  echo "目标目录不存在。正在创建..."
  mkdir -p "$target_dir"
fi

### 为备份创建时间戳
timestamp=$(date +"%Y-%m-%d_%H-%M-%S")
backup_name="backup_$timestamp"

### 执行备份
rsync -a --link-dest=$destination_dir/ultimo $origin_dir/ $destination_dir/$backup_number/

### 更新“最后”符号链接到最新备份
ln -nsf $destination_dir/$backup_name $destination_dir/last
echo "备份完成: $backup_name"

### 清理旧备份，保留最近的 3 个
(cd $destination_dir && ls -d backup_* | head -n -3 | xargs -r rm -rf)
echo "旧备份已删除，保留了最近的 3 个。"
```

### 如何使用脚本

1. 将脚本保存到文件中，例如 `backup_incremental.sh`。
2. 使用 `chmod +x backup_incremental.sh` 给文件赋予执行权限。
3. 运行脚本并将源目录和目标目录作为参数。例如：

```bash
./backup_incremental.sh /path/a/source_directory /path/a/destination_directory
```

此脚本简化了增量备份的过程，对于频繁变化但不需要每次都进行完整备份的数据特别有用。实现的保留策略确保了存储空间不会被浪费消耗。

### 开发一个 Bash 脚本，检查提供的多个网站的可用性，并将每个的状态记录在日志文件中

脚本必须对每个网站发送 HTTP 请求并检查响应是否成功（HTTP 状态码 200）。对于每个网站，脚本应在控制台输出网站是上线还是离，并将此信息带时间戳记录到日志文件中。

### Bash 脚本解决方案

此脚本将使用 `curl` 向提供的参数网站发送 HTTP 请求。对于每个站点，它将检查响应的状态码，并将网站状态同当前日期时间记录到日志文件中。

```bash
#!/bin/bash

### 记录网站状态的日志文件
log_file="site_status.log"

### 验证是否提供了参数
if [ $# -eq 0 ]; then
  echo "请提供至少一个网站参数。"
  exit 1
fi

### 检查网站状态的功能
verify_site() {
  site=$1

  # 发送 HTTP 请求并获取状态码
  status=$(curl -o /dev/null -s -w "%{http_code}\n" $site)

  # 获取当前日期时间
  date=$(date +"%Y-%m-%d %H:%M:%S")

  if [ $status -eq 200 ]; then
    echo "$date: $site 在线。" | tee -a $log_file
  else
    echo "$date: $site 离线。" | tee -a $log_file
  fi
}

### 遍历脚本提供的所有参数
for sitio in "$@"; do
  verify_site $site
done
```

### 如何使用脚本

1. 将脚本保存到文件中，例如，`verify_sites.sh`。
2. 使用命令 `chmod +x verify_sites.sh` 给文件赋予执行权限。
3. 运行脚本并将网站作为参数。例如：

```bash
./verificar_sitios.sh https://www.google.com https://www.ejemploente.com
```

此命令将检查 Google 和一个不存在的网站的可用性，打印并记录状态。

这种方法适用于简单地监控网站可用性并记录状态以备后审查。

### 开发一个 Bash 脚本，将特定目录下的所有图像文件从一种格式转换为另一种

例如，将所有图像从 JPEG 转换为 PNG。源目录和目标格式将作为参数传递给脚本。

### Bash 脚本解决方案

```bash
#!/bin/bash

### 验证是否提供了足够的参数
if [ "$#" -ne 3 ]; then
  echo "用法: $0 directory source_format destination_format"
  exit 1
fi

directory=$1
source_format=$2
destination_format=$3

### 验证目录是否存在
if [ ! -d "$directory" ]; then
  echo "指定的目录不存在。"
  exit 1
fi

### 计数并转换图像
quantity=0
for image in "$directory"/*.$source_format; do
  if [ -f "$image" ]; then
    name_without_extension="${image%.*}"
    convert "$image" "${name_without_extension}.${destination_format}"
    echo "已转换: $image 到 ${name_without_extension}.${destination_format}"
    ((quantity++))
  fi
done

echo "总转换图像数量: $quantity"
```

### 如何使用脚本

1. 将脚本保存到文件中，例如，`convert_images.sh`。
2. 使用命令 `chmod +x convert_imagenes.sh` 给文件赋予执行权限。
3. 运行脚本提供图像目录、源格式和目标格式。例如：

```bash
./convertir_imagenes.sh /path/a/mis_imagenes jpeg png
```

此脚本是批量转换图像的有用工具，特别是在处理大量文件或需要为要求特定格式的项目准备图像时。

脚本必须允许用户通过参数指定目标目录。此外，你应该包含一个选项，让用户选择在报告中包含单个文件的详细信息，还是仅包含目录的总大小。

### Bash 脚本解决方案

此脚本将允许用户指定一个目录，并选择他们想要详细报告（包含文件）还是仅目录大小的摘要。你将使用 `du` 来计算大小，并使用 `sort` 对结果进行排序。

```bash
#!/bin/bash

### 验证是否至少提供了一个参数
if [ $# -lt 1 ]; then
  echo "Usage: $0 directory [verbose]"
  exit 1
fi

directory=$1
mode=$2 # 使用 'verbose' 包含单个文件，其他任何值仅包含目录

### 验证目录是否存在
if [ ! -d "$directory" ]; then
  echo "指定的目录不存在。"
  exit 1
fi

### 生成报告
if [ "$mode" = "detailed" ]; then
  echo "正在为 $directory 生成详细报告"
  du -ah "$directory" | sort -rh | head -n 50
else
  echo "正在为 $directory 生成目录报告"
  du -sh "$directory"/* | sort -rh | head -n 50
fi

echo "报告已生成。"
```

### 如何使用脚本



1. 将脚本保存到文件，例如 `reporte_sizes.sh`。

2. 使用 `chmod +x report_sizes.sh` 给文件赋予执行权限。

3. 运行脚本并将目标目录作为参数，可选地添加 `detailed` 单词以获取包含单个文件的报告。例如：

   - 对于仅限目录的报告：

     ```bash
     ./reporte_sizes.sh /path/a/my_directory
     ```

   - 对于包含文件的详细报告：

     ```bash
     ./reporte_sizes.sh /path/a/my_detailed directory
     ```

此脚本对于系统管理员或需要监控目录空间使用情况的用户非常有用，能够让你快速识别占用空间最大的部分。

### 开发一个 Bash 脚本来监控特定接口上的网络活动，并对任何超过用户定义阈值的额外数据使用进行记录

脚本必须允许用户通过参数指定网络接口和数据阈值（单位为 MB）。如果在规定时间内数据使用超过了阈值，必须将此事件记录在日志文件中。

## Bash 脚本解决方案

此脚本将使用 `vnstat` 监控指定接口的网络使用情况。`vnstat` 是一个跟踪网络使用的控制台工具，因此必须在系统中安装它此脚本才能正常工作。脚本将定期检查数据使用情况，并将任何超过阈值的部分记录到日志文件中。

```bash
#!/bin/bash

### 验证提供了必要的参数
if [ "$#" -ne 2 ]; then
  echo "Usage: $0 network_interface MB_threshold"
  exit 1
fi

interface=$1
threshold=$($2*1024)) # 将 MB 转换为 KB 以对比 vnstat 

### 日志文件名
log_file="exceeded_network_usage.log"

### 检查数据使用并记录超额的功能
verify_usage() {
  # 获取当前月接收和传输的总 KB
  usage=$(vnstat -i $interface --oneline | cut -d ';' -f 3,4 | tr ';' '+' | bc)
  if [ "$usage" -gt "$threshold" ]; then
    # 记录额外使用量
    echo "$(date +"%Y-%m-%d %H:%M:%S"): Excessive usage on $interface - ${usage}KB exceeds ${threshold}KB threshold" >> $log_file
    echo "警告: 已记录数据使用量超标。"
  else
    echo "数据使用在设定限制范围内。"
  fi
}

### 每 10 分钟监控网络使用情况
while true; do
  verify_usage
  sleep 600
done
```

## 如何使用脚本

1. 确保你的系统中安装了 `vnstat`。如果没有安装，你可以使用发行版的包管理器进行安装，例如在 Debian/Ubuntu 上使用 `sudo apt-get install vnstat`。

2. 将脚本保存到文件，例如 `monitor_red.sh`。

3. 使用 `chmod +x monitor_red.sh` 给文件赋予执行权限。

4. 运行脚本并将网络接口和 MB 为单位的数据阈值作为参数。例如：

   ```bash
   ./monitor_red.sh eth0 500
   ```

此脚本对于系统管理员或关注网络使用情况的用户非常有用，特别是对于具有数据限制的连接，或为了识别网络上的异常活动。

### 编写一个 Bash 脚本，生成过去 24 小时内指定目录及其子目录中修改过的文件列表，并将此列表通过电子邮件发送给指定用户

要的目录和收件人邮箱地址将作为脚本的参数。

## Bash 脚本解决方案

此脚本将使用 `find` 来识别过去 24 小时内修改的文件，并使用 `mail` 通过电子邮件发送列表。请确保你的系统中正确配置了 `mail` 命令以发送电子邮件。

```bash
#!/bin/bash

### 验证提供了必要的参数
if [ "$#" -ne 2 ]; then
  echo "Usage: $0 recipient_email directory"
  exit 1
fi

directory=$1
recipient_email=$2

### 保存列表的临时文件名称
temporary_file=$(mktemp /tmp/modified_files.XXXXXX)

### 查找过去 24 小时内修改的文件
find $directory -type f -mtime -1 > $temporary_file

### 检查文件是否为空
if [ -s "$temporary_file" ]; then
  # 通过电子邮件发送列表
  mail -s "Files modified in the last 24 hours" $recipient_email < $temporary_file
  echo "邮件已发送至 $recipient_email。"
else
  echo "未发现过去 24 小时内修改过的文件。"
fi

### 删除临时文件
rm $temporary_file
```

## 如何使用脚本

1. 将脚本保存到文件，例如 `send_files.sh`。

2. 使用 `chmod +x send_files.sh` 给文件赋予执行权限。

3. 在运行脚本之前，确保系统可以发送电子邮件。根据你的电子邮件供应商，可能需要配置 `sendmail` 或 `postfix`。

4. 运行脚本并将要监控的目录和收件人邮箱作为参数。例如：

   ```bash
   ./send_files.sh /path/to/directory myemail@example.com
   ```

### 创建一个 Bash 脚本，计算文件系统的空闲和使用空间，以用户可读的格式（例如 GB）并将结果发送给系统管理员

脚本参数将是管理员的邮箱地址。

## 脚本解决方案

此脚本将使用 `df` 获取磁盘使用信息，并使用 `awk` 处理这些信息将其转换为可读格式。最后，你将使用 `mail` 将发送给系统管理员。

```bash
#!/bin/bash

### 验证是否提供了邮箱地址
if [ "$#" -ne 1 ]; then
  echo "Usage: $0 email_address"
  exit 1
fi

email_admin=$1

### 报告的临时文件
report_file=$(mktemp /tmp/disk_space_report.XXXXXX)

### 生成报告
echo "Disk space report for $(hostname)" > $report_file
echo "Generated on $(date)" >> $report_file
echo "-----------------------------" >> $report_file
df -h | awk 'NR>1 {print $5 " busy on partition " $1 ", with " $4 free."}' >> $report_file

### 通过电子邮件发送报告
if [ -s "$report_file" ]; then
  mail -s "Disk space report - $(date +'%Y-%m-%d %H:%M:%S')" $email_admin < $report_file
  echo "报告已发送至 $email_admin。"
else
  echo "错误: 磁盘空间报告为空。"
fi

### 清理
rm $report_file
```

此脚本对于需要了解所管理系统磁盘空间使用情况的系统管理员非常有用，允许他们在空间问题影响运行之前快速识别潜在的空间问题。

### 创建一个 Bash 脚本，在 Linux 系统上自动创建用户账户，并分配主目录和默认密码

脚本必须接受用户名和默认密码作为参数。此外，在尝试创建用户之前，你应该检查该用户是否已于系统中。

## Bash 脚本解决方案

此脚本将使用 `useradd` 命令创建新用户，使用 `passwd` 分配密码，并使用 `grep` 检查用户是否存在。请确保以 root 身份运行此脚本，以获得添加用户所需的权限。

```bash
#!/bin/bash

### 验证是否提供了用户名和密码

if [ "$#" -ne 2 ]; then
echo "Usage: $0 username default_password"
exit 1
fi

username=$1
password=$2

# 检查用户是否已经

if id "$username" &>/dev/null; then
echo "User $username 在系统中已存在。"
exit 1
else
### 创建带有主目录的用户
useradd -m "$username"
### 分配默认密码（使用 chpasswd 避免密码显示）
echo "$username:$password" | chpasswd
echo "用户 $username 创建成功。"
fi
```

## 如何使用该脚本

1. 将脚本内容保存到文件中，例如 `create_user.sh`。

2. 使用 `chmod +x create_user.sh` 给文件赋予执行权限。

3. 以超级用户身份运行脚本，并提供用户名和默认密码作为参数。例如：

   ```bash
   sudo ./create_user.sh new_user password123
   ```

此脚本简化了 Linux 系统上的用户管理，允许系统管理员和 IT 自动化人员快速创建带有默认设置的用户账户。在需要高效创建多个用户账户的环境中，它特别别有用。

# 开发一个 Bash 脚本，查找并删除特定目录及其子目录中的重复文件

脚本应该根据文件内容（SHA-256 哈希值）而不是文件名对文件进行比较。它应该通知用户发现的任何重复文件并删除副本，为每个文件仅保留一个实例。目标目录将作为参数传递给脚本。

## Bash 脚本解决方案

此脚本将使用 `find` 命令列出目录及其子目录中的所有文件，并使用 `sha256sum` 计算每个文件的 SHA-256 哈希值，从而通过内容识别重复文件。发现的任何重复文件将被删除，为每个唯一文件仅保留一份。

```bash
#!/bin/bash

### 验证是否传递了目录作为参数

if [ $# -ne 1 ]; then
echo "Use: $0 directory"
exit 1
fi

directory=$1

### 检查目录是否存在

if [ ! -d "$directory" ]; then
echo "指定的目录不存在。"
exit 1
fi

### 创建临时文件来保存哈希
tempfile=$(mktemp)

### 生成目录及其子目录中所有文件的 SHA-256 哈希
find "$directory" -type f -exec sha256sum {} + > "$tempfile"

### 根据哈希查找重复项，忽略第一个唯一文件
duplicates=$(awk '{print $1}' "$tempfile" | sort | uniq -d)

if [ -z "$duplicates" ]; then
echo "未发现重复文件。"
rm "$tempfile"
exit 0
fi

### 处理每个重复哈希
echo "$duplicates" | while read hash; do
### 查找相同哈希的文件
grep "$hash" "$tempfile" | awk '{print $2}' | tail -n +2 | while read file; do
echo "正在删除重复文件: $file"
rm "$file"
done
done

rm "$tempfile"
echo "处理完成。重复文件已删除。"
```

## 如何使用该脚本

1. 将脚本保存到文件中，例如 `remove_duplicates.sh`。

2. 使用 `chmod +x remove_duplicates.sh` 给文件赋予执行权限。

3. 提供目标目录作为参数运行脚本。例如：

   ```bash
   ./remove_duplicates.sh /path/to/my_directory
   ```

此脚本对于保持目录整洁非常有用，特别是对于那些容易堆积重复文件的目录，例如照片或文档集。在运行此脚本之前，备份您的数据很重要，以避免意外丢失重要文件。

### 创建一个 Bash 脚本，将用户提供的目录列表备份到 tar.gz 文件

脚本必须允许用户指定多个目录作为参数，以及备份文件的输出文件名。如果备份文件已存在，脚本应该通知用户并终止操作，以防止意外覆盖。

## Bash 脚本解决方案

此脚本将用户指定的目录合并为单个 tar.gz 文件，首先检查输出文件是否存在以防止数据丢失。

```bash
#!/bin/bash

### 验证是否至少提供了两个参数

if [ "$#" -lt 2 ]; then
echo "Use: $0 output_file.tar.gz directory1 [directory2 ...]"
exit 1
fi

output_file=$1

### 移除第一个参数，以便仅遍历目录
shift

### 检查输出文件是否存在

if [ -f "$output_file" ]; then
echo "文件 $output_file 已存在。终止操作以避免覆盖。"
exit 1
fi

### 将目录合并为 tar.gz 文件
tar -czf "$output_file" "$@"
echo "成功备份目录到 $output_file。"
```

## 如何使用该脚本

1. 将脚本内容保存到文件中，例如 `backup_directories.sh`。

2. 使用 `chmod +x backup_directories.sh` 给文件赋予执行权限。

3. 提供输出文件名和要备份的目录列表运行脚本。确保输出文件不存在。例如：

   ```bash
   ./backup_directories.sh my_backup.tar.gz /path/a/directory1 /path/a/directory2
   ```

此脚本使得创建多个目录的压缩备份变得简单，对于数据丢失预防非常有价值。适用于对系统或应用进行重大更改之前的备份。

# 开发一个 Bash 脚本，将过去 7 天内修改的文件压缩到特定目录，创建一个以戳命名的 zip 文件

脚本应允许用户将要压缩的文件源目录作为参数。

## Bash 脚本解决方案

此脚本将在用户指定的目录中搜索过去一周内修改的所有文件。

```bash
#!/bin/bash

### 验证是否传递了目录作为参数

if [ $# -ne 1 ]; then
echo "Usage: $0 source_directory"
exit 1
fi

source_directory=$1

### 检查目录是否存在

if [ ! -d "$source_directory" ]; then
echo "指定的目录不存在。"
exit 1
fi

### 生成带时间戳的 zip 文件名
file_name="modified_files_$(date +"%Y%m%d_%H%M%S").zip"

### 查找并压缩过去 7 天内修改的文件
find $source_directory -type f -mtime -7 -print | zip $file_name -@

echo "过去 7 天内修改已压缩至 $file_name。"
```

## 如何使用该脚本

1. 将脚本保存到文件中，例如 `compress_modified.sh`。

2. 使用 `chmod +x compress_modified.sh` 给文件赋予执行权限。

3. 提供源目录作为参数运行脚本。例如：

   ```bash
   ./compress_modified.sh /path/to/my_directory
   ```

此脚本对于对最近修改的文件进行定期备份非常有用，有助于版本管理和数据恢复。它也可以作为自动化备份系统或文件维护程序的一部分。

### 创建一个 Bash 脚本，清理 Linux 系统特定用户的临时和缓存文件

脚本必须允许管理员指定一组用户名作为参数。对于每个用户，脚本需要删除常见临时目录中的文件，并在存在浏览器缓存时清理它。

## Bash 脚本解决方案

此脚本将遍历作为参数提供的用户名列表，检查临时目录和浏览器缓存目录是否存在。随后，它将清理这些目录以释放空间并可能提升系统性能。



```bash
#!/bin/bash

### Verify that usernames have been provided as arguments
if [ $# -eq 0 ]; then
  echo "Usage: $0 user1 [user2 ...]"
  exit 1
fi

### Function to clean temporary directories and cache
clear_directories() {
  user=$1
  # Define the temporary and cache directories to be cleaned
  temp_dirs=("/tmp" "/var/tmp")
  cache_dirs=("/home/$user/.cache/mozilla" "/home/$user/.cache/chromium")

  # Clear temporary directories
  for dir in "${temp_dirs[@]}"; do
    if [ -d "$dir" ]; then
      echo "Cleaning temporary directory $dir for user $user..."
      rm -rf "$dir/*"
    fi
  done

  # Clear browser cache
  for dir in "${cache_dirs[@]}"; do
    if [ -d "$dir" ]; then
      echo "Clearing browser cache $dir for user $user..."
      rm -rf "$dir/*"
    fi
  done
}

### Iterate over each user provided as an argument
for usuario in "$@"; do
  echo "Processing cleanup for user: $user"
  clean_directories $user
done

echo "Cleanup completed."
```

## 如何使用该脚本

1. 将脚本保存到文件中，例如，`clean_users.sh`。
2. 使用`chmod +x clean_users.sh`给该文件赋予执行权限。
3. 以超级用户身份运行脚本，并提供用户名作为参数。例如：

```bash
sudo ./clear_users.sh user1 user2
```

注：此处示例文件名已与`clean_users.sh`保持一致。

该脚本在多用户环境中特别有用，在这些环境中，临时文件和浏览器缓存可能会堆积并占用大量的磁盘空间。它有助于保持系统的整洁高效，特别是在共享系统或教育和商业环境中。
