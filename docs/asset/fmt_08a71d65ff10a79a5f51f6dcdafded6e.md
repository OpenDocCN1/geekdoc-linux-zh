
`insert.bash`, `.ksh`, `.pl`

`print.bash`, `.ksh`, `.pl`

更多信息：`'man sed'`, `'man s2p'`; `perdoc s2p`

示例：查看：

`sed.bash`, `sed.ksh`, `sed.pl`

`delete.bash`, `.ksh`, `.pl`

`insert.bash`, `.ksh`, `.pl`

`print.bash`, `.ksh`, `.pl`

`substitute.bash`, `.ksh`, `.pl`

### SHELL 命令：`:set`

对应的 Perl 命令：无。

用途：

## 第 3 部分，Shell 命令，第 56 页

1. 声明数组：`set -a MyArray` (ksh)

参见 `array.ksh`, `sort_array.ksh`

2. 解析记录：

- 参见 `contacts.*sh`
- 参见 `record_array.sh`, `count_words.*sh`
- 另请参见，`split_record_into_pieces_using_delimiters.*sh`

3. 调试：

- `set +X` `switches.*sh`, `testing_and_debugging_tips.txt`

更多信息：`'man set'`

### BASH 或 KSH 命令：`shift`

对应的 Perl 命令：`shift`

用途：从命令行获取一个参数。

更多信息：`'man shift'`, `'perldoc find shift'`

示例请参阅：`shift.bash`, `.ksh`, `.pl`

### BASH 或 KSH 命令：`sleep 5` # 睡眠 5 秒。

对应的 Perl 命令：`sleep(5);` # 睡眠 5 秒。

用途：按用户指定的秒数进行睡眠（无任何操作）。

更多信息：`'man sleep'`, `'perldoc find sleep'`

示例请参阅：`contacts.bash`, `contacts.ksh`, `contacts.pl`

### BASH 或 KSH 命令：`sort`

对应的 Perl 命令：`sort`

用途：排序

更多信息：`'man sort'`, `'perldoc find sort'`, `'perldoc sort'`

示例请参阅：`sort.bash`, `sort.ksh`, `sort.pl`

### BASH 或 KSH 命令：`spell`

对应的 Perl 命令：`Search::Dict`

用途：识别拼写错误。

更多信息：`'man spell'`, `'perldoc Search::Dict`

### AWK 命令：`substr` (子串)

对应的 Perl 命令：

`'substr'` (子串) 既是一个字符串也是一个 AWK 命令。

`'cut -c'` 的 Perl 等效命令是 `'substr'` (子串)。

`'cut -f'` 的 Perl 等效命令是 `'split'` 命令。

bash 中的 `'cut'` 和 `'substr'` 允许你查看记录的任何部分，然后重新格式化/更改记录就会变得简单。

用途：提取或更改记录或文件中的任意列或多个列。

更多信息：`'man awk'`, `'perldoc find substr'`

示例请参阅：

`cut_AND_substring.bash`, `.pl`

`substitute_and_substitute.bash`, `.ksh`, `.pl`

### BASH 或 KSH 命令：`tail 'filename'` 或 `'tail -10 filename`

对应的 Perl 命令：无，但请参见 `grab_last_10_recs.pl`

用途：显示文件末尾底部的记录。

更多信息：`'man tail'`

示例请参阅：

`grab_last_10.recs.bash`, `.ksh`, `.pl`

### BASH 或 KSH 命令：`tar`

对应的 Perl 命令：无，但请参见 `'tar.pl'`

用途：

1. 归档文件（及目录）。
2. 创建文件（及目录）的备份副本。
3. 将许多文件收集到一个文件中，将该文件 ftp 另一另一台服务器，然后“解压”，这样你就可以访问最初收集的文件。

更多信息：`'man tar'`

示例请参阅：`tar_and_untar.bash`, `.ksh`, `.pl`

命令：`"test"` (文件条件)。

## 第 3 部分，Shell 命令，第 57 页

更多信息：`'man test'`

示例请参阅：

`if_file_exists.bash,.ksh.pl`

`eq_ne_gt_te_le_FLOAT.ksh,.pl`

`eq_ne_gt_te_le_INTEGER.bash,.ksh.pl`

`eq_ne_gt_te_le_STRING.bash,.ksh.pl`

### BASH 或 KSH 命令：`touch`

对应的 Perl 命令：`utime`

用途：1. 创建一个空文件。
2. 修改文件的访问时间。

更多信息：`'man touch'`, `'perldoc -utime'`

示例请参阅：`touch.bash`, `touch.ksh`, `utime.pl`

### BASH 或 KSH 命令：`tr`

对应的 Perl 命令：`tr`

用途：“转换”字符（或删除字符）。

更多信息：`'man tr'`, `'perldoc peril'` (然后对 `'/tr'` 执行 find 操作)。

示例请参阅：`tr.bash`, `tr.ksh`, `tr.pl`

### KSH 命令：`typeset`

注意：

某些 Linux 系统支持 `'typeset'` 命令的许多开关。

bash, ksh 有一个内置命令 `"declare"`，与 `'typeset'` 类似。

bash, ksh 以及 Perl：可以使用 `'printf'` 和 `'tr'` 代替 `'typeset'` 来格式化输出。`typeset.ksh` 中提供了 typeset 的示例。

ksh: `typeset -u` 将小写转换为大写：PerL 等效命令：`uc`

参见：`change_lower_to_UPPER_CASE.bash,.ksh.pl`

ksh: `typeset -i` 将大写转换为大写：PerL 等效命令：`lc`

参见：`change_UPPER_CASE_lower.bash,.ksh.pl`

ksh: `typeset-counter=` # i 表示整数 [整数字]

参见：`math.bash`, `ksh`, `pl` 以及 `eq_ne_gt_te_le_INTEGER.bash`

ksh: `"float" -pi 3.14` # r 是只读（常量）

ksh: `"float"` 是 `"typeset -E"` 的别名；参见：`math.ksh`

ksh: `typeset -E` 浮点数；参见：`math.ksh`

ksh: `typeset -L` 左对齐：参见：`math.ksh`

ksh: `typeset -R` 右对齐：参见：`math.ksh`

ksh: `typeset -C` 居中对：参见：`math.ksh`

ksh: `typeset -A` 关联数组：参见：`math.ksh`

ksh: `typeset -a` 索引数组：参见：`math.ksh`

ksh: `typeset -A` 关联数组：参见：`math.ksh`

ksh: `typeset -i` 整数数组：参见：`math.ksh`

ksh: `typeset -l` 逻辑数组：参见：`math.ksh`

ksh: `typeset -n` 符号数组：参见：`math.ksh`

ksh: `typeset -s` 字符串数组：参见：`math.ksh`

ksh: `typeset -t` 时间数组：参见：`math.ksh`

ksh: `typeset -u` 无符号数组：参见：`math.ksh`

ksh: `typeset -v` 变量数组：参见：`math.ksh`

ksh: `typeset -w` 路径数组：参见：`math.ksh`

ksh: `typeset -x` 导出数组：参见：`math.ksh`

ksh: `typeset -y` 标记数组：参见：`math.ksh`

ksh: `typeset -h` 历史数组：参见：`math.ksh`

ksh: `typeset - j` 索引数组：参见：`math.ksh`

ksh: `typeset -k` 键数组：参见：`math.ksh`

ksh: `typeset -m` 内存数组：参见：`math.ksh`

ksh: `typeset - n` 模式数组：参见：`math.ksh`

ksh: `typeset -p` 进程数组：参见：`math.ksh`

ksh: `typeset -q` 队列数组：参见：`math.ksh`

ksh: `typeset - r` 递归数组：参见：`math.ksh`

ksh: `typeset - s` 状态数组：参见：`math.ksh`

ksh: `typeset - t` 标签数组：参见：`math.ksh`

ksh: `typeset - v` 变量数组：参见：`math.ksh`

ksh: `typeset - w` 权重数组：参见：`math.ksh`

ksh: `typeset - x` 扩展数组：参见：`math.ksh`

ksh: `typeset - y` 坐标数组：参见：`math.ksh`

ksh: `typeset - z` 零数组：参见：`math.ksh`

(修正上述翻译)

ksh: `typeset-counter=` # i 表示整数 [整数字]
