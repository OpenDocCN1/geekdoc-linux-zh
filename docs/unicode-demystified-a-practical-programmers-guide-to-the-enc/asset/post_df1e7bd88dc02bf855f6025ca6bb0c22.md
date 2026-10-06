
The following Makefile uses macros, as well as implied dependencies and constructions:

```makefile
# makefile: report, print, printf, printf
#
CC=gcc
CFLAGS = -O3
# comment out the two lines above and uncomment the
# two below when you are using the Portland Group's compiler
#CC=pgcc
#CFLAGS = -fast
FILES = in.c out.ratio.c process.c tally.c
OBJECTS = in.o out.ratio.o process.o tally.o
HEADERS = names.h companies.h conventions.h

report: $(OBJECTS)
	$(LINK) -o report $(OBJECTS)

ratio.o: $(HEADERS)

tally.o: $(HEADERS)

print:
	pr $(FILES) $(HEADERS) | 1p

printf:
	pr $(FILES) | 1p

prints:
	pr $(HEADERS) | 1p
```

Following the comment lines, the make uses the CFLAGS macro to cause always to use the optimizer (-O3 option) when it invokes the C compiler as a result of an implied construction. (The CC and CFLAGS definitions for the gcc C compiler perform the same functions when they are uncommented and you are using gcc, except that you use -fast with gcc in place of -O3 with gcc.) Whenever you put a construction line in a Makefile, the construction line overrides the corresponding implied construction line, if one exists. If you want to apply a macro to a construction command, you must include the macro in that command. This was done, for example, with OBJECTS in the construction command for the report target. Following CFLAGS, the Makefile defines the FILES, OBJECTS, and HEADERS macros. Each of these macros defines a list of files.

The first dependency line shows that report depends on the list of files that OBJECTS defines. The corresponding construction line links the OBJECTS and executable file named report.

The next three dependency lines show that three object files depend on the list of files that HEADERS defines. There are no construction lines, so when it is necessary, make looks for a source code file corresponding to each of the object files and compiles it. These three dependency lines ensure that the object files are recompiled if any of the header files is changed.

Finally, the LINK is invoked to link the executable file. If you specify any LDFLAGS, they are used in this step.

You can combine several targets on one dependency line, these three dependency lines could have been combined into one line as:

```makefile
ratio.o process.o tally.o: $(HEADERS)
```

The three dependency lines send source and header files to the printer. They have nothing to do with compiling the report file. None of these targets (print, printf, and prints) depends on anything. When you call one of these targets from the command line, make executes the construction line following it. The following command prints all the source files that defines:

```bash
$ make printf
```

You can override macros in a Makefile by specifying them on the command line, causing debugging symbols to be added to all object files:

```bash
$ make CFLAGS=-g ...
```

## Debugging C Programs

The C compiler is liberal about the kinds of constructs it allows in programs. In keeping with the UNIX philosophy that “no news is good news” and that the user knows what is best, gcc, like many other GNU/Linux utilities, accepts almost anything that is logically possible according to the definition of the language. Although this approach gives the programmer a great deal of flexibility and control, it can make debugging difficult.

Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

In the following example, badtabs.c is compiled and then run with input from the testtabs file. Inspection of the output shows that the TAB character has not been replaced with the proper number of SPACES:

```bash
$ gcc -o badtabs.c
$ cat testtabs
abcTabxyz
$ badtabs < testtabs
abc xyz
```

```c
1 /* convert tabs in standard input to spaces /* */
2 /* standard output while maintaining columns */
3
4 #include <stdio.h>
5 #define TABSIZE 8
6
7 /* prototype for function findstop */
8 int findstop(int *);
9
10 main()
11 {
12 int c;               /* character read from stdin */
13 int posn = 0;        /* column position of character */
14 int inc;             /* column increment to tab stop */
15
16 while ((c = getchar()) != EOF)
17 {
18 switch(c) {
19
20 case 't':           /* c is a tab */
21 inc = findstop(&posn);
22 for (; inc > 0; inc--)
23 putchar('\t');
24 break;
25
26 case '\n':          /* c is a newline */
27 putchar(c);
28 posn = 0;
29 break;
30
31 default:            /* c is anything else */
32 putchar(c);
33 posn++;
34 break;
35 }
36 }
37 /* compute size of increment to next tab stop **/
38 {
39 int findstop(int *col)
40 int colindex, retval;
41 retval = (TABSIZE - (*col % TABSIZE)) % TABSIZE;
42 /* increment (current position) to next tab stop */
43 *col += retval;
44 return retval;
45 }
```

Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

In the following example, badtabs.c is compiled and then run with input from the testtabs file. Inspection of the output shows that the TAB character has not been replaced with the proper number of SPACES:

```bash
$ gcc -o badtabs.c
$ cat testtabs
abcTabxyz
$ badtabs < testtabs
abc xyz
```

One way to debug a program is to insert print statements at critical points. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

In the following example, badtabs.c is compiled and then run with input from the testtabs file. Inspection of the output shows that the TAB character has not been replaced with the proper number of SPACES:

```bash
$ gcc -o badtabs.c
$ cat testtabs
abcTabxyz
$ badtabs < testtabs
abc xyz
```

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

## Debugging C Programs

The C compiler is liberal about the kinds of constructs it allows in programs. In keeping with the UNIX philosophy that “no news is good news” and that the user knows what is best, gcc, like many other GNU/Linux utilities, accepts almost anything that is logically possible according to the definition of the language. Although this approach gives the programmer a great deal of flexibility and control, it can make debugging difficult.

Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

In the following example, badtabs.c is compiled and then run with input from the testtabs file. Inspection of the output shows that the TAB character has not been replaced with the proper number of SPACES:

```bash
$ gcc -o badtabs.c
$ cat testtabs
abcTabxyz
$ badtabs < testtabs
abc xyz
```

## Compiler Options Find Errors in Programs

Among the -W options are a class of warnings that typically result from carelessness or inexperience. The constructs causing these warnings are generally easy to fix and avoid. Table 16-2 lists some of these options.

| -W Option | Reports These Errors | table 16-2 |
| --- | --- | --- |
| -Wimplicit | When a function or parameter is not explicitly declared | |
| -Wreturn-type | When a function that is void does not return a value, or when the type of a function defaults to int | |
| -Wunused | When a variable is declared but not used | |
| -Wcomment | When the characters /* which normally begin a comment, are seen within a comment | |
| -Wformat | When certain input/output statements contain format specifications that do not match the arguments | |

Get warnings about all the preceding errors, along with others in this class, use the -Wall option.

The program badtabs.c is syntactically correct (it compiles without generating an error). However, if you compile (-c causes gcc to compile but not to link) it with the -Wall option, you see several problems:

```bash
$ gcc -c -Wall badtabs.c
badtabs.c:47: warning: '/*' within comment
badtabs.c:11: warning: return-type defaults to 'int'
badtabs.c: In function 'main'
badtabs.c:34: warning: control reaches end of non-void function
badtabs.c: In function 'findstop'
badtabs.c:40: warning: unused variable 'colindex'
badtabs.c:49: warning: control reaches end of non-void function
```

One way to debug a program is to insert print statements at critical points. Figure 16-4 badtabs.c, a flawed version of the tabs.c program discussed earlier. It contains some errors and does not run properly but illustrates some-debugging techniques.

The fprintf statements provide additional information about the execution of the program. For simple programs or when you have an idea of what is wrong with your program, using the statements can help you trace the execution.
