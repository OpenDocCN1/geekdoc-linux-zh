
As you can see, there are actually lots of exported variables in a typical login shell. On the Mac, `export -p` produces a list of 22 variables. Note that in the example shown in our earlier export experimentation, along with other variables that were exported when you logged on and your login shell was started up.

## PS1 and PS2

The sequence of characters that the shell uses as your command prompt are stored in the environment variable PS1. It turns out that you can change this to be anything you want and as soon as you change it, the new value will be used by the shell from that point on.

```
$ echo :$PS1:
$: $
$ PS1="==> "
==> pwd
/users/steve
==> PS1="I await your next command, master: "
I await your next command, master: PS1="$ "
$
```

Back to normal

Your secondary command prompt, used when a command requires more than a single line of input, defaults to `>` and is kept in the variable PS2. This too you can change to your heart’s content:

```
$ echo :$PS2:
:>
$ PS2="=======> "
$ for x in 1 2 3
=======> do
=======> echo $x
=======> done
1
2
3
$
```

Once you log off the system, all the changes will vanish, just like modifications to any other shell variables. If you change PS1, the shell will use the new value for the remainder of your login session. Next time you log in, however, you’ll get the old prompt unless you save the new PS1 value by adding it to your .profile file (discussed later in this chapter).

> **Tip**
>
> The PS1 prompt has a language all its own with special sequences that produce the command count, current directory, time of day, and much more. Learn about it by reading the “Prompting” section of the Bash or Sh man page!

## HOME

Your home directory is where you’re placed whenever you log on to the system. A special shell variable called HOME is also automatically set to this directory when you log on:

```
$ echo $HOME
/users/steve
$
```

This variable can be used by your programs to identify your home directory and is widely used by other programs in Unix for just this purpose. It’s also used by the cd command as the desired destination when you type cd with no arguments:

```
$ pwd                         *Where am I?*
/usr/src/lib/libc/port/stdio
$ cd
$ pwd
/users/steve                  *There’s no place like home*
$
```

You can change your HOME variable to anything you want, but be warned that doing so may affect the operation of any programs that rely on it:

```
$ HOME=/users/steve/book       *Change it*
$ pwd
/users/steve
$ cd
$ pwd                         *See what happened*
/users/steve/book
$
```

You can change your HOME, but you really shouldn’t unless you’re prepared to have a lot of things go wonky rather quickly.

## PATH

Let’s return to the rolo program from Chapter 9:

```
$ rolo Liz
Liz Stachiw     212-775-2298
$
```

To keep things neat and organized, the program was created in steve’s /bin subdirectory, as shown:

```
$ pwd
/users/steve/bin
$
```

Change directory to anywhere else on the system:

```
$ cd                                      *Go home*
$
```

And try to look up Liz in the phone book:

```
$ rolo Liz
sh: rolo: not found
$
```

Uh oh, that’s not good. What happened?

Whenever you type in the name of a program, the shell searches a list of directories until it finds the requested program. When found, the program is started up. This list of directories to search for user commands is stored in a shell variable called PATH and it’s automatically set when you log on. To see what it’s set to at any point, use echo:

```
$ echo $PATH
/bin:/usr/bin:.
$
```

Chances are that your PATH has a somewhat different value, but don’t worry about that—it’s just variations in system configuration. The important thing to notice is that directories are separated by a colon (:) and that the shell searches them in order, left to right, to find requested commands or programs.

In the preceding example, three directories are listed: /bin, /usr/bin, and ., (which, you’ll recall, stands for the current directory). So whenever you type in the name of a program, the shell searches the directories listed in PATH until it finds a matching executable file. Type in rolo and the shell first looks for /bin/rolo, then /usr/bin/rolo, then, finally, ./rolo in the current directory. As soon as it finds a match the shell executes it, but if the shell doesn’t find rolo in any of the directories specified in PATH, it issues a “not found” error.

To have the current directory searched before anything else, put the period at the start of PATH:

```
.:/bin:/usr/bin
```

Warning! For security reasons, it’s not a good idea to have your current directory searched before the system ones.

This is to avoid a Trojan horse attack: Imagine that someone creates their own version of a command like su (which allows you to switch to root or superuser status by prompting for the admin password) in a directory then waits for another user to change to that directory and run the command. If PATH specifies that the current directory be searched first, then the modified version of su will be executed. The problem is, this version prompts for the password, emails it to the malicious user, deletes itself, and prints out an innocuous error message. Reinvoked, password retyped, it all works fine and the administrator account has just been compromised without the user realizing anything has occurred! Sneaky, eh?

The period `.` for specifying the current directory is optional but useful as a visible reminder. For example, a `PATH` of

```
:/bin:/usr/bin
```

is equivalent to the previous one; however, throughout this text we'll specify the current directory with a period for clarity.

Worried about Trojan horses now? Don't fret, you can always override the search specified by `PATH` by specifying an explicit path to the program to be executed. For example, if you type

```
/bin/date
```

the shell goes directly to `/bin` to execute `date`. `PATH` in this case is ignored, as it is if you type in

```
../bin/lu
```

or

```
./rolo
```

This last case says to execute the program rolo in the current directory and is commonly used while developing shell programs because it lets programmers omit `.` from their `PATH`.

Now you understand why you couldn't execute rolo from your home directory: `/users/steve/bin` wasn't included in `PATH` so the shell couldn't find rolo. A simple matter to rectify: You can simply add this directory to `PATH`:

```
$ PATH=/bin:/usr/bin:/users/steve/bin:.
$
```

Now any program in `/users/steve/bin` can be executed regardless of your current directory in the file system:

```
$ pwd
/users/steve
$ rolo Liz
grep: can't open phonebook
$
```

*Where am I?*

Oops. The shell finds rolo and executes it correctly, but the grep command can't find the phonebook data file.

Look more closely at the rolo program and you'll see that the grep error message must be coming from lu. Here's lu, as it exists currently:

```
$ cat /users/steve/bin/lu
#
# Look someone up in the phone book -- version 3
#
    if [ "$#" -ne 1 ]
    then
            echo "Incorrect number of arguments"
            echo "Usage: lu name"
            exit 1

    fi

    grep "$name" phonebook
    $
```

grep is trying to open the phonebook file in the current directory—which is /users/steve—and that's the problem: where the program is being executed from has no relation to the directory in which the program and its data file reside.

PATH only specifies the directories to be searched for programs invoked on the command line, and not for any other types of files. So phonebook must be precisely located for lu to make it more useful.

There are several ways to fix this problem, which also exists with the rem and add programs. One approach is to have the lu program change directory to /users/steve/bin before it invokes grep. That way, grep finds phonebook because it exists in the new current directory:

```
    ...
    cd /users/steve/bin
    grep "$1" phonebook
```

This approach is a good one to take when you’re doing a lot of work with different files in a particular directory. Simply cd to the directory first and then you can directly reference all the files you need.

A second, more common approach is to list a full path to phonebook in the grep command:

```
    grep "$1" /users/steve/bin/phonebook
```

Suppose that you want to let others use your rolo program (and associated lu, add, and rem helper programs). You can give them each their own copy, but then you’ll have several copies on the system and what happens if you make a small change? Are you going to update all their copies as well? Tedious.

A better solution is to have a single copy of rolo but to give other users access to it.

The problem should be obvious at this point: If you change all the references of phonebook to explicitly reference your phone book, everyone else will be using your phone book too. A smarter way to solve the problem is to require that everyone have a phonebook file in their home directory and refer to the file as `$HOME/phonebook`.

To use a very common shell programming convention, define a variable inside rolo called PHONEBOOK and set it to the multi-user friendly value `$HOME/phonebook`. If you export this variable, lu, rem, and add (which are executed as subshells by rolo) can also use the value of PHONEBOOK to reference the individual user’s version of the file.
