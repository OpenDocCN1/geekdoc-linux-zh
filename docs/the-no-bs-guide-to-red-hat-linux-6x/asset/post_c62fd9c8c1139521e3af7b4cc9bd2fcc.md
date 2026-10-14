
gracefully shutting down, so don’t use CTRL-ALT-DELETE on non-Red Hat systems unless you know it’s safe.

## BASH (AND OTHER SHELLS)

Bash, the default Linux shell, is popular and offers lots of advanced features. It combines many of the niceties found in the Bourne shell (the original Unix shell) and other modern shells. But there are alternatives. The Korn shell is popular among many Unix users because it offers a rich scripting (programming) facility. Korn is commercial software, but there is a public-domain (free) version for Linux called pdksh. Another shell that’s popular with C language programmers is the C shell, which exists for Linux as tcsh. The CD that comes with this book provides both pdksh and tcsh, and you can try them out by entering their names at your shell prompt. If you decide to make a permanent switch to something other than the default bash shell, you must log in as root and edit the entry for your user ID in the /etc/passwd file. Entries in the /etc/passwd file look like the following example. Just change “bash” at the end of the line to “pdksh” or “tcsh,” and you’re done. (If you’re not familiar with Linux-based text editors, see Chapter 7, “Text Editors.”)

```
hermie:x:501:1::/home/hermie:/bin/bash
```

Though there are alternatives, I suggest you familiarize yourself with bash’s features first, because bash is the most commonly used Linux shell. In the rest of this chapter, we’ll go over the basics of working in the bash shell, so go ahead and log in as user hermie now and follow right along. It’ll help a lot to enter the commands as you go, experiment with them on your own, and see the actual output.

## LINUX COMMANDS

When you enter a command in Linux, you type a command at a prompt and then press ENTER. Commands can be more than one word—some require switches (which modify the command’s behavior) and/or file names (which tell the command what data to act on). Let's dissect the command shown here:

```
ls -l sample.doc
```

### LINUX COMMANDS ARE CASE SENSITIVE

One of the most important things to remember about entering commands in any Unix environment is that case matters. In DOS, you can type DIR or dir or even DiR and get the same result, but not in Linux. Linux will be quite put out if you type LS instead of ls to list your files. With file names, you have to be even more careful, since nearly identical files (save for capitalization) can exist in the same directory, though they may have completely different contents—Cookie_Recipe and cookie_recipe would appear as distinctly different files to Linux, though they may look pretty much the same to you except for the capital letters.

The best rule to follow is this: Almost everything in Linux is lowercase, so avoid capital letters when naming your files.

### COMMAND PROMPTS CAN VARY

When the Linux shell is ready for a command, you see a command prompt. As in DOS, Linux's command prompts vary. For example, when you log in as root, your default command prompt is the pound (#) sign, but if you log-in as a regular user (like hermie), the prompt changes to a dollar sign ($).

Bash uses the different prompts to clue you in to your user privileges. Pay attention to the prompts so you don't inadvertently wipe out important files while logged in to the root account with superuser privileges, for example.

It's especially important to mind the prompts if you use the su (switch user) command, which allows you to act temporarily as the root user while you're logged in as a regular user. Watch how the prompt changes in the following example. (User input is in boldface.)

```
$ who am i
hermie

$ su - root
Enter password for root: xxxxxxx

# who am i
root
# exit

$ who am i
hermie
```

In this example, entering the command who am i tells you who the system thinks you are—hermie. Then the su - root command switches you to the root user (note the prompt change to the pound sign). The exit command exits the root user account and brings you back to hermie; the prompt changes back to a dollar sign. (See Chapter 6, “Important Linux Commands,” for more information on the su command.)

This example used the prompt and the who am i command to show the logged-in user, but customizing your prompt is a better way to keep track of where you are.

For example, the command

```
PS1="\u \$ "
```

changes the prompt so that it displays the user name (\u), followed by the dollar sign (or pound sign, if you're a superuser). You can use other characters to insert the current time, date, or working directory (\t, \d, and \w, respectively). Here's how to use these various options:

- PS1="\t \$ " Yields 09:15:24 $.
- PS1="\u (\d) \$ " Yields hermie (Wed Nov 4) $.
- PS1="\u (\w) \$ " Yields hermie (/home/hermie) $.

All you're actually doing here is setting the variable PS1 (prompt string number 1) to a special string of characters. The bash shell interprets the value of the PS1 variable each time it's ready to build the prompt string.
