
## Your Environment

When you log on to your system, whether it’s a shiny new Mac OS X Terminal app, a clean Linux install, or a Unix server in the back office, you’re effectively given your own copy of the shell program. This login shell maintains what’s known as your *environment*—a configuration that is distinct from other users on the system. This environment is maintained from the moment you log on until the moment you log off. In this chapter you’ll learn about the shell environment and you’ll see how it relates to writing and running programs.

## Local Variables

Type the following program called `vartest` into your computer:

```sh
$ cat vartest
echo $x:
$
```

`vartest` consists of a single echo command that displays the value of the variable x surrounded by colons.

Assign any value you want to the variable x from your terminal:

```sh
$ x=100
```

Question: What do you think will be displayed when vartest is now executed? Answer:

```sh
$ vartest
::
$
```

`vartest` doesn’t know about the value of x. Therefore, its value is the default: null. The variable x that was assigned the value 100 in the login shell is known as a *local variable*. The reason why it has this name will become clear shortly.

Here’s another example called `vartest2`:

```sh
$ cat vartest2
x=50
echo :$x:
$ x=100
$ vartest2
:50:
$
```

Since the script changed the value of x from 100 to 50, the question is: What’s the value of x after the script completes?

```sh
$ echo $x
100
$
```

You can see that `vartest2` didn’t change the value of x, previously set to 100 in the interactive shell.

## Subshells

The seemingly weird behavior exhibited by `vartest` and `vartest2` is due to the fact that these programs are run within *subshells* by your login shell. A subshell is essentially an entirely new shell just to run the desired program.

When you ask the login shell to execute `vartest`, it starts up a new shell to execute the program. Whenever a new shell runs, it runs in its own environment, with its own set of local variables. A subshell has no knowledge of local variables that were assigned values by the login shell (the *parent* shell). Furthermore, a subshell cannot change the value of a variable in the parent shell, as evidenced by `vartest2`.

Let’s review the process that goes on here so you can better understand what’s called the *scoping* of variables in shell programs: Before executing `vartest2`, your shell has a variable called x that has been assigned the value 100. This is depicted in Figure 10.1.

![](img/29b87b4d3daf7eb41fe5066130730f4c_229_0.png)

Figure 10.1   Login shell with x=100

When you invoke `vartest2`, your shell starts up a subshell to run it, giving it an *empty* list of local variables to start with (see Figure 10.2).

![](img/29b87b4d3daf7eb41fe5066130730f4c_230_0.png)

Figure 10.2  Login shell executes vartest2

After the first command in vartest2 is executed, assigning 50 to the local variable x that exists in the subshell’s environment will have the value 50 (see Figure 10.3) but the value of x in the parent shell will be unchanged.

![](img/29b87b4d3daf7eb41fe5066130730f4c_230_1.png)

Figure 10.3  vartest2 executes x=50

When vartest2 finishes execution, the subshell goes away, together with any variables assigned values by the program.

This is less of a problem than it might seem. You just need to understand that the login shell environment and the environment of subshells and their shell programs are very different.

## Exported Variables

There is a way to make the value of a variable known to a subshell, and that’s by exporting it with the export command. The format of this command is simply

### *export variables*

where *variables* is the list of variable names that you want exported. For any subshells that get executed subsequent to the export command, the value of the exported variables will be passed to the subshell.

Here’s a program called `vartest3` to help illustrate the difference between local and exported variables:

```sh
$ cat vartest3
echo x = $x
echo y = $y
$
```

Assign values to the variables x and y in the login shell, and then run `vartest3`:

```sh
$ x=100
$ y=10
$ vartest3
x =
y =
$
```

x and y are both local variables, so their values aren’t passed down to the subshell that runs `vartest3`. That’s as expected.

But now let’s export the variable y and try the program again:

```sh
$ export y
$ vartest3
x =
y = 10
$
```

*Make y known to subshells*

This time `vartest3` knew about y because it is an exported variable.

Conceptually, whenever a subshell is executed the exported variables get “copied down” to the subshell, whereas the local variables do not (see Figure 10.4).

![](img/29b87b4d3daf7eb41fe5066130730f4c_231_0.png)

Figure 10.4  Execution of `vartest3`

Now it’s time for another question: What do you think happens if a subshell changes the value of an exported variable? That is, will the parent shell know about it after the subshell has finished?

To answer this question, here’s a program called `vartest4`:

```sh
$ cat vartest4
x=50
y=5
$
```

We’ll assume that you haven’t changed the values of x and y, and that y is still exported from the previous example.

```sh
$ vartest4
$ echo $x $y
100 10
$
```

The subshell couldn’t change the value of either the local variable x (no surprise!) or the exported variable y, it merely changed its local subshell copy of y that was instantiated when it was executed (see Figure 10.5). Just as with local variables, when a subshell goes away, so do the values of the exported variables. In fact, once they get to the subshell, they are local variables.

> That’s why this is true: *There is no way to change the value of a variable in a parent shell from within a subshell.*

![](img/29b87b4d3daf7eb41fe5066130730f4c_232_0.png)

Figure 10.5  Execution of `vartest4`

In the case of a shell program invoking another shell program (for example, the rolo program calling the l program), the process is repeated: the exported variables from the subshell are copied to the new subshell. These exported variables may have been exported from the login shell, or newly exported from within the subshell.

> *After a variable is exported, it remains exported to all subshells subsequently executed.*

Consider a modified version of `vartest4`:

```sh
$ cat vartest4
x=50
y=5
z=1
export z
vartest5
$
```

and `vartest5`:

```sh
$ cat vartest5
echo x = $x
echo y = $y
echo z = $z
$
```

When `vartest4` gets executed, the exported variable y will be copied into the subshell’s environment. `vartest4` sets the value of x to 50, changes the value of y to 5, and sets the value of z to 1. Then it exports z which makes the value of z accessible to any subsequent subshell.

`vartest5` is such a subshell and when it is executed the shell copies into its environment the exported variables from `vartest4`: y and z.

This explains the following output:

```sh
$ vartest4
x =
y = 5
z = 1
$
```

This entire process is depicted in Figure 10.6.

![](img/29b87b4d3daf7eb41fe5066130730f4c_234_0.png)

To summarize the way local and exported variables work:

- Any variable that is not exported is a local variable whose existence will not be known to subshells.
- Exported variables and their values are copied into a subshell’s environment, where they may be accessed and changed. However, such changes have no effect on the variables in the parent shell.
- Exported variables retain this characteristic not only for directly spawned subshells, but also for subshells spawned by those subshells (and so on down the line).
- A variable can be exported any time before or after it is assigned a value but takes on its value at the moment of export; subsequent changes aren’t tracked.

### export -p

If you type export -p, you’ll get a list of the variables and their values exported by your shell:

```sh
$ export -p
export LOGNAME=steve
export PATH=/bin:/usr/bin:.
export TIMEOUT=600
export TZ=EST5EDT
export y=10
$
```

另外，这里有一段来自前文的代码示例，它出现在讨论 printf 用途的章节之后：

```text
cat $*
while read number1 number2
do
        printf "%12d %12d\n" $number1 $number2
done
$ cat data
1234 7960
593 -595
395 304
3234 999
-394 -493
$ align data
             1234        7960
              593        -595
              395         304
             3234         999
             -394        -493
$
```

In Chapters 11, 13, and 14 you’ll see more examples of different uses for printf.
