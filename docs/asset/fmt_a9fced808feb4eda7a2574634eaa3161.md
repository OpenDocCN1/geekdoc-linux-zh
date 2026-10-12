
```bash
#!/bin/bash

# 检查是否以 root 身份运行
if [ $(id -u) -ne 0 ]; then
  echo "You must run this script as root."
  exit 1
fi

echo "User Account Management Script"
echo "1. Create a new user"
echo "2. Modify an existing user"
echo "3. Delete a user"
echo "4. Add user to a group"
echo "5. List all users"
echo "6. Check if a user exists"

read -p "Choose an option (1-6): " OPTION

case $OPTION in
  1)
    read -p "Enter username: " USERNAME
    read -p "Enter password: " PASSWORD
    useradd -m $USERNAME | passwd
    echo "User $USERNAME has been created"
    ;;
  2)
    read -p "Enter username: " USERNAME
    read -p "Enter new shell: " NEWSHELL
    usermod -s $NEWSHELL $USERNAME
    echo "User $USERNAME, shell has been changed to $NEWSHELL."
    ;;
  3)
    read -p "Enter username: " USERNAME
    userdel -r $USERNAME
    echo "User $USERNAME has been deleted"
    ;;
  4)
    read -p "Enter username: " USERNAME
    read -p "Enter group: " GROUP
    usermod -aG $GROUP $USERNAME
    echo "User $USERNAME has been added to group $GROUP ."
    ;;
  5)
    cut -d: -f1 /etc/passwd
    ;;
  6)
    read -p "Enter username: " USERNAME
    if id "$USERNAME" &2>/dev/null; then
      echo "User $USERNAME exists."
    else
      echo "User $USERNAME does not exist."
    fi
    ;;
  *)
    echo "Invalid option Exiting"
    exit 1
    ;;
esac
```

此统一脚本验证了 root 权限，为不同的用户账户任务提供了菜单，并根据用户的输入执行相应的操作。通过利用这些脚本，系统管理员可以高效管理用户账户，从而确保 Linux 环境中的安全访问控制。

## 2.9 自动化报告生成

自动化报告生成是系统管理和数据分析的一个重要方面，其中需要在没有人工干预的情况下创建并发布定期报告。通过利用 Shell 脚本，我们可以生成总结系统性能、用户活动等的报告。本节深入探讨如何编写生成此类报告的脚本、对其进行格式化以及安排创建计划。

### 收集系统信息

首先，我们考虑一个收集系统信息的脚本，例如 CPU 使用率、内存使用率和磁盘空间。这些信息对于系统管理员监控性能和做出明智决策是至关重要的。

```bash
#!/bin/bash
OUTPUT_FILE=/var/reports/sysinfo_report.txt
echo "System Information Report" > $OUTPUT_FILE
echo "Generated on: $(date)" >> $OUTPUT_FILE
echo "==========================" >> $OUTPUT_FILE
echo "Uptime:" >> $OUTPUT_FILE
uptime >> $OUTPUT_FILE
echo "Memory Usage:" >> $OUTPUT_FILE
free -h >> $OUTPUT_FILE
echo "Disk Usage:" >> $OUTPUT_FILE
df -nh >> $OUTPUT_FILE
echo "Top 10 Processes by Memory Usage:" >> $OUTPUT_FILE
ps aux --sort=%mem | head -n 11 >> $OUTPUT_FILE
echo "Top 10 Processes by CPU Usage:" >> $OUTPUT_FILE
ps aux --sort=%cpu | head -n 11 >> $OUTPUT_FILE
```

### 格式化报告

为了使报告具有可读且专业，可以使用 Markdown 或 HTML 格式化输出。以下是将之前脚本的输出封装在 HTML 标签中的示例：

```bash
#!/bin/bash
OUTPUT_FILE=/var/reports/sysinfo_report.html
echo "<html><body><h1>System Information Report</h1>" > $OUTPUT_FILE
echo "<p>Generated on: $(date)</p>" >> $OUTPUT_FILE
echo "<hr>" >> $OUTPUT_FILE
echo "<h2>Uptime:</h2>" >> $OUTPUT_FILE
echo "<pre> $(uptime)</pre>" >> $OUTPUT_FILE
echo "<h2>Memory Usage:</h2>" >> $OUTPUT_FILE
echo "<pre>$(free -h)</pre>" >> $OUTPUT_FILE
echo "<h2>Disk Usage:</h2>" >> $OUTPUT_FILE
echo "<pre>$(df -h)</pre>" >> $OUTPUT_FILE
echo "</body></html>"
```

## 内存占用前 10 进程

`$OUTPUT_FILE`

```bash
echo "<pre>$(ps aux --sort=-%mem | head -n 11) </pre>" >> $OUTPUT_FILE
```

`$OUTPUT_FILE`

```bash
echo "<h2>CPU占用前 10 进程</h2>" >> $OUTPUT_FILE
```

`$OUTPUT_FILE`

```bash
echo "<body><pre>$(ps aux --sort=-%cpu | head -n 11)</pre>" >> $OUTPUT_FILE
```

```bash
echo "</body></html>" >> $OUTPUT_FILE
```

### 通过电子邮件发送报告

报告生成后，可能需要通过电子邮件将其发送给利益相关者或系统管理员。我们利用 `mail` 工具来实现这一目标。
