

# 高级 Bash 脚本指南

```bash
IFS=${NO_WSP}
parent_child=(${parent_child[@]}) ${_den_pc[@]}
IFS=${_WSP}
fi

# 更新列表 known_pair（地址和名称）。
unique_lines _den_pair _den_pair
edit_exact known_pair[] _den_pair
if [ ${_den_pair[@]} -gt 0 ]; # 有新内容吗？
then
  IFS=${NO_WSP}
  known_pair=(${known_pair[@]}) ${_den_pair[@]}
  IFS=${_WSP}
fi

# 更新反向对列表。
unique_lines _den_rev _den_rev
edit_exact reverse_pair[] _den_rev
if [ ${_den_rev[@]} -gt 0 ]; # 有新内容吗？
then
  IFS=${NO_WSP}
  reverse_pair=(${reverse_pair[@]}) ${_den_rev[@]}
  IFS=${_WSP}
fi

# 检查间接限制，达到则放弃。
if ! _den_lmt=$(limit_chk[1])
then
  return 0
fi

# 执行定义任何 LIFO（后进先出）。挂起操作顺序很重要。
# 我们定义了新地址吗？
unique_lines _den_address _den_address
edit_exact known_address _den_address
edit_exact un_address _den_address
if [ ${_den_address[@]} -gt 0 ];
# 有新内容吗？
then
  uc_address=(${uc_address[@]}) ${_den_address[@]}
  pend_func expand_input_address(${_den_lmt})
  trace_log[${_trace_log[@]]]='Add ${_den_address[@]}' unchkd addr.
  return 0
fi

# 我们找到了任何新的吗？
unique_lines _den_name _den_name
edit_exact known_name _den_name
edit_exact uc_name _den_name
if [ ${_den_name[@]} -gt 0 ];
# 有新内容吗？
then
  uc_name=(${uc_name[@]}) ${_den_name[@]}
  pend_func expand_input_name(${_den_lmt})
  trace_log[${_trace_log[@]]]='Added ${_den_name[@]}' unchkd name.
  return 0
fi

# parse-it-yourself 委托回复
# 输入是 chk_address 列表。
detail_each_address<indirection_limit>
detail_each_address() {
  if [ ${_chk_address[@]} -gt 0 ]; || return 0
  unique_lines chk_address chk_address
}
```

## 附录 A 贡献脚本

```bash
edit_exact known_address chk_address
if [ ${chk_address[0]} -gt 0 ]
then
    known_address=${known_address[0]} ${chk_address[@]}
    unset chk_address[]
fi
```

```bash
# 应用特定的输出函数 # # #
# 格式化打印已知对。
report_pairs() {
    echo
    echo '已知网络对：'
    col_print known_pair 2 5 30
}
```

```bash
if [ ${auth_chain[0]} -gt 0 ]
then
    echo
    echo '已知权威链：'
    col_print auth_chain 2 5 55
fi
```

```bash
if [ ${reverse_pair[0]} -gt 0 ]
then
    echo
    echo '已知反向对：'
    col_print reverse_pair 2 5 55
fi
```

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

