
```
# "Comment" lines in shell scripts begin with a # character.
# They are not executed by Bash, but exist so that you may
# document your file.

# You can insert blank lines in your file to increase
# readability; Bash will not mind.

# Generate a welcome message when you log in.
figlet 'Good day, $USER!'

# Now run the commands in .bashrc
if [ -f ~/.bashrc ]; then . ~/.bashrc; fi
```

Figure 3-3. A simple .bash_profile.

```
# Alias to make color directory listings the default.
alias ls="ls --color=auto"

# Alias make "l" give a verbose directory listing.
alias l="ls -l"

# Set a custom path.
PATH="/usr/local/bin:/usr/bin:/bin:/usr/bin/X11:~/bin:.

# Set a custom shell prompt.
PS1="[\w] $ "

# Set Vi-style editing mode as the default.
set -o vi

# Make a long history list and history file.
HISTSIZE=20000
HISTFILESIZE=20000

# Check mail every ten minutes.
MAILCHECK=600

# Export the path and prompt variables for all
# variables you define.
export HISTSIZE HISTFILESIZE MAILCHECK PATH PS1
```

Figure 3-4. A simple .bashrc.

There are separate configuration files for login and all other shells so that you can put specific customizations in your `.bash_profile` that only run when you first log in to the system. To avoid having to put commands in both files when you want to run the same ones for all shells, append the following to the end of your `.bash_profile` file:

```
if [ -f ~/.bashrc ]; then . ~/.bashrc; fi
```

This makes Bash run the `.bashrc` file in your home directory when you log in. In this way, you can put *all* of your customizations in your `.bashrc` file, and they will be run *both* at log in and for all subsequent shells. Any customizations before this line in `.bash_profile` run only when you log in.

For example, a simple `.bash_profile` might look like Figure 3-3, and a simple `.bashrc` file, in turn, might look like Figure 3-4.

The `.bash_profile` in Figure 3-3 prints a welcome message with the `figlet` text font tool (see Recipe 16.4.1 [Outputting Horizontal Text Fonts], page 401), and then runs the user's `.bashrc` file.

The `.bashrc` in Figure 3-4 sets a few useful command aliases and uses a custom path and shell prompt whenever a new shell is run.

When you log out, Bash reads and executes the commands in the `.bash_logout` file in your home directory, if it exists. To run commands when you log out, put them in this file.

- ⇒ To clear the screen every time you log out, your `.bash_logout` should contain the following line:

```
clear
```

This executes the `clear` command, which clears the screen of the current terminal.

**NOTES:** Some distributions come with default shell startup files filled with all kinds of interesting things. Debian users might want to look at the example startup files in `/usr/share/doc/bash/examples/startup-files`.

## 3.8 Making a Typescript of a Shell Session

Use `script` to create a typescript, or “capture log,” of a shell session—it writes a verbatim copy of your session to a file, including commands you type and their output. This is useful to record all of your moves when you are doing something big on the system—like installing or upgrading some software, or changing a configuration. As even its manual page notes, programming instructors often request a “script” of students’ moves for compiling and running a program when they turn in assignments.

The first and last lines of the file show the beginning and ending time and date of the capture session. To stop recording the typescript, type exit at a shell prompt. By default, typescripts are saved to a file called typescript in the current directory; specify the file name as an argument.

⇒ To create a typescript of a shell session and save it to the file log.19990525, type:

```
$ script log.19990525 RET
Script started, output file is log.19990525
$ hostname RET
erie
$ apropos bash > bash.commands RET
$ exit RET
exit
Script done, output file is log.19990525
$
```

In this example, the typescript records a shell session consisting of two commands (hostname and apropos) to a file called log.19990525. The typescript looks like Figure 3-5.

```
Script started on Tue May 25 14:21:52 1999
$ hostname
erie
$ apropos bash > bash.commands
$ exit
exit
Script done on Tue May 25 14:22:30 1999
```

Figure 3-5. A typescript of a shell session.

NOTES: You won’t be happy with the output if you record a session with an interactive program such as Emacs or Vi. This is because such programs control the display; all of their screen-manipulating sequences will be saved to the typescript, where they will appear as junk characters to human eyes.

It’s possible, but usually not desirable, to run script from within another script session. This usually happens when you’ve forgotten that you are running it, and you run it again inside the current typescript, even multiple
