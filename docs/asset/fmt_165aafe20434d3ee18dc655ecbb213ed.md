
# 初始化后两个变量为 NULL

`PINGSTAT=` # 从 ping 节点接收返回的 ping 数量

`PINGSTAT=` # 第二次尝试时接收到的 ping 数量

`THISTHOST=`hostname`` # 此机器的主机名

################################################################

########################## 在此处定义函数 ###########################

################################################################

function `ping_host`

{

  # 此函数根据 Unix 变体 ping 单个节点
  # set -x # 取消注释以调试此函数
  # set -n # 取消注释以不执行检查语法
  # 查找每个参数，即要 ping 的主机
  if (( $# != 1 ));
  then
    echo "\nERROR: Incorrect number of arguments - $$"
    echo " Expecting exactly one argument\n"
    echo "\t...EXCITING...\n"
    exit 1
  fi

`HOST=$1` # 从 ARG1 获取要 ping 的主机。

# 下面的 case 语句根据 Unix 变体执行正确的 ping
# 命令

case $UNAME in

AIX|OpenBSD|Linux)
  ping -c$(PING_COUNT) $HOST 2>/dev/null
  ;;
HHP-UX)
  ping $HOST $PACKET_SIZE $PING_COUNT 2>/dev/null
  ;;
SunOS)
  ping -s $HOST $PACKET_SIZE $PING_COUNT 2>/dev/null
  ;;
*)
  echo "\nERROR: Unsupported Operating System - $(uname)"
  echo "\n\t...EXITING...\n"
exit 1
)

############################################################

function `ping_nodes`

(

############################################################################

# ping 其他系统检查
# 如果你不希望每个节点都 ping 所有其他节点，可以禁用此项。
# 并不是所有节点都有必要 ping 所有其他节点，
# 虽然你确实希望有多个节点执行 ping 操作，
# 以防 ping 节点宕机。要启用 ping 功能，
# "PINGNODES" 变量必须设置为 "TRUE"。任何其他值都将
# 禁用从此节点的 ping。
# set -x # 取消注释以调试此函数
# set -n # 取消注释以不执行检查命令语法

if [[ $PINGNODES = "TRUE" ]]
then
    echo # 向 $PINGLIST 添加单行内容
    # 遍历 $PINGLIST 中的每个节点
for HOSTPINGING in $PINGLIST # 节点间用空格
    # 列表中未被注释且非空的所有节点
    PINGLIST=$(grep -v '^#' $PINGFILE)
else
    echo "#ERROR: Missing file $PINGFILE"
    echo "\nlist of nodes to ping is unknown...EXITING...\n"
    exit 2
fi

`MAILFILE="/usr/local/bin/mail.list"` # 通知人员列表
if [ -s $MAILFILE ];
then
    # 列表中未被注释且非空的所有节点
    MAILLIST=$(cat $MAILFILE | grep -v '^#')
else
    echo "#ERROR: Missing file $MAILFILE"
    echo "\nList of persons to notify is unknown...\n"
    echo "#No one will be notified of unreachable nodes...\n"
fi

`PING_OUTPUT="/tmp/ping_file.out"` # 用于邮件通知的文件
> $PING_OUTPUT # 初始化为空文件

integer INTERVAL="3" # 重试之间的睡眠秒数

# 初始化后两个变量为 NULL

`PINGSTAT=` # 从 ping 节点接收返回的 ping 数量

`PINGSTAT=` # 第二次尝试时接收到的 ping 数量

`THISTHOST=`hostname`` # 此机器的主机名

################################################################

########################## 在此处定义函数 ###########################

################################################################

function `ping_host`

{

  # 此函数根据 Unix 变体 ping 单个节点
  # set -x # 取消注释以调试此函数
  # set -n # 取消注释以不执行检查语法
  # 查找每个参数，即要 ping 的主机
  if (( $# != 1 ));
  then
    echo "\nERROR: Incorrect number of arguments - $$"
    echo " Expecting exactly one argument\n"
    echo "\t...EXCITING...\n"
    exit 1
  fi

`HOST=$1` # 从 ARG1 获取要 ping 的主机。

# 下面的 case 语句根据 Unix 变体执行正确的 ping
# 命令

case $UNAME in

AIX|OpenBSD|Linux)
  ping -c$(PING_COUNT) $HOST 2>/dev/null
  ;;
HHP-UX)
  ping $HOST $PACKET_SIZE $PING_COUNT 2>/dev/null
  ;;
SunOS)
  ping -s $HOST $PACKET_SIZE $PING_COUNT 2>/dev/null
  ;;
*)
  echo "\nERROR: Unsupported Operating System - $(uname)"
  echo "\n\t...EXITING...\n"
exit 1
)

对于 `$PINGLIST` 中的每个节点，系统都会执行 `echo` 语句和命令替换语句。命令替换语句有三种可能的结果，我们测试了其中两种；最后一种是第一种。(1) `PINGSTAT` 的值为 0，即零。如果数据包数量为 0，则我们休眠 `$INTERVAL` 秒，然后再次访问该节点，此时将收到的数据包采样到 `PINGSTAT2` 变量中。(2) `PINGSTAT` 的值为 NULL。当您尝试 ping 一个系统不知的节点时发生。在这种情况下，我们 `echo` "Unknown host" 并继续处理列表中的下一个节点。(3) `PINGSTAT` 的值不为 0 也不为 NULL，这意味着 ping 成功。请在 `ping_nodes` 函数中学习这些每项测试。

我们在语句中使用的注意事项（notices）。其中每一项都是一个数学测试，因此我们使用双括号进行测试，如下所示：

```
if (( PINGSTAT == 0 ))
```

该语句中有两个注意点。第一个是 `PINGSTAT` 变量前面没有美元符号 (`$`)。当使用双括号方法进行数学测试时，不需要该变量，shell 会假设任何非数字字符串都是此类数学测试中的一个变量。我在前述语句中要提出的第二点是使用双等号 (`==`)。使用这种类型的数学测试时，单等号是赋值，而不是等性测试。这看起来有点奇怪，但你实际上可以在测试中给一个值赋值。在 ( math test ) 方法中测试等性时，请务必在此方法中始终使用双等号 (`==`)。
