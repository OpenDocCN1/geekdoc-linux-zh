
If the link count is greater than 1, `lnks` goes on to identify the `inode` (page 1254) for `Sfile`. As explained on page 206, comparing the inodes associated with filenames is a good way to determine whether the filenames are links to the same file. The `lnks` script uses `set` to set the positional parameters to the output of `ls`–`i`. The first argument to `set` is the inode number for the file, so the user-created variable named `inode` is assigned the value of `$1`:

```
# Get the inode of the given file
set $(ls -i "$file")
inode=$1
```

Finally `lnks` uses the `find` utility to search for files having inode numbers that match `$inode`:

```
# Find and print the files with that inode number
echo "lnks: using find to search for links..." | x-82
find "$directory" -xdev -inum $inode -print
```

The `find` utility searches the directory hierarchy rooted at the directory specified by its first argument (`$directory`) for files that meet the criteria specified by the remaining arguments. In this example, the remaining arguments send the names of files having inode numbers matching `$inode` to standard output. Because files in different filesystems can have the same inode number yet not be linked, `find` must search only directories in the same filesystem as `$directory`. The `-xdev` (cross-device) argument prevents `find` from searching directories on other filesystems. Refer to page 203 for more information about filesystems and links.

The `echo` command preceding the `find` command in `lnks`, which tells the user that `find` is running, is included because `find` can take a long time to run. Because `lnks` does not include a final exit statement, the exit status of `lnks` is that of the last command it runs, `find`.

## DEBUGGING SHELL SCRIPTS

When you are writing a script such as `lnks`, it is easy to make mistakes. You can use the shell's `-x` option to help debug a script. This option causes the shell to display each command after it expands it but before it runs the command. Tracing a script's execution in this way can give you information about why a problem lies.

You can run `lnks` (above) and cause the shell to display each command before it is executed. Either set the `-x` option for the current shell (`set`–`x`) so all scripts display commands as they are run or use the `-x` option to affect only the shell running the script called by the command line.

```
$ bash -x - lnks_letter /home
+ '[' 2 -eq 0 -o 2 -gt 2 ']'
+ '[' '-d letter ']'
+ file=letter
+ '[' 2 -eq 1 ']'
+ '[' -d /home ']'
+ directory=/home
+ '[' ']' -f letter ']'
...
```

![](img/243613168ac865b539f12460d966088e_1051_0.png)

Figure 27-4 A for...in flowchart

**PS4** Each command the script executes is preceded by the value of the PS4 variable—a plus sign (+) by default—so you can distinguish debugging output from output produced by the script. You must export PS4 if you set it in the shell that calls the script. The next command sets PS4 to `>>>` followed by a SPACE and exports it:

```
$ export PS4='>>> '
```

You can also set the -x option of the shell running the script by putting the following set command near the beginning of the script:

```
set -x
```

You can put set -x anywhere in the script to turn debugging on starting at that location. Turn debugging off using set +x. The set -o xtrace and set +o xtrace commands do the same things as set -x and set +x, respectively.

## for...in

The for...in control structure has the following syntax:

```
for loop-index in argument-list
do
    commands
done
```

The for...in structure (Figure 27-4) assigns the value of the first argument in the argument-list to the loop-index and executes the commands between the do and done statements. The do and done statements mark the beginning and end of the for loop, respectively.

After it passes control to the done statement, the structure assigns the value of the second argument in the argument-list to the loop-index and repeats the commands. It repeats the commands between the do and done statements one time for each argument in the argument-list. When the structure exhausts the argument-list, it passes control to the statement following done.

The following for...in structure assigns apples to the user-created variable fruit and then displays the value of fruit, which is apples. Next the structure assigns oranges to fruit and repeats the process. When it exhausts the argument list, the structure transfers control to the statement following done, which displays a message.

```
$ cat fruit
for fruit in apples oranges pears bananas
do
    echo "$fruit"
done
echo "Task complete."

$ ./fruit
apples
oranges
pears
bananas
Task complete.
```

The next script lists the names of the directory files in the working directory by looping through the files in the working directory and using test to determine which are directory files:

```
$ cat dirfiles
for i in *
do
    if [ -d "$i" ]
    then
        echo "$i"
    fi
done
```

The ambiguous file reference character * matches the names of all files (except hidden files) in the working directory. Prior to executing the for loop, the shell expands the * and uses the resulting list to assign successive values to the index variable i.

## STEP VALUES

As an alternative to explicitly specifying values for argument-list, you can specify step values. A for...in loop that uses step values assigns an initial value to or increments the loop-index, executes the statements within the loop, and tests a termination condition at the end of the loop.

The following example uses brace expansion with a sequence expression (page 406) to generate the argument-list. This syntax works on bash version 4.0 and above; give the command echo $BASH_VERSION to see which version you are using. The first time through the loop, **bash** assigns a value of 0 to **count** (the *loop-index*) and executes the statement between **do** and **done**. At the bottom of the loop, **bash** tests whether the termination condition has been met (is **count>10**)? If it has, **bash** passes control to the statement following **done**; if **not**, **bash** increments **count** by the increment value (**2**) and makes another pass through the loop. It repeats this process until the termination condition is met.

```
$ cat step1
for count in {0..10..2}
do
   echo -n " $count "
done
 echo

$ ./step1
0 2 4 6 8 10
```

Older versions of **bash** do not support sequence expressions; you can use the **seq** utility to perform the same function:

```
$ for count in $(seq 0 2 10); do echo -n "$count "; done; echo
0 2 4 6 8 10
```

The next example uses **bash**'s C-like syntax to specify step values. This syntax gives you more flexibility in specifying the termination condition and the increment value. Using this syntax, the first parameter initializes the *loop-index*, the second parameter specifies the condition to be tested, and the third parameter specifies the increment.

```
$ cat rand
# $RANDOM evaluates to a random value 0 < x < 32,767
# This program simulates 10 rolls of a pair of dice
for (( x=1; x<=10; x++))
do
   echo -n "Roll $#:
   echo -n   $(($RANDOM % 6 + 1))
   echo "    $(($RANDOM % 6 + 1))
done
```

## LE:+ for

The **for** control structure has the following syntax:

```
for loop-index
do
   commands
done
```

In the **for** structure, the *loop-index* takes on the value of each of the command-line arguments, one at a time. The **for** structure is the same as the **for_..in** structure (Figure 27-4, page 995) except in terms of where it gets values for the *loop-index*. The **for** structure performs a sequence of commands, usually involving each argument in turn.

The following shell script shows a **for** structure displaying each command-line argument. The first line of the script, for **arg**, implies for **arg** in "$@", where the shell expands "$@" into a list of quoted command-line arguments (i.e., "$1" "$2" "$3" ...). The balance of the script corresponds to the **for_..in** structure.
