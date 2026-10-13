
## Rolo 再探

本章介绍 rolo 程序的最终、大幅改进版本，它增加了额外的选项，并允许更通用的条目类型（不仅仅是姓名和号码）。本章各节讨论 rolo 的各个组成部分，首先从 rolo 主程序本身开始。在本章末尾，展示了示例输出。

### 数据格式化的考量

虽然本书前面展示的初始姓名与号码 rolo 程序很方便，但毫无疑问，一个更有用的程序应当不仅能存储姓名和号码。例如，你可能还想保存地址和电子邮件地址。新的 rolo 程序允许电话簿中的条目由多行组成。一个典型条目可能是

```
Steve's Ice Cream
444 6th Avenue
New York City 10003
212-555-3021
```

为了提高程序的灵活性，单个条目现在可以包含任意多行。电话簿中的另一个条目可能是

```
YMCA
(201) 555-2344
```

为了在逻辑上分隔电话簿文件中的条目，每个条目都会被“打包”成一行，方法是将条目中结尾的换行符替换为另一个字符。我们随意选中了插入符 ^，因为它在普通的用户输入、地址等中极少出现。这个决定的唯一影响是，该字符不能作为条目本身的一部分使用。

使用这种技术，上面显示的第一个条目将以如下形式存储在电话簿文件中：

```
Steve's Ice Cream^444 6th Avenue^New York City 10003^212-555-3021^
```

而第二个条目为

```
YMCA^(201) 555-2344^
```

当条目以此格式存储时，处理起来变得非常容易，这证明了真正深入思考问题和解决方案，能在进一步开发时带来巨大收益。

```sh
rolo
#
# rolo - rolodex program to look up, add,
#        remove and change entries from the phone book
#
#
# Set PHONEBOOK to point to the phone book file
# and export it so other progs know about it
# if it's set on entry, then leave it alone
#
: ${PHONEBOOK:=$HOME/phonebook}
export PHONEBOOK
if [ ! -e "$PHONEBOOK" ] ; then
        echo "$PHONEBOOK does not exist!"
        echo "Should I create it for you (y/n)? \c"
        read answer

        if [ "$answer" != y ] ; then
                exit 1
        fi

        > $PHONEBOOK || exit 1       # exit if the creation fails
fi

#
#
# If arguments are supplied, then do a lookup
#

if [ "$#" -ne 0 ] ; then
        lu "$@"
        exit
fi

#
# Set trap on interrupt (DELETE key) to continue the loop
#

trap "continue" SIGINT

#
# Loop until user selects 'exit'
#

while true
do
                #
                # Display menu
                #
                echo '
                Would you like to:

                        1. Look someone up
                        2. Add someone to the phone book
                        3. Remove someone from the phone book
                        4. Change an entry in the phone book
                        5. List all names and numbers in the phone book
                        6. Exit this program

                Please select one of the above (1-6): \c'

                #
                # Read and process selection
                #

                read choice
                echo "$choice"
                case "$choice"
                in
                        1) echo "Enter name to look up: \c"
                           read name

                           if [ -z "$name" ] ; then
                                   echo "Lookup ignored"
                           else
                                   lu "$name"
                           fi;;
                        2) add;;
                        3) echo "Enter name to remove: \c"
                           read name
                           if [ -z "$name" ] ; then
                                   echo "Removal ignored"
                           else
                                   rem "$name"
                           fi;;
                        4) echo "Enter name to change: \c"
                           read name
                           if [ -z "$name" ]; then
                              echo "Change ignored"
                           else

                              change "$name"

                           fi;;
                        5) listall;;
                        6) exit 0;;
                        *) echo "Bad choice\a";;
                esac
done
```

新代码的最开头出现了一处改进：程序不再要求用户在主目录中预先拥有电话簿文件，而是先检查 PHONEBOOK 变量是否已设置。如果已设置，则假定其中包含电话簿文件的名称。如果未设置，则将其默认设为 $HOME/phonebook。

程序随后检查实际文件是否存在，如果不存在，则询问用户是否希望创建它。可以想象，这大大改善了首次使用的体验。

这个版本的 rolo 在菜单上也有几个新选项。由于单个条目可能相当长，现在新增了一个编辑选项，允许用户更新特定条目。当然，在此之前，更改条目的唯一方式是先删除它，再添加一个全新的条目。

另一个选项是列出整个电话簿。使用此选项时，仅显示每个条目的第一行和最后一行（字段）。这假定用户遵循某种约定，例如将姓名放在第一行，号码放在最后一行。

整个菜单选择代码块现在也位于 while 循环内，这样 rolo 会持续显示菜单，直到用户选择退出程序。

正如我们上一章讨论的，请注意在进入循环之前执行了一条 trap 命令。这条 trap 指定：如果用户产生中断（SIGINT），就执行 continue 命令。如果用户在执行某个操作（例如列出整个电话簿）的途中按下 Ctrl-C，程序将停止当前操作并重新显示主菜单。

由于条目现在可以跨任意多行，选择 add 时执行的操作也发生了变化。rolo 不再询问姓名和号码，而是调用 add 程序来获取条目，并让该函数负责提示用户并判断数据输入何时完成。

对于查找、更改和删除选项，现在会进行一次检查，以确保用户在被要求输入姓名时不会仅按 Enter 键而输入空值。这避免了 grep 在收到空的第一个参数时可能发出的正则表达式错误。

现在让我们看看 `rolo` 所使用的各个程序，特别关注数据格式的变化如何在整个设计中产生连锁反应。每个原始程序都已更改，以适应新的条目格式并更加用户友好。

### add

```sh
##
# Program to add someone to the phonebook file
#

echo "Type in your new entry"
echo "When you're done, type just a single Enter on the line."

first=
entry=

while true
do
        echo ">> \c"
        read line

        if [ -n "$line" ] ; then
                entry="$entry$line"

                if [ -z "$first" ] ; then
                        first=$line
                fi
        else
                break
        fi
done

echo "$entry" >> $PHONEBOOK
sort -o $PHONEBOOK $PHONEBOOK
echo
echo "$first has been added to the phone book"
```

该程序向电话簿添加条目。它会持续提示用户输入行，直到输入一个仅含 Enter 的行（即完全空白的行）。每输入一行，都会被追加到变量 `entry` 中，并使用特殊的 `^` 字符在逻辑上分隔字段。

当退出 while 循环时，新条目会被添加到电话簿末尾，然后对文件进行排序。

### lu

```sh
lu

#
# Look someone up in the phone book
#

name="$1"
grep -i "$name" $PHONEBOOK > /tmp/matches$$

if [ ! -s /tmp/matches$$ ] ; then
    echo "I can't find $name in the phone book"
else
        #
        # Display each of the matching entries
        #

        while read line
        do
                display "$line"
        done < /tmp/matches$$
fi

rm /tmp/matches$$
```

这是用于在电话簿中查找条目的程序。不过，现在匹配的条目会被写入文件 `/tmp/matches$$`，以便在没有任何匹配项的情况下也能改善用户体验。

如果这个输出文件的大小为零（`test -s`），则说明未找到匹配项。否则，程序进入循环，从文件中读取每个匹配行并显示给用户。一个新的名为 `display` 的程序用于解开以 ^ 分隔的字段，并将它们转换为多行输出条目。`rem` 和 `change` 程序也使用这个新程序来显示条目。

还要注意脚本中的 grep 增加了 `-i` 标志。这允许不区分大小写的匹配，因此搜索“steve”也能匹配“Steve”。这是一个很好的例子，说明对 Unix 命令中 grep 各标志的实用了解，可以轻松地让你的脚本更强大、更易用。

### display

```sh
display

#
# Display entry from the phonebook
#

echo
echo "----------------------------------------"
```
