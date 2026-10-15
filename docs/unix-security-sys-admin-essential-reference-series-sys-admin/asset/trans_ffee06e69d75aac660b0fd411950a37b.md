

脚本随后对表示重复项的条目应用两个 sed 表达式。第一个表达式删除记录中的计数部分，只保留主目录名。第二个表达式将冒号放回目录名中。这些操作为再次通过密码文件进行 egrep 搜索做好了准备。egrep 将收集与这些重复主目录关联的账户名。如果账户名在初始 cut 中被收集，sort 本可以严格按主目录键排序，但 uniq 就无法如此轻松地计数重复项。

记录只有在整个记录匹配时才会被 uniq 视为重复。某些版本的 uniq 允许字段指定——我使用的版本不允许。sort 不会只输出重复的行。uniq 会只输出重复的行，但那样我就无法为每个使用重复目录的登录账户得到一行。

## Listing 2.1 shell 脚本 chkduphome 检查 /etc/passwd(4) 文件并报告任何共享相同主目录的账户名称。

```sh
#!/bin/sh
#
# chkduphome
#
# Report account entries in the /etc/passwd file
# using the same home directories.
#
# Copyright 1994, Lawrence S Reznick

PW_FILE=/etc/passwd        # Point to passwd file
DUP_FILE=tempdup.$$        # egrep search set

echo The following login accounts use the same home dirs as other accounts:

cut -d : -f6 $PW_FILE |
sort |
uniq -c |
egrep -v '^ *1 ' |
sed -e 's/^ *[0-9]*//' -e 's/^ \(.*\)/:\1:/' > $DUP_FILE

egrep -f $DUP_FILE $PW_FILE |
cut -d : -f1,6 |
sort -t : -k 1 |
tr ':' '	'                # 2nd arg has only 1 tab

rm $DUP_FILE
```

为了获取与目录关联的名称，脚本输出到一个文件中，该文件保存所有重复的目录名。确定这些重复项后，让 egrep 在 passwd 文件中搜索包含有问题目录路径的任何行就变得很简单。重复文件中命名的每个目录都有前导和尾随的冒号分隔符，如 /etc/passwd 所用。这些分隔符创建了 whole-field 匹配。它们防止在树中的上层是主目录时发生匹配，并防止匹配同一树中的子目录。例如，如果某个重复账户条目在 /usr 中，程序就不应输出其主目录路径包含 /usr 的每个账户。只有主目录为 /usr 的条目才会匹配。egrep -f 标识重复条目文件，以便 egrep 将为每个 /etc/passwd 行匹配任何重复条目。

表示来自 passwd 文件的重复条目的匹配行被传递给 cut，后者提取用户的账户名和主目录。sort 接收此信息并按主目录对记录进行排序。sort 将所有名称放在单个主目录内，然后在该单个主目录内按名称对行进行排序。最后，为了使输出更易于阅读，tr 将冒号更改为制表符。

chkduphome 的输出保持未装饰，以便可以将其通过管道传输到另一个程序。另一个程序可以根据字段之间的制表符解析输出。当然，如果不需要进一步处理，cron 作业可以简单地将输出通过邮件发送给管理员或组管理员。

## Catching Idle Users

用户工作站空闲时间过长可能代表安全问题。这样的用户可能已让登录保持活动状态但并未在工作站前。如果屏幕保护程序处于活动状态并带有密码保护锁，可能就无需担心。然而，当用户空闲超过一两周时，我开始怀疑用户是否休假时未注销。

idleuser 脚本（Listing 2.2）列出过度空闲的用户。对于此程序，空闲时间的小时或分钟并不重要，只有天数。finger(1) 命令以表格格式提供足够的信息。不幸的是，finger 不会在其表格字段之间输出方便的制表符分隔符。幸运的是，finger 的字段似乎使用统一的字符长度。因此我让 cut 使用那些字符位置范围来提取用户名及其空闲时间，只需确保在数据的字符范围内包含一些分隔空格即可。

当 finger 看到一天或多天的空闲时间时，它会在数字后显示 d。如果我告诉 egrep 查找一个或多个数字后跟该 d，它将把 finger 列表精简为仅过度空闲的记录。

