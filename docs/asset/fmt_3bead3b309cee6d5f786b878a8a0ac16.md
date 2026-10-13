
# cpio

## 语法概要
```
cpio [-o|--create] [-0acvBLV] [-C bytes] [-H format] [-M message]
-R [[user@]host]] -F [[user@]host][:archive]] -F [::archive]
---format=] [--make-directories] [-nonmatching] [-preserve-modification-time] [-numeric-uid-gid] [-swap]
---unconditional] [-verbose] [-block-size=blocks] [-swap]
```

## 简述
`cpio` 是一个类似于 `tar` 的存档工具。`cpio` 将文件复制到存档（输出模式）、从存档中提取文件（输入模式）、读取存档的目录列表并将文件从一个目录复制到另一个目录（传递模式）。`cpio` 与 `tar` 格式兼容，但有两个限制：

- `cpio` 无法存档名称超过 100 个字符的文件。
- `cpio` 无法存档“特殊”（块或字符设备）文件。

## 常用选项
- `-o` 创建存档。
- `-i` 提取存档。
- `-l` 列出存档内容。
- `-v` 在 `cpio` 运行时显示信息（详细）。

## 示例 1
```
cpio -0 < list > ArchivedFile
```
此命令将列表中的所有文件归档到名为 "ArchivedFile" 的文件中。

## 示例 2
```
cpio -i ArchivedFile
```
此命令获取存档文件 `ArchivedFile` 并提取它。

## 示例 3
```
cpio -l ArchivedFile
```
此命令获取 `ArchivedFile` 并查看其内容。

# crontab

## 简述
`crontab` 允许用户调度命令供 `cron` 守护进程运行。

## 常用选项
- `-l` 列出当前 `crontab`。
- `-r` 删除当前 `crontab`。
- `-e` 编辑当前 `crontab`。

## 示例 1
```
crontab -e
```
允许用户编辑 `crontab`。

## 示例 2
```
crontab -l
```
将用户的 `crontab` 显示到标准输出。

# debugfs

`ext2` 文件系统调试器。

## 语法概要
```
debugfs [-f cmd_file] [-R request] [-V] [-w [device]]
```

## 简述
`debugfs` 是一个文件系统调试器，用于检查和更改 `ext2` 文件系统的状态。

## 常用选项
- `-w` 指定以读/写模式打开文件系统。
- `-f` `Debugfs` 将从指定的命令文件中获取命令。

## 示例 1
```
debugfs /dev/hda
```
对第一个 IDE 分区上的文件系统进行调试。

## 示例 2
若要指示 `debugfs` 在第一个 IDE 分区上运行并从文件 `command.txt` 获取命令，请输入：
```
debugfs -f command.txt /dev/hda
```

# depmod

处理可加载内核模块的依赖描述。

## 语法概要
```
depmod -a [-ensqV] -C configfile [-F kernelsyms] [-b basedirectory] forced_version]
depmod [-ensq] [-F kernelsyms] module1.o module2.o...
```

## 简述
`depmod` 创建依赖文件，供 `modprobe` 自动加载模块使用。依赖文件根据命令行模块或配置文件中提供的信息创建。

## 常用选项
- `-a` 加载所有模块。
- `-d` 在调试模式下运行 `depmod`。`depmod` 输出其发出的所有命令。
- `-e` 输出每个模块未解析符号列表。
- `-v` 输出所有处理模块的列表（详细模式）。
- `-i` 强制 `depmod` 忽略符号版本。
- `-m <file>` 使用 `<file>` 中的符号。
- `-s` 使用系统日志记录错误。

## 示例 1
```
depmod
```
更新当前模块的依赖列表。

## 示例 2
```
depmod -a
```
更新所有模块的依赖列表。

# dial

用于电话线 IP 链路的需求拨号守护进程。

## 语法概要
```
/usr/sbin/dial [device1...] [options...] -- [pppd options...]
```

## 简述
`dial` 是一个允许需要时建立和断开 PPP 连接的守护进程。

## 常用选项
- `-f <file>` 或 `-file <file>` 读取文件中的额外命令。

## 示例 1
```
dial
```
启动拨号守护进程。

## 示例 2
```
dial -f /etc/dialup.conf
```
读取文件 `/etc/dialup.conf` 配置和额外选项。

# 点 (.)

`.` 是当前目录的缩写。

## 示例 1
将 `/etc` 目录的所有文件复制到当前目录，请输入：
```
cp /etc/* .
```

## 示例 2
它也可以作为相对路径的起点；例如：
```
find ./test -name quiz1
```
这将找到你当前工作目录下 `test` 子目录下的文件 `quiz1`。

> **注意** 许多命令假设点号存在且你想在当前目录执行执行命令。

例如，你可以输入：
```
ls
```
或者，你也可以输入：
```
ls .
```
它们将执行相同的操作。

# 双点 (..)

此命令是当前目录父目录的别名。

## 示例 1
要移动到当前目录的父目录，你需要输入：
```
cd ..
```

## 示例 2
它也可以作为相对路径的起点；例如：
```
find ../test -name quiz1
```
这将找到你当前父目录下 `test` 子目录下的文件 `quiz1`。

# dump

文件系统备份。

## 语法概要
```
dump [0123456789BbhfusTdwn [argument...]] filesystem
dump [0123456789BbhfusTdwn [argument...]] directory
```

## 简述
`dump` 是一个强大的命令，用于检查文件系统以确定哪些文件需要备份。级别 0 的 `dump` 是全备份，而级别 1–9 是具有优先级的增量备份。

## 常用选项
- `-0-9` 指定备份大小。级别 0 `dump` 复制整个文件系统，数字 0 以上指定大小递减的 `dump`。
- `-d` 允许用户将带密度设置为特定值。
- `-n` 如果程序需要注意，通知组用户中的所有人。
- `-T date` 只对自指定日期以来修改的文件进行备份。
- `-W` 打印哪些文件系统需要 `dump` 信息。

## 示例 1
```
dump 0 /home
```
将整个 `home` 目录备份到默认带单元。

## 示例 2
```
dump 1 /usr
```
将 `usr` 目录增量备份到默认带单元。

# e2fsck

检查 Linux 第二级扩展文件系统。

## 语法概要
```
e2fsck [-ABCDfGLPrstvywf] [-block] device
```

## 简述
`e2fsck` 检查文件系统错误。

## 常用选项
- `-c` 检查坏块。
- `-d` 显示坏块。
- `-E` 指定超级块。
- `-f` 即使文件系统是干净的强制检查。
- `-G` 获取最后检查时间。
- `-L` 列出坏块。
- `-N` 不执行操作，显示将执行的操作。
- `-P` 显示进度条。
- `-r` 重放检查。
- `-s` 只检查符号。
- `-t` 指定文件系统类型。
- `-v` 详细输出。
- `-w` 不写入错误。
- `-y` 对所有提示回答是。

## 示例 1
```
e2fsck /dev/hda
```
检查第一个 IDE 分区。

## 示例 2
```
e2fsck -f /dev/hda
```
强制检查第一个 IDE 分区。

# edquota

编辑配额。

## 语法概要
```
edquota [-ug] [user or group]
```

## 简述
`edquota` 程序允许编辑配额。

## 常用选项
- `-u` 用户。
- `-g` 。

## 示例 1
```
edquota
```
列出所有配额。

## 示例 2
```
edquota john
```
编辑 `john` 的配额。

# export

设置变量。

## 语法概要
```
export [name=value] name...]
```

## 简述
`export` 允许设置变量。

## 示例 1
```
export PATH=/home/usr
```
设置路径为 `/home/usr`。

## 示例 2
```
export EDITOR=vi
```
设置编辑器为 `vi`。

# fsck

检查并修复文件系统。

## 语法概要
```
fsck [-ABCDfGLPrstvyw] [-block] device
```

## 简述
