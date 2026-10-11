# **11.2.10** $\textit{BEGIN}$ and $\textit{END}$ Blocks (Startup and Finish)

The $\textit{BEGIN}$ and $\textit{END}$ special code blocks may remind UNIX programmers of the special $\textit{BEGIN}$ and $\textit{END}$ patterns used in the $awk$ programming language.
$\textit{A BEGIN}$ block is executed immediately, before the rest of the file is even parsed. If you have multiple $\textit{BEGINs}$, they will be executed in the order they were defined.
The $\textit{END}$ block is executed when all is done; that is, when the program is exiting, even if the $die$ function caused the termination. Multiple $\textit{END}$ blocks are executed in reverse order.

# **EXAMPLE 11.22**

```
use warnings;
# Program to demonstrate BEGIN and END subroutines
use warnings;
1 chdir('/stuff') || die "Can't cd: $!\n";
2 BEGIN{ print "Welcome to my Program.\n"};
3 END{ print "Bailing out somewhere near line \".$_\_LINE\_\_". "So long.\n"};

(Output):
Welcome to my Program.
Can't cd: No such file or directory
Bailing out somewhere near line 5. So long.
```

# **EXPLANATION**

+   1. An effort is made to change directories to /stuff. The $chdir$ fails and the $die$ is executed. Normally, the program would exit immediately, but this program has defined an $END$ block. The $END$ block will execute before the program dies.
+   2. The $BEGIN$ block is executed as soon as possible; that is, as soon as it has been defined. This block is executed before anything else in the program happens.
+   3. The $END$ block is always executed when the program is about to exit, even if a $die$ is called. The line printed is there just for you $awk$ programmers.

# **11.2.11** The $subs$ Function

The $subs$ function allows you to predeclare subroutine names. Its arguments are a list of subroutines. This allows you to call a subroutine without the ampersand or parentheses and to override built-in Perl functions.