

# 检查 RCS 文件之间的差异

你可以使用 `rcsdiff` 比较 RCS 文件的两个版本，或者将已提交的版本与工作文件进行比较。下面的示例将主分支（trunk）上的最新版本与工作文件 `pi.c` 进行比较——这是两个待比较版本的默认值。比较熟悉的输出来自 `diff`，它由 `rcsdiff` 调用：

```
$ rcsdiff pi.c
=============================================
RCS file: RCS/pi.c,v
retrieving revision 1.3
diff -r1.3 pi.c
136c136
< submm(a,b) /* subtract big b from big number a */
> void submm(a,b) /* subtract big b from big number a */
157c157
< inform(a) /* display the result (given in big number a) */
> void inform(a) /* display the result (given in big number a) */
170c170
< outnum(a) /* print out the big number a */
> void outnum(a) /* print out the big number a */
$
```

你可以使用 `-r` 选项指定要比较的一个或两个版本。接下面的 `rcsdiff` 比较 `pi.c` 的前两个版本：

```
$ rcsdiff -r1.1 -r1.2 pi.c
=============================================
RCS file: RCS/pi.c,v
retrieving revision 1.1
retrieving revision 1.2
diff -r1.1 -r1.2
15c15,19
< * (time to compute pi to 10000 places): <9 cpu hours on PDP-11/44,
> * (time to compute pi to 10000 places): <9 cpu hours on PDP-11/44,
> * 486dx2/66 [Linux 1.2.13]: 126 cpu seconds,
> * 486dx4/100 [Linux 1.2.13]: 92 cpu seconds,
>
>
21c25
---
< #define MAXNUM 100000 /* largest allowable accuracy */
> #define MAXNUM 100000 /* largest allowable accuracy */
$ 
```

如果你只用 `-r` 选项指定了一个版本，`rcsdiff` 将将该指定版本与工作文件进行比较：

```
$ rcsdiff -rl1.2 pi.c
RCS file: RCS/pi.c,v
retrieving revision 1.2
diff -rl1.2 pi.c
80c80
-
< outnum(r); /* display the result */
> inform(r); /* display the result */
153a154,166
}
> inform(a) /* display the result (given in big number a) */
> long a[];
{
  printf("\n\n\n\tPI Calculation\n\n\n");
  printf("\t\t# of words/number\t= %d\n",nwd);
  printf("\t\t# of digits/word\t= %d\n",NDS);
  printf("\t\t# of accurate places\t= %d\n",places);
  printf("\t\tArithmetic base is %d\n",WDSZ);
  printf("\n\n\tPI is:\%d\n\n");
}
> outnum(a);
$ 
```

# ## CVS：并发版本系统 (Concurrent Versions System)

尽管 RCS 易于使用，但作为一种源代码管理系统，它也有一些缺点，包括：

- 项目只能组织为单个文件的集合，而不能作为一个单一的集成单元。例如，如果一个项目很大并涉及多个目录，RCS 要求每个目录都关联一个修订文件。多个修订文件会使得收集特定发布所需的文件变得困难，如果有多个开发者，则很难跟踪每个人的贡献。
- RCS 使用锁定机制来控制对 RCS 文件的访问，这使得两个或更多人无法同时对文件进行更改，即使这些更改涉及文件的不同部分。这种锁定机制对于较规模的版本控制很有用，但往往会阻碍合作大型项目的开发团队的进展。

CVS（并发版本系统—www.cvhome.com）通过将整个文件集合视为单个单元来解决这些问题，使得处理大型项目变得容易，并允许多个用户处理同一个文件。CVS 还为 CVS 系统中的工具提供了价值贵的自文档功能。

# 内置 CVS 帮助

RCS 使用了几个不同的程序，而 CVS 使用单一工具：`cvs`。要显示获取帮助说明，请使用 `--help` 选项：

```
$ cvs --help
Usage: [cvs-options] command [command-options-and-arguments]
where cvs-options are -q, -n, etc.
  (specify --help-options for a list of options)
  where command is add, admin, etc.
  (specify --help-commands for a list of commands)
  or --help-synonyms for a list of command synonyms)
where command-options-and-arguments depend on the specific command
  (specify -ih followed by a command name for command-specific help)
  Specify --help to
```

并发版本系统 (www.cvhome.com) 是一个工具。更多信息请参阅 CVS 主页。

