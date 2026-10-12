
```
$ env --help

Usage: env [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...]
Set each NAME to VALUE in the environment and run COMMAND.

    -i, --ignore-environment  start with an empty environment
    -u, --unset=NAME          remove variable from the environment
    --help    display this help and exit
    --version output version information and exit

A mere - implies -i.  If no COMMAND, print the resulting environment.
Report bugs to <bug-coreutils@gnu.org>.

Here are some sample invocations:

$ env - myprog arg1
                Clear environment, run myprog with arg1
$ env - PATH=/bin:/usr/bin myprog arg1
                Clear environment, add PATH, run program
$ env -u IFS PATH=/bin:/usr/bin myprog arg1
                Unset IFS, add PATH, run program
```

代码以一个标准的 GNU 版权声明和解释性注释开始。为了简洁，我们省略了这两部分。（版权声明在第 C 附录“GNU 通用公共许可证”第 657 页中有讨论。前面显示的 `--help` 输出足以理解程序的工作原理。）在版权声明和注释之后是头文件包含和声明。`N_("string")` 宏调用（第 93 行）用于软件的国际化和本地化，这些主题在第 13 章“国际化和本地化”第 485 页中涵盖。目前，你可以将其视为所包含的字符串常量。

```
80  #include <config.h>
81  #include <stdio.h>
82  #include <getopt.h>
83  #include <sys/types.h>
84  #include <getopt.h>
85
86  #include <system.h>
87  #include <error.h>
88  #include "closeout.h"
89
90  /* The official name of this program (e.g., no 'g' prefix). */
91  #define PROGRAM_NAME "env"
92
93  #define AUTHORS N_ ("Richard Mlynarick and David MacKenzie")
94
95  int putenv ();
96
97  extern char **environ;
98
99  /* The name by which this program was run. */
100 char *program_name;
101
102 static struct option const longopts[] =
103 (
104   {"ignore-environment", no_argument, NULL, 'i'},
105   {"unset", required_argument, NULL, 'u'},
106   (GETOPT_HELP_OPTION_DECL),
107   (GETOPT_VERSION_OPTION_DECL),
108   (NULL, 0, NULL, 0)}
109 );
```

GNU Coreutils 包含大量程序，其中许多执行相同的常见任务（例如，参数解析）。为了便于维护，许多常见的惯用法被定义为宏。`GETOPT_HELP_OPTION_DECL` 和 `GETOPT_VERSION_OPTION`（第 106 和 107 行）就是其中两个。我们稍后会查看它们的定义。第一个函数 `usage()` 打印使用信息并退出。`_("string")` 宏（第 115 行，并在整个程序中使用）也用于国际化，目前你也应该将其视为所包含的字符串常量。

```
111 void  
112 usage (int status)  
113 {
114     if (status != 0)
115       fprintf (stderr, _("Try `%s --help' for more information.\n"),
116                program_name);
117     else
118       {
119         printf (_("\
120 Usage: %s [OPTION]... [-] [NAME=VALUE]... [COMMAND [ARG]...\n"],
121                   program_name);
122         fputs (_("\
123 Set each NAME to VALUE in the environment and run COMMAND.\n\
124 \
125   -i, --ignore-environment        start with an empty environment\n\
126   -u, --unset=NAME                remove variable from the environment\n\
127 "), stdout);
128         fputs (HELP_OPTION_DESCRIPTION, stdout);
129         fputs (VERSION_OPTION_DESCRIPTION, stdout);
130         fputs (_("\
131 \
132 A mere -i implies -i.  If no COMMAND, print the resulting environment.\n\
133 "), stdout);
134         printf (_("\nReport bugs to <%s>.\n"), PACKAGE_BUGREPORT);
135       }
136   exit (status);
137 }
```

`main()` 的第一部分声明变量并设置国际化。函数 `setlocale()`、`bindtextdomain()` 和 `textdomain()`（第 147–149 行）都在第 13 章“国际化和本地化”第 485 页中讨论。注意，这个程序使用了 `main()` 的 `envp` 参数（第 140 行）。它是 Coreutils 程序中唯一这样做的一个。最后，第 151 行对 `atexit()` 的调用（参见第 9.1.5.3 节“退出函数”，第 302 页）注册了一个 Coreutils 库函数，该函数刷新所有待处理的输出并关闭 `stdout`，如果有问题则报告消息。下一部分处理命令行参数，使用 `getopt_long()`。

```
139 int  
140 main (register int argc, register char **argv, char **envp)  
141 {
142   char *dummy_environ[1];  
143   int optc;  
144   int ignore_environment = 0;  
145
146   program_name = argv[0];  
147   setlocale (LC_ALL, "");  
148   bindtextdomain (PACKAGE, LOCALEDIR);  
149   textdomain (PACKAGE);  
150
151   atexit (close_stdout);
```
