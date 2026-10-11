
![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_339_0.png)

**Figure 1.** *Here you can create a new profile, and optionally base it on an existing one.*

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_339_1.png)

**Figure 2.** *The Edit Profiles dialog allows you to manage multiple profiles.*

Ultimately, the New Profile dialog doesn't do anything terribly interesting. It's the “Editing profile” dialog, shown in **Figure 3**, that holds all the action.

![](img/50a238d93c7edbdc4387d5ff7f6b7b3c_339_2.png)

**Figure 3.** *This dialog contains six tabs of attributes that describe the profile.*

You can also get to the “Editing profile” dialog by selecting Edit | Current Profile, or Edit | Edit Profiles, and then selecting the profile of interest and clicking the Edit button. Or you can right-click in the command window and select Edit Current Profile from the context menu.

On the General tab, the profile icon is the image that displays in the panel when you have a command window running. You probably don’t want to change the font, since the default choice, monospace 12, looks okay and renders fixed-pitch strings nicely. Changing to a proportional font such as Arial can make it nearly impossible to distinguish between certain characters (the lowercase letter “l” and a number “1”, for example).

On the Title and Command tab, you can control what shows up in the title bar. Choices include the name of the profile in various combinations, with the default string of “username, hostname, and current directory.”

## The environment

An environment variable is a value set in the operating system and is available both interactively and to programs. For example, the shell program running in the command window is stored in an environment variable, and you can query it by using the “echo” command. On my system, if I type:

```
echo $SHELL
```

It returns:

```
/bin/bash
```

When I am developing software, I set up several environment variables to provide identification for my software. These variables indicate that the programs are running on a development machine as opposed to running on a user’s computer in production. When my software runs, it looks for those environment variables. If it finds them, certain “developer-only” functionality is available (such as debugging tools). If the software doesn’t find the variables, the software runs as if it’s on a user’s computer. By using environment variables, I can run the software both in development and production modes on the same machine.

Linux has environment variables much like those available in Windows. A number of environment variables are set automatically, and you can set up more yourself.

You can type “env” to see a listing of the system environment variables and type “set” to display all environment variables, shell functions, and aliases. You can also see any other command by using the “echo” command as mentioned earlier. Note that environment variable names are case-sensitive, so while

```
echo $PATH
```

returns

```
/usr/kerberos/bin:/usr/local/bin, etc.
```

the command

```
echo $path
```

returns nothing.

Here are some useful environment variables:

-   **HOME**—The current user’s home directory
-   **HOSTNAME**—The name of the machine
-   **MAIL**—The name of the mail spool
-   **PATH**—The path the system looks in to find commands that the user has entered
-   **SHELL**—The current shell program that is being executed
-   **USER**—The name of the current user

You can set your own environment variables by using a command similar to that used for changing the shell prompt, mentioned earlier in this chapter. For example:

```
PYDEV='whil'
export PYDEV
```

creates the environment variable PYDEV and assigns the value "whil" to it—but only in the current shell. The export command then makes it available to subsequent programs. If you want the environment variable to be created automatically when your computer starts up, put the commands in the ~/.bashrc file along with the "PS1=" command.

## Commands

Time to talk about the commands themselves. There are two groups of commands that can be entered at the command prompt. While the difference should be transparent to the user, once in a while you can run into a problem caused by the difference.

The first type of commands are called “built-ins” (in DOS, they were called “internal”). These commands are part of the shell itself, and they don’t require a separate program file to run. For example, the command “cd” (to change to a different directory) is part of the shell—they aren’t a separate “cd” executable file on your disk somewhere. You can execute a built-in command regardless of how you’re logged in or what directory you’re in.

The second type of commands are external—they require a program to run. Most of the commands you’ll execute at the command prompt are external. The problem has to do with finding those commands, and that brings up the topic of the “path.”

### The Linux path

The “path” is the list of directories that Linux looks in when executing a file. For example, a typical path for a regular user might be:

```
/usr/local/bin:/usr/bin:/bin:/home/whil/bin
```

You can determine your own path by using this command:

```
echo $PATH
```

The “echo” command and the PATH variable are both case-sensitive.

Note that the current working directory (".") is not part of the path. In Windows, you can execute a program where executable file is in the current directory simply by typing the name of the file. This is a security risk, and thus is not default behavior in Linux.

Why is it a security risk? Suppose a user visited a malicious Web site that surreptitiously downloaded a program named “ls” into the user’s home directory. If the current directory was part of the path, the next time the user executed “ls” while in his home directory, the bogus copy of “ls” would be executed instead of the legitimate version in /bin. This behavior is just one more reason why it’s harder to take over a Linux computer than a Windows computer.

As we saw in Chapter 6, “Files, Directory Structures, and File Managers,” the /bin and /usr/bin directories contain hundreds of programs and scripts, and as a result, they’re normally part of every user’s path. However, suppose an installation routine doesn’t put its executable file, script, or symlink in those directories. Those are the times when you type a command at the command prompt and get a “command not found” response. Later in this section, I’ll discuss how to find those programs.

Global path settings are stored in the /etc/profile file. Then you can set individual paths by adding to the existing path. For example, the following command in ~/.bash_profile adds the /bin directory under the user’s home directory to the path:

```
PATH=$PATH:$HOME/bin
```

You can add your own directories to the path as well. For example, suppose you had written some custom programs or scripts (Linux’s version of Windows “batch files”-which I’ll cover later in this chapter). You could create a directory called “/scripts” or “/myprogs” under your home directory, and add that directory to your path like so:

```
PATH=$PATH:$HOME/scripts
```

(Note that each individual file path is separated by a colon.) Now you can execute those programs or scripts no matter where you are, simply by typing the name of the file instead of explicitly identifying the entire path.

## The top 10 useful commands at the command prompt

Okay, maybe more than 10. There are hundreds and hundreds of commands and programs, and it can be overwhelming to sort through them all, much less actually remember any of them. So you don’t have to wade through them. I’ve compiled a list of the commands that a typical power user will find useful on a regular basis. I’ve grouped them into a number of functional areas, together with a “didn’t fit anywhere else” group. I’ve included an example or two of the syntax if the command is used with parameters, or if it has unusual output characteristics.

Some of these commands (such as “locate” and “df”) can produce really long listings. Use Ctrl-C to interrupt the listing.

## Help commands

-   **help**—displays a list of all built-in commands. When the name of a built-in command is used as an argument, a short help topic appears.
    ```
    help
    help echo
    ```

-   **man**—displays the manual page for external commands.
    ```
    man grep
    ```
