
让我们解释这三个命令：

```bash
# 命令 1: %s/A/.
# '%s' 意味着“替换”（或“更改”）。
# 'A' 意味着“更改每一行，使得
# %s/A/ 它们将以 'cat ' 开头”。
# 如果你想在 vi 中执行相同的命令，
# 可以按下 ESCAPE 键 (ESC)，然后输入冒号 (:)
# 并输入 !cat / (然后按回车键)。
```

```bash
# 命令 2: %s/$ / >> /tmp/big_file
# '$' 意味着“替换”（或“更改”)。
# '$' 意味着“行尾”记录末尾。
# %s/$ / >> /tmp/big_file / 意味着“更改每行的末尾，
# 以便配合 'cat ' /tmp/big_file”。
```

```bash
# 命令 3: wq “写入并退出”（保存”）。
# 如果你正在使用 vi 编辑器，按下 ESCAPE 键 (ESC)，
# 然后输入冒号 (:)，最后输入 'wq'（后按回车）。
```

好的，我们正在讨论这些更改，现在让我们来实现它们：

### 示例 2：

```bash
# 首先，创建一个小的测试文件作为输入：
```

```bash
print '/tmp/file1' > /home/larry/ROSETTA/test2
print '/tmp/file2' >> /home/larry/ROSETTA/test2
print '/tmp/file3' >> /home/larry/ROSETTA/test2
```

```bash
print "这里是此脚本进行修改前的 test2：\n"
cat /home/larry/ROSETTA/test2
```

```bash
cd /home/larry/ROSETTA/TEMP
for filename in $(ls /home/larry/ROSETTA/test*)
do
    %s/A/cat
    %s/$ /$ >> /tmp/big_file
    wq
done
```

```bash
print "这里是修改后的 test2：\n"
cat /home/larry/ROSETTA/test2
```

```bash
print "如果你偶尔编写脚本，这种技术可以让你看到"
print "这种技术是多么奇妙。文件 'test2' 是一个"
print "我们命名为 test2 的 chmod 755 test2"
print "我们可以让它可执行：./test2"
print "我们可以运行它：./test2"
```

```bash
# 清理 TEMP 目录中的文件：
rm -f /home/larry/ROSETTA/TEMP/* 2>/dev/null
```

```bash
# 完成。脚本：$0
```

# 输出：change_all_TO_THAT.ksh

脚本是如何执行的：`./change_all_TO_THAT.ksh`
输出如下所示：

注释：此脚本检查 `/change_all_TO_THAT.ksh`。
目的：将列表中文件中的 string1 更改为 string2。

### 示例 1：
```bash
# 这里是此脚本进行修改前的测试文件：
```
最棒的巧克力棒是什么？Snickers!!!
perl 的主目录是 `/opt/bin/perl`

正在处理 `/home/larry/ROSETTA/TEMP/test1`

```bash
# 这里是修改后的结果：
```
最棒的巧克力棒是什么？Milky Way
perl 的主目录是 `/usr/bin/perl`

### 示例 2：

```bash
# 这里是此脚本进行修改前的 test2：
```
/tmp/file1
/tmp/file2
/tmp/file3

```bash
# 这里是修改后的 test2：
```
/tmp/file1
/tmp/file2
/tmp/file3
/tmp/file

```bash
如果你偶尔编写脚本，这种技术可以让你看到
这种技术是多么奇妙。文件 'test2' 是一个
我们命名为 test2 的 chmod 755 test2
我们可以让它可执行：./test2
然后我们可以运行它：./test2

清理 TEMP 目录中的文件：

```bash
# 完成。脚本：$0
```

# 输出：change_all_TO_THAT.ksh

脚本是如何执行的：`./change_all_TO_THAT.ksh`
输出如下所示：

注释：此脚本检查 `/change_all_TO_THAT.ksh`。
目的：将列表中文件中的 string1 更改为 string2。

### 示例 1：
```bash
# 这里是此脚本进行修改前的测试文件：
```
最棒的巧克力棒是什么？Snickers!!!
perl 的主目录是 `/opt/bin/perl`

正在处理 `/home/larry/ROSETTA/TEMP/test1`

```bash
# 这里是修改后的结果：
```
最棒的巧克力棒是什么？Milky Way
perl 的主目录是 `/usr/bin/perl`

### 示例 2：
```bash
# 这里是此脚本进行修改前的 test2：
```
/tmp/file1
/tmp/file2
/tmp/file3

```bash
# 这里是修改后的 test2：
```
/tmp/file1
/tmp/file2
/tmp/file3
/tmp/file

如果你偶尔编写脚本，这种技术可以让你看到
这种技术是多么奇妙。文件 'test2' 是一个
我们命名为 test2 的 chmod 755 test2
我们可以让它可执行：./test2
然后我们可以运行它：./test2

清理 TEMP 目录中的文件：

```bash
# 完成。脚本：$0
```

# 输出：change_all_TO_THAT.ksh

脚本是如何执行的：`./change_all_TO_THAT.ksh`
输出如下所示：

# 如果不是普通文件 或者没有大小（为空）或者不是常规文件，则 ...
if [ ! -f "$replacement_data" || ! -r "$replacement_data" ]; then
  print "ERROR" >>$LOG
```

```bash
# print "replacement file does not exist, " >>$LOG
# print "OR is empty, or not readable."
# print "replacement data file: $replacement_data" >>$LOG
# print "script: $0 Timestamp: $timestamp" >>$LOG
```

fi

# 以下 3 个用户中应有一个取消注释：
# 使用以下 list_users 从 /etc/passwd 获取用户 | cut -d: -f1
# list_of_users=$(cat passwd | cut -d: -f1)
# 如果从 NIS 获取用户，使用以下行列出代码：
# 使用以下行测试 几个用户：
# list_of_users=larry_jeanne

```bash
for userid in $list_of_users
do
  file_changed=$STARTING_DIR/$userid.special_file
  if [ -f "$file_changed" ]; # 如果文件存在，则
    print "$nheader" >>$LOG
    cp -p "$file_changed" $file_changed.timestamp 2>>$LOG
    print "stats on the file changed BEFORE it changed" >>$LOG
    ls -l "$file_changed" >>$LOG 2>&1
    print "stats on the replacement file:" >>$LOG
    ls -l "$replacement_data" >>$LOG 2>&1
    cat $replacement_data $file_changed 2>$LOG
    print "stats on the file changed AFTER its data was replaced" >>$LOG
    ls -l "$file_changed" >>$LOG 2>&1
    print "$footer" >>$LOG
```

```bash
else print "ERROR: $userid $file_changed does not EXIST" >>2>&1
done
```
