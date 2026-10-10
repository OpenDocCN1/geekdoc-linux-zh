
The output from the `ls` command is sent directly to the `sort` command as input, but behind the scenes. You don't see the output from the `ls` command displayed on the monitor; you only see the output from the last command in the pipe line, which in this case is the `sort` command. There's no limit on how many commands you can link together with piping.

![](img/c0a399aca0d18f8822d714ad0a173123_768_0.png)

The `>`, `>>`, and `|` symbols are part of a group of characters often referred to as *metacharacters*. Metacharacters are characters that have special meaning when used in the Linux shell. If you need to use a metacharacter as a standard character (such as using the `>` character to a greater-than symbol in your output instead of as a redirect symbol), you must identify the metacharacter by either placing a backslash in front of it or enclosing the metacharacter in single or double quotes. This method is called *escaping*.

## The Shell Script Format

Placing multiple commands on a single line, by using either the semicolon or piping, is a great way to process data but can still get rather tedious. Each time you want to run the set of commands, you need to type them all at the command prompt.

However, Linux allows us to place multiple commands in a text file and then run the text file as a program from the command line. This is called a *shell script* because we're scripting out commands for the Linux shell to run.

Shell script files are plain-text files. To create a shell script file, you just need to use any text editor that you're comfortable with. If you're working from a KDE-based graphical desktop, you can use the KWrite program, or if you're working from a GNOME-based graphical desktop, you can use the GEdit program.

If you're working directly in a command-line environment, you still have some options. Many Linux distributions include either the `pico` or the `nano` editor to provide a graphical editor environment by using ASCII control characters to create a full-screen editing window.

If your Linux distribution doesn't include either the `pico` or the `nano` editor, there is still one last resort: the `vi` editor. The `vi` editor is a text-based editor that uses simple single-letter commands. It's the oldest text editor in the Linux environment, dating back to the early days of Unix, which may be one reason it's not overly elegant or user-friendly.

Once you've chosen your text editor, you're ready to create your shell scripts. First, for your shell script to work you'll need to follow a specific format for the shell script file. The first line in the file usually specifies the Linux shell required to run the script. This is written in somewhat of an odd format:

```
#!/bin/bash
```

The Linux world calls the combination of the pound sign and the exclamation symbol (`#!`) the *shebang*. It signals to the operating system which shell to use to run the shell script. Most Linux distributions support multiple Linux shells, but the most common is the Bash shell. You can run shell scripts written for other shells as long as those shells are installed on the Linux distribution.

![](img/c0a399aca0d18f8822d714ad0a173123_769_0.png)

If you don't specify the shebang line in your shell script, Linux will run the script using the default shell defined for your user account in the /etc/ passwd file. It's usually recommended to specify a shell, even if it is your default shell, to avoid any confusion or mistakes.

After you specify the shell, you're ready to start listing the commands in your script. You don't need to enter all of the commands on a single line; Linux allows you to place them on separate lines. Also, the Linux shell assumes each line is a new command in the shell script, so you don't need to use semicolons to separate the commands. Listing 25.4 shows an example of a simple shell script file.

### Listing 25.4: A simple shell script file

```
$ cat test1.sh
#!/bin/bash
# This script displays the date and who's logged in
date
who
$ 
```

The test1.sh script file shown in Listing 25.4 starts out with the shebang line identifying the Bash shell, the standard shell in Linux. The second line in the code shown in Listing 25.4 demonstrates another feature in shell scripts. Lines that start with a pound sign are called comment lines. They allow you to embed comments into the shell script program to help you remember what the code is doing. The shell skips comment lines when processing the shell script. You can place comment lines anywhere in your shell script file after the opening shebang line.

![](img/c0a399aca0d18f8822d714ad0a173123_769_1.png)

Notice in Listing 25.4 we used the .sh filename extension on the shell script file. While this is not required in Linux, it's become somewhat of a de facto standard among programmers. This helps identify that the text file is a shell script that can be run at the command line.

## Running the Shell Script

If you just enter a shell script file at the command prompt to run it, you may be a bit disappointed:

```
$ test1.sh
test1.sh: command not found
$ 
```

Unfortunately, the shell doesn't know where to find the **test1.sh** command in the virtual directory. The reason for this is the shell uses a special environment variable called **PATH** to list directories where it looks for commands. If your local **HOME** folder is not included in the **PATH** environment variable list of directories, you can't run the shell script file directly. Instead, you need to use either a relative or an absolute path name to point to the shell script file. The easiest way to do that is by adding the `./` relative path shortcut to the file:

```
$ ./test1.sh
bash: ./test1.sh: Permission denied
$
```

Now the shell can find the program file, but there's still an error message. This time the error is telling us that we don't have permissions to run the shell script file. A quick look at the shell script file using the `ls` command with the `-l` option shows the permissions set for the file:

```
$ ls -l test1.sh
-rw-r--r-- 1 rich rich 73 Feb 24 19:37 test1.sh
$
```

By default, the Linux system didn't give anyone execute permissions to run the file. You can use the `chmod` command to add that permission for the file owner:

```
$ chmod u+x test1.sh
$ ls -l test1.sh
-rwxr--r-- 1 rich rich 73 Feb 24 19:37 test1.sh
$
```

The `u+x` option adds execute privileges to the owner of the file. You should now be able to run the shell script file and see the output:

```
$ ./test1.sh
Thu Feb 24 19:48:27 EST 2022
rich	:0			2022-02-24 19:15 (:0)
$
```

Now that you've seen the basics for creating and running shell scripts, the next sections dive into some more advanced features you can add to make fancier shell scripts.

## Advanced Shell Scripting

The previous section walked you through the basics of how to group normal command-line commands together in a shell script file to run in the Linux shell. We'll add to that by showing more features available in shell scripts to make them look and act more like real programs.

## Displaying Messages

When you string commands together in a shell script file, the output may be somewhat confusing to look at. It would help to be able to customize the output by separating it and adding our own text between the output from each listed command.

The echo command allows you to display text messages from the command line. When used at the command line, it’s not too exciting:

```
$ echo This is a test
This is a test
$ 
```

But now you have the ability to insert messages anywhere in the output from the shell script file. Listing 25.5 demonstrates how this is done.

> Listing 25.5: Using the echo statement in a script

```
$ cat test1.sh
#!/bin/bash
# This script displays the date and who’s logged in
echo The current date and time is:
date

echo "Let’s see who’s logged into the system:"
who
$ ./test1.sh
The current date and time is:
Thu Feb 24 19:55:44 EST 2022

Let’s see who’s logged into the system:
rich      :0     2022-02-24 19:15 (:0)
$ 
```

The shell script shown in Listing 25.5 adds three echo commands to the test1.sh script. Notice that the first echo command doesn’t use any quotes, but the third one does. The reason for that is the text output from the third echo command contains single quotes. The single quote is also a metacharacter in the shell, which will confuse the echo command, so you need to place double quotes around the text. Also notice that the second echo command doesn’t have any text on the line. That outputs a blank line, which is useful when you want to separate output from multiple commands.

## Using Variables

Part of programming is the ability to temporarily store data to use later in the program. You do that by using variables.
