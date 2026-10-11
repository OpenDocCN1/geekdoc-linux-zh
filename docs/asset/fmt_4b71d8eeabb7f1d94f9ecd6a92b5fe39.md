
```bash
PHONELIST=~/.phonelist.txt
```

```bash
# 如果没有命令行参数 ($#)，
# 说明有问题问题，所以询问他们在谈论什么。
if [ $# -lt 1 ]; then
echo "Whose phone number did you want?"
exit 1
fi
```

```bash
# 你是否想添加一个新的电话号码？
if [ $1 = "new" ]; then
shift
echo $* >> $PHONELIST
echo "* added to database"
exit 0
fi
```

```bash
# 没有。但文件里已经有内容了吗？
# 毕竟这可能可能是我们第一次使用它。
if [ ! -s $PHONELIST ]; then
echo "No name in the phone list!"
exit 1
else
grep -i "$*" $PHONELIST # 静默搜索文件
if [ $? -ne 0 ]; then # 我们找到东西了吗？
echo "Sorry, that name was not found in the phone list"
else
grep -i "$*" $PHONELIST
fi
exit 0
fi
```

# 第二部分：成为 Linux 进阶用户

所以，如果你在当前目录下创建了名为 `ph` 的电话列表文件，你可以从 shell 中输入以下内容来尝试你的 `ph` 脚本：

```bash
$ chmod 755 ph
$ ./ph new "Mary Jones" 608-555-1212
added to database
$ ./ph Mary
Mary Jones 608-555-1212
```

`chmod` 命令使 `ph` 脚本具有可执行性。`./ph` 命令从当前目录运行带有新选项的 `ph` 命令。这会将 Jones 作为名称、608-555-1212 作为数字添加到数据库（`$HOME/.ph.txt`）。下一个 `ph` 命令会在数据库中搜索名称 Mary，并显示 Mary 的电话电话列表条目。如果脚本运行正常，请将其添加到路径中的目录中（例如 `$HOME/bin`）。

# 备份脚本

因为没有什么是永远有效的，而且错误总会发生，所以在在处理计算机时，备份是生活的常态。这个简单的脚本会备份你的 Fedora 或 RHEL 系统上所有用户家目录中的数据。

```bash
#!/bin/bash

# (@)/my_backup
# 一个非常简单的备份脚本
#
# 修改 TAPE 设备以匹配你的系统。
# 检查 /var/log/messages 以确定你的磁带设备。
# 你可能还需要为内核添加 scsi-tape 支持。
TAPE=/dev/rft0

# 倒带磁带设备 $TAPE
mt $TAPE rew

# 获取家目录列表
HOMES=$(grep /etc/passwd | cut -f6 -d':')

# 备份这些目录中的数据
tar cv $TAPE $HOMES

# 倒带并弹出磁带。
mt $TAPE rewoff
```
