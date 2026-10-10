
## Caution

This example calls `/bin/ls` by specifying its complete path. In most cases, scripts work even if you don’t include the complete path to the programs they call, but it’s good practice to include the complete path, for two reasons. First, doing so minimizes the risk that a script’s behavior could be changed if duplicate programs are added elsewhere in the path. Second, specifying the complete path guarantees the script will work even for users whose paths don’t include the target directory. On the other hand, including the complete path may reduce the portability of the script because the same program may reside in different locations on different systems.

One problem with this approach is that the script won’t pass on any parameters you give it. For instance, if you type `. /lsl a*` and expect to see only files whose names begin with a, you’ll be disappointed—the script drops the a* parameter, so you’ll see all the files. The upcoming section, “Using Command-Line Arguments as Variables,” describes how to work around this limitation.

A script can call more than a single external program. Place each program call on a line by itself and the script will call them all in sequence, waiting for each program call to complete before moving on to the next. If you follow a program call with an ampersand (&), the program launches in the background, just as when you type a program name followed by an ampersand at a shell prompt. For instance, consider Listing 31-2.

### Listing 31-2
A Sample Script to Launch Several Programs

```bash
#!/bin/sh
/usr/X11R6/bin/xtwm&
/usr/X11R6/bin/xclock&
/usr/X11R6/bin/xload&
exit 0
```

This script launches three programs—an xterm window, the xclock program, and the xload program. Because these are X-based programs that you probably want to use concurrently, each one’s name is followed by an ampersand. When you run this script, you’ll see three new windows open on your screen, one for each program called.

## Piping Programs and Redirecting Input and Output

Chapter 5 introduced the use of pipes and redirection in the context of commands typed at a shell prompt. These features work in precisely the same way within a shell script. For instance, suppose you want to create a script that displays the names of all the active network interfaces on a computer. Listing 31-3 accomplishes this goal.

### Listing 31-3
An Example of Piplining in a Script

```bash
#!/bin/sh
ifconfig | grep flags | cut -f1 -d“:”
exit 0
```

**Note**

For readability, Listing 31-3 and most subsequent listings do not provide complete paths to external programs. You can add them if you like; use `whereis`, as in `whereis ifconfig`, to locate these program files.

Listing 31-3 calls three programs in a pipeline. The first, `ifconfig`, displays information on the computer's network interfaces, as described in Chapter 14. This information is too verbose, though. For instance, here's some typical output of `ifconfig`:

```sh
$ ifconfig
  vr0: flags=8843<UP,BROADCAST,RUNNING,SIMPLEX,MULTICAST>  mtu 1500
        inet 192.168.1.6  netmask 0xffffff00  broadcast 192.168.1.255
        ether 00:80:c8:fa:3b:0a
        media: Ethernet autoselect (100baseTX)
        status: active
  lp0: flags=8810<POINTOPOINT,SIMPLEX,MULTICAST>  mtu 1500
  lo0: flags=8049<UP,LOOPBACK,RUNNING,MULTICAST>  mtu 16384
        inet 127.0.0.1  netmask 0xff000000
  ppp0: flags=8010<POINTOPOINT,MULTICAST>  mtu 1500
```

The four interfaces in this example are `vr0`, `lp0`, `lo0`, and `ppp0`, but extracting them and discarding everything else requires trimming the output. The second command, `grep`, searches for the lines that contain interface names. These lines all contain the word `flags`, so that's what `grep` searches for. The third command, `cut`, trims all but the first field of the output. The `-f 1` option tells `cut` to cut everything except the first field, and the `-d " :"` option tells `cut` to use a colon as a field delimiter. Running Listing 31-3 creates output such as this:

```sh
$ ./ifinfo
vr0
lp0
lo0
ppp0
```

Although Listing 31-3 isn't likely to be a critically important program, you might use techniques such as this to generate a list of options for users of the script. Later examples also build upon Listing 31-3 to perform more interesting tasks. You might also want to record this information to a file. To do this, you might use redirection to send the output to a temporary or permanent file. For instance, you might change the second line in Listing 31-3 to this:

```sh
ifconfig | grep flags | cut -f 1 -d " :" > /tmp/if-info.txt
```

You can then examine the output after the script has run, load it into another program, or even read it into another program using the same script that created the file by using input redirection. You can combine these techniques with the use of command-line arguments (described in the upcoming section, “Using Command-Line Arguments as Variables”) to have a script read or write a file that you specify as an argument to the script.

## Using Variables

Variables are an important part of any programming language, and scripting languages are no exception to this rule. Shell script variables are closely related to environment variables, which were introduced in Chapter 6. In fact, you can treat environment variables in shell scripts just like other variables. Conventionally, environment variable names appear entirely in uppercase, whereas script variable names appear in lowercase, or occasionally in mixed case. In a shell script, variables work much as they do at a command shell prompt, but there are certain important extensions when dealing with command-line arguments. It’s common to manipulate variables in a script more than you would at a shell’s command prompt.

### Assigning Values to Variables

Chapter 6 described how to assign values to variables from a shell’s prompt, and the same procedure works in a shell script. The most basic case in a Bourne shell looks like this:

```sh
export color=red
```

This example sets the value of the $color variable to red. The value can be a string, such as red, or a number, such as 12. If the value is a string that includes a space, you should enclose it in quotation marks (“ ”). When you assign a value to a variable, you don’t include a leading dollar sign ($), but you must include this symbol when you subsequently refer to the variable.

In fact, it’s possible—and usually desirable—to do away with the export command entirely because that command is used to export a variable as an environment variable. Thus, the preceding command is better expressed as

```sh
color=red
```

> **Note**
> Do not place a space between the equal sign and either the variable name or its value. If you do, the shell will either try to interpret the variable name as a command or assign a null value to the variable and then try to interpret your intended value as a command.

### Using Command-Line Arguments as Variables

One common use for variables in scripts is to pass command-line arguments to the script. For instance, you might want to pass the name of a file or directory. Consider Listing 31-1 once again. This script displays the contents of the current directory in a long directory listing, but if you type the script name followed by another directory name, the script ignores the directory name you provide. Fortunately, there's a straightforward way to recover parameters passed to a shell script: You can refer to them as numbered variables, from $0 to $9. (You can use the shift command to access parameters beyond the ninth.) $0 is the name of the shell script itself, $1 is the first parameter passed to the script, $2 is the second parameter, and so on. If you need to know how many parameters are passed to a script, the $\# variable holds this information. Listing 31-1 rewritten to pass a single parameter on to its command is shown in Listing 31-4.

![](img/f34d37e3abe9f4517128e54f80ab2616_792_0.png)

```sh
#!/bin/sh
ls -l $1
exit 0
```

There's no need to explicitly define the parameter variable; it's defined implicitly by the shell itself. If this script is called `ls1`, then typing `./ls1` produces a long listing of the current directory, but adding a directory name (such as `./ls1 /tmp`) produces a long listing of the specified directory. One limitation with this approach, at least if the purpose is to pass a file or directory name to the script, is in the handling of wildcards. FreeBSD shells *expand* wildcards—that is, they convert the wildcards into a list of files that may span multiple parameters—before calling the program whose name a user types. Thus, if you type `./ls1 *`, Listing 31-4 receives the name of the first file or directory in the current directory as the value of $1. You can force the issue by enclosing the parameter in quotes. For instance, typing `./ls1 "*"` passes an asterisk (\*) as the value of $1, which is then expanded in the call to `ls` within the script.

You can pass information other than filenames as parameters. For instance, you might create a script that manipulates user information, in which case you might pass a username as a parameter. You could then use a parameter variable such as $1 in place of a username when the script calls account manipulation programs such as `passwd` or `adduser`.

## Displaying and Using Variables

Listing 31-4 illustrates one possible use of variables—you can pass them on to external commands. You can do other things with variables, though. For one thing, as the name implies, variables can change. It's also useful to be able to display the value of a variable, and to set a variable to a value based upon the user's input.

![](img/f34d37e3abe9f4517128e54f80ab2616_792_1.png)
