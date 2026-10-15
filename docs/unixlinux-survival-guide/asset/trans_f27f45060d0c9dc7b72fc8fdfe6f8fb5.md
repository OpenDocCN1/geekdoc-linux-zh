

如果执行该程序，输出应显示系统中 /etc/passwd 中包含的行（本示例中列出 2.19 所示的输出已缩短）。

## LISTING 2.19 Output of the Perl Script

```
erikk@unixhost:> ./ulist1.pl
root:x:0:1:Super-User::/sbin/sh
daemon:x:1:1:::
bin:x:2:2::/usr/bin:
sys:x:3:3::
adm:x:4:4:Admin:/var/adm:
lp:x:71:8:Line Printer Admin:/usr/spool/lp:
uucp:x:5:5:uucp Admin:/usr/lib/uucp:
nuucp:x:9:9:uucp Admin:/var/spool/uucppublic:/usr/lib/uucp/uucico
smmsp:x:25:25:SendMail Message Submission Program::
listen:x:37:4:Network Admin:/usr/net/nls:
nobody:x:60001:60001:Nobody::
noaccess:x:60002:60002:No Access User::
nobody4:x:65534:65534:SunOS 4.x Nobody::
erikk:x:101:10::/export/home/users/erikk:/bin/sh
```

列出 2.19 中的结果显然缺乏清晰度。它包含了一些对于程序目的而言不需要的信息，例如用户登录后将启动哪个 shell。冒号分隔各字段，而你所寻找的信息位于字段 1 和字段 3。为访问这些字段的内容，Perl 提供了函数 split。它需要两个参数：字段分隔符，在本例中为 :，以及要拆分的变量名 $_，如列出 2.20 所示。

## LISTING 2.20 Splitting the Records into Fields

```
#!/usr/bin/perl
# $Id$
#
################################################################
#
#   file:      ulist1.pl
#
#   purpose:   lists all users
#              and their respective IDs
#
#   author:    Erik Keller
#
######################################
# Variables

# list passwd first
# open the file
open(MY_PWFILE, "/etc/passwd") or die "$0: couldn't open file: $!";

# loop through the file and print the records
while(<MY_PWFILE>)
{
    chop;
    @my_records = split(":",$_);
    print "@my_records\n";
}

# close the file
close(MY_PWFILE);

# EOF
```

```
erikk@unixhost:> ./ulist1.pl
root x 0 1 Super-User /sbin/sh
daemon x 1 1 /
bin x 2 2 /usr/bin
sys x 3 3 /
adm x 4 4 Admin /var/adm
lp x 71 8 Line Printer Admin /usr/spool/lp
uucp x 5 5 uucp Admin /usr/lib/uucp
nuucp x 9 9 uucp Admin /var/spool/uucppublic /usr/lib/uucp/uucico
smmsp x 25 25 SendMail Message Submission Program /
listen x 37 4 Network Admin /usr/net/nls
nobody x 60001 60001 Nobody /
noaccess x 60002 60002 No Access User /
nobody4 x 65534 65534 SunOS 4.x Nobody /
erikk x 101 10 /export/home/users/erikk /bin/sh
```

函数 chop 删除表示行结束的字符。如果不带参数调用，chop 会作用于 $_ 的内容。即使现在还不那么明显，split 实际上已经提取了字段中包含的信息。要读取此信息，使用以下结构：$my_records[0] 访问

第一个字段的内容。数组字段的编号从 0 开始，就像大多数其他编程语言一样。这意味着第一个字段在地址 0，第二个字段在地址 1，以此类推。因此，你所寻找的信息位于字段 0 和字段 2。列出 2.21 展示了脚本及其输出。

## LISTING 2.21 Perl Script to Extract Usernames and IDs

```
#!/usr/bin/perl
# $Id: ulist1.pl,v 1.1 2004/08/10 10:57:03 erikk Exp erikk $
#
#####################################################################
#
#    file:      ulist1.pl
#
#    purpose:   lists all users
#               and their respective IDs
#
#
#    author:    Erik Keller
#
#####################################################################

# Variables

# list passwd first
# open the file
open(MY_PWFILE, "/etc/passwd") or die
    "$0: couldn't open file: $!";

# loop through the file and print the records
while(<MY_PWFILE>)
{
    chop;
    @my_records = split(":",$_);
    print "$my_records[0]\t$my_records[2]\n";
}

# close the file
close(MY_PWFILE);

# EOF

erikk@unixhost:> ./ulist1.pl
```

```
root      0
daemon    1
bin       2
sys       3
adm       4
lp        71
uucp      5
nuucp     9
smmsp     25
listen    37
nobody    60001
noaccess  60002
nobody4   65534
erikk     101
```

脚本运行正常。要在任何能够导入逗号分隔值（CSV）的程序中使用生成的列表，只需将制表符字符（\t）切换为逗号即可。输出的一种用途可能是将用户信息传输到数据库系统中，例如检查所用名称的一致性：

## 2.3.2 Using the Getopt Perl Module

一旦你的 Perl 程序开始变得复杂，你会发现一个问题浮现出来：如何处理命令行上给出的参数？流通中的相当一部分 Perl 程序使用 @ARGV 数组来评估提供的参数。这种方法并无问题，但创建这些脚本的人让自己的生活比必要的更复杂一些。Perl 标准库是每个 Perl 安装的一部分，其中包含大量可用于扩展脚本功能或以标准方式处理某些更一般性问题的函数。你可以找到现成的函数来处理参数等。

作者在创建第一个 Perl 程序时，有幸结识了几位经验丰富的 Perl 程序员。他们花时间查看了创建的代码，并听取了作者关于某些事情在 Perl 中实现起来有多困难的抱怨。他们对作者的许多程序所做的评论之一是：“但那不是标准库的一部分吗？” 作者实际上创建了复杂的函数来实现某些结果，却不知道如果正确提问，Perl 会提供解决方案。

其中一个节省时间的方法是包 Getopt。利用它可以使处理命令行开关如 -p 或评估参数如 -d /export/home 几乎成为自动过程。列出 2.22 显示了该包的使用。
