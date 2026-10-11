
scratch。如果 `clearenv()` 不可用，GNU/Linux `clearenv(3)` 手册页建议使用 `‘environ = NULL;’` 来完成此任务。

## 2.4.2 整个环境：environ

处理环境的正确方式是使用前一节中描述的函数。然而，值得了解一下“幕后”的管理方式。

外部变量 `environ` 提供了访问环境的方式，就像 `argv` 提供访问命令行参数的方式一样。你必须自己声明这个变量。尽管 `environ` 已被 POSIX 标准化，但它故意不被任何标准化头文件声明。（这似乎源于历史惯例。）声明如下：

```
extern char **environ; /* 看，没有头文件！ */ POSIX
```

与 `argv` 类似，`environ` 中的最后一个元素是 NULL。然而，并没有一个与 `argc` 对应的“环境计数”变量。这个简单的程序打印出整个环境：

```
/* ch02-printenv.c --- 打印出环境。 */
#include <stdio.h>

extern char **environ;

int main(int argc, char *argv)
{
 int i;

 if (environ != NULL)
 for (i = 0; environ[i] != NULL; i++)
 printf("%s\n", environ[i]);

 return 0;
}
```

虽然这种情况不太可能发生，但这个程序确保了在使用 `environ` 之前它不是 NULL。

变量在环境中以随机顺序保存。尽管一些 Unix shell 按变量名对环境中进行排序，但这并没有正式要求，许多 shell 也不会保持排序。

作为实现上的一种怪癖，你可以通过**声明 `main( )` 的第三个参数**来访问环境：

```
int main(int argc, char **argv, char **envp)
{
...
}
```

然后你可以像使用 `environ` 一样使用 `envp`。尽管你可能会在旧代码中偶尔看到这种做法，但我们不推荐使用它；如果你需要这样做，`environ` 是访问整个环境的官方、标准且可移植的方式。

### 2.4.3 GNU env

为了结束本章，这里介绍 GNU 版本的 `env` 命令。此命令为单条命令的执行期间向环境中添加变量。它还可以用于清除该命令的环境或移除特定的环境变量。

这个程序对我们具有双重用途，因为它同时演示了 `getopt_long( )` 和本节讨论的几个函数。以下是该程序的调用方式：

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

```
152
153	while ((optc = getopt_long (argc, argv, "+iu:", longopts, NULL)) != -1)
154	{
155	  switch (optc)
156	  {
157	    case 0:
158	      break;
159	    case 'i':
160	      ignore_environment = 1;
161	      break;
162	    case 'u':
163	      break;
164	    case_GETOPT_HELP_CHAR;
165	    case_GETOPT_VERSION_CHAR (PROGRAM_NAME, AUTHORS);
166	    default:
167	      usage (2);
168	  }
169	}
170	if (optind != argc && !strcmp (argv[optind], "-"))
171	  ignore_environment = 1;
```

以下是来自 Coreutils 分发版中 `src/sys2.h` 的宏，它们定义了我们前面看到的声明以及上面使用的 `case_GETOPT_xxx` 宏（第 164–165 行）：

```
/* Factor out some of the common --help and --version processing code.  */

/* These enum values cannot possibly conflict with the option values
   ordinarily used by commands, including CHAR_MAX + 1, etc.  Avoid
   CHAR_MIN - 1, as it may equal -1, the getopt end-of-options value.  */
enum
{
  GETOPT_HELP_CHAR = (CHAR_MIN - 2),
  GETOPT_VERSION_CHAR = (CHAR_MIN - 3)
};

#define GETOPT_HELP_OPTION_DECL \
  "help", no_argument, 0, GETOPT_HELP_CHAR
#define GETOPT_VERSION_OPTION_DECL \
  "version", no_argument, 0, GETOPT_VERSION_CHAR

#define case_GETOPT_HELP_CHAR                 \
  case GETOPT_HELP_CHAR:                      \
    usage (EXIT_SUCCESS);                     \
    break;                                    \

#define case_GETOPT_VERSION_CHAR(Program_name, Authors)  \
  case GETOPT_VERSION_CHAR:                              \
    version_etc (stdout, Program_name, PACKAGE, VERSION, Authors);  \
    exit (EXIT_SUCCESS);                                  \
    break;
```

