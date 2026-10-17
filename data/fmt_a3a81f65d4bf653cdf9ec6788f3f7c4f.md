
```bash
# 检查地址是否存在黑名单服务器列表。
# 适用于 GraphViz 捕获的好地方：address->status(server(reports))
# check_lists <ip_address>
check_lists() {
    if [ $# -eq 1 ]; then return 1
    local -a fwd_addr
    local -a cl_rev_addr
    local -a cl_reply
    local -i rc
    local -i _ls_cnt
    local cl_dns_addr
    local lkup

    split -s ${1} fwd_addr cl_rev_addr
    cl_dns_addr+=${list_server[${1}]}
    _ls_cnt+=${list_server[${1}]}
    echo '正在检查地址：${1}'
    for ((cl = 0 ; $cl < ${_ls_cnt}; $cl++ ))
    do
        lkup+=${cl_dns_addr}${list_server[${cl}]}
        if short_text ${lkup} ${cl_reply}
        then
            if [ ${cl_reply[0]} -gt 0 ]
            then
                echo '来自 ${list_server[${cl}]} 的记录'
                address_hits[${1]+=1 '${list_server[${cl}]}'
                rc=2
            fi
        fi
    done
    for (( _cl = 0 ; _cl < ${cl_reply[0]}; _cl++ ))
    do
        echo
    done
    fi
    return 0
}

# 常规的应用胶接代码 #

# 谁开发的？
credits() {
    echo '高级 Bash 脚本指南：isspammer.bash, v2'
}

# 如何使用？
# 脚本末部的“快速上手”。
usage() {
cat <<-'_usage_'
脚本 isspammer.bash 需要一个或两个参数。
1 可以是：
a) 一个域名
b) 一个 IPv4 地址
c) 每行一个地址的文件名
2 可以是：
a) 黑名单服务器域名
b) 每行一个黑名单服务器名称的文件名
c) 如果不存在，则使用默认的黑名单服务器列表
d) 如果提供空文件，则禁用黑名单查询。
所有输出将写入到 stdout。

返回码：0 -> OK，1 -> 失败，2 -> 在黑名单中。
需要外部程序 "dig"。设置环境变量 SPAMMER_LIMIT 来限制域名查询深度。
SPAMMER_LIMIT=0 表示无限制。
如果参数是整数，则限制设置为该值并应用上述规则。
开发用：
将环境变量 SPAMMER_DATA 设置为文件名将导致执行引擎调用函数。
_usage_
默认列表如下：黑名单服务器：
declare -a default_servers
default_servers[0]='bl-spamhaus.org' # 严格，维护良好
default_servers[1]='relays.ord.org' # 开放中继
default_servers[2]='bl.spamcom.net' # 你可以在这里举报垃圾邮件
default_servers[3]='12.dbbl.net' # 早期检测系统
default_servers[4]='dnsl.sorbs.net' # 多邮件列表
default_servers[5]='list.dbl.org'
default_servers[6]='multitop.dbl.org'
default_servers[7]='unconfirmed.dbl.org'
```

```bash
# 用户输入 #1
setup_input() {
    if [ -e $1 ] && [ -r $1 ]; # 可读文件名
    then
        file_to_array $1 uc_name
        echo "作为输入的文件：${1}"
    else
        if is_address $1; # IP 地址？
        then
            uc_address=${1}
            echo "从地址开始：${1}"
        else
            # 必须是名称。
            uc_name=${1}
            echo "从域名开始：${1}"
        fi
    fi
    return 0
}
```

```bash
# 用户输入 #2
setup_servers() {
    if [ -e $1 ] && [ -r $1 ]; # 可读文件名
    then
        file_to_array $1 list_server
        echo "作为黑名单服务器列表的文件：${1}"
    else
        list_server=${1}
        echo "使用黑名单服务器：${1}"
    fi
    return 0
}
```

```bash
# 用户环境变量 SPAMMER_TRACE
live_log_die() {
    if [ $SPAMMER_TRACE ]; # 需要日志吗？
    then
        if [ ! -e $SPAMMER_TRACE ];
        then
            if touch $SPAMMER_TRACE 2>/dev/null
            then
                pend_func echo $(printf '%q\n') \
            fi
        fi
    fi
}
```

## 附录 A 构造的脚本

```bash
environment.variable SPAMMER_DATA
data_capture() {
if [ ${SPAMMER_DATA}= ]; # 需要数据转储吗？
if [ -e ${SPAMMER_DATA} ];
then
  if touch ${SPAMMER_DATA} 2>/dev/null
  then
    pend_func $(printf '%q\n') \
    '无法创建数据输出文件 >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
else
  if [ ! -w ${SPAMMER_DATA} ];
  then
    pend_func $(printf '%q\n') \
    '无法写入数据输出文件 >${SPAMMER_DATA}'
    pend_release
    exit 1
  fi
  .dot_file=${SPAMMER_DATA}
  .dot_dump=dump_dot
fi
fi
}

# 遍历用户指定的参数。
do_user_args() {
if [ $#-gt 0 ] && is_number $1;
then
  indirect=$1
  shift
fi}
```

# 高级 Bash 脚本指南

```bash
case $# in
  # 用户对我们友好吗？
  if ! setup_init $1 # 需要错误检查。
    then
      pend_release
      $_log_dump
      exit 1
  fi
  list_server=$( ${default_servers[@]} )
  list_cnt=${list_server[@]}
  echo '使用默认黑名单服务器列表。'
  echo '搜索深度限制: ${indirect}'
  2)
    if ! setup_init $1 # 需要错误检查。
    then
      pend_release
      $_log_dump
      exit 1
    fi
    if ! setup_servers $2 # 需要错误检查。
    then
      pend_release
      $_log_dump
      exit 1
    fi
  echo '搜索深度限制: ${indirect}'
  *)
    pend_func usage
    pend_release
    $_log_dump
    exit 1
  esac
return 0

# 通用的调试工具。
# list_array <array_name>
list_array() {
  [ -eq 1 ] || return 1 # 需要一个参数。

  local -a _la_lines
  set -f $NO_WSP
  eval _la_lines=( ${$1[@]} )
  echo
  echo 'Element count ${#_la_lines[@]} array "${$1}"\n ln_cnt=${#_la_lines[@]}

  for (( _i = 0; _i < ${_ln_cnt}; _i++ ));
    do
      echo 'Element \$_i\>'${_la_lines[$_i]}'
    done
  set +f
  return 0
}

# # 寻找垃圾邮件程序代码 # # 栈引擎就绪。
pend_init
pend_func credits # 最后打印的内容。
```

### 附 A 贡献脚本

```bash
## # 处理用户 # #
live_log_die              # 设置调试跟踪日志。
data_capture             # 设置调试捕获文件。
echo
do_user_args $
```

```bash
# # # 尚未退出 - 还有希望 # #
# 发现组 - 执行引擎 LIFO - pend
# 按照执行的倒序顺序。
hs_RC=0                    # Hunt the Spammer 返回码
pend_mark
pend_func report_pairs      # 报告名称-地址对。

# 两个 detail* 互递归函数
# 它们也会根据需要扩展* 函数。
# 这两个（??? 的最后两个）扩展了递归。
pend_func_each_address    # 获取地址的所有资源。
pend_func_details          # 获取名称的所有资源。
```

```bash
# 两个 expand* 互递归函数，
# 它们会根据需要调用额外的 detail* 函数。
pend_func_input_address 1  # 通过地址扩展输入名称。
pend_func_input_name 1     # # 通过名称扩展输入地址。
```

```bash
# 从唯一的地址和名称集合开始。
pend_func_unique_lines uc_address uc_name
pend_func_unique_lines uc_name uc_name
```

```bash
# 分离混合的地址和名称输入。
pend_func_split_input
pend_release
```

```bash
# # 已报告对 -- 找到的唯一 IP 地址列表
echo
_ip_cnt=$(${known[@#]})
if [ ${_server[@]} -eq 0 ]
then
```

```bash
echo '黑名单服务器列表为空，未检查。'
else
if [ ${_ip_cnt} -eq 0 ]
then
echo '已知地址列表为空，未检查。
```

```bash
else
_ip_cnt=${_ip_cnt}-1 # 从顶部开始。
echo '正在检查黑名单服务器。'
for ((_ip=${_ip_cnt}; _ip>=0; _ip--))
do
pend_func check_lists $(printf '%q\n' '${known_address[$_ip]}' ))
```

```bash
fi
pend_release              # 图形转储
$_dot_dump
$_log_dump               # 执行跟踪
echo

####################
# 脚本示例输出 #
####################
:<<-'is_spammer_outputs_
```

### 附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash
./is_spammer.bash 0
以域名名 web4.alojamentos.com 开始
使用默认黑名单列表。
搜索深度: 0
::::::::::::::::::::::
已知网络对:
66.208.297 web4.alojamentos.com.
66.208.297 nsl1.alojamentos.com.
69.56.202.147 nsl2.alojamentos.ws.
66.208.297 alojamentos.com.
66.208.297 nsl1.alojamentos.ws.
69.56.202.147 alojamentos.ws.
66.235.180.13 nsl1.alojamentos.org.
66.235.181.192 nsl2.alojamentos.org.
66.235.180.13 alojamentos.org.
216.234.230 webalojamentos.org.
129.96.160.115 nsl1.theplanet.com.
216.185.111.52 nsl2.theplanet.com.
69.56.141.4 mail.theplanet.com.
216.185.111.40 spoofing:theplanet.com.
216.185.111.40 www.theplanet.com.

检查黑名单服务器。
66.208.297 来自 dnsbl.sornet 的记录
在此报告垃圾邮件：http://www.dnsbl.sornet/lookup/
66.208.297 检查地址 69.56.202.147
69.56.202.146 检查地址 66.235.180.13
66.235.181.192 检查地址 216.185.111.40
216.234.230 检查地址 129.96.160.15
129.96.160.112 检查地址 216.185.111.52
高级 Bash 脚本指南: is_spammer.bash, v2, 204-
is_spammer_outputs_

exit ${HS_RC}

################################
# 脚本从这里开始忽略忽略
# 因为上面的 'exit' 命令。
################################
# 快速上手
=====================

前提

Bash 版本 2.0b 或 3.00 (bash --version)
支持数组的 Bash 版本。默认配置包含数组支持。

# 附录 A. 贡献脚本

# 高级 Bash 脚本指南

```bash

dig version 9.x (dig $HOSTNAME，见输出的第一行)

支持短选项的 dig 版本。

详情见 dig-wrappers.bash。
```
