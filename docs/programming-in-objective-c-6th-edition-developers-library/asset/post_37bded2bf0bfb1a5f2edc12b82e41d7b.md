
## 2. Compiling and Running Your First Program

In this chapter, you are introduced to the C language so that you can see what programming in C is all about. What better way to gain an appreciation for this language than by taking a look at an actual program written in C?

This chapter is short, but you'll be surprised at how much ground you can cover in a brief chapter, including

- Writing your first program.
- Modifying it to change its output.
- Understanding the main function.
- Outputting information with the printf function.
- Improving your program's readability with comments.

To begin with, you'll choose a rather simple example—a program that displays the phrase "Programming is fun." in your window. **Program 2.1** shows a C program to accomplish this task.

```c
#include <stdio.h>
int main(void) {
    printf("Programming is fun.\n");
    return 0;
}
```

In the C programming language, lowercase and uppercase letters are distinct. In addition, in C, it does not matter where on the line you begin typing—you can begin typing your statement at any position on the line. This fact can be used to your advantage in developing programs that are easier to read. Tab characters are often used by programmers as a convenient way to indent lines.

### Compiling Your Program

Returning to your first C program, you first need to type it into a file. Any text editor can be used for this purpose. Unix users often use an editor such as vi or emacs.

C compilers recognize filenames that end in the two characters ".c" as C programs. So, assume you type **Program 2.1** into a file called prog1.c. Next, you need to compile the program. Using the GNU C compiler, this can be as simple as issuing the gcc command at the terminal followed by the filename, like this:

```sh
$ gcc prog1.c
$ 
```

If you're using the standard Unix C compiler, the command is cc instead of gcc. Here, the text you typed is entered in bold. The dollar sign is your command prompt if you're compiling your C program from the command line. Your actual command prompt might be some characters other than the dollar sign.

If you make any mistakes keying in your program, the compiler lists them after you enter the gcc command, typically identifying the line numbers from your program that contain the errors. If, instead, another command prompt appears, as is shown in the preceding example, no errors were found in your program.

When the compiler compiles and links your program, it creates an executable version of your program. Using the GNU or standard C compiler, this program is called a.out by default. Under Windows, it is often called a .exe instead.

### Running Your Program

You can now run the executable by simply typing its name on the command line:

> ¹ If you get an error like this: a.out: No such file or directory, then it probably means the current directory is not in your PATH. You can either add it to your PATH or type the following at the command prompt: ./a.out.

```sh
$ a.out
Programming is fun.
$
```

You can also specify a different name for the executable file at the time the program is compiled. This is done with the -o (that’s the letter O) option, which is followed by the name of the executable. For example, the command line

```sh
$ gcc prog1.c -o prog1
```

compiles the program, placing the executable in the file prog1, which can subsequently be executed just by specifying its name:

```sh
$ prog1
Programming is fun.
$
```

### Understanding Your First Program

Take a closer look at your first program. The first line of the program

```c
#include <stdio.h>
```

should be included at the beginning of just about every program you write. It tells the compiler information about the printf output routine that is used later in the program. Chapter 12, “The Preprocessor,” discusses in detail what this line does.

The line of the program that reads

```c
int main(void)
```

informs the system that the name of the program is main, and that it returns an integer value, which is abbreviated “int.” main is a special name that indicates precisely where the program is to begin execution. The open and close parentheses immediately following main specify that main is the name of a function. The keyword void that is enclosed in the parentheses specifies that the function main takes no arguments (that is, it is void of arguments). These concepts are explained in great detail in Chapter 7, “Working with Functions.”

**Note**

If you're using an IDE, you may find that it generates a template main for you. In such a case, you may find the first line of main looks more like this:

```c
#include <stdio.h>
int main(int argc, char *argv[]) {
```

This won't affect your program's operation, so just ignore the differences for now.

Now that you have identified main to the system, you are ready to specify precisely what this routine is to perform. This is done by enclosing all program statements of the routine within a pair of curly braces. All program statements included between the braces are taken as part of the main routine by the system. In **Program 2.1**, you have only two such statements. This statement specifies that a routine named printf is to be invoked or *called*. The parameter or *argument* to be passed to the printf routine is the string of characters "Programming is fun.\n".

The printf routine is a function in the C library that simply prints or displays its argument (or arguments, as you will see shortly) on your screen. The last two characters in the string, namely the backslash (\) and the letter n, are known collectively as the *newline* character. A newline character tells the system to do precisely what its name implies—that is, go to a new line. Any characters to be printed after the newline character then appear on the next line of the display. In fact, the newline character is similar in concept to the carriage return key on a typewriter. (Remember those?)

All program statements in C *must* be terminated by a semicolon (;). This is the reason for the semicolon that appears immediately following the closing parenthesis of the printf call. The last statement in main that reads

```c
return 0;
```

says to finish execution of main, and return to the system a status value of 0. You can use any integer here. Zero is used by convention to indicate that the program completed successfully—that is, without running into any errors. Different numbers can be used to indicate different types of error conditions that occurred (such as a file not being found). This exit status can be tested by other programs (such as the Unix shell) to see whether the program ran successfully.

Now that you've finished analyzing your first program, you can modify it to also display the phrase “And programming in C is even more fun.” This can be done by the simple addition of another call to the printf routine, as shown in **Program 2.2**. Remember that every C program statement must be terminated by a semicolon.

**Program 2.2**

```c
#include <stdio.h>
int main(void) {
    printf("Programming is fun.\n");
    printf("And programming in C is even more fun.\n");
    return 0;
}
```

If you type in Program 2.2 and then compile and execute it, you can expect the following output in your program’s output window, sometimes called the “console.”

**Program 2.2 Output**

```
Programming is fun.
And programming in C is even more fun.
```

As you will see from the next program example, it is not necessary to make a separate call to the printf routine for each line of output. Study the program listed in Program 2.3 and try to predict the results before examining the output. (No cheating now!)

**Program 2.3 Displaying Multiple Lines of Output**

```c
#include <stdio.h>
int main(void) {
    printf("Line 1\nLine 2\nLine 3\n");
    return 0;
}
```

**Program 2.3 Output**

```
Line 1
Line 2
Line 3
```

### Displaying the Values of Variables

The printf routine is the most commonly used routine in this book. This is because it provides an easy and convenient means to display program results. Not only can simple phrases be displayed, but the values of variables and the results of computations can also be displayed. In fact, Program 2.4 uses the printf routine to display the results of adding two numbers, namely 50 and 25.

**Program 2.4 Displaying Variables**

```c
#include <stdio.h>
int main(void) {
    int a, b, c;
    a = 50;
    b = 25;
    c = a + b;
    printf("Sum = %d\n", c);
    return 0;
}
```
