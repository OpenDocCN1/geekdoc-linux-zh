
```bash
set -xv

for filesize in $(ls -l . | grep "^-" | awk '{print $5}')

do

  let totalsize=$totalsize+$filesize

done

echo "Total file size in current directory: $totalsize"
```

带有调试命令的 Shell 脚本输出：

```bash
$ ./fs.sh

++ ls -l .
++ grep '^-'
++ awk '{print $5}'
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=+178
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=178+285
+ for filesize in '$(ls -l . | grep "^-" | awk '{print $5}')'
+ let totalsize=463+189
+ echo 'Total file size in current directory: 652'

Total file size in current directory: 652
```

使用调试选项执行 Shell 脚本：

除了在 shell 脚本内部给出 `set -xv` 外，你也可以在执行 shell 脚本时提供它，如下所示。

```bash
$ bash -xv filesize.sh
```

### Hack 87. 引号

不带特殊字符的 `echo` 语句。

```bash
$ echo The Geek Stuff
```

The Geek Stuff

`echo` 语句带有一个特殊字符 `;`。分号是 `bash` 中的命令终止符。在以下示例中，“The Geek” 对 `echo` 有效，而 “Stuff” 被视为单独的 Linux 命令并导致命令未找到。

```bash
$ echo The Geek; Stuff
```

The Geek

`-bash: Stuff: command not found`

为避免这种情况，你可以在分号前添加 `\`，这将移除分号的特殊含义并仅将其打印出来，如下所示。

```bash
$ echo The Geek\; Stuff
```

The Geek; Stuff

### 单引号

当你想逐字打印单引号内的所有内容时，使用单引号。即使是 `$HOSTNAME` 这样的特殊变量也会被打印为 `$HOSTNAME`，而不是打印 Linux 主机的名称。

```bash
$ echo 'Hostname=$HOSTNAME ; Message=\$ is USD'
```

Hostname=$HOSTNAME ;

Message=\$ is USD

Current User=`whoami` ;

### 双引号

当你想显示特殊变量的真实含义时，使用双引号。

```bash
$ echo "Hostname=$HOSTNAME ; Message=\$ is USD"
```

Current User=`whoami` ;

### Linux 技巧

Ajay Kumar Tiwari

主机名=dev-db ; 当前用户=ramesh ; 消息=$ 是 USD

双引号将移除所有字符的特殊含义，除了以下情况：

- `$` 参数替换。
- `` ` `` 反引号
- `\$` 字面美元符号。
- `` \` `` 字面反引号。
- `\"` 嵌入式双引号。
- `\` 嵌入式反斜杠。

### Hack 88. 在 shell 脚本中读取数据文件字段

本示例展示了如何从数据文件中读取特定字段并在 shell 脚本中对其进行操作。例如，假设 `employees.txt` 文件的格式为 `{employee-name}:{employee-id}:{department-name}`，以冒号分隔的文件如下所示。

```bash
$ cat employees.txt
Emma Thomas:100:Marketing
Alex Jason:200:Sales
Madison Randy:300:Product Development
Sanjay Gupta:400:Support
Nisha Singh:500:Sales
```

以下 shell 脚本解释了如何从此 `employees.txt` 文件中读取特定字段。

```bash
$ vi read-employees.sh
#!/bin/bash
IFS=:
echo "Employee Names:"
echo "_____"
while read name empid dept
do
  echo "$name is part of $dept department"
done < ~/employees.txt
```

为 shell 脚本分配执行权限并执行它。

```bash
$ chmod u+x read-employees.sh
```

```bash
$ ./read-employees.sh
```

员工姓名：

Emma Thomas 是 Marketing 部门的一员

Alex Jason 是 Sales 部门的一员

Madison Randy 是 Product Development 部门的一员

Sanjay Gupta 是 Support 部门的一员

Nisha Singh 是 Sales 部门的一员

## 第 12 章：系统监控与性能

### Hack 89. free 命令

`free` 命令显示有关系统物理（RAM）和交换内存的所有必要信息。

语法：`free [options]`

### 我的系统总 RAM 是多少？

在下面的示例中，此系统的总物理内存为 1GB。以下显示的值以 KB 为单位。

```bash
# free
              total       used       free     shared    buffers     cached
Mem:       1034624    1006696      27928          0      174136     615892
-/+ buffers/cache:
Swap:      2031608          0     2031608
```

### 包括 RAM 和 Swap 在内，我系统的总内存是多少？

在以下命令中：

- 选项 `m` 以 MB 显示值
- 选项 `t` 显示“Total”行，即物理内存和交换内存值的总和
- 选项 `o` 用于隐藏上述示例中的 buffers/cache 行。

```bash
# free -mto
```

输出：

| | 总计 | 已用 | 空闲 | 共享 | 缓冲 | 缓存 |
|---|---|---|---|---|---|---|
| 内存 | 1010 | 983 | 27 | 0 | 170 | 601 |
| 交换 | 1983 | 0 | 1983 | | | |
| 总计 | 2994 | 983 | 2011 | | | |

### Hack 90. top 命令

`top` 命令显示有关系统各种性能指标的实时信息，例如 CPU 负载、内存使用情况、进程列表等。

语法：`top [options]`

### 如何查看包括 CPU 使用率在内的当前系统状态？

从命令行不带任何选项执行 `top`，将显示下面所示的输出。`top` 命令输出将持续显示实时值，直到您按“Control + c”或 `q` 退出命令输出为止。

```bash
# top
top - 13:10:13 up 171 days, 20:21, 3 users, load average: 0.01, 0.05, 0.00
Tasks: 194 total, 1 running, 193 sleeping, 0 stopped, 0 zombie
Cpu(s): 0.6% us, 0.7% sy, 0.0% ni, 98.7% id, 0.0% wa, 0.0% hi, 0.0% si
Mem: 1034624k total, 1007420k used, 27204k free, 174540k buffers
Swap: 2031608k total, 0k used, 2031608k free, 615904k cached
PID USER PR NI VIRT RES SHR S %CPU %MEM TIME+ COMMAND
11912 apache 15 0 31828 13m 3916 S 10.2 0:46.35 httpd
19299 oracle 19 0 279m 18m 17m S 10.2 0:00.03 oracle
11398 jsmith 16 0 107m 28m 6404 S 0.4 0:03.07 perl
```

### 如何阅读上面显示的 top 命令输出？

- 第 1 行“top”表示系统已运行 171 天。
- 第 2 行“Tasks”显示进程总数以及运行中、睡眠中、已停止和僵尸进程数的细分。
