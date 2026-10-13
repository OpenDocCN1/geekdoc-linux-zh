
## 'Round and 'Round She Goes

In this chapter you’ll learn how to set up program loops. These loops will enable you to execute a set of commands either a specified number of times or until a specific end condition is met.

The three built-in looping commands for shell programming are

- `for`
- `while`
- `until`

You’ll learn about each one of these loops in separate sections of this chapter.

### The `for` Command

The `for` command is used to execute one or more commands a specified number of times. Its basic format is as shown:

```sh
for var in word₁ word₂ ... wordₙ
do
        command
        command
        ...
done
```

The commands enclosed between the `do` and the `done` are what’s known as the body of the loop and are executed for as many items as are listed after the `in`. When the loop is executed, the first word, word₁, is assigned to the variable `var`, and the body of the loop is then executed. Next, the second word in the list, word₂, is assigned to `var`, and the body of the loop is executed again.

This process continues with successive words in the list being assigned to `var` and the commands in the loop body being executed until the last word in the list, wordₙ, is assigned to `var` and the body of the loop executed. At that point, no words are left in the list, and execution of the `for` command is then complete. Execution then continues with the command that immediately follows the `done`.

If there are *n* words listed after the `in`, the body of the loop will have been executed a total of *n* times when the loop has finished.

Here’s a loop that will be executed three times:

```sh
for i in 1 2 3
do

        echo $i

done
```

To try it out, type this in directly at the terminal, just like any other shell command:

```sh
$ for i in 1 2 3
> do
>
>        echo $i
>
> done
1
2
3
$
```

While the shell is waiting for the `done` to be typed to complete the `for` command, it keeps showing the secondary command prompt. When the user enters `done`, the shell then proceeds to execute the loop. Because three items are listed after the `in` (1, 2, and 3), the body of the loop—in this case a single `echo` command—will be executed a total of three times.

The first time through the loop, the first value in the list, 1, is assigned to the variable `i`. Then the body of the loop is executed. This displays the value of `i` at the terminal. The next word in the list, 2, is assigned to `i` and the `echo` command re-executed, resulting in the display of 2 at the terminal. The third word in the list, 3, is assigned to `i` for the third time through the loop and the `echo` command is executed. This results in 3 being displayed at the terminal. At that point, no more words are left in the list, so execution of the `for` command is complete, and the shell displays the command prompt to let you know it’s done.

Now let’s back up to Chapter 6 and recall the `run` program that enabled you to run a file through `tbl`, `nroff`, and `lp`:

```sh
$ cat run
tbl $1 | nroff -mm -Tlp | lp
$
```

If you wanted to run the files memo1 through memo4, you could type the following at the terminal:

```sh
$ for file in memo1 memo2 memo3 memo4
> do
>        run $file
> done
request id is laser1-33 (standard input)
request id is laser1-34 (standard input)
request id is laser1-35 (standard input)
request id is laser1-36 (standard input)
$
```

The four values memo1, memo2, memo3, and memo4 will be assigned in turn to the variable `file` and the `run` program will be executed with that value as the argument. Execution will be just as if you typed in four commands:

```sh
$ run memo1
request id is laser1-33 (standard input)
$ run memo2
request id is laser1-34 (standard input)
$ run memo3
request id is laser1-35 (standard input)
$ run memo4
request id is laser1-36 (standard input)
$
```

The shell permits filename substitution in the list of words in the `for` statement, so the previous loop could have also been written this way:

```sh
for file in memo[1-4]
do
        run $file
done
```

If you wanted to print all the files in your current directory using the `run` program, you could type

```sh
for file in *
do
        run $file
done
```

To do something more sophisticated, imagine `filelist` contains a list of the files that you want to run through `run`. You can type

```sh
files=$(cat filelist)

for file in $files
do
        run $file
done
```

to run each of the files, or, more succinctly,

```sh
for file in $(cat filelist)
do
        run $file
done
```

The better way to address this, however, is to actually improve the `run` script itself, and it turns out that the `for` statement is perfect for the job:

```sh
$ cat run
#
# process files through nroff -- version 2
#
for file in $*
do
        tbl $file | nroff -mm -Tlp | lp
done
$
```

Recall that the special shell variable `$*` stands for all the arguments typed on the command line. If you executed the new version of `run` by typing

```sh
run memo1 memo2 memo3 memo4
```

the `$*` in the `for`’s list would be replaced by the four arguments memo1, memo2, memo3, and memo4. Of course, you could also type

```sh
run memo[1-4]
```

to achieve the same results.

### The `$@` Variable

While we’re utilizing `$*`, let’s have a closer look at how it and its cousin `$@` work. To do that, let’s write a program called `args` that displays all the arguments typed on the command line, one per line.

```sh
$ cat args
echo Number of arguments passed is $#

for arg in $*
do
        echo $arg

done
$
```

Now to try it:

```sh
$ args a b c
Number of arguments passed is 3
a
b
c
$ args 'a b' c
Number of arguments passed is 2
a
b
c
$
```

Look closely at the second example: even though `a b` was passed as a single argument to `args`, it was split into two values within the `for` loop. That’s because the `$*` in the `for` command was replaced by the shell with `a b c` and the quotes were lost. Thus the loop was executed three times.

The shell replaces the value of `$*` with `$1, $2, ...`, but if you instead use the special shell variable `"$@"` the values will be passed with `"$1", ...`. The key difference is the double quotes around the `$@`: without them this variable behaves just like `$*`.

Go back to the `args` program and replace the unquoted `$*` with `"$@"`:

```sh
$ cat args
echo Number of arguments passed is $#

for arg in "$@"
do
        echo $arg

done
$
```

Now try it:

```sh
$ args a b c
Number of arguments passed is 3
a
b
c
$ args 'a b' c
Number of arguments passed is 2
a b
c
$ args
Number of arguments passed is 0
$
```

*Try it with no arguments*

In the last case, no arguments were passed to the program so the variable `"$@"` was replaced by *nothing*. The net result is that the body of the loop was not executed at all.

### The `for` Without the List

A special notation is recognized by the shell when writing `for` commands. If you omit the `in` element and its subsequent list

```sh
for var
do
    command
    command
    ...
done
```

the shell automatically sequences through all the arguments typed on the command line, just as if you had written

```sh
for var in "$@"
do
    command
    command
    ...
done
```

With that in mind, here’s the third and last version of the `args` program:

```sh
$ cat args
echo Number of arguments passed is $#

for arg
do
        echo $arg
done
$ args a b c
Number of arguments passed is 3
a
b
c
$ args 'a b' c
Number of arguments passed is 2
a b
c
$
```

### The `while` Command

The second type of looping command is the `while` statement. The format of this command is

```sh
while command_t
do
    command
    command
    ...
done
```

`command_t` is executed and its exit status tested. If it’s zero, the commands enclosed between the `do` and `done` are executed once. Then `command_t` is executed again and its exit status tested.

If it’s zero, the commands enclosed between the `do` and `done` are once again executed. This continues until `command_t` returns a nonzero exit status. At that point, execution of the loop is terminated. Execution then proceeds with the command that follows the `done`.

Note that the commands between the `do` and `done` might never be executed if `command_t` returns a nonzero status the first time it’s executed.

Here’s a program called *while* that simply counts to 5:

```sh
$ cat twhile
i=1

while [ "$i" -le 5 ]
do
        echo $i
        i=$((i + 1))
done
$ twhile                         Run it
1
2
3
4
5
$
```

The variable `i` is initially set to the value 1. Then the `while` loop is entered, succeeding on the conditional test so the code block is executed. The shell continues execution as long as `i` is less than or equal to 5. Inside the loop, the value of `i` is displayed at the terminal, then incremented by one.

The `while` loop is often used in conjunction with the `shift` command to process an unknown number of arguments typed on the command line.

Consider the next program, called `prargs`, which prints each of the command-line arguments out, one per line.

```sh
$ cat prargs
#
# Print command line arguments one per line
#

while [ "$#" -ne 0 ]
do
        echo "$1"
        shift
done
$ prargs a b c
a
b
c
```
