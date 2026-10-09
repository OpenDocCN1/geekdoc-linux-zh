
## Menu Display Logic

A menu is formatted with numbers before each item. For example, a select structure that begins with:

```bash
select fruit in apple banana blueberry kiwi orange watermelon STOP
```

displays the following menu:

```text
1) apple        3) blueberry    5) orange       7) STOP
2) banana       4) kiwi         6) watermelon
```

The select structure uses the values of the LINES (default is 80) and COLUMNS (default is 80) variables to specify the size of the display. With COLUMNS set to 20, the menu looks like this:

```text
1) apple
2) banana
3) blueberry
4) kiwi
5) orange
6) watermelon
7) STOP
```

**PS3** After displaying the menu, select displays the value of **PS3**, the select prompt. The default value of **PS3** is `#`, but it is typically set to a more meaningful value. When you enter a valid number (one in the menu range) in response to the **PS3** prompt, select sets varname to the argument corresponding to the number you entered. An invalid entry causes the shell to set varname to null. Either way, select stores your response in the keyword variable REPLY and then executes the commands between do and done. If you press RETURN without entering a choice, the shell redisplays the menu and the **PS3** prompt.

The select structure continues to issue the **PS3** prompt and execute the commands until something causes it to exit—typically a break or an exit statement. A break statement exits from the loop and an exit statement exits from the script.

### Example Script: fruit2

The following script illustrates the use of select:

```bash
$ cat fruit2
#!/bin/bash
PS3="Choose your favorite fruit from these possibilities: "
select FRUIT in apple banana blueberry kiwi orange watermelon STOP
do
    if [ "$FRUIT" == "" ]; then
        echo -e "Invalid entry.\n"
        continue
    elif [ $FRUIT = STOP ]; then
        echo "Thanks for playing!"
        break
    fi
    echo "You chose $FRUIT as your favorite."
    echo -e "That is choice number $REPLY.\n"
done
```

Executing this script produces the following interaction:

```text
$ ./fruit2
1) apple 2) banana 3) blueberry 4) kiwi 5) orange 6) watermelon 7) STOP
Choose your favorite fruit from these possibilities: 3
You chose blueberry as your favorite.
That is choice number 3.
Choose your favorite fruit from these possibilities: 99
Invalid entry.
Choose your favorite fruit from these possibilities: 7
Thanks for playing!
```

After setting the PS3 prompt and establishing the menu with the select statement, fruit2 executes the commands between do and done. If the user submits an invalid entry, the shell sets varname ($FRUIT) to a null value. If $FRUIT is null, echo displays an error message; continue then causes the shell to redisplay the PS3 prompt. If the entry is valid, the script tests whether the user wants to stop. If so, echo displays an appropriate message and break exits from the select structure (and from the script). If the user enters a valid response and does not want to stop, the script displays the name and number of the user’s response. (See page 1009 for information about the echo -e option.)

# Here Document

A Here document allows you to redirect input to a shell script from within the shell script itself. A Here document is so named because it is here—immediately accessible in the shell script—instead of there, perhaps in another file.

### Example Script: birthday

The following script, named birthday, contains a Here document. The two less than symbols (`<<`) in the first line indicate a Here document follows. One or more characters that delimit the Here document follow the less than symbols—this example uses a plus sign. Whereas the opening delimiter must appear adjacent to the less than symbols, the closing delimiter must be on a line by itself. The shell sends everything between the two delimiters to the process as standard input. In the example, it is as though you have redirected standard input to grep from a file, except that the file is embedded in the shell script:

```bash
$ cat birthday
grep -i "\$1" <<+
Max		June 22
Barbara	February 3
Darlene	May 8
Helen		March 13
Zach		January 23
Nancy		June 26
+

$ ./birthday Zach
Zach		January 23

$ ./birthday june
Max      June 22
Nancy    June 26
```

When you run **birthday**, it lists all the Here document lines that contain the argument you called it with. In this case, the first time **birthday** is run, it displays Zach’s birthday because it is called with an argument of **Zach**. The second run displays all the birthdays in June. The `-i` argument causes **grep**’s search not to be case sensitive.

### Optional: The bundle Script

The next script, named **bundle**, includes a clever use of a Here document. The **bundle** script is an elegant example of a script that creates a shell archive (**shar**) file. The script creates a file that is itself a shell script containing several other files as well as the code needed to re-create the original files:

```bash
$ cat bundle
#!/bin/bash
# bundle: group files into distribution package

echo "# To unbundle, bash this file"
for i
do
    echo "echo $i 1>&2"
    echo "cat >$i <<'End of $i'"
    cat $i
    echo "End of $i"
done
```

Just as the shell does not treat special characters that occur in standard input of a shell script as special, so the shell does not treat the special characters that occur between the delimiters in a Here document as special.

As the following example shows, the output of **bundle** is a shell script, which is redirected to a file named **bothfiles**. It contains the contents of each file given as an argument to **bundle** (**file1** and **file2** in this case) inside a Here document. To extract the original files from **bothfiles**, you simply give it as an argument to a **bash** command. Before each Here document is a **cat** command that causes the Here document to be written to a new file when **bothfiles** is run:

```text
$ cat file1
This is a file.
It contains two lines.
$ cat file2
This is another file.
It contains three lines.
```

The execution output is as follows:

```text
$ ./bundle file1 file2 > bothfiles
$ cat bothfiles
# To unbundle, bash this file
echo file1 1>&2
cat >file1 <<'End of file1'
This is a file.
It contains two lines.
End of file1
echo file2 1>&2
cat >file2 <<'End of file2'
This is another file.
It contains
three lines.
End of file2
```

In the next example, file1 and file2 are removed before bothfiles is run. The bothfiles script echoes the names of the files it creates as it creates them. The ls command then shows that bothfiles has re-created file1 and file2:

```text
$ rm file1 file2
$ bash bothfiles
file1
file2
$ ls
bothfiles
file1
file2
```

# FILE DESCRIPTORS

As discussed on page 334, before a process can read from or write to a file, it must open that file. When a process opens a file, Linux associates a number (called a file descriptor) with the file. A file descriptor is an index into the process's table of open files. Each process has its own set of open files and its own file descriptors. After opening a file, a process reads from and writes to that file by referring to its file descriptor. When it no longer needs the file, the process closes the file, freeing the file descriptor.

A typical Linux process starts with three open files: standard input (file descriptor 0), standard output (file descriptor 1), and standard error (file descriptor 2). Often these are the only files the process needs. Recall that you redirect standard output with the symbol `>` or the symbol `1>` and that you redirect standard error with the symbol `2>`. Although you can redirect other file descriptors, because file descriptors other than 0, 1, and 2 do not have any special conventional meaning, it is rarely useful to do so. The exception is in programs that you write yourself, in which case you control the meaning of the file descriptors and can take advantage of redirection.

## Opening A File Descriptor

The Bourne Again Shell opens files using the **exec** builtin with the following syntax:

```bash
exec n> outfile  
exec m< infile
```

The first line opens `outfile` for output and holds it open, associating it with file descriptor *n*. The second line opens `infile` for input and holds it open, associating it with file descriptor *m*.

## Duplicating A File Descriptor

The `<&` token duplicates an input file descriptor; `>&` duplicates an output file descriptor. You can duplicate a file descriptor by making it refer to the same file as another open file descriptor, such as standard input or output. Use the following syntax to open or redirect file descriptor *n* as a duplicate of file descriptor *m*:

```bash
exec n<&m
```

Once you have opened a file, you can use it for input and output in two ways. First, you can use I/O redirection on any command line, redirecting standard output to a file descriptor with `>&n` or redirecting standard input from a file descriptor with `<&n`. Second, you can use the `read` (page 1041) and `echo` builtins. If you invoke other commands, including functions (page 396), they inherit these open files and file descriptors. When you have finished using a file, you can close it using the following syntax:

```bash
exec n<&-
```

## File Descriptor Examples

When you call the following `mycp` function with two arguments, it copies the file named by the first argument to the file named by the second argument. If you supply only one argument, the script copies the file named by the argument to standard output. If you invoke `mycp` with no arguments, it copies standard input to standard output.

### Note: A function is not a shell script

The `mycp` example is a shell function; it will not work as you expect if you execute it as a shell script. (It will work. The function will be created in a very short-lived subshell, which is of little use.) You can enter this function from the keyboard. If you put the function in a file, you can run it as an argument to the `. ` (dot) builtin (page 332). You can also put the function in a startup file if you want it to be always available (page 397).
