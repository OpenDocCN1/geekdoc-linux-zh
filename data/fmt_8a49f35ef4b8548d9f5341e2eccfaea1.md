
```bash
for G in $GROUP
do
    echo "$GROULIST" | grep -q $G || group_error $G
done

# 如果到达这里说明所有组都是有效的！

WINLIST="" # 将 WINLIST 变量为空

# 遍历 $GROUP 中的每个组
;;

esac

done

done
```

**列表 25.9** broadcast.lksh shell 脚本列表。

# 从 Unix 向 Windows 发送弹出消息

```bash
# 构建要发送消息的节点列表。

for GRP in $GROUP
do
    # 使用 "eval" 显示变量指向的内容！
    # 确保每个组都有一个非空列表
    # 文件

    if [ -s $(eval echo \$GRP) ]
    then
        WINLIST="$WINLIST cat \$GRP" \
        | grep -v # | awk '(print $1)' \
        | uniq"
    else
        group_file_error $(eval echo \$GRP)
    fi
done

case $1 in
    *\?) 
        echo "\n错误：无效参数！"
        usage
        exit 1 
        ;;
esac

################################################################
################################# 主体开始 ##################################

# 确保至少定义了一个节点来发送消息。
# 如果没有，则在此循环中停留，直到在命令行上输入了一个或多个节点

until check_for_null_winlist
do
    echo "\nEnter要发送此消息的一个或多个节点:"
    echo "\n完成后按列表 \n\n"
    echo "节点列表 => \c"
    read WINLIST
done

################################################################

# "if (($# == 0))" 测试结束。

# 提示用户输入要发送的消息。循环直到（继续）
```

**列表 25.9** broadcast.ksh shell 脚本列表。

```bash
# 用户已为要发送的消息输入了至少一个字符。

until check_for_null_message
do
    echo "\nEnter要发送的消息:"
    echo "\n完成后按回车\n\n"
    echo "消息 => \c"
    read MESSAGE
done

################################################################

# 通知用户此消息发送到的宿主机列表...

echo "\n正在向以下主机发送消息:\n"
echo "\nWIN_HOSTS:\n$WINLIST\n\n"

################################################################

echo "\n正在发送消息...\n"

# 遍历 $WINLIST 中的每个主机并发送弹出消息

for NODE in $WINLIST
do
    echo "正在发送到 \$NODE"
    echo \$$NODE | \$SMBCLIENT -M \$NODE 1>/dev/null
    if (( \$? == 0 )); then
        echo "发送成功 => \$NODE"
    else
        echo "发送失败 => \$NODE"
    fi
done

echo "\n"

################################################################

#
# 此代码段默认是被注释掉的
#
# 如果你需要，也可以使用 "wall" 和 "rwall"
# 将消息发送到 Unix 机器。这段代码默认
# 是注释掉的。
#

echo "\n正在向 Unix 机器发送消息...\n"
# echo \$MESSAGE | rwall -h \$UnixHOSTLIST
```

**列表 25.9** broadcast.ksh 脚本列表。

```bash
# echo $MESSAGE | wall
# echo "\n\n消息已发送...\n\n"
# #################################################
# 从系统中删除消息文件
rm -f $MESSAGE
```

**列表 25.9** broadcast.ksh shell 脚本列表。（续）

在学习学习了列表 25.9 后，我希望你能看到这些部分是如何组合在一起以产生逻辑流的。你可能注意到有一个函数 `check_for_smclient_command()`，它检查 `smbclient` 命令是否在 PATH 中。

![](img/70ab22c9088bb2e63808e021dd493267_668_0.png)

**图 25.1** 发送到 Windows 桌面的弹出窗口消息。

## 下载和安装 Samba

你可以从以下 URL 下载最新版本的 Samba：www.samba.org/samba。

从主页选择一个下载站点。可以使用来自世界各地的下载站点。该页面有一个指向 `samba-latest.tar.gz` 的链接，对应最新版本的源码。如果你下载了源代码，则你需要一个 C 编译器来编译 Samba 发布版本。当你开始编译过程时，`./configure` 文件会寻找 `gcc` 或 `cc`。如果找不到合适的 C 编译器，你将无法安装 Samba 代码。出于我们的目的，我们可以下载可用的预编译二进制代码版本。其中一些是旧版本，但 `smclient` 命令可以正常工作。

当你下载了 Samba 源码后，按照以下步骤在你的机器上编译代码。点击跳转到 Samba 最新版本的链接。将代码下载到 Unix 机器上空间充足的目录中，至少要有 500MB。接下来，解压我下载的代码，它是一个用 gzip 压缩的 tar 文件。假设你将 Samba 代码下载到了 `/usr/local` 目录，文件名为 `samba.2.7.latest.tar.gz`。在下载文件时，你可以进行任何命名。列表 25.12 中的后续命令将用于解压、打包和安装 Samba 代码。

```bash
root:yogi@/usr/local > gunzip samba.2.7.latest.tar.gz
root:yogi@/usr/local > tar -xf samba.2.7.latest.tar
root:yogi@/usr/local > cd samba.2.7
root:yogi@/usr/local/samba.2.7 > ./configure
root:yogi@/usr/local/samba.2.7 > make
root:yogi@/usr/local/samba.2.7 > make install
```
