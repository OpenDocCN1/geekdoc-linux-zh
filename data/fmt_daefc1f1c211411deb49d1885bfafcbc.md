
```
[root@booboo #] date %+Y-%m-%d %H:%M:%S
2007-12-11 08:22:07
[root@booboo #]#
```

现在，我们如何用这个新的时间戳修改摘要文件？我们可以使用 `sed` 语句进行字符替换。查看列表 27-14 中的此 `sed` 语句，并在末尾查看详情。

```
sed $(grep Expire $(B)/$(H)/$(IMAGE_NAME)/summary)*$(grep Expire $(B)/$(H)/$(IMAGE_NAME)/summary | cut -f 1-4 -d ' ')
$EXPIRE_STAMP*$(B)/$(H)/$(IMAGE_NAME)/summary >
$$(B)/$(H)/$(IMAGE_NAME)/summary2

if (( $? == 0 ));
then
mv $(B)/$(H)/$(IMAGE_NAME)/summary2 $(B)/$(H)/$(IMAGE_NAME)/summary
```

列表 27-14 使用 `sed` 语句修改摘要文件

该 `sed` 语句是一个跨越四行的单摘要行。此 `sed` 语句首先对摘要文件中的 `Expire` 组分组，并将此结果作为替换的值。`sed` 语句的第二部分从摘要文件中提取相同的行，但使用 `cut` 命令提取前四个字段，随后跟上我们的新时间戳。此替换结果被重定向到新文件名 `summary2`。如果 `sed` 语句的返回码为 0，我们将 `summary2` 文件移动并替换摘要文件。通过此更改，备份现在已过期但尚未删除。

# 添加新备份

要添加新备份，我们需要做的只是在现有的库（bank）中创建一个新的库（vault），并创建一个 `default.conf` 文件来定义备份。为了创建这个新的 `default.conf` 文件，我们需要向用户查询信息以及我们已经知道的一些信息。查看列表 27-15 中的 Dirvish 添加新备份菜单。

![](img/7585d864ba54b249b05d6a57265e6a0e_915_0.png)

列表 27-15 Dirvish 添加新备份菜单

# 第 27 章使用 dirsync 和 rsync 创建快照类型备份 885

| 选项 | 说明 |
| :--- | :--- |
| 2) | 为此备份选择一个库 (Bank) |
| 3) | 输入要备份的目录树 |
| 4) | 输入忽略的文件和目录 |
| 5) | 输入每个备份保留的天数 |
| 6) | 将新备份添加到 Dirvish |
| 7) | 创建初始备份 |
| 8) | 主菜单 |

选择每个选项以添加新备份

输入选项：

**列表 27-15（续）**

要创建新备份，用户需要选择每个选项。选项 1–5 可以顺序选择，添加新备份定义并运行初始备份（选项 6 和 7）应在该系列的最后完成。

让我们逐一查看。在选项 1 中，我要求用户输入我们要添加到 Dirvish 的服务器主机名。请记住；我写这段代码是为了备份一组服务器，因此主机名就是我们正在创建的新库（vault）的名称。我们在库中搜索输入的库/主机名，以确保它已存在。该选项的代码在列表 27-16 中。

```
echo -e "\n\t输入此备份的主机名: \c"
read HN
for B in $BANK_LIST
do
P=$(find $B -type d -name $HN)
if [ -z $P ]
then
echo -e "\n\t警告: 库 HN 已存在于以下库中:"
echo -e "\n\$P"
echo -e "\n\t按回车继续...\c"
read KEY
fi
```

**列表 27-16** 输入主机名并确保其不存在于库中的代码

注意，我们使用 `find` 命令在所有库中搜索此新库/主机名。在此脚本中，每个主机只能有一个库。

选项 2 显示了 Dirvish 配置文件 `master.conf` 中定义的所有库。然后我们要求用户输入用于备份的库。此代码在列表 27-17 中。

```
FINISH=0

until (( FINISH == 1 )); do

  clear

  BANK=

  echo -e "\n\t选择一个库来存储此备份\n"

  echo -e "\n\t可用库:\n"

  for B in $BANK_LIST

  do

    echo -e "\t$B"

  done

  echo -e "\n请选择库: \c"

  read BANK

  if echo $BANK_LIST | grep -q "$BANK"

  then

    echo "已选择 $BANK"

    FINISH=1

  else

    echo "$BANK 选择无效"

  fi

done
```

**列表 27-17** 显示所有库并请求选择的代码

注意在选项 27 中，我们验证所选库是有效的。在选项 3 中，我们要求输入要备份的目录树。在选项 4 中，我们输入要忽略的文件。`read_input` 函数的代码如下：

```
read_input () {

  LINE=

  while true

  do

    read ENTRY

    if [ "$ENTRY" = "99" ];

    then

      echo "$LINE"

      break

    fi

    LINE="$ENTRY"

  done

}
```

**列表 27-18** `read_input` 函数

`read_input` 函数的逻辑是循环读取直到输入 99，这信号着循环结束。在列表 27-19 中显示排除项。

```
echo -e "\n输入要备份的目录树: \c"
read TREE
if [ "$HN" = "$(hostname)" ];
then
  ls "$TREE"
else
  ssh "$HN" "ls"
fi

echo -e "\n排除任何文件或目录吗? (y/n):"
read ANS3

case $ANS3 in

  y|Y)

    echo "\n要排除的项:\n"
    IGNORE_LIST=$(read_input)
    continue
    ;;

  n|N)

    IGNORE_LIST=$(echo)
    continue
    ;;

  *)

    echo "\n无效输入...\n"
    ;;

esac
```

**列表 27-19** 读取并保存排除数据

在显示了指定树中的所有文件后，我们询问用户要保留备份的天数。查询代码如下所示：

```
echo -e "\n每个备份过期天数: \c"
read DAYS
```

很简单。我们只需将变量赋值给 `DAYS`。

选项 6 添加备份是实际上创建创建新 `default.conf` 文件的地方。查看列表 27-20 中的代码，我们将在末尾介绍详情。

```
build_default_conf ()

{

  #在此处定义文件和变量
  HN="$1"               # 要添加的主机名
  BANK="$2"             # 用于备份的库
  DAYS="$3"             # 过期天数
  TREE="$4"             # 要备份的目录树
  IGNORE_LIST="$5"      # 要忽略的文件和目录
  OUTFILE="default.conf $6" # 输出文件名
  # 以下所有输出都用于构建
  # 此备份的新 default.conf 文件
  {

    echo "client: $HN"
    echo "bank: $BANK"
    echo "server: $DIRVISH_SERVER"
    echo "expire: $DAYS day"
    echo "index: gzip"
    echo "log: gzip"
    echo "image: $HN-%Y%m%d%H%M%S"
    echo "tree: $TREE"
    echo ":exclude:"
    echo "$IGNORE_LIST" | sed '/^$/d' | while read Q;
    do
      echo -e "\t$Q"
    done

  } >"$OUTFILE"

}
```
