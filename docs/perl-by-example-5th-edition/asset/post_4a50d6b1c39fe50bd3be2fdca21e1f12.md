
## Part 4

- 1. Sort the datebook file by names, using a pipe.

## Part 5

- 1. Create a number of duplicate entries in the datebook file. Fred Fardarkle, for example, might appear five times, and Igor Chevsky three times. In most editors, this will be a simple copy/paste operation.
    - a. Write a program that will assign the name of the datebook file to a scalar and check to see if the file exists. If it does exist, the program will check to see if the file is readable and writable. Use the die function to send any errors to the screen. Also tell the user when the datebook was last modified.
    - b. The program will read each line of the datebook file giving each person a 10% raise in salary. If, however, the person appears more than once in the file (assume having the same first and last name means it is a duplicate), he will be given a raise the first time, but if he appears again, he will be skipped. Send each line of output to a file called raise. The raise file should not contain any person's name more than once. It will also reflect the 10% increase in pay. Display on the screen the average salary for all the people in the datebook file. For duplicate entries, print the names of those who appeared in the file more than once, and how many times each appeared.
- 2. Write a script called checking that will take any number of filenames as command-line arguments and will print the names of those files that are readable and writable text files. The program will print an error message if there are no arguments, and exit.

## Chapter 11

### How Do Subroutines Function?

![](img/8556abcb353c0991f12099420ec28735_376_0.png)

In computer programming, a **subroutine** is a sequence of program instructions that perform a specific task, packaged as a unit. This unit can then be used in programs wherever that particular task should be performed. Subprograms may be defined within programs, or separately in libraries that can be used by multiple programs. In different programming languages, a subroutine may be called a procedure, a function, a routine, a method, or a subprogram. The generic term callable unit is also sometimes used.[^1]

Perl allows you to collect a sequence of statements, give the collection a name, and use the collection just as you use the built-in functions, such as `print` and `localtime`. This collection can be called a subroutine or a function. It doesn't matter.

By the end of this chapter, you should be able to explain each line in the following program.

```perl
1 use feature 'say';
2
3 print "What is the current Fahrenheit temperature? ";
4 chomp( $fahr = <STDIN> );
5 say "$fahr Fahrenheit converted to Celsius is ", converter($fahr), ".";
6 say "program continues here";
7
8 sub converter{
9     my $fTemp = @_;
10    if ($fTemp < -459 ) { return "too cold"; }
11    my $celsius = ($fTemp - 32 ) * 5/9;
12    return int $celsius;
13}
```

[^1]: Wikipedia, "Subroutine," http://en.wikipedia.org/wiki/Subroutine.

### 11.1 Subroutines/Functions

We have been using a number of Perl's built-in functions since the beginning of this book. In addition to the large number of Perl functions already available, you can create your own. Some languages distinguish between the terms **function** and *subroutine*. Perl doesn't. Technically, a function is a block of code that returns a value, whereas a subroutine is a block of code that performs some task, but doesn't return anything. Perl subroutines and functions can do both, so we'll use the two terms interchangeably in this text. For now, we'll use the term “subroutine” when referring to user-defined functions.

Let's further define the Wikipedia definition of subroutine. Subroutines are self-contained units of a program designed to accomplish a specified task, such as calculating a mortgage payment, retrieving data from a database, or checking for valid input. When a subroutine is called in a program, it is like taking a detour from the main part of the program. Perl starts executing the instructions in the subroutine and when finished, returns to the main program and picks up where it left off. You can use subroutines over and over again and thus save you from repetitive programming. They are also used to break up a program into smaller units to keep it better organized and easier to maintain. If the subroutine proves to be useful in other programs, you can store it in a library as a module (discussed in Chapter 13, “Modularize It, Package It, and Send It to the Library!”).

The subroutine definition consists of one or more statements enclosed in a *black box*, independent of your program and not executed until it is called. It is often referred to as a *black box*. Information goes into the black box as input (like the calculator or remote control when you push buttons), and the action or value returned from the box is its output (such as a calculation or a different channel, continuing the analogy). What goes on inside the box is transparent to the user. The programmer who writes the subroutine is the *only* one who cares about those details. When you use Perl's built-in functions, such as *print* or *rand*, you send a string of text or a number to the function, and it sends something back. You don't care how it does its job; you just expect it to work. If you send bad input, you get bad back or output or maybe nothing, hence the expression “garbage in, garbage out.”

The *scope* of a subroutine is *where* it is *visible* in the program. Up to this point, all scripts have been in the namespace *main*, the *main package*. Subroutines are global in that they are visible or available to the entire script *where* they are defined. And you can place them *anywhere* in the script. You can define them in another file, and when coming from another file, they are loaded into the script with the *require* or *use* functions. All variables *created within* a subroutine or accessed by *it* are also *global*, unless specifically made local with *either the local* or *my* operators.

The subroutine is called, or invoked, by appending a set of empty parentheses to the subroutine name. (Rarely you will see a function called by prepending it with an ampersand, but that style is outdated in modern Perl.) If you use a forward reference, neither ampersands nor parentheses are needed to call the subroutine. You can send scalars, arrays, hashes, references, and the like to subroutines in an argument list and receive them by the function. This is all covered in the following pages.

If a nonexistent subroutine is called, the program quits with an error message: Undefined subroutine in "main::prog" .... If you want to check whether the subroutine has been defined, you can do so with the built-in defined function.

The return value of a subroutine is the value of the last expression evaluated (either a scalar or a list). You can use the return function explicitly to return a value or to exit from the subroutine early, based on the result of testing some condition.

If you make the call to the subroutine part of an expression, you can assign the returned value to a variable, thus emulating a function call.

### FORMAT

```text
Subroutine declaration:
sub subroutine_name;
Subroutine definition:
sub subroutine_name { Block }
Subroutine call:
subroutine_name();
subroutine_name; # Alternate method
subroutine_name;
Subroutine call with parameters:
subroutine_name(parameter1, parameter2, ... )
```

#### 11.1.1 Defining and Calling a Subroutine

A declaration simply announces to the Perl compiler that a subroutine is going to be defined in the program and may take specified arguments. Declarations are global in scope for a package (we have been working in package main). In other words, they are visible no matter where you put them in the program, although it is customary to put declarations at the beginning or end of the program, or in another file. (For now, we will define the subroutines in one file, package main.) We will discuss packages in Chapter 13, “Modularize It, Package It, and Send It to the Library!” but it is important to note that when we use the term global variable, it is technically called a package variable. A subroutine definition is a block of statements that follows the subroutine name. A subroutine you do not explicitly declare is declared at the same time it is defined.

- Declaration: sub name;
- Definition: sub name { statement; statement; }

You can define a subroutine anywhere in your program (or even in another file). The subroutine consists of the keyword sub followed by an opening curly brace, a set of statements, and ending in a closing curly brace.
