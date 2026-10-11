
## EXAMPLE 3.5

**The Script**
```perl
print "Hello, world";
1 print "How are you doing?
2 print "Have you found any problems in this script?";
```

**Output**
```text
Bareword "found where operator expected at errors.plx line 3, near "*print*
*"Have".

(Might be a runaway multi-line **"* string *starting on line 2)

(Do you need to predeclare print?)

syntax error at errors.plx line 3, near "print "Have you "*
Search pattern not terminated at errors.plx line 3.
```

## EXPLANATION

- 1. This line should have a closing double quote and a terminating semicolon. Since it doesn't end in a double quote, Perl continues onto the next line looking for it.
- 2. This Perl statement is correct, but Perl is still looking for the closing quote on the previous line and finds it just before the word *Have*. Now the rest of this statement is left hanging without an initial opening quote. Whenever you see the word *runaway* in the error message, it usually means a quote that has "run away" (that is, missing). If you see *Bareword*, it means that a word has no quotes surrounding it.

After the program passes the compile phase (that is, you don't get any syntax errors or complaints from the compiler), then you may get what are called runtime, or logical, errors. These errors are harder to find and are probably caused by not anticipating problems that might occur when the program starts running. Or it's possible that the program has faulty logic in the way it was designed. Runtime errors may be caused if a file or database you're trying to open doesn't exist, a user enters bad input, you get into an infinite loop, or you try to illegally divide by zero. Whatever the case, these problems, called "bugs," are harder to find. Perl comes with a debugger that is helpful in determining what caused these logical errors by letting you step through your program line by line. (See Appendix A, "Perl Built-ins, Pragmas, Modules, and the Debugger," specifically Section A.6, "Debugger.")

## 3.5 Perl Switches

Although most of your work with Perl will be done in scripts, you can also execute Perl at the command line for simple tasks, such as testing a function, a *print* statement, or simply testing Perl syntax. Perl has a number of command-line switches, also called command-line options, to control or modify its behavior. The switches discussed next are not a complete list (again, see Appendix A), but will demonstrate a little about Perl syntax at the command line.

When working at the command line, you will see a shell prompt. The shell is called a **command interpreter**. UNIX shells such as *Korn* and *bash* display a default $ prompt, and *C* and *tcsh* shell display a # prompt. The UNIX, Linux (*bash* and *tcsh*), and Mac OS shells are quite similar in how they parse the command line. By default, if you are using Windows, the MS-DOS command-line prompt displays a \>. The Win32 shell has its own way of parsing the command line. Since most of your Perl programming will be done in script files, you will seldom need to worry about the shell's interaction, but when a script interfaces with the operating system, problems will occur unless you are aware of what commands you have and how the shell executes them on your behalf.

### 3.5.1 The -e Switch (Quick Test at the Command Line)

The *-e* switch allows Perl to execute Perl statements at the command line instead of from a script. This is a good way to test simple Perl statements before putting them into a script file, but the shells for UNIX and MS-DOS don't always parse the command line in the same way, as shown in Example 3.6.

**EXAMPLE 3.6**
```text
1  $ perl -e 'print "hello dolly\n";'      # UNIX/Linux
   hello dolly
2  $ perl -e "print qq/hello dolly\n/;"     # Windows and UNIX/Linux
   hello dolly
```

**EXPLANATION**

- 1. Perl prints the string *hello dolly* to the screen followed by a newline \n. The dollar sign ($) is the UNIX shell prompt. The single quotes surrounding the Perl statement protect it from the UNIX shell when it scans and interprets the command line. This will fail to execute on a Windows system.
- 2. At the MS-DOS prompt, Perl statements must be enclosed in double quotes. The *qq* construct surrounding *hello dolly* is another way Perl represents double quotes. For example, *qq/hello/* is the same as *"hello"*. An error is displayed if you type the following at the MS-DOS prompt:
  `perl -e 'print "hello dolly\n";'`
  `Can't find string terminator "" anywhere before EOF at -e line 1.`
  Note: UNIX systems can use this format as well.
- 4. It is possible that your command-line prompt has been customized to contain the current directory history number, drive number, and so forth.

As we demonstrated earlier in this chapter, the -c switch is used to **check** the Perl syntax without actually executing the Perl commands. If the syntax is correct, Perl will tell you so. It is a good idea to *always check scripts with the -c switch*. This is especially important with CGI scripts written in Perl, because error messages that are normally sent to the terminal screen are sent to a log file instead. (See also the -w switch in Chapter 4, “Getting a Handle on Printing.”)

**EXAMPLE 3.7**
```perl
1  print "hello";
   # Can't find string terminator "/" anywhere before EOF at test.plx
2  print "hello";
   # test.plx syntax OK
```

**EXPLANATION**

- 1. The string 'hello' starts with a double quote but ends with a single quote. The quotes should be matched—that is, the first double quote should be matched at the end of the string with another double quote but instead ends with a single quote. With the -c switch, Perl will complain if it finds syntax errors while compiling.
- 2. After correcting the previous problem, Perl lets you know that the syntax is correct.

### 3.5.3 The -w Switch (Warnings)

Even though your script may pass the compile test, when you run it, something seems strange, for example, perhaps a variable doesn’t have a value or an operation isn’t producing what you expected. The -w switch sends warning messages if you have, for example, misused operators, or if you have variables used only once, or scalar variables used before they are set, or references to undefined filehandles, and so forth.

A warning is just that: a warning. It doesn’t mean that your program has syntax errors; it means you are doing something questionable and your output might reflect that. It is a good practice to use *warnings* in your scripts rather than at the *command line*. We’ll have more about warnings and the use of the *warnings pragma* in Chapter 4. (See *perldiag documentation* for more detail.)

```perl
1  $sum = "dogs" + "5cats\n";   # trying to add two strings;
                                  # should be numbers
2  print "The sum is $sum.\n";

3  $name = "Jack";
4  print "I know $nime well.\n"; # Misspelled variable;
                                   # should be $name, not $nime
```

## 3.6 What You Should Know

1. How do you set up a script?
2. How do you name a script?
3. How are statements terminated?
4. What is whitespace?
5. What is meant by free form?
6. What is a variable?
7. What is a built-in function?
8. What is the #! line?
9. What is meant by scalar or list context?
10. How do you make a script executable?
11. Why use comments?
12. How do you execute a Perl script if not using the shebang line.
13. What command-line option lets you check Perl syntax?
14. What is the -w switch for?

## 3.7 What's Next?

**(At the Command line)**
```bash
perl -w context.plx
Name "main::nime" used only once: possible typo at context line 4.
Argument "Scats\n" isn't numeric in addition (+) at context line 1.
Argument "dogs" isn't numeric in addition (+) at context line 1.
The sum is 5.
Use of uninitialized value $nime in concatenation (.) or string at context
line 4.
I know well.
```

If you can't print what your program is supposed to do, it's like trying to read the mind of a person who can't speak. In the next chapter, we discuss Perl functions to print output to the screen ( *stdout* ) and how to format the output. You will learn how Perl views words, whitespace, literals, backslash sequences, numbers, and strings. You will learn how to use *single*, *double*, and *backquotes* and their alternative form. We will discuss *here documents* and how to use them in CGI scripts. You will also learn how to use warnings and diagnostics to help debug your scripts.
