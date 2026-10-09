

我该如何处理这个问题？[稍后再处理] r

在合并文件时，*mergemaster* 使用 *sdiff*(1) 将你的命令窗口分成两半。左侧显示当前已安装文件的开头部分，而右侧显示新版本。仅显示存在差异的部分。在你的新 *master.passwd* 文件中，选择你想要的一侧。

```
# $FreeBSD: releng/11.1/etc/master.passwd 299 | # $FreeBSD: stable/11/etc/master.passwd 29936
```

这一行显示了 */etc/passwd* 两个副本的版本控制信息。左侧是来自 releng/11.1 分支的版本，即 11.1。右侧是来自 stable/11 的版本，即 11-stable。未来的 *mergemaster* 运行将使用版本信息（以及其他工具）来确定文件是否需要更新，因此我们的合并文件需要正确的版本号。在左列 (i) 和右列 (r) 之间进行选择。我想要右侧的条目，所以我输入 r。

*mergemaster* 显示下一个差异。

```
root:$6$fD7a5caQtK2bG93EswGfw5G2zNORLq8qxLT8z | root::0:0::0:0:Charlie &:/root:/bin/csh
```

我更改了 root 密码，并且希望保留它。输入 t 以保留左侧版本。

```
> _dhcp:*:65:65::0:0:dhcp programs:/var/empty/:
```

在这个下一个示例中，当前文件中没有条目，而新用户 _dhcp 在新文件中。我们需要用户 _dhcp 来完成 installworld，因此输入 r 选择右侧条目并获取下一个差异。

```
mwlucas:$1$zxU7ddkNS$9GUEEVJH0r.oWyAwU0NXf1:10 <
```

这里是 my 账户。如果我希望在升级后以我自己登录，最好输入 t。

一旦我们遍历了文件中的每个差异，mergemaster 就会呈现我们的下一个选择：

```
Use 'i' to install merged file
Use 'r' to re-do the merge
Use 'v' to view the merged file
Default is to leave the temporary file to deal with by hand

** How should I deal with the merged file? [Leave it for later]
```

查看合并后的文件总是个好主意，除非你已经知道搞砸了并想重做。使用 v 查看你的合并文件，如果看起来正确，则使用 i 安装它。

```
*** You installed a new master.passwd file, so make sure that you run
	/usr/sbin/pwd_mkdb -p /etc/master.passwd'
	to rebuild your password files

Would you like to run it now? y or n [n]
```

只有当你希望新用户账户工作时，才需要重建密码数据库。输入 y。

现在你可以安装新的用户空间了。

## 安装 World

仍处于单用户模式下，你可以使用 make installworld 安装全新的 FreeBSD。你会看到大量信息滚动过屏幕，其中大部分包含单词 install。

```
# cd /usr/src
# make installworld
```

现在你拥有了与你的崭新内核配套的新用户空间。恭喜！

## 过时文件

然而，安装所有新程序并不足够。更新可能会从基础系统中删除程序和文件。要查看哪些内容已过时，请运行 make check-old。

```
# make check-old
>>> Checking for old files
/usr/include/sys/ksyms.h
/usr/lib/clang/4.0.0/include/sanitizer/allocator_interface.h
/usr/lib/clang/4.0.0/include/sanitizer/asan_interface.h
/usr/lib/clang/4.0.0/include/sanitizer/common_interface_defs.h
--snip--
```

这列出了系统中曾经安装但不再需要的每个部分。确认你不再使用这些程序；如果你在使用，要么保留现有的不受支持的程序，要么寻找替代方案。

在输出稍后的部分，你将看到现在过时的共享库：

```
>>> Checking for old libraries
/lib/libzfs.so.2
/usr/lib/debug/lib/libzfs.so.2.debug
/usr/lib/libarchive.so.6
/usr/lib/debug/usr/lib/libarchive.so.6.debug
/usr/lib/libbnfilter.so.5
--snip--
```

最后，你可能会看到不再需要的目录列表。与删除文件相比，删除目录的情况比较少见。

如果你没有专门使用任何旧程序或目录，请使用 make delete-old 删除它们。make(1) 会提示每个文件的名称，并要求你确认你想删除该文件。

```
# make delete-old
>>> Removing old files (only deletes safe to delete libs)
remove /usr/include/sys/ksyms.h? y
remove /usr/lib/clang/4.0.0/include/sanitizer/allocator_interface.h? y
remove /usr/lib/clang/4.0.0/include/sanitizer/asan_interface.h?
```

这很愚蠢。这些文件有几十个。而且我要删除每一个。幸运的是，每个真正的 Unix 都包含自动化工具来处理这种愚蠢行为。

```
# yes | make delete-old
```

所有这些文件都消失了。或者，如果你想使用 FreeBSD 的内置选项，请使用 BATCH_DELETE_OLD_FILES 标志。

```
# make -DBATCH_DELETE_OLD_FILES delete-old
```

不过，我觉得 yes(1) 更容易。

## 过时的共享库

过时的共享库需要更多的小心。许多第三方程序链接到共享库。如果你删除共享库，程序将无法运行。如果你删除了关键应用程序所需的库，这会真的、真的令人讨厌。恢复服务的唯一方法是重新编译程序或替换共享库。我们在第 17 章中讨论共享库。如果你的程序都不需要该库，你可以删除它。然而，识别每个需要该库的程序是一个大麻烦。

例如，检查上面列出的过时共享库列表。其中一个条目是 libzfs.so.2。查看 /lib，我看到我们现在有 libzfs.so.3。也许我不需要两个不同版本的 ZFS 库。但是，这台主机使用 ZFS，而且我安装了一堆 ZFS 实用工具。如果删除旧版本的 libzfs，其中某个程序可能不再工作。这些过时库版本的存在短期内不会造成任何伤害；你可以用旧库和新库一起恢复系统上线，并以更从容的方式重新安装你的附加软件。我们将在本章稍后更新你的 ports。

如果你认为列出的旧库都不重要且可以安全删除，请在删除前备份每一个。只需将库复制到某个 old-libs 目录，当你发现关键软件不再工作时，恢复就会简单得多。

你还可以将旧库复制到 /usr/lib/compat，以便你的程序继续运行，但旧库会被安全地移开。这里的问题是，我们都完全清楚你永远不会去清理那些库。

我更喜欢备份库，然后从活动系统中删除它们。当我发现某个程序无法工作时，我会暂时将缺失的库从备份复制到 compat 目录。额外的烦恼让我足够恼火去解决真正的问题，这样我就可以删除 compat 库了。

```
# make check-old-libs | grep '^/' | tar zcvf -T - -f /root/old-libs.tgz
```

一旦备份了库，删除它们所有。你可以使用 `BATCH_DELETE_OLD_FILES` 选项，但再次，我觉得 `yes(1)` 更容易输入。

```
# yes | make delete-old-libs
```

如果万一删除这些库破坏了 pkg(8)，运行 `pkg-static install -f pkg` 来修复 pkg(8) 本身，或运行 `pkg-static upgrade -f` 来重新安装所有包。

另一个选项是使用 `libchk` 包来识别链接到旧库的程序。

## 重温 mergemaster

我们快完成了！虽然我们已经在 */etc* 中更新了密码和组信息，但我们必须更新其余的文件。mergemaster 有许多特殊功能，都在其手册页中有文档记录。我将特别推荐我发现特别有用的两个功能。

当文件被添加到基础 FreeBSD 安装中时，没有必要将其与任何内容进行比较。`-i` 选项使 mergemaster 自动安装 */etc* 中的新文件。我将在 mergemaster 运行结束时获得自动安装文件列表。

另一组我真正不在意的文件是我未编辑过的文件。例如，FreeBSD 在 */etc/rc.d* 中有几十个启动脚本。如果我没有编辑启动脚本，我只想安装脚本的最新版本。`-u` 标志告诉 mergemaster 自动更新任何我未编辑的基础系统文件。

```
# mergemaster -iU
```

mergemaster 程序检查 */etc* 中的每个文件，并将其与 FreeBSD 基础发行版中的文件进行比较。这与你在安装前运行 mergemaster 的方式完全相同，因此我们不会

