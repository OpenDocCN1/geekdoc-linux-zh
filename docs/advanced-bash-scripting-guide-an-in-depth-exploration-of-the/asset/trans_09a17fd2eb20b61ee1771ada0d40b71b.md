

# 高级 Bash 脚本指南

```bash
si_input=$($1)
IFS=${WSP_IFS}
eval $2=("${si_input[@]}")
if [ $# -eq 3 ];
then
    # 构建查询顺序数组。
    local -a dns_ip
    dns_ip[0]=${si_input[3]}
    dns_ip[1]=${si_input[2]}
    dns_ip[2]=${si_input[1]}
    dns_ip[3]=${si_input[0]}
    eval $3=("${dns_ip[@]}")
fi
return 0
}

# 此函数在 dot.array.bash 中描述
# dot_array <array_name>
dot_array() {
    if [ $# -ne 1 ] || return 1; # 需要单个参数.
    local -a da_input
    eval da_input=("${$1[@]}")
    local IFS=${DOT_IFS}
    local da_output=${da_input[0]}
    IFS=${WSP_IFS}
    echo ${da_output}
    return 0
}

# 此函数在 file_to_array.bash 中描述
# file_to_array <name> <line_name>
file_to_array() {
    if [ $# -ne 2 ] || return 1; # 需要两个参数.
    local IFS=${NO_WSP}
    local -a fta_tmp
    fta_tmp=($(cat $1))
    eval $2=("${fta_tmp[@]}")
    return 0
}

# 多字段字符串数组的列化打印。
# col_print <array_name> <min_space>
# +tab_stop [tabs_stops]
col_print() {
    if [ $# -lt 2 ] || return 0;
    local -a cp_inp
    local -a cp_sp
    local -a cp_line
    local cp_min
    local cp_cnt
    local cp_pos
    local cp_tab
    local -i _cp
    local -i _cpf
    local cp_fld
    # 警告：后续行不是空白的 - 它带有引号。
    local _cp_max
    set -f
    local IFS=${NO_WSP}
    eval cp_inp=("${$1[@]}")
    if [ ${#cp_inp[@]} -eq 0 ] || return 0; # 空情况简单.

    _cp_max=$2
    cp_min=${2:1}
    shift
    shift
    cp_cnt=0
    for ((cp=0; _cp < cp_cnt; _cp++));
    do
        cp_sp[$cp]=${_cp_max:cp_min}"
        shift
    done
    cp_cnt=${#cp_inp[@]}
    for ((cp=0; _cp < cp_cnt; _cp++));
    do
        cp_pos=1
        IFS=' '
        cp_line=("${cp_inp[$cp]}")
        IFS=${WSP_IFS}
        for ((cpf=0; _cpf < ${#cp_line[@]}; _cpf++));
        do
            cp_tab=${cp_sp[$cpf]}:${cp_pos}
            if [ "${#cp_tab}" -lt "${cp_min}" ];
            then
                cp_tab="${cp_min}"
            fi
            echo -n "${cp_tab}"
            ((cp_pos += ${#cp_tab}))
            cp_fld=${cp_line[$cpf]}
            echo -n "${cp_fld} "
            ((cp_pos += ${#cp_fld}))
        done
    done
    set +f
    return 0
}
```

### 追踪垃圾邮件者数据流 # # #

# 返回码
declare -i _RC

# 原始输入，从中移除了 IP 地址
# 之后，是需要检查的域名
declare -a uc_name

# 原始输入的 IP 地址被移动到此处
# 之后是需要检查的 IP 地址
declare -a uc_address

# 执行扩展的名称
# 准备进行名称详情查找
declare -a chk_name

# 执行扩展的地址
# 准备进行地址详情查找
declare -a chk_address

# 递归是按名称深度优先的。
# expand_address 维护此列表
# 以防止在域名递归期间
# 重复查找地址。
declare -a been_addr

been_addr=( '127.0.0.1' ) # 白名单本地
# 我们已经检查过（或放弃）的名称
declare -a known_name

# 我们已经检查过（或放弃）的地址
declare -a known_address

# 待检查的零或多个黑名单服务器列表。
# 每个 'known_address' 都将与每个服务器进行检查，
# 并抑制负面响应和失败。
declare -a list_server

# 递归限制 - 设置为为无限制
${SPAMMER_LIMIT:-2}

# 追踪垃圾邮件者信息输出数据 # # #

# 任何域名都可能有多个 IP 地址。
# 任何 IP 地址都可能有多个域名。
# 因此，跟踪唯一的地址-名称对。
declare -a known_pair
declare -a reverse_pair

# 除了数据流变量；known_address
# known_name 和 list_server 之外，以下内容输出到
# 外部图形接口文件。

# 权威链，父节点 -> SOA 字段。
declare -a auth_chain

# 引用链，父名称 -> 子名称
declare -a ref_chain

# DNS 链 - 域名 -> 地址
declare -a name_address

# 名称和服务对 - 域名 -> 服务
declare -a name_srvrc

# 名称和资源对 - 域名 -> 资源记录
declare -a name_resource

# 父节点和子节点对 - 子名称
# 这可能与所遵循的 ref_chain 不同！
declare -a parent_child

# 地址和黑名单命中对 地址->服务器
declare -a address_hits

# 导出接口文件数据
declare -f dot_dump
dump_dot_pend_dummy # 初始为无操作

# 通过将环境变量 SPAMMER_DATA 设置为# 可写文件名来启用数据转储
declare -a dot_file

# 用于 dump-to-dot-file 的辅助函数
dump_to_dot <array_name> <prefix>
dump_to_dot() {
local -a _dda_tmpn
```