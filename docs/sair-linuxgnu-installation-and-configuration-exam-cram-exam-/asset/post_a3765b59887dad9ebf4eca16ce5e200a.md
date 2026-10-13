
## Running in the Background

Linux is a multitasking system. When you don't have additional terminals or virtual consoles available, you can still run multiple programs from a single command line. If you are running a program that takes 10 minutes to finish, you don't have to wait to run other programs.

There are two ways to make your program run in the background. For example, let's assume you have a script named test in your current directory. This script starts an alarm in an hour. You want to run test, but you want to keep working while you wait. To do this, you can run the following command:

```
./test &
```

The ampersand (&) sends program execution to the background, which returns you to the command-line interface.

Alternately, if you're running a program to calculate the value of pi to a large number of digits, such a program might take a while to complete. If you forget to use the ampersand (&), you will need another way to send the program to the background. You can use the following commands to do this:

```
<Ctrl>Z
bg
```

When you press Ctrl+Z, you suspend the program that's currently running in your shell. The bg command then sends the program to the background.

TIP: There are other ways to get to another command-line interface. You can open additional virtual consoles as discussed in Chapter 3. If you're in a graphical user interface window, you can also open as many shell windows as your RAM can handle.

## Special Shell Characters

Special shell characters regulate standard output (stdout). You may already have some special characters assigned to you in your shell. To check, run the stty -a command. An example based on the author's Corel Linux setup is shown in Figure 7.2.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_153_0.png)

Figure 7.2 Typical setup for special shell characters.

> Note: The stty -echo option is a relic of computer input from teletype machines.

You can assign different sets of special characters with the stty command. For example, if you want to suspend a program with Ctrl+X (instead of Ctrl+Z), run the following command:

```
stty susp ^X
```

The carat (^) is used to represent the Ctrl key on the keyboard. You can also change other settings that you see in the output to the stty -a command. For a full list of settings that you can set or suspend, refer to the man page for stty.

> Note: The carat (^) is above the number 6 on a standard U.S. keyboard.

## Wildcards

There are two other special characters in Linux commands, which are variations on the Microsoft concept of "wildcards." The characters are the asterisk (*) and the question mark (?). The asterisk represents any number of numbers or letters. Each question mark represents one alphanumeric character. For example, if you were to run the following command, you'd get a list of all files that start with the letter a:

```
ls a*
```

If you have a file named a, it would be part of this list. In contrast, if you were to run the following command, you'd get a list of all files with two alphanumeric characters starting with a:

```
ls a?
```

If you have a file named a, it would not be a part of this list. You can also perform more complex file searches with commands like the following:

```
ls ?at?
```

This command returns files with names like cate, kata, mate, and so on. It would not return files like Catherine, matador, or cat.

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_154_0.png)

You can use wildcards to apply a command to a number of files. For example, if you were to use the cat b* command, you would see the contents of all files in your directory that start with the letter b. If the text consists of too much data for you to read on your monitor, you can direct the data to a file; the cat b* >> b-files command directs the text of each file that starts with the letter b to the file named b-files. The double arrow (>>) ensures that each file that starts with b gets appended to the end of the b-files file.

You can even define special characters in more detail with brackets ([]). For example, if you want to see all files in your directory between fig07-01.tif and fig07-06.tif, you can run the following command:

```
ls fig07-0[1-6].tif
```

Alternatively, the following command serves the same purpose:

```
ls fig07-0[123456].tif
```

The characters in brackets define the range that you're searching for. This method works just as well with upper- or lowercase letters. For example, if you're searching for all files between fig07-01a.tif and fig07-01g.tif, you can run the following command: `ls fig07-01[a-g].tif` You can also use multiple search terms; for example, the following command searches for all file names between fig07-01a.tif and fig07-06g.tif: `ls fig07-0[1-6][a-g].tif`

## Quotes in the Shell

There are three types of quote characters on your keyboard: the single quote ('), the double quote (") , and the back quote (`). When applied to standard input (stdin), they perform different functions.

*Note: You can find the back quote key above the Tab key on a standard U.S. keyboard.*

The difference between these characters is in how they affect variables, such as $NAME, and shell commands, such as date. With any pair of quotes, the shell sends everything inside the quotes to the command. In the following example, the command echo is used. In detail, the difference is as follows:

- Single quotes—The shell does not process any variables or commands within the quotes.
- Double quotes—The shell processes variables, such as $NAME, but does not process any commands within the quotes.
- Back quotes—The shell tries to process every word in quotes as a command. If there are variables, they are evaluated first, and then processed as a command. Thus, if $NAME were in back quotes, it would be processed, and then the result (Michael) would be evaluated as a command.

You can see how this works in the following examples. Assume $NAME=Michael. Remember, date is a command that returns the current date and time:

```
echo Welcome $NAME, the date is date
echo 'Welcome $NAME, the date is date'
echo "Welcome $NAME, the date is date"
echo "Welcome $NAME, the date is `date`"
```

The first command has no quotes. The second command is surrounded by single quotes. The third command is surrounded by double quotes. The final command has double quotes as well as back quotes around the command date. These commands return the following results:

```
Welcome Michael, the date is date
Welcome $NAME, the date is date
Welcome Michael, the date is date
Welcome Michael, the date is Sat Sep 9 11:16:33 PDT 2000
```

Without quotes, the shell interprets the $NAME variable, but does not run the date command. With single quotes, the shell doesn't interpret variables or commands. With double quotes, the result is similar to the result without quotes. If a command is in back quotes, the shell interprets the command.

> You can take advantage of back quotes. For example, if you want to run a program on several data files that happen to end in .dat, you can run a command like ./majorprogram `cat *.dat`.

## Backslashes

A backslash (\) tells the shell to ignore spaces (or other special characters). You can use it to manage a directory like the My Documents directory on a Microsoft Windows partition. For example, if you mounted your Windows C: drive on the /dos directory, you could list the contents of the My Documents directory with the ls /dos/My\ Documents command. With the backslash, the shell ignores the space and sends the request as stdin to the ls command. Without the backslash, the shell would look for the contents of the /dos/My directory.

You can also use the backslash for special characters, like the question mark (?) or asterisk (*).

> When you use the backslash, you are "escaping" the functionality of the next space or character.

## Aliases

An example of a shell variable is alias. This variable lists the commands that you can substitute for others. One common alias is:

```
alias dir='ls -l'
```

There is no dir command native to Linux. But when you set this alias, you can run the dir command instead of ls -l. However, because any alias is a shell variable, the alias that you set does not apply if you change shells. You can delete an alias with the unalias command. For example, if you set up dir as an alias for ls -l, the unalias dir command removes this link. Some Linux distributions set up several aliases by default on your shell. To check your currently active aliases, type the alias command.

## Navigational Commands

There are two basic navigational commands for getting around the shell. The cd command lets you navigate between directories. The ls command lets you know what's in a directory (including other directories).
