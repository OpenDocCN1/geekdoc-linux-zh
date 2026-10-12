Click here to view code image

```
$ cc mod1.o mod2.c main.o -o dbtest
```

So, not only do you not have to reedit m______ and m______ if no errors are discovered by the compiler, but you also don’t have to recompile them.

If your compiler automatically deletes the intermediate .o files, you are still take advantage of performing incremental compilations by compiling each module separately and using the -c command-line option. This option tells the compiler not to link your file (that is, not to try to produce an executable) and to retain the intermediate object file that it creates. So, typing

```
$ gcc -c mod2.c
```

compiles the file m______ placing the resulting executable in the file m______.

So, in general, you can use the following sequence to compile your three-module program dbtest using the incremental compilation technique:

Click here to view code image

```
$ gcc -c mod1.c		Compile mod1.c => mod1.o
$ gcc -c mod2.c		Compile mod2.c => mod2.o
$ gcc -c main.c		Compile main.c => main.o
$ gcc mod1.o mod2.o mod3.o -o dbtest
```

The three modules are compiled separately. The previous output shows no errors were detected by the compiler. If any were, the file could be edited and incrementally recompiled. The last line that reads

```
$ gcc mod1.o mod2.o mod3.o
```

lists only object files and no source files. In this case, the object files are just linked together to produce the executable output file dbtest.

If you extend the preceding examples to programs that consist of many modules, you can see how this mechanism of separate compilations can enable you to develop large programs more efficiently. For example, the commands

Click here to view code image

```
$ gcc -c legal.c		Compile legal.c, placing output in legal.o
$ gcc legal.o makmove.o exec.o enumerator.o evaluator.o display.o -o superchess
```

could be used to compile a program consisting of six modules, in which only the module legal.c needs to be recompiled.

As you’ll see in the last section of this chapter, the process of incremental compilation can be automated by using a tool called make. The IDE tools that were mentioned at the beginning of this chapter invariably have this knowledge of what needs recompilation, and they only recompile files as necessary.