
#DV.C0P_DSL;$&88(~$U:6$J9T7Z+VAO;6$4Q95QLZG;64Z+M5S

"+#B]B:6X&Q8+W="0!C

`11` `root::X:0:1:Super-User:/:/usr/bin/csh`

`daemon::X:2:1:/:/`

`bin::X:2:2:/usr/bin/:/`

`ysb:X:3:3:/:/`

`admx:4:4:Admin:/var/adm:`

`1p;x:7:1:Line Printer Admin:/usr/spool/lp:`

`smt:p:x:0:0:Mail Daemon User:/`

`uucp:x:5:5:uucp:/usr/lib/uucp`

`news:x:9:9:News Admin:/usr/spool/news:/usr/lib/uucp`

`listen:x:37:4:Network Admin:/usr/net/ nis:`

`nobody:x:60001:60001:Nobody:/:`

`noaccess:x:60002:60002:No Access User:/:`

`nobody1:x:65534:65534:SunOS 4.x Nobody:/`

`#lIie:x:9496:40:Ellie Quigley:/home/ellie:/usr/bin/csh`

```
```

## 解释

1. 打开本地 `passwd` 文件以进行读取。
2. 打开另一个名为 `codedpw` 的文件以进行写入。
3. 文件句柄的每一行被读入 `$_`，直到文件末尾。
4. `pack` 函数对行 (`$_`) 进行编码，并将编码后的行赋值给标量 `$uline`。打印编码后的字符串。`unpack` 函数将编码的字符串转换回其原始形式，并将其赋值给 `@decodeline`。
5. 解码后的字符串发送到文件句柄。
6. 包含解码文本的文件被打开以进行读取。
7. 每一行解码文本被打印。
8. 解码后的文件被打开以进行读取。
10. 从文件句柄读取文件的每一行并存储在 `$_` 中。`unpack` 函数将编码的字符串转换回其原始形式，并将其赋值给 `@decodeline`。
11. 打印解码后的行。

## 示例 16.27

(脚本)

```perl
use warnings;

1 @ints=pack("i3", 5,-10,15); # 打包成二进制结构

2 open(my $bin, ">", "binary") || die;

3 print $bin $ints;

4 seek($bin, 0,0) || die;

while(<$bin>) {
5 ($n1,$n2,$n3)=unpack("i3", $_);
6 print "$n1 $n2 $n3\n";
}
```

(输出)

```
6  5 -10 15
```

## 解释

1. 三个整数 5、-10 和 15 被打包成三个有符号整数。返回的值是一个二进制结构，赋值给 `$ints`。
2. `BINARY` 文件句柄被打开以进行写入。
3. 打包后的整数被发送到文件。该文件是二进制的，作为文本完全不可读。要读取它，必须将其转换回 ASCII 字符串。这通过 `unpack` 完成。
4. `seek` 函数将文件指针放回文件顶部的字节位置 0。
5. 我们从文件中一次读取一行。每一行存储在 `$_` 中，被解包并返回到其原始值列表。
6. 打印原始列表值。

## 示例 16.28

(脚本)

```perl
use warnings;

my $str="0x123456789ABCDE ellice...";

1 print "$str\n";

my $bytes=unpack("H*",$str); # 十六进制字符串（常规顺序）

2 print "$bytes\n";

my $str2 = pack("H*", $bytes);

3 print "$str2\n";

$bytes = unpack("h*",$str); # 十六进制字符串（反向顺序）

4 print "$bytes\n";

my $str1 = pack("h*", $bytes);

5 print "$str1\n";
```

(输出)

```
1   0x123456789ABCDE ellice...
2   307831323334353637383941424344540256c6c69652e2e2e
3   0x123456789ABCDE ellice...
4   0387132334353637383931424344540256c6c69652e2e2e
5   0x123456789ABCDE ellice...
```

## 解释

1. 字符串包含一个十六进制数和一些文本。
2. `h` 和 `H` 字段打包一个由许多半字节（4 位组，可表示为十六进制数字，0..9..F）长的字符串。输入字段的每个字节生成结果中的 4 位。星号 (*) 代表字符串中的所有字符。变量 `$bytes` 由常规十六进制顺序的十六进制字符串组成，其中原始字符串中的每个字符由两个十六进制数表示。（例如，*ellice* 表示为 65 63 6c 6c 69 65，三个点表示为 2e 2e 2e。关于此的进一步讨论，请参见 <http://stackoverflow.com/questions/3857499/when-would-you-use-unpackh-or-packh>)
3. `H` * 字段是将字节通常转换为十六进制（高半字节优先）的方式。
4. 十六进制字符串转换回字节。

## 16.2 进程

你的 Perl 脚本是驻留在磁盘上的程序。当程序被放入内存并开始执行时，它被称为一个**进程**。每个进程都有许多从其父进程，即**调用进程**继承的属性。每个 Perl 都有许多函数，允许你检索关于进程的信息。在检查这些函数之前，关于进程的一些简短讨论可能有助于你理解（或回忆）Perl 某些系统调用的目的。

### 16.2.1 UNIX 进程

每个进程都有一个唯一的进程 ID，即一个称为**pid** 的正整数。除了进程 0（交换器）之外，每个进程都有一个**父进程**。第一个进程，*init*（pid 1），是所有未来进程的祖先，称为**后代**，或更常见的，**子**进程。

在图 16.5 中，Perl 进程是 UNIX shell（*sh*）的后代。第一个进程是 *pid* 1，称为 *init*。*init* 进程生成 *getty*，*getty* 执行 *login*，*login* 执行 *sh*（shell 程序）。从 shell 程序生成 Perl 进程；也就是说，shell 是 Perl 的父进程。

![](img/8556abcb353c0991f12099420ec28735_659_0.png)

每个进程还属于一个**进程组**，这是一个用于作业控制和信号处理的一个或多个进程的集合。每个进程组也有一个唯一的 *pid* 和一个进程组长。当你登录时，进程组长可能是你的登录 shell。从你的 shell 创建的任何都将成为这个进程组的成员。进程组长打开的终端被称为**控制终端**，其生成的任何进程都继承它。发送到该进程的任何信号都会发送到组中的所有进程。这就是为什么当你按下 <CTRL>+C 时，你正在运行的进程及其任何子进程都会终止。Perl 提供函数来获取进程组 ID 并设置进程组。

当创建进程时，它被分配四个数字，表明谁拥有该进程。它们是真实和有效用户 ID，以及真实和有效组 ID。用户 ID，称为 *real uid*，是一个与你的登录名关联的正整数。real uid 是 `/etc/passwd` 文件中的第三个字段。当你登录时，创建的第一个进程称为 *login shell*，并被分配用户 ID。从 shell 生成的任何进程也继承这个 *uid*。以 *uid* 为 0 运行的任何进程被称为 **root** 或 **superuser** 进程，具有特殊权限。

还有一个组 ID 数字，称为 *real gid*，它将组与你的登录名关联。默认 *gid* 是 *password* 文件中的第四个字段，并且也被任何子进程继承。系统管理员可以通过在 `/etc/group` 文件中分配条目，允许用户成为其他组的成员。

以下是来自 *passwd* 文件的一个条目，说明了 *uid* 和 *gid* 值的存储方式（字段用冒号分隔）。

## 示例 16.29

`(/etc/passwd` 中的条目)

```
john:aYdI7I8sJBM9Gg:9495:41:John Doe:/home/dolphin:/john:/bin/ksh
```
