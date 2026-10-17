
```bash
local array_details=" # 阵详情的临时变量

array_details=$(mdadm --detail "$mddev" 2>/dev/null) # 获取 RAID 详情；如果失败则跳过

if [ -n "$array_details" ]; then

    # 从详情中提取 RAID 阵信息

    local array_name=$(echo "$array_details" | grep "Array Device:" | awk '{print $3}') # 名称即阵名

    local array_type=$(echo "$array_details" | grep "Type:" | awk '{print $2}') # 类型为 RAID 类型

    # 使用类型判断该阵是用于引导、根还是其他

    if [ "$array_type" == "boot" ]; then

        log_message "Array $array_name is boot array" # 记录带有 "boot" 键的阵

    elif [ "$array_type" == "root" ]; then

        log_message "Array $array_name is root array" # 记录带有 "root" 键的阵

    elif [ "$array_type" == "overraid" ]; then

        log_message "Array $array_name is overraid array" # 记录带有 "overraid" 键的阵

    fi

fi

done

}

# 检查是否存在引导和根阵，如果有任何则记录错误

if [ -z "$boot_name" ] || [ -z "$root_name" ]; then

    log_error "RAID arrays not found" # 引导缺失时的特定消息

    log_error "RAID arrays not found" # 根缺失时的特定消息

fi

return 1 # 返回错误代码

fi

# 打印找到的所有阵的摘要

log_message "Detected arrays"

for array in "${raidarrays[@]}"; do

    log_message "$array" # 示例: "RAID_ARRAYS($array)"

done
```

## 检查特定 RAID 阵的健康状况

```bash
check_array_status() {
  local device="$1 # 阵设备的路径
  local purpose="$2 # "boot" 或 "root"，用于明确此用途
```

```bash
# 获取 RAID 阵详情并存储在变量中
local details
details=$(echo -detail "RAID $device" 2>/dev/null | awk '{print $2}') # 如果发生错误则捕获
  return 1
fi
```

```bash
# 提取状态（如 "clean" 或 "active"）并记录
local state
state=$(echo "$details" | grep "State :" | awk '{print $3}') # 从详情中获取
```

```bash
# 如果不稳定，记录警告
if [ "$state" != "DEGRADED" ]; then
  log_error "array $device is degraded state: $state"
```

```bash
# 检测故障设备
local failed_devs
failed_devs=$(echo "$details" | grep "Failed :" | awk '{print $4}') # 获取计数
if [ "$failed_devs" -gt 0 ]; then
  # 有故障设备，遍历每一个
  while read -r line; do
    failed_dev=$(echo "$line" | awk '{print $7}') # 获取第7单词（设备名）
    log_error "array $device has failed: $failed_dev" # 哪个设备故障了
  fi
done < $(echo "$details" | grep -A20 "Number") # 查看 Number 后的20行
```

```bash
# 检查是否有设备正在重建并记录它们
if grep -q "rebuilding" "$details"; then
  log_error "rebuilding" # 在行中检查
  while read -r line; do
    local rebuilding_dev
    rebuilding_dev=$(echo "$line" | grep "State :" | awk '{print $3}') # 获取设备名
    log_error "array $device is rebuilding: $rebuilding_dev" # 记录重建
  fi
done < $(echo "$details" | grep -A20 "Number" | grep "rebuilding") # 合并，查找 rebuilding 行
```

```bash
# 检查 RAID 阵内每个设备的健康状况
local health_score
health_score="$1 # 设备检查（例如 /dev/sda）
score=100 # 初始化健康分为100
local issues=
```

```bash
# 如果不是块设备则跳过
if [ ! -b "$device" ]; then
  log_error "$device is not a block device" # 记录无效设备
  return 1
fi
```

```bash
# 记录正在检查健康状况...
# 宣布我们正在检查的健康分
# 运行 SMART 健康，如果失败则降低健康分
if ! smart -H "$device" | grep -q "PASSED"; then
  # 如果不是 "PASSED"
  health_score=$((health_score-30)) # 如果失败扣30分
  issues+=" Overall failed" # 记录此问题
```

```bash
# 收集 SMART 属性进一步检查
local smart_attrs
smart_attrs=$(smart -A "$device" 2>/dev/null) # 重定向到 /dev/null
# 重道扇（磨损程度）
local relocated_devs
relocated_devs=$(echo "$smart_attrs" | awk '/5/ {print $5}') # 在 SMART 数据中查找 ID 5
health_score=$((health_score-10)) # 如果有重道扇扣10分
issues+=" Relocated sectors" # 添加到列表
```

## 检查等待扇（可能导致读取/错误）

```bash
local pending
if [ -n $(smartctl | awk '/197/ {print $3}') ]; then # 在 SMART 数据中查找 ID 197
  health=$((health_score-10)) # 如果存在等待扇扣10分
  issues+=" $health" # 添加到列表
fi
```

```bash
if [ -n "$score" ]; then # 在 SMART 阵中保存分数
  drive_health="$score" # 将健康状况保存到变量
  drive_report="Health report: $score/100%:$issues" # 如果发现报告则添加问题
```

```bash
if [ -n "$errors" ] || [ -n "$drive_report" ]; then
  subject="Alert: Monitor $hostname" # 设置主题行
  content="RAID Monitor Health Report from $hostname: $(date '+%Y-%m-%d %H:%M:%S')\n"
```
