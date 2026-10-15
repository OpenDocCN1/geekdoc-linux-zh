

script, 但在更异构的环境中也可能有用。清单 2.16 显示了在 Solaris 系统上的输出。

## LISTING 2.16 Output of df_check.sh

```
Operating system: SunOS 5.9 Generic_112233-11
-----------------------------
/ : 73%
/var : 79%
```

此脚本可作为监控系统其他部分的模板，因为它可以轻松扩展。如果您决定使用 cron 机制每天运行一次（有关更多信息，请参阅本章稍后的第 2.4.2 节“cron 机制”），则文件系统的状态，即可用空间，始终可用。

## 2.3 PERL SCRIPTS

Perl 是“Practical Extraction and Reporting Language”的缩写。如今它包含在大多数 *NIX 发行版中。其中一些实际上依赖于 Perl 的存在来处理管理任务。Perl 最初是为了提供一种高效地提取和格式化较大文本或日志文件中找到的信息的方法而创建的。无论其起源如何，Perl 开始演变为一种功能齐全的编程语言；甚至支持面向对象的编程技术。

Perl 的一个独特之处在于其简单性；它允许您以无与伦比的轻松构建方便的工具。与其他脚本甚至编程语言相比，Perl 感觉不同。Perl 的创建方式允许您以简单的方式完成简单任务，同时不会阻止您用它来处理更复杂的任务。Perl 中最重要的说法是：程序如果完成了它的工作，就是一个好程序。使用 Perl 只需要对另一种编程语言有初步的经验。如果您已经完成了 shell 脚本示例的学习，您应该已经准备好了。如果您是一位经验丰富的程序员，并且急于学习 Perl，您会发现其中有很多熟悉的功能。

### 2.3.1 Creating a Perl Script

下面的 Perl 脚本将输出所有用户及其各自 UID 的列表。首先在您的项目层次结构中创建另一个子目录；示例中使用的目录称为 ulist1。在此目录中，创建 RCS 目录和一个名为 ulist1.pl 的文件，根据清单 2.17 中的描述进行操作。

## LISTING 2.17 Creating the Structure for the Perl Example

```
erikk@unixhost:~> pwd
/export/home/users/erikk/work
erikk@unixhost:~> mkdir ulist1
erikk@unixhost:~> mkdir ulist1/RCS
erikk@unixhost:~> cd ulist1
erikk@unixhost:~> ls -l
total 2
drwxr-xr-x 2 erikk staff 512 Aug 9 16:56 RCS
erikk@unixhost:~> touch ulist1.pl
erikk@unixhost:~> chmod u+x ulist1.pl
erikk@unixhost:~> ls -l
total 2
drwxr-xr-x 2 erikk staff 512 Aug 9 16:56 RCS
-rwxr--r-- 1 erikk staff 0 Aug 9 16:57 ulist1.pl
erikk@unixhost:~>
```

到目前为止，该过程与 shell 示例相同。然而，在这种情况下，您必须确定 Perl 解释器的路径。要查找 $PATH 中程序的确切位置，您可以使用 which 命令。which perl 应该返回类似 /usr/bin/perl 的内容。清单 2.18 中显示的内容需要插入到文件中。

## LISTING 2.18 First Version of the Perl Example

```
#!/usr/bin/perl
# $Id$
#
###################################################
#
#    file:        ulist1.pl
#
#    purpose:     lists all users
#                 and their respective IDs
#
#
#    author:      Erik Keller
#
###################################################
```

```
# Variables

# list passwd first
# open the file
open(MY_PWFILE, "/etc/passwd") or die "$0: couldn’t open file: $!";

# loop through the file and print the records
while(<MY_PWFILE>)
{
    print $_;
}

# close the file
close(MY_PWFILE);

# EOF
```

如果您从未见过 Perl 程序，以下列表包含正在发生的事情的简短说明。

- open(MY_PWFILE, "/etc/passwd") 指示程序打开文件 /etc/passwd 并将其附加到句柄 MY_PWFILE。句柄指向计算机内存中文件存储的位置。程序稍后将使用它来访问文件。行的延续，or die "$0: couldn’t open file: $!";，告诉程序在出现错误时停止执行并打印出以下信息：$0 包含程序的名称，$! 为错误描述。

- 指令 <MY_PWFILE> 是 Perl 如何简化事物的有力证明。它意味着，“只要您还没有到达句柄指向的文件末尾。”因此 while(<MY_PWFILE>) 逐行遍历文件，直到到达文件末尾并执行大括号 {} 之间的命令。

- print $_; 输出当前记录而不更改它。变量 $_ 会自动创建并包含当前记录。

- close(MY_PWFILE); 做它所说的事情——关闭句柄及其指向的文件。请确保始终在使用的程序中关闭打开的文件；依赖操作系统来执行此操作可能会损坏文件或产生难以找到的错误条件。

