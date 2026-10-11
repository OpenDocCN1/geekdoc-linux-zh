
``` 
return 0
```
################################################################################

# `log_failure_msg()`

# 用法：`log_failure_msg ["message"]`

# 目的：将失败状态消息打印到屏幕和

# 启动日志文件。

# 输入：`$@` - 消息

# 返回值：未使用

################################################################################

```
log_failure_msg({
  /bin/echo -ne "${BMPREFIX}$@"
  /bin/echo -ne "${CURS_ZERO}${FAILURE_PREFIX}${SET_COL}${FAILURE_SUFFIX}"
  # 从日志文件中剔除非可打印字符
  timespec
  logmessage=$(echo "$@" | sed 's/\\033[a-zA-Z]*/g')
  /bin/echo -e "${STAMP} ${logmessage}" >> ${BOOTLOG}
  return 0
})
```

```
log_failure_msg2({
  /bin/echo -ne "${BMPREFIX}$@"
  /bin/echo -ne "${CURS_ZERO}${FAILURE_PREFIX}${SET_COL}${FAILURE_SUFFIX}"
  echo "FAIL" >> ${BOOTLOG}
  return 0
})
```

################################################################################

# `log_warning_msg()`

# 用法：`log_warning_msg "[message]"`

# 目的：将警告状态消息打印到屏幕和

# 启动日志文件。

# 返回值：未使用

################################################################

```
log_warning_msg() {
  /bin/echo -ne "${BMPREFIX}${"
  /bin/echo -ne "${CURS_ZERO}${WARNING_PREFIX}${SET_COL}${WARNING_SUFFIX}"
  # 从日志文件中剔除非可打印字符
  logmessage=$(echo "${@}" | sed 's/\\033[a-zA-Z].*//g')
  timespec
  /bin/echo -ne "${STAMP} ${logmessage}" >> ${BOOTLOG}
  return 0
}
```

```
log_skip_msg() {
  /bin/echo -ne "${BMPREFIX}${"
  /bin/echo -ne "${CURS_ZERO}${SKIP_PREFIX}${SET_COL}${SKIP_SUFFIX}"
  # 从日志文件中剔除非可打印字符
  logmessage=$(echo "${@}" | sed 's/\\033[a-zA-Z].*//g')
  /bin/echo "SKIP" >> ${BOOTLOG}
  return 0
}
```

```
log_info_msg()
################################################################
# 目的：将信息消息打印到屏幕和
# 启动日志文件。不打印末尾换行符。
# 返回值：未使用
################################################################
```

```
log_info_msg() {
  /bin/echo -ne "${BMPREFIX}${"
  # 从日志文件中剔除非可打印字符
  logmessage=$(echo "${@}" | sed 's/\\033[a-zA-Z].*//g')
  timespec
  /bin/echo -ne "${STAMP} ${logmessage}" >> ${BOOTLOG}
  return 0
}
```

```
log_info_msg2() {
  /bin/echo -ne "${@}"
  # 从日志文件中剔除非可打印字符
  logmessage=$(echo "${@}" | sed 's/\\033[a-zA-Z].*//g')
  /bin/echo -ne "${message}"
  return 0
}
```

############################################################
# `evaluate_retval()`
# 用法：评估返回值并打印成功或失败
# 目的：终止消息的便利函数
# 返回值：未使用
################################################################
```
evaluate_retval()
{
    local error_value="${error_value}"
    if [ "${error_value}" -eq 0 ]; then
        log_success_msg
    else
        log_failure_msg
    fi
}
```

############################################################

# `check_signal() [-signal]`

# 目的：检查信号是否有效。LSB 草案中未定义，

# 但需要检查信号以确定是否为无效参数。

# 输入：格式为 `{-signal}` 的单个字符串

# 返回：

#   0 - 成功（信号有效）

#   1 - 信号无效

############################################################

```
check_signal()
{
    local valsig
    # 为无效信号添加处理
    valsig="-ALRM -HINT -KILL -KIFE -POLL -TERM -USRI -USR2"
    if echo "$valsig" | grep -qE "ALRM|INT|KILL|KIFE|POLL|TERM|USRI|USR2"; then
        return 0
    else
        return 1
    fi
}
```

############################################################

# `check_sig_type() [-signal]`

# 目的：检查信号是否为程序终止或控制信号

# LSB 草案中未定义，但需要检查信号以确定

# 是结束程序还是简单的控制。

# 输入：格式为 `{-signal}` 的单个字符串

# 返回：

#   0 - 信号用于终止

#   1 - 信号用于控制

############################################################

```
check_sig_type() {
  local vaisig
  valsig="ALRM -INT -KILL -PWR -QUIT -SEGV -TRAP"
  if echo "$valsig" | grep -qE "ALRM|INT|KILL|PWR|QUIT|SEGV|TRAP"; then
    return 0
  else
    return 1
  fi
}
```

################################################

# `wait_for_user()`

# 目的：如果不是无头系统，则等待用户响应

################################################

```
wait_for_user() {
  # 默认等待用户
  if [ "$HEADLESS" = "0" ]; then
    read
  fi
  return 0
}
```

################################################

# `is_true()`

# 目的：测试变量是否为 true

################################################

```
is_true() {
  if [ "$1" = "1" ] || [ "$1" = "yes" ] || [ "$1" = "true" ] || [ "$1" = "t" ]; then
    return 0
  else
    return 1
  fi
}
```
