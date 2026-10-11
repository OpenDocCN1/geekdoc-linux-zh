
you can take a pencil and a piece of paper and draw computer memory and a screen. One sheet of paper can serve as the memory and another as the screen. It's that simple.

Consider that the following program isn't working. It says "Hello" to all your friends and then "Good-bye"—but keeps repeating these messages endlessly. Look through the following example to see whether you can determine the problem:

```bash
#!/bin/bash
let flag=1
while [ "$flag" -eq 1 ]
do
    for friend in Bob Mary Sue
    do
        echo "Hello $friend."
    done
    echo "Good-bye!"
    let flag=1
done
```

The first thing that you need to do is to indent your code to make it readable, as in the following example:

```bash
#!/bin/bash
let flag=1
while [ "$flag" -eq 1 ]
do
    for friend in Bob Mary Sue
    do
        echo "Hello $friend."
    done
    echo "Good-bye!"
    let flag=1
done
```

Next, on the piece of paper that represents your computer's memory, write the line `let flag=1`. That's what your computer is doing.

The next instruction tells your computer to check whether the value of `$flag` is 1. So look at the piece of paper, and you can see that, yes, it's equal to 1 (and for this discovery you went to college?). You must, therefore, follow the instructions inside the loop.

The first of these instructions tells the computer to place the string `Bob` into the string variable `$friend`. Write this information on the paper. Your paper version of your computer memory should now appear as follows:

```text
let flag=1
declare friend="Bob"
```

The next line tells the computer to display `Hello Bob.` on-screen. Write this greeting on the paper that you're using as your screen.

Continue this process until all the names appear on-screen. Your paper should now look as follows:

```text
Hello Bob.
Hello Mary.
Hello Sue.
```

You don't find any more values in the `for` loop, so the loop ends and the next line executes. This line tells your computer to display `Good-bye!` on-screen.

Now write that same line on your paper so that what appears on your paper is as follows:

```text
Hello Bob.
Hello Mary.
Hello Sue.
Good-bye!
```

The next line tells your computer to place the value 1 in the `$flag` variable. Go to the piece of paper that contains the variables, find the `$flag` variable, and erase whatever value appears there. Place a 1 next to the `$flag` variable.

Why erase the value? You're doing exactly what your computer does as it reads your program. It always overwrites whatever value you already assigned to a variable (picky, picky).

Return to the top of the loop, check the value of the `$flag` variable, and repeat the process.

Wait! Do you see the bug? The computer keeps displaying the same messages because the value of the `$flag` variable is now always 1.

The following example shows how you fix the bug:

```bash
#!/bin/bash
let flag=1
while [ "$flag" -eq 1 ]
do
    for friend in Bob Mary Sue
    do
        echo "Hello $friend."
    done
    echo "Good-bye!"
    let flag=0
done
```

The value of `let flag` now changes to 0 at the end of the loop.

## Look at your code while the program's running

Reviewing each line of your code is fine for short programs, but it's a nightmare if you're using this method to debug a much larger and more complex program.

Debugging a program (that's nerd talk for finding the problem with your program) is tedious work. Regardless of what method you use to locate the problem, you still need to review the lines of your code as the final step in this process.

Your inability to see your instructions while your program is running is a drawback in debugging your program. You simply can't see what's happening in that black box.

The following list describes two ways that you can solve this problem (assuming that the name of your program is `myprogram` and you're using the `bash` shell):

- Use the `-v` option, also known as the verbose option, to tell your computer to display each line of code before it executes it. You use the following expression:
  ```text
  $ bash -v myprogram
  ```
  You call the `bash` shell explicitly with the `-v` option and the name of your program by using this expression.
- Use the `-x` option, also known as the echo option, to make your computer display each line after it executes it. Use the following expression to do so:
  ```text
  $ bash -x myprogram
  ```

The major difference between these two methods is that `-v` shows you the instruction before the computer executes it, and `-x` shows it to you after it executes the instruction.

## Laying a Trap for the Bug

Sometimes you can look at your code until you can't see straight, and you still can't determine why your program isn't working. This situation can become very frustrating, but don't give up. Instead, try another tactic.

Following are some good fallback plans that you can try:

- **Set flags for yourself throughout the program.** A *flag* is a message that appears on-screen to tell you what part of your program your computer is currently reading (see Chapter 4).
- **Display the value of all the variables in your program on-screen.** This procedure gives you a glimpse of what's happening behind the scenes (see Chapter 4).
- **Turn parts of your program off and on by making the expression `true` or `false`.** This process helps you to isolate the part of your program that's causing the trouble (see Chapter 3).

Just use a little common sense in using any of these methods. You must decide where to place the flags and which parts of your program you turn off and on.

## Setting flags

A *flag* is simply a message that appears on-screen. The message of a flag can be as simple as “I got this far.”

The following example shows you how to use flags in your program (and notice that the `let` command designates the flag):

```bash
#!/bin/bash
let flag=1
echo "Outside of while loop"
while [ "$flag" -eq 1 ]
do
    echo "Inside of while loop"
    for friend in Bob Mary Sue
    do
        echo "Inside of for-in loop"
        echo "Hello $friend."
    done
    echo "Outside of for-in loop"
    echo "Good-bye!"
    let flag=1
    echo "last line in while loop"
done
echo "last line in the program"
```

You see the following messages on-screen as you run this program:

```text
Outside of while loop
Inside of while loop
Inside of for-in loop
Hello Bob.
Inside of for-in loop
Hello Mary.
Inside of for-in loop
Hello Sue.
Outside of for-in loop
Good-bye!
last line in while loop
Inside of while loop
Inside of for-in loop
Hello Bob.
Inside of for-in loop
Hello Mary.
Inside of for-in loop
Hello Sue.
Outside of for-in loop
Good-bye!
last line in while loop
```

Take a close look at these flags. Do you see anything strange? Following are some clues:

- All the flags inside the `while` loop repeat. They repeat endlessly if you run this program.
- The flag `last line in the program` doesn't appear on-screen.

Where's the problem? The computer enters the `while` loop but doesn't leave the `while` loop; the value of `flag` is always equal to 1. The condition in the `while` loop, therefore, is always true, and the loop never ends.

## Display hidden values

You can ask the computer to show you values of variables while the program's running. You can combine this method with the flag method to give you more clues to the puzzle. Normally, the value of the `flag` variable doesn't appear on-screen because you use the `flag` variable only to control active instructions. You can, however, use the `echo` command to display the value of the `flag` variable on-screen.

The following example shows you how to use this method:

```bash
#!/bin/bash
let flag=1
echo "Outside of while loop flag = $flag"
while [ $flag -eq 1 ]
do
    echo "Inside of while loop flag = $flag "
    for friend in Bob Mary Sue
    do
        echo "Inside of for in loop flag = $flag "
        echo "Hello $friend."
    done
    echo "outside of for in loop flag = $flag "
    echo "Good-bye!"
    let flag=
    echo "last line in while loop flag = $flag "
done
echo "last line in the program flag = $flag "
```

Following is what you see on-screen as a result of running this program:

```text
Outside of while loop flag = 1
inside of while loop flag = 1
inside of for in loop flag = 1
Hello Bob.
outside of for in loop flag = 1
inside of for in loop flag = 1
Hello Mary.
inside of for in loop flag = 1
Hello Sue.
outside of for in loop flag = 1
Good-bye!
last line in while loop flag = 1
inside of while loop flag = 1
inside of for in loop flag = 1
Hello Bob.
inside of for in loop flag = 1
Hello Mary.
inside of for in loop flag = 1
Hello Sue.
outside of for in loop flag = 1
Good-bye!
last line in while loop flag = 1
```

Now you realize that your program never assigns the `let flag` variable the value of 0. You know the cause of the problem because it creates an endless loop (see Chapter 10).

## Using a file to help find the problem

Displaying flags and the value of variables on-screen is helpful in finding a problem in your program. With some programs, however, this method isn't practical. You have just too much information to keep on-screen.

A better approach is to make the computer save the stuff that appears on-screen to a file. You use the following command to do so:

```text
myprogram > flagfile
```

In this example, you tell the computer to run `myprogram` and to redirect to the file `flagfile` anything that goes to the screen. You can review the flag-file by using a text editor such as `vi`.
