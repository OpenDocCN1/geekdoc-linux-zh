
`carol@octarine "/test" cat tolower.sh`

```bash
#!/bin/bash

# 此脚本将所有包含大写字母的文件名转换为

# 仅包含小写字母的文件名。

LIST=$(ls)

for name in "$LIST"; do

  if [[ "$name" != *([[:upper:]])* ]]; then

    continue

  fi

# 原文此处逻辑不完整，仅按格式保留

done
```

### 9.5.1 示例

在接下来的示例中，文件名被转换为小写。如果不需要转换，`continue`语句将重启循环的执行。这些命令不会消耗系统资源，而且可能可以使用`sed`和`awk`解决类似的问题。然而，在执行重型任务时，了解这种结构是有用的，而当在脚本正确的位置插入测试时，这些操作可能根本不是必要的，从而节省系统资源。

```bash
carol@octarine "/test" cat tolower.sh

#!/bin/bash

# 此脚本将所有包含大写字母的文件名转换为

# 仅包含小写字母的文件名。

LIST=$(ls)

for name in "$LIST"; do

  if [[ "$name" != *([[:upper:]])* ]]; then

    continue

  fi
```

## 第 9 章：重复性任务

### 9.2

显示了一个改进后的`picturesort.sh`脚本（见第 9.2.1 节），它可以测试可用磁盘空间。如果磁盘空间不足，脚本将移动上几个月的文件。

注意`HOUR`和`DISKFULL`变量的初始化，以及使用`-is`选项和`date`命令来为`TOREMOVE`获取正确的列表。

## 9.4 I/O 重定向与循环

与其通过测试命令结果或用户输入来控制循环，你也可以指定一个从该文件中读取输入来控制循环。在这种情况下，`read`通常是控制命令。只要输入行不断送入循环中，循环命令的执行就会持续进行。一旦输入行结束，循环就会退出。

由于循环被视为一个命令结构（例如`while TEST-COMMAND; do CONSEQUENT-COMMANDS; done`），因此重定向应该发生在`done`语句之后，以便它以如下形式完成：

```bash
command < file
```

这种重定向也适用于其他类型的循环。

### 9.4.1 输出重定向

在下面的示例中，`find`命令的输出被用作控制`while`循环的`read`命令的输入：

```bash
carol@octarine ~/testdir) cat archiveoldstuff.sh

#!/bin/bash

# 此脚本在当前目录下创建一个子目录，并将

# 旧文件移动到其中。

# 可能会用于 cron（如果稍作修改）每周或

# 每月执行一次。

ARCHIVER='date +%Y%m%d'

DESTDIR="$PWD/archive-$ARCHIVER"

mkdir $DESTDIR

find $PWD -type f -a -mtime +5 | while read file

do

  gzip "$file"; mv "$file".gz "$DESTDIR"

  echo "$file archived"

done
```

文件在移动到归档目录之前会进行压缩。

## 9.5 Break 和 continue

### break 内置命令

`break`语句用于在循环正常结束之前退出当前循环。这在你预先不知道循环需要执行多少次时使用，例如因为它依赖于用户输入。

下面的示例演示了一个可以中断的`while`循环。这是第 9.2.1 节中`wisdom.sh`脚本的稍微改进版本。

```bash
#!/bin/bash

# 此脚本提供格言

# 你现在可以体面地退出了。

FORTUNE=/usr/games/fortune

while true; do

  echo "你想听哪个主题的建议?"

  echo "1. politics"

  echo "2. startrek"

  echo "3. kernelnewbies"

  echo "4. sports"

  echo "5. bofh-excuses"

  echo "6. magic"

  echo "7. love"

  echo "8. literature"

  echo "9. drugs"

  echo "10. education"

  echo

  echo -n "输入你的选择，或输入 0 退出: "

  read choice

  echo

  case $choice in

    1)

      $FORTUNE politics

      ;;

    2)

      $FORTUNE startrek

      ;;

    3)

      $FORTUNE kernelnewbies

      ;;

    4)

      echo "运动浪费时间、精力和金钱。"

      echo "回到你的键盘去吧。"

      echo -e "\t\t\t\t -- \"不健康是我的中间名\" Soggie"

      ;;

    5)

      $FORTUNE bofh-excuses

      ;;

    6)

      $FORTUNE magic

      ;;

    7)

      $FORTUNE love

      ;;

    8)

      $FORTUNE literature

      ;;

    9)

      $FORTUNE drugs

      ;;

    10)

      $FORTUNE education

      ;;

    0)

      echo "好的，再见"

      break

      ;;

    *)

      echo "这不是有效选择，请尝试 0 到 10 之间的数字。"

      ;;

  esac

done
```

注意`break`退出的是循环，而不是脚本。可以通过在脚本末尾添加一个`echo`命令来演示这一点。当输入导致`break`执行时（当用户输入 "0"），这个`echo`也会被执行。

在嵌套循环中，`break`允许指定退出哪一个循环。更多信息请参阅 Bash info 页面。

### continue 内置命令

`continue`语句恢复外层`for`、`while`、`until`或`select`循环的迭代。

在`for`循环中使用时，控制变量获取列表中下一个元素的值。相反，在`while`或`until`结构中使用时，执行从循环顶部的`TEST-COMMAND`开始恢复。

### 9.5.1 示例

在接下来的示例中，文件名被转换为小写。如果不需要转换，`continue`语句将重启循环的执行。这些命令不会消耗系统资源，而且可能可以使用`sed`和`awk`解决类似的问题。然而，在执行重型任务时，了解这种结构是有用的，而当在脚本正确的位置插入测试时，这些操作可能根本不是必要的，从而节省系统资源。

```bash
carol@octarine "/test" cat tolower.sh

#!/bin/bash

# 此脚本将所有包含大写字母的文件名转换为

# 仅包含小写字母的文件名。

LIST=$(ls)

for name in "$LIST"; do

  if [[ "$name" != *([[:upper:]])* ]]; then

    continue

  fi
```
