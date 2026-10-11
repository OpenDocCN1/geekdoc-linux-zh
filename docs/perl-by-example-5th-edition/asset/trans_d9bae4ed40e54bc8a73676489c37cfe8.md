

## 说明（续）

- 4. 文件以追加模式打开。
- 5. `flock` 函数对文件加排他锁。
- 6. 数据被追加到文件中。
- 7. 数据追加完成后，文件解锁，以便其他人可以访问。

### 10.2.12 seek 和 tell 函数

**seek 函数。** `seek` 允许你随机访问文件。`seek` 函数与 C 语言中的标准 I/O 函数 `fseek` 相同。它允许你在不关闭并重新打开文件的情况下，移动到文件中的某个字节（而非行）位置。如果成功，`seek` 函数返回 1，否则返回 0。

# 格式

```
seek(FILEHANDLE, BYTEOFFSET, FILEPOSITION);
```

`seek` 函数设置文件中的位置，其中第一个字节的索引为 0。位置定义如下：

- 0 = 文件开头
- 1 = 文件当前位置
- 2 = 文件末尾

偏移量（offset）是相对于文件位置的字节数。正偏移量使位置在文件中向前移动；对于位置 1 或 2，负偏移量使位置在文件中向后移动。

`od` 命令可以让你查看文件中字符的存储方式。此文件是在 Win32 平台上创建的；在 UNIX 系统中，换行符/新行是单个字符，\n。

```
$ od -c db
0000000000    S   t       e       v       e       e       B   l   e   e   n   h   e   i   m   /r \n
0000000020    B       e       t       t   y       z   \r \n   B   o   o   o   p   \r   \n   L   o   x   r   i
0000000040    G       o   r   t   z   \r \n   S   i   r   L   a   n   c
0000000060    e   l   \n   J   o   /r \n   N   o   r   m   a   c   h   C   o   r   d
0000000100   \r   \n   J   o   n   D   e   E   L   o   a   c   h   \r   \n   K
0000000120    a   r   e   n       E   v   i   c   h   \r   \n
0000000134
```

### 示例 10.24

```
(文本文件：db)
Steve Blenheim
Betty Boop
Lori Gartz
Sir Lancelot
Norma Cord
Jon DeLoach
Karen Evich
--- --- --- --- --- --- --- --- ---

(脚本)
use warnings;
# 使用 seek 函数的示例
open(my $fh, "<", "db") or die "Can't open: $!\n";
while(<$line=<$fh>) { # 循环遍历整个文件
    if ($line =~ /Lori/) { print "--$line--\n";}
}
seek($fh, 0, 0); # 从文件开头开始
while(<$fh>) {
    print if /Steve/;
}
close $fh;

(输出)
--Lori Gartz--
Steve Blenheim
```

# 说明

- db 文件被赋值给文件句柄 $fh 并以只读模式打开。
- 在循环遍历文件时，文件的每一行依次被赋值给标量 $line。
- 如果 $line 以 Lori 开头，则执行 print 语句。
- `seek` 函数使文件指针定位到文件顶部（位置 0），并从字节 0（第一个字符）开始读取。如果你希望在不使用 `seek` 的情况下回到文件顶部，必须首先使用 `close` 函数显式关闭文件句柄。
- 从文件顶部开始，进入循环。从文件句柄读取第一行并赋值给默认文件持有者 `$_`。
- 如果在变量（原文此处为 $，推测应为 $_）中找到模式 Steve，则打印该行。

### 示例 10.25

(文本文件：db)

```
Steve Blenheim
Betty Boop
Lori Gartz
Sir Lancelot
Norma Cord
Jon DeLoach
Karen Evich
```

```
(脚本)

use warnings;
1 open($fh, "<", "db") or die "Can't open datebook: $!\n";
2 while(<$fh>){
3 last if /Norma/; # 这是最后一行被处理的行
 # 
 }
4 seek($fh,0,1) or die; # 从当前位置进行 seek
5 $line=<$fh>; # 这是读取重新开始的地方
6 print "$line";
7 close $fh;

(输出)

Jon DeLoach
```

# 说明

- 1 通过文件句柄 $fh 以只读模式打开 db 文件。
- 2 进入 while 循环。从文件读取一行并赋值给 $_。
- 3 当读取到包含模式 Norma 的行时，`last` 函数导致退出循环。
- 4 `seek` 函数将文件指针重新定位到字节位置 0，即下一次读取操作原本将执行的位置，也就是位置 1；换句话说，就是 Norma 行之后的那一行。字节位置可以是负值或正值。
- 5 从 db 文件读取一行并赋值给标量 $line。读取的行是 `last` 函数导致循环退出后本应紧接着读取的那一行。
- 6 打印 $line 的值。

### 示例 10.26

```
(脚本):

use warnings;

1 open(my $fh, "<", "db") or die "Can't open datebook: $!\n";

2 seek($fh,-13,2) or die;

3 while(<$fh>){

4 print;

}

close $fh;

(输出):

Karen Evich
```

# 说明

- 1 通过文件句柄 $fh 以只读模式打开 db 文件。
- 2 `seek` 函数从文件末尾（位置 2）开始，向后回退 13 个字节。虽然不可见，但换行符 (\n) 在 Windows 系统中表示为行末尾的最后两个字节。
- 3 进入 while 循环，依次从文件句柄 $fh 读取每一行。
- 4 打印每一行。通过从文件末尾向后回退 13 个字符，打印出了 Karen Evich。请注意 `od -c` 命令的输出，并从文件末尾向前数 13 个字符。

```
0000000000 S t e v e B l e n h e i m \ r \ n
0000000020 B e t t y B o o p \ r \ n L o r i
0000000040 G o r t z \ r \ n S i r L a n
0000000060 c e l o t \ n J o n D e L o a c h \ r \ n K
0000000100 \ r \ n J o n D e L o a c h \ r \ n K
0000000120 a r e n E v i c h \ r \ n
0000000134
```

**tell 函数。** `tell` 函数返回文件中的当前字节位置，并与 `seek` 函数配合使用，以移动到文件中的该位置。如果省略 FILEHANDLE，`tell` 返回最后读取的文件位置。

# 格式

```
tell (FILEHANDLE);
tell;
```

# 说明

- 1. 变量 $fh 被赋值给 db 文件句柄并以只读模式打开。
- 2. 在循环遍历文件时，文件的每一行依次被赋值给标量 $line。
- 3. 如果标量 $line 包含正则表达式 Lori，则进入 if 代码块。
- 4. 调用 `tell` 函数，返回文件中的当前字节位置（从字节 0 开始）。这代表在包含 Lori 的行被处理后，刚刚读取的行中第一个字符的位置。
- 5. 字节值存储在 $currentpos 中，并予以打印。字节位置 40 代表 Sir Lancelot 行开始的位置。

# 说明（续）

- 6. 打印包含正则表达式 Lori 的行。
- 7. `seek` 函数将 $fh 的文件指针定位在字节偏移处，即 $currentpos，也就是从文件开头起 +40 字节处。如果没有 `seek`，无法直接跳到字节 40；唯一的选项是从文件开头重新开始。
- 8. 从偏移 40 开始读取的行被读入并存储在数组 @lines 中。
- 9. 打印数组，从偏移 40 开始。

### 10.2.13 读写模式打开

下一个示例中使用两个文件：一个名为 visitor.txt 的文本文件，其唯一文本初始值为 1；以及 countem.pl，一个用于跟踪运行该脚本的用户数量的脚本。

visitor_count 文件是一个 Perl 脚本，每次执行该脚本时都会将 visitor.txt 文件的值加 1。

表 10.2 读写操作

| 符号 | 打开模式 |
|--------|----------|
| +<     | 先读后写。 |
| +>     | 先写后读（> 会覆盖你的文件）。 |
| +>>    | 先追加后读。 |

### 示例 10.28

(文本文件，visitor.txt)

```
1
```

(脚本)

```
use warnings;
# 脚本名：countem.pl
# 先以读模式打开 visitor.count，然后以写模式打开
1  open(my $fh, "+<", "visitor.txt") ||
   die "Can't open visitor.txt: $!\n";
2  $count=<$fh>;                # 读入数字，并回到文件顶部
3  print "You are visitor number $count.";
4  $count++;
5  seek($fh, 0,0) || die;       #  seek 回文件顶部
6  print $fh $count;             # 将新数字写入文件
7  close $fh;
```

