# **Compiling Multiple Source Files from the Command Line**

Suppose you have conceptually divided your program into three modules and have entered the statements for the first module into a file called m       , the statements for the second module into a file called m     , and the statements for your m          routine into the file m       . To tell the system that these three modules actually belong to the same program, you simply include the names of all three files when you enter the command to compile the program. For example, using g   , the command

Click here to view code image

```
$ gcc mod1.c mod2.c main.c -o dbtest
```

has the effect of separately compiling the code contained in m          , m       , and m       . Errors discovered in m     , m     , and m      are separately identified by the compiler. For example, if the g    compiler gives output that looks like this:

Click here to view code image

```
m
m
m
```

then the compiler indicates that m         has an error at line 10, which is in the function f  . Because no messages are displayed for m       and m     , no errors are found compiling those modules.

Typically, if there are errors discovered in a module, you have to edit the module to correct the mistakes.¹ In this case, because an error was discovered only inside m       , you have to edit only this file to fix the mistake. You can then tell the C compiler to recompile your modules after the correction has been made:

> ¹ The error might be due to a problem with a header file included by that module, for example, which means the header file and not the module would have to be edited.

Click here to view code image

```
$ gcc mod1.c mod2.c main.c -o dbtest
$
```

Because no error message was reported, the executable was placed in the file d   .

Normally, the compiler generates intermediate object files for each source file that it compiles. The compiler places the resulting object code from compiling m     into the file m       by default. (Most Windows compilers work similarly, only they might place the resulting object code into  .files instead of  . files.) Typically, these intermediate object files are automatically deleted after the compilation process ends. Some C compilers (and, historically, the standard Unix C compiler) keep these object files around and do not delete them when you compile more than one file at a time. This fact can be used to your advantage for recompiling a program after making a change to only one or several of your modules. So in the previous example, because m     and m      had no compiler errors, the corresponding  . files—m      and m       —would still be around after the g    command completed. Replacing the c from the filename m      with an o tells the C compiler to use the object file that was produced the last time m     was compiled. So, the following command line could be used with a compiler (in this case, c  ) that does not delete the object code files: