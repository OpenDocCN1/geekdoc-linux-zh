
```bash
echo "HELLO WORLD - $DATE_ST" > $UNIQUE_FN &

# 无操作，什么都不做，但返回代码为零
}

###########################################################
#################################### 主体开始 #######################################
###########################################################

SCRIPT_NAME=$(basename $0) # 查询此脚本的名称

# 检查参数数量是否正确——恰好为 1 个

if (( $# != 1 ));
then
    echo "ERROR: 使用错误...正在退出..."
    usage
fi

# 我们需要将哪个文件名唯一化？

BASE_FN=$1 # 获取要唯一化的基础文件名

RANDOM=$$ # 初始化 RANDOM 环境变量
# 使用当前进程 ID (PID)

UPPER_LIMIT=32767 # 设置 UPPER_LIMIT

CURRENT_SECOND=99 # 初始化为非当前秒数
LAST_SECOND=98 # 初始化为非当前秒数

USED_NUMBERS= # 初始化为空

PROCESSING="TRUE" # 初始化为运行模式

while [[ $PROCESSING = "TRUE" ]]
do
    DATE_ST=$(get_date_timestamp) # 获取当前日期/时间
    CURRENT_SECOND=$(get_second) # 获取当前秒

    RN=$(range_fixed_length_random_number_typeset) # 获取一个新数字

    # 检查在这一秒内是否已经使用过该数字
    if (( CURRENT_SECOND == LAST_SECOND ));
    then
      UNIQUE=FALSE # 初始化为 FALSE
      while [[ "$UNIQUE" != "TRUE" ]] && [[ -z "$UNIQUE" ]]
      do
        # 该数字在这一秒内是否使用过？
        echo $UNIQUE_NUMBERS | grep $RN >/dev/null 2>&1
        if (( $? == 0 ));
        then
          # 已使用..获取另一个数字
          RN=$(range_fixed_length_random_number)
        else
          # 数字在这一秒内是唯一的...
          UNIQUE=TRUE
          # 将此数字加入唯一数字列表
          USED_NUMBERS="$USED_NUMBERS $RN"
        fi
      done
    else
      USED_NUMBERS= # 新的一秒..重新初始化为空
    fi
    # 将唯一文件名赋值给变量 UNIQUE_FN
    UNIQUE_FN=$$(BASE_FN).$(DATE_ST).$RN
    # echo $UNIQUE_FN # 注释掉这一行！

    LAST_SECOND=$CURRENT_SECOND # 保存上一次秒的值
    # 我们有了一个唯一文件名...
    #
    # 在此处处理某些内容并将输出重定向到 $UNIQUE_FN
    my_program
    #
    # 如果处理完成，将 "FALSE" 赋值给
    # PROCESSING 变量
    # if [[ $MY_PROCESS = "done" ]]
    then
      #
      PROCESSING="FALSE"
    fi
done
```

### Listing 21.10 `mk_unique_filename.ksh` 脚本列表

在这个 shell 脚本中我们需要五个函数。按照惯例，我们需要一个用于正确用法的函数。我们期望此 shell 脚本恰好接收一个参数，即**基础文件名**，用于将其转换为唯一文件名。第二个函数用于获取日期/时间戳。

`date` 命令有很多开关，允许创建灵活的日期/时间戳。我们对月、日、年、时、分、秒使用两位数字，并在输出的日期和时间部分之间使用句号（.）。这个结构是添加到文件名中的第一部分。`date` 命令具有以下语法：`+%m%d%y.%H%M%S`。

我们还需要当前分钟的当前秒。当前秒数是为了确保我们创建的伪随机数在每一秒都是唯一的，从而产生唯一的文件名。再次使用 `date` 命令，语法如下：`+%S`。

`in_range_fixed_length_random_number_typeset` 用于在此脚本中创建我们的伪随机数。该函数保持每个被创建数字的位数一致。通过将基础文件名、时间戳和唯一数字组合，我们确保每个文件名具有相同数量的字符。

脚本中又添加了一个函数。`my_program` 函数用于指向需要所有这些唯一文件名的程序或 shell 脚本。与其尝试将所有内容放入内部 `my_program` 函数并在已运行的 shell 上调试内部函数，不如指向一个外部程序或 shell 脚本更好。当然，我假设你会在每次迭代中执行一次程序，事实可能并非如此。无论如何，此脚本将展示在保持循环的同时创建唯一文件名的概念。

在 shell 脚本主体的“BEGINNING OF MAIN”部分，我们首先查询系统获取 shell 脚本的名称。我们检查每个命令行参数。这个唯一的命令行参数就是我们用于创建唯一文件名的基础文件名。下一步是将基础文件名赋值给变量 `BASE_FN` 以备后用。`RANDOM` 环境变量用初始种子初始化，种子决定了当前的进程 ID (PID)。这种技术有助于确保种子在每次执行脚本时发生变化。对于此脚本，我们想使用最大值作为 `UPPER_LIMIT`。

# 542 第 21 章

```
/tmp/myfilename.120601.131516.07809
/tmp/myfilename.120601.131524.03831
/tmp/myfilename.120601.131524.21628
/tmp/myfilename.120601.131524.19801
/tmp/myfilename.120601.131518.13556
/tmp/myfilename.120601.131518.24618
/tmp/myfilename.120601.131518.12763
```

# 新创建的文件列表
