
要监控后台作业，可以使用`jobs`命令。它列出当前会话期间启动的所有作业，提供它们的作业 ID、状态和命令。例如：

```bash
#!/bin/bash
sleep 30 &
jobs
```

执行此脚本将显示启动的后台作业，通常输出类似：`[1]+ Running sleep 30 &`

使用`fg`命令可以将作业带到前台，后跟作业 ID。如果没有指定作业 ID，shell 默认选择最近的作业。相反，`bg`命令在后台恢复挂起的作业。例如：

```bash
#!/bin/bash
sleep 30 &
sleep 60 &
jobs
fg %1
bg %2
```

在需要同步的场景中，使用了`wait`命令。它暂停脚本执行，直到指定的后台作业完成。如果不带任何参数，`wait`会等待所有后台作业。下面的示例演示了这一点：

```bash
#!/bin/bash
sleep 30 &
job1=$!
sleep 60 &
job2=$!
wait $job1
wait $job2
echo "Both jobs have completed"
```

在这里，`sleep 30`和`sleep 60`在后台运行，其进程 ID 分存储在`job1`和`job2`中。`wait`命令阻塞脚本直到两个`sleep`命令完成，确保随后的`echo`命令在两个作业完成后执行。

高级作业控制可能涉及捕获如`SIGCHLD`之类的信号，以捕获子进程的终止。这种技术确保了后台进程的正确清理和处理。例如，以下脚本捕获了`SIGCHLD`信号：

```bash
#!/bin/bash

trap echo "A child process has terminated", SIGCHLD

sleep 30 & wait
```

当`sleep 30`命令终止时，`SIGCHLD`信号会触发捕获器，执行相关的`echo`命令。

作业控制不仅限于管理异步任务。Shell 分别支持使用`Ctrl-Z`和`bg`/`fg`命令来停止（挂起）和恢复进程。通过向进程发送`SIGSTOP`或`SIGTSTP`，可以将其挂起，稍后通过`SIGCONT`恢复：

```bash
#!/bin/bash

# 启动 sleep 命令并立即停止它
sleep 300 &
sleep_pid=$!
kill -SIGSTOP $sleep_pid
echo "sleep 300 has been stopped"

# 恢复 sleep 命令
kill -SIGCONT $sleep_pid
echo "sleep 300 has been resumed."
wait $sleep_pid
echo "sleep 300 has completed."
```

此脚本启动了一个后台`sleep 300`进程，用`SIGSTOP`停止它，稍后用`SIGCONT`恢复它。`wait`命令确保脚本等待直到`sleep`命令完成。

理解作业控制是编写高效且响应的 Shell 脚本的基础。采用这些技术可以确保脚本能够管理多个进程，对其状态做出反应，并程序化地处理它们的执行流。

## 9.10

## 创建和使用临时文件

临时文件在 Shell 脚本中经常用于存储在脚本执行的不同阶段之间使用的中间数据。正确处理临时文件对于确保数据完整性和脚本可靠性至关重要，有助于防止潜在的资源泄漏。

在 Unix 类系统中，创建临时文件有多种实现方法，每种方法对安全性和可移植性都有其影响。`mktemp`命令是安全创建临时文件或目录的一种健壮且优的方法。

`mktemp`生成一个唯一的文件名并安全地打开读写。`mktemp`的基本用法如下：

```bash
temp_file=$(mktemp)
```

该命令将新创建的临时文件名赋值给变量。默认情况下，`mktemp`在`/tmp`目录中创建文件。创建的临时文件仅允许创建它的用户访问，权限设置为。

要创建临时目录，使用`-d`选项：

```bash
temp_dir=$(mktemp -d)
```

该命令在`/tmp`中创建一个新目录并将路径赋值给变量。

临时文件在不再需要时应被删除以释放系统资源。可以使用`rm`命令处理文件，使用`rmdir`命令处理目录：

```bash
rm -f "$temp_file"
rmdir "$temp_dir"
```

然而，强烈建议即使脚本意外退出，也要确保临时文件始终被清理。使用`trap`语句处理脚本终止信号可以增加可靠性：

```bash
trap 'rm -f "$temp_file", rmdir "$temp_dir"' EXIT
```

该命令确保在脚本退出时（无论退出状态如何）都会执行指定的操作（删除临时文件和目录）。

有时，手动为临时文件名或目录指定模板可能是必要的。模板必须以至少六个`X`结尾，`mktemp`将这些这些替换为随机字符。例如：

```bash
temp_file=$(mktemp /tmp/mytempfileXXXXXX)
temp_dir=$(mktemp -d /tmp/mytempdir.XXXXXX)
```

临时文件的安全性至关重要。避免使用可预测的临时文件对于防止恶意用户利用竞态条件至关重要。`mktemp`工具通过确保唯一且安全的文件来降低此类风险。

另一种创建临时文件的常用方法是通过`${TMPDIR}`环境变量使用系统的内置设施。如果未定义`TMPDIR`，回退目录通常是：

```bash
temp_file=$(mktemp "${TMPDIR:-/tmp}/mytempfileXXXXXX)
```

这种方法确保了与配置了自定义`TMPDIR`路径系统的兼容性。

在处理大型数据集或多阶段流水线时，临时文件通过避免大量的内存操作来显著提高性能。以下是一个脚本示例，展示了临时文件在处理中的实际用例：

```bash
#!/bin/bash

# 创建临时文件
temp_file=$(mktemp)
trap 'rm -f "$temp_file"' EXIT

# 模拟数据处理
for i in {1..1000}; do
    echo "Processing item $i" >> "$temp_file"
done

# 读取并处理临时文件的内容
while read -r line; do
    echo "$line - processed"
done < "$temp_file"
```

此脚本在循环操作期间将中间数据存储在临时文件中，以处理大量项目。在脚本退出前，文件会被读回并处理。

将临时文件集成到 Shell 脚本中通过为中间数据存储提供受控范围，增强了效率、安全可靠性。及时删除临时文件可以保留系统资源并维护操作完整性。

## 9.11

## 处理大型数据集

在 Shell 脚本中处理大型数据集需要高效处理与对环境限制的理解。本节介绍了管理大型数据集的策略，确保脚本高效运行而不遇到瓶颈。由于内存的限制，处理大型数据集可能具有挑战性。

使用`awk`、`sed`和`cut`进行流式处理：处理大型数据集的一种有效方法是通过流式处理工具。`awk`、`sed`和`cut`等工具可以逐行处理数据，最大限度地减少任何时刻内存中保留的数据量。

```bash
awk '{print $1, $2}' large_data_file.txt > processed_data.txt
```

在上面的示例中，`awk`处理每行提取前两个字段，并将输出写入这种流式处理方法确保了只有文件的一小部分位于内存中。

利用`sort`和`uniq`处理大型数据集：使用`sort`和`uniq`命令可以高效地对大型数据集进行排序去重。这些命令对处理大量数据进行了优化。

```bash
split -l 10000 large_data_file.txt chunk_
```

上述命令将`large_data_file.txt`分分为较小文件，每个文件包含10000行，文件名以前为这种方法有助于独立处理每个块，避免内存过载。

使用 GNU Parallel 进行并行处理：并行处理可以显著缩短处理时间。GNU Parallel 工具允许并发运行操作，利用多核心处理器。

```bash
cat file_list.txt | parallel -j 4 process_script.sh {}
```

这里，`file_list.txt`包含要处理的文件列表。`parallel`命令为每个文件运行`process_script.sh`，最多运行四个作业。这利用了多核心处理器来加速数据处理任务。

使用 buffer 进行内存高效的数据处理：`buffer`工具可以封装数据流以控制数据流，从而在处理期间优化内存使用。

```bash
cat large_data_file.txt | buffer -s 1M
```

processing_script.sh

在本示例中，`buffer`设置的大小为 1 兆字节，通过控制数据流来平衡内存使用和处理速度。

使用 rg 和 jq 进行高效文本处理：如诸像 `ripgrep`（用于文本搜索）和 `jq`（用于 JSON 处理）等工具针对高效处理大数据进行了优化。
