
echo "Fingering logged in users . . ."

`finger`

echo "End of processing. Have a nice day. . . ."

echo "========================================"

```
miss_scarlet@tweety$ bash info
Retrieving today's date . . . .
. . . . . . . . . . .
Sun Sep 24 20:09:23 EDT 2000
```

Looking for empty files. Please delete . . . .

`./knife`

`./lead_pipe`

`./rope`

`./candlestick`

`./kde/share/config/ksapshotrc`

`./mail`

`./friends/colonel_mustard`

`./friends/emily`

`./friends/marshall`

`./friends/miss_scarlet`

`./x`

`./gobbige`

`./databases`

`./Emmy_Horse_File`

`./ch15_newpics`

```
Fingering logged in users
```

| Login | Name | Tty | Idle | Login Time | Office | Phone |
|---|---|---|---|---|---|---|
| candace | candace leiden | /5 | | Sep 24 20:15 | (192.168.0.5) | | |
| miss_scarlet | emily lauren scar | /0 | 1:32 | Sep 24 18:10 | (192.168.0.5) | | |
| miss_scarlet | emily lauren scar | /4 | | Sep 24 19:27 | (192.168.0.5) | | |
| root | root | /1 | 2d | Sep 10 22:12 | (:0) | | |
| root | root | /2 | 2d | Sep 10 22:12 | (:0) | | |

End of processing. Have a nice day. . . .
==================================

# 实现一个简单的菜单

在本章前面的部分，你看到了在 `rc.local` 中使用 `case` 语句根据计算机架构设置值。`case` 语句的另一个常见用途是评估并对用户的菜单选择执行操作。如果你希望用户仅通过菜单访问命令和应用程序，可以编写如下所示的脚本并在用户的 `.bash_profile` 文件中调用它。从 `.bash_profile` 执行该脚本将会在用户登录并使用 bash 时自动显示菜单。

```
#! /bin/bash

# /home/miss_scarlet/bash_profile_menu

#

# 显示菜单

echo "Please select an option from the menu "

echo "Option          Description"

echo "--------------------------------"

echo "List files in your directory"

echo "Display a file"

echo "Print a file"

echo "Exit"

# 获取用户的选择。

# 使用 case 语句控制逻辑。

case $menu_choice in

  l)

    ls -l

    ;;

  d)

    echo "File to display"

    ;;

  p)

    echo "File to print"

    ;;

  r)

    echo "File to remove"

    ;;

  *)

    echo "Exiting..."

    ;;

esac
```

`miss_scarlet@tweety$ bash_profile_menu`

Please select an option from the menu

Option          Description

--------------------------------

# 第 30 章 系统管理员的脚本脚本 583

Name of file(s) to remove?

xxxxxxxx

# 第 30 章 - 系统管理员的 Shell 脚本

```bash
# 家目录是 /etc/passwd 中的第六个字段。
Home_Dir=`grep $1 /etc/passwd | cut -d ' ' -f6`

# du 用制表符分隔字段，我们只需要第一个字段
used=`du -s $Home_Dir | cut -f1`
```

```bash
# **** 主程序 *****
# 主程序
#
while read username
do
    space_used $username
    echo "$username has used $used"
done < $DiskHogFile
```

# 使用函数测试用户输入

如果你在脚本中对用户错误进行测试，就可以让你的脚本更易用。最常见的用户错误之一是忘记传递脚本所需的正确数量的命令行参数。你可以创建一个简单的函数来检查命令行参数，如果用户输入的参数数量不，则显示语法提示。

```bash
#!/bin/bash

# usage_check.bsh

# 检查命令行上的位置参数

# 包含一个显示语法提示的用法函数

usage() {
    echo "Error"
    echo "Correct usage: disk_report.bsh username"
    echo "Reports on disk use by user"
}

# 测试命令行上是否存在 1 个位置参数。
# 如果位置参数的数量不是 1，则调用
# usage 函数并退出。
if [ $# != 1 ];
then
    usage
    exit
fi

# 继续处理报告。
```

`root@flyingpenguin# chmod +x $HOME/check_usage.bsh`

`root@flyingpenguin# $HOME/check_usage.bsh`

Error

# 第 V 部分 ♦ 高级系统管理与网络管理

```bash
Correct usage: disk_report.bsh username
Reports on disk use by user
```

`root@flyingpenguin# $HOME/check_usage.bsh emily miss_scarlet`

Error

Correct usage: disk_report.bsh username

Reports on disk use by user

`root@flyingpenguin# $HOME/check_usage.bsh emily`

# 用法正确，报告处理在此处继续。
