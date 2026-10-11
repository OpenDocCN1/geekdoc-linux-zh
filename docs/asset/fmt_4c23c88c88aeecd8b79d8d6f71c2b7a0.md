
```bash
check_device() {
    local pool=$1
    while read -r name device status; do
        if [ "$name" == "$pool" ] && ([ "$device" == "mirror" ] || [ "$device" == "raid1" ] || [ "$device" == "raid2" ]) && [ "$status" ]; then
            log_error "ALERT: Device $device in Pool $pool has $status"
        fi
    done < <(zpool list -H -o name,device,status)
}
```

### 检查容量阈值（默认 80%）

```bash
check_capacity() {
    local pool=$1
    while read -r pool capacity; do
        if [ $(echo $capacity% | awk '{print $1}') -ge 80 ]; then
            log_error "WARNING: Pool $pool is $capacity full"
        fi
    done < <(zpool list -H -o name,capacity)
}
```

### 检查数据集属性

```bash
check_compression() {
    local dataset=$1
    while read -r name value; do
        if [ "$name" == "compression" ] && [ "$value" == "off" ]; then
            log_error "WARNING: Compression is disabled on dataset $dataset"
        fi
    done < <(zfs get -H -o compression "$dataset")
}
```

### 检查数据集是否挂载

```bash
check_mounted() {
    local dataset=$1
    if zfs get -o mounted "$dataset" | awk '{print $3}' != "mounted"; then
        log_error "WARNING: Dataset $dataset is not mounted"
    fi
}
```

### 检查可用空间

```bash
available=$(zfs -h $dataset | awk '{print $3}')
if [ "$available" == "0" ]; then
    log_error "CRITICAL: Dataset $dataset has no available space"
fi
```

# 发送邮件函数

```bash
sendmail() {
  local subject="$1"
  local content="$2"
  echo "Subject: $subject"
  echo "From: $FROM_NAME <$FROM>"
  echo "To: $EMAIL"
  echo "Reply-To: $REPLY_TO"
  echo "MIME-Type: text/plain; charset=UTF-8"
  echo "$content" | mail -s -
}
```

# 主执行

```bash
for pool in $(zpool list -H -o name); do
    check_pool_status "$pool"
    check_errors "$pool"
    check_device "$pool"
    check_capacity "$pool"
done

for dataset in $(zfs list -H -o name); do
    check_compression "$dataset"
    check_mounted "$dataset"
    # 检查逻辑
    available=$(zfs -h $dataset | awk '{print $3}')
    if [ "$available" == "0" ]; then
        log_error "CRITICAL: Dataset $dataset has no available space"
    fi
done
```

```bash
mkdir -p "$SLOG_DIR" || { echo "ERROR: Cannot create log directory SLOG_DIR"; exit 1; } # 如果无法创建目录则报错退出
chmod 755 "$SLOG_DIR" # 设置权限，允许所有者访问，其他人限制
# 检查文件是否存在并超过最大大小
if [ -f "$SLOG_FILE" ] && [ $(stat -c%s "$SLOG_FILE") -ge $MAX_SIZE ]; then
    mv "$SLOG_FILE" "$SLOG_FILE.old" # 通过重命名来归档旧文件
fi
#
如果不存在，则创建一个空日志文件
touch "$SLOG_FILE" # 创建日志文件（所有者读写，组只读）
# 带有时间戳的日志记录函数
log_message() {
    local message="$1" # 此消息的局部变量
    timestamp=$(date "%Y-%m-%d %H:%M:%S") # 生成特定格式的时间戳
    echo "[$timestamp] - $message" # 将带时间戳的消息输出到控制台和日志
}
# 记录错误的函数（将其添加到错误字符串并标记为 "ERROR"）
log_error() {
    local error="$1" # 传递给此函数的参数
    errors+="$error " # 将错误添加到错误字符串
    log_message "ERROR: $error" # 记录带时间戳的错误
}
# 检查系统是否安装了所需的依赖
check_dependencies() {
    log_message "Checking dependencies..." # 在日志中宣布开始检查
    local missing=()
    for cmd in "@"; do
        if ! command -v "$cmd" >/dev/null 2>&1; then
            missing+=("$cmd") # 将缺失的命令添加到数组
        fi
    done
    if [ ${#missing[@]} -ne 0 ]; then
        log_error "Missing dependencies: ${missing[*]}" # 记录缺失的错误
        echo "The following tools are not installed: ${missing[*]}" # 列出缺失的工具
        exit 1 # 因为缺少所需资源而退出（如果你看到这个）
    fi
}
# 遍历我们需要的每个命令，检查其是否可用
for cmd in "@"; do
    if ! command -v "$cmd" >/dev/null 2>&1; then
        missing+=("$cmd") # 如果命令缺失，则将其添加到数组
    fi
done
# 如果缺失的依赖数组不为空，记录错误并退出
if [ ${#missing[@]} -ne 0 ]; then
    log_error "Missing dependencies: ${missing[*]}" # 记录缺失的错误
    exit 1 # 退出
fi
# 查找并检测系统上的 RAID 阵
detect_raidarrays() {
    log_message "Searching for RAID arrays..." # 记录正在搜索 RAID 阵
    local devices=()
    # 查找所有名称类似 /dev/md, /dev/mdX 的设备（这些是你为操作系统和引导创建的 RAID 阵）
    for mddev in /dev/md[0-9]* /dev/md0; do
        devices+=("$mddev") # 保存到 md devices 变量中
    done
    # 遍历每个 md 设备并查找详细信息
    for mddev in "${devices[@]}"; do
```

