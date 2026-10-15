
一旦在脚本文件中定义了变量 `card1` 到 `card7`，就会生成 `run_mrolsq.scr` 文件，该文件包含适当的符号链接，用于将数据文件与 FORTRAN 单元号关联。当然，数据文件与 FORTRAN 单元号关联的方式取决于 UNIX 版本和 FORTRAN 编译器的版本。程序 `prolssq.exe` 然后通过 `time` 命令执行，并提供计时信息；任何程序输出都会发送到 `stdout`（即终端）。

第二个示例 `menu_script` 演示了如何使用菜单界面访问由多个文件组成的简单数据库。数据库中的每个文件在每个记录的末尾都有一个名为 `recognition code`（识别码）的字段，它是文件名的一部分。每个接受识别码的菜单选项都使用该代码指向一个或多个文件。

### UNIX

```bash
% cat menu_script
#!/bin/csh -f
#
# 菜单脚本：简单的菜单驱动数据库查询
#
#
#
# 保留原始目录指针并移动到数据库目录
pushd /datal/pdb
# 显示横幅
echo " Brookhaven Database Utility Program "`date` "
# (反引号) 会立即执行 date 命令
# 返回脚本被调用的时间
onintr menu
# 发生中断时返回菜单
menu:
echo .... 
# 显示选项菜单
echo " The following options are available:"
echo " "
echo " I list identity of the "database""
echo " D list a directory of the database contents"
echo " SD search the directory listing for keywords"
echo " SF search full database for keywords"
echo " T list a database entry at the terminal"
echo " C copy database entry with possible format conversion"
echo " Q quit the "database""
```

![](img/e259ba2750941fa3d146eda78c65e89d_345_0.png)

## 10.11 总结

```csh
echo "*"
echo -n "Option> # 用户在此输入选项
set command = $<
goto command # 分支到选项
#
i identity 选项---描述最近的数据库更新
#
i: # 考虑大写和
i: # 以及小写的用户响应
echo "This database is the April 1986 release"
#
goto menu # 返回菜单

#
directory 选项---显示汇总所有数据库条目的的文件
#
D:
d:
echo " Type <ctrl>-C to return to menu"
echo " 使用每个条目末尾的 4 位识别码"
echo " 通过随后的菜单选项处理条目"
# 目录文件包含目录中每个文件的头信息
# 并使用命令 head -4 *.dat >> directory 创建的
acat directory
goto menu
#
# 使用 grep 搜索目录中的关键词——返回的记录
# 包含从 head 命令原始提取处的文件名
#
SD:
d:
echo " *keyword(s).*"
set string = $\$
grep -i $string directory # 忽略大小写或字符串 (i)
goto menu
#
# 搜索所有文件中的字符串 N。注意：这比搜索
# 文件目录慢得多，只有在搜索目录选项未能返回
# 有用信息后才应使用
#
sf:
SF:
echo -n "Keyword(s):-"
set string = $\$
grep -i $string *.dat # 搜索所有数据文件
goto menu
```

```csh
# 列出数据库条目
#
T:
t:
echo -n "Enter recognition code:-"
# 从搜索获取代码
option
set entry = $<
cat 'entry'
goto menu
#
# 拷贝条目---调用程序 format.exe，该程序将
# 数据库条目格式化为适合编辑的形式。用户将被
# 提示输出文件，并为输入文件（数据库条目）和
# 输出文件（用户文件）建立适当的符号链接
#
C-
c:
echo -n "Enter recognition code:-"
set temp_file = $<
set filein = '/datal/pdb/'$temp_file
echo -n "Filename for output:"
set fileout = $<
ln -s $filein fort
ln -s $fileout fort.exe
rm fort.*
# 符号链接
goto menu
#
# 退出---从菜单优雅退出脚本
Q:
q:
echo "Exit database utility program"
popd
# 返回到原始目录
exit
```

`menu_script` 向用户展示了一个选项菜单。用户的响应引导控制流。脚本使用 `pushd` 和 `popd` 保留工作目录以便后续恢复。使用 `grep` 搜索用户指定字符串的文件，使用 `cat` 打印条目，或执行程序执行用户指定的格式化。在下一个示例中，它将定位作为参数提供的任何命令的路径，前提该路径在用户的 `path` 列表中。`which` 命令用于查找系统程序或用户所在的目录。此示例直接源自 BSD 版本的 UNIX，并为了清晰起见增加了额外的注释。

![](img/e259ba2750941fa3d146eda78c65e89d_347_0.png)注：此处原文意为“此示例直接源自 BSD 版本的 UNIX”，

## 10.1 总结

```perl
# Check parameters and prompt for Perl expression. 
#
die("usage: $0 files...\n") if (@ARGV <= 0); 
print(STDERR " Enter Perl expression,\n or press [ENTER] for help > "); 
$op = <STDIN>; 
chomp ($op); 
if ($op eq "") 
{ 
print STDERR <<'HELP'
Enter a Perl expression that will transform the contents of the $_ 
variable from the names you have to to the names you want. You will 
be shown a list of all changes *before* they are made allowing 
you to change your mind before committing.
Examples:
(1) strip extension from all files matching *.bak 
s/\.bak$// 
(2a) append ".bak" to all specified files 
$_ .= ".bak" 
(2b) as above only using substitution 
s/./.bak/ 
(3) change all *foo*, *Foo*, and *FOO* files to *_bar_* 
s/foo/_bar_/i 
(4) translate uppercase names to lower case 
tr/A-Z/a-z/ 
(5) rename 
input *.dat 
output *.dat 
s/input (.*).dat/output_$1.dat/
HELP
exit; 
} # if ($op eq "") 
# 
# For each file-spec, check to see if it exists and then determine 
# and remember the resulting new name. 
# 
```

![](img/e259ba2750941fa3d146eda78c65e89d_350_0.png)
