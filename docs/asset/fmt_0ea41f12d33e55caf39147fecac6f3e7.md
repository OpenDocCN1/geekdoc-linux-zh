
```sh
$ cat rolo
#
# rolo - rolodex program to look up, add, and
#        remove people from the phone book
#

# Display menu
#

echo '
        Would you like to:

                1. Look someone up
                2. Add someone to the phone book
                3. Remove someone from the phone book

        Please select one of the above (1-3): \c'

#
# Read and process selection
#

read choice
echo ""
case "$choice"
in
        1) echo "Enter name to look up: \c"
           read name
           lu "$name";;
        2) echo "Enter name to be added: \c"
           read name
           echo "Enter number: \c"
           read number
           add "$name" "$number";;
        3) echo "Enter name to be removed: \c"
           read name
           rem "$name";;
        *) echo "Bad choice";;
esac
$ 
```

注意，这里仅用一个 `echo` 命令就显示了完整的多行菜单，利用的是引号会保留格式和嵌入换行符这一特性。然后 `read` 从用户处获取选择并将其存入变量 `choice`。

`case` 语句用于确定做出了哪个选择。如果选择了选项 1，则表示用户想要在电话簿中查找某人。在这种情况下，会要求用户输入所需姓名，然后以指定的参数调用 `lu` 程序。还要注意，`lu "$name"` 中 `name` 两边的双引号是必需的，以确保用户输入的两个或更多单词作为单个参数传递给 `lu`。

如果用户选择菜单项 2 或 3，也会发生类似的流程。

程序 `lu`、`rem` 和 `add` 来自前面的章节。

以下是一些 `rolo` 的示例运行：

```text
$ rolo

Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book

Please select one of the above (1-3): 2
Enter name to be added: El Coyote
Enter number: 212-567-3232
$ rolo
```

*再试一次*

```text
Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book

Please select one of the above (1-3): 1

Enter name to look up: Coyote
El Coyote        212-567-3232
$ rolo
```

*再来一次*

```text
Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book

Please select one of the above (1-3): 4
Bad choice
$
```

当输入无效选择时，程序会显示 `Bad choice` 然后终止。更友好的做法是循环返回，再次提示用户，直到做出正确的选择。这可以通过将整个程序封装在 `until` 循环中来实现，该循环将一直执行，直到做出有效选择为止。

对 `rolo` 的另一个修改反映了它最可能的用法：由于最常见的操作是查找某人，用户往往会避免输入 `rolo`、再选择选项 1、然后输入所需姓名这一系列步骤。相反，直接输入 `lu name` 要容易得多。鉴于此，让我们给 `rolo` 添加一些有用的命令行参数，以便它也能被高效使用。默认情况下，如果指定了任何参数，`rolo` 将假定用户请求执行查找，并直接调用 `lu`，将所有参数一并传递。如果用户想要快速查找，可以输入 `rolo` 后跟姓名。如果他们想要完整的菜单界面，只需输入 `rolo` 也可以做到。

上述两项修改（循环直到选择有效选项，以及快速查找）被添加到了 `rolo` 的第 2 版中：

```sh
$ cat rolo
#
# rolo - rolodex program to look up, add, and
#     remove people from the phone book -- version 2

#
# If arguments are supplied, then do a lookup
#

if [ "$#" -ne 0 ]; then
        lu "$@"
        exit
fi

validchoice=""        # set it null

#
# Loop until a valid selection is made
#

until [ -n "$validchoice" ]
do
        #
        # Display menu
        #

echo '

Would you like to:

    1. Look someone up
    2. Add someone to the phone book
    3. Remove someone from the phone book

Please select one of the above (1-3): \c'

#
# Read and process selection
#
read choice
echo

case "$choice"
in
    1) echo "Enter name to look up: \c"
       read name
       lu "$name"
       validchoice=TRUE;;

    2) echo "Enter name to be added: \c"
       read name
       echo "Enter number: \c"
       read number
       add "$name" "$number"
       validchoice=TRUE;;

    3) echo "Enter name to be removed: \c"
       read name
       rem "$name"
       validchoice=TRUE;;

    *) echo "Bad choice";;
esac
done
$
```

如果 `$#` 不为零，则直接以命令行上输入的参数调用 `lu`，然后程序退出。否则，执行 `until` 循环，直到变量 `validchoice` 非空。请记住，只有执行选项 1、2 或 3 的 `case` 中的命令 `validchoice=TRUE` 时，它才会被赋值。否则，程序将继续循环。

```text
$ rolo Bill        Quick lookup
Billy Bach    201-331-7618
$ rolo             Let's have the menu this time
```

您想做什么：

- 1. 查找某人

- 2. 将某人添加到电话簿

- 3. 从电话簿中删除某人

请选择以上选项之一（1-3）：4

错误的选择

您想做什么：

- 1. 查找某人

- 2. 将某人添加到电话簿

- 3. 从电话簿中删除某人

请选择以上选项之一（1-3）：0

错误的选择

您想做什么：

- 1. 查找某人

- 2. 将某人添加到电话簿

- 3. 从电话簿中删除某人

请选择以上选项之一（1-3）：1

输入要查找的姓名：Tony

Tony Iannino    973-386-1295

$

## $$ 变量和临时文件

如果系统中有两个或更多人同时使用 `rolo` 程序，就可能出现潜在问题。看看 `rem` 程序，看你能不能发现问题。问题出在用于创建电话簿文件新版本的临时文件 `/tmp/phonebook` 上。

`rem` 程序中的具体语句如下所示：
