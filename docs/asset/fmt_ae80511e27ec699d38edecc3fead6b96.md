
# Shell 命令对照

## `ksh` 或 `bash`：`kill -9 1234`
```
ksh or bash: kill -9 1234
Perl: kill 9, 1234
```

`Perl`：如果“信号”（例如 `-9`）为负数，它会杀死“进程组”而不是单个进程；因此，你可能**不要**使用负信号！

## KSH 命令
`ksh -n myscript` 或 `ksh -n ./myscript`

## BASH 命令
`bash -n myscript.ksh` `bash -n myscript.ksh`

对应的 `Perl` 命令：`perl -c myscript.pl` `perl -c ./myscript.pl`

更多信息：`'man ksh'`, `'man bash'`

用途：检查脚本的语法（脚本不会被**执行**）。

注意：此命令从命令行执行，而不是在脚本内部执行。

另参见：`switches.bash,.ksh,.pl`

## BASH OR KSH 命令：`ln oldfile new`
硬链接（作者不建议）

`ln oldfile newfile` # 符号链接（推荐）。

对应的 `Perl` 命令：`link(oldfile,newfile);` # 硬链接

`symlink(oldfile,newfile);` # 符号链接

用途：链接2 个文件。

更多信息：`'man ln'`, `'perldoc -f link'`, `'perldoc -f symlink`

注意：`Perl` 的 `'unlink'` 命令等于 UNIX 的 `'rm'` 命令。

## BASH OR KSH 命令：`ls -i myfile`

对应的 `Perl` 命令：`ls`

用途：按 inode 列出文件。

```
($.inode,$perms,$uid,$gid,$dev,$size,$atime,$mtime,$ctime,$bsize,$blks)@nstat($filename);
```

`stat`：列出文件的属性（大小、顺序、最后修改日期等）。

更多信息：

`'man ls'`, `'perldoc -f stat'` 或 `'perldoc -f stat'`

示例查看：`ls_minus_1.ksh`, `ls_minus_1.pl`

## BASH OR KSH 命令：`mail` (or `mailx`)

对应的 `Perl` 命令：`Net::SMTP`

用途：向另一个用户发送邮件。

更多信息：`'man mail'`, `'perldoc Net::SMTP'`

示例查看：`email_warning.bash,.ksh,.pl`

## BASH OR KSH 命令：`man`

对应的 `Perl` 命令：`perldoc`

用途：获取文档。

更多信息：`'man man'`, `'perldoc perldoc'`

示例查看：`man.txt`, `perldoc.txt`

## BASH OR KSH 命令：`mkdir`

对应的 `Perl` 命令：`mkdir`

用途：“创建”（make）目录。

示例查看：

`mkdir.bash,.ksh,.pl`

`change_string_in_all_files.bash`, `ksh`, `and pl`

第 3. Shell 命令，第 54 页

更多信息：`'man mkdir'`, `'perldoc -f mkdir'`

## BASH OR KSH 命令：`more`

对应的 `Perl` 命令：无，但在 `'contacts.pl'` 中执行 `'find'`：

用途：允许用户一次查看输出。

示例查看：`contacts.bash`, `ksh`, `and pl`

更多信息：`'man page'`, `'man less'`

## BASH OR KSH 命令：`mv`

对应的 `Perl` 命令：`'rename'` 或 `File::Copy` 中包含 `'move'` 函数

用途：允许用户移动（或重命名）文件。

更多信息：`'man mv'`, `'perldoc -f rename'`, `'perldoc File::Copy'`

示例查看：`rename.bash`, `.ksh`, `and pl`

## BASH OR KSH 命令：`ping`

对应的 `Perl` 命令：`Net::Ping`

用途：确定服务器是否在线/离机。

更多信息：`'man ping'`, `'perldoc Net::Ping'`

示例查看：`ping.bash`, `.ksh`, `.pl`

示例查看：`check_health.bash`, `.ksh`

## BASH OR KSH 命令：`pipe`

对应的 `Perl` 命令：`'readpipe'` 或 `'IO::Pipe'`

用途：发送数据流到虚拟。

更多信息：`'man IO::Pipe'`, `'perldoc -f readpipe'`

示例查看：`pipe.bash`, `.ksh`, `pipe.pipe`

## KSH 命令：`print`

对应的 `Perl` 命令：`print`

用途：显示字符串或记录。

更多信息：`'man print'`, `'perldoc -f print'`

示例查看：`print.ksh`, `print.pl`

另参见：`sprintf` (`Perl`)。

## BASH OR KSH 命令：`printf`

对应的 `Perl` 命令：`printf`

用途：显示并格式化字符串或记录。

更多信息：`'man printf'`, `'perldoc -f printf'`

示例查看：`printf.bash`, `printf.ksh`, `printf.pl`

## BASH OR KSH 命令：`ps`

对应的 `Perl` 命令：查看 `'ps.pl'` 中的示例。

用途：显示正在运行的进程。

更多信息：`man ps`

示例查看：`ps.bash`, `ps.ksh`, `ps.ps`

## BASH OR KSH 命令：`pwd`

对应的 `Perl` 命令：`cwd`

`use Cwd;` #允许我们确定当前目录

用途：显示工作目录 (`cwd`)。

注意：“工作”目录是你的当前目录。

例如，如果你切换 (`cwd`) 到 `/tmp`，那么你的工作目录就是 `/tmp`。

更多信息：`'man pwd'`, `'perldoc cwd'` (`'perldoc cwd'`)

示例查看：`pwd.bash`, `pwd.ksh`, `cwd.pl`

## BASH OR KSH 命令：`read`

注意 1：`bash`, `ksh` 和 `Perl` 都有 `'read'` 命令；然而，`Perl` 的等价于 `ksh-bash` 命令 `'read'` 不是 `'read'`。

注意 2：如何从用户处获取信息：

# 3. Shell 命令，第 55 页

`bash` and `ksh`：`print -n "What is your name?"; read -r first_name`

`Perl`：`print "What is your name?"; $name=<STDIN>`

对应的 `Perl` 命令：`'open'` 和 `'split'` 可以模拟 `bash-ksh` 命令 `'read'`。

更多信息：`'man read'`, `'perldoc -f split'`

用途：读取文件或从用户处获取信息。

示例查看：`user_input_from.keyboard.bash`, `.ksh`, `.pl`

`read1_field2_of_record.bash`, `.ksh`, `.pl`

## BASH OR KSH 命令：`rm` 示例：`rm /tmp/junk`

对应的 `Perl` 命令：示例：`unlink("/tmp/junk");`

用途：删除文件

更多信息：`'man rm'`, `'perldoc -f unlink'`

## BASH OR KSH 命令：`rmdir`

注意：`'rm mydir'` 更快，但不应由没有经验的用户使用。

对应的 `Perl` 命令：`rmdir`

用途：删除任何目录。

更多信息：`'man rmdir'`; `'perldoc -f rmdir'`

## BASH OR KSH 命令：`script`

对应的 `Perl` 命令：无。

用途：`'script'` 命令捕捉你输入的每一个按键；它还捕捉屏幕上出现的每行输出。

从命令行输入命令：

示例 1：`script my_output_file [回]`

脚本启动，文件是 `my_output_file` <<- 来自系统。

示例 2：`script [回]` # 输出被放入文件 `'typescript'` 中。

要结束 `'script'`，输入 `'exit'`。

`'script'` 对于需要记录在线工作或与任何类型的脚本或程序交互时发生的情况有用。（不幸的是，每次按下退格键或回车键，那些按键也会被记录。许多控制字符（如 ^M）可以使用 `dos2unix` 命令删除：`dos2unix my_output_file`）。

磁盘文件以后可以打印：`lp my_output_file`

在创建期间，我使用了 `'script'` 命令来捕捉 `'contacts'` 脚本的输出。查看 `contacts.bash`, `.ksh`, `.pl`

## BASH OR KSH 命令：`sed`

对应的 `Perl` 命令：无，但 `Perl` 提供了一个名为 `'sed'` 的实用程序将 `sed` 转换为 `Perl`。

用途：`'sed'` 允许你删除、插入、替换等。

注意：我创建了一个名为 `sed.bash` 的脚本以及一个名为 `sed.ksh` 的脚本；由于 `Perl` 中没有 `'sed'` 函数，我创建了执行 `sed` 完成的任务的。

例如：

`substitute.bash`, `.ksh`, `.pl`

`delete.bash`, `.ksh`, `.pl`
