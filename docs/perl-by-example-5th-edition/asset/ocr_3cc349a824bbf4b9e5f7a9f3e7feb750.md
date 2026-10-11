# # 4

# ## Getting a Handle
## on Printing

When you complete this chapter, you should be able to explain each of the following statements (each statement is an entity unto itself):

```
```perl
10 print$ "$-10g\\t($$$10.2f\\t$@\\t&x\\t$o\\n", "Jack", 15,15,15,15,15;
11 print 'She cried, "I can\\'t help you!"\\n';
12 $str = sprintf "%$.2F", $aa!;
13 print qq!\\u$name, the local time is !, $calar localtime, "\\n";
14 use feature qw(say);
15 say "The sum is ", 5 + 4;
16 say "No more! "
```
```

Before we get started, please take note that each line of code, in most of the examples throughout this book, is numbered. The output and explanations are also numbered to match the numbers in the code. These numbers are provided to help you understand important lines of each program. When copying examples into your text editor, don't include these numbers, or you will generate many unwanted errors!

# ### 4.1 The Special Filehandles STDOUT, STDIN, STDERR

In Chapter 3, "Perl Scripts," we briefly introduced standard I/O. By convention, whenever your program starts execution, the parent process (normally a shell program) opens three predefined streams called *stdin*, *stdout*, and *stderr*. All three of these streams are connected to your terminal by default.

*stdin* is the place where input comes from, the terminal keyboard; *stdout* is where output normally goes, the screen; and *stderr* is where errors from your program are printed, also the screen.