
# Using foreach

When you find yourself putting in commands over and over, you can use the foreach statement that executes a code block for each data item in an array. An array is a set of elements indexed sequentially that have the same type of data. Most times, each element of an array has a unique identifying index number. Changes made to one element of an array do not affect the others. foreach specifies that for each entry in the array of entries, Unix will output the entries to the terminal. Commonly, foreach is used in place of a standard for loop. Unlike this for construct, a foreach loop usually does not specify the order in which the items are considered.

The point of this is, if you don't want to spend a massive amount of time inputting files into a command to automate them, you can use the foreach command, which takes a list of files, and does something "each of" based on what you specify. The commands' use is much easier to demonstrate than to explain. If you have a list of files that you need to do something to, you can follow these steps to use foreach:

- Figure out what you want to do. In the following example, you've got a bunch of directories (1 through 3), and you want to create a tar file of each of them.

- Decide on the names of the files/directories that you want to do something to. In this case, you're going to create tar files for the directories directory1, directory2, and directory3.

- Pick a variable name that you want to use. For this example, you're going to use a variable named test. It doesn't matter what the variable name is, as long as it doesn't conflict with the name of the command.

- Issue the foreach command as foreach <variable> (<filenames>). The foreach command then asks what you want to do for each file by displaying a question mark. Fill this in with whatever you need to do. Again, you're going to be taring files in the example. After giving foreach the command for whatever it is you want to do, finish it by putting the command on a line by itself.

# Lesson 14

This can be seen as:

```
> foreach test (directory1 directory2 directory3)
? tar -cvf $test.tar $test
? end
```

Your machine responds by running the tar command for each file you gave to it. Inside the foreach command loop, note the use of the expression $test. foreach goes through the list of filenames you gave to and puts each sequentially in the test variable. To use the contents of a variable in a shell, put a $ sign before it. For example, foreach first puts mydirectory1 in the test variable. It runs the tar command, and the shell expands the variable to directory1. The tar command that gets executed actually looks like this: tar -cvf mydirectory.tar mydirectory. The next time through the loop, foreach puts directory2 in the variable test, and the process is repeats.

You can use regex in the shell instead of enumerating filenames to the foreach command. If you notice in the previous example, all the directories you want to tar foreach have part of their names in common directory. If you want to produce the same results without having to enumerate all the directory names to foreach, you might issue the preceding foreach command as follows: foreach test (*directory).

> What Shell Should I Use? In some examples, you may see the C shell used (csh). It is the opinion of this author that csh is a tool not adequate for programming and learning shell scripting. Also, it is better for you to learn on the shell you know, or a commonly used and supported shell, especially if you are a new learner to Unix. The use of csh to create shell scripts should be avoided if you can. The use of csh to build simple scripts is cumbersome, problematic, and some-times next to impossible.

It's easy to see how you can use Unix to control process, and now, you should start to see the granular level of control Unix can give you over what it is you do work on.

![](img/9552a570ce35faac09a770fd5ff1ede3_190_0.png)

You can fine-tune, tweak, and customize your system once you know how to master these fundamentals. Now that you are familiar with the foreach command, let's look at conditional statements such as while and if.

# Using while and if

If you want to build more complex scripts, you can use other statements to control your automations. You can turn to activate certain sections of your script only when certain conditions apply. To use conditional statements, you need to create a condition for the statement to test. This lesson covers the basics; just be aware that this can get in-depth as there are many operators, and different items of syntax you can work with.

> Hello Operator? Almost all programming languages in existence have a set of operators that perform arithmetical operations. Computers are mathematical devices, which function based on Boolean math.

The if command works in much the same way as the while command, except it doesn't loop; it simply executes one command based on the condition. The syntax of the if command is as follows: if (<condition>) <command>. The while command, with the syntax while (<condition>), does things while a condition holds.

To set up a conditional statement, you can check out the following syntax, which is based on if and evaluates an expression placed in parentheses as seen here:

```
if ( the expression )
actionA
else
actionB
```

If the expression evaluates as true, the first action (actionA) is done. The other clause you can specify is else, which makes sense. “If you don’t have key, then else.”

- actionA
- actionB

# Summary

In this lesson, we covered what you need to know, and now we will wrap up. There are many shells and your shell might work differently than is presented. Here’s a review of the key points:

- The foreach command enables you to repeat a set of commands for each of files.
- The while command enables you to repeat a set of commands while a condition holds.
- The if command enables you to execute a command, or not execute it, based on a condition.

# Lesson 15

# User Utilities

In this lesson, you will learn how to change settings on your Unix system and modify or alter your environment.

When working with Unix, you will undoubtedly come to a point where some form of customization is required. For instance, we talked about logging in to your Unix system, but what about changing your password? We have also discussed the shell many times, especially in the last lesson on shell scripting, but what if you want to change your shell?

# Using chsh

In our discussion of shells earlier in this book, we have talked many times about what shell you are using or what shell prompt commands you can perform. We have also touched on why you may want to change your shell, and now we will cover how to just that.

In the beginning of this book, you learned that there are a variety of different shells that you can run; covered most if not all of them. There will be times when you want to change your shell, and to do that, you can use the change shell command, or chsh. This means that you must have a shell on your system in order to request it.

One problem you may encounter is not knowing which shell to choose; after all, there are so many shells, and how do you know which ones are registered for use on your system? To solve this problem, you can use the chsh command with the -l option. The chsh -l command will
